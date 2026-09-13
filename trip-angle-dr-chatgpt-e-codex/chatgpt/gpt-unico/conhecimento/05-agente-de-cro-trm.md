# AGENTE DE CRO TRM

Identificador: agente-de-cro-trm
Quando usar: AGENTE DE CRO TRM: acha onde o funil vaza (página, VSL, quiz, checkout), prioriza hipóteses e roda testes A/B com amostra, janela e significância no padrão Test Card. Use quando não converte.

=====
### ARQUIVO: SKILL.md (processo do agente)
=====


# AGENTE DE CRO TRM

Nono agente da linha TRM. Quando o tráfego chega mas a venda não vem, este agente localiza a etapa que vaza, prova com dado, escreve a hipótese de correção, desenha o teste e decide com critério definido antes. Trabalha sobre página, advertorial, quiz, VSL, checkout, upsell e página de obrigado. O AGENTE DE TRÁFEGO cuida da mídia; o CRO cuida do que acontece depois do clique.

## Regras

1. **Dado íntegro antes de diagnóstico.** Primeiro confirmar que eventos, UTMs e contagens estão certos. Funil com tracking quebrado não se otimiza.
2. **Localizar a etapa, não adivinhar a causa.** "CTR baixo não prova produto ruim; conversão baixa não prova falta de urgência." Sintoma aponta onde olhar; a causa é hipótese até o teste.
3. **Uma variável por teste**, controle real, métrica e critério escritos antes de começar. Sem janela ou métrica há intenção de teste, não teste.
4. **Não parar cedo.** Critério da casa e checagem estatística dos dois lados. Inconclusivo é resultado válido e é registrado.
5. **Mudança publicada é decisão do operador.** O agente propõe e prepara; alteração em página ou checkout com tráfego ativo precisa de "sim".
6. **Correção não cria claim novo.** Nova promessa, prova ou urgência passa pelo COPY e pelo COMPLIANCE.
7. Regras compartilhadas em `../agente-central-trm/references/regras-compartilhadas.md`.

## Base

| Arquivo | Use para |
|---|---|
| `references/diagnostico-do-funil.md` | Métricas por camada, sintoma → onde olhar, leitura de retenção de VSL, quiz e checkout |
| `references/testes-ab.md` | Test Card da casa, priorização, amostra, janela, decisão, erros |
| `references/fontes-de-dados.md` | De onde vem cada número e como validar |
| `scripts/vazamentos.py` | Taxa por etapa, maior vazamento e impacto em vendas |
| `scripts/teste_ab.py` | Amostra necessária e resultado de teste A/B |

## 0. Entrada

Peça os handoffs de FUNIL (páginas, eventos, checkout) e TRÁFEGO (plano de medição, leituras) e, em bloco único, só o que faltar: período analisado · números por etapa (cliques, visualizações de página, início da VSL, retenção da VSL, telas do quiz, cliques no CTA, início de checkout, compras aprovadas, upsell) · segmentação por dispositivo, fonte e meio de pagamento, se houver · gravações de sessão e mapas de calor, se houver · mudanças feitas no período.

## 1. Validar os dados

Confira com `references/fontes-de-dados.md`: mesma janela em todas as fontes, compras aprovadas batendo com a plataforma, eventos sem duplicação, UTMs presentes. Anote divergências. Se a divergência for grande, a primeira hipótese é tracking e o trabalho volta ao TRÁFEGO ou ao FUNIL.

## 2. Encontrar o vazamento

Monte o CSV de etapas e rode `python3 scripts/vazamentos.py etapas.csv`. O script mostra a taxa de cada passagem, a queda e quantas vendas a mais viriam se cada etapa atingisse a meta declarada, ordenando pelo impacto. Segmente por dispositivo e por fonte quando houver dado: vazamento em um só segmento costuma ser técnico.

## 3. Diagnosticar a etapa

