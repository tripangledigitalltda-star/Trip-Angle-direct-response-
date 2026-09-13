# AGENTE CENTRAL TRM

Identificador: agente-central-trm
Quando usar: AGENTE CENTRAL TRM: recebe o pedido, diz qual agente TRM usar, abre e guarda o estado do projeto e passa o handoff entre etapas. Use ao iniciar oferta, ver status ou perguntar próximo passo.

=====
### ARQUIVO: SKILL.md (processo do agente)
=====


# AGENTE CENTRAL TRM

Orquestrador da linha TRM de direct response. Não executa o trabalho das etapas: entende o pedido, localiza o projeto, confere o que já foi entregue, escolhe o agente certo, entrega a ele exatamente o handoff que ele precisa e registra o resultado.

## Linha de produção

| # | Etapa | Agente | Entrega principal |
|---|---|---|---|
| 1 | Espionagem | `agente-de-espionagem-trm` | Ofertas qualificadas, funis, sinais de escala |
| 2 | Criativos e temas | `agente-de-ads-trm` | Radar de temas, hooks, matriz de conceitos, Creative Cards, registro TRM LAB |
| 3 | Copy e modelagem | `agente-de-copy-trm` | Oferta modelada, VSL, página, leads, hooks, tabela de claims |
| 4 | Funil | `agente-de-funil-trm` (AGENTE DE FUNIL TRM) | Páginas, quiz, checkout, bump e upsell |
| 5 | Produção de criativos | `agente-de-producao-de-criativos-trm` (AGENTE DE PRODUÇÃO DE CRIATIVOS TRM) | Peças finais e variações |
| 6 | Compliance | `agente-de-compliance-trm` (AGENTE DE COMPLIANCE TRM) | Revisão antes de publicar |
| 7 | Tráfego | `agente-de-trafego-trm` | Medição validada, campanhas pausadas, leituras e decisões |
| 8 | Backend e CRO | `agente-de-backend-trm` e `agente-de-cro-trm` | Margem, recuperação, testes de página |
| 9 | Produto | `agente-de-produto-trm` (AGENTE DE PRODUTO TRM) | Entregável, matriz promessa × produto, PDF, área de membros |

A ordem é padrão, não obrigatória. Um projeto pode começar pela copy de uma oferta já escolhida ou pelo tráfego de uma oferta que já roda.

## 1. Entender o pedido

Classifique a intenção com `references/roteamento.md` e responda em uma linha: qual agente, por quê e o que ele vai entregar. Se o pedido cobrir várias etapas, divida em sequência e execute uma de cada vez. Se couber em uma etapa, siga direto para ela sem cerimônia.

Pedido ambíguo entre dois agentes: escolha pelo **artefato** que o operador quer receber, não pela palavra usada. "Hook" para pesquisar referências vai ao ADS; "hook" para escrever a copy da oferta vai ao COPY.

## 2. Localizar ou abrir o projeto

Todo trabalho pertence a um projeto: uma oferta, um país.
- `python3 scripts/projeto.py listar` mostra os projetos existentes.
- `python3 scripts/projeto.py status <projeto>` mostra etapas concluídas, pendências e a próxima ação.
- `python3 scripts/projeto.py novo <projeto> --oferta "..." --pais BR --nicho "..."` abre um projeto novo.

Pasta padrão: `~/Desktop/trip-angle-dr/projetos/` (ou a variável `TRM_PROJETOS`). Estrutura e campos em `references/estado-do-projeto.md`. Se o operador não citar projeto e só existir um ativo, use esse e diga qual é.

## 3. Conferir entradas antes de acionar o agente

Leia o estado e os handoffs anteriores. Monte o **pacote de entrada** da etapa com `references/handoff.md`, seção 3: o que o agente de destino exige, o que já existe no projeto e o que falta. Falta algo que só o operador tem: pergunte em bloco único. Falta algo que outra etapa produz: diga qual etapa rodar antes ou siga com a lacuna declarada, se o operador pedir.

## 4. Acionar o agente

Delegue a etapa ao **subagente do plugin com o mesmo nome** (por exemplo `agente-de-copy-trm`), que roda em Opus. Passe no pedido o pacote de entrada completo, a pasta da etapa do projeto e o objetivo. Quando subagentes não estiverem disponíveis no ambiente, carregue a skill do agente e execute na conversa. Etapa sem agente criado ainda: diga isso, ofereça fazer em modo manual com as regras compartilhadas e registre como "manual".

## 5. Registrar a saída

Ao fim de cada etapa:
1. Salve os artefatos na pasta da etapa do projeto.
2. Exija o bloco `HANDOFF DO PROJETO` (`references/handoff.md`, seção 1) preenchido pelo agente. Sem bloco, a etapa não fecha.
3. `python3 scripts/projeto.py registrar <projeto> <etapa> handoff.md` grava o handoff, atualiza o estado e a próxima ação.
4. Responda ao operador: o que ficou pronto, o que depende de aprovação e qual é a próxima ação única.

## Convenção de caminhos

Caminhos como `../agente-de-copy-trm/references/...` são relativos à pasta desta skill dentro de `skills/` do plugin.

## 6. Regras compartilhadas

Valem para todos os agentes e estão em `references/regras-compartilhadas.md`: rótulos de evidência, nada inventado, prova próxima do claim, claims sensíveis, escassez só verdadeira, ROAS não é lucro, contingência é conformidade, e aprovação humana para publicar, gastar, precificar, prometer e disparar. Quando um agente não citar uma regra, ela vale mesmo assim.

## Vocabulário da casa

Glossário, sequência canônica, rótulos de evidência, bases técnicas e Test Card ficam em `references/vocabulario/`. Todos os agentes usam esses termos; em dúvida sobre um conceito (hook, lead, ângulo, mecanismo, prova, oferta, funil), consulte o glossário antes de responder.

## Status rápido

Quando o operador perguntar "em que pé está" ou "qual o próximo passo", rode `status` e responda em até cinco linhas: projeto, etapas concluídas, aprovações pendentes, bloqueios e próxima ação única.

## Erros que invalidam a orquestração

Acionar agente sem conferir o estado · rodar duas etapas ao mesmo tempo sobre a mesma oferta · fechar etapa sem handoff · deixar o agente seguinte reinventar o que a etapa anterior já entregou · misturar projetos · ativar campanha ou publicar sem aprovação registrada · esconder etapa pulada.


=====
### ARQUIVO: references/estado-do-projeto.md
=====

# Estado do projeto

