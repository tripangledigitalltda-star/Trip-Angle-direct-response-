# AGENTE DE ESPIONAGEM TRM

Identificador: agente-de-espionagem-trm
Quando usar: AGENTE DE ESPIONAGEM TRM: minera ofertas DR na Biblioteca de Anúncios, abre e mapeia funis, tria o que é DR, agrupa clones e entrega ofertas qualificadas. Use ao minerar ou espionar ofertas.

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


=====
### ARQUIVO: references/analise-de-criativos.md
=====

# Análise de criativos e referências (swipe diagnóstico)

Origem: "04 — Criativos e Biblioteca Visual" (seções 1.1, 2.2, 3.2, 3.3, 4.2, 4.3, 4.4), Conceitos Canônicos AD, HOOK, FORMATO, ÂNGULO e PROVA, e "Mineração Avançada — Meta Ads" da Trip Angle. Campos e listas são literais salvo indicação.

## 1. Unidade de análise

"Ad é a unidade de entrada que interrompe atenção, seleciona uma pessoa, estabelece uma tensão e conduz a um próximo passo do funil. É uma peça, não a campanha inteira." "Sua função é qualificar e iniciar a jornada, não provar sozinho a eficácia da oferta." Analise o Ad junto com o destino: "Se você analisou o Ad sem abrir o destino, faltou funil."

Cobertura: cinco Ads por oferta qualificada, escolhidos entre os de maior contagem e os que parecem ângulos diferentes. Pareie cada ficha ao ID; nunca por posição na lista.

## 2. Ficha de decomposição (uma por Ad)

| Campo | O que preencher |
|---|---|
| URL e data da coleta | URL do anúncio na Biblioteca, ID, data e hora |
| País, idioma e canal | Como exibido |
| Oferta e público aparente | A quem a peça fala e o que oferece, como aparece |
| Estágio de consciência | Não consciente / problema / solução / produto / muito consciente, com a evidência textual |
| Ângulo | Família (seção 4) e os elementos enfatizados e omitidos |
| Primeiro frame | O que aparece antes de qualquer fala |
| Hook verbal | Primeira frase, literal |
| Texto na tela | Literal |
| Formato e duração | Tipo (seção 5) e duração; se só houver "vídeo", não especificar mais sem suporte |
| Corpo do argumento | Sequência: contexto → problema → mecanismo → prova → oferta → CTA, ou a ordem observada |
| Mecanismo/prova | O que a copy alega como causa e o que apresenta como prova |
| Objeção tratada | Qual dúvida a peça responde |
| CTA | Ação pedida e destino |
| Elementos de produção | Pessoa, cenário, B-roll, legenda, ritmo, som |
| **O que é observável** | Somente o que está na peça e no destino, com rótulo OBSERVAÇÃO ou FATO CONFIRMADO |
| **O que é apenas interpretação** | Leituras do analista, com rótulo INTERPRETAÇÃO ESTRATÉGICA |
| Hipótese reutilizável | Função transferível, escrita como hipótese, não como frase para copiar |

Campos da auditoria da Mineração Avançada que complementam a ficha: fato observado · inferência · fonte · data de captura · confiança (A–D) · sinal de escala · **gap promessa/entrega** · risco de compliance · o que preservar · o que substituir · o que não reutilizar · próximo teste.

## 3. Hook

Tipos (04, 4.2): **Visual** (movimento, demonstração, objeto, contraste, tela) · **Verbal** (pergunta, observação, diagnóstico, declaração específica) · **Textual** (frase curta que contextualiza sem som) · **Narrativo** (tensão, erro, tentativa, descoberta, transformação) · **Prova imediata** (resultado ou processo verdadeiro já no início) · **Objeção** (começa pela dúvida que o público já tem).

Ficha do hook (conceito canônico): tipo · padrão de atenção · quebra de padrão · curiosidade · tensão · persona selecionada · crença pressuposta · promessa implícita · ângulo · lead · formato · consciência · próximo bloco. "Se você só classificou como 'curioso', faltaram persona, crença, promessa implícita e próximo bloco." "Curiosidade sem relação com o corpo cria ruptura e pode atrair clique sem fit." "Não reescreva nem aumente o claim; descreva atenção, tensão e promessa implícita."