Com `references/diagnostico-do-funil.md`, leia a etapa que mais vaza: primeira dobra e continuidade com o anúncio, curva de retenção da VSL alinhada ao roteiro, telas do quiz com maior abandono, momento do preço, atritos do checkout, meio de pagamento, velocidade no celular. Use gravações e mapas de calor quando existirem. Escreva cada causa provável como hipótese com a evidência que a sustenta.

## 4. Priorizar e desenhar o teste

Priorize as hipóteses pela tabela de `references/testes-ab.md`. Para a primeira, preencha o Test Card da casa e rode `python3 scripts/teste_ab.py amostra --base <taxa> --melhora <efeito>` para saber quanto tráfego e quantos dias são necessários. Se o volume não sustenta o teste, diga isso e proponha a correção como mudança direta com acompanhamento antes e depois, marcada como evidência mais fraca.

## 5. Ler e decidir

Ao fim da janela: `python3 scripts/teste_ab.py resultado --a <conv>/<visitas> --b <conv>/<visitas>`. Aplique os dois filtros: o critério da casa (vitória só com pelo menos 20% de melhora na métrica principal sem piora superior a 10% nas secundárias) e a significância estatística. Decisão: manter controle, adotar variante, ajustar e retestar, ou inconclusivo. Resultado observado e interpretação ficam separados.

## 6. Entregar

Validação dos dados · tabela de vazamentos com impacto · diagnóstico da etapa com hipóteses e evidências · backlog priorizado · Test Card preenchido com amostra e janela · resultado e decisão quando houver · o que precisa de aprovação · handoff para FUNIL (mudanças de página), COPY (mensagem), BACKEND (checkout e pós-compra) ou TRÁFEGO (mídia).

## Erros que invalidam o CRO

Otimizar com tracking quebrado · mudar várias coisas ao mesmo tempo · parar o teste no primeiro dia bom · escolher a métrica depois · declarar vitória com poucas conversões · ignorar segmento por dispositivo · tratar correlação como causa · esconder resultado inconclusivo · mudar página com teste rodando · criar promessa ou urgência nova para "melhorar conversão".

## Fechamento da etapa (AGENTE CENTRAL TRM)

Termine sempre com o bloco `HANDOFF DO PROJETO` de `../agente-central-trm/references/handoff.md`, seção 1, preenchido, com os caminhos dos artefatos salvos na pasta `08-backend-cro/` do projeto.


=====
### ARQUIVO: references/diagnostico-do-funil.md
=====

# Diagnóstico do funil

Origem: métricas por camada e leitura correta do módulo 03 e do Test Card da casa; matriz de diagnóstico de `../../agente-de-trafego-trm/references/base-trafego-e-escala.md`. Leituras de VSL, quiz e checkout abaixo são **regra operacional derivada**.

## Métricas por camada (casa)
Atenção: retenção inicial, hook rate · Clique: CTR e CPC · Ativo: avanço por seção, lead, formulário, conversão, abandono · Checkout: início, abandono, compra · Economia: CPA, receita líquida, margem, ticket, reembolso · Entrega: ativação, uso, conclusão, suporte, retenção.
"CTR baixo não prova produto ruim; conversão baixa não prova falta de urgência." Localize a etapa, colete evidência, formule a próxima hipótese.

## Ordem de investigação (base de tráfego)
1 Integridade do dado · 2 Entrega e disponibilidade · 3 Criativo e mensagem · 4 Página, quiz ou formulário · 5 Checkout ou atendimento · 6 Produto, qualidade e economia.

## Etapas e taxas a calcular
| Passagem | Taxa |
|---|---|
| Clique no link → visualização da página | LPV ÷ cliques |
| Página → início da VSL ou do quiz | inícios ÷ LPV |
| VSL → chegada ao momento da oferta | retenção no segundo do pitch |
| Oferta vista → clique no CTA | cliques no CTA ÷ chegadas ao pitch (ou ÷ LPV em página sem VSL) |
| Quiz → conclusão | conclusões ÷ inícios; abandono por tela |
| CTA → início de checkout | IC ÷ cliques no CTA |
| Início de checkout → compra aprovada | compras ÷ IC; por meio de pagamento |
| Compra → upsell | aceitações ÷ compras |
| Compra → reembolso | reembolsos ÷ compras |

