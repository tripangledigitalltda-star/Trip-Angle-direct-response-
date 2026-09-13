# Scripts dos agentes TRM

Para usar no interpretador de código: copie o bloco do script, grave em /mnt/data com o nome do arquivo e execute.


=====
### ARQUIVO: agente-central-trm/scripts/projeto.py
=====

```python
#!/usr/bin/env python3
"""AGENTE CENTRAL TRM · estado de projetos.

  listar
  novo <projeto> --oferta "..." [--pais BR] [--nicho "..."]
  status <projeto>
  registrar <projeto> <etapa> <arquivo-handoff.md>
  etapa <projeto> <etapa> <pendente|em andamento|concluida|pulada|manual> [--motivo "..."]
  proxima <projeto> "texto da próxima ação única"

Etapas: espionagem, ads, copy, funil, producao-criativos, compliance, trafego, backend-cro, produto
Pasta: $TRM_PROJETOS ou ~/Desktop/trip-angle-dr/projetos
"""
import json, os, re, sys, shutil
from datetime import datetime

ROOT = os.path.expanduser(os.environ.get("TRM_PROJETOS", "~/Desktop/trip-angle-dr/projetos"))
ETAPAS = ["espionagem", "ads", "copy", "funil", "producao-criativos", "compliance", "trafego", "backend-cro", "produto"]
now = lambda: datetime.now().strftime("%Y-%m-%d %H:%M")

def path(p, *a): return os.path.join(ROOT, p, *a)
def load(p):
    f = path(p, "estado.json")
    if not os.path.exists(f): sys.exit(f"Projeto '{p}' não existe em {ROOT}. Use: novo {p} --oferta ...")
    s = json.load(open(f))
    for e in ETAPAS: s["etapas"].setdefault(e, {"status": "pendente"})
    return s
def opt(a, k, d=None): return a[a.index(k)+1] if k in a else d

def save(s):
    s["atualizado"] = now(); p = s["projeto"]
    json.dump(s, open(path(p, "estado.json"), "w"), ensure_ascii=False, indent=1)
    L = [f"# {p}", f"Oferta: {s['oferta']} · País: {s['pais']} · Nicho: {s['nicho']} · Atualizado: {s['atualizado']}", ""]
    pend = [f"{e}: {v['portao']}" for e, v in s["etapas"].items() if v.get("portao", "").startswith("pendente")]
    if pend: L += ["## Aprovações pendentes"] + [f"- {x}" for x in pend] + [""]
    L += ["## Etapas", "| Etapa | Status | Data | Portão | Último handoff |", "|---|---|---|---|---|"]
    for i, e in enumerate(ETAPAS, 1):
        v = s["etapas"][e]; L.append(f"| {i:02d} {e} | {v['status']} | {v.get('data','')} | {v.get('portao','')} | {v.get('handoff','')} |")
    L += ["", f"## Próxima ação única\n{s.get('proxima','(definir)')}", "", "## Histórico"] + [f"- {h}" for h in s["historico"][-15:]]
    open(path(p, "ESTADO.md"), "w").write("\n".join(L) + "\n")

def field(txt, name):
    m = re.search(rf"^{name}:\s*(.*)$", txt, re.M | re.I); return m.group(1).strip() if m else ""

def main():
    a = sys.argv[1:]
    if not a: print(__doc__); return
    c = a[0]
    if c == "listar":
        os.makedirs(ROOT, exist_ok=True)
        ps = sorted(d for d in os.listdir(ROOT) if os.path.exists(path(d, "estado.json")))
        if not ps: print(f"Nenhum projeto em {ROOT}")
        for d in ps:
            s = load(d); done = sum(v["status"] == "concluida" for v in s["etapas"].values())
            print(f"{d} · {s['oferta']} · {done}/{len(ETAPAS)} etapas · próxima: {s.get('proxima','-')}")
    elif c == "novo":
        p = a[1]
        if not re.fullmatch(r"[a-z0-9-]+", p): sys.exit("Nome do projeto: minúsculas, números e hífens (ex.: br-mounjaro-natural).")
        if os.path.exists(path(p, "estado.json")): sys.exit("Projeto já existe.")
        for i, e in enumerate(ETAPAS, 1): os.makedirs(path(p, f"{i:02d}-{e}"), exist_ok=True)
        os.makedirs(path(p, "handoffs"), exist_ok=True)
        s = {"projeto": p, "oferta": opt(a, "--oferta", ""), "pais": opt(a, "--pais", "BR"), "nicho": opt(a, "--nicho", ""),
             "criado": now(), "etapas": {e: {"status": "pendente"} for e in ETAPAS}, "historico": [f"{now()} projeto criado"],
             "proxima": "Rodar a espionagem ou informar em qual etapa o projeto começa"}
        save(s); print(f"Projeto criado em {path(p)}")
    elif c == "status":
        s = load(a[1]); save(s); print(open(path(a[1], "ESTADO.md")).read())
    elif c == "registrar":
        p, e, f = a[1], a[2], a[3]
        if e not in ETAPAS: sys.exit(f"Etapa inválida. Use: {', '.join(ETAPAS)}")
        s = load(p); txt = open(f).read()
        if "HANDOFF DO PROJETO" not in txt: sys.exit("Arquivo sem bloco HANDOFF DO PROJETO. Etapa não fechada.")
        miss = [k for k in ["Etapa concluída", "Artefatos produzidos", "Portão de aprovação", "Próximo agente", "Próxima ação única"] if not field(txt, k)]
        if miss: sys.exit("Handoff incompleto, faltam: " + ", ".join(miss))
        dest = path(p, "handoffs", f"{datetime.now():%Y%m%d-%H%M}__{e}.md"); shutil.copy(f, dest)
        portao = field(txt, "Portão de aprovação")
        s["etapas"][e] = {"status": "concluida" if not portao.lower().startswith("pendente") else "em andamento",
                          "data": now(), "portao": portao, "handoff": os.path.basename(dest), "agente": field(txt, "Agente")}
        s["proxima"] = field(txt, "Próxima ação única"); s["historico"].append(f"{now()} {e}: handoff registrado · portão: {portao}")
        save(s); print(f"Registrado. Status de {e}: {s['etapas'][e]['status']}. Próxima: {s['proxima']}")
    elif c == "etapa":
        p, e, st = a[1], a[2], a[3]; s = load(p)
        if e not in ETAPAS: sys.exit("Etapa inválida.")
        st = st.replace("concluída", "concluida")
        s["etapas"][e].update(status=st, data=now()); s["historico"].append(f"{now()} {e}: {st} {opt(a,'--motivo','')}".strip())
        save(s); print(f"{e}: {st}")
    elif c == "proxima":
        s = load(a[1]); s["proxima"] = a[2]; s["historico"].append(f"{now()} próxima ação: {a[2]}"); save(s); print("ok")
    else: print(__doc__)

if __name__ == "__main__": main()

```