## Estrutura de pastas
```
projetos/<projeto>/
├── estado.json          controle das etapas (gerado pelo script)
├── ESTADO.md            resumo legível (gerado pelo script)
├── 01-espionagem/
├── 02-ads/
├── 03-copy/
├── 04-funil/
├── 05-producao-criativos/
├── 06-compliance/
├── 07-trafego/
├── 08-backend-cro/
├── 09-produto/
└── handoffs/            um arquivo por handoff: AAAAMMDD-HHMM__<etapa>.md
```
Nome do projeto: `pais-oferta` em minúsculas e hífens, por exemplo `br-mounjaro-natural`.

## Campos do estado
Projeto · oferta · país · nicho · criado em · atualizado em · etapas (status: pendente, em andamento, concluída, pulada, manual; data; agente; último handoff; portão de aprovação) · aprovações pendentes · bloqueios · próxima ação única · histórico de decisões.

## Regras
- Só o AGENTE CENTRAL altera `estado.json`, via script.
- Uma etapa só vira "concluída" com handoff registrado e portão de aprovação preenchido.
- Aprovação pendente de publicar, gastar, precificar ou prometer aparece no topo do status até ser resolvida.


=====
### ARQUIVO: references/handoff.md
=====

# Handoff entre agentes

## 1. Bloco obrigatório (template da Biblioteca Operacional Trip Angle)

```
HANDOFF DO PROJETO
Projeto:
Etapa concluída:
Agente:
Versão e data:
Objetivo:
Entradas utilizadas:
Evidências confirmadas:
Hipóteses abertas:
Decisões aprovadas:
Artefatos produzidos:
Claims e provas pendentes:
Riscos e restrições:
Métrica principal:
Portão de aprovação:
Próximo agente:
Próxima ação única:
```
"Portão de aprovação" é `aprovado por <nome> em <data>` ou `pendente: <o que precisa ser aprovado>`. "Artefatos produzidos" lista caminhos de arquivo.

## 2. Regras
- Toda etapa termina com o bloco. Sem ele a etapa fica "em andamento" no estado.
- O agente seguinte abre pedindo o bloco da etapa anterior e só os artefatos listados nele.
- Hipótese aberta não vira fato na etapa seguinte. Claim pendente continua pendente até alguém anexar a prova.
- Etapa pulada é registrada como "pulada" com o motivo.

## 3. Pacote de entrada por agente

| Agente | Precisa do projeto | Precisa do operador |
|---|---|---|
| ESPIONAGEM | Nicho, país, termos, tipo de oferta-alvo | Recorte e prioridade |
| ADS | Handoff da ESPIONAGEM (oferta, anunciantes, IDs, destino) ou oferta e assunto | Objetivo da pesquisa, países |
| COPY | Handoffs de ESPIONAGEM e ADS (oferta de referência, funil, hooks, temas) | Produto real, entregáveis, preço, provas próprias, país de destino |
| FUNIL | Handoff do COPY (oferta modelada, copy aprovada, claims) | Plataforma de página e checkout, domínio |
| PRODUÇÃO DE CRIATIVOS | Handoffs de ADS (Creative Cards, ondas) e COPY (hooks, roteiros curtos, claims) | Ferramentas de produção, identidade visual, direitos de imagem |
| COMPLIANCE | Peças de COPY, FUNIL e PRODUÇÃO | País e categoria do produto |
| TRÁFEGO | Handoffs de COPY (URL, claims), PRODUÇÃO ou ADS (criativos), FUNIL (checkout, eventos) | Custos, orçamento, limite de perda, conta, pixel, rota de subida |
| PRODUTO | Handoff do COPY (promessa, stack, bônus, claims) e do BACKEND (motivos de reembolso) | Formato, plataforma de membros, identidade visual, conteúdo existente, especialista |
| BACKEND e CRO | Handoffs de FUNIL e TRÁFEGO (dados por etapa) | Ferramentas de e-mail e WhatsApp, acesso a dados |

## 4. Saídas esperadas por agente (para "Artefatos produzidos")
- ESPIONAGEM: relatório da rodada, tabela de triagem, Mapa de Oportunidades.
- ADS: relatório do editor, radar de temas, banco de hooks, matriz de conceitos, Creative Cards, planilha TRM LAB.
- COPY: mapa da oferta, diagnóstico, card da oferta modelada, VSL, página, leads, banco de headlines, roteiros de anúncio, tabela de claims, hipóteses de teste.
- PRODUTO: arquitetura, matriz promessa × produto, conteúdo em Markdown, PDF, roteiros de aula, estrutura da área de membros.
- TRÁFEGO: economia unitária, plano de medição, QA de tracking, plano de campanha, IDs subidos, registro de decisão.


=====
### ARQUIVO: references/regras-compartilhadas.md
=====

# Regras compartilhadas da linha TRM

Origem: handoff de conversão Trip Angle (guardrails dos módulos 03, 04 e 05) e Biblioteca Operacional de Direct Response com IA.

1. Nunca inventar número, prova, depoimento, pesquisa ou resultado.
2. Separar sempre evidência, hipótese, decisão e informação ausente. Rótulos: FATO CONFIRMADO, ALEGAÇÃO DA COPY, OBSERVAÇÃO, INTERPRETAÇÃO ESTRATÉGICA, PADRÃO IDENTIFICADO, HIPÓTESE, NÃO MAPEADO NOS MATERIAIS.
3. Prova deve ser a mais próxima possível do claim (hierarquia: demonstração, dados próprios, caso verificável, depoimento autorizado, credencial, explicação plausível, opinião).
4. Claims sensíveis (saúde, emagrecimento, renda, finanças, segurança, crianças) exigem revisão específica. CONAR, CDC e ANPD se aplicam; ANVISA quando houver produto de saúde.
5. Escassez e urgência só quando verdadeiras.
6. Anúncio ativo, contagem e longevidade são sinal de escala, não prova de venda. Views são sinal de alcance, não conversão.
7. ROAS não é lucro. Não somar conversões de plataformas com janelas de atribuição diferentes.
8. Contingência significa conformidade, nunca burla de política.
9. Modelagem não é cópia: reutiliza função, nunca texto, identidade, prova, número ou ativo de terceiros.
10. Modo rascunho: publicação, gasto, preço, promessa e disparo exigem aprovação humana explícita e registrada.
11. Credenciais nunca passam pelo chat.


=====
### ARQUIVO: references/roteamento.md
=====

# Roteamento de pedidos

## Por artefato desejado