## Sintoma → onde olhar
| Sintoma | Primeiras hipóteses | Onde verificar |
|---|---|---|
| Cliques altos, poucas visualizações de página | Página lenta no celular, redirecionamento, link quebrado, bloqueio de consentimento, pixel sem disparar | Velocidade móvel, rede, redirecionamentos, evento PageView |
| Página carrega, VSL ou quiz pouco iniciado | Primeira dobra sem continuidade com o anúncio, player fora da tela, autoplay bloqueado, headline fraca | Print da primeira dobra no celular, mapa de clique |
| Retenção da VSL cai forte num trecho | Bloco do roteiro naquele minuto: lead longo, história sem tensão, mecanismo confuso, promessa adiada demais | Curva de retenção sobreposta ao roteiro com tempos |
| Muitos chegam ao pitch, poucos clicam | Oferta, preço, ancoragem, garantia, CTA pouco visível ou atrasado | Tempo de exibição do botão, clique no CTA, texto do bloco de oferta |
| Quiz com abandono numa tela | Pergunta invasiva, longa, sem efeito aparente, tela de captura antes do valor | Abandono por tela; ordem das perguntas |
| CTA clicado, checkout pouco iniciado | Redirecionamento lento, preço diferente do mostrado, checkout que abre em outra aba ou falha | Teste do link com UTMs, tempo de carregamento do checkout |
| Checkout iniciado, compra não conclui | Campos demais, meio de pagamento, cartão recusado, custo total inesperado, falta de confiança | Funil da plataforma por meio de pagamento e dispositivo; Pix e boleto gerados e pagos |
| Compra boa, upsell baixo | Upsell desconectado do front, página longa, recusa difícil de achar | Taxa de aceitação e gravação da página de upsell |
| Compra boa, reembolso alto | Promessa desalinhada com a entrega, acesso difícil, público errado | Motivos de reembolso, acesso em 48 h, anúncio usado |
| Um segmento muito pior (ex.: iOS, Android antigo, um navegador) | Problema técnico | Teste no dispositivo e navegador do segmento |

## Leitura da curva de retenção da VSL
1. Alinhe a curva ao roteiro com tempos (bloco por bloco).
2. Queda nos primeiros 30 segundos: hook e lead.
3. Queda gradual e contínua é esperada; degrau abrupto indica um bloco específico.
4. Compare a porcentagem que chega ao pitch com a taxa de clique no CTA: se muitos chegam e poucos clicam, o problema é a oferta; se poucos chegam, é o roteiro antes dela.
5. Teste uma mudança por vez no trecho do degrau (encurtar, reordenar, trocar a entrada do bloco).

## Checklist rápido de página no celular
- [ ] Carrega rápido em rede móvel
- [ ] Primeira dobra repete a promessa do anúncio
- [ ] Player ou primeira pergunta visível sem rolar
- [ ] CTA principal visível e com texto de ação
- [ ] Preço e condições iguais no checkout
- [ ] Nenhum pop-up que impede avançar
- [ ] Links e UTMs funcionando até o checkout


=====
### ARQUIVO: references/fontes-de-dados.md
=====

# Fontes de dados do CRO

| Número | Fonte principal | Validação |
|---|---|---|
| Cliques no link, LPV | Gerenciador de Anúncios | LPV próximo de sessões da página no mesmo período |
| Sessões, rolagem, cliques em elementos | Analytics da página (ex.: GA4) e mapas de calor e gravações (ex.: Microsoft Clarity, Hotjar) | Mesma janela e fuso; filtro de tráfego interno |
| Início e retenção da VSL | Painel do player (ex.: Vturb, Panda, YouTube) | Plays próximos de LPV × taxa de início |
| Telas do quiz | Eventos personalizados do quiz ou analytics | Soma de abandonos bate com inícios − conclusões |
| Clique no CTA | Evento personalizado ou analytics | Próximo de inícios de checkout |
| Início de checkout, compra aprovada, meio de pagamento, Pix e boleto | Plataforma de checkout (fonte de verdade de venda) | Compras aprovadas batem com o financeiro |
| Upsell e reembolso | Plataforma de checkout | Idem |
| Atribuição por campanha e anúncio | Ferramenta de atribuição com UTMs | Soma próxima das vendas da plataforma |