=====
### ARQUIVO: agente-de-ads-trm/scripts/adlib_extract.js
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
### ARQUIVO: agente-de-ads-trm/scripts/lab_listar.py
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
### ARQUIVO: agente-de-ads-trm/scripts/radar_temas.py
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

=====
### ARQUIVO: agente-de-backend-trm/scripts/economia_backend.py
=====

```python
#!/usr/bin/env python3
"""Economia do backend (AGENTE DE BACKEND TRM).

Uso: python3 economia_backend.py dados.json
     python3 economia_backend.py --exemplo   (gera dados-exemplo.json)
Percentuais em decimal (0.3 = 30%). Valores em reais. Rode cenários: pessimista, base, otimista.
Os números de aceitação, recuperação e reembolso devem ser dados reais ou metas declaradas.
"""
import json, sys

EX = {"moeda": "BRL", "taxa_plataforma": 0.099, "taxa_fixa": 1.0, "imposto": 0.06, "custo_entrega": 0.0,
      "front": {"preco": 37.0},
      "bump": {"preco": 17.0, "aceitacao": {"pessimista": 0.15, "base": 0.25, "otimista": 0.35}},
      "upsell": {"preco": 97.0, "aceitacao": {"pessimista": 0.05, "base": 0.10, "otimista": 0.15}},
      "downsell": {"preco": 47.0, "aceitacao": {"pessimista": 0.05, "base": 0.10, "otimista": 0.15}},
      "reembolso": {"pessimista": 0.12, "base": 0.08, "otimista": 0.05},
      "recuperacao": {"abandono_por_venda": 1.5, "taxa": {"pessimista": 0.05, "base": 0.10, "otimista": 0.15}},
      "_nota": "Exemplo ilustrativo. Substitua por dados reais ou metas declaradas."}

def liq(preco, d): return preco * (1 - d["taxa_plataforma"] - d["imposto"]) - d["taxa_fixa"] if preco else 0.0

def cenario(d, c):
    f = liq(d["front"]["preco"], d)
    b = d.get("bump"); u = d.get("upsell"); w = d.get("downsell")
    vb = b["aceitacao"][c] * liq(b["preco"], d) if b else 0
    vu = u["aceitacao"][c] * liq(u["preco"], d) if u else 0
    vw = (1 - (u["aceitacao"][c] if u else 0)) * w["aceitacao"][c] * liq(w["preco"], d) if w else 0
    bruto_cliente = f + vb + vu + vw
    reemb = d["reembolso"][c] * bruto_cliente
    contrib = bruto_cliente - reemb - d.get("custo_entrega", 0)
    rec = d.get("recuperacao"); vendas_rec = rec["abandono_por_venda"] * rec["taxa"][c] if rec else 0
    return {"front_liquido": f, "bump": vb, "upsell": vu, "downsell": vw, "reembolso": -reemb,
            "contribuicao_por_cliente": contrib, "cpa_equilibrio_so_front": f * (1 - d["reembolso"][c]) - d.get("custo_entrega", 0),
            "cpa_equilibrio_com_backend": contrib, "vendas_recuperadas_por_venda_paga": vendas_rec,
            "contribuicao_por_venda_paga_com_recuperacao": contrib * (1 + vendas_rec)}

def main():
    a = sys.argv[1:]
    if not a: print(__doc__); sys.exit(1)
    if a[0] == "--exemplo":
        json.dump(EX, open("dados-exemplo.json", "w"), ensure_ascii=False, indent=1); print("dados-exemplo.json criado"); return
    d = json.load(open(a[0])); cs = ["pessimista", "base", "otimista"]
    res = {c: cenario(d, c) for c in cs}
    rot = {"front_liquido": "Front líquido", "bump": "+ Bump (esperado)", "upsell": "+ Upsell (esperado)", "downsell": "+ Downsell (esperado)",
           "reembolso": "− Reembolso", "contribuicao_por_cliente": "= Contribuição por cliente", "cpa_equilibrio_so_front": "CPA de equilíbrio só front",
           "cpa_equilibrio_com_backend": "CPA de equilíbrio com backend", "vendas_recuperadas_por_venda_paga": "Vendas recuperadas por venda paga",
           "contribuicao_por_venda_paga_com_recuperacao": "Contribuição por venda paga c/ recuperação"}
    print("| Item | " + " | ".join(cs) + " |\n|---|" + "---|" * len(cs))
    for k, l in rot.items():
        fmt = (lambda v: f"{v:.2f}") if k == "vendas_recuperadas_por_venda_paga" else (lambda v: f"R$ {v:,.2f}".replace(",", "X").replace(".", ",").replace("X", "."))
        print(f"| {l} | " + " | ".join(fmt(res[c][k]) for c in cs) + " |")
    base = res["base"]; lev = {"bump": base["bump"], "upsell": base["upsell"], "downsell": base["downsell"], "reembolso evitado": -base["reembolso"]}
    print(f"\nMaior alavanca no cenário base: {max(lev, key=lev.get)}. Janela de reembolso aberta = contribuição provisória.")
    print("Recuperação entra como venda adicional; o CPA de equilíbrio por venda paga já descontada a mídia continua sendo a contribuição por cliente.")

if __name__ == "__main__": main()

```