| O operador quer receber | Agente | Frases típicas |
|---|---|---|
| Ofertas que estão rodando, funis, anunciantes, sinais de escala | `agente-de-espionagem-trm` | "minera", "espiona", "o que está escalando em", "acha ofertas de", "tria esses cartões" |
| Referências de vídeo, hooks usados, temas virais, formatos em alta, ideias de criativo, registro no TRM LAB | `agente-de-ads-trm` | "traz referências de criativos", "hooks virais de", "o que viraliza no TikTok sobre", "formatos em alta", "alimenta o lab" |
| Mapa de uma oferta, diagnóstico de copy, oferta modelada, VSL, página, leads, headlines, stack, garantia | `agente-de-copy-trm` | "modela essa oferta", "escreve a VSL", "copy da página", "novos ângulos para a oferta", "mapeia personas e dores" |
| Economia da oferta, plano de medição, pixel, CAPI, UTMs, campanha, subida, leitura de métricas, escala | `agente-de-trafego-trm` | "sobe a campanha", "configura o tracking", "qual CPA máximo", "analisa os números", "escalo ou pauso" |
| Página, quiz, pré-lander, checkout, order bump, upsell construídos | `agente-de-funil-trm` (AGENTE DE FUNIL TRM) | "monta a página", "cria o quiz", "estrutura o checkout" |
| Peça final de criativo, roteiro final, prompts de IA de imagem ou vídeo | `agente-de-producao-de-criativos-trm` | "roteiriza", "gera os prompts", "faz as variações" |
| Revisão de política e claims antes de publicar | `agente-de-compliance-trm` | "isso passa na Meta?", "revisa os claims" |
| Recuperação, e-mails, WhatsApp, upsell pós-compra, reembolso | `agente-de-backend-trm` (AGENTE DE BACKEND TRM) | "sequência de recuperação", "pós-venda" |
| Gargalo de página ou checkout, teste A/B de página | `agente-de-cro-trm` (AGENTE DE CRO TRM) | "a página não converte", "onde o funil vaza" |
| Entregável do produto: ebook, protocolo, cardápio, receitas, aulas, bônus, área de membros | `agente-de-produto-trm` | "cria o ebook", "monta o protocolo", "estrutura a área de membros", "faz os bônus" |
| Estado do projeto, próximo passo, o que falta | `agente-central-trm` | "em que pé está", "próximo passo", "abre um projeto" |

## Casos de fronteira

| Pedido | Vai para | Motivo |
|---|---|---|
| "Analisa esse anúncio concorrente" | ADS se o foco é o criativo; ESPIONAGEM se o foco é a oferta e o funil | Decidir pelo artefato |
| "Quero hooks para a minha oferta" | COPY | Hooks escritos para a oferta própria |
| "Quais hooks estão sendo usados em mounjaro" | ADS | Pesquisa de referências |
| "Essa oferta gringa funciona no Brasil?" | ESPIONAGEM para sinais; COPY para localização | Sequência de duas etapas |
| "O CPA subiu" | TRÁFEGO | Diagnóstico por camada começa na mídia e no tracking |
| "A VSL não converte" | TRÁFEGO para confirmar dados; depois COPY | Primeiro descartar tracking e tráfego |

## Skills antigas consolidadas (13/09/2026)

As skills `ta-*` foram incorporadas: vocabulário e Test Card em `../../agente-central-trm/references/vocabulario/`; leitura, modelagem sem cópia e criação do zero no AGENTE DE COPY; templates de criativos no AGENTE DE PRODUÇÃO; fases de tráfego no AGENTE DE TRÁFEGO; mineração virou AGENTE DE ESPIONAGEM (`agente-de-espionagem-trm`). Cópias originais em `~/Desktop/trip-angle-dr/arquivo-skills-antigas/`.


=====
### ARQUIVO: references/vocabulario/bases-tecnicas.md
=====

# As 19 bases técnicas (Arsenal Técnico) — esquemas e uso

Ordem de consulta: diagnóstico → mensagem → criativos/percurso → oferta/risco → modelagem/teste. Cada registro carrega: Nicho/Mercado, Confiabilidade (Nível A–D; D = hipótese), fonte/linhagem e rótulo de evidência. Convenção de IDs por oferta: `<OFERTA>-AD01`, `-VSL01`, `-HK01`, `-ANG01`, `-MEC01`, `-TC01`, `-OP01`.

## Diagnóstico e oportunidade
- **01 — Fontes e Evidências**: Fonte URL, Origem (Meta Ad Library, Google Ads Transparency, página, checkout, review), Grupo, Nicho/Mercado, Status, Confiabilidade, Limitações, Observações. Regra: registrar data, ID do anúncio, anunciante, país e etapa realmente acessada.
- **02 — Personas**: Contexto, Idade provável, Dor visível, Dor invisível, Dor emocional, Frustrações, Desejo emocional, Linguagem e frases (literal).
- **19 — Mapa de Oportunidades**: Oportunidade, Lacuna, Tipo (Teste/Pesquisa/Produto), Prioridade, Base observada (IDs e linhas), Persona, Dor, Desejo, Mecanismo, Ângulo, Funil sugerido, Produto sugerido, Prova necessária, Risco, Confiabilidade, Status (Hipótese). Regra: oportunidade derivada de lacuna observada, não de desejo importado de livros.

## Mensagem e persuasão
- **03 — Hooks**: Formato, Ângulo, Mecanismo, Curiosidade, Desejo, Risco, Ofertas relacionadas.
- **04 — Ângulos**: Definição, Problema, Variações, Hooks compatíveis, Criativos compatíveis, VSLs compatíveis, Confiabilidade.
- **05 — Mecanismos**: Tipo (problema/solução/único), Novidade percebida, Facilidade de explicação, Curiosidade, Capacidade de criativos, Saturação interna, Risco científico, Ofertas que utilizam.
- **15 — Promessas e Desejos**: Promessa original (literal), Tipo, Ângulo, Prova necessária, Risco, Status.
- **16 — Objeções e Crenças**: Crença ou dúvida, Trecho original, Resposta usada, Etapa, Persona, Oferta, Risco.

## Criativos e percurso
- **06 — Formatos de Criativos**: Duração, Cenas, Variações, Exemplos, Hooks e Mecanismos compatíveis, Facilidade de escala, Saturação interna.
- **08 — Ads e Criativos**: Texto original, Estrutura abstrata (função por bloco), Problema, Mecanismo, CTA, Formato, Status de linhagem.
- **09 — VSLs**: Lead, Mecanismo do problema, Transição para produto, Preço e ancoragem, Bônus, Depoimentos, Confiabilidade.
- **10 — Funis**: Entrada observada, Sequência observada, VSL, Retenção, Oferta relacionada, Hipóteses, Inconsistências, Confiabilidade. Só etapas observadas.

