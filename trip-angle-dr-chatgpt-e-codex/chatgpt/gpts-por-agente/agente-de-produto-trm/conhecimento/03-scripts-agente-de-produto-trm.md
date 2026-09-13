# Scripts do AGENTE DE PRODUTO TRM

No interpretador de código: grave cada bloco em /mnt/data com o nome do arquivo e execute.

=====
### ARQUIVO: scripts/montar_ebook.py
=====

```python
#!/usr/bin/env python3
"""Markdown → ebook HTML diagramado e PDF (AGENTE DE PRODUTO TRM).

Uso: python3 montar_ebook.py conteudo.md --titulo "Título" [--subtitulo "..."] [--autor "..."]
     [--cor "#16a34a"] [--fonte "Georgia"] [--saida pasta] [--sem-pdf]
Suporta: # ## ### títulos, parágrafos, **negrito**, *itálico*, listas (-, 1.), - [ ] checklist,
> citações/avisos, tabelas com |, ---pagina--- (quebra de página), imagens ![alt](arquivo).
Gera capa, sumário (a partir dos ##) e PDF A4 via Google Chrome headless, se instalado.
"""
import html, os, re, subprocess, sys

CHROME = ["/Applications/Google Chrome.app/Contents/MacOS/Google Chrome", "google-chrome", "chromium"]

def inline(t):
    t = html.escape(t)
    t = re.sub(r"!\[([^\]]*)\]\(([^)]+)\)", r'<img alt="\1" src="\2">', t)
    t = re.sub(r"\[([^\]]+)\]\(([^)]+)\)", r'<a href="\2">\1</a>', t)
    t = re.sub(r"\*\*(.+?)\*\*", r"<strong>\1</strong>", t)
    return re.sub(r"(?<!\*)\*(?!\*)(.+?)\*", r"<em>\1</em>", t)

def convert(md):
    out, toc, lines, i = [], [], md.split("\n"), 0
    def slug(s): return re.sub(r"[^a-z0-9]+", "-", s.lower()).strip("-")
    while i < len(lines):
        l = lines[i].rstrip()
        if l.strip() == "---pagina---":
            if out and out[-1] != '<div class="pb"></div>': out.append('<div class="pb"></div>')
            i += 1; continue
        m = re.match(r"^(#{1,3})\s+(.*)", l)
        if m:
            n, txt = len(m.group(1)), m.group(2)
            if n == 1 and not out: i += 1; continue  # título já vai na capa
            sid = slug(txt)
            if n == 2: toc.append((sid, txt))
            out.append(f'<h{n} id="{sid}">{inline(txt)}</h{n}>'); i += 1; continue
        if l.startswith("|"):
            rows = []
            while i < len(lines) and lines[i].startswith("|"):
                if not re.match(r"^\|\s*:?-+", lines[i]): rows.append([c.strip() for c in lines[i].strip().strip("|").split("|")])
                i += 1
            if rows:
                h = "".join(f"<th>{inline(c)}</th>" for c in rows[0]); b = "".join("<tr>" + "".join(f"<td>{inline(c)}</td>" for c in r) + "</tr>" for r in rows[1:])
                out.append(f"<table><thead><tr>{h}</tr></thead><tbody>{b}</tbody></table>")
            continue
        if l.startswith(">"):
            buf = []
            while i < len(lines) and lines[i].startswith(">"): buf.append(lines[i][1:].strip()); i += 1
            out.append(f'<div class="aviso">{inline(" ".join(buf))}</div>'); continue
        if re.match(r"^\s*(-|\d+\.)\s+", l):
            ordered = bool(re.match(r"^\s*\d+\.", l)); tag = "ol" if ordered else "ul"; items = []
            while i < len(lines) and re.match(r"^\s*(-|\d+\.)\s+", lines[i]):
                it = re.sub(r"^\s*(-|\d+\.)\s+", "", lines[i])
                if it.startswith("[ ]") or it.startswith("[x]"):
                    items.append(f'<li class="check"><span class="box">{"✓" if it.startswith("[x]") else ""}</span>{inline(it[3:].strip())}</li>')
                else: items.append(f"<li>{inline(it)}</li>")
                i += 1
            out.append(f"<{tag}>{''.join(items)}</{tag}>"); continue
        if not l.strip(): i += 1; continue
        buf = []
        while i < len(lines) and lines[i].strip() and not re.match(r"^(#|\||>|\s*-\s|\s*\d+\.\s|---pagina---)", lines[i]):
            buf.append(lines[i].strip()); i += 1
        out.append(f"<p>{inline(' '.join(buf))}</p>")
    return "\n".join(out), toc

def main():
    a = sys.argv[1:]
    if not a: print(__doc__); sys.exit(1)
    opt = lambda k, d=None: a[a.index(k)+1] if k in a else d
    src = a[0]; md = open(src, encoding="utf-8").read()
    m = re.search(r"^#\s+(.*)", md, re.M)
    titulo = opt("--titulo", m.group(1) if m else "Material"); sub = opt("--subtitulo", ""); autor = opt("--autor", "")
    cor = opt("--cor", "#16a34a"); fonte = opt("--fonte", "Georgia")
    saida = opt("--saida", os.path.dirname(os.path.abspath(src))); os.makedirs(saida, exist_ok=True)
    body, toc = convert(md)
    toc_html = "".join(f'<li><a href="#{s}">{html.escape(t)}</a></li>' for s, t in toc)
    css = f"""@page{{size:A4;margin:22mm 18mm}}body{{font-family:{fonte},serif;font-size:11.5pt;line-height:1.6;color:#1f2328;margin:0}}
h1,h2,h3{{font-family:-apple-system,Segoe UI,Helvetica,Arial,sans-serif;color:{cor};line-height:1.25}}h2{{font-size:20pt;border-bottom:3px solid {cor};padding-bottom:4px;margin-top:0}}h3{{font-size:13.5pt}}
.capa{{height:250mm;display:flex;flex-direction:column;justify-content:center;text-align:center;page-break-after:always}}.capa h1{{font-size:34pt;margin:0 0 12px}}.capa .sub{{font-size:14pt;color:#555}}.capa .autor{{margin-top:40px;color:#777}}
.sumario{{page-break-after:always}}.sumario ol{{font-size:12.5pt}}.sumario a{{color:#1f2328;text-decoration:none}}
.pb{{page-break-after:always}}table{{width:100%;border-collapse:collapse;margin:12px 0;font-size:10pt;page-break-inside:avoid}}th{{background:{cor};color:#fff;text-align:left}}th,td{{border:1px solid #ddd;padding:6px 8px;vertical-align:top}}
.aviso{{border-left:5px solid {cor};background:#f6f8f6;padding:10px 14px;margin:14px 0;font-size:10.5pt}}li.check{{list-style:none;margin-left:-18px}}.box{{display:inline-block;width:13px;height:13px;border:1.5px solid #555;margin-right:8px;vertical-align:-2px;text-align:center;font-size:10px;line-height:12px}}
img{{max-width:100%;page-break-inside:avoid}}h2,h3{{page-break-after:avoid}}"""
    doc = f"""<!doctype html><html lang="pt-BR"><head><meta charset="utf-8"><title>{html.escape(titulo)}</title><style>{css}</style></head><body>
<section class="capa"><h1>{html.escape(titulo)}</h1><div class="sub">{html.escape(sub)}</div><div class="autor">{html.escape(autor)}</div></section>
<section class="sumario"><h2>Sumário</h2><ol>{toc_html}</ol></section>{body}</body></html>"""
    base = os.path.join(saida, re.sub(r"[^a-z0-9]+", "-", titulo.lower()).strip("-") or "ebook")
    open(base + ".html", "w", encoding="utf-8").write(doc); print("HTML:", base + ".html")
    pend = sorted(set(re.findall(r"\[[A-ZÁÉÍÓÚÂÊÔÃÕÇ][^\]\n]{2,60}\]", md)))
    if pend: print(f"aviso: {len(pend)} campos entre colchetes sem preencher, ex.: {', '.join(pend[:3])}")
    if "--sem-pdf" in a: return
    for c in CHROME:
        if os.path.exists(c) or c in ("google-chrome", "chromium"):
            try:
                subprocess.run([c, "--headless", "--disable-gpu", "--no-pdf-header-footer", f"--print-to-pdf={base}.pdf", "file://" + base + ".html"],
                               check=True, capture_output=True, timeout=120); print("PDF:", base + ".pdf"); return
            except Exception: continue
    print("PDF não gerado (Chrome não encontrado). Abra o HTML no navegador e imprima em PDF.")

if __name__ == "__main__": main()

```