## 4. Ângulo

Famílias (04, 3.2): Situação reconhecível · Problema ou custo · Mecanismo · Nova oportunidade · Demonstração · Prova · Objeção · Comparação · Identidade ou aspiração · História.

Elementos (conceito canônico, 11): tese · enquadramento · situação · desejo · inimigo · emoção · contraste · reframe · mecanismo · persona · nível de consciência. "Pergunte qual item foi enfatizado e qual foi omitido." "Em cada item, marque literal, padrão ou interpretação." "Um ângulo completo mostra seleção, omissão e ordem; uma lista de adjetivos não demonstra enquadramento." Não atribua inimigo que não aparece; não confunda tema com ângulo nem formato com ângulo.

## 5. Formato

Tipos (04, 4.3) com o risco comum de cada um: UGC/creator-led (fingir espontaneidade) · Talking head (monólogo sem apoio visual) · Demonstração (mostrar sem explicar) · Screen recording (texto pequeno) · Estático (excesso de texto) · Carrossel (primeiro cartão sem motivo para avançar) · Testimonial/case (resultado sem contexto ou permissão) · Animação/motion (estética que distrai). Conceito canônico acrescenta: unboxing, entrevista, VSL, live, página.

Elementos: tipo · abertura · primeira cena · arquitetura · edição · ritmo · duração · fala · B-roll · visual · autoridade · demonstração · prova · CTA · relação com o argumento · estágio do funil. "sem inferir performance apenas por duração, estilo ou aparência." Não chame canal de formato; não confunda VSL com funil.

## 6. Prova

Hierarquia visual (04, 3.3), do mais forte ao mais fraco: 1 produto ou processo em funcionamento · 2 demonstração comparável · 3 dado próprio com contexto e método · 4 caso verificável · 5 depoimento genuíno e autorizado · 6 credencial relevante · 7 explicação · 8 afirmação sem suporte.

Decomposição (conceito canônico): afirmação → prova apresentada → fonte → tipo → função → limite → objeção respondida. "'A copy mostra' é diferente de 'está comprovado'." "Depoimento, autoridade ou número podem ser prova alegada, não validação causal." "não somar fontes distintas como uma prova única." Prova não independente recebe ALEGAÇÃO DA COPY. Garantia não é evidência de resultado.

## 7. As três comparações que mais revelam

1. **Mecanismo narrado × mecanismo entregue.** O que o anúncio diz que causa o problema e resolve, contra o que a primeira dobra, o quiz ou a VSL realmente explicam e vendem. Diferença grande é gap promessa/entrega.
2. **Continuidade anúncio → destino.** Mesma promessa, mesma situação, mesmo nível de consciência? Hook que o corpo não entrega e página que muda de promessa são quebras.
3. **Prova × claim.** "A prova sustenta exatamente o claim, ou apenas parece impressionante?" Antes/depois não verificável, resultados extremos sem contexto, números escolhidos e depoimentos vagos não são prova suficiente.

## 8. Clone, variação ou ângulo novo

Agrupe os Ads de uma oferta por função do hook e problema declarado. Ângulo novo só com mudança substancial de desejo, problema, mecanismo, promessa, persona ou prova; troca de apresentador, cenário ou avatar é variação de execução. Copy ou vídeo idênticos em anunciantes diferentes é clone, registrado como família (ver `triagem-dr.md`, seção 6).

## 9. O que vira princípio e o que não se copia (04)

Pode reaproveitar como princípio: sequência narrativa · tipo de pergunta · categoria de hook · forma de demonstrar · lógica de prova · ritmo ou contraste · relação entre problema e CTA.

Não copie: texto integral · identidade, personagem ou rosto sem direito · cenas e composição reconhecíveis · depoimento ou resultado · logo, música, vídeo e propriedade intelectual · promessa que sua oferta não sustenta. Modelagem é sempre HIPÓTESE até o Test Card.

Compliance: "claims de renda rápida, saúde, before/after, autopercepção negativa, controle psicológico, urgência artificial e depoimentos não auditados devem ser marcados como risco, não copiados." Aprovação na plataforma não substitui conformidade legal.

