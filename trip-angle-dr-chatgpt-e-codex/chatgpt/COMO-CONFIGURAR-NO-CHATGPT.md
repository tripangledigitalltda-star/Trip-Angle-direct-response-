# Como configurar os agentes TRM no ChatGPT

Pacote gerado a partir do plugin trip-angle-dr. O conteúdo das skills está completo; só o formato mudou.

## Qual usar
- **gpt-unico/**: um GPT "TRM Direct Response" com os 11 agentes. Mais prático.
- **gpts-por-agente/**: um GPT por agente. Mais preciso, porque cada GPT carrega só o conhecimento da sua etapa.
Dá para usar os dois: o único para o dia a dia e os separados para Copy, Compliance e Tráfego.

## Criar o GPT (repita para cada pasta)
1. No ChatGPT, abra **Explorar GPTs → Criar** e vá para a aba **Configurar**.
2. **Nome:** "TRM Direct Response" (ou o nome do agente, por exemplo "AGENTE DE COPY TRM").
3. **Instruções:** cole todo o conteúdo de `instrucoes.txt`.
4. **Iniciadores de conversa:** use as linhas de `iniciadores.txt`.
5. **Conhecimento:** envie todos os arquivos da pasta `conhecimento/`.
6. **Capacidades:** ligue **Pesquisa na web** e **Interpretador de código e análise de dados**. Geração de imagem é opcional (útil para o AGENTE DE PRODUÇÃO DE CRIATIVOS).
7. Salve com visibilidade **Somente eu** (ou quem você quiser).
Confira no próprio ChatGPT os limites atuais de tamanho das instruções e de arquivos de conhecimento. Este pacote usa até 20 arquivos por GPT e instruções abaixo de 8000 caracteres.

## Como usar
- Comece com: "Abra um projeto para a oferta X e comece pela espionagem" ou chame o agente pelo nome.
- Ao fim de cada etapa, baixe o `ESTADO-<projeto>.md` e o HANDOFF. Em uma conversa nova ou em outro GPT, anexe os dois para continuar.
- Nos GPTs separados, leve o HANDOFF de um GPT para o próximo.

## O que funciona diferente do Claude
- Não há subagentes em Opus nem troca automática de agente: a mesma conversa executa uma etapa por vez.
- Scripts em Python rodam no interpretador de código; os que precisam de internet ou do seu computador (subida pela API da Meta, listagem do TRM LAB, PDF pelo Chrome) são entregues prontos para você rodar localmente.
- Navegação na Biblioteca de Anúncios e em destinos depende da pesquisa na web ou do modo agente do ChatGPT.
- A qualidade final depende do modelo da OpenAI escolhido na conversa.

## Codex
A pasta `../codex/` tem as skills no padrão Agent Skills. Copie `.agents/skills/` e `AGENTS.md` para a raiz do seu projeto no Codex.
