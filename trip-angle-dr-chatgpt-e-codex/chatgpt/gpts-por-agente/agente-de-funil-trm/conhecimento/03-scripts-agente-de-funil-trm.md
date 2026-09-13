# Scripts do AGENTE DE FUNIL TRM

No interpretador de código: grave cada bloco em /mnt/data com o nome do arquivo e execute.

=====
### ARQUIVO: scripts/checar_funil.py
=====

```python
#!/usr/bin/env python3
"""QA automático de páginas do funil (AGENTE DE FUNIL TRM).
Uso: python3 checar_funil.py <pasta-ou-arquivo.html>
Verifica: campos [..] não preenchidos, viewport mobile, pixel, passagem de UTMs, links de
checkout/próxima etapa, política/termos/contato, legenda/player na VSL, CTAs, sinais de
pressão falsa (timer que reinicia, vagas/compras inventadas) e claims sensíveis para revisão.
Não substitui o teste manual do caminho nem a revisão de compliance.
"""
import os, re, sys
SENS = [r"\bcura\b", r"garantid[oa]", r"perca \d+ ?kg", r"\d+ ?kg em \d+ dias", r"sem dieta", r"sem exerc", r"renda extra garantida", r"fique rico", r"100% natural", r"aprovado pela anvisa", r"médicos odeiam", r"milagr", r"definitiv"]
FAKE = [r"setInterval\([^)]*(timer|count|countdown)", r"localStorage[^;]*(timer|deadline)", r"restam \d+ vagas", r"\d+ pessoas (compraram|estão vendo)", r"acabou de comprar"]

def check(f):
    t = open(f, encoding="utf-8", errors="ignore").read(); low = t.lower(); out = []
    ph = sorted({x for x in re.findall(r"\[[^\]\n]{3,80}\]", t) if re.match(r"\[[A-Z0-9]", x)})
    if ph: out.append(("PENDENTE", f"{len(ph)} campos sem preencher, ex.: {', '.join(ph[:4])}"))
    if 'name="viewport"' not in t: out.append(("ERRO", "sem meta viewport (mobile)"))
    if "fbq(" not in t or "fbq('init'" not in t and 'fbq("init"' not in t: out.append(("ERRO", "pixel base da Meta não instalado (fbq init)"))
    if "trmLink" not in t and "URLSearchParams" not in t: out.append(("ERRO", "sem passagem de UTMs"))
    links = re.findall(r'href="([^"#]+)"', t)
    if not any(("cta" in m or "data-next" in m) for m in re.findall(r"<a[^>]+>", t)) and "destino:" not in t: out.append(("ERRO", "nenhum CTA para próxima etapa ou checkout"))
    for w, lab in [("privacidade", "política de privacidade"), ("termos", "termos de uso"), ("contato", "contato")]:
        if w not in low: out.append(("ERRO", f"sem link de {lab}"))
    if "player" in low and "legenda" not in low: out.append(("AVISO", "página com player sem menção a legenda"))
    ctas = len(re.findall(r'class="cta"', t))
    dests = {l for l in links if "privacidade" not in l.lower() and "termos" not in l.lower() and "contato" not in l.lower()}
    if len(dests) > 2: out.append(("AVISO", f"{len(dests)} destinos diferentes em links: confira se há CTAs concorrentes"))
    for p in FAKE:
        if re.search(p, low): out.append(("BLOQUEIO", f"possível pressão falsa: /{p}/"))
    hits = sorted({m.group(0) for p in SENS for m in re.finditer(p, low)})
    if hits: out.append(("REVISAR", "claims sensíveis para compliance: " + ", ".join(hits)))
    if "publicidade" not in low and "advertorial" in os.path.basename(f).lower(): out.append(("ERRO", "advertorial sem identificação de publicidade"))
    return ctas, out

def main():
    if len(sys.argv) < 2: print(__doc__); sys.exit(1)
    p = sys.argv[1]; files = [p] if p.endswith(".html") else [os.path.join(r, n) for r, _, fs in os.walk(p) for n in fs if n.endswith(".html")]
    bad = 0
    for f in sorted(files):
        ctas, out = check(f); print(f"\n## {os.path.relpath(f, p if os.path.isdir(p) else os.path.dirname(p))} · CTAs: {ctas}")
        if not out: print("OK")
        for lvl, msg in out:
            print(f"- {lvl}: {msg}"); bad += lvl in ("ERRO", "BLOQUEIO")
    print(f"\n{len(files)} página(s) · {bad} erro(s) ou bloqueio(s). Teste manual do caminho continua obrigatório.")
    sys.exit(1 if bad else 0)
if __name__ == "__main__": main()

```