# Referências do AGENTE DE BACKEND TRM

=====
### ARQUIVO: references/metricas-backend.md
=====

# Métricas do backend

## Fórmulas
- **Receita líquida do front** = preço − taxas da plataforma e de pagamento − impostos.
- **Valor esperado do bump** = taxa de aceitação × receita líquida do bump.
- **Valor esperado do upsell** = taxa de aceitação × receita líquida do upsell.
- **Valor esperado do downsell** = (1 − aceitação do upsell) × aceitação do downsell × receita líquida do downsell.
- **Perda por reembolso** = taxa de reembolso × (receita líquida do front + valores adicionais reembolsados).
- **Contribuição por cliente** = receita líquida do front + bump + upsell + downsell − reembolso − custo variável de entrega.
- **Vendas recuperadas** = abandonos contatados × taxa de recuperação; entram como vendas adicionais sem custo de mídia direto.
- **CPA de equilíbrio com backend** = contribuição por cliente. Comparar com o CPA de equilíbrio só do front mostra quanto o backend sustenta.
- **AOV (valor médio do pedido)** = receita bruta ÷ número de pedidos.

## Painel semanal
| Métrica | Fonte | Semana atual | Semana anterior | Meta declarada |
|---|---|---|---|---|
| Vendas do front | Plataforma | | | |
| Aceitação do bump | Plataforma | | | |
| Aceitação do upsell e do downsell | Plataforma | | | |
| AOV | Plataforma | | | |
| Abandono de checkout e recuperação | Plataforma e ferramenta | | | |
| Pix e boleto pagos ÷ gerados | Plataforma | | | |
| Taxa de acesso em 48 h | Área de membros | | | |
| Reembolso e motivo principal | Plataforma | | | |
| Chargeback | Plataforma | | | |
| Contribuição por cliente | Cálculo | | | |

## Leitura
- Janela de reembolso ainda aberta: contribuição é provisória. Não escale mídia com base nela.
- Aceitação de bump muito baixa: argumento ou relação com o produto, antes de preço.
- Upsell alto com reembolso alto: promessa desalinhada ou pressão na página.
- Recuperação baixa com abandono alto: primeiro checar atrito no checkout (FUNIL), depois a sequência.
- Um teste por vez; registrar hipótese, variável, janela e decisão.


=====
### ARQUIVO: references/ofertas-pos-compra.md
=====

# Ofertas pós-compra

Origem: regras de order bump, upsell e downsell do AGENTE DE FUNIL (`../../agente-de-funil-trm/references/checkout-e-ofertas-de-compra.md`), equação de valor e melhoria de oferta de `../../agente-de-copy-trm/references/base-oferta-e-mecanismo.md`. Faixas de preço e posições abaixo são **ponto de partida derivado**, para testar, não regra da casa.

## Princípio
Cada oferta adicional resolve o **próximo obstáculo** que o cliente vai encontrar depois de comprar: fazer mais rápido, com menos esforço, com mais certeza ou ir além do resultado inicial. Oferta que não conversa com a compra só aumenta atrito e reembolso.

## Order bump
- **O que é:** complemento pequeno, marcado pelo próprio cliente no checkout.
- **Bom bump:** acelera, facilita ou protege o resultado do produto principal (lista de compras pronta, versão em áudio, planilha, bônus de implementação).
- **Preço:** baixo em relação ao principal, para ser decisão de impulso. Ponto de partida derivado: 20% a 50% do preço do front.
- **Copy:** título com benefício, uma ou duas frases, preço claro, caixa desmarcada.
- **Não pode:** pré-seleção, custo escondido, bump que muda as condições da compra principal.

## Upsell
- **O que é:** oferta mostrada depois do pagamento aprovado, antes do acesso.
- **Bom upsell:** o próximo passo lógico. Ex.: front ensina o que fazer; upsell entrega feito, acompanhado ou mais rápido.
- **Formato:** página curta ou vídeo curto; continuidade com a compra ("parabéns, seu acesso está garantido; antes de entrar..."), uma decisão, recusa visível.
- **Um clique:** use o upsell de um clique da plataforma quando existir.
- **Preço:** pode ser maior que o front; justificado pelo obstáculo que remove.

## Downsell
- Oferecido uma única vez, só a quem recusou o upsell.
- Versão menor, parcelada ou sem um componente do upsell. Não é o mesmo produto mais barato sem motivo, o que desvaloriza o upsell.

## Página de obrigado
Confirmação da compra · como e quando acessar · primeiro passo · suporte · convite para grupo ou comunidade se existir · pedido de opt-in do WhatsApp com finalidade clara.

## Escada de ascensão
| Degrau | Função | Exemplo em infoproduto |
|---|---|---|
| Front | Resolver um problema específico e gerar primeira vitória | Ebook, protocolo, minicurso |
| Bump | Facilitar o front | Material prático complementar |
| Upsell | Próximo obstáculo | Programa completo, acompanhamento em grupo |
| Recorrência | Manter o resultado | Assinatura, comunidade, cardápios mensais |
| Alto ticket | Feito com você ou para você | Mentoria, consultoria |
Convide para o próximo degrau depois da primeira vitória, não antes.

## Ficha de cada oferta
Nome · degrau · obstáculo que remove · público (todos ou segmento) · preço e condição · posição no fluxo · argumento em uma frase · copy · prova disponível · claims para o COMPLIANCE · métrica (taxa de aceitação) · meta declarada.


=====
### ARQUIVO: references/onboarding-e-reembolso.md
=====

