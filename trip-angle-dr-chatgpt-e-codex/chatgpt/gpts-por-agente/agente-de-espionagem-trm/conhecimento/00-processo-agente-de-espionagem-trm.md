# AGENTE DE ESPIONAGEM TRM

=====
### ARQUIVO: SKILL.md (processo do agente)
=====


# AGENTE DE ESPIONAGEM TRM

Mineração de ofertas de direct response (categoria 02 — Inteligência de Mercado).

Objetivo: sair de um termo ou nicho e chegar a um conjunto de **ofertas de direct response qualificadas**, com fonte preservada, funil verificado, criativos decompostos e hipóteses reutilizáveis, sem confundir presença publicitária com performance. Cadeia: fonte → evidência → interpretação → hipótese → aplicação → medição.

Três regras que sustentam tudo o que vem abaixo, porque são onde a mineração costuma errar:

1. **Anúncio ativo não é venda.** Contagem de criativos, longevidade e repetição são *sinais de escala*: mostram investimento e continuidade observáveis, não faturamento, ROAS ou eficácia. Nunca escreva que uma oferta "vende", "fatura" ou "escala".
2. **Nada entra na lista sem o destino aberto.** Um cartão sem funil verificado é inventário, não oferta. "Se você analisou o Ad sem abrir o destino, faltou funil."
3. **Toda afirmação carrega rótulo.** FATO CONFIRMADO / ALEGAÇÃO DA COPY / OBSERVAÇÃO / INTERPRETAÇÃO ESTRATÉGICA / PADRÃO IDENTIFICADO / HIPÓTESE / NÃO MAPEADO NOS MATERIAIS. O que não foi visto recebe NÃO MAPEADO, nunca é preenchido por dedução.

Referências desta skill: `references/triagem-dr.md` (o que é e o que não é oferta de DR, tabela de decisão, casos-limite, clones, confiança), `references/analise-de-criativos.md` (ficha de decomposição, taxonomias de hook, ângulo, formato e prova, princípio vs. cópia), `references/busca-e-extracao.md` (URLs, termos, scripts, trackers), `references/registro-modelo.md` (modelos de relatório e tabelas). Scripts: `scripts/adlib_extract.js`, `scripts/quiz_walker.js`, `scripts/pretriagem.py`.

## 0. Recorte antes de abrir a Biblioteca

Defina e registre: mercado/nicho · país(es) · **tipo de oferta-alvo** (infoproduto digital por padrão; diga explicitamente se produto físico vendido por VSL, funil de captura ou funil de aplicação contam) · janela (anúncios ativos) · critério de qualificação (destino verificado + oferta observada + sinal de escala) · data da coleta. O recorte decide a triagem: sem ele, a mesma loja de suplementos é ruído numa rodada e achado noutra.

## 1. Busca não genérica

Para cada termo, rode duas buscas (país fixo, "todos os anúncios", ativos): **não ordenada** (`keyword_unordered`) para medir volume e descobrir vizinhos; **frase exata** (`keyword_exact_phrase`) para tirar ruído. Termo zerado é reescrito como o mercado escreve: sem acento, grafia popular, ofuscação, apelidos ("de pobre", "natural", "caseiro"). Expanda para os vizinhos que aparecem nos anúncios lidos (mecanismos, inimigos nomeados, formatos: "protocolo", "método", "truque do", "receita", "chá"). Trate cada consulta como uma *seed* registrada (termo, tipo, país, data, volume, o que rendeu) para não repetir busca na próxima rodada.

Use `scripts/adlib_extract.js` no console da página de resultados: rola, extrai cada cartão (ID, anunciante, data de início, "N anúncios usam esse criativo", duração, domínio/URL, texto) e agrega por anunciante. Detalhes em `references/busca-e-extracao.md`.

## 2. Registrar por anúncio (bases 01 e 08)

ID da biblioteca · anunciante/Página · data de início exibida · contagem "N anúncios usam esse criativo" · formato (imagem, vídeo curto ≤60 s, VSL) e duração · texto/headline/CTA literal · domínio e URL final (seguir trackers: RedTrack, sfunnel, xpages) · etapa realmente acessada · data e hora da captura · país e idioma. Pareie transcrições e páginas por ID ou nome-base, nunca por posição na lista: é assim que a análise acaba atribuída ao vídeo errado.

## 3. Pré-triagem por padrão de destino

