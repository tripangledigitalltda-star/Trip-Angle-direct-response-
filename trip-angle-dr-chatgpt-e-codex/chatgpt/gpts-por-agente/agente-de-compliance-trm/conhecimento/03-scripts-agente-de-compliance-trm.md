# Scripts do AGENTE DE COMPLIANCE TRM

No interpretador de código: grave cada bloco em /mnt/data com o nome do arquivo e execute.

=====
### ARQUIVO: scripts/varrer_claims.py
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