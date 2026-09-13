# Referências do AGENTE DE COPY TRM

=====
### ARQUIVO: references/aprovacao-da-oferta-etapa-04.md
=====

# Aprovação da oferta: três conceitos, scorecard e Offer Card (origem: skill 04-mineracao-de-ofertas, consolidada em 13/09/2026)


# 04 — Mineração de Ofertas (construção e aprovação da oferta)

Etapa 04 de 09 da linha de produção Trip Angle. Entra com briefing, inteligência, modelagem e avatar aprovados; sai com **três conceitos de oferta, uma recomendação principal e o conjunto aprovado de promessa, mecanismo, prova, bônus, garantia e preço**, gravado em `04-oferta-aprovada.md` e fechado com o bloco de handoff que abre a Etapa 05 — Copy.

Não é a mineração na Biblioteca de Anúncios (isso é `agente-de-espionagem-trm`). Aqui "minerar" é extrair a oferta do que o projeto já provou.

Dependências externas (repositório `coreyhaines31/marketingskills`, nomes v2): `offers`, `pricing`, `marketing-psychology`, `competitor-profiling`, `customer-research`. Use-as como apoio de método; o procedimento desta etapa é o descrito abaixo.

## Regras desta etapa

1. Nunca inventar número, prova, depoimento, pesquisa ou resultado. O que não está nas entradas é **informação ausente** e entra como pendência, nunca como conteúdo.
2. Rotular toda afirmação como **evidência**, **hipótese**, **decisão** ou **ausente**.
3. Prova sempre a mais próxima possível do claim (hierarquia em `offer-card-7-perguntas-hierarquia-prova.md`).
4. Claims sensíveis (saúde, emagrecimento, renda, finanças, segurança, crianças) exigem revisão específica. CDC, CONAR e ANPD se aplicam.
5. Escassez e urgência só quando verdadeiras. "Por que agora" precisa de motivo real.
6. Modo rascunho: preço, promessa e aprovação final são decisões humanas. A skill recomenda; o operador aprova.
7. Não encerrar sem o bloco `HANDOFF DO PROJETO` preenchido.

## 0. Verificação de entradas (antes de produzir qualquer coisa)

Abra pedindo o **handoff da Etapa 03** e os artefatos anteriores. Confira item a item e liste o que falta. Não gere conceito, promessa, prova ou preço enquanto a tabela abaixo tiver linha em aberto sem decisão explícita do operador.

| Entrada | Onde vem | Se faltar |
|---|---|---|
| `00-briefing-e-plano.md` | Etapa 00 | Pedir. Sem briefing não há recorte de produto, público e restrições. |
| `01-inteligencia-dr.md` (diagnóstico de mercado) | Etapa 01 | Pedir. Sem diagnóstico, "diferenciação" e "relevância" ficam sem base. |
| `02-modelagem.md` (matriz de modelagem) | Etapa 02 | Pedir. Referências entram como padrão observado, nunca como cópia. |
| `03-avatar-ads.md` (avatar, consciência, objeções, linguagem) + bloco `HANDOFF DO PROJETO` da Etapa 03 | Etapa 03 | Pedir. Sem avatar a skill não escreve promessa nem objeções. |
| Custos, preço mínimo e capacidade de entrega | Operador | Pedir. Sem isso, preço e viabilidade ficam marcados como **ausente** e não entram na recomendação. |
| Provas e diferenciais reais (o que existe hoje, com fonte) | Operador | Pedir. Sem prova, todo claim vira hipótese e a oferta não pode ser aprovada. |
| Regras da plataforma e do mercado (política de anúncios, categoria sensível, restrições legais) | Operador | Pedir. Define os claims proibidos. |

Formato da checagem: uma lista "Recebido / Faltando / Ausente por decisão do operador". Quando o operador declarar que algo não existe, registre como **informação ausente** e siga com a restrição correspondente. Não preencha o vazio.

## 1. Processo

### 1.1 Base da oferta
A partir das entradas, fixe em uma linha cada: **problema** (no vocabulário do avatar), **transformação** (estado atual → desejado, delimitada e responsável), **mecanismo do problema** e **mecanismo da solução**. Cada linha recebe rótulo (evidência / hipótese) e aponta a fonte no arquivo de origem.

### 1.2 Produto principal e pilha de valor
Liste o produto principal e os entregáveis com formato, acesso, suporte, prazo e limites. Bônus só entram se removem obstáculo, aceleram ou reduzem risco; caso contrário são volume. Registre o que a operação consegue entregar com a capacidade informada.

### 1.3 Três conceitos com ângulos distintos
Produza três conceitos, cada um com ângulo diferente (não três variações da mesma promessa). Preencha o formulário de conceito de `modelo-oferta-aprovada.md`, campo a campo:
avatar e problema · transformação · promessa responsável · mecanismo · produto principal · bônus · prova disponível · prova ainda necessária · garantia · preço e justificativa · objeções · riscos · headline e CTA provisórios.

Responda para cada conceito as **sete perguntas obrigatórias** (`offer-card-7-perguntas-hierarquia-prova.md`). Pergunta sem resposta sustentada = lacuna declarada no conceito.

### 1.4 Comparação e scorecard
Pontue cada conceito de 1 a 5 nos dez critérios do scorecard (`scorecard-da-oferta.md`): clareza, relevância para o avatar, diferenciação, credibilidade, força da prova, viabilidade de entrega, margem, reversão de risco, simplicidade da decisão, compliance. Nota baixa não se esconde com copy: vira pendência ou hipótese de teste, escrita ao lado da nota.

### 1.5 Recomendação
Recomende um vencedor e justifique com base em **evidência, clareza, desejo, credibilidade e viabilidade**, citando as notas do scorecard e os arquivos de origem. Diga o que os outros dois conceitos perdem e se algum elemento deles migra para o vencedor.

### 1.6 Validação do conceito recomendado
Antes de pedir aprovação, valide: promessa específica e comprovável; mecanismo claro; prova, garantia e preço coerentes com custos e capacidade informados; escassez real ou inexistente. Preencha o **Offer Card** completo (`offer-card-7-perguntas-hierarquia-prova.md`) para o conceito recomendado.

### 1.7 Aprovação humana
Apresente o Offer Card e peça aprovação formal. Registre quem aprovou e quando. Sem aprovação registrada, o arquivo fica como rascunho e o handoff marca "Portão de aprovação: pendente".

## 2. Saída obrigatória

Grave `04-oferta-aprovada.md` seguindo `modelo-oferta-aprovada.md`:

1. Resumo das entradas usadas (com o que ficou ausente).
2. Base da oferta (problema, transformação, mecanismos) com rótulos.
3. Três conceitos completos.
4. Scorecard comparativo.
5. Recomendação e justificativa.
6. Offer Card do conceito aprovado.
7. Claims e provas pendentes, riscos legais e operacionais.
8. Bloco `HANDOFF DO PROJETO`.

## 3. Checklist de saída

- [ ] Todas as entradas da seção 0 foram conferidas e o que falta está listado.
- [ ] Promessa é específica e comprovável.
- [ ] Mecanismo está claro.
- [ ] Valor percebido não depende de exageros.
- [ ] Preço e entrega são viáveis com os custos e a capacidade informados.
- [ ] Escassez e prova são reais.
- [ ] Nenhuma nota baixa do scorecard ficou sem pendência ou hipótese.
- [ ] Claims sensíveis marcados para revisão.
- [ ] Uma oferta foi formalmente aprovada (ou o arquivo está marcado como rascunho).
- [ ] Bloco `HANDOFF DO PROJETO` preenchido.

## 4. Handoff obrigatório

Encerre sempre com o bloco abaixo, todos os campos preenchidos. Somente a oferta aprovada alimenta a Etapa 05; conceitos descartados ficam registrados no arquivo, não no handoff.

```
HANDOFF DO PROJETO
Etapa concluída: 04 — Mineração de Ofertas
Versão e data:
Objetivo:
Entradas utilizadas:
Evidências confirmadas:
Hipóteses abertas:
Decisões aprovadas:
Artefatos produzidos: 04-oferta-aprovada.md
Claims e provas pendentes:
Riscos e restrições:
Métrica principal:
Portão de aprovação:
Próximo agente: 05 — Copy
Próxima ação única:
```

A Etapa 05 abre pedindo exatamente este bloco mais o Offer Card aprovado, o avatar e as provas autorizadas.


=====
### ARQUIVO: references/base-consciencia-sofisticacao-leads.md
=====

# Base: consciência, sofisticação e leads (Schwartz + Masterson & Forde)

Destilado operacional de "Breakthrough Advertising" (Eugene Schwartz) e "Great Leads"
(Michael Masterson & John Forde). Use para diagnosticar em que ponto o mercado está
e escolher headline, lead e mecanismo. Não é teoria — é checklist de decisão.

## 1. Desejo de massa

O desejo de massa é "a difusão pública de uma necessidade privada" (Schwartz, cap. 1,
p18): um desejo que já
existe, sozinho, na cabeça de milhões de pessoas, e que a copy não cria — só canaliza.
A copy nunca gera desejo do zero; ela pega esperança, medo ou vontade que já circula
no mercado e aponta essa energia para um produto específico. Tentar remar contra um
desejo de massa (vender o que o mercado não quer, do jeito que ele não quer) sempre
perde para quem segue a maré, não importa o orçamento.

O desejo de massa tem duas origens:
- **Forças permanentes** — instintos que não mudam (atração, virilidade, saúde,
  status) ou problemas técnicos não resolvidos (dor que volta, produto que falha).
  Aqui a tarefa não é descobrir o desejo — ele é óbvio — é diferenciar seu produto
  dos concorrentes que já exploram o mesmo instinto.
- **Forças de mudança** — tendências em início, ápice ou reversão (moda, medo
  econômico, nova tecnologia). Aqui a tarefa é sentir a maré cedo e migrar o ângulo
  antes da concorrência.

Todo desejo de massa tem três dimensões que você mede para escolher qual explorar:
**urgência** (quão forte é a dor agora), **poder persistente** (quão repetitivo,
insaciável) e **escopo** (quantas pessoas compartilham esse desejo). Um produto
sempre toca vários desejos de massa possíveis — a escolha de qual vai para a
headline é a decisão mais importante da copy.

Sequência de trabalho do redator: (1) escolher o desejo de massa mais forte que o
produto pode capturar; (2) declarar, reforçar ou apontar a solução desse desejo na
headline, no ponto de consciência exato em que o cliente já está; (3) mostrar que o
desempenho do produto satisfaz esse desejo.

[aplicação] Na mineração Trip Angle, use isto para separar "ângulo" (recorte de um
desejo de massa já existente) de "mecanismo" (a explicação de como o produto entrega
esse desejo) — são camadas diferentes do mesmo anúncio.

(Schwartz, cap. 1, p18)

## 2. Cinco níveis de consciência

Cada headline responde a uma pergunta: quanto esse mercado já sabe sobre o desejo e
sobre o seu produto? Quanto mais consciente, menos a copy precisa dizer.

| Nível | O cliente já sabe | O que a headline/lead deve fazer |
|---|---|---|
| 1. Mais consciente | Conhece o produto, sabe que funciona, só falta comprar | Ir direto ao nome do produto e ao preço/oferta. Zero criatividade exigida — é vitrine de loja. |
| 2. Consciente do produto | Conhece o produto, mas não está convencido ou não sabe de tudo que ele faz | Reforçar o desejo, ampliar a prova, estender onde/quando o produto entrega, apresentar novidade. |
| 3. Consciente da solução | Sabe que quer o resultado, não sabe que existe um produto que entrega | Nomear o desejo/solução na headline, provar que é alcançável, mostrar que o mecanismo está no seu produto. |
| 4. Consciente do problema | Sente a dor ou a necessidade, mas não liga isso a nenhuma solução | Nomear o problema (ou a solução) na headline, dramatizar a necessidade, depois apresentar o produto como solução inevitável. |
| 5. Totalmente inconsciente | Não percebe que tem o problema, ou não admite, ou o desejo é vago demais para virar frase | Não pode abrir com produto nem com problema direto — precisa de história, identificação ou choque de imagem para trazer o leitor até o desejo antes de nomeá-lo. |

Regra prática: comece a copy exatamente no ponto de consciência em que o leitor já
está. Abrir "abaixo" do nível dele soa condescendente e o perde; abrir "acima" (falando
do produto para quem nem sabe que tem o problema) soa sem contexto e ele não conecta.

(Schwartz, cap. 2, p29)

## 3. Estágios de sofisticação do mercado

Sofisticação mede quantas ofertas parecidas o mercado já viu — não o que ele sabe do
desejo (isso é consciência), mas o quanto ele já está cansado das promessas.

| Estágio | Sinal no mercado | Estratégia de promessa/mecanismo |
|---|---|---|
| 1. Primeiro no mercado | Ninguém fez essa promessa antes para esse público | Declaração direta e simples do desejo/benefício. Nada de mecanismo, nada de ângulo complexo — a novidade da promessa já vende. |
| 2. Segundo a chegar | A promessa direta já rodou, mas ainda é crível | Copie a promessa vencedora e amplie até o limite (mais forte, mais rápido, mais quilos, mais alcance). Funciona até estourar a credibilidade. |
| 3. Mercado saturado de promessa | Toda promessa já foi feita e ampliada ao extremo; ceticismo alto | Pare de brigar pela promessa, mude a arma: entre com um mecanismo novo ("como" funciona) que torna a mesma promessa antiga crível de novo. O mecanismo domina a headline. |
| 4. Mecanismo virou o novo campo de batalha | Concorrentes já lançaram mecanismos concorrentes | Amplie e refine o mecanismo (mais fácil, mais rápido, mais seguro, resolve mais) — mesma lógica de ampliação do estágio 2, agora aplicada ao "como". |
| 5. Mercado exausto | Ninguém mais acredita em promessa nem em mecanismo novo; concorrentes saindo do mercado | A ênfase sai da promessa/mecanismo e vai para identificação com o leitor (quem ele é, não o que ele ganha) — é o mesmo problema do nível 5 de consciência, resolvido pela técnica de Identificação. |

[aplicação] Na prática Trip Angle: estágio de sofisticação é o motivo pelo qual um
"copiar oferta vencedora" que funcionou há 1 ano pode falhar hoje — o mercado avançou
de estágio 2/3 para 4/5 e a mesma promessa nua não fecha mais.

(Schwartz, cap. 3, p54)

## 4. Sete técnicas de Schwartz para construir o corpo

| Técnica | Definição em uma linha | Como aplicar |
|---|---|---|
| Intensificação | Ampliar o desejo já despertado, multiplicando cenas concretas de realização | Depois de nomear o desejo, mostre-o de vários ângulos: prove a alegação, coloque em ação, traga testemunhos, compare com a concorrência, mostre o lado negativo de não ter, sele com garantia. |
| Identificação | Vender o papel/personalidade que o produto permite ao cliente assumir, não só a função física | Construa uma imagem de quem o comprador se torna (o papel, o status, a tribo) e ligue essa imagem ao produto — essencial quando o desejo funcional já está saturado. |
| Gradualização | Fazer o leitor crer na alegação antes de ela ser dita, para fundir desejo + crença em convicção | Construa a crença por etapas — fatos pequenos e aceitáveis primeiro, depois a conclusão maior — em vez de afirmar o benefício grande logo de cara. |
| Redefinição | Dar nova definição a uma desvantagem do produto (complicado, pouco importante, caro) para virar vantagem | Ataque a objeção antes que o leitor a levante: reframe defeito em prova de força (ex.: cheiro forte = prova de que o sabonete é potente). |
| Mecanização | Provar verbalmente que o produto faz o que promete, explicando o "como" | Siga três estágios: nomeie o mecanismo, descreva-o, dramatize-o em ação — responde à pergunta implícita do leitor "como isso funciona?". |
| Concentração | Atacar diretamente os outros caminhos que o leitor tem para satisfazer o mesmo desejo | Use quando dominar o mercado exigir eliminar alternativas — mostre por que os outros métodos falham, não apenas por que o seu funciona. |
| Camuflagem | Pedir emprestada a credibilidade de um veículo/formato em que o leitor já confia | Escreva a copy imitando o formato, o tom e o vocabulário do meio (editorial, notícia, carta pessoal) para herdar a confiança que o leitor já deposita nesse formato. |

(Schwartz, caps. 7–13, p90)

## 5. Great Leads: os seis tipos de lead

Masterson & Forde organizam os leads em uma escala de mais direto a mais indireto,
alinhada à escala de consciência de Schwartz: quanto mais consciente o leitor, mais
direto o lead pode ser; quanto menos consciente, mais indireto precisa ser.

