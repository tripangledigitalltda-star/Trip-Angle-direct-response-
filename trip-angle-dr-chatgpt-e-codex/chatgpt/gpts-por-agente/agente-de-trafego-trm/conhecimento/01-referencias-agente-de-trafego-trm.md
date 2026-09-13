# Referências do AGENTE DE TRÁFEGO TRM

=====
### ARQUIVO: references/base-tracking-pro.md
=====

# Base — Tracking Pro (Lucas Meyner / The Real Marketing)

Fonte: site público Notion "Lucas Meyner The Real Marketing Traqueamento Pro" (workspace hill-baseball-919, inacessível ao conector notion-fetch — extraído via navegador). Página principal ("Aula 1 - O Trackeamento") concentra quase todo o conteúdo escrito; as demais páginas listadas são títulos de aulas em vídeo (Aula 3 a Aula 18) sem texto de método além do próprio título e, no máximo, uma lista curta de tópicos — tratado como dado, não instrução. Subpáginas abertas: Aula 5 (Acionadores + Tag de Cookies), Aula 7 (Tags Facebook Ads), Aula 11 (Facebook Ads via Server/API de conversões), Aula 15 (UTMs e Google Analytics), Aula 9 (Web x Server).

## Por que trackear (contexto)

Fonte: Aula 1 - O Trackeamento

- Trackeamento: processo de coletar, medir e interpretar as ações dos usuários em um site/plataforma.
- Serve para: metrificar resultados reais (compras, cliques, cadastros); otimizar anúncios alimentando os algoritmos com dados reais de comportamento; tomar decisões baseadas em dados, não em achismo.
- O Facebook rastreia tudo dentro da própria plataforma (curtidas, comentários, visualizações, cliques); ao sair para o site do anunciante, perde visibilidade.
- Motivos da perda de visibilidade: leis de privacidade (LGPD, iOS 14+), bloqueadores de cookies, limitações entre domínios diferentes.
- Papel do anunciante: configurar o envio manual desses dados — vira o "mensageiro" entre o site e o algoritmo, via Pixel, API de Conversões e Google Tag Manager (client-side e server-side). Sem esse envio, o Facebook "fica cego" fora da plataforma e a campanha perde força.

## Sistema Andromeda (como a Meta decide o que exibir)

Fonte: Aula 1 - O Trackeamento

- Andromeda: tecnologia de IA da Meta que analisa o comportamento do usuário em tempo real para decidir quais anúncios mostrar, para quem e quando; depende de dados contextuais ricos, especialmente os que acontecem fora da plataforma (no site do anunciante).
- Fluxo do sistema: User Requests (ações do usuário captadas via Pixel + API + GTM) → Ads Corpus (banco de milhões de anúncios candidatos) → Hierarchical Ad Index + Hierarchical Model (organiza em camadas e filtra por comportamento) → Ad Candidates (anúncios mais relevantes levados à exibição final).
- Referência citada: engineering.fb.com — "Meta Andromeda: Advantage+ automation next-gen personalized ads retrieval engine" (dez/2024).
- Advantage+ (criativos, orçamento, públicos) não funciona bem sem dados; performance vem de campanhas que ensinam o algoritmo a trabalhar por você.

## Plano de medição / funil de eventos

Fonte: Aula 1 - O Trackeamento

Advanced Matching: além do evento em si (ex.: "Purchase"), enviar dados do usuário — nome, e-mail, telefone, ID do cliente — para atribuir a conversão a um usuário real. Isso permite ao sistema identificar em que etapa do funil o usuário está e construir públicos semelhantes (lookalikes) com base real.

Etapas do funil (sequência citada literalmente):
1. Desconhecido
2. Viu o anúncio
3. Clicou no anúncio
4. Visitou a página
5. Viu 50% do vídeo
6. Acessou o checkout
7. Comprou

Sem eventos bem configurados e dados de usuário, o sistema não sabe como ajudar o anunciante.

### UTMs (Aula 15 — UTMS e Google Analytics)

- Usar ga-dev-tools.google/ga4/campaign-url-builder/ para criar UTMs que diferenciem campanhas.
- Usar link com UTMs em diferentes anúncios.
- Analisar campanhas/públicos/anúncios no Google Analytics.

## Pixel

Fonte: Aula 1 - O Trackeamento

- Pixel: mecanismo histórico de rastreamento do Facebook fora da plataforma; hoje perde eficácia por privacidade (LGPD, iOS 14+), bloqueadores de cookies e limitações entre domínios.
- Variáveis relevantes para o Pixel/GTM: nome, email, ID do Pixel, UTMs de origem, qualquer outra informação presente na navegação.

## CAPI (API de Conversões)

Fonte: Aula 1 - O Trackeamento / Aula 11 - Facebook Ads via Server (API de conversões) / Bônus

- API de Conversões: canal usado (junto a Pixel e GTM) para enviar ao Facebook as ações do usuário quando o navegador perde visibilidade.
- GTM Server-Side é usado para: enviar eventos via API de Conversões do Facebook (mais confiável que o Pixel); receber dados externos via Webhook ou Postback; salvar eventos em banco de dados; aumentar privacidade, performance e controle.
- Bônus citado (título da aula): "Adicionando localização e External Id na tag do Facebook - Server" — indica localização (geolocalização) e External Id como parâmetros enviados na tag de servidor do Facebook.
- Aula 11 (corpo da página): apenas o título "Facebook Ads", sem texto adicional além do vídeo.

## Deduplicação

Não encontrado nas páginas (termo "duplicação/deduplicação" não aparece no texto extraído desta fonte).

## GTM (Google Tag Manager)

Fonte: Aula 1 - O Trackeamento (visão geral) + títulos das Aulas 3–18 (conteúdo em vídeo, sem texto detalhado no Notion)

GTM: ferramenta que permite instalar códigos e medir eventos sem editar o código-fonte do site. Componentes citados:
- **Instalação:** instalar o GTM no site para capturar interações dos usuários com a página.
- **Variáveis:** armazenam/tratam dados importantes — nome, email, ID do Pixel, UTMs de origem, qualquer outra informação da navegação.
- **Acionadores (triggers):** disparam eventos com base em ações específicas — clique no botão "Comprar Agora", visualização de página específica, envio de formulário, qualquer outra ação do usuário.
- **Tags:** códigos que enviam os dados para Facebook, Google ou outras plataformas, ou adicionam informações no navegador. Exemplos citados: envio do evento de Purchase para o Facebook Ads; envio de evento de Lead para o Google Ads; adicionar dados de geolocalização no navegador do usuário.
- **GTM Server-Side (avançado):** ver seção CAPI acima.