=====
### ARQUIVO: agente-de-compliance-trm/scripts/varrer_claims.py
=====

```python
#!/usr/bin/env python3
"""Varredura de claims de risco (AGENTE DE COMPLIANCE TRM).
Uso: python3 varrer_claims.py <pasta-ou-arquivo> [--nicho emagrecimento|saude|renda|relacionamento|beleza|geral]
Lê .txt .md .html .srt .csv .json. Aponta trechos para leitura humana, com categoria e severidade.
Não entende contexto nem imagem: não é parecer. Checa também itens legais em páginas HTML.
"""
import os, re, sys, html as H

R = {  # categoria: [(regex, severidade, motivo)]
 "medicamento": [(r"\b(mounjaro|monjaro|ozempic|wegovy|saxenda|semaglutida|tirzepatida|liraglutida|sibutramina|victoza)\b", "VERMELHO", "nome de medicamento de prescrição"),
                 (r"\b(canetinha|caneta emagrecedora|m0unj|0zemp)", "VERMELHO", "alusão a medicamento ou grafia ofuscada"),
                 (r"substitu\w* (o |seu )?(remédio|rem[eé]dio|medicamento|tratamento)", "VERMELHO", "sugere substituir tratamento")],
 "saude": [(r"\b(cura|curar|reverte|reverter|trata\b|tratamento de)\b", "VERMELHO", "alegação terapêutica"),
           (r"\b(diabetes|hipertens|press[aã]o alta|colesterol|c[aâ]ncer|tireoide|ansiedade|depress[aã]o)\b", "AMARELO", "condição de saúde citada: checar alegação e atributo pessoal"),
           (r"aprovado pela anvisa|sem efeitos? colaterais|100% natural|cientificamente comprovado", "VERMELHO", "alegação absoluta ou regulatória sem prova"),
           (r"\bdetox\b|elimina toxinas|queima gordura|derret\w+ (a )?gordura|acelera (o )?metabolismo|barriga negativa", "AMARELO", "alegação fisiológica: exige prova")],
 "resultado": [(r"\d+\s?kg (em|por) \d+\s?(dias|semanas|dia)", "VERMELHO", "resultado com prazo"),
               (r"perca \d+|perder \d+\s?kg|perdi \d+\s?kg|eliminei \d+", "VERMELHO", "resultado numérico de peso"),
               (r"sem dieta|sem exerc[ií]cio|sem academia|sem esfor[cç]o|dormindo", "AMARELO", "resultado sem esforço"),
               (r"garantid[oa]s?|100% (eficaz|garantido)|resultado certo|funciona para todos", "VERMELHO", "resultado garantido"),
               (r"rejuvene\w+ \d+ anos|milagr\w*|definitiv\w*|para sempre|nunca mais", "AMARELO", "promessa absoluta")],
 "renda": [(r"(ganhe|fature|lucre|renda de)\s*r?\$?\s?\d", "VERMELHO", "renda com valor"),
           (r"renda (extra )?garantida|fique rico|dinheiro f[aá]cil|liberdade financeira garantida|trabalhe (apenas |só )?\d+\s?h", "VERMELHO", "promessa de renda"),
           (r"sem precisar (trabalhar|vender|aparecer)", "AMARELO", "renda sem esforço")],
 "atributo_pessoal": [(r"\bvoc[eê] (est[aá]|é|tem|sofre)\b[^.?!\n]{0,40}(peso|gord|obes|diab|d[ií]vid|sozinh|ansios|depress|doen)", "VERMELHO", "atributo pessoal na segunda pessoa"),
                      (r"\bseu (diabetes|peso|excesso de peso|problema de|casamento est[aá] acabando|nome sujo)", "VERMELHO", "atributo pessoal")],
 "autoridade": [(r"\b(harvard|stanford|nobel|nasa|oms|minist[eé]rio da sa[uú]de)\b", "AMARELO", "autoridade externa: exige fonte real e pertinente"),
                (r"m[eé]dic[oa]s? (revela|descobre|odeiam|confirma)|estudo (comprova|revela)|cientistas descobriram", "AMARELO", "autoridade ou estudo não verificável")],
 "urgencia": [(r"(restam|últimas|ultimas) \d+ vagas|s[oó] hoje|[uú]ltimas unidades|acaba em \d+ minutos", "AMARELO", "urgência: exige prova de limite real"),
              (r"setinterval\([^)]*(timer|count|countdown)|localstorage[^;]*(timer|deadline)", "VERMELHO", "timer possivelmente falso"),
              (r"\d+ pessoas (compraram|est[aã]o vendo)|acabou de comprar", "VERMELHO", "prova social dinâmica possivelmente falsa")],
 "espiritualidade": [(r"(ora[cç][aã]o|simpatia|ritual|feiti[cç]o)[^.\n]{0,40}(dinheiro|rico|voltar|amarra)", "VERMELHO", "promessa material por prática espiritual"),
                     (r"maldi[cç][aã]o|olho gordo|trabalho feito", "AMARELO", "exploração de medo ou superstição")],
 "antes_depois": [(r"antes e depois|antes/depois|before.?after", "VERMELHO", "antes e depois")],
}
NICHO = {"emagrecimento": ["medicamento", "saude", "resultado", "atributo_pessoal", "autoridade", "urgencia", "antes_depois"],
         "saude": ["medicamento", "saude", "resultado", "atributo_pessoal", "autoridade", "urgencia", "antes_depois"],
         "renda": ["renda", "resultado", "atributo_pessoal", "autoridade", "urgencia"],
         "relacionamento": ["espiritualidade", "resultado", "atributo_pessoal", "urgencia"],
         "beleza": ["saude", "resultado", "atributo_pessoal", "autoridade", "urgencia", "antes_depois"]}
EXT = (".txt", ".md", ".html", ".htm", ".srt", ".csv", ".json")

def text_of(f):
    t = open(f, encoding="utf-8", errors="ignore").read()
    if f.endswith((".html", ".htm")):
        scripts = " ".join(re.findall(r"<script[^>]*>(.*?)</script>", t, re.S | re.I))
        body = re.sub(r"<(script|style)[^>]*>.*?</\1>", " ", t, flags=re.S | re.I)
        body = H.unescape(re.sub(r"<[^>]+>", "\n", body))
        return body + "\n" + scripts, t
    return t, None

def legal(raw):
    low = raw.lower(); out = []
    checks = [(r"\b\d{2}\.?\d{3}\.?\d{3}/?\d{4}-?\d{2}\b|cnpj", "CNPJ ou identificação do fornecedor (Decreto 7.962/2013)"),
              (r"privacidade", "política de privacidade (LGPD)"), (r"termos", "termos de uso"), (r"contato|atendimento|suporte", "canal de atendimento"),
              (r"arrependimento|7 dias|sete dias", "direito de arrependimento (CDC art. 49)")]
    for rx, lab in checks:
        if not re.search(rx, low): out.append(("AMARELO", "legal", f"não encontrado: {lab}"))
    if "advertorial" in low or "matéria" in low:
        if "publicidade" not in low and "patrocinado" not in low: out.append(("VERMELHO", "legal", "advertorial sem rótulo de publicidade (CDC art. 36)"))
    return out

def main():
    a = sys.argv[1:]
    if not a: print(__doc__); sys.exit(1)
    nicho = a[a.index("--nicho")+1] if "--nicho" in a else "geral"
    cats = NICHO.get(nicho, list(R.keys()))
    p = a[0]; files = [p] if os.path.isfile(p) else sorted(os.path.join(r, n) for r, _, fs in os.walk(p) for n in fs if n.lower().endswith(EXT))
    tot = {"VERMELHO": 0, "AMARELO": 0}
    for f in files:
        txt, raw = text_of(f); hits = []
        for i, line in enumerate(txt.split("\n"), 1):
            l = line.lower()
            for c in cats:
                for rx, sev, why in R[c]:
                    for m in re.finditer(rx, l):
                        s = max(0, m.start() - 40); hits.append((sev, c, why, i, line[s:m.end() + 40].strip()))
        if raw: hits += [(sev, c, why, "-", "") for sev, c, why in legal(raw)]
        print(f"\n## {f}")
        if not hits: print("sem padrões de risco encontrados (ler a peça mesmo assim)"); continue
        print("| Severidade | Categoria | Motivo | Linha | Trecho |\n|---|---|---|---|---|")
        seen = set()
        for h in sorted(hits, key=lambda x: (x[0] != "VERMELHO", x[1])):
            k = (h[0], h[2], h[4]);
            if k in seen: continue
            seen.add(k); tot[h[0]] += 1
            print(f"| {h[0]} | {h[1]} | {h[2]} | {h[3]} | {h[4][:110].replace('|','/')} |")
    print(f"\n{len(files)} arquivo(s) · {tot['VERMELHO']} vermelho(s) · {tot['AMARELO']} amarelo(s) · nicho: {nicho}")
    print("Varredura não é parecer: leia cada peça inteira, inclusive imagens e sequência.")

if __name__ == "__main__": main()

```