| Tipo de lead | Definição | Quando usar (consciência) |
|---|---|---|
| Oferta | Vai direto à oferta — produto, preço, desconto, prêmio, garantia — já na headline ou nas primeiras linhas | Nível 1 (mais consciente): cliente já confia e já quer o produto, só falta o gatilho comercial. |
| Promessa | Abre com o maior benefício do produto, sem necessariamente citar o produto de cara | Nível 2: cliente conhece o produto/categoria, falta reforçar por que este é a melhor entrega do desejo. |
| Problema-solução | Adia o produto e abre com a questão emocional ("hot button") do leitor, depois liga à solução | Nível 3–4: cliente sente o problema ou já busca a solução, mas ainda não liga ao seu produto. |
| Grande segredo | Abre prometendo conhecimento exclusivo (fórmula, sistema, informação escondida), revelado ao comprar | Nível 3–4, quando a categoria já está cética e precisa de um motivo novo para acreditar. |
| Proclamação/revelação | Abre desarmando o leitor com um fato chocante, previsão ousada ou afirmação inesperada, propositalmente indireto | Nível 4–5: leitor não liga o problema à solução ou nem admite o problema — precisa ser abalado antes de ouvir a oferta. |
| História | Abre contando uma história (depoimento, trajetória, prova histórica) que conduz até a promessa | Nível 5 (inconsciente) ou qualquer nível quando o leitor desconfia de abordagem direta — a história rende engajamento sem pedir crença antecipada. |

Regras de ouro de um lead forte:
- **Regra do Um**: um lead vencedor carrega uma única Grande Ideia. Misturar duas
  ou três ideias centrais dilui a força de todas.
- Todo lead forte, direto ou indireto, contém cinco elementos: uma boa ideia, uma
  emoção essencial, uma história (ou gancho) cativante, um benefício desejável e
  uma reação inevitável (o que o leitor faz a seguir).
- Todo lead — por mais indireto que seja — precisa chegar ao benefício do produto e
  à oferta o mais cedo que o nível de consciência permitir. Indireto não é sinônimo
  de vago.
- A escolha direto vs. indireto não é de gosto: é function do quanto o leitor já
  confia em você, já aceita que o problema existe e já aceita que existe solução.

(Masterson & Forde, cap. 3)

## 6. Tabela-síntese: consciência × sofisticação → lead

| Consciência | Sofisticação típica | Tipo de lead recomendado | Foco da headline | Papel do mecanismo |
|---|---|---|---|---|
| 1. Mais consciente | Qualquer | Oferta | Nome do produto + preço/condição | Irrelevante — já aceito |
| 2. Consciente do produto | Estágio 1–2 | Promessa | Benefício mais forte do produto | Ausente ou coadjuvante |
| 3. Consciente da solução | Estágio 2–3 | Promessa ampliada / grande segredo | Solução nomeada, ampliada ao limite crível | Começa a aparecer como diferenciação |
| 4. Consciente do problema | Estágio 3–4 | Problema-solução / grande segredo | Problema dramatizado, depois mecanismo novo | Domina a headline — é o que renova a credibilidade |
| 5. Inconsciente / mercado exausto | Estágio 4–5 | Proclamação, revelação ou história | Choque, identificação ou narrativa — nunca o produto de cara | Secundário — a identificação com o leitor substitui a lógica do mecanismo |

[aplicação] Esta tabela cruza os dois eixos (Schwartz) com a escolha de lead
(Masterson & Forde); a combinação exata célula a célula é inferência minha — os
livros tratam consciência e sofisticação como eixos correlacionados, não idênticos, e
o operador deve checar os dois separadamente antes de travar o lead.

## 7. Checklist de diagnóstico de oferta

1. Qual desejo de massa específico este produto está canalizando — e ele é
   permanente ou uma tendência de mudança que pode virar amanhã?
2. Esse desejo, medido nas três dimensões (urgência, poder persistente, escopo),
   é forte o suficiente para sustentar a campanha, ou é secundário?
3. Em qual dos cinco níveis de consciência está o público que este anúncio/copy
   está tentando atingir — e a headline atual fala nesse nível ou em outro?
4. A headline exige que o leitor já saiba algo que ele ainda não sabe?
5. Em qual estágio de sofisticação este nicho está — quantas promessas parecidas
   o público já viu, e o mercado ainda acredita em promessa nua ou já exige
   mecanismo?
6. Se o estágio for 3+, existe um mecanismo nomeado e dramatizado, ou a copy só
   repete a promessa antiga com adjetivos mais fortes?
7. A copy usa alguma das sete técnicas (intensificação, identificação,
   gradualização, redefinição, mecanização, concentração, camuflagem) de forma
   deliberada, ou só empilha alegações soltas?
8. Existe uma desvantagem óbvia do produto (caro, complicado, nicho) que precisa
   de redefinição e ainda não foi endereçada?
9. Qual tipo de lead (dos seis) está sendo usado — e ele é compatível com o nível
   de consciência mapeado na pergunta 3?
10. O lead obedece à Regra do Um, ou está tentando vender duas ou três ideias
    centrais ao mesmo tempo?
11. O lead entrega os cinco elementos (ideia, emoção, história/gancho, benefício,
    reação inevitável) ou falta algum?
12. Se o mercado estiver no estágio 5 de sofisticação/consciência, a copy está
    usando identificação e história em vez de insistir em promessa e mecanismo?
13. O mecanismo, se existe, seria aceito como verossímil por este público
    específico, ou soa reciclado de outra oferta já vista?
14. Existe evidência (nos próprios anúncios/páginas coletados) de que o mercado já
    rejeitou esse ângulo — sinal de estágio de sofisticação mais avançado do que
    o suposto?
15. Se fosse necessário reabrir este mercado do zero (estágio 5), qual seria a
    nova promessa, o novo mecanismo ou a nova identificação a testar?


=====
### ARQUIVO: references/base-desejos-segmentacao-swipes.md
=====

# Base de Desejos, Segmentação e Swipes — Referência Operacional

Destilado de três fontes para uso em copy e modelagem de oferta: Drew Eric Whitman
(*Cashvertising*), Ryan Levesque (*Ask*) e Dan Kennedy (*Swipe Titans*). Escrito com as
próprias palavras do operador; citações literais são raras e sinalizadas.

## 1. Cashvertising — desejos e gatilhos psicológicos

### 1.1 Life-Force 8 (LF8) — desejos primários (biológicos, não aprendidos)

| # | Desejo | Aplicação em uma linha |
|---|---|---|
| 1 | Sobrevivência, prazer e prolongamento da vida | Use como base de qualquer promessa de saúde, segurança ou longevidade — é o desejo mais forte, ancore nele antes de qualquer secundário. |
| 2 | Prazer com comida e bebida | Em ofertas de alimentação/emagrecimento, venda o prazer sensorial do alimento, não só a restrição. |
| 3 | Liberdade do medo, dor e perigo | Nomeie o medo específico do nicho e prometa a remoção dele, não uma vaga "tranquilidade". |
| 4 | Companhia sexual / atração | Use em ofertas de estética, relacionamento e autoestima como benefício final, não como gancho vulgar. |
| 5 | Condições de vida confortáveis | Venda a redução de fricção e desconforto do dia a dia (tempo, dinheiro, esforço). |
| 6 | Ser superior, vencer, superar os vizinhos | Funciona em ofertas de status, dinheiro e performance — comparação social implícita vende. |
| 7 | Cuidado e proteção de quem se ama | Muito forte em ofertas de saúde e finanças familiares — o comprador age para proteger terceiros. |
| 8 | Aprovação social | Use prova social e transformação visível para quem "os outros vão notar". |

### 1.2 Desejos secundários (aprendidos) — reforçam, não substituem o LF8

Estar informado; curiosidade; higiene do corpo e do ambiente; eficiência; conveniência;
confiabilidade/qualidade; expressão de beleza e estilo; economia/vantagem; pechincha.
**[aplicação]** use-os em bullets e objeções, nunca como promessa central — eles não têm
tração biológica.

### 1.3 Princípios e técnicas de copy (seleção com aplicação)

- **Fator medo** — nomeie o pior cenário antes de oferecer a saída. [aplicação]
- **Transformação de ego** — deixe o leitor se identificar com quem ele quer ser, não quem é hoje.
- **Transferência (credibilidade por associação)** — empreste autoridade de uma fonte já confiável (especialista, mídia, instituição).
- **Efeito carona (bandwagon)** — mostre volume de gente já comprando/agindo para reduzir o risco percebido de ser o primeiro.
- **Cadeia meios-fins** — conecte o atributo do produto ao benefício final que o LF8 realmente quer, em 2-3 passos explícitos.
- **6 armas de influência (Cialdini)** — reciprocidade, compromisso, prova social, autoridade, afeição, escassez: escolha 2 por peça, não as seis juntas.
- **Exemplos vs. estatística** — histórias específicas convencem mais que números frios; use números para sustentar a história, não substituí-la.
- **Perguntas retóricas** — force concordância silenciosa antes do pedido de ação.
- **Repetição e redundância** — repita a promessa central em 3+ pontos da peça com palavras diferentes.
- **Heurísticas (atalhos mentais)** — preço "ancorado", "mais vendido", "recomendado por" poupam o leitor de pensar — use com honestidade.
- **Bombardeio de benefícios** — liste benefícios em profusão antes de qualquer detalhe técnico.
- **Maior benefício no título** — nunca enterre a melhor promessa no meio do texto.
- **Aumento de escassez** — escassez real (unidades, vagas, prazo) supera qualquer adjetivo de urgência.
- **Especificidade extrema** — números exatos ("37 dias", "R$ 214,90") são mais cridos que "rápido" ou "barato".
- **Prova social** — depoimento com nome, contexto e resultado específico vale mais que nota genérica de estrelas.
- **PVA (linguagem visual positiva)** — escreva para instalar um "filme mental" do uso do produto, com verbos de ação e detalhes sensoriais.
- **Direção de filmes mentais** — descreva a cena do resultado (onde, o quê, como se sente) em vez de afirmar o benefício de forma abstrata.
- **Combater a inércia** — dê um primeiro passo tão pequeno que recusar pareça mais custoso que aceitar.
- **USP (proposta única de venda)** — defina o que só a sua oferta entrega e repita como coluna vertebral da peça.
- **Psicologia do preço** — preço quebrado, parcelamento e comparação com alternativa mais cara mudam a percepção de valor.
- **"Cleverectomia"** — corte qualquer trocadilho ou criatividade que atrapalhe o entendimento imediato da oferta.

Fonte: Drew Eric Whitman, *Cashvertising* (ed. espanhola), cap. 1 "Lo que la gente
realmente quiere" (LF8 e desejos secundários, p. 20-23), cap. 2 "17 principios
fundamentales" (p. 29+), cap. 3 "41 técnicas" (p. 79+) e cap. 4 "101 maneiras" (p. 187+).
Citação literal: "Los llamo Life-Force 8 (LF8 para abreviar)" (Whitman, *Cashvertising*, p. 21).

## 2. Ask (Ryan Levesque) — pesquisa de público e segmentação

Framework do livro (cap. 12, "The Process"): **Prepare → Persuade → Segment → Prescribe
→ Profit → Pivot**, apoiado em quatro pesquisas sequenciais (a "Survey Funnel Strategy"):

1. **Deep Dive Survey** (Prepare) — pesquisa aberta enviada à lista ou captada em landing
   page de tráfego frio. Uma única pergunta central: *"What's your #1 single biggest
   marketing challenge right now?"* (Levesque, *Ask*, cap. 13, p. 80) — adaptar para "qual
   é o seu maior desafio/frustração com [tema]" sempre em formato aberto. Não ofereça
   incentivo genérico (sorteio, brinde caro): isso atrai respondente errado e polui a
   linguagem coletada. O objetivo é capturar a linguagem natural do cliente, não validar uma hipótese.
2. **Prospect Self-Discovery Landing Page** (Persuade) — página simples com a pergunta
   aberta como isca, sem formulário longo; a promessa é ajudar o próprio respondente a
   entender seu problema (o "ethical bribe" pode ser um relatório/kit gratuito ligado ao tema).
3. **Micro-Commitment Bucket Survey** (Segment) — depois da Deep Dive, monta-se um quiz de
   múltipla escolha que começa com uma pergunta binária de baixíssimo atrito (A/B, não
   ameaçadora) antes de pedir e-mail ou dados sensíveis — a lógica é criar "momentum de
   compromisso" com decisões pequenas e sucessivas. As respostas classificam o respondente
   em "buckets" (segmentos), que passam a receber mensagem, oferta e produto diferentes.
4. **"Do You Hate Me?" Survey** — enviada a quem não comprou, pergunta direta pelo maior
   motivo de não ter comprado; usada para corrigir objeções na copy e na oferta.
5. **Pivot** — sequência de e-mail de acompanhamento que realimenta o ciclo com o
   comportamento observado.

**Como transformar respostas em copy e segmentação de oferta:**
- As frases literais mais repetidas na Deep Dive viram manchete, subtítulos e bullets — é a
  linguagem do próprio cliente, não a do redator. [aplicação]
- Os motivos mais frequentes de "maior desafio" definem os buckets; cada bucket recebe uma
  landing page, e-mail ou oferta de upsell prescrita para ele (etapa "Prescribe"). [aplicação]
- Perguntas de "personalização" (idade, tipo de negócio, estágio) alimentam campos de
  mesclagem (merge fields) para e-mail e VSL personalizados por segmento.
- O "Do You Hate Me" survey vira checklist de objeções a antecipar na página de vendas e no
  script de criativo. [aplicação]

Fonte: Ryan Levesque, *Ask* (Dunham Books, 2015), Parte II — cap. 12 "The Process", cap.
13 "Prepare: The Deep Dive Survey", cap. 14 "Persuade: The Prospect Self-Discovery
Landing Page", cap. 15 "Segment: The Micro-Commitment Bucket Survey" (PDF sem texto
extraível; lido via renderização de página, cap. 12-15).

## 3. Swipe Titans (Dan Kennedy) — padrões estruturais recorrentes

Amostragem de cartas e anúncios comentados no arquivo (não reproduzidos, apenas
estrutura descrita):

| Elemento | Padrão observado | Aplicação em uma linha |
|---|---|---|
| Abertura por dor nomeada | Carta do "Giorgio" (jantar romântico): título com imagem, endereçada diretamente ao marido, problema do casamento nomeado na 1ª linha. | Nomeie a dor do leitor específico na primeira frase, antes de qualquer credencial. |
| Abertura por metáfora estendida | Promoção de evento usa metáfora de "circo" (picadeiro, atrações) para organizar toda a oferta. | Uma metáfora única sustentada do início ao fim organiza ofertas com muitos componentes. |
| Abertura por alerta/ameaça | Carta B2B a CFOs de hospital abre com "WARNING" e metáfora de tempestade/maré. | Em B2B ou temas de risco, o alerta direto supera a curiosidade suave como gancho. |
| Uso de história | Carta de confirmação de evento usa a história pessoal do fundador como diferenciação, evitando o clichê "do zero ao topo" quando não é verdade. | Conte a história real, mesmo que não seja de superação — autenticidade pesa mais que arquétipo. |
| Prova | Caso de sucesso nomeado (nome, cidade, investimento e retorno exatos: "US$74,12 geraram US$4.812"). | Prova forte é nominal e numérica, nunca genérica ("muita gente aprovou"). |
| Oferta | Segunda carta de reativação ao mesmo prospect soma um novo incentivo (limusine) sem tirar o anterior. | Ao reabordar quem não comprou, acrescente valor à oferta original em vez de só descontar o preço. |
| Garantia | Garantia de até o triplo do valor de volta, condicionada a "abertura de mente", não a resultado místico. | Garantias fortes reduzem risco percebido sem prometer o impossível — condicione ao esforço mínimo do comprador. |
| Prazo | Desconto por data-limite explícita + tabela de vagas limitadas justificada (capacidade real do evento). | Combine prazo de preço com limite de vagas apenas quando ambos forem reais — a dupla urgência funciona porque é verdadeira. |
| P.S. em camadas | Carta de inscrição de seminário usa P.S. #1, #2 e #3, cada um somando um motivo novo (palestrante extra, garantia, objeção). | Use múltiplos P.S. para empilhar razões independentes de agir, não para repetir a mesma. |
| "Reason why" | Preço e prazo do bônus sempre justificados ("por isso o desconto expira em tal data"). | Toda condição especial de oferta precisa de uma razão explícita — nunca "porque sim". |
| Sequência de concordância | Comentário do autor: mapear, de trás para frente, cada concordância que o leitor precisa dar antes da compra, e escrever nessa ordem. | Antes de redigir, liste as objeções/crenças que precisam cair uma a uma até a venda, e siga essa ordem no texto. |
| Extremos emocionais e autoidentificação | Comentário do autor: boa copy de resposta direta usa extremos (porque é preciso força para vencer hábito) e manchetes de autoidentificação ("se você é..."). | Escreva manchetes que filtrem o leitor certo por identidade/papel, não só por interesse no tema. |