## Oferta, entrega e risco
- **07 — Ofertas**: Big Idea, Dor, Desejo, Mecanismo da solução, Provas, Urgência, Pontos fortes, Produto relacionado.
- **11 — Provas**: Tipo, Texto ou descrição original, O que pretende provar, Fonte, Risco, Status, Confiabilidade.
- **12 — Claims e Risco**: Original, O que a copy apresenta como prova, Evidência real disponível, Risco, Reformulação segura, Princípio de aprendizado, Confiabilidade.
- **17 — Produtos e Entregáveis**: Problema resolvido, Transformação proposta, Bônus, Order bump, Upsell, Risco.
- **18 — Componentes de Oferta**: Descrição, Função na oferta, Problema que resolve, Prova necessária.

## Modelagem e aprendizagem
- **13 — Swipe File**: Texto original, Fonte, Etapa do funil, Consciência, Emoção, Ângulo, Mecanismo, Confiabilidade. Estudo, não cópia; consultar só depois de entender o problema.
- **14 — Test Cards**: Nome, Hipótese, O que estamos testando, Tipo de variável, Variação A/B/C, Controle, O que não pode mudar, Persona, Audiência, Canal, Destino, Formato, Hook, Ângulo, Mecanismo, Promessa, CTA, Script, Métrica principal, Métrica secundária, Amostra planejada, Janela, Critério de vitória, Critério de descarte, Prova necessária, Confiabilidade, Status, Resultado, Aprendizado.

## Bases por fonte de registro na mineração
Uma rodada de mineração alimenta, nesta ordem: 01 (fonte) → 08/09/10 (peças e funil observados) → 02/15/16 (persona, promessa, objeções literais) → 05/04/03 (mecanismo, ângulo, hook por função) → 07/17/18/11/12 (oferta, produto, componentes, provas, claims) → 19 (oportunidade) → 13 (swipe) → 14 (test card).


=====
### ARQUIVO: references/vocabulario/glossario.md
=====

# Glossário de Engenharia de Ofertas (dicionário operacional)

Cada termo: o que é · com o que não confundir · exemplo · onde estudar (base técnica).

1. **Hook** — dispositivo inicial que interrompe a atenção e cria relevância. Não é o lead. Ex.: pergunta, descoberta, segredo ou identificação nos Ads. Base 03.
2. **Lead** — desenvolvimento inicial que confirma relevância e conduz à próxima leitura. Não é headline nem hook isolado. Ex.: abertura e primeiros blocos de uma VSL. Base 09. Famílias de lead (Great Leads): oferta, promessa, solução de problema, grande segredo, revelação, história; abertura direta ou indireta.
3. **Ângulo** — enquadramento escolhido para apresentar problema, desejo ou oportunidade. Não é a promessa. Ex.: bloqueio invisível, conhecimento reservado, ciclo herdado. Base 04.
4. **Promessa** — benefício ou resultado que a copy associa à oferta. Não é claim validado nem garantia. Base 15.
5. **Claim** — afirmação que pode exigir prova, validação ou qualificação de risco. Não é evidência independente. Ex.: alegações financeiras, médicas, científicas, de resultado. Base 12.
6. **Mecanismo** — explicação causal apresentada pela copy para o problema ou para a solução. Não é o produto nem o nome proprietário. Camadas: mecanismo do problema, mecanismo da solução, mecanismo único (diferenciação percebida), skin (nome/ritual/personagem/superfície). Teste: remova o nome; se não sobra lógica, é skin. Base 05.
7. **Big Idea** — tese central que organiza a interpretação da oferta. Não é frase de anúncio nem slogan. Teste: resuma a tese sem headline, nome, personagem ou bordão; se o resumo desaparece, você capturou superfície. Matriz Mestre / Base 07.
8. **Nova oportunidade** — caminho que surge quando a copy reenquadra o problema ("talvez o caminho não seja X, mas Y"). Não é mercado novo nem demanda comprovada. Permanece hipótese até produto e teste. Base 19.
9. **Formato** — recipiente de produção e distribuição (Ad, VSL, página, quiz, UGC, unboxing, live). Não é argumento, ângulo ou mecanismo. Base 06.
10. **Ad** — unidade de entrada e teste de atenção/qualificação. Desmontar por função: interrupção, seleção, tensão, reframe, prova, ponte, CTA. Base 08.
11. **VSL** — roteiro e progressão de crença. Não é o funil inteiro. Blocos: situação → agitação → explicação antiga falha → mecanismo do problema → nova oportunidade → mecanismo da solução → promessa → prova → produto → objeções → condições/risco/CTA. Base 09.
12. **Prova** — elemento usado pela copy para sustentar uma afirmação (depoimento, autoridade, demonstração, história, referência). Não é validação independente. Hierarquia: demonstração > dados próprios com método > caso verificável semelhante > depoimento específico autorizado > credencial > explicação plausível > opinião. Base 11.
13. **Objeção** — resistência, dúvida ou risco percebido que a copy responde. Não é a crença central. Base 16.
14. **Crença** — explicação ou pressuposto que a copy precisa manter, tensionar ou substituir. Não é fato sobre o mercado. Base 16.
15. **Persona** — pessoa ou grupo descrito pela situação e linguagem da oferta (circunstância, comportamento, tensão, evento de mudança). Não é público estatístico. Base 02.
16. **Desejo** — estado ou mudança desejada pela persona na narrativa. Não é promessa validada nem demanda comprovada. Base 15. **Dor** — tensão vivida ou narrada (custo emocional, funcional, social, financeiro).
17. **Produto** — bem, serviço ou entregável recebido. Não é a oferta completa. Base 17.
18. **Oferta** — produto + promessa + mecanismo + prova + preço + redução de risco + condições + CTA (quando observados). Não é produto isolado. Base 07.
19. **Funil** — sequência de páginas, eventos e transições da entrada à ação (Ad → página/quiz/VSL → checkout → acesso → pós-compra). Não é VSL isolada. Só registrar etapas observadas. Base 10.
20. **Modelagem** — reconstrução funcional de princípios transferíveis em outro contexto. Não é copiar frases, identidade, prova ou claim. Manual de Modelagem.
21. **Hipótese** — previsão operacional ainda não confirmada, escrita para ser testada. Não é resultado. Bases 14 e 19.
22. **Test Card** — registro estruturado de uma hipótese e de como será testada (variável, controle, métrica, janela, critério, risco). Não é lista de ideias. Base 14.
23. **Stack** — conjunto de itens apresentados como pacote de valor. Não é prova. Base 18. **Bump** — oferta adicional no checkout. **Upsell** — oferta superior após a decisão principal. **Downsell** — alternativa menor após recusa. Registrar só quando observados.
24. **DNA da oferta** — relação entre as decisões que organizam a venda (persona → problema → mecanismo → nova oportunidade → Big Idea → promessa → prova → produto → oferta → funil), separada da superfície proprietária.
25. **Princípio transferível** — função que permanece quando se remove nome, headline, personagem, autoridade, números, preço, garantia e visual (ex.: reduzir culpa, tornar problema visível, demonstrar antes de afirmar, simplificar decisão).
26. **Sinal de escala** — repetição de anúncios, longevidade e arquitetura do funil observáveis na Biblioteca. Não comprova faturamento.
27. **Skin** — nome, ritual, personagem ou superfície que torna o sistema memorável. Sem lógica por trás, é só skin.
28. **Estágio de consciência** (Schwartz): inconsciente → consciente do problema → consciente da solução → consciente do produto → muito consciente. Registrar como leitura da comunicação, não rótulo permanente. **Sofisticação**: quais promessas e explicações concorrentes o mercado já viu.