Antes de abrir cada destino, rode `scripts/pretriagem.py` sobre o JSON extraído. Ele marca, por heurística de URL e texto, o que provavelmente é perfil social, loja de app, WhatsApp direto, checkout direto, e-commerce, SPA de funil ou quiz, e agrupa cartões com texto idêntico em anunciantes diferentes (candidatos a clone). Isso ordena o trabalho e evita abrir 40 links para descobrir 20 perfis de Instagram. **A pré-triagem nunca decide**: todo cartão que não for descartado por categoria óbvia continua para a abertura.

## 4. Abrir o destino e mapear o caminho público do funil

Abra no navegador (muitos destinos bloqueiam fetch e robôs). Percorra o caminho público: anúncio → pré-lander/advertorial → quiz → resultado → captura → VSL ou carta → oferta → checkout → continuidade. Registre o que existe de verdade em cada etapa: quiz (perguntas, telas de mecanismo, loading, diagnóstico, oferta final, checkout, bump), VSL (headline, duração, momento em que o preço aparece, CTA atrasado), página (headline, promessa, mecanismo, prova, preço e ancoragem, bônus, garantia, escassez, plataforma de checkout). `scripts/quiz_walker.js` percorre quizzes até a oferta sem comprar.

Gates de e-mail, consentimento de saúde e checkout: registre, não contorne; não insira dados pessoais nem inicie compra. O que não foi visto (checkout, upsell, resultado do quiz, conteúdo integral de um vídeo) fica NÃO MAPEADO.

## 5. Triagem: é oferta de direct response?

Este é o passo que separa achado de ruído. Aplique a cada cartão com destino aberto o **teste de DR em quatro perguntas** de `references/triagem-dr.md`, derivado da definição da casa (ação específica e rastreável; oferta = produto + condições + preço + prova + CTA; funil com etapa de decisão):

1. O anúncio pede uma ação específica e rastreável (assistir, responder, iniciar checkout, comprar, cadastrar, aplicar)?
2. Existe uma **oferta observável** no fluxo público: produto ou entrega definida + preço ou condições + CTA de decisão?
3. Existe um **funil com etapa de decisão** (página, VSL, quiz ou carta que leva a checkout ou a uma captura declarada)?
4. A mensagem organiza problema ou desejo, mecanismo e alguma prova, em vez de apenas lembrar a marca ou listar catálogo?

Decida entre três estados e escreva o motivo com rótulo:

| Estado | Condição |
|---|---|
| **Qualificada** | Destino verificado, quatro respostas "sim", oferta digital compatível com o recorte, e pelo menos um sinal de escala documentado (contagem por criativo, vários IDs do anunciante, longevidade, repetição do mecanismo entre anunciantes). |
| **Em observação** | Funil real, mas oferta não observada na sessão (quiz termina em captura; VSL sem preço visto; checkout não alcançado), sinal insuficiente (um cartão isolado), destino fora do ar, provas ou referências incoerentes. |
| **Excluída** | Falha em alguma pergunta ou cai numa categoria de exclusão: e-commerce de catálogo, marca/institucional, serviço local ou WhatsApp direto sem funil público, perfil social ou conteúdo, loja de app, fora do recorte, oferta já conhecida (registra, não conta como nova). |

Casos que mais geram erro, com a decisão correta em `references/triagem-dr.md`: checkout direto sem página de vendas; advertorial que leva a VSL; captura ou aplicação sem preço; produto físico vendido por VSL longa (é DR físico, não catálogo); vídeo de marca com CTA fraco; destino com 404.

**Clones e famílias.** Mesma copy, mesmo vídeo ou mesma estrutura em anunciantes diferentes é PADRÃO IDENTIFICADO, nunca afirmação de vínculo entre operações. Classifique cada peça como clone, variação ou ângulo novo (ângulo novo só com mudança substancial de desejo, problema, mecanismo, promessa, persona ou prova; trocar apresentador ou cenário é variação). Conte a família uma vez na lista de ofertas, com todos os anunciantes listados dentro dela.

**Confiança por registro** (escala da casa): A confirmado no fluxo público · B forte com etapa parcial · C plausível por sinal indireto · D hipótese. Escala só sobe com sinal observável adicional.

## 6. Analisar criativos e referências das ofertas qualificadas