=====
### ARQUIVO: agente-de-cro-trm/scripts/teste_ab.py
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
### ARQUIVO: agente-de-cro-trm/scripts/vazamentos.py
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

=====
### ARQUIVO: agente-de-espionagem-trm/scripts/adlib_extract.js
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
### ARQUIVO: agente-de-espionagem-trm/scripts/pretriagem.py
=====

```python
#!/usr/bin/env python3
"""Pré-triagem heurística de cartões extraídos da Biblioteca de Anúncios.

Uso: python3 pretriagem.py cartoes.json [--md]
Entrada: JSON com lista de cartões (ou objeto com chave "cartoes"/"cards"), cada um com
id, page, start, n, dur, dom, u, body (saída do adlib_extract.js).
Saída: tabela com uma sugestão de rota por cartão e famílias de texto idêntico.

A pré-triagem NÃO decide. Ela ordena o trabalho e aponta descartes prováveis por padrão
de destino; a decisão final exige abrir o destino (skill, seções 4 e 5).
"""
import json, re, sys
from collections import defaultdict
from datetime import date

CHECKOUT = ("pay.hotmart", "hotmart.com", "kiwify", "cakto", "wiapy", "perfectpay", "lastlink",
            "cartpanda", "monetizze", "eduzz", "braip", "ticto", "greenn", "kirvano", "payt.", "pepper.")
SOCIAL = ("instagram.com", "facebook.com", "tiktok.com", "youtube.com", "youtu.be", "t.me", "linktr.ee")
APPSTORE = ("apps.apple.com", "play.google.com")
SPA = ("lovable.app", "vercel.app", "netlify.app", "xpages", "framer.app", "webflow.io")
ECOM_URL = (".shop", "/produto", "/product", "/collections", "/carrinho", "/cart", "myshopify", "nuvemshop", "lojaintegrada")
ECOM_TXT = ("frete", "compre 3", "leve 4", "cupom", "off só hoje", "kit com", "entrega para todo")
WPP_TXT = ("whatsapp", "agende", "avaliação gratuita", "chame no")
LEAD_TXT = ("inscreva", "cadastre", "gratuito", "vagas", "aplicação", "preencha")

def route(c):
    u = (c.get("u") or "").lower(); dom = (c.get("dom") or "").lower(); body = (c.get("body") or "").lower()
    target = u or dom
    flags = []
    if not target and any(k in body for k in WPP_TXT):
        return "E3? WhatsApp direto / local", ["sem URL exposta"]
    if not target:
        return "abrir (sem URL no cartão; ver 'Ver resumo' ou modal por ID)", []
    if any(k in target for k in SOCIAL): return "E4? perfil social ou conteúdo", []
    if any(k in target for k in APPSTORE): return "E5? loja de app", []
    if any(k in target for k in CHECKOUT): return "abrir: checkout direto (oferta pode estar observável no checkout)", []
    if any(k in target for k in ECOM_URL) or sum(k in body for k in ECOM_TXT) >= 2:
        return "abrir: possível E1 e-commerce de catálogo (confirmar se há VSL/página longa: pode ser DR físico)", []
    if "quiz" in target: return "abrir: quiz (percorrer com quiz_walker.js até a oferta)", []
    if any(k in target for k in SPA): flags.append("SPA de funil: abrir no navegador, fetch não funciona")
    if any(k in body for k in LEAD_TXT): flags.append("possível captura/aplicação/lançamento: oferta pode não estar na sessão")
    try:
        d = c.get("dur") or ""
        m, s = d.split(":")[:2] if ":" in d else (0, 0)
        if int(m) >= 5: flags.append("vídeo longo: candidato a VSL")
    except Exception: pass
    return "abrir: página/VSL", flags

def age_days(start):
    try:
        y, m, d = [int(x) for x in start[:10].split("-")]; return (date.today() - date(y, m, d)).days
    except Exception: return None

def main():
    if len(sys.argv) < 2: print(__doc__); sys.exit(1)
    data = json.load(open(sys.argv[1]))
    cards = data if isinstance(data, list) else data.get("cartoes") or data.get("cards") or []
    fam = defaultdict(list)
    rows = []
    for c in cards:
        key = re.sub(r"\W+", " ", (c.get("body") or "").lower()).strip()[:120]
        if key: fam[key].append(c)
        r, flags = route(c)
        a = age_days(c.get("start") or "")
        rows.append((str(c.get("id")), c.get("page", ""), str(c.get("n", "")), f"{a}d" if a is not None else "?", c.get("dom") or "(sem URL)", r, "; ".join(flags)))
    print("| ID | Anunciante | N criativos | Ativo há | Destino | Rota sugerida | Observações |")
    print("|---|---|---|---|---|---|---|")
    for r in rows: print("| " + " | ".join(r) + " |")
    clones = {k: v for k, v in fam.items() if len({x.get('page') for x in v}) > 1}
    print("\nFamílias com texto idêntico em anunciantes diferentes (candidatas a clone; PADRÃO IDENTIFICADO, não vínculo):")
    if not clones: print("- nenhuma")
    for k, v in clones.items():
        print(f"- IDs {', '.join(str(x.get('id')) for x in v)} | anunciantes: {', '.join(sorted({x.get('page','') for x in v}))} | texto: \"{k[:70]}…\"")
    print("\nLembrete: rota sugerida não é decisão. Abra cada destino antes de qualificar, observar ou excluir.")

if __name__ == "__main__": main()

```

