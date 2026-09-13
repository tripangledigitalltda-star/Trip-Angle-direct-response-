# Scripts do AGENTE DE ADS TRM

No interpretador de código: grave cada bloco em /mnt/data com o nome do arquivo e execute.

=====
### ARQUIVO: scripts/adlib_extract.js
=====

```javascript
// Extrator de cartões da Biblioteca de Anúncios da Meta (rodar no console da página de resultados).
// Uso: colar inteiro; ajustar SCROLLS. Retorna JSON com total exibido, cartões únicos e agregado por anunciante.
(async () => {
  const SCROLLS = 8;
  for (let i = 0; i < SCROLLS; i++) { window.scrollTo(0, document.body.scrollHeight); await new Promise(r => setTimeout(r, 1500)); }
  const walker = document.createTreeWalker(document.body, NodeFilter.SHOW_TEXT);
  const cards = new Set(); let n;
  while (n = walker.nextNode()) {
    if (n.textContent.trim() === 'Patrocinado') {
      let el = n.parentElement;
      while (el && !/Identificação da biblioteca/.test(el.innerText || '')) el = el.parentElement;
      if (el) cards.add(el);
    }
  }
  const skip = ['Saiba mais', 'Ver resumo', 'Ver detalhes do anúncio', 'Enviar mensagem pelo WhatsApp', 'Ver mais'];
  const list = [];
  for (const c of cards) {
    const t = c.innerText; const lines = t.split('\n').map(s => s.trim()).filter(Boolean);
    const id = (t.match(/Identificação da biblioteca: (\d+)/) || [])[1];
    const start = ((t.match(/Veiculação iniciada em ([^\n·]+)/) || [])[1] || '').trim();
    const num = (t.match(/(\d+) anúncios usam/) || [])[1] || '1';
    const pi = lines.findIndex(l => l === 'Patrocinado'); const page = pi > 0 ? lines[pi - 1] : '';
    const rest = lines.slice(pi + 1).filter(l => !/^\d+:\d\d \/ \d+:\d\d$/.test(l) && !skip.includes(l));
    const dom = rest.find(l => /^[A-Z0-9.\-]+\.[A-Z]{2,}$/.test(l) || l === 'WHATSAPP') || '';
    const a = c.querySelector('a[href*="l.php"]'); let u = '';
    try { u = decodeURIComponent(new URL(a.href).searchParams.get('u')); } catch (e) {}
    const dur = (t.match(/0:00 \/ (\d+:\d\d)/) || [])[1] || '';
    list.push({ id, start, n: num, page, dom, u, dur, body: rest.join(' | ').slice(0, 400) });
  }
  const m = {};
  for (const o of list) {
    const p = o.page || '?';
    const a = m[p] = m[p] || { page: p, ids: new Set(), maxN: 0, sumN: 0, starts: new Set(), bodies: new Set(), doms: new Set(), urls: new Set(), durs: new Set() };
    if (a.ids.has(o.id)) continue; a.ids.add(o.id);
    a.maxN = Math.max(a.maxN, +o.n); a.sumN += +o.n;
    if (o.start) a.starts.add(o.start); if (o.body) a.bodies.add(o.body.slice(0, 240));
    if (o.dom) a.doms.add(o.dom); if (o.u) a.urls.add(o.u.slice(0, 120)); if (o.dur) a.durs.add(o.dur);
  }
  const agg = Object.values(m).map(a => ({ page: a.page, cards: a.ids.size, maxN: a.maxN, sumN: a.sumN, starts: [...a.starts].slice(0, 3), doms: [...a.doms], urls: [...a.urls].slice(0, 3), durs: [...a.durs].slice(0, 4), bodies: [...a.bodies].slice(0, 2) })).sort((x, y) => y.sumN - x.sumN);
  const total = (document.body.innerText.match(/~?[\d.]+ resultados|Nenhum anúncio/) || [])[0];
  const uniq = Object.values(list.reduce((acc, o) => { if (o.id && !acc[o.id]) acc[o.id] = o; return acc; }, {}));
  const out = { capturedAt: new Date().toISOString(), url: location.href, total, cards: uniq.length, agg, cardsList: uniq };
  console.log(JSON.stringify(out));
  return out;
})();

```

=====
### ARQUIVO: scripts/lab_listar.py
=====

```python
#!/usr/bin/env python3
"""Lista itens de uma pasta pública do Google Drive via embeddedfolderview.

Uso: python3 lab_listar.py [ID_DA_PASTA]   (padrão: TRM LAB CRIATIVOS)
Saída: tipo (pasta/arquivo), nome e id de cada item, para descer com o id de uma subpasta.
"""
import html, re, sys, urllib.request

ID = sys.argv[1] if len(sys.argv) > 1 else "1zvNYizDu7PcgIrRgGm7RDsKP-N88-bBK"
url = f"https://drive.google.com/embeddedfolderview?id={ID}"
req = urllib.request.Request(url, headers={"User-Agent": "Mozilla/5.0"})
page = urllib.request.urlopen(req, timeout=30).read().decode("utf-8", "ignore")
items = re.findall(r'id="entry-([\w-]+)".*?href="([^"]+)".*?flip-entry-title">(.*?)</div>', page, re.S)
if not items:
    print("Nenhum item encontrado (pasta privada, vazia ou layout mudou)."); sys.exit(1)
for iid, href, name in items:
    kind = "pasta" if "/folders/" in href else "arquivo"
    print(f"{kind}\t{html.unescape(name).strip()}\t{iid}")
print(f"\n{len(items)} itens em {ID}")

```

