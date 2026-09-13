# Scripts do AGENTE DE CRO TRM

No interpretador de código: grave cada bloco em /mnt/data com o nome do arquivo e execute.

=====
### ARQUIVO: scripts/teste_ab.py
=====

```python
#!/usr/bin/env python3
"""Teste A/B de proporções (AGENTE DE CRO TRM).

Amostra necessária por braço:
  python3 teste_ab.py amostra --base 0.02 --melhora 0.20 [--confianca 0.95] [--poder 0.80] [--trafego-dia 1500]
  (--melhora é relativa: 0.20 = +20% sobre a taxa base, o mínimo do critério da casa)

Resultado:
  python3 teste_ab.py resultado --a 40/2000 --b 55/2010 [--confianca 0.95]
  (conversões/visitas do controle A e da variante B)

Teste z de duas proporções, bicaudal. Aplique também o critério da casa (+20% na métrica principal,
sem piora > 10% nas secundárias, mínimo de 100 cliques por braço e 7 dias).
"""
import math, sys

def phi(x): return 0.5 * (1 + math.erf(x / math.sqrt(2)))
def z_of(p):  # inversa da normal por bisseção
    lo, hi = -10.0, 10.0
    for _ in range(100):
        mid = (lo + hi) / 2
        if phi(mid) < p: lo = mid
        else: hi = mid
    return (lo + hi) / 2
def opt(a, k, d=None):
    return a[a.index(k) + 1] if k in a else d

def amostra(a):
    p1 = float(opt(a, "--base")); rel = float(opt(a, "--melhora", 0.20)); p2 = p1 * (1 + rel)
    conf = float(opt(a, "--confianca", 0.95)); pw = float(opt(a, "--poder", 0.80))
    za, zb = z_of(1 - (1 - conf) / 2), z_of(pw); pbar = (p1 + p2) / 2
    n = ((za * math.sqrt(2 * pbar * (1 - pbar)) + zb * math.sqrt(p1 * (1 - p1) + p2 * (1 - p2))) ** 2) / (p2 - p1) ** 2
    n = math.ceil(n)
    print(f"Taxa base {p1:.2%} → alvo {p2:.2%} (+{rel:.0%}) · confiança {conf:.0%} · poder {pw:.0%}")
    print(f"Amostra por braço: {n:,} visitas ({n*2:,} no total) · conversões esperadas no controle: {n*p1:.0f}".replace(",", "."))
    td = opt(a, "--trafego-dia")
    if td:
        dias = math.ceil(n * 2 / float(td)); print(f"Com {float(td):.0f} visitas/dia divididas nos dois braços: ~{dias} dias (mínimo da casa: 7 dias)")
        if dias > 28: print("Aviso: volume insuficiente para esse efeito. Teste uma mudança maior, uma etapa com mais tráfego, ou faça mudança direta com leitura antes e depois (evidência mais fraca).")

def resultado(a):
    ca, na = map(float, opt(a, "--a").split("/")); cb, nb = map(float, opt(a, "--b").split("/"))
    conf = float(opt(a, "--confianca", 0.95))
    pa, pb = ca / na, cb / nb; p = (ca + cb) / (na + nb)
    se = math.sqrt(p * (1 - p) * (1 / na + 1 / nb)); z = (pb - pa) / se if se else 0
    pval = 2 * (1 - phi(abs(z))); lift = (pb - pa) / pa if pa else float("inf")
    se2 = math.sqrt(pa * (1 - pa) / na + pb * (1 - pb) / nb); zc = z_of(1 - (1 - conf) / 2)
    lo, hi = (pb - pa) - zc * se2, (pb - pa) + zc * se2
    print(f"A (controle): {pa:.2%} ({ca:.0f}/{na:.0f}) · B (variante): {pb:.2%} ({cb:.0f}/{nb:.0f})")
    print(f"Diferença relativa: {lift:+.1%} · diferença absoluta: {pb-pa:+.2%} (IC {conf:.0%}: {lo:+.2%} a {hi:+.2%}) · p-valor: {pval:.4f}")
    sig = pval < (1 - conf); casa = lift >= 0.20
    avisos = []
    if min(na, nb) < 100: avisos.append("menos de 100 visitas em um braço (abaixo do mínimo da casa)")
    if min(ca, cb) < 30: avisos.append("menos de 30 conversões em um braço: resultado instável")
    if abs(na - nb) / max(na, nb) > 0.2: avisos.append("braços desequilibrados (>20%): critério de descarte da casa")
    if sig and casa: dec = "Variante vence: critério da casa e significância atendidos (confira as métricas secundárias e os 7 dias)."
    elif casa and not sig: dec = "Promissor, não conclusivo: +20% atingido sem significância. Estender janela ou retestar."
    elif sig and lift < 0: dec = "Controle vence com significância. Manter controle."
    elif sig: dec = "Diferença significativa, mas abaixo de +20%: não atende o critério de vitória da casa. Manter controle ou redesenhar."
    else: dec = "Inconclusivo. Registrar como inconclusivo; não declarar vencedor."
    print("Decisão sugerida:", dec)
    for x in avisos: print("aviso:", x)

def main():
    a = sys.argv[1:]
    if not a or a[0] not in ("amostra", "resultado"): print(__doc__); sys.exit(1)
    (amostra if a[0] == "amostra" else resultado)(a)

if __name__ == "__main__": main()

```