=====
### ARQUIVO: agente-de-espionagem-trm/scripts/quiz_walker.js
=====

```javascript
// Percorre um quiz de funil clicando a primeira opção de cada tela e "Continuar" quando existir.
// Para antes de botões de compra/checkout e de links externos. Retorna o texto de cada tela e a URL final.
// Uso: colar no console; rodar de novo se a tela travar (telas com imagem-botão precisam de clique manual).
(async () => {
  const BUDGET_MS = 36000, MAX_STEPS = 20;
  const vis = e => e.offsetParent !== null;
  const steps = []; const t0 = Date.now();
  for (let i = 0; i < MAX_STEPS && Date.now() - t0 < BUDGET_MS; i++) {
    await new Promise(r => setTimeout(r, 1300));
    const root = document.body;
    steps.push(root.innerText.replace(/\n{2,}/g, '\n').trim().slice(0, 900));
    let btns = [...root.querySelectorAll('button,[role=button],a')].filter(b => vis(b) && b.innerText.trim().length > 1 && !/voltar|back/i.test(b.innerText));
    if (!btns.length) btns = [...root.querySelectorAll('div,label,span,p')].filter(b => vis(b) && getComputedStyle(b).cursor === 'pointer' && b.innerText.trim().length > 1 && b.innerText.trim().length < 60);
    if (!btns.length) { steps.push('NO-BTN (clique manual necessário)'); break; }
    const buy = btns.find(b => /comprar|garantir|checkout|pagar|finalizar|adquirir/i.test(b.innerText) || (b.href && /^http/.test(b.href) && !b.href.includes(location.host)));
    if (buy) { steps.push('CTA-> ' + buy.innerText.trim().slice(0, 80) + ' href=' + (buy.href || '')); break; }
    const opt = btns.find(b => !/^(continuar|próximo|avançar|prosseguir)/i.test(b.innerText.trim())) || btns[0];
    steps.push('CLICK: ' + opt.innerText.trim().slice(0, 40));
    opt.click();
    await new Promise(r => setTimeout(r, 700));
    const cont = [...document.body.querySelectorAll('button,[role=button]')].find(b => vis(b) && /^(continuar|próximo|avançar|prosseguir)/i.test(b.innerText.trim()));
    if (cont) cont.click();
  }
  const out = { url: location.href, steps };
  console.log(JSON.stringify(out));
  return out;
})();

```