## 10. Erros de leitura (literais)

AD: tratar CTR como conversão; ignorar destino; avaliar Ad fora do funil; copiar hook sem lead; chamar qualquer criativo de Ad. HOOK: considerar todo início como hook; confundir choque com relevância; avaliar só pela curiosidade; não apontar a crença pressuposta. FORMATO: copiar estética sem entender argumento; achar que duração explica resultado; avaliar somente a primeira cena. ÂNGULO: confundir tema com ângulo; tratar emoção como mecanismo. PROVA: confundir presença com qualidade; aceitar autoridade como prova causal; somar provas sem função; chamar garantia de evidência de resultado. Criativos: confundir imagem bonita com criativo estratégico; copiar anúncio sem entender o princípio; medir apenas CTR.


=====
### ARQUIVO: references/busca-e-extracao.md
=====

# Busca e extração na Biblioteca de Anúncios da Meta

## URLs de busca
- Não ordenada: `https://www.facebook.com/ads/library/?active_status=active&ad_type=all&country=BR&q=<termo>&search_type=keyword_unordered&media_type=all`
- Frase exata: `...&q=%22<termo>%22&search_type=keyword_exact_phrase&media_type=all`
- Detalhe de um anúncio: `https://www.facebook.com/ads/library/?id=<ID>` (abre modal; anúncios de WhatsApp mostram "Enviar mensagem pelo WhatsApp" e não expõem link).
- Colômbia: `country=CO`; termos em espanhol ("gelatina bariátrica", "reinicio metabólico", "plan imprimible").
- Google Ads Transparency Center: busca por anunciante ou domínio, região e período, para confirmar presença fora da Meta.

## Estratégia de termos
1. Termo pedido (acentuado e sem acento).
2. Grafia popular e ofuscada (monjaro, m0unj4r0, "canetinha").
3. Apelidos de mecanismo ("de pobre", "natural", "caseiro", "do jeito certo").
4. Formatos ("protocolo", "método", "truque do", "receita", "chá", "sopa", "gelatina", "desafio").
5. Vizinhos que aparecem nos anúncios lidos (inimigos nomeados, ingredientes, prazos).
6. Assinaturas de operação (domínios lovable.app, vercel.app, netlify.app, xpages.co, .shop; plataformas Wiapy, Cakto, PerfectPay, Kiwify, Hotmart, Lastlink) para achar clones da mesma operação.

## Extração
Cole `scripts/adlib_extract.js` no console (ou via ferramenta de JavaScript do navegador) na página de resultados. Ele:
- rola a página N vezes para carregar mais cartões;
- localiza cada cartão pelo texto "Patrocinado" + "Identificação da biblioteca";
- extrai id, start, n (contagem de criativos), page (anunciante), dom (domínio em caixa alta exibido), u (URL de destino decodificada do l.php quando existe), dur (duração do vídeo), body (texto);
- agrega por anunciante: cards, maxN, sumN, datas, domínios, URLs, durações, amostras de texto, ordenado por sumN.

Interprete `sumN` como sinal de volume dentro da busca, não como total do anunciante. Cartões sem texto costumam ser vídeo-only com link escondido em "Ver resumo".

## Quiz e páginas
- Muitos destinos são SPA (lovable, vercel): use o navegador; `fetch` retorna só o título.
- Trackers: seguir `Location` de RedTrack (`red.track.*`), `click.*/sf/?sfunnel=`, `insight.*`; registrar URL final.
- `scripts/quiz_walker.js` percorre etapas clicando a primeira opção, tratando multi-select (botão "Continuar"), sliders e telas de loading; para antes de botões de compra e de links externos; devolve o texto de cada tela e a URL final. Etapas com botões de imagem exigem clique manual (localizar por acessibilidade).
- Registrar por quiz: número de telas, perguntas literais, tela de mecanismo, prova (áudio, depoimento), diagnóstico (IMC, "zona de alerta"), loading de personalização, oferta (preço, ancoragem, bônus, garantia, escassez, timer), checkout (plataforma, bump).