=====
### ARQUIVO: scripts/vazamentos.py
=====

```python
#!/usr/bin/env python3
"""Vazamentos do funil (AGENTE DE CRO TRM).
Uso: python3 vazamentos.py etapas.csv
CSV com colunas: etapa,quantidade[,meta_taxa]
Cada linha é uma etapa em ordem (ex.: cliques, lpv, inicio_vsl, chegou_pitch, clique_cta, inicio_checkout, compra).
meta_taxa (opcional, decimal) é a taxa de passagem desejada DA ETAPA ANTERIOR PARA ESTA, declarada pelo operador.
Saída: taxa de cada passagem, queda, taxa acumulada e vendas adicionais se cada passagem atingisse a meta
(mantendo as demais iguais), ordenado por impacto.
"""
import csv, sys

def main():
    if len(sys.argv) < 2: print(__doc__); sys.exit(1)
    rows = [r for r in csv.DictReader(open(sys.argv[1], encoding="utf-8"))]
    q = [float(r["quantidade"]) for r in rows]; nomes = [r["etapa"] for r in rows]
    if len(q) < 2: sys.exit("Informe pelo menos duas etapas.")
    taxas = [q[i] / q[i-1] if q[i-1] else 0 for i in range(1, len(q))]
    final = q[-1]
    print("| Passagem | De | Para | Taxa | Queda | Acumulada | Meta | Vendas adicionais na meta |\n|---|---|---|---|---|---|---|---|")
    imp = []
    for i, t in enumerate(taxas, 1):
        meta = rows[i].get("meta_taxa", "").strip()
        extra = ""
        if meta:
            m = float(meta)
            if m > t and t > 0:
                ganho = final * (m / t) - final; extra = f"{ganho:.1f}"; imp.append((ganho, f"{nomes[i-1]} → {nomes[i]}"))
            else: extra = "meta já atingida"
        acum = q[i] / q[0] if q[0] else 0
        print(f"| {nomes[i-1]} → {nomes[i]} | {q[i-1]:.0f} | {q[i]:.0f} | {t:.1%} | {1-t:.1%} | {acum:.2%} | {meta and f'{float(meta):.1%}' or '-'} | {extra or '-'} |")
    if imp:
        imp.sort(reverse=True)
        print("\nPrioridade por impacto (vendas adicionais mantendo o resto igual):")
        for g, n in imp: print(f"- {n}: +{g:.1f}")
    else:
        pior = min(range(len(taxas)), key=lambda i: taxas[i])
        print(f"\nSem metas declaradas. Menor taxa de passagem: {nomes[pior]} → {nomes[pior+1]} ({taxas[pior]:.1%}). Declare metas por etapa para priorizar por impacto.")
    print("Queda alta nem sempre é o maior problema: compare com a meta da etapa e confirme a integridade dos dados antes.")

if __name__ == "__main__": main()

```