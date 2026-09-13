# Scripts do AGENTE DE BACKEND TRM

No interpretador de código: grave cada bloco em /mnt/data com o nome do arquivo e execute.

=====
### ARQUIVO: scripts/economia_backend.py
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