## Sinais de operação clonada
Mesma copy em anunciantes diferentes; mesmo app em dois domínios; páginas com nomes de chef/nutri trocados e estrutura idêntica (2 planos, 5 bônus, "N pessoas já transformaram", 4.9 de N avaliações, timer com data do dia). Registrar como PADRÃO IDENTIFICADO, sem afirmar vínculo entre as operações.

## Limites obrigatórios no relatório
Amostra não exaustiva; contagens e datas mudam; checkout, order bump, upsell e entrega comprada não auditados salvo quando vistos; alegações de saúde/dinheiro não validadas; anúncio ativo ≠ venda.

## Seeds e snowball
Registre cada consulta como uma seed: termo | tipo de busca (não ordenada / frase exata) | país | data | volume aproximado exibido | o que rendeu (IDs, vizinhos descobertos, zero). A tabela de seeds evita repetir buscas zeradas na rodada seguinte e transforma cada hipótese ("o mercado escreve 'canetinha'") em uma consulta rastreável. Descoberta também por marca, domínio, frase de hook, mecanismo, promessa, idioma e anunciante (SOP da Mineração Avançada). Cobertura de análise: cinco Ads por oferta qualificada.

## Pré-triagem
`scripts/pretriagem.py cartoes.json` lê a saída do extrator e sugere uma rota por cartão (perfil social, loja de app, WhatsApp direto, checkout direto, e-commerce provável, quiz, SPA, página/VSL), calcula há quantos dias o anúncio está ativo e agrupa textos idênticos em anunciantes diferentes. Serve para ordenar a abertura dos destinos; não substitui a abertura.


=====
### ARQUIVO: references/registro-modelo.md
=====

# Modelos de registro (páginas de mineração no Notion Trip Angle)

## A. Página "Nova Mineração — Funis e Sinais de Escala" (modelo literal, 07 — Nova Mineração Brasil + Colômbia)

Cabeçalho: "Coleta ao vivo na Biblioteca de Anúncios da Meta, com destinos abertos e verificados em <data>." · Mercados · Status: anúncios ativos · Critério: funil verificado + sinais de escala · Fonte.

**Resumo executivo** — quantas ofertas qualificadas, quantas em observação, por quê. Aviso fixo: "Sinal de escala não é comprovação de faturamento. Repetição de anúncios, longevidade e arquitetura do funil mostram investimento e continuidade observáveis, mas não comprovam vendas, lucro ou ROAS."

**Ofertas qualificadas** — tabela: Prioridade | Funil confirmado | Sinal observado | Mercado | Oferta.

**Uma seção por oferta**:
- Destino verificado · Anunciante observado · IDs observados · Início exibido
- Entrada (o que a primeira tela faz)
- Mecanismo de entrada / mecanismo comercial (como a copy explica)
- Estrutura de copy (identidade → inimigo → prazo → prazer preservado, etc.)
- Sinal de mercado (volume da busca, agrupamentos observados) com a ressalva "confirma repetição do mecanismo, mas não vínculo entre as operações"
- Hipótese reutilizável (função, não frase)
- Risco (alegações não validadas)

**Ofertas em observação** — destino, ID, início, motivo (um só cartão; provas não auditadas; referências incoerentes).

**Exclusões relevantes** — o que ficou fora e por quê (já conhecida; produto físico; WhatsApp direto; destino quebrado).

**Padrões reutilizáveis para o próximo teste** — lista numerada (prazo fechado; persona declarada; inimigo nomeado; fases visíveis; entrada de baixa fricção; ativo concreto; prazer preservado).

**Prioridade para o próximo teste** — primeira tese + Variação A/B/C como hipóteses independentes: "Não misturar as três causas no mesmo criativo."

**Limites da pesquisa** — amostra, mutabilidade, o que não foi auditado.

## B. Página "Registro de Evidências — N anúncios" (modelo)
Tabela por cartão: ID | Anunciante | Data de início | Agrupamento (N criativos) | Formato/duração | Destino | Texto (literal, truncado) | Etapa acessada | Observações. Rodapé: "Foram documentados N cartões distintos: X da busca ampla e Y da página <anunciante>, descontando Z sobreposições." Regra de evolução: preservar data e fonte da observação anterior; distinguir mudança real de falha de carregamento; não substituir contagem histórica.