=====
### ARQUIVO: scripts/radar_temas.py
=====

```python
#!/usr/bin/env python3
"""Radar de temas: conta expressões recorrentes nos textos dos cartões da Biblioteca.

Uso: python3 radar_temas.py cartoes.json [--min-anunciantes 2] [--hoje AAAA-MM-DD]
Entrada: saída do adlib_extract.js (lista ou objeto com "cartoes"/"cards"); campos usados:
id, page, start, n, dur, body. Opcional: "transcricao" por cartão.
Saída: expressões de 2 a 4 palavras presentes em anunciantes diferentes, com difusão,
recência, soma de contagem e classe sugerida (emergente, em alta, perene), mais um
resumo de durações. É triagem de candidatos: o operador consolida o tema lendo as peças.
"""
import json, re, sys, statistics
from collections import defaultdict
from datetime import date

STOP = set("a o as os de da do das dos e é em um uma para por com sem que se seu sua no na nos nas ao à mais como você voce isso esse essa este esta já ja só so até ate ou the and of to".split())

def days(s, hoje):
    try: y, m, d = map(int, s[:10].split("-")); return (hoje - date(y, m, d)).days
    except Exception: return None

def grams(text):
    w = [x for x in re.findall(r"[a-zà-ú0-9]+", text.lower())]
    out = set()
    for k in (2, 3, 4):
        for i in range(len(w) - k + 1):
            g = w[i:i+k]
            if g[0] in STOP or g[-1] in STOP: continue
            out.add(" ".join(g))
    return out

def main():
    a = sys.argv[1:]
    if not a: print(__doc__); sys.exit(1)
    minadv = int(a[a.index("--min-anunciantes")+1]) if "--min-anunciantes" in a else 2
    hoje = date.fromisoformat(a[a.index("--hoje")+1]) if "--hoje" in a else date.today()
    data = json.load(open(a[0]))
    cards = data if isinstance(data, list) else data.get("cartoes") or data.get("cards") or []
    idx = defaultdict(list); body_key = defaultdict(set)
    for c in cards:
        txt = (c.get("body") or "") + " " + (c.get("transcricao") or "")
        body_key[re.sub(r"\W+", " ", txt.lower()).strip()[:120]].add(c.get("page"))
        for g in grams(txt): idx[g].append(c)
    # clones: texto idêntico conta como um anunciante
    def advertisers(cs):
        seen, n = set(), 0
        for c in cs:
            k = re.sub(r"\W+", " ", ((c.get("body") or "") + " " + (c.get("transcricao") or "")).lower()).strip()[:120]
            if k in seen: continue
            seen.add(k); n += 1
        return n, sorted({c.get("page") for c in cs})
    counts = [int(c.get("n") or 0) for c in cards] or [0]
    med = statistics.median(counts)
    rows = []
    for g, cs in idx.items():
        indep, pages = advertisers(cs)
        if len(pages) < minadv: continue
        ages = [d for d in (days(c.get("start") or "", hoje) for c in cs) if d is not None]
        soma = sum(int(c.get("n") or 0) for c in cs)
        recentes = sum(1 for d in ages if d <= 14)
        cls = []
        if indep >= 3 and ages and max(ages) <= 30 and soma > med: cls.append("em alta")
        if indep >= 2 and ages and recentes > len(ages) / 2: cls.append("emergente")
        if indep >= 2 and sum(1 for d in ages if d > 60) >= 2: cls.append("perene")
        rows.append((indep, soma, g, len(pages), pages, [c.get("id") for c in cs], min(ages) if ages else None, max(ages) if ages else None, "/".join(cls) or "candidato"))
    rows.sort(key=lambda r: (-r[0], -r[1]))
    # remove gramas contidos em outro com os mesmos IDs
    kept = []
    for r in rows:
        if any(r[2] in k[2] and set(r[5]) == set(k[5]) for k in kept): continue
        kept.append(r)
    print(f"Amostra: {len(cards)} cartões · mediana de contagem {med} · data de referência {hoje}")
    print("| Expressão | Anunciantes independentes | Páginas | Soma contagem | Ativo há (min–máx dias) | Classe sugerida | IDs |")
    print("|---|---|---|---|---|---|---|")
    for r in kept[:40]:
        print(f"| {r[2]} | {r[0]} | {r[3]} | {r[1]} | {r[6]}–{r[7]} | {r[8]} | {', '.join(map(str, r[5][:8]))} |")
    durs = defaultdict(int)
    for c in cards:
        d = c.get("dur") or ""
        try:
            m, s = map(int, d.split(":")[:2]); t = m*60+s
            durs["≤15 s" if t <= 15 else "16–60 s" if t <= 60 else "1–5 min" if t <= 300 else ">5 min (VSL?)"] += 1
        except Exception: durs["estático ou sem duração"] += 1
    print("\nDurações:", ", ".join(f"{k}: {v}" for k, v in durs.items()))
    print("Lembrete: expressão recorrente é candidata a tema. Circulação não é performance. Clones contam como um anunciante.")

if __name__ == "__main__": main()

```