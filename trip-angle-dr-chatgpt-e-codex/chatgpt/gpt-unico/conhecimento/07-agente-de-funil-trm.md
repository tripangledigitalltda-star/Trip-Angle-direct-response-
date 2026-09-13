# AGENTE DE FUNIL TRM

Identificador: agente-de-funil-trm
Quando usar: AGENTE DE FUNIL TRM: escolhe e constrói o funil DR: pré-lander, advertorial, quiz, página de VSL, página de vendas, checkout, bump e upsell, com UTMs, eventos e QA. Use ao montar páginas ou funil.

=====
### ARQUIVO: SKILL.md (processo do agente)
=====


# AGENTE DE FUNIL TRM

Quinto agente da linha TRM. Recebe a oferta modelada e a copy aprovada do AGENTE DE COPY e entrega o caminho completo entre o clique no anúncio e a compra: arquitetura do funil, páginas prontas em HTML, quiz funcional, configuração do checkout com order bump e upsell, passagem de UTMs, eventos de conversão e QA. O AGENTE DE TRÁFEGO só ativa campanha com este funil validado.

## Regras

1. **Cada etapa precisa de motivo.** "Uma sequência de links sem motivo é inventário, não engenharia de funil." Toda página responde: o que a pessoa acabou de ver, o que espera agora, qual dúvida resolve, qual ação única pede, qual evento registra.
2. **A copy vem pronta.** O agente organiza, adapta ao formato e corta. Não inventa promessa, prova, depoimento, número, contador ou escassez. Texto faltando fica como `[COPY PENDENTE: ...]`.
3. **Nada de truque de pressão falso.** Timer que reinicia, "restam 3 vagas" inventado, notificação falsa de compra e depoimento fictício não entram.
4. **Evento de compra só em pagamento aprovado.** UTMs passam de página em página até o checkout.
5. **Publicar é decisão do operador.** O agente gera os arquivos e o checklist. Subir para domínio, alterar checkout ativo ou mudar preço só depois de "sim" explícito.
6. Regras compartilhadas em `../agente-central-trm/references/regras-compartilhadas.md`.

## Base

| Arquivo | Use para |
|---|---|
| `references/arquitetura-de-funil.md` | Escolher o funil, perguntas de passagem, erros |
| `references/paginas-e-quiz.md` | Blocos de página, VSL, advertorial, quiz, QA do ativo |
| `references/checkout-e-ofertas-de-compra.md` | Plataformas, configuração, bump, upsell, downsell, obrigado, atritos |
| `references/tracking-do-funil.md` | Mapa de eventos por página, UTMs, pixel, deduplicação |
| `assets/quiz.html` | Quiz configurável por JSON |
| `assets/vsl.html` | Página de VSL com CTA atrasado |
| `assets/advertorial.html` | Pré-lander em formato de matéria |
| `assets/pagina-de-vendas.html` | Página de vendas em blocos |
| `scripts/checar_funil.py` | QA automático das páginas geradas |

## 0. Entrada

Peça o handoff do AGENTE DE COPY (oferta modelada, copy aprovada, tabela de claims, hipótese de teste) e, em bloco único, só o que faltar: plataforma de checkout · link ou produto no checkout · onde as páginas vão rodar (HTML próprio, Lovable, WordPress, construtor da plataforma) · domínio · pixel e ferramenta de atribuição · player de vídeo (Vturb, Panda, YouTube) · links de política de privacidade, termos e contato.

## 1. Escolher a arquitetura

Com `references/arquitetura-de-funil.md`, decida pelo que a oferta precisa (consciência, complexidade, preço, necessidade de segmentar), não por moda. Desenhe o caminho com setas e, para cada seta, responda as perguntas de passagem. Registre a hipótese: por que este funil e não o mais curto.

## 2. Mapear eventos e UTMs

Com `references/tracking-do-funil.md`, monte a tabela: página · evento · quando dispara · parâmetros · onde é conferido. Defina como as UTMs atravessam cada página até o checkout.

