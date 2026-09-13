# Scripts do AGENTE DE TRÁFEGO TRM

No interpretador de código: grave cada bloco em /mnt/data com o nome do arquivo e execute.

=====
### ARQUIVO: scripts/meta_ads.py
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
### ARQUIVO: scripts/plano-exemplo.json
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