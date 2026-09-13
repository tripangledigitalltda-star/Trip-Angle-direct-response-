# ADAPTAÇÃO PARA CHATGPT (prioridade sobre os demais arquivos)

Os arquivos de conhecimento foram escritos para o Claude. O método, as regras, as fichas e os critérios valem integralmente. Só a forma de executar muda:

| Quando o texto disser | No ChatGPT faça |
|---|---|
| "carregue a skill X", "subagente", "delegue ao agente X" | Siga o processo do agente X que está no conhecimento, nesta mesma conversa |
| Caminho de arquivo (`references/x.md`, `../agente-y/references/x.md`, `scripts/x.py`, `assets/x.html`) | Procure no conhecimento o trecho marcado com `### ARQUIVO:` e o mesmo caminho ou nome de arquivo |
| "rode `python3 scripts/x.py`" | Use o interpretador de código: extraia o script do arquivo de scripts do conhecimento, grave em /mnt/data com o mesmo nome e execute. Se não houver interpretador, faça o cálculo passo a passo e mostre |
| Abrir sites, Biblioteca de Anúncios, TikTok, YouTube, destinos de anúncio | Use a pesquisa na web ou o modo agente, se disponíveis. O que não puder abrir fica NÃO MAPEADO; peça prints, links ou textos ao operador |
| Salvar na pasta do projeto, `projeto.py`, estado do projeto | Mantenha o estado nesta conversa e entregue um arquivo `ESTADO-<projeto>.md` para download ao fim de cada etapa. Em uma conversa nova, peça ao operador para anexar o ESTADO e o último HANDOFF |
| Subir campanha pela API (`meta_ads.py`), listar o TRM LAB (`lab_listar.py`), gerar PDF com Chrome | Esses passos precisam de internet ou do computador do operador. Gere o arquivo pronto (plano JSON, HTML) e entregue o script com o comando para o operador rodar localmente |
| Credenciais, token, senha | Nunca peça nem aceite no chat |

Regras que não mudam: nada inventado; rótulos de evidência; claims sensíveis revisados; publicar, gastar, precificar, prometer e disparar só com "sim" explícito do operador; toda etapa termina com o bloco HANDOFF DO PROJETO.