## 3. Construir as páginas

Copie os modelos de `assets/` para a pasta `04-funil/` do projeto e preencha:
- **Quiz:** edite só o bloco `CONFIG` (telas, opções, loading, resultado, destino). Toda pergunta precisa mudar o diagnóstico, a recomendação ou a segmentação.
- **VSL:** headline, player, segundo em que o botão e o preço aparecem, stack, garantia, FAQ, link do checkout.
- **Advertorial:** matéria que leva ao próximo passo, identificada como publicidade.
- **Página de vendas:** só os blocos necessários, na ordem que a consciência pede.
Mantenha a promessa do anúncio na primeira dobra. Mobile primeiro.

Quando o operador usar um construtor (Lovable, WordPress, plataforma), entregue o conteúdo por bloco e as especificações em vez do HTML.

## 4. Configurar o checkout

Com `references/checkout-e-ofertas-de-compra.md`: produto, preço, parcelamento, meios de pagamento, order bump, upsell de um clique, downsell, página de obrigado, integrações de pixel e UTM. Pela plataforma no navegador já logado, ou entregando a ficha de configuração ao operador. Alteração em checkout que já recebe tráfego exige "sim".

## 5. QA

1. `python3 scripts/checar_funil.py <pasta>` nas páginas geradas.
2. QA manual do ativo e dos atritos de checkout das referências.
3. Teste do caminho: anúncio → página → quiz → VSL → checkout com UTMs de teste, conferindo que parâmetros chegam e que eventos aparecem no Gerenciador de Eventos. Compra de teste só com o operador.

## 6. Entregar

Mapa do funil com hipótese · páginas e quiz em `04-funil/` · ficha de configuração do checkout · tabela de eventos e UTMs · resultado do QA com pendências · o que precisa de aprovação para publicar · handoff para COMPLIANCE e TRÁFEGO.

## Erros que invalidam o funil

Página sem motivo no caminho · promessa da página diferente da do anúncio · quiz com pergunta que não muda nada · VSL sem legenda ou sem botão acessível · CTA concorrentes · preço ou condição que muda no checkout · UTMs perdidas entre páginas · Purchase no clique do botão · timer falso ou escassez inventada · página sem política, termos e contato · publicar sem aprovação.

## Fechamento da etapa (AGENTE CENTRAL TRM)

Termine sempre com o bloco `HANDOFF DO PROJETO` de `../agente-central-trm/references/handoff.md`, seção 1, preenchido, com os caminhos dos artefatos salvos na pasta da etapa do projeto. Ao começar, peça o handoff da etapa anterior quando houver projeto aberto.


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


=====
### ARQUIVO: assets/advertorial.html
=====