Citação literal: "Great direct-response copy takes people into dark (emotional) places
then provides relief by purchase." (Dan Kennedy, *Swipe Titans*, p. 44).

Fonte: Dan Kennedy, *Swipe Titans* (GKIC/Kennedy Inner Circle, resource book), cartas
"Giorgio's Italian Grotto" (cap. 12 do *Ultimate Sales Letter*, p. 138-141), "The SECRET
Psychology of Direct-Response" (p. 44), carta de confirmação Phill Grove (p. 206-207),
carta CFO hospitalar (p. 111-112), carta de inscrição de seminário (p. 263-266).

## 4. Mapa desejo → dor → promessa → prova **[aplicação]**

Síntese própria, cruzando LF8 (Cashvertising), linguagem de pesquisa (Ask) e prova
nominal (Swipe Titans). Use como template ao construir persona de oferta:

| Desejo (LF8/secundário) | Dor / tensão (o que a falta dele produz) | Promessa (transformação vendida) | Prova exigida |
|---|---|---|---|
| Condições de vida confortáveis | Cansaço, falta de tempo, sobrecarga diária | "Resolva X em [tempo curto] sem mudar sua rotina" | Depoimento nominal com contexto de rotina real |
| Ser superior / aprovação social | Comparação com pares, medo de ficar para trás | "Alcance [resultado visível] antes de [prazo/evento]" | Antes/depois verificável, nome e contexto |
| Liberdade do medo/dor | Ansiedade com um risco específico (saúde, dinheiro) | "Elimine [risco nomeado] com [mecanismo]" | Fonte de autoridade + mecanismo explicado, não só afirmado |
| Cuidado com quem se ama | Culpa por não proteger terceiros | "Proteja [pessoa/família] de [ameaça]" | Caso real de terceiro protegido, nunca hipotético |

Preencha as colunas com a linguagem literal coletada na Deep Dive Survey (seção 2), não
com adjetivos do redator — é o que garante que a promessa bate no desejo certo.

Fonte: síntese do operador a partir das seções 1-3 deste documento.

## 5. Checklist para intensificar desejo sem inventar prova **[aplicação]**

1. Ancore a promessa central em um LF8 explícito, não apenas em desejo secundário.
2. Escreva com linguagem visual específica (PVA) para instalar o "filme mental" do resultado.
3. Nomeie a dor com as palavras exatas do cliente, coletadas em pesquisa (Deep Dive/comentários), não em jargão de nicho.
4. Coloque o maior benefício no título ou nos primeiros segundos, nunca enterrado no meio.
5. Reduza a distância entre desejo e ação com um próximo passo de baixíssimo atrito (micro-compromisso).
6. Use perguntas retóricas para gerar concordância silenciosa antes de pedir a ação.
7. Mapeie a sequência de concordâncias necessárias e escreva a copy nessa ordem, de trás para frente.
8. Intensifique com contraste antes/depois real (o que muda na rotina), sem inflar números.
9. Use manchetes de autoidentificação ("se você é...") para qualificar o leitor certo.
10. Explique sempre o motivo ("reason why") do preço, do prazo e do bônus.
11. Reforce com prova social nominal já existente — nunca fabrique depoimento ou estatística.
12. Feche com P.S. que reforce o maior desejo e uma urgência real, nunca escassez falsa.


=====
### ARQUIVO: references/base-headlines-e-copy-testada.md
=====

# Base de headlines e copy testada — Hopkins, Caples, Schwab

Destilado de três clássicos de resposta direta para uso operacional na modelagem de ofertas. Fontes: Claude Hopkins, *Scientific Advertising*; John Caples, *Tested Advertising Methods*; Victor Schwab, *How to Write a Good Advertisement* (tradução automática consultada). Nota de origem: o arquivo de Caples fornecido para extração veio com OCR corrompido (texto ilegível em toda a extensão); a seção 2 usa o conteúdo consolidado e amplamente documentado do livro, em prosa própria, sem citação literal nem número de página.

## 1. Hopkins — princípios operacionais

| Princípio | O que ele defende | Aplicação |
|---|---|---|
| Publicidade é só venda | Copy é venda escrita multiplicada; todo anúncio deve se justificar como um vendedor se justificaria | [aplicação] meça cada bloco de copy perguntando "isso ajudaria um vendedor a fechar pessoalmente?" |
| Oferecer serviço, não pedir compra | O leitor é egoísta; anúncio bom vende informação e vantagem, não grita "compre" | [aplicação] abra a oferta pelo problema resolvido, não pelo nome do produto |
| Ser específico | Números e fatos concretos pesam; superlativo genérico é descontado pelo leitor | Hopkins cita: "Chavões e generalidades rolam do entendimento humano como água de um pato" (Hopkins, p.30) |
| Amostragem e prova de risco zero | Reduzir o risco do primeiro contato (amostra, teste grátis, devolução) converte melhor que pedir decisão de compra direta | [aplicação] toda oferta nova testa uma variante com trial, amostra ou garantia estendida antes de subir orçamento |
| Campanha de teste acima de opinião | Nenhuma discussão de mesa decide o que funciona; só o teste em pequena escala, com custo e retorno medidos, decide | [aplicação] nunca escale criativo ou oferta sem teste controlado prévio em orçamento pequeno |
| Psicologia do leitor | O publicitário competente entende por que certos estímulos levam à ação; a copy deve seguir reação humana previsível, não gosto pessoal | [aplicação] valide hipótese de gatilho psicológico com dado de resposta, não com preferência do time |
| Headline seleciona o leitor certo | A função do título é isolar quem pode se interessar, não agradar a todos | [aplicação] escreva o headline pensando em uma pessoa específica da persona, não no "público geral" |
| Contar a história completa | O anúncio deve resolver a objeção até o fim; corte por medo de tamanho é erro, não virtude | [aplicação] a VSL ou página só corta quando a objeção foi de fato neutralizada, nunca por "está longo" |
| Nome que carrega a promessa | Um nome de produto ou mecanismo que já conta parte da história economiza esforço de venda | [aplicação] nomeie mecanismo e oferta com uma palavra que já sugira o benefício ou o inimigo |
| Individualidade | Uma voz e um personagem reconhecíveis rendem mais confiança que um anúncio genérico do mercado | [aplicação] fixe um narrador ou personagem consistente na oferta em vez de trocar voz a cada criativo |
| Os melhores anúncios não pedem para comprar | A copy vende demonstrando serviço; o pedido de compra é consequência, não abertura | Hopkins cita: "Os melhores anúncios não pedem a ninguém para comprar" (Hopkins, p.15) |

**Fonte:** Claude Hopkins, *Scientific Advertising*, capítulos 2 (Apenas vendas), 3 (Oferecer serviço), 5 (Manchetes), 6 (Psicologia), 7 (Ser específico), 13 (Uso de amostras), 15 (Campanhas de teste), 17 (Individualidade), 20 (Um nome que ajuda).

## 2. Caples — o que faz uma headline funcionar

**Os três motores de interesse:**
- **Interesse próprio (self-interest):** o leitor só para quando o título promete algo que resolve a vida dele — ganho, economia, ou solução de um incômodo nomeado.
- **Novidade:** anúncio de algo novo (produto, método, descoberta) tira o leitor do piloto automático porque ele ainda não tem uma resposta pronta para ignorar aquilo.
- **Curiosidade:** funciona como gatilho de atenção, mas sozinha (sem benefício embutido) tende a atrair curioso que não compra; Caples recomenda sempre casar curiosidade com um benefício explícito na mesma frase.

**Categorias de headline com o histórico de resposta mais forte, documentadas por Caples:**
1. Oferta gratuita ou de baixo risco anunciada já no título.
2. "Como fazer" (how-to) — promete um método replicável.
3. Pergunta direta que o leitor já se fez sobre o próprio problema.
4. Notícia — algo nomeado como novo, lançado, descoberto.
5. Testemunho/depoimento em primeira pessoa como manchete.
6. Comando direto ao leitor (verbo de ação no imperativo).
7. Redução de risco explícita (garantia, teste, devolução) já na chamada.

**Padrões de abertura documentados no livro (moldes, não frases literais):**
- Abertura por "Como [verbo] [resultado]" — a fórmula mais recorrente nos testes do autor.
- Abertura por pergunta que nomeia o problema do leitor antes de qualquer menção ao produto.
- Abertura por anúncio de novidade ("Agora", "Novo", "Anunciamos").
- Abertura por número ("X maneiras de", "X motivos para") quando o corpo entrega uma lista real.
- Abertura por depoimento citado, com atribuição a uma pessoa nomeada ou perfil de cliente.

**Regras para o corpo da copy:**
- Frase e parágrafo curtos; uma ideia por parágrafo, sem embutir dois argumentos na mesma sentença.
- Falar direto com "você", nunca em terceira pessoa distante.
- Substituir adjetivo vago por número, prazo ou fato checável.
- Repetir o benefício central mais de uma vez com ângulos diferentes, não só uma vez no topo.
- Fechar todo bloco de argumento com a ponte para a ação, nunca deixar o leitor "só informado".

**O que testar primeiro (ordem de prioridade documentada):**
1. Headline — é o elemento que mais move o retorno; teste-a antes de qualquer outra coisa.
2. Oferta e condição de risco (preço, garantia, bônus) — segundo maior impacto.
3. Formato e extensão do corpo da copy.
4. Layout, imagem e elementos visuais — testado por último, porque move menos o resultado do que o texto.

**Fonte:** John Caples, *Tested Advertising Methods* — síntese de conteúdo consolidado da obra; arquivo-fonte fornecido estava com OCR ilegível, sem citação literal nem número de página.

## 3. Schwab — a estrutura de um bom anúncio

| Passo | Função | Aplicação |
|---|---|---|
| 1. Chamar atenção | Vencer a concorrência editorial e de outros anúncios pela própria manchete ou layout | [aplicação] teste o headline isolado, fora do design, perguntando se ele para o scroll sozinho |
| 2. Mostrar vantagem | Deixar claro, cedo, o que o leitor ganha ou economiza usando o produto | [aplicação] a vantagem central aparece nos primeiros segundos de VSL ou na dobra da página |
| 3. Provar | Sustentar a vantagem com prova concreta antes de pedir crença cega | [aplicação] cada claim de benefício vem com prova associada na mesma seção, não só no fim |
| 4. Persuadir a agarrar a vantagem | Traduzir a prova em desejo pessoal de posse, não só em concordância intelectual | [aplicação] reforce identidade e resultado emocional, não apenas o dado técnico |
| 5. Pedir ação | Fechar com instrução clara do próximo passo, sem deixar a decisão em aberto | [aplicação] todo bloco de fechamento tem um único CTA visível, sem ambiguidade |

Schwab reforça que o leitor é um "convidado não convidado" na publicação: "Você, o anunciante, é o Convidado Não Convidado" (Schwab, p.5) — a copy compete por um espaço que não lhe pertence, então precisa pagar a entrada com relevância imediata.

**Categorias de headline descritas por Schwab:**
- **Positiva (ganho):** mostra o que o leitor ganha, economiza ou realiza usando o produto.
- **Negativa (evitar perda):** mostra o risco, erro ou desconforto que o produto evita — Schwab observa que o medo de perder algo que já se tem costuma pesar mais que a chance de ganhar algo novo.
- **Curiosidade pura:** atrai atenção mas, sem benefício embutido, gera leitura de compromisso frouxo.
- **Apelo ao específico:** número, prazo ou fato concreto no título aumenta a crença mais que o adjetivo genérico.
- **Novo vs. velho e testado:** o apelo à novidade compete com o apelo à segurança do que já é comprovado; a escolha depende de qual objeção pesa mais na persona.

**Desejos humanos listados por Schwab** (a lista que ele recomenda usar para ancorar todo benefício):
saúde e vitalidade · mais dinheiro (ganhar, gastar, economizar, doar) · segurança na terceira idade e independência · avanço profissional e social · mais conforto e lazer · aparência e beleza · aprovação e popularidade · orgulho de realização e de posse · superar obstáculos e competição · curiosidade satisfeita · ser reconhecido como autoridade · pertencer e ser aceito socialmente · proteger quem se ama.

**Fonte:** Victor Schwab, *How to Write a Good Advertisement*, capítulo 1 (Chamar atenção) e capítulo sobre vantagens/desejos humanos (tradução automática consultada, p.4–5, p.39–42).

## 4. Banco de padrões de headline e hook

Moldes com lacunas para preencher por oferta — não são frases dos livros, são estruturas extraídas do padrão documentado. Nível de consciência na escala: inconsciente · consciente do problema · consciente da solução · consciente do produto · mais consciente.

| # | Molde | Origem | Nível de consciência |
|---|---|---|---|
| 1 | Como [resultado desejado] sem [sacrifício comum] em [prazo] | Caples | Consciente do problema |
| 2 | [Número] [pessoas/casos] descobriram como [resultado] mesmo [obstáculo] | Caples | Consciente da solução |
| 3 | O erro em [hábito/área] que está [custando/sabotando] seu [resultado] | Hopkins (especificidade) | Consciente do problema |
| 4 | Descubra por que [grupo] consegue [resultado] enquanto [maioria] continua [problema] | Schwab (curiosidade + benefício) | Consciente do problema |
| 5 | Anunciamos: [novidade/mecanismo] que [benefício específico] | Caples (novidade) | Inconsciente / consciente do produto |
| 6 | Você também comete esse erro em [área]? | Schwab (negativo/pergunta) | Consciente do problema |
| 7 | [Prova social: número] já [resultado] usando [método] — veja como | Caples (testemunho) | Consciente da solução |
| 8 | A verdade sobre [crença comum] que [autoridade/indústria] não conta | Schwab (curiosidade) | Consciente do problema |
| 9 | [Nome do mecanismo]: o motivo real por trás de [problema] | Hopkins (nome que ajuda) | Consciente do problema |
| 10 | Se você consegue [ação simples], você consegue [resultado maior] | Caples (facilidade) | Consciente da solução |
| 11 | [Quantidade específica] em [prazo específico] — sem [sacrifício comum] | Hopkins (especificidade) | Consciente da solução |
| 12 | Pare de [ação errada comum] antes que [consequência nomeada] | Schwab (evitar perda) | Consciente do problema |
| 13 | Como [pessoa comum] conseguiu [resultado] mesmo com [limitação relacionável] | Caples (história pessoal) | Consciente do problema |
| 14 | O [adjetivo] jeito de [resultado] que [grupo/autoridade] usa | Schwab (aprovação social) | Consciente da solução |
| 15 | [Risco evitado] garantido: [condição da garantia] ou [devolução] | Hopkins (amostragem/risco zero) | Consciente do produto |
| 16 | Novo em [ano/contexto]: [mecanismo] substitui [método antigo e desgastado] | Caples (novo vs. velho) | Consciente da solução |
| 17 | [Número] sinais de que [problema] está [piorando/custando caro] | Schwab (específico + negativo) | Consciente do problema |
| 18 | O que [autoridade/especialista] faz de diferente para [resultado] | Caples (autoridade) | Consciente da solução |
| 19 | Antes de [ação que a persona já faz], leia isto sobre [risco oculto] | Schwab (curiosidade + perda) | Consciente do problema |
| 20 | [Resultado] em [prazo curto] — o método que [instituição/grupo] testou | Hopkins (teste/prova) | Consciente da solução |
| 21 | Por que [crença popular] está errada sobre [tema da oferta] | Schwab (curiosidade) | Inconsciente |
| 22 | A pergunta que [persona] devia se fazer antes de [decisão comum] | Caples (pergunta) | Consciente do problema |
| 23 | [Número] passos para [resultado], mesmo começando do zero | Caples (lista/how-to) | Consciente da solução |
| 24 | O que ninguém te disse sobre [problema] antes de [evento/decisão] | Schwab (curiosidade + negativo) | Consciente do problema |
| 25 | De [situação ruim nomeada] para [resultado desejado] em [prazo] | Hopkins (específico) + Caples (história) | Consciente do problema |
| 26 | [Grupo específico]: veja como [resultado] sem [objeção comum da persona] | Hopkins (headline seleciona o leitor) | Consciente da solução |
| 27 | O teste que provou que [crença comum sobre a categoria] está errada | Hopkins (campanha de teste) | Consciente da solução |
| 28 | Só funciona se você [condição simples] — veja se é o seu caso | Schwab (qualificação) | Consciente do problema |
| 29 | [Autoridade/instituição] recomenda [ação] para quem sofre com [problema] | Schwab (autoridade + aprovação) | Consciente da solução |
| 30 | A [objeção comum] que impede [resultado] tem solução em [prazo] | Caples (self-interest + objeção) | Consciente do problema |