## C. Classificação de cada anotação (Emagrecimento — hub)
| Classificação | Significado | Exemplo |
|---|---|---|
| Dado observado | Informação lida na fonte e datada | ID e data de início exibidos pela Meta |
| Alegação do anunciante | Promessa ou informação comercial não verificada | Preço na copy, prazo de preparo, valor nutricional |
| Interpretação | Nossa leitura do que o anúncio tenta comunicar | Monotonia como obstáculo à constância |
| Hipótese | Ideia que precisa de validação própria | Testar produto organizado por ingrediente |
| Pendente | Ainda não acessado ou confirmado | Checkout, upsell, entrega comprada, vendas |

## D. Ficha de Fonte e Linhagem (Como Ler uma Oferta do Zero)
[ ] URL do anúncio e URL final · [ ] Página/anunciante, domínio, país, idioma · [ ] Data da primeira captura e da revisão · [ ] Texto, headline, criativo, CTA, formato · [ ] Transcrição integral do vídeo/áudio · [ ] Página/VSL/quiz e ordem dos blocos · [ ] Produto, entregáveis, preço, parcelas, garantia, condições · [ ] Checkout, bump, upsell, downsell, pós-compra quando observados · [ ] Evidências ausentes e links quebrados · [ ] Código interno e versão da análise.

## E. Registro na base 19 — Mapa de Oportunidades
Nome (`<OFERTA>-OP0n — <oportunidade>`) · Oportunidade · Lacuna · Tipo (Teste/Pesquisa/Produto) · Prioridade · Base observada (IDs) · Persona · Dor · Desejo · Mecanismo · Ângulo · Funil sugerido · Produto sugerido · Prova necessária · Risco · Confiabilidade (Nível D — Hipótese) · Status (Hipótese). Regra: "Oportunidade derivada de lacuna observada, não de desejo importado dos livros." "Não criar produto novo; revisar a clareza da oferta observada antes de qualquer modelagem" quando a lacuna for de evidência.

## F. Ficha de análise por oferta (Aplicação — seção 7, literal)
Data e fonte · Anunciante e oferta (separadamente) · ID do anúncio ou cartão · País, categoria e status da consulta · Quantidade observada (separar total da página, cartões e agrupamentos) · Data de início informada (não assumir continuidade) · Situação do público sugerida pela copy (interpretação) · Consciência pressuposta (hipótese com justificativa) · Sofisticação e concorrência (não inferir estágio pelo volume) · Headline e lead (observado ou autoral?) · Referência de copy (autor, obra, páginas) · Promessa e mecanismo comercial (alegação) · Produto, preço e condições (fonte) · Formato visual (só o que foi visto) · Destino (link extraído ou página aberta?) · Checkout, complementos e entrega (confirmado/pendente) · Evidência de vendas (normalmente não disponível) · Aprendizado transferível · Hipótese própria · Mapa promessa–prova · Objeções e condições · Decisão e pendências (aprofundar, testar, aguardar ou descartar).

## G. Ficha de oferta das rodadas 04/06/07
Destino · Preço · Anunciante · ID Meta · Início exibido · Status observado · Busca utilizada · Mecanismo comercial · Evidência · Ressalva · (CO) Oferta observada · Mecanismo nomeado · Estrutura de copy · Leitura de copy · Provas que faltam · Aprendizado transferível · Teste recomendado · (07) Sinal observado · Hipótese reutilizável · Risco · Persona · Causa narrada · Sequência da solução · Entregas exibidas.
Tabela de termos: Termo | Total aproximado mostrado pela Meta | Cartões lidos nesta amostra.

