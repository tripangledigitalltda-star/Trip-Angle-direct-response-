# Referências do AGENTE DE FUNIL TRM

=====
### ARQUIVO: references/arquitetura-de-funil.md
=====

# Arquitetura de funil

Origem: módulo 03 — Engenharia de Ofertas, Copy e Vendas (fase 5 e 6) e Conceito Canônico FUNIL da Trip Angle. Tipos observados no mercado vêm das rodadas de mineração 08–09/2026.

## Definição
"Funil é a sequência de entradas, mensagens, páginas, VSL, checkout, entrega, ascensão e possíveis saídas pela qual a pessoa passa. VSL é apenas uma etapa ou formato dentro dessa sequência." Caminho completo: origem → mensagem → ativo → decisão → pagamento → confirmação → onboarding → entrega → aprendizado.

## Escolha pela condição (módulo 03)
| Condição | Rota provável |
|---|---|
| Produto simples e compra autônoma | Anúncio → página → checkout → onboarding |
| Necessidade de educação | Anúncio → VSL ou página → checkout |
| Necessidade de segmentação | Quiz → recomendação → página ou VSL |
| Ticket ou risco alto | Anúncio → aplicação → conversa → proposta |
| Serviço configurável | Entrada → diagnóstico → escopo → proposta |

## Formatos de ativo (módulo 03)
| Formato | Use quando | Cuidado |
|---|---|---|
| Página curta | Oferta simples, familiar, baixo risco | Não omitir informação essencial |
| Página longa | Oferta nova, cara, complexa, muitas objeções | Cada seção reduz uma dúvida |
| VSL | Mecanismo pede narrativa, demonstração ou sequência | Legenda, controles e resumo escrito |
| Quiz ou diagnóstico | Precisa segmentar ou personalizar | Nenhuma pergunta sem efeito na saída |
| WhatsApp ou ligação | Diagnóstico, configuração ou confiança | Qualificar fit, sem pressão |

## Arquiteturas comuns em DR de infoproduto (observadas nas minerações)
| Arquitetura | Quando faz sentido | Risco principal |
|---|---|---|
| Anúncio → checkout direto | Low ticket, oferta óbvia, público muito consciente | Sem espaço para objeções; reembolso |
| Anúncio → página de vendas → checkout | Oferta clara com algumas objeções | Página genérica que repete o anúncio |
| Anúncio → VSL → checkout | Mecanismo novo, consciência de problema | VSL longa sem legenda; preço escondido demais |
| Anúncio → quiz → resultado → VSL ou página → checkout | Público amplo, várias personas, necessidade de diagnóstico | Quiz longo sem efeito; queda entre resultado e oferta |
| Anúncio → advertorial → VSL ou página → checkout | Público pouco consciente, ângulo de notícia ou descoberta | Matéria que parece jornalismo sem identificação de publicidade |
| Anúncio → captura → evento ou conteúdo → oferta | Lançamento, desafio, alto envolvimento | Oferta não observável na primeira sessão |

## Perguntas de passagem (para cada seta)
O que a pessoa acabou de ver? · O que ela espera encontrar agora? · Qual dúvida precisa ser resolvida? · Qual é a única ação principal? · Que dado precisa ser registrado? · O que acontece se ela não avançar?

## Checkpoint (módulo 03)
Cada etapa entrega o que a anterior prometeu? Existem páginas órfãs, CTAs concorrentes, formulário sem destino ou compra sem onboarding?

## Erros de leitura e construção (Conceito Canônico FUNIL)
Chamar VSL de funil · listar URLs sem função · inventar etapa ausente · ignorar saída · não mapear checkout e entrega · medir somente entrada · importar arquitetura de outro nicho.


=====
### ARQUIVO: references/checkout-e-ofertas-de-compra.md
=====

# Checkout, order bump, upsell e downsell