**Fonte:** moldes derivados de Hopkins (cap. 5, 7, 13, 15, 20), Caples (categorias e fórmulas de abertura documentadas no livro) e Schwab (cap. 1 e lista de desejos humanos, p.5–42).

## 5. Checklist de revisão de copy

1. O headline isola a persona certa, não tenta agradar todo mundo (Hopkins).
2. O headline promete um benefício específico, não um clichê ou superlativo vago (Hopkins).
3. A vantagem principal aparece cedo, nos primeiros segundos ou na primeira dobra (Schwab).
4. Toda claim de benefício vem com prova associada na mesma seção (Schwab).
5. A copy fala direto com "você", em frases e parágrafos curtos (Caples).
6. Números, prazos e fatos concretos substituem adjetivo genérico onde for possível (Hopkins).
7. O anúncio oferece serviço ou informação antes de pedir a compra (Hopkins).
8. Existe redução de risco explícita — amostra, teste, garantia ou devolução (Hopkins).
9. A objeção mais forte da persona foi nomeada e respondida, não ignorada (Hopkins/Schwab).
10. O benefício central é repetido mais de uma vez, com ângulos diferentes (Caples).
11. Todo bloco de argumento termina com uma ponte para a ação, sem deixar o leitor só "informado" (Caples).
12. O fechamento pede uma ação única e clara, sem ambiguidade sobre o próximo passo (Schwab).
13. A voz e o personagem da copy são consistentes do início ao fim (Hopkins).
14. Pelo menos um elemento de novidade ou curiosidade está casado com um benefício explícito, nunca sozinho (Caples).
15. Existe um plano de teste definido: qual elemento muda primeiro (headline), o que muda depois (oferta), o que muda por último (formato/visual) (Caples/Hopkins).

**Fonte:** consolidado de Hopkins (*Scientific Advertising*), Caples (*Tested Advertising Methods*) e Schwab (*How to Write a Good Advertisement*).


=====
### ARQUIVO: references/base-oferta-e-mecanismo.md
=====

# Base de Oferta e Mecanismo — Hormozi, Carneiro e Kennedy

Referência operacional para modelar oferta, mecanismo e carta de vendas. Use junto com a metodologia Trip Angle (mineração → leitura → modelagem → criação).

> **Aviso de fonte:** o arquivo `hormozi-100m-offers.txt` fornecido está corrompido (texto embaralhado, sem nenhuma ocorrência real dos termos "value equation", "grand slam", "dream outcome", "guarantee", "scarcity" etc. — é lixo de OCR/anti-pirataria, não o livro). A seção 1 foi escrita com conhecimento consolidado do conteúdo público do livro $100M Offers, sem citação literal e sem número de página verificável. Trate como paráfrase de alta confiança, não como transcrição.

## 1. Hormozi — $100M Offers

### 1.1 Equação de Valor (4 variáveis)

| Variável | O que é | Como mexer para cima |
|---|---|---|
| Resultado dos sonhos | O estado final que o cliente quer (não a feature) | Aumente a ambição da promessa; venda o resultado, não o processo |
| Probabilidade percebida de sucesso | Quanto o lead acredita que VAI dar certo pra ele | Prova (depoimento, case, número), garantia, autoridade, demonstração |
| Tempo até o resultado | Distância entre comprar e sentir o benefício | Quick wins, resultado parcial rápido, entrega imediata de uma parte |
| Esforço e sacrifício percebidos | Trabalho, dinheiro, dor, mudança de hábito exigidos | Simplifique passos, remova decisões, entregue "feito para você" |

Regra prática: valor sobe quando o numerador (resultado × probabilidade) cresce e o denominador (tempo × esforço) encolhe. Toda melhoria de oferta é, no fundo, mexer em uma dessas quatro alavancas. [aplicação: ao auditar uma oferta minerada, classifique cada elemento novo do concorrente em qual das 4 variáveis ele ataca]

### 1.2 Grand Slam Offer — passo a passo

1. **Liste os problemas** que o cliente enfrenta no caminho até o resultado dos sonhos (sequência cronológica, do primeiro obstáculo ao último).
2. **Transforme cada problema em solução** (uma frase de solução para cada problema listado).
3. **Defina o veículo de entrega de cada solução** — o "como" você entrega: cursos, templates, chamadas, software, feito-para-você, comunidade, etc. Para cada veículo, pergunte três coisas: como entregar mais resultado, como entregar mais rápido, como entregar com menos esforço do cliente.
4. **Corte e empacote (trim & stack):** elimine os itens de alto custo/baixo valor percebido para você e mantenha os de alto valor percebido/baixo custo de entrega. O que sobra vira o stack final da oferta.

### 1.3 Mercado e precificação

Critérios de um mercado bom: dor forte e urgente (não capricho), público com poder de compra, fácil de alcançar/segmentar, mercado em crescimento (não encolhendo). Oferta boa em mercado ruim perde para oferta mediana em mercado bom.

Precificação: cobrar mais, não menos, costuma aumentar o resultado do negócio — preço alto financia melhor entrega, atrai cliente mais comprometido e permite garantias mais fortes. O preço deve refletir o valor percebido (equação acima), não o custo de produção. [aplicação: ao modelar, teste preço acima do concorrente principal se a oferta ataca melhor as 4 variáveis]

### 1.4 Melhoria da oferta: escassez, urgência, bônus, garantias, nome

- **Escassez:** limitar quantidade (vagas, unidades, atendimentos). Só vale se a limitação for real — escassez falsa mina a confiança e a garantia (variável 2 da equação) no médio prazo.
- **Urgência:** limitar tempo (prazo de inscrição, turma, preço promocional, bônus por tempo). Mesma regra: só use prazo que você vai cumprir.
- **Bônus:** empacote bônus que resolvem objeções específicas (uma por bônus), nomeie cada um, e apresente o valor somado antes do preço final — o stack de bônus pode valer mais que o produto principal aos olhos do lead.
- **Garantias:** incondicional (devolve por qualquer motivo), condicional (devolve se cumprir X e não funcionar), anti-garantia (declara que não há devolução e explica por quê, usado para qualificar), garantia implícita/de performance (só paga se o resultado acontecer). Escolha a garantia pela variável que mais precisa reforçar: probabilidade percebida.
- **Nomeação da oferta:** nome forte junta avatar + resultado específico + prazo + palavra-recipiente (sistema, método, protocolo, desafio) + gancho de mecanismo. Nome genérico perde no leilão de atenção contra nome específico.

**Fonte:** Alex Hormozi, *$100M Offers* — capítulos "A Equação de Valor", "Como Criar sua Oferta Grand Slam" e "Aumente o Valor Percebido" (conteúdo consolidado; página não verificável — arquivo-fonte corrompido, ver aviso acima).

## 2. Carneiro — Copy e Mecanismo

**O que é mecanismo:** a explicação lógica/técnica que faz a promessa parecer inevitável, não apenas desejável. Carneiro divide o mecanismo em três camadas:

- **Mecanismo do problema:** a causa raiz da dor (não o sintoma). Ex.: não é "estar gordo", é o corpo não produzir hormônio de saciedade.
- **Mecanismo da função:** a ponte lógica — o que precisa acontecer fisiologicamente ou logicamente para resolver a causa raiz.
- **Mecanismo da solução:** o produto/método específico que executa essa função.

**Como construir:** não é invenção, é descoberta e associação. Três caminhos: (1) mineração de hypes atuais — pegar o mecanismo de ação de algo em alta (ex.: hormônios GLP-1/GIP do Ozempic) e associar a um produto próprio; (2) mineração histórica — resgatar mecanismo antigo e esquecido, que soa novo para a audiência atual; (3) pesquisa em ferramentas de tendência (Google Trends, comentários virais de YouTube/TikTok) para achar o ingrediente/termo que vira o mecanismo da solução.

**Erros:** tratar o mecanismo como precisando ser 100% original (trava a criação); usar o mesmo nome de mecanismo que um concorrente que investe mais em mídia — "se for genérico ou igual ao da concorrência, a performance cai" (Carneiro, p.4); construir mecanismo sem prender a um problema validado (que já convertia antes).

**Ligação com promessa e copy:** o mecanismo só funciona colado a uma Big Idea formada por **pergunta paradoxal** (explora uma crença ou preconceito social — ex.: "por que japonesas comem arroz e são magras?") + **nome chiclete** (nome que gruda, usando associações que a audiência já tem). Na estrutura da carta/VSL, o mecanismo é o que resolve o paradoxo e sustenta a promessa contra ceticismo. Na entrega (VSL → CSL), o mecanismo precisa ser vestido de conteúdo que a audiência já consome voluntariamente (vlog, entrevista, podcast), não de discurso de vendas explícito.

**Fonte:** Derick Carneiro, *Copy e Mecanismo* (texto curto, lido integralmente), páginas 1–4.

## 3. Kennedy — The Ultimate Sales Letter

Passos do sistema (lista curta, com aplicação):

1. **Entre na cabeça do cliente** — mapeie o que ele já sabe, teme e quer antes de escrever uma linha.
2. **Entre na oferta** — reformule o produto pelo benefício oculto mais forte, não pela característica óbvia. [aplicação: reescreva o benefício principal da oferta minerada pelo ângulo que o concorrente não usou]
3. **Admissão danosa** — reconheça um defeito real da oferta/nicho antes que o lead pense nisso; isso destrava a credibilidade do resto da carta.
4. **Garanta que a carta seja entregue/aberta** — trate envelope/assunto/thumbnail como parte da copy, não como embalagem.
5. **Prenda a atenção logo no topo** — headline e primeiras linhas decidem se o resto é lido.
6. **Use fórmulas de headline testadas** — "Quem mais quer ___?", "Como ___ me fez ___", "Você é ___?", "Como eu ___", "Como ___" (todas com exemplos no livro, p.43–44).
7. **Vença a objeção de preço** — empacote em partes (cada parte com valor individual somando mais que o preço total) ou oculte o preço fracionando em parcelas pequenas (p.55–56).
8. **Responda objeções abertamente** — liste as razões reais para não comprar e rebata cada uma com resposta direta + prova + reforço da garantia (p.101).
9. **Provoque ação imediata** — combine gatilhos reais: disponibilidade limitada, bônus por tempo, sorteio/concurso com prazo, e facilite ao máximo o ato de responder (telefone grátis, link direto) (p.103–110).
10. **Escreva um P.S. de peso** — o P.S. funciona como uma segunda headline para quem pula direto ao fim da carta; resuma oferta + urgência ali (p.111).

**Oferta irresistível:** empilhar partes com valor individual declarado até a soma superar visivelmente o preço pedido (exemplo do livro: pacote de seminários + kit de marketing + clube de conteúdo mensal somando "valor duro" declarado, vendido por fração disso).

**Garantia:** usada no livro como resposta-padrão dentro do bloco de objeções — sempre que o lead hesita, a carta reafirma a garantia/teste grátis como redutor de risco.

**P.S.:** nunca finalize uma carta sem P.S.; ele existe porque muita gente pula direto para o fim — cite a citação do próprio Kennedy: "The P.S. can make or break your letter!" (Kennedy, p.111).

**Urgência:** "Your letter's job is to get the reader to respond right now." (Kennedy, p.104) — os gatilhos citados no livro incluem disponibilidade limitada, prêmios/bônus, sorteios com prazo e facilidade de resposta (telefone 24h, formulário simples).

**Fonte:** Dan Kennedy, *The Ultimate Sales Letter* (2ª edição), Seção II "The System", passos 2, 6, 7, 12, 13 e 14 — páginas 21–22, 43–44, 55–56, 101, 103–110, 111.

## 4. Tabela-síntese — auditoria da oferta modelada

| Elemento | Pergunta de diagnóstico | Como intensificar sem mentir |
|---|---|---|
| Promessa | Qual variável da equação de valor ela ataca primeiro? | Deixe o resultado mais específico e mensurável, não mais exagerado |
| Mecanismo | O paradoxo/crença que ele resolve é real para o meu avatar? | Troque o "hype" de referência por um que o seu público reconheça mais |
| Stack | Cada item resolve uma objeção diferente ou está redundante? | Some valor individual declarado a cada item antes de mostrar o preço |
| Bônus | Existe um bônus específico para a maior objeção de compra? | Nomeie o bônus e ligue-o explicitamente à objeção que ele mata |
| Garantia | A garantia reforça a probabilidade percebida ou só existe por padrão? | Suba o nível (de condicional para incondicional) só se a entrega aguentar |
| Preço | O preço reflete o valor da equação ou o custo de produção? | Ancore com a soma do stack antes de revelar o preço final |
| Urgência | O prazo/estoque é real e verificável pelo lead? | Torne o motivo do prazo explícito (turma, lote, data) em vez de genérico |
| Nome | O nome é específico o bastante para vencer o leilão de atenção? | Adicione avatar + resultado + prazo + palavra-recipiente ao nome |
| CTA | O próximo passo está claro e sem fricção extra? | Reduza para uma única ação e reafirme a garantia ao lado do botão |

**Fonte:** síntese própria a partir das seções 1–3 acima.

## 5. Checklist — de oferta que já vende para versão modelada mais forte

1. Reescreva a promessa em uma frase que mira só uma das 4 variáveis da equação de valor, a mais fraca hoje.
2. Liste os problemas do avatar em ordem cronológica até o resultado — confirme que o stack cobre do primeiro ao último.
3. Escreva o mecanismo em três frases: problema, função, solução.
4. Teste se o mecanismo resolve uma pergunta paradoxal real do seu nicho (não inventada).
5. Troque o nome do mecanismo se ele for igual ao de um concorrente maior.
6. Corte um item do stack que custa caro para você e vale pouco para o lead; substitua por algo barato e de alto valor percebido.
7. Nomeie cada bônus pela objeção que ele resolve, não pelo conteúdo que ele contém.
8. Confirme que a soma declarada do stack aparece antes do preço final.
9. Escolha o tipo de garantia pela objeção mais forte do avatar, não por hábito do nicho.
10. Verifique se toda escassez/urgência declarada é 100% real e sustentável na operação.
11. Reescreva a headline testando ao menos duas fórmulas da lista de Kennedy.
12. Adicione um bloco de objeções respondidas (pergunta real + resposta + prova + garantia).
13. Escreva um P.S. que resuma oferta + urgência + prova em três linhas.
14. Confirme que o nome final da oferta carrega avatar, resultado, prazo e palavra-recipiente.
15. Releia o CTA e reduza para uma única ação possível.

**Fonte:** síntese própria a partir das seções 1–3 acima.


=====
### ARQUIVO: references/criacao-cards.md
=====

# Cards, matrizes e checklists de criação (literais do Notion Trip Angle)

## Resumo estratégico de uma página (Fase 1 do módulo 03)
Público específico · Situação observável · Desejo prioritário · Problema e impacto · Alternativas já tentadas · Por que não funcionaram · Objeção dominante · Linguagem recorrente · Prova disponível · Hipóteses ainda abertas. Checkpoint: você explica o problema com palavras do cliente e aponta as fontes.

## Pré-requisitos antes de abrir um documento de copy
[ ] mercado e recorte de público · [ ] situação observável · [ ] desejo expresso · [ ] problema prioritário e consequências · [ ] soluções já tentadas · [ ] alternativas e concorrentes · [ ] frases reais coletadas · [ ] objeções e riscos percebidos · [ ] provas disponíveis · [ ] limites legais, operacionais ou de promessa.

## Banco de voz do cliente
| Frase exata (sem reescrever) | Fonte | Situação (quando acontece) | Desejo | Objeção | Prova necessária |

## Estágios de consciência e entrada
| Estágio | O que a pessoa pensa | Objetivo da mensagem | Boa entrada |
|---|---|---|---|
| Não consciente | não nomeia o problema | tornar a situação reconhecível | cena, sintoma, contraste, pergunta concreta |
| Consciente do problema | sabe que algo está errado | organizar o problema e consequências | diagnóstico, causa, custo de manter |
| Consciente da solução | compara caminhos | diferenciar mecanismo e critérios | nova oportunidade, comparação, como funciona |
| Consciente do produto | conhece a oferta, tem dúvidas | reduzir risco, provar adequação | provas, objeções, escopo, garantia, demo |
| Muito consciente | perto de decidir | facilitar a ação | resumo, condições, urgência verdadeira, CTA |
Checkpoint: headline, lead e CTA começam no mesmo nível de consciência.