## H. Como foram as rodadas anteriores (referência de método)
- Rodada 01 (28/08/2026, BR, "receitas proteicas"): busca ampla → 25 cartões → aprofundar na página do anunciante mais concentrado (28 cartões) → tabela comparativa → ângulos por ID → hipóteses → limitações. Total 49 IDs.
- Rodada 04 (28/08, BR): 10 termos por frente (doces, marmitas, café da manhã, cardápio, pilates, cadeira, caminhada, sem whey, air fryer, saladas) → 17–26 cartões por termo (221 IDs) → abrir cada destino → qualificar só quiz (até a primeira pergunta, sem enviar dados) ou página de vendas digital → excluir físicos, WhatsApp, Instagram, lojas de app, fora do nicho, já conhecidos → 14 ofertas.
- Rodada 06 (29/08, CO): 10 buscas em espanhol, ordenação por impressões → 122 cartões / 56 destinos → 10 ofertas, com "Provas que faltam" e "Leitura de copy".
- Rodada 07 (02/09, BR+CO): critério "funil verificado + sinais de escala" → 4 qualificadas, 2 em observação, exclusões, padrões reutilizáveis, tese + 3 variações.
Entregável da página-mãe: ficha de oferta com fontes, hipótese de posicionamento, três briefs de criativos e plano de medição.

## I. Tabela de triagem (todos os cartões da rodada)
| ID | Anunciante | Destino final | Tipo de funil | Decisão | Categoria e motivo | Confiança (A–D) | Sinais de escala (n, IDs, início) | Família/clone |
Uma linha por cartão aberto; cartões descartados na pré-triagem por categoria óbvia (perfil social, loja de app) também entram, com "Excluída — E4/E5" e a URL. Decisão só entre Qualificada / Em observação / Excluída; motivo com rótulo. Critérios em `triagem-dr.md`.

## J. Ficha de criativo (uma por Ad analisado)
Campos em `analise-de-criativos.md`, seção 2. Anexe ao bloco da oferta correspondente no relatório, pareada por ID.


=====
### ARQUIVO: references/triagem-dr.md
=====

# Triagem: o que é e o que não é oferta de direct response

Origem: definição de direct response e de oferta das páginas "01 — Direct Response e Economics", "Conceito Canônico — Oferta", "Conceito Canônico — Funil", "Arsenal de Mineração — Direct Response & Quiz-First" e "Mineração Avançada — Meta Ads" da Trip Angle, mais as regras de exclusão praticadas nas rodadas de mineração de 08–09/2026. O Notion define o conceito; a tabela de decisão e as categorias de exclusão abaixo são **regra operacional derivada** dessa definição, marcada como tal.

## 1. Definição da casa (literal)

"Direct response é uma abordagem de marketing construída para provocar uma ação específica e rastreável em um intervalo curto ou imediatamente após a exposição. Essa ação pode ser uma compra, um cadastro, o início de um checkout, uma mensagem ou outra conversão definida previamente." Quatro componentes: oferta específica, público relevante, mensagem persuasiva, chamada para ação clara. O que descaracteriza: "campanha cujo objetivo principal é apenas construir lembrança de marca ao longo do tempo."

"Oferta é a proposta percebida de troca: produto + stack + condições + preço + ancoragem + risco + prova + urgência/escassez + CTA e, quando observados, bump, upsell e downsell." "Não é apenas produto, copy, VSL, promessa ou funil." "não deve ser preenchido por inferência quando o material não traz evidência."

"Funil é a sequência de entradas, mensagens, páginas, VSL, checkout, entrega, ascensão e possíveis saídas." Caminho público: anúncio, pré-lander, quiz, resultado, captura, VSL ou carta, checkout e continuidade. "Uma sequência de links sem motivo é inventário, não engenharia de Funil."

Limite da fonte: a Biblioteca de Anúncios revela "ângulos, formatos, oferta aparente e maturidade competitiva", e "não revela economics, targeting completo ou causalidade". "A existência de anúncio, landing, quiz, app ou assinatura não prova lucro, volume de vendas ou escala financeira."

## 2. Teste de DR em quatro perguntas (regra derivada)

Responda com o destino aberto. Cada resposta cita o que foi visto.