Sequência de aulas em vídeo sobre GTM (títulos, sem detalhamento textual disponível):
| Aula | Tópico |
|---|---|
| 3 | Configuração Google Tag Manager |
| 4 | Variáveis |
| 5 | Acionadores + Tag de Cookies (subtópicos: Tag com Acionador Geral; Tag com Acionador Específico; Tag para salvar Cookies) |
| 6 | Tags GA4 |
| 7 | Tags Facebook Ads (subtópico: Configurações no Google Tag Manager) |
| 8 | Tags Google Ads |
| 9 | Web x Server (subtópico: Entendendo o problema) |
| 10 | Implementação via Server pela Stape |
| 11 | Facebook Ads via Server (API de conversões) |
| Bônus | Localização e External Id na tag do Facebook - Server |
| 12 | Implementação do zero na LP |
| 13 | Utilizando a inteligência enviada para as plataformas |
| 14 | Microsoft Clarity |
| 15 | UTMs e Google Analytics |
| 16 | Importar e exportar containers |
| 17 | Envio de eventos que acontecem fora do domínio (1) |
| 18 | Trackeamento de infoproduto sem formulário (1) |

## Eventos padrão e personalizados

Fonte: Aula 1 - O Trackeamento

- Evento citado como exemplo padrão: Purchase (enviado ao Facebook Ads).
- Evento citado como exemplo: Lead (enviado ao Google Ads).
- Acionadores de eventos citados: clique em "Comprar Agora"; visualização de página específica; envio de formulário; "50% do vídeo visto" (etapa de funil).
- Dados de Advanced Matching a enviar junto ao evento: nome, e-mail, telefone, ID do cliente.

## Ferramentas citadas

Fonte: Aula 1, Aula 10, Aula 14, Aula 15

Google Tag Manager (client-side e server-side); Meta Pixel; Meta API de Conversões; Stape (implementação server-side); Microsoft Clarity; Google Analytics (GA4); GA4 Campaign URL Builder (ga-dev-tools.google/ga4/campaign-url-builder/).

## Estrutura de campanha e conjuntos

Não encontrado nas páginas.

## Nomenclatura

Não encontrado nas páginas.

## Criativos por conjunto

Não encontrado nas páginas.

## Orçamento (ABO/CBO/Advantage+)

Não encontrado nas páginas (Advantage+ é citado apenas como recurso de automação da Meta que "não funciona bem sem dados", sem detalhamento de orçamento).

## Testes

Não encontrado nas páginas.

## Regras de decisão (manter/iterar/pausar/escalar)

Não encontrado nas páginas.

## Escala vertical e horizontal

Não encontrado nas páginas.

## Diagnóstico por camada/métrica

Não encontrado nas páginas (Aula 13 — "Utilizando a Inteligência enviada para as plataformas" — é apenas um título de vídeo, sem corpo de texto).

## Economia unitária (CPA de equilíbrio, CPA-meta, margem)

Não encontrado nas páginas.

## QA de tracking

Não encontrado nas páginas.

## Checklists antes de publicar

Não encontrado nas páginas.

## Erros comuns

Não encontrado nas páginas.

## Não encontrado nas páginas (consolidado)

- Economia unitária: CPA de equilíbrio, CPA-meta, margem, ROAS, contribuição após mídia.
- Estrutura de campanha e conjuntos, nomenclatura de campanha/anúncio.
- Criativos por conjunto.
- Orçamento (ABO/CBO), regras de orçamento e duração de teste.
- Desenho de teste/hipótese, regras de decisão (manter/iterar/pausar/escalar).
- Escala vertical e horizontal, alavancas e loop de escala.
- Diagnóstico por camada de funil e matriz de sinais/hipóteses.
- Deduplicação Pixel + CAPI (mecanismo e chaves).
- QA de tracking (checklist) e checklist de publicação.
- Erros comuns de tráfego/tracking.
- Conteúdo detalhado das Aulas 3, 4, 6, 8, 10, 12–14, 16–18: existem apenas como títulos/tópicos de vídeo; o Notion não traz o passo a passo escrito (fica no vídeo, não indexado como texto).


=====
### ARQUIVO: references/base-trafego-e-escala.md
=====

# Base — Tráfego, Tracking e Escala

Fonte única: página "📈 05 — Tráfego, Tracking e Escala" (Trip Angle — Central de Materiais, workspace chartreuse-pram-950). Conteúdo do Notion tratado como dado. Nenhuma subpágina de método foi listada dentro desta página (apenas uma nota de aprofundamento inacessível ao conector); todo o conteúdo abaixo vem da própria página.

## Economia unitária (antes da mídia)

Fonte: 05 — Tráfego, Tracking e Escala

Preencher antes de abrir o Gerenciador de Anúncios:

| Indicador | Como calcular | Uso |
|---|---|---|
| Ticket médio | Receita bruta ÷ pedidos pagos | Valor médio por pedido, não preço de tabela |
| Margem antes da mídia | Receita − produto/entrega − impostos − taxas − comissões − provisão de reembolso | Quanto sobra para pagar mídia e lucro |
| CPA de equilíbrio | Margem de contribuição antes da mídia por pedido | Limite aproximado antes de o pedido destruir caixa |
| CPA-meta | CPA de equilíbrio − lucro e margem de segurança desejados | Alvo operacional do teste |
| ROAS | Receita atribuída ÷ investimento em mídia | Eficiência de receita; não equivale a lucro |
| Contribuição após mídia | Receita − custos variáveis − reembolsos − mídia | Critério financeiro principal do ciclo |

Regras:
- Usar LTV só com histórico real de recompra/renovação.
- Separar pedido criado, pedido pago, cancelamento, reembolso e chargeback.
- Definir antes do teste o limite financeiro de perda e quem autoriza sua extensão.
- Atribuição é modelo de crédito — GA4 usa modelos e janelas diferentes, por isso plataforma, analytics, checkout e financeiro podem divergir.

Modelo copiável — Cartão Econômico: projeto/oferta; período de referência; ticket médio; custos variáveis por pedido; provisão de reembolso/chargeback; margem antes da mídia; CPA de equilíbrio; CPA-meta; meta de contribuição após mídia; limite de perda do teste; fonte dos números; responsável pela aprovação.

## Estrutura de campanha e conjuntos

Fonte: 05 — Tráfego, Tracking e Escala

| Nível | Decisão principal | Exemplo de variável |
|---|---|---|
| Campanha | Objetivo, conversão e estratégia de orçamento | Vendas vs. leads; orçamento na campanha |
| Conjunto | Evento de otimização, público, placement, agenda | Amplo vs. segmento qualificado |
| Anúncio | Criativo, mensagem, identidade e destino | Ângulo de prova vs. demonstração |

Orçamento Advantage+ distribui verba entre conjuntos conforme oportunidades previstas — é escolha de alocação, não prova de causalidade entre públicos.