=====
### ARQUIVO: agente-de-funil-trm/scripts/checar_funil.py
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

=====
### ARQUIVO: agente-de-producao-de-criativos-trm/scripts/manifesto.py
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
### ARQUIVO: agente-de-producao-de-criativos-trm/scripts/roteiro_para_srt.py
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

=====
### ARQUIVO: agente-de-produto-trm/scripts/montar_ebook.py
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

=====
### ARQUIVO: agente-de-trafego-trm/scripts/meta_ads.py
=====

```python
#!/usr/bin/env python3
"""AGENTE DE TRÁFEGO TRM · cliente mínimo da Meta Marketing API (só biblioteca padrão).

Comandos:
  validar  plano.json                       confere estrutura, nomes, UTMs, orçamento e força PAUSED
  subir    plano.json [--executar]          cria campanha, conjuntos, criativos e anúncios PAUSADOS
                                            (sem --executar só imprime as chamadas: dry-run)
  insights <id> [--periodo last_7d] [--nivel campaign|adset|ad]
  ativar   <id> --confirmado-pelo-operador  muda status para ACTIVE (só após "sim" explícito no chat)
  pausar   <id>                             muda status para PAUSED

Credenciais só por variável de ambiente, definidas pelo operador no próprio terminal:
  META_ACCESS_TOKEN (obrigatória) · META_API_VERSION (padrão v23.0; confirme a versão vigente
  no changelog da Graph API) · META_AD_ACCOUNT_ID (act_...; pode vir no plano)
O token nunca é impresso nem gravado em arquivo.
"""
import json, os, sys, urllib.parse, urllib.request, urllib.error

VER = os.environ.get("META_API_VERSION", "v23.0")
BASE = f"https://graph.facebook.com/{VER}"
OBJ = {"OUTCOME_SALES", "OUTCOME_LEADS", "OUTCOME_TRAFFIC", "OUTCOME_ENGAGEMENT", "OUTCOME_AWARENESS", "OUTCOME_APP_PROMOTION"}

def token():
    t = os.environ.get("META_ACCESS_TOKEN")
    if not t: sys.exit("Defina META_ACCESS_TOKEN no seu terminal (não cole o token no chat).")
    return t

def call(method, path, params=None, dry=False):
    params = {k: (json.dumps(v) if isinstance(v, (dict, list)) else v) for k, v in (params or {}).items()}
    if dry:
        print(f"[dry-run] {method} /{path} {json.dumps(params, ensure_ascii=False)[:600]}"); return {"id": f"<{path.split('/')[-1]}>"}
    params["access_token"] = token()
    data = urllib.parse.urlencode(params).encode()
    url = f"{BASE}/{path}" + ("?" + data.decode() if method == "GET" else "")
    req = urllib.request.Request(url, data=None if method == "GET" else data, method=method)
    try:
        return json.load(urllib.request.urlopen(req, timeout=60))
    except urllib.error.HTTPError as e:
        err = json.load(e).get("error", {})
        sys.exit(f"Erro da API em /{path}: {err.get('message')} (code {err.get('code')}, subcode {err.get('error_subcode')}). Nada foi ativado.")

def validar(p):
    errs, warn = [], []
    acc = p.get("ad_account_id") or os.environ.get("META_AD_ACCOUNT_ID", "")
    if not acc.startswith("act_"): errs.append("ad_account_id ausente ou sem prefixo act_")
    c = p.get("campanha", {})
    if c.get("objective") not in OBJ: errs.append(f"objective inválido: {c.get('objective')}")
    if not c.get("name"): errs.append("campanha sem nome")
    if "special_ad_categories" not in c: warn.append("special_ad_categories não informado; será enviado []")
    cbo = "daily_budget" in c or "lifetime_budget" in c
    if not p.get("conjuntos"): errs.append("nenhum conjunto")
    for i, s in enumerate(p.get("conjuntos", []), 1):
        if not s.get("name"): errs.append(f"conjunto {i} sem nome")
        if not cbo and not ("daily_budget" in s or "lifetime_budget" in s): errs.append(f"conjunto {i} sem orçamento (campanha não é CBO)")
        if cbo and ("daily_budget" in s or "lifetime_budget" in s): errs.append(f"conjunto {i} tem orçamento em campanha CBO")
        if c.get("objective") in {"OUTCOME_SALES", "OUTCOME_LEADS"} and not s.get("promoted_object", {}).get("pixel_id"):
            errs.append(f"conjunto {i} sem promoted_object.pixel_id para objetivo de conversão")
        if not s.get("targeting", {}).get("geo_locations"): errs.append(f"conjunto {i} sem geo_locations")
        if not s.get("anuncios"): errs.append(f"conjunto {i} sem anúncios")
        for j, a in enumerate(s.get("anuncios", []), 1):
            cr = a.get("creative", {})
            if not a.get("name"): errs.append(f"anúncio {i}.{j} sem nome")
            if not cr.get("url_tags"): errs.append(f"anúncio {i}.{j} sem url_tags (UTMs)")
            oss = cr.get("object_story_spec", {})
            if not cr.get("creative_id") and not oss.get("page_id"): errs.append(f"anúncio {i}.{j} sem creative_id nem object_story_spec.page_id")
    for x in [c] + p.get("conjuntos", []) + [a for s in p.get("conjuntos", []) for a in s.get("anuncios", [])]:
        if x.get("status", "PAUSED") != "PAUSED": errs.append(f"'{x.get('name')}' com status {x.get('status')}: a subida é sempre PAUSED")
    return errs, warn

def subir(p, dry):
    errs, warn = validar(p)
    for w in warn: print("aviso:", w)
    if errs: sys.exit("Plano inválido:\n- " + "\n- ".join(errs))
    acc = p.get("ad_account_id") or os.environ["META_AD_ACCOUNT_ID"]
    c = dict(p["campanha"]); c["status"] = "PAUSED"; c.setdefault("special_ad_categories", []); c.setdefault("buying_type", "AUCTION")
    camp = call("POST", f"{acc}/campaigns", c, dry)["id"]; print("campanha:", camp)
    out = {"campaign_id": camp, "adsets": []}
    for s in p["conjuntos"]:
        ads = s.pop("anuncios"); s = dict(s, campaign_id=camp, status="PAUSED")
        aset = call("POST", f"{acc}/adsets", s, dry)["id"]; print("  conjunto:", s["name"], aset)
        rec = {"adset_id": aset, "ads": []}
        for a in ads:
            cr = a["creative"]
            cid = cr.get("creative_id") or call("POST", f"{acc}/adcreatives", {k: v for k, v in cr.items()}, dry)["id"]
            ad = call("POST", f"{acc}/ads", {"name": a["name"], "adset_id": aset, "creative": {"creative_id": cid}, "status": "PAUSED"}, dry)["id"]
            print("    anúncio:", a["name"], ad); rec["ads"].append(ad)
        out["adsets"].append(rec)
    print(json.dumps(out, indent=1)); print("Tudo criado PAUSADO. Ativação só com confirmação explícita do operador.")

def main():
    a = sys.argv[1:]
    if not a: print(__doc__); return
    cmd = a[0]
    if cmd in ("validar", "subir"):
        p = json.load(open(a[1]))
        if cmd == "validar":
            e, w = validar(p); [print("aviso:", x) for x in w]
            print("OK: plano válido." if not e else "Erros:\n- " + "\n- ".join(e))
        else: subir(p, dry="--executar" not in a)
    elif cmd == "insights":
        per = a[a.index("--periodo")+1] if "--periodo" in a else "last_7d"
        niv = a[a.index("--nivel")+1] if "--nivel" in a else "adset"
        f = "campaign_name,adset_name,ad_name,spend,impressions,reach,frequency,cpm,clicks,ctr,cpc,inline_link_click_ctr,actions,cost_per_action_type,purchase_roas"
        print(json.dumps(call("GET", f"{a[1]}/insights", {"fields": f, "date_preset": per, "level": niv}), indent=1, ensure_ascii=False))
    elif cmd == "ativar":
        if "--confirmado-pelo-operador" not in a: sys.exit("Ativação bloqueada: requer confirmação explícita do operador no chat.")
        print(call("POST", a[1], {"status": "ACTIVE"}))
    elif cmd == "pausar":
        print(call("POST", a[1], {"status": "PAUSED"}))
    else: print(__doc__)

if __name__ == "__main__": main()

```