| # | Pergunta | "Sim" quando | Rótulo do que sustenta |
|---|---|---|---|
| 1 | Ação específica e rastreável? | O anúncio ou a primeira tela pede assistir, responder, iniciar checkout, comprar, cadastrar ou aplicar, com destino próprio. | OBSERVAÇÃO |
| 2 | Oferta observável? | No fluxo público aparecem produto ou entrega definida **e** preço ou condições **e** CTA de decisão. Preço só na copy do anúncio é ALEGAÇÃO DA COPY; preço em página ou checkout é FATO CONFIRMADO. | FATO CONFIRMADO / ALEGAÇÃO DA COPY |
| 3 | Funil com etapa de decisão? | Há página, VSL, quiz ou carta que conduz a checkout, ou a uma captura cuja continuidade está declarada. | OBSERVAÇÃO |
| 4 | Mensagem de resposta direta? | A peça organiza problema ou desejo, mecanismo e alguma prova, e não apenas lembrança de marca, catálogo ou conteúdo. | INTERPRETAÇÃO ESTRATÉGICA |

Quatro "sim" não bastam para qualificar: falta o recorte (seção 0 da skill) e o sinal de escala.

## 3. Tabela de decisão (regra derivada)

| Estado | Entra quando | O que registrar |
|---|---|---|
| **Qualificada** | Destino verificado · quatro "sim" · oferta compatível com o recorte · pelo menos um sinal de escala documentado | Tipo de funil, oferta observada (produto, preço, plataforma), sinais de escala, confiança A ou B, família (se clone) |
| **Em observação** | Funil real mas oferta não observada na sessão · sinal insuficiente (um cartão isolado, sem repetição) · destino fora do ar · provas ou referências incoerentes · gate não contornável antes da oferta | Motivo específico, o que falta ver, data das tentativas, confiança C ou D |
| **Excluída** | Qualquer categoria de exclusão abaixo, ou "não" em uma das quatro perguntas sem chance de mudar com mais navegação | Categoria (E1–E7) e evidência de uma linha |

Sinais de escala que contam (todos são OBSERVAÇÃO, nenhum é prova de venda): contagem "N anúncios usam esse criativo"; número de IDs do mesmo anunciante na busca; data de início antiga com anúncio ainda ativo (longevidade); repetição do mecanismo ou da estrutura entre anunciantes independentes. Registre os números com data; não substitua contagem antiga por atual sem anotar a revisão.

## 4. Categorias de exclusão (regra derivada das rodadas)

| Código | Categoria | Como reconhecer | Por que sai |
|---|---|---|---|
| E1 | E-commerce de catálogo | Loja com vários produtos, carrinho, CEP e frete, sem página de vendas, VSL ou quiz | Não há mensagem de resposta direta nem funil de decisão; é varejo |
| E2 | Marca ou institucional | Site da marca, catálogo, "conheça a linha", localizador de lojas, sem oferta nem CTA de conversão | Objetivo é lembrança de marca |
| E3 | Serviço local ou WhatsApp direto | Botão "Enviar mensagem pelo WhatsApp" sem página pública, clínica ou negócio com endereço e agendamento | Funil não é auditável e a oferta não é observável; fora do recorte de infoproduto |
| E4 | Perfil social ou conteúdo | Destino é perfil de Instagram, TikTok, YouTube ou post, sem oferta | Não há etapa de decisão |
| E5 | Loja de app | App Store ou Google Play | Oferta é assinatura in-app fora do funil público; registrar como "app" se o recorte pedir |
| E6 | Fora do recorte | Nicho, país ou tipo de produto diferentes do definido na seção 0 | Ruído para esta rodada; pode virar seed de outra |
| E7 | Já conhecida | Oferta já registrada nas bases | Registra a nova observação (IDs, contagem, data) na ficha existente; não conta como achado novo |

Exclusão sempre vem com o motivo em uma linha e o rótulo. Exemplo: "Excluída — E3: destino é botão de WhatsApp, sem página pública [OBSERVAÇÃO]."

## 5. Casos-limite e a decisão correta