## Nomenclatura

Fonte: 05 — Tráfego, Tracking e Escala

- Padrão de campanha: `PAÍS__OFERTA__OBJETIVO__FASE__AAAA-MM`
- Padrão de anúncio: `ÂNGULO__HOOK__FORMATO__PERSONA__VERSÃO`
- Manter convenção estável de UTM (grafia, maiúsculas, separadores) durante todo o ciclo.
- Exemplo real de utm_campaign: `br__curso_foto__teste01`
- Exemplo real de utm_content: `ang_prova__vid_vertical__v01` / `ang_demonstracao__video_vertical__v01`

## Criativos por conjunto

Não encontrado nesta página como seção própria (ver "Não encontrado" ao final).

## Orçamento (ABO/CBO/Advantage+)

Fonte: 05 — Tráfego, Tracking e Escala

- Estimar orçamento a partir do CPA-meta, da quantidade de conversões necessária para decisão de negócio e do limite de perda.
- Se o orçamento não permite observar a conversão final: reduzir complexidade, aumentar janela ou assumir teste exploratório.
- Considerar atraso entre clique, venda, aprovação, reembolso e fechamento no CRM.
- Evitar editar orçamento, público e criativo repetidamente no mesmo período — alterações significativas afetam distribuição e podem reiniciar/prolongar a fase de aprendizado.
- Nunca transformar referência de mercado em garantia estatística.
- Advantage+ campaign budget: automação de alocação entre conjuntos, não prova causal.
- Não existe número mágico universal de CTR, CPA, ROAS, orçamento ou duração — depende de modelo de negócio, ticket, margem, atraso de conversão, volume, mercado e risco de caixa.

## Testes

Fonte: 05 — Tráfego, Tracking e Escala

Regra da hipótese — um teste útil declara: evidência de origem; hipótese ("se mudarmos X, esperamos Y porque Z"); variável principal (criativo, público, oferta, página, placement ou estratégia); controle (o que permanece igual); resultado primário; guardrails (margem, qualidade, reembolso, reclamação, capacidade); janela e atraso; limite de perda; próxima ação (regras escritas antes dos resultados).

A ferramenta de A/B test da Meta compara versões mudando um elemento (imagem, texto, público, placement) — variar um fator principal e preservar o restante.

Modelo copiável — Plano do Teste: ID/nome do teste; oferta e versão; evidência de origem; hipótese; variável principal; controle; público; criativos e IDs; destino/URL; evento de otimização; orçamento e duração planejados; métrica primária; métricas de diagnóstico; guardrails; limite de perda; critério de manter; critério de iterar; critério de pausar; responsável; data da revisão.

### Checklist de publicação
- [ ] Test Card do módulo de criativos está completo.
- [ ] Objetivo e evento correspondem ao resultado de negócio.
- [ ] Nome, UTM, público, placement, orçamento e agenda revisados.
- [ ] Criativo não contém claim não comprovado, elemento enganoso ou violação de política.
- [ ] Página corresponde à promessa do anúncio.
- [ ] Tracking passou no QA com conversão de teste.
- [ ] Métrica, janela, limite de perda e regras de decisão registrados.
- [ ] Operação consegue atender leads, pedidos e suporte.
- [ ] Responsável sabe onde registrar incidentes e decisões.

## Regras de decisão (manter/iterar/pausar/escalar)

Fonte: 05 — Tráfego, Tracking e Escala

| Decisão | Quando usar | Ação |
|---|---|---|
| Manter | Sinal coerente, tracking estável, guardrails preservados | Continuar até a janela planejada sem mudanças desnecessárias |
| Iterar | Gargalo provável identificado e uma alteração pode testá-lo | Criar nova versão; preservar controle e histórico |
| Pausar | Limite de perda, falha técnica, política, margem ou qualidade violados | Interromper, diagnosticar e registrar causa |
| Escalar | Resultado replicável, contribuição positiva, operação preparada | Aplicar uma alavanca por vez com guardrails |

Cadência: monitoramento operacional (reprovação, gasto fora do esperado, página fora do ar, pagamento, tracking); leitura diagnóstica na janela definida por volume/atraso de conversão; revisão financeira (vendas pagas, reembolso, custos, contribuição); revisão de aprendizado (hipótese, resultado, confiança, decisão, próximo teste). Exceção de urgência: falha técnica, risco financeiro, política ou experiência grave trata-se imediatamente.

Modelo copiável — Registro de Decisão: teste/período; dados conferidos em; fonte de verdade; métrica principal; guardrails; o que aconteceu; onde está o gargalo; evidência que sustenta a leitura; explicações alternativas; decisão (manter/iterar/pausar/escalar); uma variável do próximo teste; o que permanecerá igual; responsável e data.

## Escala vertical e horizontal

Fonte: 05 — Tráfego, Tracking e Escala

Portão de entrada — só escalar se: tracking e deduplicação estáveis; pedidos pagos e contribuição conciliados; CPA/qualidade dentro dos guardrails; volume suficiente para reduzir risco de acaso; criativo vencedor não depende de claim inseguro; página, checkout, estoque, agenda, suporte e entrega suportam crescimento; caixa para atraso de recebimento/reembolso/oscilação; plano define alavanca, limite, janela e reversão.

| Alavanca | O que muda | Risco principal |
|---|---|---|
| Vertical | Aumenta orçamento mantendo estrutura | Mudar o leilão e deteriorar eficiência |
| Horizontal | Expande público, geografia ou estrutura controlada | Fragmentar aprendizado e sobrepor audiência |
| Criativa | Cria novos hooks, ângulos e formatos a partir do princípio vencedor | Confundir cópia superficial com novo conceito |
| Funil/oferta | Melhora página, checkout, ticket ou recuperação | Alterar muitas etapas e perder causalidade |
| Retenção | Aumenta recompra, renovação, upsell ou indicação | Usar LTV projetado sem coorte real |

Loop de escala: 1) salvar baseline e versão dos ativos; 2) escolher uma alavanca principal; 3) definir incremento, janela, guardrails e condição de reversão; 4) fazer a mudança e documentar horário/responsável; 5) aguardar ciclo compatível com volume e atraso de conversão; 6) comparar contribuição, qualidade e estabilidade — não só ROAS; 7) manter, reverter ou abrir próximo teste.

Sobre horário (aumentar de dia/reduzir à noite): só é hipótese de teste com volume, padrão consistente, fuso e atraso de conversão compreendidos. Não usar corte noturno automático como regra geral — mudanças frequentes alteram entrega, confundem atribuição e mascaram conversões tardias.

