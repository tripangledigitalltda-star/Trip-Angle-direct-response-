# Referências do AGENTE DE CRO TRM

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
