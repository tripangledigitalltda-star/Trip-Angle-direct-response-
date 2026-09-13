# Scripts do AGENTE DE ESPIONAGEM TRM

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
### ARQUIVO: scripts/pretriagem.py
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
### ARQUIVO: scripts/quiz_walker.js
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