Modelo copiável — Cartão de Escala: baseline e período; contribuição após mídia; CPA/ROAS/qualidade; volume e atraso de conversão; alavanca escolhida; mudança planejada; o que permanecerá igual; janela de observação; guardrails; condição de reversão; capacidade operacional confirmada por; decisão e próximo checkpoint.

## Diagnóstico por camada/métrica

Fonte: 05 — Tráfego, Tracking e Escala

| Camada | Métrica | Cálculo/pergunta |
|---|---|---|
| Entrega | CPM | Investimento ÷ impressões × 1.000 — o anúncio entra no leilão? |
| Atenção | Retenção inicial/consumo | Permanecem após o primeiro contato? |
| Resposta | CTR de saída | Cliques de saída ÷ impressões — mensagem gera ação? |
| Eficiência do clique | CPC de saída | Investimento ÷ cliques de saída |
| Carregamento | Taxa de LPV | Visualizações da página ÷ cliques de saída |
| Página | Taxa de lead/checkout | Leads ou checkouts ÷ visitas qualificadas |
| Venda | Taxa de compra | Compras pagas ÷ visitas qualificadas |
| Aquisição | CPA | Investimento ÷ compras pagas |
| Receita atribuída | ROAS | Receita atribuída ÷ investimento |
| Negócio | Contribuição após mídia | Ciclo gerou caixa após custos, reembolsos e mídia? |
| Qualidade | Reembolso, show rate, fechamento, retenção | Conversão trouxe cliente adequado e entrega saudável? |

Regra: usar a mesma definição de clique, visita, compra, receita e período em todas as comparações.

### Matriz de diagnóstico

| Sinal observado | Hipóteses prováveis | Próxima verificação |
|---|---|---|
| Entrega baixa ou CPM anormal | Leilão, público estreito, política, orçamento, qualidade | Status, audiência, overlap, placement, aprovação |
| Entrega existe, atenção cai cedo | Primeiro frame, hook, ritmo, falta de contraste | Retenção por trecho e versão de abertura |
| Atenção boa, CTR de saída baixo | Ângulo curioso sem ponte, promessa fraca, CTA ambíguo | Mensagem, oferta e próxima ação |
| Cliques altos, LPV baixa | Página lenta, link, redirecionamento, consentimento | Teste móvel, velocidade e rede |
| LPV boa, lead/checkout baixo | Quebra de promessa, fricção, prova ou oferta insuficiente | Correspondência anúncio-página e gravação de sessão |
| Checkout inicia, compra não conclui | Pagamento, confiança, preço, campos, erro técnico | Funil por dispositivo e método de pagamento |
| CPA aceitável, contribuição ruim | Custos ignorados, ticket real menor, reembolso | Financeiro por coorte e margem real |
| Venda boa, qualidade ruim | Claim exagerado, público errado, onboarding falho | Reembolso, suporte, qualificação e entrega |

Ordem de investigação: 1) integridade do dado; 2) entrega e disponibilidade; 3) criativo e mensagem; 4) página, quiz ou formulário; 5) checkout ou atendimento; 6) produto, qualidade e economia. Não criar mais anúncios para esconder um checkout quebrado; não refazer a página para corrigir um evento duplicado.

## Plano de medição

Fonte: 05 — Tráfego, Tracking e Escala

Para cada etapa responder: qual ação do usuário importa, como será observada, onde será registrada, qual decisão habilita.

| Objetivo | Evento | Fonte primária | Decisão |
|---|---|---|---|
| Venda | purchase / pedido pago | Checkout ou back-end | Manter, pausar ou escalar por contribuição |
| Lead | generate_lead / formulário confirmado | CRM ou formulário | Avaliar custo e qualidade do lead |
| Agendamento | schedule / horário confirmado | Agenda ou CRM | Avaliar comparecimento e venda posterior |
| Checkout | initiate_checkout | Site ou checkout | Localizar fricção entre intenção e pagamento |
| Consumo crítico | quiz_complete, demo_complete ou equivalente | Produto ou analytics | Medir progressão, não apenas clique |

Modelo copiável — Plano de Medição: objetivo de negócio; conversão principal; eventos intermediários; definição de cada evento; parâmetros obrigatórios; fonte da verdade; Meta Pixel/dataset; GA4/fluxo; checkout/CRM; convenção de UTMs; janela de análise escolhida; responsável pelo QA; métrica de sucesso; guardrails (margem, reembolso, qualidade, capacidade).

Privacidade: coletar só o necessário para finalidade legítima e documentada; nunca colocar e-mail, telefone, CPF, condição de saúde ou dado sensível em URL/UTM; explicar cookies em linguagem clara e respeitar as escolhas do usuário; consent mode do Google comunica a escolha do banner às tags, não substitui banner nem análise jurídica.

## UTMs

Fonte: 05 — Tráfego, Tracking e Escala

| Parâmetro | Função | Exemplo |
|---|---|---|
| utm_source | Origem | meta |
| utm_medium | Meio | paid_social |
| utm_campaign | Campanha/oferta | br__curso_foto__teste01 |
| utm_content | Criativo/variação | ang_prova__vid_vertical__v01 |
| utm_term | Segmento ou termo, quando útil | publico_amplo |

GA4 usa os parâmetros UTM da URL para preencher dimensões de aquisição — manter convenção estável, sem trocar grafia/maiúsculas/separadores durante o ciclo.

## Pixel

Fonte: 05 — Tráfego, Tracking e Escala. Camada Pixel/navegador: observa ações no cliente e alimenta otimização. Limite: pode perder sinais por bloqueios, consentimento ou falhas de página.

## CAPI (Conversions API)

Fonte: 05 — Tráfego, Tracking e Escala. Camada Conversions API/servidor: envia eventos a partir de servidor, plataforma ou CRM; complementa fontes do navegador; pode receber eventos de sites, lojas, CRM e outras origens. Exige governança, parâmetros corretos e deduplicação. Server-side tagging permite validar, normalizar e controlar o que é enviado a terceiros, mas aumenta a responsabilidade técnica e de privacidade.

## Deduplicação

Fonte: 05 — Tráfego, Tracking e Escala.
- Registrar para cada evento a deduplicação: como eventos do navegador e do servidor são reconhecidos como a mesma ação.
- Exemplo: Purchase = pagamento confirmado, não clique no botão "comprar". Enviar valor e moeda corretos. Quando Pixel e CAPI registram a mesma compra, usar chaves consistentes de deduplicação para não contar duas vezes.
- QA: "Pixel e servidor usam a mesma identidade de evento quando precisam ser deduplicados" e "cada conversão real aparece uma vez na fonte de verdade".
- Erro comum: ignorar duplicação entre navegador e servidor.

## GTM (Google Tag Manager)

Fonte: 05 — Tráfego, Tracking e Escala. Mencionado apenas como parte do server-side tagging (validar, normalizar e controlar dados enviados a terceiros). Não há passo a passo de configuração nesta página — ver base-tracking-pro.md.