=====
### ARQUIVO: agente-de-trafego-trm/scripts/plano-exemplo.json
=====

```json
{
 "_nota": "Exemplo de estrutura. Troque todos os IDs e valores. Orçamento em centavos da moeda da conta. Nomes seguem a nomenclatura da skill. Nome de campanha e anúncio no padrão da página 05 — Tráfego; nome de conjunto é padrão derivado (a página não define).",
 "ad_account_id": "act_000000000000000",
 "campanha": {
  "name": "BR__OFERTA__VENDAS__TESTE01__2026-09",
  "objective": "OUTCOME_SALES",
  "special_ad_categories": [],
  "status": "PAUSED"
 },
 "conjuntos": [
  {
   "name": "ABERTO__PURCHASE__ABO__V01",
   "daily_budget": 5000,
   "billing_event": "IMPRESSIONS",
   "optimization_goal": "OFFSITE_CONVERSIONS",
   "bid_strategy": "LOWEST_COST_WITHOUT_CAP",
   "promoted_object": {
    "pixel_id": "000000000000000",
    "custom_event_type": "PURCHASE"
   },
   "targeting": {
    "geo_locations": {
     "countries": [
      "BR"
     ]
    },
    "age_min": 25,
    "age_max": 55,
    "genders": [
     2
    ]
   },
   "status": "PAUSED",
   "anuncios": [
    {
     "name": "ANG_MECANISMO__HOOK_PERGUNTA__UGC__MULHER40__V01",
     "creative": {
      "name": "CR__ANG_MECANISMO__HOOK_PERGUNTA__UGC__MULHER40__V01",
      "object_story_spec": {
       "page_id": "000000000000000",
       "video_data": {
        "video_id": "000000000000000",
        "image_hash": "HASH_DA_THUMBNAIL",
        "message": "Texto principal aprovado pelo AGENTE DE COPY",
        "title": "Headline aprovada",
        "call_to_action": {
         "type": "LEARN_MORE",
         "value": {
          "link": "https://seudominio.com/vsl"
         }
        }
       }
      },
      "url_tags": "utm_source=facebook&utm_medium=paid&utm_campaign=br__oferta__teste01&utm_content=ang_mecanismo__ugc__v01&utm_term={{adset.name}}"
     }
    }
   ]
  }
 ]
}
```