=====
### ARQUIVO: references/vocabulario/hub-engenharia-de-ofertas.md
=====

# Hub de engenharia de ofertas (origem: skill agente-central-trm (vocabulário), consolidada em 13/09/2026)

# Engenharia de Ofertas — Trip Angle (hub)

Esta é a camada de regras e navegação. As etapas têm skills próprias:

| Fase | Pergunta | Skill a abrir | Entregável |
|---|---|---|---|
| 02 Inteligência | O que está rodando no mercado e com que sinal? | `agente-de-espionagem-trm` | Registro de evidências + Mapa de Oportunidades |
| 02→03 Leitura | Como essa oferta funciona por dentro? | `../../../agente-de-copy-trm/references/leitura-de-oferta.md` | Ficha de Fonte, Mapa Estratégico, Matriz Claim→Prova→Limite, DNA |
| 03 Modelagem | O que é transferível sem copiar? | `../../../agente-de-copy-trm/references/modelagem-sem-copia.md` | DNA funcional, matriz verde/amarelo/vermelho, hipótese, nova configuração, auditoria |
| 03 Criação | Como fica a nossa oferta? | `../../../agente-de-copy-trm/references/criacao-de-oferta-do-zero.md` | Dossiê, tese, Offer Card, Card Final, briefings para 04 Criativos e 05 Tráfego |
| 03→05 Teste | O que aprendemos primeiro? | `references/test-card.md` (aqui) | Test Card com variável, controle, métrica, janela, critério |
| 04 Criativos / 05 Tráfego | Como virar peça, campanha e decisão? | `agente-de-producao-de-criativos-trm` | Creative Card, matriz, roteiro, QA; economia unitária, tracking, diagnóstico, escala |

Fluxo por categoria do workspace: 02 Inteligência → 03 Engenharia → 04 Criativos → 05 Tráfego → registrar aprendizado e decisão em 07 Governança. Nada pula etapa: hooks só depois de situação, problema, desejo, crenças e mecanismo registrados.

## Por que a metodologia é assim

O workspace foi construído para que qualquer pessoa consiga auditar uma análise voltando da interpretação até o trecho original. Por isso o sistema separa observação de interpretação, alegação de prova, modelagem de cópia e hipótese de resultado. Uma análise que mistura essas camadas parece completa, mas não permite decidir nem aprender. Trate cada afirmação como algo que outra pessoa vai conferir.

## Rótulos de evidência (obrigatórios em toda análise)

Marque cada afirmação antes de interpretá-la:

- **ORIGINAL OBSERVADO** — aparece literalmente na fonte (preço, texto, estrutura).
- **ALEGAÇÃO DA COPY** — a peça afirma; não foi validado (todo claim de resultado, mecanismo, saúde, dinheiro).
- **OBSERVAÇÃO** — descrição verificável da estrutura (o anúncio abre com pergunta).
- **INTERPRETAÇÃO ESTRATÉGICA** — leitura fundamentada do analista.
- **PADRÃO IDENTIFICADO** — relação repetida em fontes independentes.
- **HIPÓTESE** — explicação ou aplicação ainda não testada.
- **NÃO MAPEADO NOS MATERIAIS** — a fonte não permite responder. Nunca preencher lacuna por inferência.
- Para Big Idea: CONFIRMADA / PROVÁVEL / NÃO CONFIRMADA (como tese comunicada, nunca como performance).

Anúncio ativo, contagem "N anúncios usam esse criativo", data de início e repetição de mecanismo são **sinal de escala**: mostram investimento e continuidade observáveis, não comprovam vendas, lucro, ROAS ou eficácia. Escreva "sinal de escala", nunca "está escalando" ou "domina".

## Sequência canônica (resumo)

Mercado → Persona → Situação → Problema → Dor → Desejo → Crenças → Soluções tentadas → Mecanismo do problema → Mecanismo da solução → Mecanismo único → Nova oportunidade → Big Idea → Ângulo → Promessa → Hook → Lead → Formato → Ad → Prova → Objeção → VSL → Produto → Oferta → Componentes → Funil → DNA → Engenharia reversa → Modelagem → Nova oferta → Test Card → Teste → Aprendizado.

Régua pedagógica em cada conceito: Entender → Identificar → Ver no Original → Decompor → Comparar → Modelar → Testar. Detalhes, portões P1–P8 e 47 dimensões em `references/sequencia-canonica.md`.

## Regras da casa que não se negociam

1. Modelagem não é cópia. Transfere-se função (verde), adapta-se padrão contextual com prova própria (amarelo), nunca se reutiliza expressão, nome, personagem, prova, número, preço, escassez ou identidade (vermelho).
2. Não inventar prova, depoimento, dado, escassez, credencial ou resultado. Se não existe, é HIPÓTESE ou NÃO MAPEADO.
3. Mecanismo é a lógica que sobra quando se remove o nome proprietário. Se não sobra lógica, é skin.
4. Uma variável por teste. Critério de decisão antes do resultado. Resultado inconclusivo não é vitória.
5. Claims de saúde, emagrecimento, dinheiro, comparação absoluta e garantia de retorno exigem revisão (CDC arts. 36–38, CONAR, Padrões de Publicidade da Meta). Registrar em 12 — Claims e Risco antes de qualquer teste.
6. Registrar fonte, data, ID, anunciante, país e versão em tudo. Sem linhagem, a análise não vale.
7. IA organiza, compara e gera variações; não substitui briefing, evidência nem decisão.

## Vocabulário

Use os termos do glossário (`references/glossario.md`): Hook ≠ Lead ≠ Headline; Ângulo ≠ Promessa ≠ Claim; Produto ≠ Oferta ≠ Funil ≠ VSL; Mecanismo do problema / da solução / único / skin; Stack, Bump, Upsell, Downsell só quando observados.