## Offer Card (módulo 03)
| Campo | Preenchimento |
|---|---|
| Público + situação | quem enfrenta qual momento específico |
| Transformação | do estado atual ao desejado |
| Mecanismo da solução | princípio e sequência que tornam a mudança plausível |
| Entregáveis | o que entra, formato, duração, suporte, acesso |
| Prova | evidências verificáveis e relevantes para o claim |
| Objeções | confiança, valor, tempo, esforço, prioridade, autoridade, risco |
| Preço e condições | valor, parcelas, renovação, custos adicionais, regras |
| Garantia e limites | o que é coberto, prazo, procedimento, exclusões |
| CTA | uma próxima ação objetiva |
Checkpoint: a oferta é entendida sem adjetivos vagos; mecanismo plausível; escopo e limites visíveis; cada claim importante tem prova.

## Estrutura da oferta (Fase 4)
Produto central · Transformação principal · Mecanismo · Entregáveis · Forma de acesso · Onboarding · Prazo e cadência · Suporte · Critérios de sucesso do cliente · Bônus funcionais · Preço e condições · Garantia/redução de risco · Escassez/urgência real · Provas · Limitações e responsabilidades.

## Matriz de prova
| Tipo de prova | O que sustenta | Limite |
|---|---|---|
| Demonstração | funcionamento do processo/produto | não garante o resultado final |
| Dados do produto | uso, conclusão, velocidade, comportamento | precisa de fonte e contexto |
| Caso de cliente | resultado em contexto específico | não representa resultado típico |
| Depoimento | experiência declarada | confirmar autorização e veracidade |
| Especialista/estudo | princípio geral | não prova que seu produto entrega |
| Prova inexistente | nada | bloqueia claim forte; transforme em hipótese |

## Revisão de claims antes de publicar
[ ] resultado anunciado dentro do que o produto entrega · [ ] evidência arquivada para números e declarações · [ ] exceção não tratada como típica · [ ] depoimentos com autorização e contexto · [ ] limitações não omitidas · [ ] garantia, preço, prazo e escassez verdadeiros · [ ] regras do canal, país e categoria · [ ] claims sensíveis (saúde, emagrecimento, dinheiro, segurança, garantia de retorno, comparação absoluta) revisados. CDC arts. 36–38; CONAR; Padrões de Publicidade da Meta.

## Matriz de mensagem
| Elemento | Pergunta | Saída |
|---|---|---|
| Situação | que momento faz a mensagem ser relevante? | cena ou contexto reconhecível |
| Problema | o que impede o progresso? | diagnóstico específico |
| Desejo | que progresso a pessoa procura? | resultado em linguagem real |
| Mecanismo | por que persiste e como a solução muda isso? | explicação simples e diferenciada |
| Promessa | qual mudança responsável propomos? | benefício com condição e escopo |
| Prova | o que reduz a incerteza? | prova conectada ao claim |
| Objeção | o que impede o próximo passo? | resposta, pergunta e evidência |
| CTA | qual é a menor decisão útil agora? | ação única e clara |

## Checklist de uma boa frase
[ ] compreendida na primeira leitura · [ ] verbo e imagem concreta · [ ] benefício relevante, não só função · [ ] sem superlativo sem prova · [ ] voz do público sem caricatura · [ ] leva à próxima frase · [ ] não promete além do que a entrega sustenta.

## Escolha do ativo de venda
| Use quando | Formato | Cuidado |
|---|---|---|
| oferta simples, familiar, baixo risco | página curta | não omitir informação essencial |
| oferta nova, cara, complexa, muitas objeções | página longa | cada seção reduz uma dúvida |
| mecanismo precisa de narrativa/demonstração/sequência | VSL | legenda, controles, resumo escrito |
| segmentar ou personalizar recomendação | quiz/diagnóstico | nenhuma pergunta sem efeito na saída |
| diagnóstico, configuração, confiança | WhatsApp ou ligação | qualificar fit, documentar próximo passo, sem pressão |
| prova depende de ver o produto | demo ou aplicação | critérios de entrada e decisão |

## Estrutura modular de página ou VSL (use só os blocos necessários)
1 Entrada (headline, subheadline, contexto) · 2 Reconhecimento (situação, sintomas, custo) · 3 Diagnóstico (mecanismo do problema) · 4 Nova oportunidade (mecanismo da solução) · 5 Transformação (promessa e para quem) · 6 Como funciona (processo/demonstração) · 7 Prova · 8 Oferta (entregáveis, suporte, limites) · 9 Valor e condições · 10 Risco (garantia, privacidade, política) · 11 Objeções (FAQ priorizada) · 12 Ação (CTA e o que acontece depois).

## QA do ativo
[ ] título e anúncio falam da mesma promessa · [ ] um CTA principal · [ ] oferta e preço claros · [ ] prova próxima do claim · [ ] botão explica a ação · [ ] formulário pede só o necessário · [ ] funciona no celular · [ ] vídeo com legenda e controle · [ ] carregamento e links testados · [ ] política, termos, contato e reembolso acessíveis · [ ] pós-clique e pós-compra definidos. Checkpoint: alguém entende "para quem é, o que recebe, por que acreditar, quanto custa e o que acontece depois" sem falar com você.

## Escolha do funil
| Condição | Rota provável |
|---|---|
| produto simples, compra autônoma | anúncio/conteúdo → página → checkout → onboarding |
| necessidade de educação | conteúdo/anúncio → VSL/página → checkout ou conversa |
| necessidade de segmentação | quiz → recomendação → página/conversa |
| ticket ou risco alto | conteúdo/anúncio → aplicação → descoberta → proposta → onboarding |
| serviço configurável | entrada → diagnóstico → escopo → proposta → kickoff |
Atritos de checkout: [ ] custo total antes da confirmação · [ ] meios de pagamento · [ ] política e suporte visíveis · [ ] poucos campos · [ ] erros orientam correção · [ ] confirmação e próximos passos imediatos · [ ] evento de conversão validado.

## Roteiro de descoberta (venda consultiva)
1 Contrato da conversa · 2 Contexto · 3 Estado atual · 4 Problema · 5 Impacto · 6 Tentativas · 7 Estado desejado · 8 Decisão · 9 Fit · 10 Próximo passo (decisão, tarefa, responsável, data). Perguntas: "O que mudou para isso virar prioridade agora?", "Pode me mostrar como você faz hoje?", "Onde o processo trava?", "Quem mais sente o impacto?", "O que já tentaram?", "Que resultado faria valer a pena?", "Quais critérios para decidir?", "Existe condição que impediria?", "Qual próximo passo faz sentido para os dois?".

## Método CALMA e matriz de objeções
C Calar e ouvir · A Acolher · L Localizar a raiz · M Mostrar evidência · A Acordar o próximo passo.
| Objeção | Raízes possíveis | Pergunta de diagnóstico | Resposta responsável |
|---|---|---|---|
| "Está caro." | valor não entendido, orçamento, prioridade, risco | "Comparado a qual alternativa ou resultado?" | revisar escopo, impacto, prova e condição; não inventar desconto |
| "Não tenho tempo." | esforço, prioridade, momento | "Qual parte parece exigir mais tempo?" | explicar participação real, simplificar ou admitir falta de fit |
| "Preciso pensar." | dúvida não dita, outra pessoa, comparação, baixa urgência | "Que ponto você precisa esclarecer para decidir?" | informação e prazo natural; evitar perseguição |
| "Já tentei algo parecido." | desconfiança, experiência ruim | "O que foi tentado e onde falhou?" | diferenciar mecanismo e limites com prova |
| "Preciso falar com alguém." | autoridade compartilhada | "Quem participa e quais critérios usa?" | preparar resumo, incluir decisores |
| "Agora não." | prioridade, orçamento, capacidade, ausência de dor | "O que precisaria mudar para reavaliar?" | acordar condição/data real ou encerrar |

## Follow-up (três mensagens)
1 Recapitulação: "Pelo que entendi, hoje [situação], isso gera [impacto] e a prioridade é [objetivo]. Combinamos [próximo passo] até [data]. Aqui está [material]. Se algo estiver incorreto, me avise." · 2 Evidência relevante: "Você comentou [objeção]. Separei [demonstração/caso/dado] porque mostra [ponto]. Isso responde ou falta contexto?" · 3 Fechamento do ciclo: "Não quero insistir sem contexto. Faz sentido [próximo passo], prefere retomar em [condição/data] ou encerro por agora?" Registro mínimo: data e canal, etapa, necessidade e impacto, objeção aberta, material enviado, decisão e responsável, próxima ação e data, motivo de perda ou pausa.

## Card Final da Oferta
Nome · Versão e data · Mercado · Segmento · Situação de compra · Desejo · Problema · Crença dominante · Mecanismo do problema · Mecanismo da solução · Nova oportunidade · Big Idea · Ângulo principal · Promessa · Produto · Entregáveis · Bônus funcionais · Preço e condições · Garantia/redução de risco · Provas · Claims pendentes de revisão · Funil escolhido · Métrica principal · Primeiro Test Card · O que permanece como hipótese.

## Rubrica de prontidão (0–2 cada, máx. 20)
Criação: demanda e problema · clareza do segmento · situação observável · força lógica do mecanismo · especificidade da promessa · coerência promessa/produto · prova disponível · economia mínima · segurança dos claims · qualidade do Test Card. 15 = pode seguir para teste pequeno; zero em evidência, entrega, claims ou tracking bloqueia.
Engenharia (módulo 03): público e situação · problema e desejo com evidência · consciência definida · mecanismo plausível · promessa responsável · prova próxima dos claims · escopo/preço/risco/limites · ativo e funil sem lacunas · objeções e follow-up · teste com critério. 17–20 pronto para teste controlado; 12–16 corrigir; 0–11 voltar à pesquisa.

## Briefing de passagem
Para 04 — Criativos: público e situação · estágio de consciência · hipótese de ângulo · hook e promessa · mecanismo · prova disponível · objeção prioritária · CTA · formato e canal · claims proibidos ou que exigem revisão.
Para 05 — Tráfego: objetivo e evento · público/segmento · ativo e URL · hipótese · variável · orçamento e janela · métrica principal · guardrails · critério de pausa · decisão pós-teste.


=====
### ARQUIVO: references/criacao-de-oferta-do-zero.md
=====

# Criação de oferta do zero (origem: skill agente-de-copy-trm (criacao-de-oferta-do-zero.md), consolidada em 13/09/2026)

# Como criar uma oferta do zero (Modo 04 — Criar) e engenharia de copy e vendas

A oferta não nasce do volume de criativos. Nasce de evidência sobre uma situação, um desejo, um problema e uma razão crível para acreditar na solução. Mapa completo: Mercado → Persona → Situação → Desejo → Problema → Crença → Mecanismo do problema → Mecanismo da solução → Nova oportunidade → Big Idea → Ângulo → Promessa → Produto → Oferta → Hook → Formatos → Ads → VSL/Página/Quiz → Funil → Test Card → Dados → Decisão. Cada etapa produz uma decisão documentada ou permanece HIPÓTESE. Tempo: dois a quatro blocos de trabalho; não conclua tudo em uma sessão. Templates e checklists em `criacao-cards.md`.

| Função | Elemento | Erro comum |
|---|---|---|
| O que é entregue | Produto | confundir lista de aulas/recursos com valor |
| Produto + promessa + mecanismo + prova + preço + redução de risco + condições | Oferta | só bônus e desconto |
| Como a oportunidade é apresentada | Mensagem | começar pelos hooks sem tese |
| Caminho entre atenção, entendimento, decisão e compra | Funil | escolher quiz ou VSL por moda |
| Experimento que reduz uma incerteza | Teste | mudar tudo e chamar de aprendizado |

## Fase 0 — Recorte
Um mercado, um segmento, uma situação de compra, um resultado principal, um projeto para testar. Briefing de partida: mercado, segmento, quem decide, situação que dispara a busca, alternativa usada hoje, resultado desejado, problema percebido, hipótese inicial de solução, orçamento e prazo do teste, métrica de avanço real. Se o briefing fala com "todo mundo", volte.

## Fase 1 — Evidência de mercado e voz do cliente
Nota de oportunidade 0–2 em: problema/desejo, demanda, capacidade de pagamento, acesso ao público, alternativas existentes, possibilidade de entrega. Ausência de concorrência não prova oportunidade; concorrência prova atividade, não lucro de uma oferta específica. Dossiê com pelo menos três tipos de fonte (primária: entrevistas, calls, suporte; comportamento observável: compras, buscas, anúncios, checkouts; voz pública: comentários, reviews, fóruns; fonte técnica; copy concorrente só para mapear alegações e linguagem). Linha de partida: cinco conversas e trinta trechos de linguagem. Entrevista de descoberta: quando o problema aconteceu pela última vez, o que estava acontecendo, o que tentou, quanto custou, qual alternativa, o que frustrou, o que fez procurar, o que teme perder, que resultado justificaria agir, quem influencia, o que faria desconfiar, que palavras usa. Nunca "você compraria?". Banco de voz do cliente: frase exata, fonte, situação, desejo, objeção, prova necessária. Uma fala é sinal; repetição é padrão; padrão testado é aprendizado. Checkpoint: você descreve a situação com palavras do mercado, e aponta as fontes.

## Fase 2 — Tese da oferta
Situação (o que acontece antes de procurar ajuda) · Desejo · Problema percebido · Problema estratégico (gargalo que você vê nas evidências) · Crença dominante · Alternativa atual · Objeções. Dor observável, não adjetivo ("recebe leads, demora horas e perde o agendamento", não "está frustrado"). Mecanismo do problema: "A pessoa tenta [alternativa], mas continua com [problema] porque [causa]. Enquanto [condição] permanecer, o resultado tende a [consequência]." Mecanismo da solução: "A solução atua em [causa] por meio de [processo], permitindo [resultado intermediário observável] antes de buscar [resultado final]." Nova oportunidade: o que a pessoa passa a fazer, deixa de fazer, por que agora, que crença muda, que evidência permite. Controle de certeza: observado / inferido / hipótese / alegação / comprovado para esta oferta. Estágio de consciência do público e ponte em quatro frases (você está aqui → isso acontece porque → existe outro caminho → o próximo passo é).

## Fase 3 — Big Idea, ângulo e promessa
Big Idea: compreendida em uma frase, importante para esta persona, muda a interpretação do problema/solução, sustenta anúncios, página e produto, diferente sem afirmação falsa. Três hipóteses de ângulo entre: problema (custo de continuar), resultado, mecanismo/nova oportunidade, prova/demonstração, situação/persona, contraste. Não misture ângulos no mesmo criativo na fase de aprendizado. Promessa: "Para [segmento em situação], alcançar [resultado observável] por meio de [mecanismo], reduzindo [obstáculo], dentro de [condição defensável]" — específica, desejável, compreensível, compatível com o produto, plausível, proporcional à prova, segura para canal e lei. Força vem de aumentar resultado percebido e confiança e reduzir demora, esforço e risco, não de exagerar. Entregável: uma Big Idea, três ângulos, uma promessa com duas variações.

## Fase 4 — Produto e arquitetura da oferta
Desenhe o produto a partir dos obstáculos: obstáculo → resultado intermediário → prova de conclusão → formato → componente. Camadas possíveis: diagnóstico e plano, método central, ferramentas/templates, implementação guiada, suporte, acompanhamento, comunidade, medição. Bônus que não remove obstáculo, acelera ou reduz risco só aumenta volume. As sete perguntas: para quem, qual mudança, como acontece, o que recebe, por que acreditar, qual esforço/risco permanece, por que agora (motivo verdadeiro, nunca escassez inventada). Economia mínima: receita líquida, taxas/impostos, custo de entrega, variável, reembolso, comissão, margem de contribuição (= receita líquida − taxas − custos variáveis − provisão de reembolso), CPA máximo teórico, caixa, capacidade. Garantia reduz risco que a operação suporta; escassez e urgência só verdadeiras. Matriz de prova (hierarquia: demonstração > dados próprios > caso verificável > depoimento autorizado > credencial > explicação plausível > opinião; prova inexistente bloqueia claim forte → hipótese). Revisão de claims antes de publicar (checklist em `criacao-cards.md`). Entregável: Offer Card com produto, preço, prova, garantia e condições fechados.

