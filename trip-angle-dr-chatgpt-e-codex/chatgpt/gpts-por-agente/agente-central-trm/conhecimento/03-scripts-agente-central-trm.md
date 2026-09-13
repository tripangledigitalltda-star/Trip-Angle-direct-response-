# Scripts do AGENTE CENTRAL TRM

No interpretador de código: grave cada bloco em /mnt/data com o nome do arquivo e execute.

=====
### ARQUIVO: scripts/projeto.py
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