## Onde cada registro entra (19 bases técnicas)

Ordem de consulta: diagnóstico (01 Fontes, 02 Personas, 19 Mapa de Oportunidades) → mensagem (03 Hooks, 04 Ângulos, 05 Mecanismos, 15 Promessas, 16 Objeções) → criativos/percurso (06 Formatos, 08 Ads, 09 VSLs, 10 Funis) → oferta/risco (07 Ofertas, 11 Provas, 12 Claims e Risco, 17 Produtos, 18 Componentes) → modelagem/aprendizagem (13 Swipe File, 14 Test Cards). Esquemas de colunas em `references/bases-tecnicas.md`. Toda entrega deve dizer em qual base cada registro seria gravado.

## Formato de entrega

Comece por "Resumo de uma linha": "Para [pessoa em situação], a oferta apresenta [produto] como meio de alcançar [progresso], porque [mecanismo], sustentado por [prova observada], mediante [condições]." Depois, tabelas com a coluna de rótulo de evidência. Termine com: limites da leitura, claims pendentes de revisão, próxima hipótese e Test Card proposto. Tom da marca: direto, analítico, sem motivação vazia, sem promessa mágica.


=====
### ARQUIVO: references/vocabulario/rotulos-e-regras.md
=====

# Rótulos de evidência, controle de certeza e regras de risco

## Tabela de rótulos (Como Ler uma Oferta do Zero)
| Exemplo | Significado | Etiqueta |
|---|---|---|
| A página informa preço de R$ 97 | Aparece literalmente na fonte | ORIGINAL OBSERVADO |
| "Transformação em sete dias" | A peça afirma, não validado | ALEGAÇÃO DA COPY |
| O anúncio começa com uma pergunta | Descrição verificável da estrutura | OBSERVAÇÃO |
| A pergunta parece reduzir culpa | Leitura fundamentada do analista | INTERPRETAÇÃO ESTRATÉGICA |
| Três ofertas usam diagnóstico antes da promessa | Relação repetida em fontes independentes | PADRÃO IDENTIFICADO |
| O reframe pode aumentar avanço para a VSL | Aplicação ainda não testada | HIPÓTESE |
| Margem ou taxa de conversão ausentes | A fonte não permite responder | NÃO MAPEADO |

Cadeia: ORIGINAL → OBSERVAÇÃO → INTERPRETAÇÃO → DNA → PRINCÍPIO → HIPÓTESE → TEST CARD → RESULTADO.

## Controle de certeza (Como Criar do Zero)
| Status | Significado | Uso permitido |
|---|---|---|
| Observado | Aparece diretamente na fonte | Descrever com referência |
| Inferido | Conclusão razoável a partir de sinais | Apresentar como interpretação |
| Hipótese | Explicação ainda não testada | Levar a Test Card |
| Alegação/claim | Afirmação comercial que exige sustentação | Revisar prova e risco |
| Comprovado para esta oferta | Evidência direta, adequada e documentada | Comunicar dentro do alcance da prova |

Regra de síntese (voz do cliente): uma fala isolada é sinal; repetição entre fontes vira padrão; padrão testado pode virar aprendizado.

## Claim → Prova → Limite
| Claim | Prova apresentada | O que a prova sustenta | Limite / risco |
|---|---|---|---|
| Resultado | Depoimento ou caso | Experiência daquela fonte | Representatividade, autorização, contexto |
| Mecanismo | Demonstração ou explicação | Compreensão ou funcionamento observado | Não prova causalidade universal |
| Velocidade | Prazo declarado | Condição apresentada | Variação individual, base factual |
| Autoridade | Credencial | Qualificação no domínio | Autenticidade, pertinência |
| Escassez | Prazo ou quantidade | Limite comercial verificável | Falsa urgência, omissão |

Claims implícitos contam: o anunciante responde também por mensagens razoavelmente sugeridas.

## Compliance mínimo
- CDC (Lei 8.078/1990) arts. 36–38: identificação da publicidade, manutenção dos dados que sustentam a mensagem, vedação a publicidade enganosa ou abusiva; ônus da veracidade é do anunciante.
- CONAR — Código Brasileiro de Autorregulamentação Publicitária.
- Meta — Padrões de Publicidade: atributos pessoais, práticas enganosas, saúde (antes/depois, promessas de emagrecimento, nomes de medicamentos).
- Direitos autorais (Lei 9.610/1998): ideias e métodos não são protegidos; expressão concreta (texto, imagem, vídeo, voz, design) é.

Checklist antes de publicar: resultado anunciado dentro do que o produto entrega · evidência arquivada para números e declarações · exceção não tratada como típica · depoimentos com autorização e contexto · limitações não omitidas · garantia, preço, prazo e escassez verdadeiros · regras do canal, país e categoria · claims sensíveis revisados.

## Regras de estudo (Portal)
Original ≠ Observação ≠ Interpretação ≠ Modelagem ≠ Teste. Alegação de copy não é automaticamente fato. Modelagem não é cópia. Se algo não aparece nos materiais, registre NÃO MAPEADO NOS MATERIAIS. Não altere várias partes do projeto ao mesmo tempo sem registrar a variável. Não comece um novo projeto para fugir do desconforto de testar o atual.


=====
### ARQUIVO: references/vocabulario/sequencia-canonica.md
=====

# Sequência canônica, portões e checkpoints (Trip Angle)

Fonte: Jornada de Engenharia de Ofertas, Jornada Mestre, Portal Geral do Aluno, Agenda Oficial de Calls (Notion Trip Angle, set/2026).

## 1. As 29 etapas da Jornada de Engenharia de Ofertas

01 Como Ler uma Oferta · 02 Inteligência de Mercado · 03 Persona, Situação e Contexto · 04 Dor, Desejo e Crenças · 05 Soluções Tentadas · 06 Mecanismo do Problema · 07 Mecanismo da Solução · 08 Mecanismo Único · 09 Nova Oportunidade · 10 Big Idea · 11 Ângulo · 12 Promessa · 13 Hook · 14 Lead · 15 Formato · 16 Engenharia do Ad · 17 Prova · 18 Objeções · 19 Engenharia da VSL · 20 Produto · 21 Engenharia da Oferta · 22 Componentes · 23 Engenharia do Funil · 24 DNA da Oferta · 25 Engenharia Reversa · 26 Modelagem · 27 Criação de Nova Oferta · 28 Test Cards · 29 Teste e Aprendizado.