| Situação | Decisão | Por quê |
|---|---|---|
| Anúncio manda direto para checkout (Hotmart, Kiwify, Cakto, Wiapy, PerfectPay, Lastlink, CartPanda) com produto e preço visíveis | **Qualificada**, funil "checkout direto", ressalva "página de vendas não localizada" | Oferta observada (produto, preço, CTA); funil curto ainda é funil |
| Advertorial ou pré-lander que leva a VSL ou página | Classifique pelo **destino final**; registre o advertorial como etapa | Pré-lander é entrada, não oferta |
| Quiz que termina em captura de e-mail ou WhatsApp sem oferta na sessão | **Em observação**, "funil de captura; oferta NÃO MAPEADA"; qualifica só se o recorte incluir funis de lead | Ação rastreável existe, oferta não |
| Página de aplicação para mentoria ou acompanhamento (formulário, sem preço) | **Em observação**, "funil de aplicação"; qualifica se o recorte incluir alto ticket | Idem: DR de aplicação, oferta não observável publicamente |
| Evento gratuito, desafio ou webinar com inscrição e promessa de turma depois | **Em observação**, "funil de lançamento"; anotar a data prometida para revisitar | Oferta virá depois; hoje é captura |
| VSL longa em que o preço só aparece após N minutos e não foi assistida até lá | **Em observação** até ver o preço ou alcançar o checkout | Sem preço visto, a oferta é alegação |
| Produto físico (suplemento, gel, chá) vendido por VSL ou página longa com mecanismo e checkout | É **DR físico**: qualifica se o recorte aceitar físico; senão, **Excluída E6** com nota "funil DR, produto físico" | Não confundir com E1; o funil é de resposta direta |
| Vídeo de marca grande com CTA genérico ("saiba mais") para site institucional | **Excluída E2** | Sem oferta nem decisão |
| Destino retorna 404 ou fora do ar | **Em observação** com data e hora de duas tentativas; nunca qualificada | Não há destino verificado |
| Mesma copy ou vídeo em dois anunciantes, checkout em plataformas diferentes | **Família** (clone): uma entrada na lista com os anunciantes listados; PADRÃO IDENTIFICADO | Repetição é sinal de mecanismo em circulação, não duas ofertas nem vínculo provado |
| Anúncio ativo com sinais de violar política (antes/depois, nome de medicamento, promessa de emagrecimento) | Pode qualificar; marcar **risco de compliance** na ficha | "Anúncios ativos podem violar políticas": ativo não é sinal de qualidade |
| Contagem alta, mas destino é perfil ou WhatsApp | **Excluída** (E3/E4) mesmo com sinal de escala | Sinal sem funil auditável não vira oferta |

## 6. Clone, variação ou ângulo novo (literal da Mineração Avançada)

"Só classifique como ângulo novo quando houver mudança substancial de desejo, problema, mecanismo, promessa, persona ou prova; uma troca de apresentador, cenário ou avatar não basta." Classificação por peça: clone (copy, vídeo ou estrutura idênticos), variação (mesmo argumento, execução diferente), ângulo novo. Sinais de operação clonada: mesma copy em anunciantes diferentes; mesmo app em dois domínios; páginas com nome do especialista trocado e estrutura idêntica (dois planos, cinco bônus, "N pessoas já transformaram", 4.9 de N avaliações, timer com a data do dia). Registre a família e a evidência; não afirme que são a mesma empresa.

## 7. Escala de confiança por registro (literal do Arsenal de Mineração)

- **A — confirmado:** observado diretamente em fonte pública primária ou no fluxo público acessível.
- **B — forte:** confirmado por fonte oficial ou metadata consistente, mas com alguma etapa parcial.
- **C — plausível:** sinal indireto, página de loja, conteúdo editorial ou relação provável sem confirmação completa.
- **D — hipótese:** inferência útil para orientar pesquisa, ainda sem evidência suficiente.

Qualificada exige A ou B. "Atualização de escala apenas quando houver sinal observável adicional."

## 8. Erros de leitura que a triagem deve evitar (literais)

Oferta: "Confundir produto com oferta; tratar bônus como prova; aceitar urgência como fato; confundir ancoragem com valor real; omitir condições; chamar bump de produto principal; inferir performance do preço." Funil: "Chamar VSL de funil; listar URLs sem função; inventar etapa ausente; ignorar saída; não mapear checkout/entrega; medir somente entrada; importar arquitetura de outro nicho." Mineração: "'Ativo' ou 'visível' não significa 'vencedor'"; "sem tratar simples presença em loja como prova de atividade publicitária"; "não contorne esses controles nem preencha lacunas por suposição."