```html
<!-- AGENTE DE FUNIL TRM · advertorial (pré-lander). Identificação de publicidade obrigatória. Sem logos de mídia reais. -->
<!doctype html><html lang="pt-BR"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><title>[TITULO]</title>
<!-- PIXEL: cole aqui o código base do Pixel da Meta (fbq init + PageView) fornecido no Gerenciador de Eventos -->
<style>*{box-sizing:border-box}body{margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,sans-serif;color:#1a1a1a;background:#fff;line-height:1.55}main{max-width:720px;margin:0 auto;padding:20px 16px 60px}h1{font-size:clamp(1.6rem,5vw,2.3rem);line-height:1.2;margin:.4em 0}h2{font-size:1.35rem;margin-top:1.8em}.cta{display:block;text-align:center;background:#16a34a;color:#fff;font-weight:700;font-size:1.15rem;padding:18px;border-radius:10px;text-decoration:none;margin:24px 0}.box{border:1px solid #e5e5e5;border-radius:12px;padding:16px;margin:16px 0}.legal{max-width:720px;margin:40px auto;padding:16px;font-size:.8rem;color:#666;text-align:center}.tag{font-size:.75rem;text-transform:uppercase;letter-spacing:.05em;color:#777}.hidden{display:none}</style></head><body><main>
<p class="tag">Publicidade · Conteúdo patrocinado</p>
<h1>[TÍTULO DE DESCOBERTA OU NOTÍCIA ligado à promessa do anúncio]</h1>
<p><em>[Autor ou marca real] · [data]</em></p>
<p>[LEAD: situação reconhecível da persona]</p>
<h2>[Intertítulo: o problema]</h2><p>[Mecanismo do problema]</p>
<h2>[Intertítulo: a descoberta]</h2><p>[Mecanismo da solução, com a prova disponível]</p>
<div class="box">[PROVA: só a autorizada e documentada]</div>
<h2>[Intertítulo: o próximo passo]</h2><p>[Transição para a VSL ou página]</p>
<a class="cta" data-next href="[URL_PROXIMA_ETAPA]">[CTA: o que a pessoa vai ver]</a>
</main><footer class="legal"><p>[AVISO LEGAL: resultados variam; não substitui acompanhamento profissional quando o tema for saúde]</p><p>[RAZÃO SOCIAL] · CNPJ [CNPJ] · [ENDEREÇO] · [E-MAIL DE ATENDIMENTO]</p><p>Direito de arrependimento: 7 dias após a compra, conforme o CDC.</p><a href="[URL_PRIVACIDADE]">Política de privacidade</a> · <a href="[URL_TERMOS]">Termos de uso</a> · <a href="[URL_CONTATO]">Contato</a></footer>
<script>
/* TRM: passa UTMs e parâmetros de entrada para links com data-next ou classe .cta */
(function(){var q=new URLSearchParams(location.search);if(![...q].length)return;
function add(u){try{var x=new URL(u,location.href);q.forEach(function(v,k){if(!x.searchParams.has(k))x.searchParams.set(k,v)});return x.toString()}catch(e){return u}}
window.trmLink=add;document.querySelectorAll('a.cta,a[data-next]').forEach(function(a){a.href=add(a.getAttribute('href'))});})();
function trmEvent(n,p,custom){try{if(window.fbq)fbq(custom?'trackCustom':'track',n,p||{})}catch(e){}}
</script>
</body></html>

```

=====
### ARQUIVO: assets/pagina-de-vendas.html
=====