Regra: cada etapa leva a uma definição, uma base técnica, um exemplo real e uma ação. Se faltar informação, NÃO MAPEADO NOS MATERIAIS.

Ações por etapa (rota operacional clicável):
- 02 → 01 Fontes e Evidências + 19 Mapa de Oportunidades → separar fonte, observação e hipótese.
- 03 → 02 Personas → descrever somente a situação apresentada pela copy.
- 04 → 15 Promessas e Desejos + 16 Objeções e Crenças → separar dor observada, desejo declarado e crença pressuposta.
- 05 → 16 → registrar somente tentativas explicitadas.
- 06/07 → 05 Mecanismos → marcar como alegação da copy quando não validado; diferenciar mecanismo alegado de produto.
- 08 → Matriz Mestre → registrar como não confirmado quando for apenas diferenciação percebida.
- 09 → 19 Mapa de Oportunidades → formular o reenquadramento sem inventar mercado.
- 10 → resumir a tese central, não uma frase isolada.
- 11 → 04 Ângulos → distinguir enquadramento de promessa.
- 12 → 15 → qualificar resultados como alegação quando necessário.
- 13 → 03 Hooks → identificar função, não copiar frase.
- 14 → 09 VSLs → separar entrada de desenvolvimento da tese.
- 15 → 06 Formatos → distinguir formato, argumento e canal.
- 16 → 08 Ads → seguir o link do anúncio original e registrar a linhagem.
- 17 → 11 Provas → separar prova alegada de validação independente.
- 18 → 16 → registrar resposta da copy sem assumir eficácia.
- 19 → 09 → separar roteiro de sequência de funil.
- 20 → 17 Produtos → identificar entregável sem confundir com promessa.
- 21 → 07 Ofertas → separar produto, condições, stack, CTA e risco.
- 22 → 18 Componentes → diferenciar componente, bônus, bump, upsell e downsell quando observados.
- 23 → 10 Funis → desenhar somente etapas observadas.
- 24 → Matriz Mestre + Estudo de Caso → preencher o DNA e marcar lacunas.
- 25 → Como Modelar sem Copiar → extrair princípio antes da superfície.
- 26 → escolher uma variável e escrever nova hipótese.
- 27 → Como Criar do Zero → começar por mercado e persona, não por volume de hooks.
- 28 → 14 Test Cards → registrar variável, controle, métrica, janela, critério e risco.
- 29 → registrar resultado real e aprendizado; sem dados, manter como hipótese.

## 2. Jornada Mestre — 6 fases e 47 dimensões

- FASE 01 Inteligência de Mercado: 1 Mercado · 2 Persona · 3 Situação e Contexto · 4 Problema · 5 Dor · 6 Desejo · 7 Crenças · 8 Soluções Tentadas.
- FASE 02 Engenharia da Oportunidade: 9 Mecanismo do Problema · 10 Mecanismo da Solução · 11 Mecanismo Único · 12 Nova Oportunidade · 13 Big Idea.
- FASE 03 Engenharia da Mensagem: 14 Ângulo · 15 Promessa · 16 Hook · 17 Lead · 18 Formato · 19 Engenharia do Ad · 20 Prova · 21 Objeção.
- FASE 04 Engenharia da Venda: 22 Engenharia da VSL · 23 Progressão de Crença · 24 Produto · 25 Engenharia da Oferta · 26 Componentes · 27 Stack · 28 Garantia · 29 Condições.
- FASE 05 Engenharia do Funil: 30 Jornada · 31 Presell/Advertorial/Quiz · 32 VSL/Página · 33 Checkout · 34 Bump · 35 Upsell · 36 Downsell · 37 Pós-compra.
- FASE 06 Modelagem, Teste e Aprendizado: 38 DNA · 39 Engenharia Reversa · 40 Modelagem · 41 Nova Hipótese · 42 Test Cards · 43 Teste · 44 Leitura dos Resultados · 45 Iteração · 46 Aprendizado.

Checkpoints mestre (critério de passagem):
1. ENTENDER — define o conceito, diz com o que não confundir, aponta anterior e seguinte. Saída: definição + distinção + link ao conceito.
2. IDENTIFICAR — encontra o conceito em peça real e registra trecho, fonte, formato, função com classificação de evidência.
3. VER NO ORIGINAL — abre o Ad/VSL/página; se a fonte não existir, registra lacuna, não cria abertura plausível.
4. DECOMPOR — separa pessoa, situação, dor, desejo, crença, problema, solução, mecanismo único, skin, prova, produto, oferta, funil.
5. COMPARAR — compara duas ofertas por função, não por vocabulário: tese comum, tese específica, skin que não se copia, classificação da Big Idea, limite de evidência.
6. MODELAR — referência → DNA → princípio → variável → hipótese → reconstrução, com persona, história, mecanismo, prova, produto e oferta próprios.
7. TESTAR — Test Card com variável isolada, controle, métrica, amostra, janela e critério antes da execução.

Porta de retorno: falhou em Entender → volta ao conceito; em Identificar/Ver no Original → Estudo de Caso; em Decompor/Comparar → Matriz Mestre; em Modelar → Laboratório; em Testar → Test Card antes de nova variação.

## 3. Rota do projeto (Portal Geral do Aluno) — 7 etapas e checkpoints

| Etapa | Objetivo | Entregável | Checkpoint para avançar |
|---|---|---|---|
| 01 Fundamento e direção | definir o projeto único | Briefing do Projeto + um modelo de negócio | explica o que vende, para quem, qual problema, qual resultado |
| 02 Mercado, oportunidade e público | substituir achismo por leitura | mapa com mercado, público, dores, desejos, concorrentes, ofertas, oportunidade escolhida | existe evidência de demanda e justificativa para testar |
| 03 Oferta e proposta de valor | razão clara para comprar | Card da Oferta (público, problema, resultado, promessa, mecanismo, produto, entregáveis, bônus, preço, garantia, provas, objeções) | oferta específica, compreensível, defensável, sem frases genéricas |
| 04 Copy, ângulos e criativos | comunicação que gera atenção e ação | 3 ângulos, 3 hooks por ângulo, ≥3 criativos | cada criativo comunica público, dor/desejo, mecanismo e próxima ação |
| 05 Funil e conversão | caminho entre atenção e compra | mapa do funil: anúncio, página/quiz, checkout, oferta adicional, pós-compra | links, páginas, preços, pixels e ações conferidos de ponta a ponta |
| 06 Tráfego e lançamento | hipótese diante do mercado com teste controlado | Plano do Teste: hipótese, público, criativos, orçamento, duração, métricas, limite de perda, critério manter/alterar/encerrar | campanha publicada, rastreamento conferido, critérios registrados antes do resultado |
| 07 Tracking, análise e refinamento | dados viram decisão | Test Card concluído: hipótese, variável, período, investimento, dados, interpretação, decisão, próximo teste | sabe o que manter, alterar e qual nova hipótese testar |