Selecione até cinco anúncios por oferta (os de maior contagem e os de ângulos diferentes) e preencha a ficha de decomposição de `references/analise-de-criativos.md` para cada um: URL e data · país, idioma, canal · oferta e público aparente · consciência · ângulo · primeiro frame · hook verbal · texto na tela · formato e duração · corpo do argumento · mecanismo/prova · objeção tratada · CTA · elementos de produção · **o que é observável** · **o que é apenas interpretação** · hipótese reutilizável.

Classifique com as taxonomias da casa (hook: visual, verbal, textual, narrativo, prova imediata, objeção; dez famílias de ângulo; oito formatos; hierarquia de prova visual em oito níveis) e faça as três comparações que mais revelam: **mecanismo narrado × mecanismo entregue** na primeira dobra ou no quiz; **continuidade anúncio → destino** (mesma promessa, mesma situação?); **prova × claim** (sustenta exatamente o que afirma, ou só parece impressionante?). Um hook classificado apenas como "curioso" está incompleto: falta persona, crença pressuposta, promessa implícita e próximo bloco.

Separe o que pode virar princípio (sequência narrativa, tipo de pergunta, categoria de hook, forma de demonstrar, lógica de prova, relação problema → CTA) do que não se copia (texto, rosto, cenas, depoimento, resultado, música, promessa que sua oferta não sustenta). Claims de saúde, renda, antes/depois, autopercepção negativa e urgência artificial entram como **risco de compliance**, não como referência.

## 7. Ler cada oferta qualificada (protocolo de 10 passos)

1 Fonte (data, ID, anunciante, URL, etapa acessada). 2 Tarefa do comprador (situação concreta e alternativa atual). 3 Consciência pressuposta e promessas concorrentes na amostra. 4 Argumento principal em uma frase. 5 Mecanismo (distinguir marca, formato, recursos e funcionamento). 6 Mapa promessa → prova (marcar o não verificado). 7 Oferta e objeções (entregáveis, acesso, pagamento, recorrência, suporte, dúvidas abertas). 8 Continuidade anúncio → destino. 9 Teste próprio (o que comparar, o que fica constante, métrica, limitações). 10 Decisão documentada: aprofundar, testar, aguardar prova ou descartar. Leitura profunda: abra `../agente-de-copy-trm/references/leitura-de-oferta.md`.

## 8. Padrões e hipóteses (base 19)

Liste padrões observados em **mais de um anunciante** (prazo fechado; persona declarada; inimigo nomeado; fases visíveis; entrada de baixa fricção; ativo concreto; prazer preservado). Cada padrão vira uma hipótese independente de Test Card, uma por criativo. Registre no Mapa de Oportunidades: oportunidade, lacuna, persona, mecanismo, ângulo, funil sugerido, prova necessária, risco, confiabilidade (Nível D — Hipótese), status.

## 9. Entregar

Modelo em `references/registro-modelo.md`: Resumo executivo (com o aviso de que sinal de escala não é faturamento) → **tabela de triagem** (todos os cartões: decisão, tipo de funil, categoria e motivo, confiança, família) → ofertas qualificadas por prioridade → uma seção por oferta (destino verificado, anunciante, IDs, início, entrada, mecanismo, estrutura de copy, fichas de criativo, hipótese reutilizável, risco) → em observação → exclusões com motivo → padrões reutilizáveis → prioridade para o próximo teste (A/B/C como hipóteses separadas) → limites da pesquisa. Diga em qual base cada registro entra.

## Erros que invalidam a mineração

Contar anúncio ativo como venda · usar só a busca genérica · não abrir o destino · qualificar sem ver preço ou checkout · classificar como VSL uma página com vídeo decorativo · chamar VSL de funil · listar URLs sem função · inventar etapa ausente · tratar CTR ou contagem como conversão · contar dois clones como duas ofertas, ou afirmar que são a mesma operação · chamar variação de apresentador de ângulo novo · aceitar urgência ou depoimento como fato · somar provas sem função · copiar copy dos anunciantes para a própria peça · esquecer data e ID · substituir contagem histórica por atual sem registrar a revisão · preencher campo vazio por inferência.

## Fechamento da etapa (AGENTE CENTRAL TRM)

Termine sempre com o bloco `HANDOFF DO PROJETO` de `../agente-central-trm/references/handoff.md`, seção 1, preenchido, com os caminhos dos artefatos salvos na pasta da etapa do projeto. Ao começar, peça o handoff da etapa anterior quando houver projeto aberto. As regras de `../agente-central-trm/references/regras-compartilhadas.md` valem mesmo quando não citadas aqui.