```html
<!-- AGENTE DE FUNIL TRM · página de vendas modular (12 blocos do módulo 03). Apague os blocos que a oferta não precisa. -->
<!doctype html><html lang="pt-BR"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><title>[TITULO]</title>
<!-- PIXEL: cole aqui o código base do Pixel da Meta (fbq init + PageView) fornecido no Gerenciador de Eventos -->
<style>*{box-sizing:border-box}body{margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,sans-serif;color:#1a1a1a;background:#fff;line-height:1.55}main{max-width:720px;margin:0 auto;padding:20px 16px 60px}h1{font-size:clamp(1.6rem,5vw,2.3rem);line-height:1.2;margin:.4em 0}h2{font-size:1.35rem;margin-top:1.8em}.cta{display:block;text-align:center;background:#16a34a;color:#fff;font-weight:700;font-size:1.15rem;padding:18px;border-radius:10px;text-decoration:none;margin:24px 0}.box{border:1px solid #e5e5e5;border-radius:12px;padding:16px;margin:16px 0}.legal{max-width:720px;margin:40px auto;padding:16px;font-size:.8rem;color:#666;text-align:center}.tag{font-size:.75rem;text-transform:uppercase;letter-spacing:.05em;color:#777}.hidden{display:none}</style></head><body><main>
<section><h1>[1 ENTRADA: headline]</h1><p>[subheadline e contexto]</p><a class="cta" href="[URL_CHECKOUT]" onclick="trmEvent('InitiateCheckout')">[CTA]</a></section>
<section><h2>[2 RECONHECIMENTO]</h2><p>[situação, sintomas, custo de continuar]</p></section>
<section><h2>[3 DIAGNÓSTICO]</h2><p>[mecanismo do problema]</p></section>
<section><h2>[4 NOVA OPORTUNIDADE]</h2><p>[mecanismo da solução]</p></section>
<section><h2>[5 TRANSFORMAÇÃO]</h2><p>[promessa qualificada e para quem é / não é]</p></section>
<section><h2>[6 COMO FUNCIONA]</h2><div class="box">[processo ou demonstração em passos]</div></section>
<section><h2>[7 PROVA]</h2><div class="box">[provas autorizadas, perto do claim que sustentam]</div></section>
<section><h2>[8 OFERTA]</h2><div class="box">[entregáveis, suporte, limites, bônus e o obstáculo que cada um remove]</div></section>
<section><h2>[9 VALOR E CONDIÇÕES]</h2><div class="box">[preço, parcelamento, custos adicionais]</div><a class="cta" href="[URL_CHECKOUT]" onclick="trmEvent('InitiateCheckout')">[CTA]</a></section>
<section><h2>[10 RISCO]</h2><div class="box">[garantia, privacidade, política]</div></section>
<section><h2>[11 OBJEÇÕES]</h2><div class="box">[FAQ priorizada]</div></section>
<section><h2>[12 AÇÃO]</h2><p>[o que acontece depois da compra]</p><a class="cta" href="[URL_CHECKOUT]" onclick="trmEvent('InitiateCheckout')">[CTA]</a></section>
</main><footer class="legal"><p>[AVISO LEGAL: resultados variam; não substitui acompanhamento profissional quando o tema for saúde]</p><p>[RAZÃO SOCIAL] · CNPJ [CNPJ] · [ENDEREÇO] · [E-MAIL DE ATENDIMENTO]</p><p>Direito de arrependimento: 7 dias após a compra, conforme o CDC.</p><a href="[URL_PRIVACIDADE]">Política de privacidade</a> · <a href="[URL_TERMOS]">Termos de uso</a> · <a href="[URL_CONTATO]">Contato</a></footer>
<script>
/* TRM: passa UTMs e parâmetros de entrada para links com data-next ou classe .cta */
(function(){var q=new URLSearchParams(location.search);if(![...q].length)return;
function add(u){try{var x=new URL(u,location.href);q.forEach(function(v,k){if(!x.searchParams.has(k))x.searchParams.set(k,v)});return x.toString()}catch(e){return u}}
window.trmLink=add;document.querySelectorAll('a.cta,a[data-next]').forEach(function(a){a.href=add(a.getAttribute('href'))});})();
function trmEvent(n,p,custom){try{if(window.fbq)fbq(custom?'trackCustom':'track',n,p||{})}catch(e){}}
</script>
</body></html>

```

=====
### ARQUIVO: assets/quiz.html
=====