## Eventos padrão e personalizados

Fonte: 05 — Tráfego, Tracking e Escala. Preferir nomes padrão da Meta quando representarem corretamente o comportamento; usar eventos personalizados só quando houver necessidade real. Taxonomia mínima por evento: nome e definição; gatilho; momento (antes/depois da confirmação); parâmetros (valor, moeda, ID do pedido, produto, plano, origem); fonte da verdade; deduplicação; proprietário (quem corrige quando falhar).

## Ferramentas citadas

Fonte: 05 — Tráfego, Tracking e Escala. Meta Pixel; Meta Conversions API; Meta A/B Testing; Meta Advantage+ campaign budget; Google Analytics 4 (GA4); Google Tag Manager (client-side e server-side); Business Support Home (Meta).

## QA de tracking

Fonte: 05 — Tráfego, Tracking e Escala

- [ ] Domínio, página, checkout, formulário e redirecionamentos funcionam em desktop e celular.
- [ ] URL final mantém os parâmetros UTM.
- [ ] Evento correto dispara na ação correta — não no carregamento errado.
- [ ] Cada conversão real aparece uma vez na fonte de verdade.
- [ ] Pixel e servidor usam a mesma identidade de evento quando precisam ser deduplicados.
- [ ] Valor, moeda, produto e ID do pedido corretos.
- [ ] Teste, pedido recusado, reembolso e cancelamento têm tratamento definido.
- [ ] GA4 recebe a origem/campanha esperada.
- [ ] Checkout ou CRM armazena a origem quando necessário.
- [ ] Consentimento testado nas opções aceitar, rejeitar e revogar.
- [ ] Nenhum dado pessoal desnecessário em URL, logs ou painel.
- [ ] Capturas do teste, horário, dispositivo e responsável registrados.

Protocolo quando os números divergem: 1) não "corrigir" escolhendo a plataforma que parece melhor; 2) comparar mesmo período, fuso, moeda, status de pagamento e janela; 3) conferir UTMs, redirecionamento, atraso de processamento e duplicação; 4) separar conversão atribuída de pedido confirmado; 5) usar checkout/CRM/financeiro para contagem de negócio e plataformas para otimização/leitura de canal; 6) registrar a diferença e a causa provável antes de decidir.

## Checklists antes de publicar

Fonte: 05 — Tráfego, Tracking e Escala. Ver "Checklist de publicação" (seção Testes) e "QA de tracking" acima.

## Erros comuns

Fonte: 05 — Tráfego, Tracking e Escala

- Otimizar por vaidade (curtida, impressão, CTR) sem conectar ao negócio.
- Tratar ROAS da plataforma como lucro contábil.
- Usar Purchase em clique ou página de agradecimento acessível sem pagamento.
- Ignorar duplicação entre navegador e servidor.
- Misturar períodos, fusos, moedas, janelas e status de pedido.
- Alterar público, criativo, orçamento e página ao mesmo tempo.
- Escalar um pico curto sem volume, margem ou capacidade.
- Usar LTV projetado para justificar prejuízo atual.
- Reduzir orçamento por horário sem teste e sem compreender atraso de conversão.
- Chamar tentativa de burlar política de "contingência".

## Não encontrado nas páginas

- Criativos por conjunto (quantidade/variação recomendada por conjunto) — não detalhado nesta página.
- ABO vs. CBO como comparação explícita — só Advantage+ é citado; ABO/CBO não são nomeados.
- Passo a passo de configuração de GTM (variáveis, acionadores, tags) — não está nesta página.
- Lista de eventos padrão da Meta com nomes técnicos completos (ex.: Purchase, Lead, InitiateCheckout como identificadores de API) — a página cita os conceitos em português, não a lista técnica de nomes de evento.


=====
### ARQUIVO: references/criativos-e-trafego-hub-antigo.md
=====

# Hub antigo de criativos e tráfego (origem: skill agente-de-producao-de-criativos-trm, consolidada em 13/09/2026)

# Criativos (04) e Tráfego, Tracking e Escala (05)

Entradas obrigatórias: pesquisa (02) e estratégia (03) com público, consciência, ângulo, promessa, prova e CTA definidos; página/checkout funcionando; meta financeira e limite de perda. Sem briefing, não abra ferramenta nenhuma: prompt, câmera, ator, avatar, edição e gerenciador entram depois da hipótese. Detalhes literais em `references/criativos.md` e `references/trafego.md`.

## Criativos — o que é um criativo pronto
Tem hipótese identificável, uma mensagem principal, prova compatível, versão correta para o canal, registro de origem e critério de teste. Imagem bonita sem isso não é criativo. Camadas: Ângulo (perspectiva) → Hook (primeiro estímulo) → Conceito (ideia que une mensagem e representação) → Formato (recipiente) → Execução (peça) → Variação (mudança controlada para aprender).

Rota em 9 fases: Briefing → Creative Card · Pesquisa → swipe diagnóstico · Hipótese → variável e motivo · Conceito → matriz · Roteiro → storyboard · Produção → ativo mestre · Adaptação → pacote por placement · QA → checklist · Teste → Test Card + briefing para 05.

**Creative Card** (regra da unidade: um público, uma situação, uma mensagem, uma prova, um CTA): projeto e versão da oferta · público + situação · estágio de consciência · objetivo (parar, educar, demonstrar, qualificar, converter) · mensagem única · ângulo · prova · objeção · CTA · canal e placement · restrições · métrica. Checkpoint: outra pessoa lê e explica em uma frase o que o anúncio quer fazer.

**Hipótese criativa**: "Para [público em situação], acreditamos que o ângulo [perspectiva], apresentado por [hook/formato] e sustentado por [prova], aumentará [comportamento/métrica], porque [evidência de partida]." Famílias de ângulo: situação reconhecível, problema/custo, mecanismo, nova oportunidade, demonstração, prova, objeção, comparação, identidade/aspiração, história. Hierarquia de prova visual: produto em funcionamento > demonstração comparável > dado próprio > caso verificável > depoimento autorizado > credencial > explicação > afirmação.

**Matriz de conceitos**: uma perspectiva por linha — Ângulo | Hook visual | Hook verbal | Formato | Prova | CTA. Tipos de hook: visual, verbal, textual, narrativo, prova imediata, objeção. Hook compra atenção para a mensagem; curiosidade sem relação com o corpo rompe. Estrutura-base: hook → contexto → problema → mecanismo → prova → oferta → CTA (público muito consciente pode abrir pela oferta). Checkpoint: sem som, a abertura continua compreensível?