## Fase 5 — Mensagem, ativo e funil
Matriz de mensagem: situação → problema → desejo → mecanismo → promessa → prova → objeção → CTA (público × consciência × dor × promessa × prova × CTA). Ordem para escrever: ação desejada → promessa principal → provas → objeções por prioridade → estrutura antes das frases → variações de headline/lead/CTA → edição por clareza e continuidade → revisão factual, jurídica, visual e mobile. Hook interrompe com relevância; headline comunica situação/benefício/nova oportunidade; lead confirma para quem é e abre a explicação; corpo traz mecanismo, prova, oferta e objeções; CTA diz o que fazer e o que acontece depois. Pacote inicial: 3 ângulos × 3 hooks = 9 combinações documentadas. Escolha do formato pela necessidade (página curta: simples/baixo risco; página longa: nova/cara/complexa; VSL: mecanismo pede narrativa; quiz: segmentar/personalizar, sem pergunta sem efeito; WhatsApp/ligação: diagnóstico e confiança; demo: prova depende de ver). Estrutura modular de página/VSL em 12 blocos e QA do ativo em `criacao-cards.md`. Funil: origem → mensagem → ativo → decisão → pagamento → confirmação → onboarding → entrega → aprendizado; perguntas de passagem por seta; atritos de checkout. Coerência de ponta a ponta: anúncio e página na mesma situação; hook no mesmo ângulo; promessa sustentada pelo mecanismo; produto entrega a promessa; preço e garantia claros; checkout não muda condições; tracking acompanha a ação.

## Fase 6 — Validação e Test Card
Escada de evidência 0–6 (opinião → clique → lead → início de checkout → pagamento → uso → recompra). Uma variável por vez. Test Card completo (ver `../../agente-central-trm/references/vocabulario/test-card.md`). Métricas por camada. Entregável: Test Card registrado antes do lançamento e preenchido após a janela.

## Fase 7 — Venda consultiva (quando houver conversa)
Roteiro de descoberta em 10 passos, método CALMA para objeções (Calar e ouvir · Acolher · Localizar a raiz · Mostrar evidência · Acordar próximo passo), matriz de objeções ("está caro", "não tenho tempo", "preciso pensar", "já tentei", "preciso falar com alguém", "agora não"), follow-up em três mensagens com motivo, valor, CTA e saída. Detalhes em `criacao-cards.md`.

## Saídas obrigatórias
Card Final da Oferta · Rubrica de prontidão 0–20 (15 permite teste pequeno; zero em evidência, entrega, claims ou tracking bloqueia) · Briefing para 04 — Criativos (público e situação, consciência, hipótese de ângulo, hook e promessa, mecanismo, prova, objeção prioritária, CTA, formato e canal, claims proibidos) · Briefing para 05 — Tráfego (objetivo e evento, público, ativo e URL, hipótese, variável, orçamento e janela, métrica principal, guardrails, critério de pausa, decisão pós-teste). Próximos passos: comparar com a Matriz Mestre, consultar modelagem sem cópia, registrar em 14 — Test Cards, revisar em 12 — Claims e Risco.

## Erros que mais enfraquecem uma oferta
Criar produto antes de entender a situação de compra; misturar personas; tratar anúncio concorrente como prova de faturamento; nome bonito chamado de mecanismo; promessa que o produto não sustenta; bônus sem obstáculo; desconto/escassez/urgência fictícia; depoimento sem contexto ou autorização; copiar identidade e claims; várias variáveis no mesmo teste; sucesso só por CTR; ignorar margem, reembolso e capacidade; mais criativos para fugir de oferta mal resolvida; uma venda como prova de escala; encerrar teste sem aprendizado.


=====
### ARQUIVO: references/entregaveis-copy.md
=====

# Entregáveis de copy

Escreva cada peça depois do card da oferta modelada. Use moldes de headline e padrões de lead das bases de inteligência. Não copie frases da referência.

## 1. Roteiro de VSL (padrão, ajustável)
| # | Bloco | Função | Duração sugerida |
|---|---|---|---|
| 1 | Hook | Parar e selecionar a persona pela situação ou pela promessa | 0–30 s |
| 2 | Lead | Promessa ou lacuna central, conforme o tipo de lead | 30 s–2 min |
| 3 | Qualificação | Para quem é e para quem não é | curto |
| 4 | História ou descoberta | Tornar o mecanismo crível e humano | 2–5 min |
| 5 | Mecanismo do problema | Por que tudo o que a pessoa tentou falhou, sem culpá-la | 2–4 min |
| 6 | Mecanismo da solução | Como a nova abordagem resolve a causa | 2–4 min |
| 7 | Prova | Demonstração, dados próprios, casos autorizados | 1–3 min |
| 8 | Produto | O que é e como funciona na prática | 1–2 min |
| 9 | Stack | Entregáveis e bônus, cada um ligado a um obstáculo | 1–2 min |
| 10 | Preço e ancoragem | Comparação honesta com alternativas e custo de não agir | 1 min |
| 11 | Garantia | Remove o risco da decisão | 30 s |
| 12 | Urgência | Motivo real para agir agora | 30 s |
| 13 | CTA | Ação única e o que acontece depois | 30 s |
| 14 | FAQ e objeções | Últimas travas | 1–3 min |
Durações são ponto de partida. Formato do roteiro: bloco · fala · texto na tela · visual · função.

## 2. Carta ou página de vendas em blocos
Headline · subheadline · lead · identificação do problema · agitação com custo de continuar · mecanismo · apresentação do produto · benefícios em bullets · prova · stack · preço e ancoragem · garantia · urgência · CTA · FAQ · P.S. Cada bullet: benefício específico, curiosidade ou prova, nunca uma característica solta.

## 3. Leads alternativos
Três leads do mesmo produto em tipos diferentes adequados à consciência (por exemplo promessa, segredo, história). Cada um com 150 a 300 palavras e a indicação do nível de consciência para o qual foi escrito.

## 4. Banco de headlines e hooks
| Texto | Molde de origem | Desejo acionado | Consciência | Ângulo | Formato sugerido para anúncio |
Mínimo de 30, com pelo menos cinco ângulos diferentes.

## 5. Roteiros de anúncio curtos (para o AGENTE DE ADS TRM)
| Tempo | Fala | Texto na tela | Visual | Função |
Estrutura: hook 0–3 s · situação ou problema · mecanismo ou virada · prova · promessa e CTA. Um ângulo por roteiro. Mínimo de 5 roteiros.

## 6. FAQ de objeções
| Objeção | Resposta | Prova ou garantia que sustenta |

## 7. Tabela de claims (obrigatória)
| Claim | Onde aparece | Prova própria | Sensível? | Risco | Versão segura se faltar prova |

## 8. Hipóteses de teste
| Variável (promessa, mecanismo, lead, stack, preço, garantia) | Controle | Variante | Métrica principal | Critério de decisão |
Uma variável por teste.


=====
### ARQUIVO: references/leitura-de-oferta.md
=====

# Leitura de oferta do zero (origem: skill agente-de-copy-trm (leitura-de-oferta.md), consolidada em 13/09/2026)

# Como ler uma oferta do zero (Modo 02 — Analisar)

Leitura de oferta é engenharia reversa, não opinião. O objetivo é reconstruir o sistema que conecta uma pessoa em uma situação, uma explicação do problema, uma oportunidade, uma promessa, uma prova, um produto, condições comerciais e um caminho de compra. Você procura relações, funções, limites e hipóteses, não frases para copiar. O entregável é uma Ficha de Leitura que outra pessoa consiga auditar voltando da interpretação até o trecho original.

Entradas obrigatórias: peça original (anúncio, página, quiz, VSL, checkout), URL, anunciante, país e data da captura, transcrição e capturas. Saídas: Ficha de Fonte e Linhagem · Mapa Estratégico · Matriz Claim → Prova → Limite · Mapa de Ads, VSL, Oferta e Funil · DNA, princípio transferível e próxima hipótese. Templates em `leitura-fichas.md`.

## Leitura rápida em dois minutos (antes de tudo)
O que é vendido? Quem é chamado? Que situação abre a conversa? Que problema e desejo aparecem? Que resultado é prometido? Que mecanismo é apresentado? Que prova? Que ação? Para onde o anúncio leva? Resumo de uma linha: "Para [pessoa em situação], a oferta apresenta [produto] como meio de alcançar [progresso], porque [mecanismo], sustentado por [prova observada], mediante [condições]." Se não dá para preencher sem inventar, a captura está incompleta.

## As cinco passagens (uma camada por vez, nunca tudo na primeira visualização)

**1 — Fonte.** Consuma a peça inteira sem pausar; na segunda vez transcreva e marque blocos; capture os pontos decisivos; desenhe a sequência sem nomear frameworks; registre lacunas como NÃO MAPEADO. Entrega: linhagem, transcrição, lacunas.

**2 — Demanda.** Persona situada (circunstância, comportamento, tensão, evento de mudança; o que tentou; o que empurra e o que atrai; que ansiedade impede; que hábito mantém; comprador = usuário?). Separe situação / problema / dor / desejo / crença / solução tentada. Classifique o estágio de consciência que a peça pressupõe (inconsciente → problema → solução → produto → mais consciente) como leitura da comunicação.

**3 — Tese.** Mecanismo do problema: "A copy afirma que o problema persiste não apenas por [explicação comum], mas porque [causa proposta]." Mecanismo da solução: "A solução produziria progresso porque [processo] atua sobre [causa] por meio de [entrega]." Separe mecanismo, método, produto e nome proprietário: se retirar o nome elegante e não restar lógica, é só skin. Nova oportunidade: "Talvez o caminho não seja [velha solução], mas [nova categoria/abordagem]." Big Idea: resuma a tese sem headline, nome, personagem ou bordão; se o resumo desaparece, você capturou superfície. Depois ângulo, promessa, hook (que pergunta o próximo bloco responde?) e lead (que crença é trabalhada?).

**4 — Persuasão.** Engenharia do anúncio por função: interrupção → seleção → tensão → reframe → prova → ponte → CTA (registre também imagem, ritmo, personagem, áudio, legenda, placement, duração, destino). Formato não é argumento. Progressão da VSL/página em blocos (situação, agitação, explicação antiga, mecanismo do problema, nova oportunidade, mecanismo da solução, promessa, prova, produto, objeções, condições/risco/CTA); para cada bloco: que crença estabelece e por que o próximo se torna necessário. Matriz Claim → Prova → Limite, incluindo claims implícitos.

**5 — Negócio.** Produto ≠ transformação ≠ oferta ≠ copy ≠ funil. Registre só o que aparece: produto principal, entregáveis, bônus e função de cada um, preço/parcelas/total, ancoragem, garantia e condições, urgência/escassez, CTA, bump/upsell/downsell, suporte, reembolso. Um bônus só fortalece a oferta quando remove obstáculo, reduz tempo/esforço, aumenta confiança ou amplia etapa coerente. Funil: para cada transição (anúncio → quiz/página/VSL → checkout → pós-compra) a ação solicitada, a expectativa criada e o dado necessário. Teste de congruência: anúncio, destino, checkout e produto sustentam a mesma promessa e condições.

## DNA e princípio transferível
Remova nome e marca, headline e frases, personagem e história, autoridade e depoimentos, números/preço/garantia, mecanismo proprietário e visual. O que permanece é a função (reduzir culpa, tornar problema visível, demonstrar antes de afirmar, simplificar decisão, aumentar confiança, diminuir esforço percebido). Pode inspirar hipótese: função psicológica e ordem dos argumentos, tipo de demonstração, relação problema-mecanismo-solução, pergunta de teste, função de uma etapa do funil. Não deve ser copiado: frases, scripts, nomes, bordões, prova de terceiros, claim sem base, identidade, preço/escassez/garantia não verdadeiros. Feche com uma hipótese própria e uma variável para Test Card.

## Roteiro operacional (A–E)
A Fonte e contexto · B Demanda · C Tese · D Persuasão · E Oferta e extração — lista completa em `leitura-fichas.md`. Cadeia: ORIGINAL → OBSERVAÇÃO → INTERPRETAÇÃO → DNA → PRINCÍPIO → HIPÓTESE → TEST CARD → RESULTADO.

## Rubrica de qualidade (0 ausente, 1 parcial, 2 completo)
Fonte e linhagem · Persona e situação · Problema, dor, desejo, crenças · Mecanismos · Big Idea, ângulo, promessa · Hook, lead, formato, progressão · Prova, objeções, claims, limites · Produto, oferta, condições · Funil e congruência · DNA, princípio, hipótese. Pronto para modelar: 16/20 sem zero em Fonte, Claims, Produto/Oferta ou Princípio.

## Erros que invalidam a leitura
Começar pelo hook e ignorar a situação de compra; confundir anúncio ativo com oferta lucrativa; preencher lacunas com estruturas de livros; chamar nome proprietário de mecanismo; confundir Big Idea, ângulo, promessa e headline; tratar depoimento como prova universal; ignorar claims implícitos; confundir produto, oferta, copy, VSL e funil; copiar frase, personagem, prova, preço, escassez ou identidade; modelar antes de concluir a observação; mudar várias dimensões na hipótese; não registrar versão, fonte e data.

## Formato de entrega
Ficha de Leitura em tabelas (Elemento | Leitura auditada | Rótulo de evidência | Trecho/fonte), seguida de Equação estratégica, Progressão de crença em 7 passos, Claim → Prova → Limite, Mapa do funil, DNA/princípio/não transferível, hipótese e variável de Test Card, lacunas e riscos. Indique a base técnica de destino de cada registro.


=====
### ARQUIVO: references/leitura-fichas.md
=====

# Fichas e templates de leitura (literais do Notion Trip Angle)

## 1. Ficha de Fonte e Linhagem
- Código interno da oferta (`PE-Oxx`, `EM-Oxx`…) e versão da análise
- URL do anúncio · URL final · Anunciante/Página · Domínio · País · Idioma
- Data da primeira captura · Data da revisão
- Formato · Texto · Headline · Criativo · CTA
- Transcrição integral (vídeo/áudio) · Ordem dos blocos da página/VSL/quiz
- Produto, entregáveis, preço, parcelas, garantia, condições (quando observados)
- Checkout, bump, upsell, downsell, pós-compra (quando observados)
- Evidências ausentes · Links quebrados
- Status de linhagem: Confirmada / Parcial controlada / Mesclada (materiais de ofertas diferentes misturados → separar antes de analisar)

## 2. Mapa Estratégico da Oferta (DNA — 19 linhas)
| Elemento | Leitura auditada | Rótulo |
|---|---|---|
| Persona | quem é chamado | |
| Situação | circunstância apresentada pela copy; população externa não mapeada | |
| Desejo | funcional / emocional / social / identitário / espiritual quando aplicável | |
| Dor / problema visível | | |
| Crença pressuposta | "a explicação convencional ou o esforço anterior não explica o resultado" | |
| Inimigo narrativo | somente quando aparece no material | |
| Mecanismo do problema | — alegação da copy | |
| Mecanismo da solução | — apresentação da copy, não fato | |
| Mecanismo único de marketing | "Não confirmado; diferenciação percebida: …" | |
| Big Idea | tese central + CONFIRMADA/PROVÁVEL/NÃO CONFIRMADA | |
| Ângulo | enquadramento escolhido | |
| Promessa | resultado associado — alegação | |
| Hook dominante | função, tipo, próximo bloco | |
| Formato dominante | recipiente; formato ≠ argumento | |
| Prova | depoimento/autoridade/demonstração/história — prova alegada | |
| Produto | o que está documentado; não confundir com arquitetura total | |
| Oferta | produto + condições + componentes + CTA quando observados | |
| Funil | Ad → … ; VSL é roteiro, funil é sequência | |
| CTA | conforme o original; não criar CTA novo | |

## 3. Equação estratégica
Persona (…) + Situação (circunstância apresentada) + Desejo (…) + Problema (…) + Nova causa (…) + Mecanismo (…) + Nova solução (produto/método documentado) + Promessa (…, alegação) + Prova (evidência apresentada) + Oferta (produto, condições e CTA observados) = proposta de venda da copy. "Ferramenta de leitura; não significa que a nova causa seja verdadeira ou que o mecanismo funcione."

## 4. Progressão de crença (7 passos)
1. Crença inicial: a pessoa reconhece dor, estagnação ou curiosidade.
2. Tensão: a explicação anterior parece insuficiente.
3. Nova causa: a copy introduz <mecanismo do problema>.
4. Mecanismo: a copy apresenta <mecanismo da solução>.
5. Aceitação da solução: o produto passa a parecer o próximo passo.
6. Redução de risco/prova: demonstração, autoridade, depoimento, stack, garantia ou urgência, quando observados.
7. Ação: CTA original, sem etapa não mapeada.
"A progressão é uma interpretação estratégica. Ela não mede persuasão real."

## 5. Ângulo em 11 dimensões
Tese · situação · desejo · inimigo · emoção · contraste · reframe · mecanismo · persona · consciência · a própria tese como enquadramento.