```html
<!-- AGENTE DE FUNIL TRM · quiz configurável. Edite apenas o objeto CONFIG. Toda pergunta deve alterar o resultado ou a segmentação. -->
<!doctype html><html lang="pt-BR"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><title>[TITULO]</title>
<!-- PIXEL: cole aqui o código base do Pixel da Meta (fbq init + PageView) fornecido no Gerenciador de Eventos -->
<style>*{box-sizing:border-box}body{margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,sans-serif;color:#1a1a1a;background:#fff;line-height:1.55}main{max-width:720px;margin:0 auto;padding:20px 16px 60px}h1{font-size:clamp(1.6rem,5vw,2.3rem);line-height:1.2;margin:.4em 0}h2{font-size:1.35rem;margin-top:1.8em}.cta{display:block;text-align:center;background:#16a34a;color:#fff;font-weight:700;font-size:1.15rem;padding:18px;border-radius:10px;text-decoration:none;margin:24px 0}.box{border:1px solid #e5e5e5;border-radius:12px;padding:16px;margin:16px 0}.legal{max-width:720px;margin:40px auto;padding:16px;font-size:.8rem;color:#666;text-align:center}.tag{font-size:.75rem;text-transform:uppercase;letter-spacing:.05em;color:#777}.hidden{display:none}</style>
<style>.bar{height:6px;background:#eee;border-radius:3px;margin:8px 0 20px}.bar i{display:block;height:100%;background:#16a34a;border-radius:3px;width:0}.opt{display:block;width:100%;text-align:left;padding:16px;margin:10px 0;border:2px solid #e5e5e5;border-radius:10px;background:#fff;font-size:1.05rem;cursor:pointer}.opt.sel{border-color:#16a34a;background:#f0fdf4}input.field{width:100%;padding:14px;font-size:1rem;border:1px solid #ccc;border-radius:8px;margin:6px 0}</style>
</head><body><main><div class="bar"><i id="prog"></i></div><div id="app"></div></main><footer class="legal"><p>[AVISO LEGAL: resultados variam; não substitui acompanhamento profissional quando o tema for saúde]</p><p>[RAZÃO SOCIAL] · CNPJ [CNPJ] · [ENDEREÇO] · [E-MAIL DE ATENDIMENTO]</p><p>Direito de arrependimento: 7 dias após a compra, conforme o CDC.</p><a href="[URL_PRIVACIDADE]">Política de privacidade</a> · <a href="[URL_TERMOS]">Termos de uso</a> · <a href="[URL_CONTATO]">Contato</a></footer>
<script>
/* TRM: passa UTMs e parâmetros de entrada para links com data-next ou classe .cta */
(function(){var q=new URLSearchParams(location.search);if(![...q].length)return;
function add(u){try{var x=new URL(u,location.href);q.forEach(function(v,k){if(!x.searchParams.has(k))x.searchParams.set(k,v)});return x.toString()}catch(e){return u}}
window.trmLink=add;document.querySelectorAll('a.cta,a[data-next]').forEach(function(a){a.href=add(a.getAttribute('href'))});})();
function trmEvent(n,p,custom){try{if(window.fbq)fbq(custom?'trackCustom':'track',n,p||{})}catch(e){}}
</script>
<script>
var CONFIG={
 destino:"[URL_VSL_OU_PAGINA]",           /* recebe ?perfil=...&respostas UTMs preservadas */
 telas:[
  {tipo:"inicio",titulo:"[PROMESSA DO QUIZ]",texto:"[em N perguntas você descobre ...]",botao:"Começar"},
  {tipo:"escolha",id:"objetivo",titulo:"[PERGUNTA]",opcoes:[{t:"[opção A]",pontos:{A:1}},{t:"[opção B]",pontos:{B:1}}]},
  {tipo:"multipla",id:"rotina",titulo:"[PERGUNTA DE MARCAR VÁRIAS]",opcoes:[{t:"[x]",pontos:{A:1}},{t:"[y]",pontos:{B:1}}],botao:"Continuar"},
  {tipo:"info",titulo:"[TELA DE MECANISMO]",texto:"[explicação curta ligada às respostas]",botao:"Continuar"},
  {tipo:"captura",id:"contato",titulo:"[Onde enviar seu resultado?]",campos:["nome","email"],consentimento:"Concordo em receber meu resultado e comunicações. Veja a política de privacidade.",botao:"Ver meu resultado",opcional:true},
  {tipo:"loading",titulo:"[Analisando suas respostas...]",segundos:4},
  {tipo:"resultado"}
 ],
 perfis:{
  A:{titulo:"[RESULTADO PERFIL A]",texto:"[diagnóstico de hábitos, sem diagnóstico médico]",botao:"[CTA para a oferta]"},
  B:{titulo:"[RESULTADO PERFIL B]",texto:"[...]",botao:"[CTA para a oferta]"}
 }
};
(function(){var i=0,score={},resp={},el=document.getElementById('app'),T=CONFIG.telas;
function pts(p){for(var k in p)score[k]=(score[k]||0)+p[k]}
function perfil(){var best=null;for(var k in CONFIG.perfis){if(best===null||(score[k]||0)>(score[best]||0))best=k}return best}
function next(){i++;render()}
function btn(t,f){var b=document.createElement('a');b.className='cta';b.href='#';b.textContent=t;b.onclick=function(e){e.preventDefault();f()};return b}
function render(){var s=T[i];document.getElementById('prog').style.width=Math.round(i/(T.length-1)*100)+'%';el.innerHTML='';
 var h=document.createElement('h1');h.textContent=s.titulo||'';el.appendChild(h);
 if(s.texto){var p=document.createElement('p');p.textContent=s.texto;el.appendChild(p)}
 if(i===1)trmEvent('TRM_Quiz_Inicio',{},true);
 if(s.tipo==='inicio'||s.tipo==='info')el.appendChild(btn(s.botao||'Continuar',next));
 if(s.tipo==='escolha')s.opcoes.forEach(function(o){var b=document.createElement('button');b.className='opt';b.textContent=o.t;b.onclick=function(){resp[s.id]=o.t;pts(o.pontos||{});next()};el.appendChild(b)});
 if(s.tipo==='multipla'){var sel=[];s.opcoes.forEach(function(o,j){var b=document.createElement('button');b.className='opt';b.textContent=o.t;b.onclick=function(){b.classList.toggle('sel');var k=sel.indexOf(j);k<0?sel.push(j):sel.splice(k,1)};el.appendChild(b)});
  el.appendChild(btn(s.botao||'Continuar',function(){if(!sel.length)return;resp[s.id]=sel.map(function(j){return s.opcoes[j].t}).join('|');sel.forEach(function(j){pts(s.opcoes[j].pontos||{})});next()}))}
 if(s.tipo==='captura'){var f={};s.campos.forEach(function(c){var x=document.createElement('input');x.className='field';x.placeholder=c;x.type=c==='email'?'email':'text';f[c]=x;el.appendChild(x)});
  var lb=document.createElement('label');lb.innerHTML='<input type="checkbox" id="ok"> '+s.consentimento;el.appendChild(lb);
  el.appendChild(btn(s.botao,function(){var ok=document.getElementById('ok').checked,filled=s.campos.every(function(c){return f[c].value.trim()});
   if(filled&&ok){trmEvent('Lead');/* integração: envie f para a ferramenta de e-mail aqui */next()}else if(s.opcional&&!filled)next();}));
  if(s.opcional){var sk=document.createElement('p');sk.style.textAlign='center';var a=document.createElement('a');a.href='#';a.textContent='Pular';a.onclick=function(e){e.preventDefault();next()};sk.appendChild(a);el.appendChild(sk)}}
 if(s.tipo==='loading')setTimeout(next,(s.segundos||3)*1000);
 if(s.tipo==='resultado'){var k=perfil(),r=CONFIG.perfis[k];h.textContent=r.titulo;var p2=document.createElement('p');p2.textContent=r.texto;el.appendChild(p2);
  trmEvent('TRM_Quiz_Concluido',{perfil:k},true);
  var u=new URL(CONFIG.destino,location.href);u.searchParams.set('perfil',k);var a2=document.createElement('a');a2.className='cta';a2.textContent=r.botao;a2.href=window.trmLink?trmLink(u.toString()):u.toString();el.appendChild(a2)}
}render()})();
</script></body></html>

```