Plano de 30 dias: dias 1–7 briefing/mercado/público; 8–14 oferta; 15–21 copy, criativos, funil, tracking; 22–30 lançamento, dados, refinamento.

Rota por situação: começando do zero → Etapa 01; tem ideia sem oferta → 02; tem oferta e não vende → 03 + diagnóstico; vende e quer conversão → 04–05; vende e quer escalar → 06–07.

## 4. Portões do programa (Agenda de Calls) — P1 a P8

| Portão | Calls | Saída obrigatória | Não avança quando |
|---|---|---|---|
| P1 Direção | 01 | Briefing e projeto único | tenta executar vários projetos |
| P2 Mercado | 02–03 | Dossiê de mercado e pessoa em situação | opinião sem fonte ou persona genérica |
| P3 Leitura | 04–05 | DNA da oferta e tese estratégica | observação, interpretação e hipótese misturadas |
| P4 Modelagem e oferta | 06–07 | Nova hipótese, Offer Card, produto e prova | cópia, claim sem prova ou produto incompatível |
| P5 Mensagem e venda | 08–09 | Matriz de mensagem, ativo e funil | copy não conduz à mesma promessa e entrega |
| P6 Criativo | 10 | Creative Card, roteiro, QA e Test Card | peça bonita sem hipótese |
| P7 Teste e escala | 11–12 | Tracking, plano de teste e decisão | sem economia, medição ou limite de perda |
| P8 Aprendizado | 13 | Dossiê final e próximo ciclo | resultado não convertido em aprendizado |

Status padronizados: AVANÇA / REVISA / RETORNA / BLOQUEADO (claim, originalidade, tracking, economia ou entrega impedem) / CONCLUÍDO.

Antes de pedir ajuda (hot seat): projeto e versão, etapa atual, entregável produzido, evidência observada, decisão a tomar, pergunta específica.

## 5. Sprint de 14 dias (módulo 03 Engenharia)

1–2 Resumo estratégico + padrões · 3 Estágio de consciência + ponte · 4–5 Offer Card + provas + riscos · 6–7 Briefing + estrutura de copy · 8–9 Roteiro de página/VSL/conversa · 10 Mapa do funil + QA · 11–12 Scripts, matriz de objeções, follow-up · 13 Claims, limites e correções · 14 Test Card + briefings 04/05.


=====
### ARQUIVO: references/vocabulario/test-card.md
=====

# Test Card — modelo e regras da casa

Teste transforma hipótese em comparação executável. Exige variável isolada, controle, canal, audiência, destino, janela, amostra, métrica primária/secundária, critério de vitória, critério de descarte, resultado e aprendizado separados. Sem janela ou métrica há intenção de teste, não teste.

## Template (preencher antes de publicar)

- Nome do teste (ID: `<OFERTA>-TC0n — <o que compara>`)
- Oferta e versão
- Hipótese: "Se eu mudar X mantendo Y, espero Z porque…" (específica, rastreável à observação, limitada ao contexto, falsificável, compatível com o produto, proporcional à prova, separada de promessa pública)
- Evidência que originou a hipótese (fonte, ID, linhas)
- O que estamos testando (uma variável): segmento · situação · promessa · mecanismo · ângulo · hook · lead · prova · preço · garantia · formato · página/destino · criativo · CTA · sequência
- Variação A / Variação B / (C somente se definida)
- Controle: versão original observada, mantendo oferta, formato, CTA, destino e condições constantes. Sem controle real, registrar a limitação antes do teste.
- O que não pode mudar: oferta, público, destino, condições, período, critério de medição
- Persona · Audiência · Canal (mesmo canal e posicionamento nos braços) · Destino (idêntico nos braços)
- Orçamento · Limite de perda
- Amostra planejada: dois braços A/B; mínimo de 100 cliques por braço e distribuição equivalente de tráfego. Não iniciar se a amostra ficar desequilibrada.
- Janela: 7 dias de tráfego simultâneo, ou até ambos os braços atingirem a amostra mínima, o que ocorrer por último.
- Métrica principal (definir antes: CTR qualificado, retenção, avanço, conversão, CPA)
- Métricas secundárias: retenção inicial, CPC, avanço para a próxima etapa, conversão observada, sinais de reclamação/compliance
- Critério de vitória: declarar vencedor somente se uma variação superar o controle em pelo menos 20% na métrica principal predefinida, sem piora superior a 10% nas secundárias e sem novo risco de compliance. Sem dados, não há vencedor.
- Critério de descarte: descartar somente por falha de rastreamento, violação de integridade da fonte, erro de entrega ou desequilíbrio de amostra; não por impressão subjetiva.
- Critério para manter / alterar / encerrar
- Risco / claim revisado (12 — Claims e Risco)
- Prova necessária
- Confiabilidade: Nível D — Hipótese (até haver dados)
- Status: Rascunho / Pronto / Em execução / Concluído
- Resultado (observado) · Interpretação (separada) · Decisão · Aprendizado · Próximo teste

## Métricas por camada (leitura correta)
- Atenção: retenção inicial, hook rate, impressão qualificada.
- Clique: CTR e CPC, sempre com o objetivo.
- Ativo: avanço por seção, lead, formulário, conversão, abandono.
- Checkout: início, abandono, compra.
- Venda (consultivo): comparecimento, qualificação, avanço, fechamento, ciclo.
- Economia: CPA/CAC, receita líquida, margem, ticket, reembolso.
- Entrega: ativação, uso, conclusão, satisfação, suporte, retenção.

CTR baixo não prova produto ruim; conversão baixa não prova falta de urgência; fechamento baixo não prova vendedor fraco. Localize a etapa, colete evidência, formule a próxima hipótese. "A versão B vendeu mais nesta janela" é observação; "vendeu mais por causa do mecanismo" é interpretação que pode exigir novo teste.

## Escada de evidência (o que cada sinal indica)
0 opinião/elogio → 1 atenção e clique → 2 lead ou resposta → 3 início de checkout/aplicação → 4 pagamento → 5 uso e conclusão → 6 recompra, retenção ou indicação. Uma venda isolada não prova escala, margem ou retenção.

## Erros que invalidam o teste
Mudar muitas coisas; parar cedo; ignorar amostra; escolher métrica depois; tratar correlação como causalidade; declarar vitória por um resultado; esconder inconclusividade; chamar backlog de experimento executado ou hipótese de aprendizado.