## 6. Matriz Claim → Prova → Limite
| Claim (literal) | Tipo (resultado, mecanismo, velocidade, autoridade, escassez, saúde, financeiro) | Prova apresentada | O que a prova sustenta | Limite / risco | Evidência real disponível | Reformulação segura |

## 7. Mapa do Funil
| Etapa | Ação solicitada | Expectativa criada | Dado necessário | Observado? |
|---|---|---|---|---|
| Anúncio | clicar / assistir | por que prestar atenção | impressão, retenção, clique | |
| Quiz / página / VSL | avançar / comprar | por que a tese e a oferta fazem sentido | visita, avanço, lead | |
| Checkout | pagar | quais condições serão contratadas | início, abandono, compra | |
| Pós-compra | ativar / consumir | como começar e receber valor | entrega, ativação, uso | |
Teste de congruência: mudança inesperada de preço, público, mecanismo ou resultado rompe a continuidade. Para cada seta: o que a pessoa acabou de ver, o que espera, que dúvida precisa resolver, qual a única ação, que dado registrar, o que acontece se não avançar.

## 8. Ficha Final de Leitura (DNA, princípio, hipótese)
| Elemento | Leitura auditada |
|---|---|
| Persona / situação | |
| Problema apresentado | explicação da copy, não verdade universal |
| Desejo | |
| Mecanismo da solução | |
| Big Idea | |
| Ângulo | |
| Hook | |
| Prova observada | e o que não prova |
| Produto | |
| Oferta / funil | condições ausentes permanecem não mapeadas |
| Princípio transferível | função → função → função |
| Não transferível | nome, promessa, tradição, currículo, autores, frases, provas, CTA |
| Hipótese | "testar X contra Y, medindo Z" |
"O exemplo confirma a tese comunicada, não a eficácia ou performance comercial."

## 9. Roteiro operacional completo
A — Fonte e contexto: identifique a fonte primária e preserve o original; registre anunciante, domínio, país, idioma, data e versão; transcreva Ads, VSL, página, quiz e checkout; diferencie presença publicitária de performance.
B — Demanda: identifique o produto sem usar a promessa como descrição; quem é chamado; situação e evento de mudança; separe problema, dor, desejo e crenças; soluções tentadas; estágio de consciência.
C — Tese: mecanismo do problema; mecanismo da solução; separe mecanismo, método, produto e skin; nova oportunidade; Big Idea; ângulo e promessa.
D — Persuasão: separe Hook de Lead; formato, canal e placement; desmonte o anúncio por função; progressão da VSL/página; provas, objeções e claims; limite de cada prova.
E — Oferta e extração: separe produto de oferta; stack, preço, garantia, CTA e condições; funil e transições; DNA; princípio funcional vs superfície proprietária; transferível vs não; nova hipótese com identidade, produto e prova próprios; uma variável no Test Card.

## 10. "Faça você primeiro" (seis perguntas antes do gabarito)
1. Persona e situação: quem é chamado e em qual circunstância concreta?
2. Dor e desejo: qual tensão é apresentada e quais dimensões de desejo estão documentadas?
3. Hook, Lead e Ângulo: qual é a entrada, como ela é desenvolvida e qual enquadramento aparece?
4. Mecanismo e prova: qual causa e solução a copy apresenta e qual limite tem a prova?
5. Produto, oferta e funil: o que é entregue, quais condições aparecem e quais etapas são observáveis?
6. Modelagem e teste: qual função pode ser transferida sem copiar superfície, claims ou identidade? Proponha uma variável.

## 11. Comparação transversal (quando houver duas ou mais ofertas)
Passa quando aponta: (1) função comum; (2) tese específica de cada uma; (3) skin/identidade que não se copia; (4) classificação da Big Idea; (5) limite de evidência; (6) uma variável de Test Card. Classificação entre ofertas: clone só com coincidência simultânea de produto, mecanismo e entrega; senão VARIANTE / EXPANSÃO / NOVA FAMÍLIA. Vocabulário semelhante não prova mecanismo igual. Não importar inteligência de um nicho para outro.


=====
### ARQUIVO: references/mapa-da-oferta.md
=====

# Mapa da oferta de referência

Preencha a partir do que foi visto. Cada linha leva rótulo. Campo sem fonte: NÃO MAPEADO.

## 1. Fonte
Nome da oferta · anunciante · país · idioma · moeda · URLs (anúncio, quiz, VSL, página, checkout) · data da captura · sinais de escala (contagem, IDs, início, repetição) · plataforma de checkout · o que não foi acessado.

## 2. Personas
| Persona | Situação observável | Gatilho que dispara a compra | Linguagem literal usada | Nível de consciência | Evidência |
Uma linha por persona chamada no anúncio, no quiz ou na VSL. Não crie persona que a copy não chama.

## 3. Dores, desejos e crenças
| Dor (na voz do público) | Desejo correspondente | Desejo primário acionado | Crença atual | Crença que a copy instala | Onde aparece |

## 4. Promessa e benefícios
- Promessa principal, literal, com prazo, condição e resultado.
- Promessas secundárias.
- Benefícios em três camadas:
| Característica ou entregável | Benefício funcional | Benefício emocional ou identitário |

## 5. Mecanismo e Big Idea
- Mecanismo do problema: a causa que a copy aponta.
- Mecanismo da solução: como o produto resolve essa causa.
- Nome do mecanismo e o que resta da lógica se o nome for removido.
- Big Idea em uma frase.
- Inimigo nomeado.

## 6. Provas
| Claim | Prova apresentada | Tipo | Fonte | O que sustenta de fato | Limite |
Depoimento, autoridade, estudo e número citados pela copy são ALEGAÇÃO DA COPY.

## 7. Oferta
Produto principal · entregáveis e formato · bônus e o obstáculo que cada um remove · preço · parcelamento · ancoragem · garantia (tipo, prazo, condição) · urgência e escassez (e se parecem verdadeiras) · order bump · upsell · downsell · nome da oferta.

## 8. Objeções
| Objeção | Como a copy responde | Momento na VSL ou página | Força da resposta |

## 9. Funil e estrutura da copy
- Caminho: anúncio → pré-lander → quiz → VSL ou página → checkout → upsell.
- VSL ou carta bloco a bloco:
| Bloco | Tempo ou posição | Função | Resumo em suas palavras | Técnica usada |
Blocos típicos: hook, lead, história, descoberta, mecanismo do problema, mecanismo da solução, prova, apresentação do produto, stack, preço e ancoragem, garantia, urgência, CTA, FAQ, P.S.

## 10. Anúncios e hooks
| ID ou URL | Hook (tipo e texto) | Ângulo | Formato | Lead usado | Continuidade com a VSL |

## 11. Contexto de país (ofertas globais)
Referências culturais, unidades, sazonalidade, regulação, termos que não traduzem, provas que dependem do país, meios de pagamento.


=====
### ARQUIVO: references/modelagem-e-expansao.md
=====

# Modelagem e expansão

## 1. DNA funcional
Converta cada elemento do mapa em verbo de função: hook chama a persona pela situação; lead aumenta relevância e abre lacuna; mecanismo torna a solução compreensível e diferente; prova derruba uma dúvida específica; stack reduz risco, tempo e esforço percebidos; urgência justifica agir agora. O nome, a história e a frase são superfície. A função é o que se modela.

## 2. Semáforo (método Trip Angle)
| Cor | O que é | Uso |
|---|---|---|
| Verde | Função abstrata: autorreconhecimento, contraste, progressão de crença, demonstração, redução de risco, sequência de blocos | Modelar livremente |
| Amarelo | Padrão contextual: tipo de mecanismo, tipo de lead, arquitetura de funil, categoria de prova, modelo de garantia, estrutura de stack | Adaptar à persona, ao produto e à prova própria |
| Vermelho | Expressão e ativos: frases, nomes, histórias, personagens, especialistas, depoimentos, números, imagens, voz, design, promessa específica | Não reutilizar |
Teste rápido: se a copy nova depende de palavras, personagens, provas ou ativos da referência para funcionar, ainda não foi modelada. Auditoria completa em `../../agente-de-copy-trm/references/modelagem-sem-copia.md`.

## 3. Onde a expansão nasce
Cada ponto fraco do diagnóstico vira uma frente de expansão:
| Ponto fraco encontrado | Frente de expansão |
|---|---|
| Mercado sofisticado, promessa gasta | Mecanismo novo ou reposicionado; promessa pelo mecanismo |
| Consciência baixa tratada com oferta direta | Lead de história, segredo ou problema-solução |
| Prova fraca para o claim | Promessa um degrau abaixo, prova própria, demonstração |
| Stack com bônus de volume | Bônus que removem obstáculos reais do caminho |
| Objeção principal sem resposta | Bloco dedicado, garantia específica, FAQ |
| Uma única persona | Segmentação por situação, com lead e hook próprios |
| Urgência fraca ou falsa | Motivo real: lote, turma, bônus com prazo, custo de esperar |

## 4. Ângulo novo: ficha
Tese · inimigo · desejo de massa · persona e situação · nível de consciência · tipo de lead · mecanismo que sustenta · prova necessária · hook de exemplo · risco.

## 5. Mecanismo próprio: ficha
Nome candidato · causa que ele explica · por que as alternativas falharam · como a solução age · o que o produto entrega de fato para isso · prova disponível · prova necessária · teste do nome removido (a lógica se sustenta sem o nome?).

## 6. Escada de intensidade da promessa
Suba degrau a degrau e pare no último que a prova própria sustenta:
1. Benefício genérico.
2. Benefício específico com resultado concreto.
3. Resultado específico com prazo ou condição.
4. Resultado com mecanismo nomeado.
5. Resultado com mecanismo, prazo e contraste com o que falhou.
6. Resultado com mecanismo, prazo, contraste e prova visual ou demonstração.
Intensifique também sem subir o claim: mais desejo (cena, identidade, perda evitada), mais especificidade (números da própria oferta, passos, detalhes), mais contraste (antes e depois da situação, inimigo), mais facilidade (esforço e tempo menores percebidos).

## 7. Localização de oferta global
1. Traduza a função, nunca a frase.
2. Troque referências culturais, unidades, preços, datas comemorativas e exemplos.
3. Ajuste o nível de consciência e de sofisticação ao mercado local, que pode estar em estágio diferente.
4. Refaça provas com fontes locais ou próprias.
5. Revise regulação local: CDC, CONAR, ANVISA, LGPD e políticas da Meta no Brasil.
6. Reescreva a voz do cliente com frases do público local (comentários, fóruns, AGENTE DE ADS).

## 8. Oferta modelada (card)
Nome da oferta · persona principal · desejo de massa · consciência e sofisticação · Big Idea · mecanismo do problema · mecanismo da solução · promessa (degrau da escada) · produto e entregáveis · bônus e obstáculo removido · preço e ancoragem · garantia · urgência verdadeira · provas próprias · objeções prioritárias · lead escolhido · funil · linhagem (o que veio da referência como função) · claims pendentes · primeira hipótese de teste.


=====
### ARQUIVO: references/modelagem-sem-copia.md
=====

# Modelagem sem copiar (origem: skill agente-de-copy-trm (modelagem-sem-copia.md), consolidada em 13/09/2026)

# Como modelar uma oferta sem copiar (Modo 03 — Modelar)

Objetivo: transformar uma oferta já analisada em uma hipótese original, documentada e pronta para teste controlado, preservando a função estratégica que gerou o insight sem reutilizar identidade, expressão, prova ou claims da referência. Regra central: a referência fornece perguntas e funções; sua pesquisa fornece a linguagem; seu produto fornece a promessa; sua evidência fornece os claims. Se a nova oferta depende das palavras, personagens, provas ou ativos da referência para funcionar, ela ainda não foi modelada.

Cadeia: REFERÊNCIA → ORIGINAL → OBSERVAÇÃO → DNA → FUNÇÃO → PRINCÍPIO → SUPERFÍCIE → TRANSFERIBILIDADE → VARIÁVEL → HIPÓTESE → RECONSTRUÇÃO → AUDITORIA → TEST CARD → DADOS → APRENDIZADO.

Por que tanta cautela: ideias e métodos não têm proteção autoral, mas texto, imagem, vídeo, voz, design e depoimentos têm; e uma oferta que depende de prova alheia não sustenta a própria promessa. Modelagem bem feita produz algo que funciona sozinho.

## Checkpoint de entrada (não avance com item faltando)
[ ] original preservado (link, arquivo ou gravação) · [ ] data, canal, idioma, país, unidade analisada · [ ] Ficha Final de Leitura concluída · [ ] persona em situação, desejo, problema e crença identificados ou marcados NÃO MAPEADO · [ ] mecanismo do problema e da solução separados · [ ] Big Idea, ângulo, promessa, produto, oferta, prova e funil separados · [ ] claims tratados como alegações · [ ] capacidade própria de entrega definida · [ ] origem/autorização das provas próprias conhecida. Se a análise ainda mistura observação com hipótese, volte à leitura.

## Método em 10 etapas
1. **Escolha uma referência útil** por pergunta estratégica (atenção, explicação, desejo, prova, oferta, funil, conversão), não por gosto: anúncio com destino identificável, página/VSL/quiz acessível, produto e condições compreensíveis, alguma prova, situação de público discernível, comparável com outras.
2. **Descreva a função antes de procurar inspiração**: converta substantivos em verbos funcionais (Hook → chamar pela situação reconhecida; Lead → aumentar relevância e abrir lacuna; Ângulo → reenquadrar a causa; Mecanismo → tornar a solução compreensível e diferenciada; Prova → reduzir dúvida específica; Oferta → reduzir risco/esforço/demora; Funil → conduzir do reconhecimento à ação). "Os três portais secretos" é superfície; "organizar um problema confuso em poucas categorias memoráveis" é função.
3. **Extraia o DNA estratégico**: a relação entre as decisões que organizam a venda (template em `modelagem-templates.md`).
4. **Separe princípio, superfície e propriedade** com o semáforo: VERDE função abstrata (autorreconhecimento, contraste, progressão de crença, demonstração, redução de risco) pode orientar hipóteses; AMARELO padrão contextual (tipo de mecanismo, sequência de funil, categoria de prova, formato, modelo de garantia) exige pesquisa, adaptação profunda e prova própria; VERMELHO expressão e ativo (frases, nomes, histórias, personagens, imagens, vídeos, voz, design, depoimentos, números, autoridade, claim, escassez) não se reutiliza.
5. **Escolha a variável estratégica** (situação/persona, problema, mecanismo, ângulo, produto, prova, formato/funil). Na reconstrução, mude tudo o que for necessário para ser própria; no experimento, isole uma variável.
6. **Escreva a hipótese antes da peça**: "Para pessoa em situação X, aplicar o princípio Y por meio da configuração própria Z poderá melhorar o comportamento M, porque R. Saberemos pela métrica K dentro da janela J." Específica, rastreável, limitada, falsificável, compatível com o produto, proporcional à prova, separada de promessa pública.
7. **Reconstrua em página em branco** (feche a referência): situação com palavras da própria pesquisa → progresso desejado → problema sem o nome/metáfora da referência → mecanismo próprio e defensável → produto a partir dos obstáculos reais → promessa limitada ao que a entrega sustenta → prova própria por claim → Big Idea, ângulos, hooks e linguagem originais → formato e funil pela necessidade de compreensão → só então compare com a referência.
8. **Matriz de linhagem** referência × nova oferta (o que foi aprendido, o que foi reconstruído, por dimensão).
9. **Auditoria de originalidade** (dez testes): página em branco · identificação reversa · dependência · transformação · prova própria · promessa sustentada pelo produto · multiplicidade (princípio + pesquisa, não uma única referência) · verbal (sem tradução/paráfrase próxima) · visual (sem clonar layout, personagens, paleta, cenas, ritmo) · risco (marca, copyright, imagem, música, voz, privacidade, categoria sensível). Falhou item crítico → volta à reconstrução; não corrija trocando sinônimos.
10. **Converta em Test Card** (base 14) antes de publicar. "A versão B vendeu mais nesta janela" é observação; "por causa do mecanismo" é interpretação.

## Coerência promessa × produto × prova
O que a pessoa recebe (entregáveis, acesso, prazo, suporte) · que obstáculo cada componente remove · que resultado é controlável · que prova existe · que limites precisam aparecer. Bloqueios: produto abstrato, bônus por volume, promessa dependente de fatores externos, claim forte sem sustentação, omissão material. Registre alegações sensíveis em 12 — Claims e Risco. Claims de prosperidade, dinheiro, cura, saúde, ciência, energia, religião, autoridade, celebridade, escassez, garantia e resultado permanecem qualificados; não usar medo, culpa ou vulnerabilidade como pressão.