**Roteiro 0–30 s**: 0–3 s atenção relevante (primeiro frame + hook + contexto curto) · 3–10 s identificação (situação/problema, palavra-chave) · 10–20 s compreensão (mecanismo ou demo) · 20–27 s reduzir dúvida (prova e oferta, escopo) · 27–30 s direção (produto/ação, CTA). Pacote inicial de 3 ângulos × 3 hooks; primeira onda varia só o ângulo mantendo formato, oferta, prova e CTA.

**Produção com IA**: kit de identidade (persona com atributos bloqueados, realismo, ambiente, câmera, luz, composição, continuidade, restrições) e prompt em 10 blocos (objetivo e uso · sujeito · ação · ambiente · composição · câmera · luz e cor · textura e realismo · continuidade · restrições). Imagem canônica antes das cenas; mudar uma dimensão por vez; salvar prompt, ferramenta, modelo e data; nunca prometer "pessoa real" para avatar nem usar rosto reconhecível sem autorização. Biblioteca visual TRM: identidade → persona → aparência → ambiente → ação. Nome de arquivo `PROJETO__OFERTA__PAIS__PERSONA__ANGULO__HOOK__FORMATO__V01__AAAAMMDD`.

**QA e compliance** (estratégica, visual/técnica, factual, direitos): Meta não permite afirmar ou insinuar atributos pessoais (escreva sobre situações e soluções, não "você tem X"); antes/depois e promessas de emagrecimento, dinheiro, saúde e resultados extraordinários exigem revisão específica; rótulo de IA; CONAR; aprovação na plataforma não substitui conformidade legal.

**Testes em ondas**: 1 ângulo → 2 hook → 3 formato → 4 corpo/prova → 5 CTA, uma mudança principal por onda. Leitura por etapa: baixa retenção inicial → primeiro frame/hook; atenção boa e pouco clique → promessa/prova/CTA; clique sem conversão → message match/página; leads sem qualificação → ângulo amplo; venda com reembolso → promessa/expectativa/entrega.

## Tráfego — não existe número mágico
Não há CTR, CPA, ROAS, orçamento ou duração universal. Sequência: 0 economia unitária → 1 plano de medição → 2 tracking e QA → 3 teste → 4 métricas por camada → 5 decisão → 6 escala → 7 contingência. Entregável: Dossiê do Ciclo.

**Economia unitária (antes de qualquer campanha)**: ticket médio = receita bruta ÷ pedidos pagos · margem antes da mídia = receita − produto/entrega − impostos − taxas − comissões − provisão de reembolso · CPA de equilíbrio = margem de contribuição por pedido · CPA-meta = CPA de equilíbrio − lucro e segurança desejados · ROAS = receita atribuída ÷ investimento (não é lucro) · contribuição após mídia = receita − custos variáveis − reembolsos − mídia (critério financeiro principal). Definir limite de perda e quem autoriza extensão.

**Medição e tracking**: Purchase = pagamento confirmado, nunca clique no botão. Taxonomia por evento (nome, gatilho, momento, parâmetros, fonte da verdade, deduplicação, dono). UTMs e nomes padronizados (`PAÍS__OFERTA__OBJETIVO__FASE__AAAA-MM`; anúncio `ÂNGULO__HOOK__FORMATO__PERSONA__VERSÃO`). Nunca e-mail, telefone, CPF ou dado de saúde em URL. QA completo antes do primeiro real (12 itens em `references/trafego.md`). Quando os números divergem: não escolha a plataforma que agrada; compare período, fuso, moeda, status, janela; separe conversão atribuída de pedido confirmado; checkout/CRM/financeiro contam o negócio, plataformas otimizam.

**Teste**: hipótese com evidência de origem, variável principal, controle, resultado primário, guardrails (margem, qualidade, reembolso, reclamação, capacidade), janela e atraso, limite de perda, próxima ação escrita antes. Orçamento a partir de CPA-meta × conversões necessárias. Evitar edições repetidas (aprendizado reinicia). Advantage+ é alocação, não prova de causalidade.

**Diagnóstico por camada** (CPM → retenção → CTR de saída → CPC → LPV → lead/checkout → compra → CPA → contribuição → qualidade): ordem de investigação 1 integridade do dado, 2 entrega, 3 criativo/mensagem, 4 página/quiz, 5 checkout/atendimento, 6 produto/economia. Não crie mais anúncios para esconder um checkout quebrado. Matriz completa em `references/trafego.md`.

**Decisão**: manter (sinal coerente, tracking estável, guardrails ok) · iterar (gargalo identificado, preservar controle) · pausar (limite de perda, falha técnica, política, margem ou qualidade violados) · escalar (resultado replicável, contribuição positiva, operação preparada). Olhar várias vezes ao dia detecta incidentes; mudar estratégia várias vezes ao dia destrói comparabilidade.

**Escala**: portão de entrada (tracking estável, pedidos pagos conciliados, CPA e qualidade nos guardrails, volume suficiente, criativo vencedor sem claim inseguro, operação e caixa suportam, plano com alavanca/limite/janela/reversão). Alavancas: vertical (orçamento), horizontal (público/geografia), criativa (novos hooks do princípio vencedor), funil/oferta, retenção. Loop: salvar baseline → uma alavanca → incremento, janela, guardrails, reversão → mudar e documentar → aguardar ciclo compatível → comparar contribuição, qualidade e estabilidade → manter, reverter ou novo teste. Escala por "vendas e ROI ao longo do dia" e corte noturno são hipóteses operacionais, não regra: só com volume por faixa, atraso compreendido, resultado repetido em vários ciclos.

**Contingência** não é conta descartável, identidade falsa, clonar anúncio reprovado ou burlar revisão: é acesso por função, 2FA, dois admins legítimos, backup, dados fora da plataforma, e reprovação tratada por evidência → política → correção → revisão oficial.

## Erros que mais geram retrabalho
Abrir a ferramenta antes do briefing; imagem bonita como criativo; copiar anúncio sem princípio; testar ângulo, hook, formato e CTA juntos; personagem diferente por cena; cortar 16:9 para 9:16; texto demais no primeiro frame; hook que o corpo não entrega; depoimento/resultado/especialista fictício; ignorar licenças; medir só CTR; não registrar versão; escalar sem revisar a entrega; otimizar por vaidade; ROAS como lucro; Purchase em clique; misturar períodos; escalar pico curto; LTV projetado para justificar prejuízo; chamar burla de contingência.


=====
### ARQUIVO: references/subida-e-operacao.md
=====

# Subida de campanhas e operação no Gerenciador

## 1. Portões de aprovação (não negociáveis)