# Onboarding, reembolso e prova real

Regra base: reembolso cai quando o cliente acessa, começa e percebe valor cedo. O direito de arrependimento de 7 dias do CDC não pode ser dificultado; o trabalho é de ativação, não de retenção forçada.

## Primeiros 7 dias (sequência base, derivada)
| Momento | Canal | Objetivo | Conteúdo |
|---|---|---|---|
| Imediato | E-mail e WhatsApp (com opt-in) | Acesso | Link de acesso, login, onde começar, suporte |
| Dia 1 | E-mail ou WhatsApp | Primeira vitória | Uma ação de 10–15 minutos que gera resultado visível (ex.: a primeira receita, o primeiro cardápio) |
| Dia 2 ou 3 | E-mail | Remover travas | Dúvidas mais comuns, como usar no dia a dia |
| Dia 4 ou 5 | WhatsApp ou e-mail | Engajamento | Pergunta simples sobre o progresso; convite para o próximo passo do produto |
| Dia 6 ou 7 | E-mail | Consolidar | Resumo do que já foi feito, próximo marco, apoio disponível |
Quem não acessou em 24 a 48 horas recebe mensagem específica de acesso.

## Pedido de reembolso
1. Processar conforme o direito do cliente, sem condicionar.
2. Perguntar o motivo de forma opcional e curta (não acessou, não era o esperado, dificuldade técnica, arrependimento de compra, outro).
3. Se for dificuldade técnica ou de acesso, oferecer ajuda **junto com** a confirmação de que o reembolso segue se ele quiser.
4. Registrar motivo para o COPY (promessa desalinhada?) e para o FUNIL (checkout confuso?).

## Chargeback
Evidências a guardar: confirmação da compra, acesso e uso registrados, comunicações, termos aceitos. Chargeback alto sinaliza promessa desalinhada, cobrança não reconhecida (nome na fatura diferente da marca) ou fraude: investigar a causa.

## Prova real a partir do backend
- Pedir depoimento depois da primeira vitória, com pergunta aberta sobre o que mudou.
- Autorização escrita para uso em anúncio e página, com nome ou anonimização combinada.
- Registrar contexto: tempo de uso, ponto de partida, o que fez. Resultados atípicos marcados como atípicos.
- Enviar ao AGENTE DE COPY como prova autorizada, com o arquivo da autorização.


=====
### ARQUIVO: references/recuperacao.md
=====

# Recuperação de vendas

Origem: follow-up orientado por contexto do módulo 03 (motivo, valor, CTA e condição de saída; recapitulação, evidência, fechamento do ciclo) e regras de consentimento do AGENTE DE COMPLIANCE. Tempos abaixo são **ponto de partida derivado**; ajuste ao prazo de expiração de Pix e boleto da plataforma e teste.

## Regras
- Configure primeiro a recuperação nativa da plataforma de checkout e evite mandar duas mensagens iguais por ferramentas diferentes.
- Só contate quem deixou contato no checkout com base legal para isso, e sempre com saída (descadastro, "não quero receber").
- WhatsApp com opt-in e canal oficial. Poucas mensagens, espaçadas, com valor.
- Nunca inventar escassez, desconto "que acaba em 10 minutos" sem prazo real, ou pressão emocional.

## Sequências por situação
| Situação | Gatilho | Mensagem 1 | Mensagem 2 | Mensagem 3 | Saída |
|---|---|---|---|---|---|
| Carrinho abandonado | Dados preenchidos, sem pagamento | ~15–60 min: lembrete útil com link direto do checkout | ~24 h: responder a objeção principal (prova, garantia, como funciona) | ~48–72 h: fechamento do ciclo | Sem resposta: parar |
| Pix gerado e não pago | Pix emitido, não compensado | Poucos minutos: código e passo a passo para pagar | Antes de expirar: aviso de expiração e novo código se necessário | Após expirar: link para gerar outro pagamento | Parar após a 3ª |
| Boleto emitido | Boleto gerado | Logo após: linha digitável e prazo | Véspera do vencimento: lembrete | Após vencer: link para nova forma de pagamento | Parar |
| Cartão recusado | Transação recusada | Imediato: tentar outro cartão ou Pix, sem expor dado | ~1–3 h: link com meios alternativos | — | Parar |
| Upsell recusado | Recusa na página | Opcional, no dia seguinte ao acesso: benefício do upsell ligado à primeira vitória | — | — | Não insistir |

## Moldes de mensagem (adaptar à voz do COPY)
**Lembrete útil (carrinho):** "Oi, [nome]. Seu pedido de [produto] ficou em aberto. Se foi falta de tempo, o link continua aqui: [link]. Qualquer dúvida sobre [ponto comum de dúvida], é só responder."

**Evidência (objeção):** "Você deixou [produto] no carrinho. Muita gente pergunta [objeção real]. [Resposta com prova ou garantia]. Se isso resolve, finalize aqui: [link]."

**Fechamento do ciclo:** "Não quero ficar insistindo. Se ainda fizer sentido, [link]. Se não for o momento, tudo bem: não envio mais mensagens sobre este pedido."

**Pix:** "Seu Pix de [valor] para [produto] foi gerado. Para pagar: abra o app do banco, escolha Pix copia e cola e cole o código: [código]. Ele vale até [horário]."

## Registro mínimo por contato (módulo 03)
Data e canal · etapa · necessidade e impacto · objeção aberta · material enviado · decisão e responsável · próxima ação e data · motivo de perda ou pausa.