## 1. Plataformas comuns no Brasil (observadas nas minerações)
Hotmart, Kiwify, Cakto, Wiapy, PerfectPay, Lastlink, CartPanda, Ticto, Greenn, Braip, Eduzz, Monetizze. Nome de parâmetro de rastreio, integração de pixel e API de Conversões, one-click upsell e regras de reembolso variam por plataforma: confirme na documentação atual da plataforma antes de configurar e registre o que foi confirmado.

## 2. Ficha de configuração (entregar preenchida)
Plataforma · produto e ID · nome exibido no checkout · preço e moeda · parcelamento e juros · meios de pagamento (Pix, cartão, boleto) · order bump (produto, preço, texto) · upsell (produto, preço, página, one-click sim/não) · downsell · página de obrigado (URL, próximos passos, acesso) · garantia e política de reembolso · e-mail de acesso · pixel e API de Conversões da plataforma (IDs, eventos) · parâmetros de rastreio aceitos (UTMs ou equivalentes) · webhook ou integração com ferramenta de atribuição · teste de compra (quem fará e quando).

## 3. Order bump, upsell e downsell (regras operacionais)
- **Order bump:** complemento pequeno, relacionado e que acelera ou facilita o resultado do produto principal. Uma frase de benefício, preço claro, desmarcado por padrão.
- **Upsell:** próximo passo lógico depois da compra, que remove o obstáculo seguinte. Página curta ou vídeo curto, com recusa visível.
- **Downsell:** versão menor ou parcelada do upsell recusado, oferecida uma vez.
- Nada que mude as condições da compra principal, nada cobrado sem aceite claro, nenhuma pré-seleção de adicional.
- Cada peça tem copy aprovada pelo AGENTE DE COPY e claim revisado.

## 4. Atritos de checkout (módulo 03)
- [ ] Custo total aparece antes da confirmação
- [ ] Meios de pagamento adequados
- [ ] Política e suporte visíveis
- [ ] Poucos campos e sem cadastro desnecessário
- [ ] Mensagens de erro orientam a correção
- [ ] Confirmação e próximos passos são imediatos
- [ ] Evento de conversão foi validado
"Custos inesperados, falta de confiança, cadastro forçado, processo longo, erros e pouca transparência" são diagnóstico de experiência, não desculpa para aumentar pressão.

## 5. Página de obrigado e onboarding
Confirmação da compra · como acessar e em quanto tempo · primeiro passo do produto · contato de suporte · oferta de upsell só se não houver fluxo de upsell anterior.


=====
### ARQUIVO: references/paginas-e-quiz.md
=====

# Páginas, VSL, advertorial e quiz

## 1. Página de vendas ou VSL: estrutura modular (módulo 03)
Use só os blocos necessários e reorganize conforme a consciência:
1 Entrada: headline, subheadline, contexto · 2 Reconhecimento: situação, sintomas, custo · 3 Diagnóstico: mecanismo do problema · 4 Nova oportunidade: mecanismo da solução · 5 Transformação: promessa e para quem é · 6 Como funciona: processo ou demonstração · 7 Prova · 8 Oferta: entregáveis, suporte, limites · 9 Valor e condições: preço, pagamento, custos · 10 Risco: garantia, privacidade, política · 11 Objeções: FAQ priorizada · 12 Ação: CTA e o que acontece depois.

## 2. Página de VSL (regras operacionais)
- Primeira dobra: headline com a mesma promessa do anúncio, player visível sem rolar, legenda ativa.
- Botão e bloco de oferta aparecem no momento em que a VSL apresenta a oferta. O atraso é configurável no modelo. Deixe um link "prefere ler?" para o resumo escrito quando possível.
- Abaixo do player, depois do atraso: stack, preço, garantia, FAQ e o mesmo CTA.
- Não use autoplay com som, não esconda controles e não bloqueie a página.

## 3. Advertorial (pré-lander)
- Formato de matéria ou relato, com rótulo visível de publicidade ou conteúdo patrocinado.
- Estrutura: título de descoberta ou notícia · lead com situação reconhecível · história ou explicação do mecanismo · prova disponível · transição para o próximo passo · CTA textual e botão.
- Não imite marca de veículo de imprensa real, não use logos de mídia sem autorização, não invente especialista.