| Ação | Quem decide | Como |
|---|---|---|
| Montar plano, nomes, estrutura, UTMs, textos | Agente | Livre, em rascunho |
| Criar campanha, conjuntos e anúncios **PAUSADOS** | Agente, após o operador pedir a subida | Script ou navegador |
| Ativar, publicar, aumentar ou reduzir orçamento, duplicar para escalar, trocar público de conjunto ativo | **Operador** | "Sim" explícito no chat para cada ação, com o resumo do que muda e do gasto diário |
| Pausar anúncio ou conjunto que viola regra de stop-loss combinada | Agente propõe; operador confirma | Mesmo fluxo de confirmação |
| Excluir campanha, alterar forma de pagamento, dados da conta, BM, permissões | **Operador faz sozinho** | O agente não executa |

Antes de pedir o "sim", mostre: conta, campanha, conjuntos, orçamento diário total, data de início, evento de otimização, URL de destino e o checklist de QA marcado.

Credenciais: o agente nunca pede token, senha ou código no chat e nunca digita credenciais em formulários. O operador define `META_ACCESS_TOKEN` no próprio terminal ou já está logado no navegador.

## 2. Duas rotas de execução

**Rota A: Marketing API (preferida quando o operador tiver token).** `scripts/meta_ads.py`
1. Montar o plano em JSON (modelo em `scripts/plano-exemplo.json`).
2. `python3 meta_ads.py validar plano.json`.
3. `python3 meta_ads.py subir plano.json` para dry-run e mostrar as chamadas ao operador.
4. `python3 meta_ads.py subir plano.json --executar` depois do pedido de subida. Tudo nasce PAUSED.
5. Conferir no Gerenciador (prévia dos anúncios, destino, pixel) e registrar os IDs.
6. `ativar <id> --confirmado-pelo-operador` somente depois do "sim" no chat.
Vídeos e imagens precisam existir na conta (video_id, image_hash). Se faltar, peça ao operador para subir na biblioteca de mídia ou use o upload da API com arquivo que ele indicar. Confirme a versão da API vigente antes da primeira subida; erro da API é mostrado ao operador sem nova tentativa às cegas.

**Rota B: navegador no Gerenciador de Anúncios.** Use o Chrome do operador já logado. Monte campanha, conjuntos e anúncios seguindo o plano, com status desativado, e pare antes do botão Publicar. Mostre prints da revisão e peça o "sim". Não resolva CAPTCHA, não faça login, não aceite termos em nome do operador.

## 3. Plano de subida (campos mínimos)

- Conta (`act_`), página, pixel ou conjunto de dados, domínio verificado.
- Campanha: nome, objetivo (`OUTCOME_SALES`, `OUTCOME_LEADS` etc.), categoria especial, CBO ou ABO, orçamento se CBO.
- Conjunto: nome, orçamento se ABO, evento de otimização (`promoted_object`), estratégia de lance, público e posicionamentos, início.
- Anúncio: nome, criativo (vídeo ou imagem, texto, headline, CTA), URL de destino, `url_tags` com UTMs.
- Hipótese de teste da campanha (variável, controle, métrica, critério de decisão) e stop-loss combinado.
Orçamento na API vai em centavos da moeda da conta.

## 4. QA antes de subir (marcar tudo)

- [ ] Evento de compra dispara só em pagamento aprovado, com valor e moeda corretos.
- [ ] Pixel e API de Conversões recebendo o mesmo evento com `event_id` para deduplicação.
- [ ] Domínio verificado e eventos priorizados quando exigido.
- [ ] URL de destino abre no celular, sem erro, com a mesma promessa do anúncio.
- [ ] UTMs em todos os anúncios e chegando na ferramenta de atribuição.
- [ ] Nomes no padrão da nomenclatura.
- [ ] Criativos e copy revisados (claims sensíveis, políticas da Meta).
- [ ] Orçamento diário total e stop-loss aprovados.
- [ ] Hipótese e critério de decisão registrados antes de ativar.

## 5. Rotina de leitura

`python3 meta_ads.py insights <campaign_id> --periodo last_7d --nivel adset` ou exportação do Gerenciador. Compare sempre com a fonte de verdade de vendas (checkout ou ferramenta de atribuição), não só com a Meta. Decida com as regras de `base-trafego-e-escala.md` e registre: data, janela, dado, decisão proposta, quem aprovou.
ROAS não é lucro. Não some conversões de plataformas com janelas de atribuição diferentes.

## 6. Handoff de entrada

Do AGENTE DE COPY TRM: oferta modelada, promessa, claims aprovados, URL. Do AGENTE DE ADS TRM: criativos priorizados, Creative Cards, ordem das ondas de teste. Sem criativo aprovado e sem tracking validado, o agente monta o plano mas não sobe.


=====
### ARQUIVO: references/trafego-fases-e-contingencia.md
=====

# Tráfego, Tracking e Escala — templates literais (05)

## Fase 0 — Cartão econômico
Ticket médio = receita bruta ÷ pedidos pagos · Margem antes da mídia = receita − produto/entrega − impostos − taxas − comissões − provisão de reembolso · CPA de equilíbrio = margem de contribuição antes da mídia por pedido · CPA-meta = CPA de equilíbrio − lucro e margem de segurança · ROAS = receita atribuída ÷ investimento · Contribuição após mídia = receita − custos variáveis − reembolsos − mídia. LTV só com histórico real. Separar pedido criado / pago / cancelamento / reembolso / chargeback. Limite de perda e quem autoriza extensão. Atribuição é modelo de crédito: plataforma, GA4, checkout e financeiro divergem.
Exemplo: ticket R$297; custos variáveis + taxas + reembolso R$107; margem antes da mídia R$190; CPA-meta R$120. Teste R$360 por variação: A demonstração 3 vendas (CPA R$120, meta atingida, volume pequeno); B aspiracional 1 venda (CPA R$360); C benefícios 0 vendas (pausar no limite). Decisão: manter A em validação controlada, não declarar vencedor definitivo; pausar C; B vira nova hipótese. Outro: 3 pedidos de R$300 = R$900 brutos; custos e reembolsos R$330; mídia R$450; contribuição após mídia R$120, não R$450.

## Fase 1 — Plano de medição
Eventos: purchase/pedido pago (checkout ou back-end) → manter/pausar/escalar por contribuição; generate_lead; schedule; initiate_checkout; quiz_complete/demo_complete. Por evento: nome e definição; gatilho; momento; parâmetros (valor, moeda, ID, produto, plano, origem); fonte da verdade; deduplicação; proprietário.
UTMs: utm_source=meta · utm_medium=paid_social · utm_campaign=`br__curso_foto__teste01` · utm_content=`ang_prova__vid_vertical__v01` · utm_term=`publico_amplo`. Campanha `PAÍS__OFERTA__OBJETIVO__FASE__AAAA-MM`; anúncio `ÂNGULO__HOOK__FORMATO__PERSONA__VERSÃO`. Privacidade: nada de e-mail, telefone, CPF ou saúde em URL/UTM; consent mode não substitui banner; ANPD.

