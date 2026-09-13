# Scripts do AGENTE DE PRODUÇÃO DE CRIATIVOS TRM

No interpretador de código: grave cada bloco em /mnt/data com o nome do arquivo e execute.

=====
### ARQUIVO: scripts/manifesto.py
=====

```python
#!/usr/bin/env python3
"""Manifesto de variações de criativos.
Uso: python3 manifesto.py variacoes.csv [--pasta <exports>] [--saida manifesto.csv]
Entrada mínima (CSV): angulo,hook,formato,persona,versao,proporcao,variavel_da_onda,controle
Opcionais: duracao_s,texto_principal,titulo,cta,url_destino,status_qa,autorizacoes
Saída: manifesto com nome no padrão ÂNGULO__HOOK__FORMATO__PERSONA__VERSÃO e arquivo esperado
(__PROPORÇÃO), mais checagens: códigos fora do padrão, onda mudando mais de uma variável,
ausência de controle, arquivo faltando na pasta, URL sem UTM.
"""
import csv, os, re, sys, unicodedata

def code(x, pref=""):
    x = unicodedata.normalize("NFKD", (x or "").strip()).encode("ascii", "ignore").decode().upper()
    x = re.sub(r"[^A-Z0-9]+", "", x.replace(" ", ""))
    return (pref + x) if pref and not x.startswith(pref) else x

def main():
    a = sys.argv[1:]
    if not a: print(__doc__); sys.exit(1)
    pasta = a[a.index("--pasta")+1] if "--pasta" in a else None
    saida = a[a.index("--saida")+1] if "--saida" in a else os.path.splitext(a[0])[0] + "_manifesto.csv"
    rows = list(csv.DictReader(open(a[0], encoding="utf-8"))); avisos = []
    arquivos = set(os.listdir(pasta)) if pasta and os.path.isdir(pasta) else set()
    for r in rows:
        v = re.sub(r"\D", "", r.get("versao", "1")) or "1"
        nome = "__".join([code(r["angulo"], "ANG_"), code(r["hook"], "HOOK_"), code(r["formato"]), code(r["persona"]), f"V{int(v):02d}"])
        prop = (r.get("proporcao") or "9x16").lower().replace(":", "x")
        r["nome"] = nome; r["arquivo"] = f"{nome}__{prop}"
        if pasta:
            achou = [f for f in arquivos if f.startswith(r["arquivo"])]
            r["arquivo"] = achou[0] if achou else r["arquivo"] + " (FALTANDO)"
            if not achou: avisos.append(f"arquivo faltando: {nome}__{prop}")
        u = r.get("url_destino", "")
        if u and "utm_" not in u: avisos.append(f"{nome}: url_destino sem UTM (ok se as UTMs vão no anúncio)")
    ondas = {}
    for r in rows: ondas.setdefault(r.get("variavel_da_onda", "").strip().lower(), []).append(r)
    if len([k for k in ondas if k]) > 1: avisos.append(f"mais de uma variável no mesmo lote: {', '.join(k for k in ondas if k)}")
    if rows and not any((r.get("controle", "").strip().lower() in ("sim", "s", "1", "true")) for r in rows): avisos.append("nenhuma peça marcada como controle")
    campos = ["nome", "angulo", "hook", "formato", "persona", "versao", "proporcao", "duracao_s", "variavel_da_onda", "controle", "arquivo", "texto_principal", "titulo", "cta", "url_destino", "status_qa", "autorizacoes"]
    with open(saida, "w", newline="", encoding="utf-8") as fh:
        w = csv.DictWriter(fh, fieldnames=campos, extrasaction="ignore"); w.writeheader(); [w.writerow({k: r.get(k, "") for k in campos}) for r in rows]
    print(f"{len(rows)} variações → {saida}")
    for x in avisos: print("aviso:", x)

if __name__ == "__main__": main()

```

=====
### ARQUIVO: scripts/roteiro_para_srt.py
=====

```python
#!/usr/bin/env python3
"""Gera legenda .srt e lista de textos na tela a partir do roteiro CSV.
Uso: python3 roteiro_para_srt.py roteiro.csv [--max-chars 42]
CSV: inicio_s,fim_s,imagem_acao,fala,texto_tela,som,funcao (modelo em assets/roteiro-modelo.csv).
A fala de cada linha é dividida em blocos de até 2 linhas, com tempo proporcional ao tamanho.
Legenda baseada no roteiro: confira contra o áudio final antes de exportar.
"""
import csv, sys, textwrap, os

def ts(s):
    ms = int(round(s * 1000)); h, ms = divmod(ms, 3600000); m, ms = divmod(ms, 60000); sec, ms = divmod(ms, 1000)
    return f"{h:02d}:{m:02d}:{sec:02d},{ms:03d}"

def main():
    a = sys.argv[1:]
    if not a: print(__doc__); sys.exit(1)
    mx = int(a[a.index("--max-chars")+1]) if "--max-chars" in a else 42
    rows = list(csv.DictReader(open(a[0], encoding="utf-8")))
    srt, n, tela, avisos = [], 1, [], []
    for r in rows:
        i, f = float(r["inicio_s"]), float(r["fim_s"]); fala = (r.get("fala") or "").strip()
        if r.get("texto_tela", "").strip(): tela.append(f"{ts(i)} → {ts(f)} · {r['funcao']} · {r['texto_tela'].strip()}")
        if not fala or fala.startswith("["): 
            if fala.startswith("["): avisos.append(f"linha {r['inicio_s']}s: fala não preenchida")
            continue
        linhas = textwrap.wrap(fala, mx); blocos = [linhas[k:k+2] for k in range(0, len(linhas), 2)]
        total = sum(len(" ".join(b)) for b in blocos); t = i
        for b in blocos:
            d = (f - i) * len(" ".join(b)) / total
            srt.append(f"{n}\n{ts(t)} --> {ts(t+d)}\n" + "\n".join(b) + "\n"); n += 1; t += d
            if d < 0.8: avisos.append(f"bloco curto demais ({d:.2f}s) em {r['inicio_s']}s: encurte a fala ou aumente a cena")
    base = os.path.splitext(a[0])[0]
    open(base + ".srt", "w", encoding="utf-8").write("\n".join(srt))
    open(base + "_texto_tela.txt", "w", encoding="utf-8").write("\n".join(tela) + "\n")
    print(f"{n-1} legendas → {base}.srt\n{len(tela)} textos na tela → {base}_texto_tela.txt")
    for x in avisos: print("aviso:", x)

if __name__ == "__main__": main()

```