## 4. Quiz (padrões observados e regras)
Estrutura observada nos quizzes minerados: tela de entrada com promessa e seleção inicial de baixa fricção (idade, gênero, objetivo) · perguntas de situação e rotina · telas informativas de mecanismo entre perguntas · loading de personalização · diagnóstico ou resultado · oferta ou VSL.
Regras:
- Toda pergunta muda o resultado, a recomendação ou a segmentação. Pergunta decorativa sai.
- Resultado baseado nas respostas, sem diagnóstico médico. Em saúde, fale de perfil e hábitos, não de doença.
- Loading de personalização só se o resultado de fato usa as respostas.
- Captura de e-mail ou WhatsApp com consentimento claro e link de privacidade (LGPD).
- Tamanho: o mínimo que sustenta o resultado. Registre a taxa de avanço por tela para cortar depois.

## 5. QA do ativo (módulo 03)
- [ ] Título e anúncio falam da mesma promessa
- [ ] Há um CTA principal
- [ ] Oferta e preço estão claros
- [ ] Prova está próxima do claim
- [ ] Botão explica a ação
- [ ] Formulário pede somente o necessário
- [ ] Página funciona no celular
- [ ] Vídeo tem legenda e controle
- [ ] Carregamento e links foram testados
- [ ] Política, termos, contato, CNPJ, arrependimento de 7 dias e reembolso estão acessíveis
- [ ] O pós-clique e o pós-compra foram definidos
Checkpoint: uma pessoa entende "para quem é, o que recebe, por que acreditar, quanto custa e o que acontece depois" sem falar com você?


=====
### ARQUIVO: references/tracking-do-funil.md
=====

# Tracking do funil

Fonte das regras gerais: `../../agente-de-trafego-trm/references/base-trafego-e-escala.md` e `base-tracking-pro.md`. Aqui fica só o mapa por página.

## Tabela de eventos (modelo)
| Página | Evento | Quando dispara | Parâmetros | Origem | Onde conferir |
|---|---|---|---|---|---|
| Advertorial | PageView; ViewContent opcional | Carregamento; rolagem ou tempo | content_name | Pixel | Gerenciador de Eventos |
| Quiz | PageView; evento personalizado de início e de conclusão | Primeira resposta; tela de resultado | etapa, perfil | Pixel | Gerenciador de Eventos |
| Captura | Lead | Envio com consentimento | — | Pixel + CAPI com event_id | Gerenciador e ferramenta de e-mail |
| VSL | PageView; ViewContent; evento personalizado de CTA exibido | Carregamento; momento do CTA | segundos | Pixel | Gerenciador de Eventos |
| Botão para checkout | InitiateCheckout só se o checkout não disparar | Clique | value, currency | Pixel | Evitar duplicar com a plataforma |
| Checkout | InitiateCheckout, AddPaymentInfo | Pela plataforma | value, currency | Plataforma | Gerenciador e plataforma |
| Compra | Purchase | **Pagamento aprovado** | value, currency, event_id | Plataforma e CAPI deduplicados | Gerenciador, plataforma e atribuição |
| Upsell | Purchase separado ou evento próprio | Aprovação do upsell | value, currency | Plataforma | Idem |

Nome e existência de cada evento dependem da configuração da conta: confirme no Gerenciador de Eventos.

## UTMs atravessando o funil
- Todas as páginas próprias rodam o script de passagem que já vem nos modelos: lê os parâmetros da URL de entrada e acrescenta aos links de próxima etapa e do checkout.
- Confirme o nome dos parâmetros que a plataforma de checkout aceita e mapeie as UTMs para eles.
- Teste com uma URL marcada (`utm_source=teste&utm_campaign=qa_funil`) e confira o registro no checkout e na ferramenta de atribuição.