## Fase 2 — Tracking
Fluxo: anúncio → URL com UTM → página/quiz → evento no navegador → evento no servidor (quando aplicável) → plataforma/GA4 → checkout/CRM → financeiro → painel de decisão. Camadas: Pixel (pode perder sinais) · CAPI (exige dedup) · GA4 · Checkout/CRM · Financeiro (lento, decide sustentabilidade).
QA antes do primeiro real: [ ] domínio, página, checkout, formulário e redirecionamentos em desktop e celular · [ ] URL final mantém UTMs · [ ] evento correto na ação correta · [ ] cada conversão aparece uma vez na fonte da verdade · [ ] pixel e servidor com a mesma identidade de evento · [ ] valor, moeda, produto e ID corretos · [ ] teste, recusado, reembolso e cancelamento tratados · [ ] GA4 recebe origem/campanha · [ ] checkout/CRM armazena origem · [ ] consentimento testado (aceitar, rejeitar, revogar) · [ ] nenhum dado pessoal desnecessário em URL, logs ou painel · [ ] capturas, horário, dispositivo e responsável registrados.
Divergência de números: 1 não "corrija" escolhendo a plataforma melhor · 2 mesmo período, fuso, moeda, status, janela · 3 UTMs, redirecionamento, atraso, duplicação · 4 conversão atribuída ≠ pedido confirmado · 5 checkout/CRM/financeiro contam o negócio; plataformas otimizam · 6 registre diferença e causa provável.

## Fase 3 — Teste
Regra da hipótese: evidência de origem · "se mudarmos X, esperamos Y porque Z" · variável principal · controle · resultado primário · guardrails (margem, qualidade, reembolso, reclamação, capacidade) · janela e atraso · limite de perda · próxima ação escrita antes. Estrutura: campanha (objetivo, conversão, orçamento) → conjunto (evento de otimização, público, placement, agenda) → anúncio (criativo, mensagem, destino). Orçamento = CPA-meta × conversões necessárias, dentro do limite de perda; se a conversão final não é observável, reduzir complexidade, aumentar janela ou assumir exploratório; considerar atraso; evitar edições repetidas.
Checklist de publicação: Test Card completo · objetivo/evento = resultado de negócio · nome/UTM/público/placement/orçamento/agenda revisados · sem claim não comprovado · página corresponde ao anúncio · tracking passou no QA com conversão de teste · métrica/janela/limite/regras registrados · operação atende leads e suporte · responsável sabe onde registrar incidentes.

## Fase 4 — Métricas por camada
CPM = investimento ÷ impressões × 1.000 (entrega) · retenção inicial (atenção) · CTR de saída = cliques de saída ÷ impressões (resposta) · CPC de saída (eficiência) · taxa de LPV = visualizações da página ÷ cliques de saída (carregamento) · lead/checkout ÷ visitas qualificadas (página) · compras pagas ÷ visitas qualificadas (venda) · CPA = investimento ÷ compras pagas · ROAS · contribuição após mídia (negócio) · reembolso, show rate, fechamento, retenção (qualidade).
Matriz de diagnóstico: entrega baixa/CPM anormal → leilão, público, política, orçamento · atenção cai cedo → primeiro frame/hook/ritmo · atenção boa, CTR baixo → ângulo sem ponte, promessa fraca, CTA ambíguo · cliques altos, LPV baixa → página lenta, link, redirecionamento, consentimento · LPV boa, checkout baixo → quebra de promessa, fricção, prova · checkout inicia, compra não conclui → pagamento, confiança, preço, campos · CPA ok, contribuição ruim → custos ignorados, ticket real menor, reembolso · venda boa, qualidade ruim → claim exagerado, público errado, onboarding.
Ordem de investigação: 1 integridade do dado · 2 entrega · 3 criativo e mensagem · 4 página/quiz/formulário · 5 checkout/atendimento · 6 produto/qualidade/economia.

## Fase 5 — Decisão e cadência
Manter · Iterar · Pausar · Escalar (uma alavanca por vez). Cadência: monitoramento operacional; leitura diagnóstica na janela; revisão financeira; revisão de aprendizado.

## Fase 6 — Escala
Portão: [ ] tracking e deduplicação estáveis · [ ] pedidos pagos e contribuição conciliados · [ ] CPA/qualidade nos guardrails · [ ] volume suficiente · [ ] vencedor não depende de claim inseguro · [ ] página, checkout, estoque, agenda, suporte e entrega suportam · [ ] caixa para atraso, reembolso e oscilação · [ ] plano com alavanca, limite, janela e reversão.
Alavancas: vertical (orçamento; risco: mudar leilão) · horizontal (público/geografia; risco: fragmentar) · criativa (novos hooks/ângulos do princípio vencedor) · funil/oferta (página, checkout, ticket, recuperação) · retenção (recompra, upsell).
Loop: 1 salvar baseline e versão dos ativos · 2 uma alavanca · 3 incremento, janela, guardrails, reversão · 4 mudar e documentar horário/responsável · 5 aguardar ciclo compatível com volume e atraso · 6 comparar contribuição, qualidade e estabilidade, não só ROAS · 7 manter, reverter ou abrir próximo teste.
Protocolo de escala vertical: 1 Purchase = pagamento · 2 conciliar plataforma, checkout/CRM e financeiro no mesmo período · 3 CPA, contribuição, reembolso e qualidade · 4 salvar baseline · 5 incremento, janela e limite de deterioração · 6 uma mudança · 7 aguardar ciclo · 8 manter, reverter ou nova hipótese. Reduzir à noite só com volume por faixa horária, fuso/janela/atraso compreendidos, repetição em vários ciclos, restrição real de atendimento/estoque e demais variáveis controladas.

## Fase 7 — Contingência legítima
Proprietários documentados; acesso por função; 2FA; ≥2 admins legítimos; auditoria; políticas revisadas; backup/versionamento; dados fora da plataforma; canal alternativo; incidentes com responsável. Reprovação: preservar evidências → comparar com política → corrigir → revisão oficial → não burlar → registrar.

## Sprint de 14 dias e rubrica
D1 cartão econômico e limite de perda · D2 eventos/UTMs · D3–4 pixel/CAPI/GA4/checkout/CRM · D5 QA · D6 plano de teste · D7 publicação · D8–10 coleta sem mudanças · D11 diagnóstico · D12 decisão · D13 próxima versão (uma variável) · D14 dossiê. Rubrica 0–2 × 8: pronto para operar 13/16 sem zero em Economia, Medição, QA ou Segurança; pronto para escalar com todos os itens e resultado replicado nos guardrails.