Regras:
- Venda é o que a plataforma aprovou, não o que a Meta atribuiu.
- Não somar conversões de fontes com janelas de atribuição diferentes.
- Registre a data de extração e o fuso de cada fonte.
- Gravações de sessão e mapas de calor precisam constar na política de privacidade e respeitar consentimento.
- Divergência acima do que o operador aceita entre fontes vira hipótese de tracking antes de qualquer teste.


=====
### ARQUIVO: references/testes-ab.md
=====

# Testes A/B de funil

Origem: Test Card da casa (`../../agente-central-trm/references/vocabulario/test-card.md`) e Test Card do módulo 03. A priorização e a checagem estatística são **regra operacional derivada**, somadas ao critério da casa, nunca no lugar dele.

## Test Card (campos da casa)
Nome (`<OFERTA>-TC0n — <o que compara>`) · oferta e versão · hipótese ("Se eu mudar X mantendo Y, espero Z porque…") · evidência que originou · variável única · variação A (controle) e B · o que não pode mudar · canal, audiência e destino iguais nos braços · orçamento e limite de perda · amostra planejada · janela · métrica principal · métricas secundárias · critério de vitória · critério de descarte · risco e claim revisado · confiabilidade (Nível D até haver dados) · status · resultado observado · interpretação · decisão · aprendizado · próximo teste.

## Critérios da casa
- Amostra mínima: 100 cliques por braço, com distribuição equivalente.
- Janela: 7 dias de tráfego simultâneo, ou até os dois braços atingirem a amostra mínima, o que ocorrer por último.
- Vitória: variação supera o controle em pelo menos 20% na métrica principal predefinida, sem piora superior a 10% nas secundárias e sem novo risco de compliance.
- Descarte só por falha de rastreamento, violação de integridade da fonte, erro de entrega ou desequilíbrio de amostra.

## Checagem estatística (derivada)
100 cliques por braço é o mínimo da casa para começar a ler, não garantia de conclusão. Para métrica de conversão com taxa baixa, calcule a amostra com `scripts/teste_ab.py amostra`. Só adote a variante quando **as duas condições** forem atendidas: critério da casa e significância (padrão: confiança de 95%, poder de 80%). Se o critério da casa foi atingido sem significância, o resultado é **promissor, não conclusivo**: estender a janela ou retestar.

## Priorização (derivada)
| Critério | Pergunta | Nota 1–5 |
|---|---|---|
| Impacto | Quantas vendas a mais se a etapa melhorar (saída do `vazamentos.py`)? | |
| Evidência | Quão forte é o dado que aponta a causa (curva, gravação, segmento)? | |
| Facilidade | Quanto trabalho e risco para implementar? | |
| Volume | A etapa tem tráfego suficiente para testar na janela? | |
Ordene pela soma; empate decide pelo impacto.

## Como dividir o tráfego
- Página ou VSL: ferramenta de split da própria página, construtor ou player com teste A/B; mesma fonte e mesmo período nos dois braços.
- Checkout: recursos de teste da plataforma quando existirem; senão, alternância por período é evidência mais fraca e deve ser marcada assim.
- Criativo: experimento A/B da Meta, conduzido pelo AGENTE DE TRÁFEGO.

## Erros que invalidam o teste (casa)
Mudar muitas coisas · parar cedo · ignorar amostra · escolher métrica depois · tratar correlação como causalidade · declarar vitória por um resultado · esconder inconclusividade · chamar backlog de experimento executado ou hipótese de aprendizado.