=====
### ARQUIVO: assets/vsl.html
=====

```html
<!-- AGENTE DE FUNIL TRM · página de VSL. Preencha os [CAMPOS]. Copy só da aprovada pelo AGENTE DE COPY. -->
<!doctype html><html lang="pt-BR"><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1"><title>[TITULO]</title>
<!-- PIXEL: cole aqui o código base do Pixel da Meta (fbq init + PageView) fornecido no Gerenciador de Eventos -->
<style>*{box-sizing:border-box}body{margin:0;font-family:system-ui,-apple-system,Segoe UI,Roboto,sans-serif;color:#1a1a1a;background:#fff;line-height:1.55}main{max-width:720px;margin:0 auto;padding:20px 16px 60px}h1{font-size:clamp(1.6rem,5vw,2.3rem);line-height:1.2;margin:.4em 0}h2{font-size:1.35rem;margin-top:1.8em}.cta{display:block;text-align:center;background:#16a34a;color:#fff;font-weight:700;font-size:1.15rem;padding:18px;border-radius:10px;text-decoration:none;margin:24px 0}.box{border:1px solid #e5e5e5;border-radius:12px;padding:16px;margin:16px 0}.legal{max-width:720px;margin:40px auto;padding:16px;font-size:.8rem;color:#666;text-align:center}.tag{font-size:.75rem;text-transform:uppercase;letter-spacing:.05em;color:#777}.hidden{display:none}</style></head><body><main>
<h1>[HEADLINE: mesma promessa do anúncio]</h1>
<p>[SUBHEADLINE]</p>
<div class="box" id="player">[EMBED DO PLAYER: Vturb, Panda ou YouTube, com legenda ativa e controles]</div>
<p style="text-align:center;font-size:.9rem">[Assista com som ou ative a legenda]</p>
<section id="oferta" class="hidden">
  <a class="cta" href="[URL_CHECKOUT]" onclick="trmEvent('InitiateCheckout')">[TEXTO DO BOTÃO: ação e o que acontece depois]</a>
  <h2>O que você recebe</h2><div class="box">[STACK: entregável — benefício]</div>
  <h2>Investimento</h2><div class="box">[PREÇO, PARCELAMENTO E ANCORAGEM HONESTA]</div>
  <h2>Garantia</h2><div class="box">[GARANTIA: prazo, como pedir, exclusões]</div>
  <a class="cta" href="[URL_CHECKOUT]" onclick="trmEvent('InitiateCheckout')">[TEXTO DO BOTÃO]</a>
  <h2>Perguntas frequentes</h2><div class="box">[FAQ: objeção — resposta]</div>
</section>
</main><footer class="legal"><p>[AVISO LEGAL: resultados variam; não substitui acompanhamento profissional quando o tema for saúde]</p><p>[RAZÃO SOCIAL] · CNPJ [CNPJ] · [ENDEREÇO] · [E-MAIL DE ATENDIMENTO]</p><p>Direito de arrependimento: 7 dias após a compra, conforme o CDC.</p><a href="[URL_PRIVACIDADE]">Política de privacidade</a> · <a href="[URL_TERMOS]">Termos de uso</a> · <a href="[URL_CONTATO]">Contato</a></footer>
<script>
/* TRM: passa UTMs e parâmetros de entrada para links com data-next ou classe .cta */
(function(){var q=new URLSearchParams(location.search);if(![...q].length)return;
function add(u){try{var x=new URL(u,location.href);q.forEach(function(v,k){if(!x.searchParams.has(k))x.searchParams.set(k,v)});return x.toString()}catch(e){return u}}
window.trmLink=add;document.querySelectorAll('a.cta,a[data-next]').forEach(function(a){a.href=add(a.getAttribute('href'))});})();
function trmEvent(n,p,custom){try{if(window.fbq)fbq(custom?'trackCustom':'track',n,p||{})}catch(e){}}
</script>
<script>
/* Segundos até exibir botão e oferta: ajuste para o momento em que a VSL apresenta a oferta. */
var TRM_DELAY_SEGUNDOS=[SEGUNDOS_ATE_OFERTA];
setTimeout(function(){document.getElementById('oferta').classList.remove('hidden');trmEvent('TRM_CTA_Exibido',{segundos:TRM_DELAY_SEGUNDOS},true)},(isNaN(TRM_DELAY_SEGUNDOS)?0:TRM_DELAY_SEGUNDOS)*1000);
</script></body></html>

```