## O que este módulo não autoriza
Copiar frases trocando palavras; traduzir e apresentar como nova; manter persona, história, mecanismo, promessa, provas e visual mudando só o nome; reutilizar depoimentos, números, autoridades, imagens, vídeos, áudios, personagens ou escassez de terceiros; declarar referência "validada" por ter anúncios ativos; usar princípio de marketing para justificar alegação que o produto não comprova.

## Rubrica de prontidão (0–2 por critério, máx. 20)
Rastreabilidade · Decomposição · Princípio × superfície · Originalidade · Pesquisa da persona · Mecanismo · Promessa × produto · Prova e claims · Hipótese · Test Card. 16–20 segue para revisão final e teste pequeno; 12–15 revisar lacunas; 0–11 voltar à análise. Zero em originalidade, promessa × produto, prova/claims ou Test Card bloqueia.

## Entregável obrigatório
Uma página com: evidência de origem, DNA funcional, matriz verde/amarelo/vermelho, variável e hipótese, Nova Configuração da Oferta, Matriz de Linhagem, auditoria de originalidade, claims pendentes e Test Card. Templates em `modelagem-templates.md`.


=====
### ARQUIVO: references/modelagem-templates.md
=====

# Templates de modelagem (Trip Angle)

## Ficha de Origem
Referência (nome/código) · Fonte preservada (link, arquivo, gravação) · Data, canal, idioma, país · Unidade analisada (Ad / VSL / página / quiz / checkout) · Pergunta estratégica que justifica a escolha (atenção, explicação, desejo, prova, oferta, funil, conversão) · Ficha de Leitura vinculada · Status de linhagem.

## DNA funcional da referência
| Dimensão | O que a referência faz (função, em verbo) | Como faz (superfície, só para registro) | Rótulo |
|---|---|---|---|
| Interrupção / seleção (hook) | | | |
| Relevância e lacuna (lead) | | | |
| Reenquadramento da causa (ângulo / mecanismo do problema) | | | |
| Explicação da solução (mecanismo) | | | |
| Nova oportunidade / Big Idea | | | |
| Promessa e condições | | | |
| Prova (que dúvida reduz) | | | |
| Produto e componentes (que obstáculo removem) | | | |
| Redução de risco (garantia, urgência) | | | |
| Funil (por que cada transição existe) | | | |
| Ordem dos argumentos / progressão de crença | | | |

## Matriz verde / amarelo / vermelho
| Elemento observado | Faixa | Tratamento |
|---|---|---|
| ex.: diagnóstico de 3 perguntas antes da promessa | VERDE — função "permitir autorreconhecimento antes da solução" | pode orientar hipótese |
| ex.: quiz de 16 telas com IMC | AMARELO — padrão contextual (formato/sequência) | exige pesquisa, adaptação e prova própria |
| ex.: "Mounjaro de Pobre", áudio da nutricionista, "4 pessoas comprando agora" | VERMELHO — nome, prova de terceiros, escassez | não reutilizar |

Transferível como função: interromper pela situação; selecionar a pessoa certa; tornar problema complexo compreensível; contraste entre tentativa anterior e nova possibilidade; demonstrar uma etapa do processo; antecipar objeção; reduzir esforço/demora/risco percebido; organizar progressão de crença; definir decisão mensurável.
Precisa nascer de novo: persona e contexto; pesquisa e linguagem; tese, mecanismo e explicação; Big Idea, ângulo, promessa, hooks; produto, método, componentes, experiência; provas, demonstrações e casos autorizados; nome, identidade, estética, ativos; preço, garantia, bônus, escassez, condições; página, VSL, criativos, checkout.

## Card da Hipótese
- Situação X (persona em circunstância, com linguagem própria):
- Princípio Y (função transferida):
- Configuração própria Z (produto/mecanismo/prova/formato):
- Comportamento M esperado:
- Porque R (razão observável):
- Métrica K · Janela J:
- Variável isolada no experimento:
- O que não muda:
- Risco/claim a revisar:

## Nova Configuração da Oferta
Persona em situação · Problema · Mecanismo do problema · Mecanismo da solução · Princípio transferido · Produto próprio · Promessa defensável (sem resultado automático) · Prova própria · Formato/funil · Hipótese de teste.

## Matriz de Linhagem — referência × nova oferta
| Dimensão | Referência (observado) | Nova oferta (reconstruído) | O que foi aprendido | Distância |
|---|---|---|---|---|
| Persona/situação | | | | |
| Problema e mecanismo | | | | |
| Big Idea / ângulo | | | | |
| Promessa | | | | |
| Prova | | | | |
| Produto e stack | | | | |
| Preço, garantia, escassez | | | | |
| Formato e funil | | | | |
| Hook / linguagem | | | | |
| Identidade visual | | | | |

## Auditoria de originalidade (marcar cada item)
[ ] Página em branco · [ ] Identificação reversa · [ ] Dependência · [ ] Transformação · [ ] Prova própria · [ ] Promessa sustentada · [ ] Multiplicidade · [ ] Verbal · [ ] Visual · [ ] Risco.

## Por que isso é modelagem e não cópia (checklist do exemplo)
O problema de mercado mudou · situação e linguagem reconstruídas · mecanismo operacional próprio · produto e demonstração nasceram do novo obstáculo · promessa limitada ao que a entrega controla · nenhum nome, frase, personagem, claim, prova ou ativo reutilizado · o que permaneceu foi apenas a função abstrata.

## Erros mais comuns
Trocar palavras mantendo a copy; traduzir criativo estrangeiro; confundir mecanismo com nome chamativo; modelar promessa sem produto equivalente; usar prova da referência; manter personagem/autoridade/história alheia; escolher oferta "bonita" sem pergunta estratégica; misturar observação com interpretação; mudar tudo no teste; tratar CTR como prova de oferta; urgência/escassez fictícia; ocultar limitações; depender de uma única referência; consultar swipe file antes de entender o problema; encerrar o teste sem registrar aprendizado.


=====
### ARQUIVO: references/modelo-oferta-aprovada.md
=====

# Modelo de `04-oferta-aprovada.md`

Copie a estrutura abaixo. Toda afirmação recebe um rótulo entre colchetes: **[EVIDÊNCIA — fonte]**, **[HIPÓTESE]**, **[DECISÃO — quem, quando]** ou **[AUSENTE]**.

---

# 04 — Oferta aprovada · [produto] · v[n] · [data]

## 1. Entradas utilizadas
| Entrada | Recebida | Observação |
|---|---|---|
| 00-briefing-e-plano.md | sim / não | |
| 01-inteligencia-dr.md | sim / não | |
| 02-modelagem.md | sim / não | |
| 03-avatar-ads.md + handoff da Etapa 03 | sim / não | |
| Custos, preço mínimo, capacidade de entrega | sim / não / ausente por decisão | |
| Provas e diferenciais reais | sim / não / ausente por decisão | |
| Regras da plataforma e do mercado | sim / não | |

## 2. Base da oferta
- Problema (vocabulário do avatar): … [rótulo]
- Transformação (estado atual → desejado): … [rótulo]
- Mecanismo do problema: … [rótulo]
- Mecanismo da solução: … [rótulo]
- Produto principal e pilha de valor (entregáveis, formato, acesso, suporte, prazo, limites): … [rótulo]

## 3. Conceitos de oferta

### Conceito A — ângulo: [nome do ângulo]
| Campo | Conteúdo | Rótulo |
|---|---|---|
| Avatar e problema | | |
| Transformação | | |
| Promessa responsável | | |
| Mecanismo | | |
| Produto principal | | |
| Bônus (cada um: que obstáculo remove, acelera ou que risco reduz) | | |
| Prova disponível (com fonte) | | |
| Prova ainda necessária | | |
| Garantia (cobertura, prazo, procedimento, exclusões) | | |
| Preço e justificativa | | |
| Objeções | | |
| Riscos (legais, operacionais, de plataforma) | | |
| Headline provisória | | |
| CTA provisório | | |

Sete perguntas — respostas curtas (ver `offer-card.md`):
1. Para quem é: …
2. Qual mudança é prometida: …
3. Como acontece: …
4. O que a pessoa recebe: …
5. Por que acreditar: …
6. Qual esforço e risco permanecem: …
7. Por que decidir agora: …

### Conceito B — ângulo: [nome do ângulo]
(mesma estrutura)

### Conceito C — ângulo: [nome do ângulo]
(mesma estrutura)

## 4. Scorecard comparativo
(tabela de `scorecard.md`, com evidência ao lado de cada nota e lista de notas baixas convertidas em pendência ou hipótese)

## 5. Recomendação
- Conceito recomendado: …
- Justificativa por evidência, clareza, desejo, credibilidade e viabilidade: …
- O que os descartados perdem: …
- Elementos que migram para o vencedor: …

## 6. Offer Card do conceito aprovado
(tabela completa de `offer-card.md`, 13 campos; campo sem informação = AUSENTE)

## 7. Claims e provas pendentes · riscos
| Claim | Prova disponível | Prova necessária | Sensível? | Ação |
|---|---|---|---|---|
| | | | sim / não | |

Riscos legais e operacionais: …

## 8. Aprovação
- Status: rascunho / aprovada
- Aprovada por: … em …
- Condições da aprovação: …

## 9. HANDOFF DO PROJETO
```
HANDOFF DO PROJETO
Etapa concluída: 04 — Mineração de Ofertas
Versão e data:
Objetivo:
Entradas utilizadas:
Evidências confirmadas:
Hipóteses abertas:
Decisões aprovadas:
Artefatos produzidos: 04-oferta-aprovada.md
Claims e provas pendentes:
Riscos e restrições:
Métrica principal:
Portão de aprovação:
Próximo agente: 05 — Copy
Próxima ação única:
```


=====
### ARQUIVO: references/offer-card-7-perguntas-hierarquia-prova.md
=====

# Offer Card, sete perguntas e hierarquia de prova (versão consolidada)

Fonte única para a Etapa 04 e para o módulo 03 — Engenharia de Ofertas, Copy e Vendas. As duas páginas de origem traziam redações divergentes; esta versão é a união dos campos, sem acréscimo de conteúdo novo. Onde a redação diverge, a escolha está anotada.

## As sete perguntas obrigatórias

Toda oferta responde às sete. Pergunta sem resposta sustentada por evidência é lacuna declarada, não texto de preenchimento.

| # | Pergunta | O que a resposta precisa conter |
|---|---|---|
| 1 | **Para quem é?** | Recorte de público e situação específica. |
| 2 | **Qual mudança é prometida?** | Resultado específico, responsável e delimitado. |
| 3 | **Como acontece?** | Mecanismo da solução e sequência de etapas. |
| 4 | **O que a pessoa recebe?** | Produto, entregáveis, acesso, suporte e limites. |
| 5 | **Por que acreditar?** | Evidência adequada ao claim: demonstração, evidência, processo, credencial ou caso verificável. |
| 6 | **Qual esforço e risco permanecem?** | Tempo, participação, requisitos e limitações. |
| 7 | **Por que decidir agora?** | Motivo verdadeiro: janela, capacidade, agenda, bônus ou custo da espera. Nunca escassez inventada. |

Nota de consolidação: a pergunta 5 usa a redação do módulo 03 (lista os tipos de evidência); a Etapa 04 dizia apenas "evidência adequada ao claim". A pergunta 7 usa os exemplos de motivo do módulo 03.

## Offer Card

Preencha todos os campos para o conceito recomendado. Campo sem informação recebe **AUSENTE** e vira item em "Claims e provas pendentes" ou "Riscos e restrições" do handoff.

| Campo | Preenchimento | Origem do campo |
|---|---|---|
| Público + situação | Quem enfrenta qual momento específico. | 03 e 04 |
| Transformação | Do estado atual ao estado desejado. | 03 e 04 |
| Mecanismo do problema | Por que o problema persiste apesar das alternativas atuais. | 04 |
| Mecanismo da solução | Princípio e sequência que tornam a mudança plausível. | 03 e 04 |
| Entregáveis e limites | O que entra, formato, duração, acesso, o que não está incluído. | 03 e 04 |
| Suporte e prazo | Canal, cadência e duração do suporte; prazo de entrega ou acesso. | 04 |
| Prova disponível | Evidências verificáveis e relevantes para o claim, com fonte. | 03 e 04 |
| Prova ainda necessária | O que precisaria existir para sustentar cada claim ainda sem prova. | 04 |
| Objeções | Confiança, valor, tempo, esforço, prioridade, autoridade e risco. | 03 e 04 |
| Preço e condições | Valor, parcelas, renovação, custos adicionais e regras. | 03 e 04 |
| Garantia e limites | O que é coberto, prazo, procedimento e exclusões claras. | 03 e 04 |
| CTA | Uma próxima ação objetiva. | 03 e 04 |
| Riscos legais e operacionais | Claims sensíveis, política de plataforma, capacidade de entrega, reembolso. | 04 |

Critério de fechamento (checkpoint 3 do módulo 03): a oferta é entendida sem adjetivos vagos; o mecanismo é plausível; escopo e limites estão visíveis; cada claim importante tem prova correspondente.

## Hierarquia de prova

Use sempre a prova mais próxima possível da promessa. Quanto mais abaixo na lista, menor o alcance do claim que ela sustenta.

1. Demonstração do produto ou processo.
2. Dados próprios com método e contexto.
3. Caso verificável semelhante ao público.
4. Depoimento específico e autorizado.
5. Credencial relevante.
6. Explicação plausível.
7. Opinião.

Prova inexistente bloqueia claim forte: o claim volta a ser hipótese até a prova existir.

## Claims sensíveis

Resultados financeiros, saúde, emagrecimento, segurança, garantia de retorno, crianças e comparações absolutas exigem revisão própria antes de qualquer publicação. Aplicam-se o Código de Defesa do Consumidor (arts. 36–38), o Código do CONAR e a LGPD/ANPD para dados pessoais. Não publicar prova, depoimento ou urgência fabricados.


=====
### ARQUIVO: references/scorecard-da-oferta.md
=====

# Scorecard da oferta e comparação de conceitos

## Como usar

Pontue cada um dos três conceitos de 1 a 5 em cada critério. Ao lado de toda nota, escreva em uma linha a evidência que a sustenta (ou "hipótese" se não houver). Nota baixa não pode ser escondida por copy: vira **pendência** (o que precisa existir) ou **hipótese de teste** (o que será verificado na Etapa 08).

A origem não fixa o que é "nota baixa". Até o operador definir um corte, trate 1 e 2 como baixa e registre o critério adotado no arquivo.

## Critérios

| Critério | Pergunta de apoio | 1 | 5 |
|---|---|---|---|
| Clareza | A oferta se entende em uma leitura, sem adjetivo vago? | Precisa de explicação | Entendida na primeira leitura |
| Relevância para o avatar | Fala da situação e do desejo registrados no avatar? | Genérica | Usa a situação e a linguagem do avatar |
| Diferenciação | O mecanismo se distingue das alternativas mapeadas na inteligência e na modelagem? | Igual ao mercado | Mecanismo próprio e reconhecível |
| Credibilidade | A promessa é proporcional ao que o produto entrega? | Promete além da entrega | Promessa dentro do escopo |
| Força da prova | A prova disponível está no topo da hierarquia para o claim principal? | Só opinião ou nenhuma | Demonstração ou dados próprios |
| Viabilidade de entrega | A operação entrega com a capacidade informada? | Não comprovada | Confirmada pelo operador |
| Margem | Preço cobre custos e preço mínimo informados? | Ausente ou negativa | Confirmada com números do operador |
| Reversão de risco | A garantia cobre o risco percebido e a operação suporta? | Nenhuma ou insustentável | Clara, com procedimento e exclusões |
| Simplicidade da decisão | Há uma próxima ação e uma condição de compra? | Várias decisões ou condições ocultas | Uma ação, condições visíveis |
| Compliance | Há claim sensível sem revisão ou política de plataforma em risco? | Claims sem revisão | Sem claim sensível pendente |

## Tabela comparativa

| Critério | Conceito A | Conceito B | Conceito C |
|---|---|---|---|
| Clareza | | | |
| Relevância para o avatar | | | |
| Diferenciação | | | |
| Credibilidade | | | |
| Força da prova | | | |
| Viabilidade de entrega | | | |
| Margem | | | |
| Reversão de risco | | | |
| Simplicidade da decisão | | | |
| Compliance | | | |
| **Total (máx. 50)** | | | |
| Notas baixas → pendência ou hipótese | | | |

## Recomendação

A recomendação do vencedor é justificada por **evidência, clareza, desejo, credibilidade e viabilidade**, citando as notas acima e os arquivos de origem (00 a 03). Registre também o que os conceitos descartados perdem e se algum elemento deles migra para o vencedor.
