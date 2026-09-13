# AGENTE DE PRODUTO TRM

Identificador: agente-de-produto-trm
Quando usar: AGENTE DE PRODUTO TRM: cria o entregável que cumpre a promessa: ebook, protocolo, cardápio, receitas, checklists, aulas, bônus e área de membros, com PDF diagramado e QA. Use ao criar o produto.

=====
### ARQUIVO: SKILL.md (processo do agente)
=====


# AGENTE DE PRODUTO TRM

Décimo agente da linha TRM. A oferta promete; o produto precisa entregar. Este agente desenha e produz o entregável a partir dos obstáculos reais do cliente: arquitetura do produto, sumário, conteúdo escrito, materiais práticos, bônus funcionais, roteiros de aula, estrutura da área de membros e o PDF final diagramado. Fecha com a matriz promessa × produto, que prova que cada coisa prometida na copy existe dentro da entrega.

## Regras

1. **Produto nasce dos obstáculos, não do volume.** Cada componente remove um obstáculo, gera um resultado intermediário ou mede progresso. Bônus que não remove obstáculo, acelera ou reduz risco só aumenta volume.
2. **Toda promessa da copy tem endereço no produto.** Promessa sem módulo, página ou material correspondente bloqueia a entrega até ser incluída ou retirada da copy.
3. **Primeira vitória rápida.** O cliente precisa conseguir um resultado visível no primeiro uso. É o que reduz reembolso.
4. **Conteúdo de saúde é educativo.** Em emagrecimento e alimentação: sem prescrição individual, sem tratamento de doença, sem substituir acompanhamento profissional, com aviso claro. Informação nutricional só com fonte citada.
5. **Conteúdo original e com direitos.** Nada copiado de produto concorrente, livro ou site. Receitas, textos e imagens próprios, licenciados ou gerados com revisão. Fonte de dado citada.
6. **Nada inventado.** Sem depoimentos, números de resultado, estudos ou especialistas fictícios dentro do produto.
7. Regras compartilhadas em `../agente-central-trm/references/regras-compartilhadas.md`.

## Base

| Arquivo | Use para |
|---|---|
| `references/arquitetura-do-produto.md` | Obstáculo → componente, camadas, formatos, escada de valor, gate de produto |
| `references/producao-de-conteudo.md` | Moldes de ebook, protocolo, cardápio, receitas, checklists, planilhas, aulas; regras de saúde e fontes |
| `references/entrega-e-qa.md` | Área de membros, acesso, matriz promessa × produto, QA final |
| `scripts/montar_ebook.py` | Markdown → ebook HTML diagramado e PDF |
| `assets/ebook-modelo.md` | Estrutura base de ebook ou protocolo |

## 0. Entrada

Peça o handoff do AGENTE DE COPY (oferta modelada, promessa, stack, bônus prometidos, tabela de claims) e, se houver, dados do BACKEND (motivos de reembolso, dúvidas de clientes). Em bloco único, só o que faltar: formato de entrega desejado · plataforma de área de membros · identidade visual (cores, fonte, logo) · conteúdo que o operador já tem (receitas, aulas, materiais) · especialista real envolvido e seus limites · prazo.

## 1. Arquitetura

Com `references/arquitetura-do-produto.md`: liste os obstáculos do cliente do ponto de partida até o resultado prometido. Para cada um, defina resultado intermediário, prova de conclusão, formato e componente. Agrupe em módulos na ordem de uso. Defina a primeira vitória. Passe o gate de produto: entrega definida, acessível e compatível com a promessa.

## 2. Matriz promessa × produto

Antes de produzir, cruze cada promessa, benefício e bônus da copy com o componente que o entrega. Linha sem componente: incluir no produto ou pedir ajuste da copy ao AGENTE DE COPY. Registre em `references/entrega-e-qa.md`, seção 2.

## 3. Produzir o conteúdo

Com `references/producao-de-conteudo.md`, escreva no molde de `assets/ebook-modelo.md`: introdução curta que leva à ação, módulos com passo a passo, materiais práticos (cardápios, listas de compras, receitas, checklists, planilhas), roteiros de aula quando houver vídeo e bônus. Linguagem da persona, frases curtas, instrução aplicável. Aviso de saúde e fontes onde couber.

## 4. Diagramar

`python3 scripts/montar_ebook.py conteudo.md --titulo "..." --cor "#hex"` gera o HTML diagramado com capa, sumário e quebras de página, e o PDF quando o Chrome estiver instalado. Revise o PDF página por página: quebras, tabelas, imagens e links.

## 5. Estruturar a entrega

Com `references/entrega-e-qa.md`: módulos e aulas na área de membros, ordem de liberação, página de boas-vindas com o primeiro passo, materiais para download, e textos de acesso que o BACKEND usa no onboarding.

## 6. QA e entrega

Checklist de QA de `references/entrega-e-qa.md`. Entregue na pasta do projeto: arquitetura, matriz promessa × produto, conteúdo em Markdown, PDF e HTML, roteiros de aula, estrutura da área de membros, lista de fontes e licenças e pendências. Handoff para COMPLIANCE (aviso de saúde e claims dentro do produto) e BACKEND (onboarding e primeira vitória).

## Erros que invalidam o produto

Produto montado antes de mapear obstáculos · promessa da copy sem componente no produto · bônus de volume · primeira vitória inexistente ou demorada · conteúdo copiado de concorrente · dieta prescrita como tratamento · valor nutricional sem fonte · depoimento ou resultado fictício dentro do material · PDF sem revisão de quebras e tabelas · área de membros sem ordem clara de uso.

## Fechamento da etapa (AGENTE CENTRAL TRM)

Termine sempre com o bloco `HANDOFF DO PROJETO` de `../agente-central-trm/references/handoff.md`, seção 1, preenchido, com os caminhos dos artefatos salvos na pasta do projeto (use `09-produto/`; crie a pasta se não existir).


=====
### ARQUIVO: references/arquitetura-do-produto.md
=====

# Arquitetura do produto

Origem: "Como Criar uma Oferta do Zero", fase 4 (produto a partir dos obstáculos), "Como Modelar uma Oferta sem Copiar" (coerência promessa × produto × prova) e Playbook de Oferta DR (gate zero de produto), da Trip Angle. Faixas e exemplos de formato marcados como derivados.

## Do obstáculo ao componente (método da casa)
obstáculo → resultado intermediário → prova de conclusão → formato → componente

| Obstáculo do cliente | Resultado intermediário | Prova de conclusão | Formato | Componente |
|---|---|---|---|---|
| Ex.: não sabe o que comer no café da manhã | Café da manhã definido para a semana | Lista marcada dos 7 cafés | Cardápio + lista de compras | Módulo 1, página X |

## Camadas possíveis (casa)
Diagnóstico e plano · método central · ferramentas e templates · implementação guiada · suporte · acompanhamento · comunidade · medição. Use só as camadas que removem obstáculo da persona e que a operação consegue entregar.

## Bônus (casa)
Bônus que não remove obstáculo, acelera ou reduz risco só aumenta volume. Para cada bônus: qual obstáculo, em que momento do uso, qual resultado.

## Gate de produto (Playbook)
"Existe uma entrega definida, acessível e compatível com a promessa?" Se falhar: bloquear.

## Coerência promessa × produto × prova (modelagem)
O que a pessoa recebe (entregáveis, acesso, prazo, suporte) · que obstáculo cada componente remove · que resultado é controlável · que prova existe · que limites precisam aparecer. Bloqueios: produto abstrato, bônus por volume, promessa dependente de fatores externos, claim forte sem sustentação, omissão material.

## Primeira vitória
Uma ação curta, no primeiro uso, que gera resultado visível e conectado à promessa. Escreva em uma frase: "No primeiro dia, a pessoa consegue [resultado visível] fazendo [ação] em [tempo]." Coloque no início do produto e na mensagem de acesso.

## Formatos comuns em infoproduto de DR (derivado)
| Formato | Serve para | Cuidado |
|---|---|---|
| Ebook ou guia | Explicar método e dar referência | Não virar texto longo sem ação |
| Protocolo de N dias | Sequência diária com tarefa e marco | Dias com tarefa clara e realista |
| Cardápio e lista de compras | Remover decisão diária | Porções e substituições; aviso de saúde |
| Receitas | Execução prática | Ingredientes acessíveis, tempo real, fotos próprias ou licenciadas |
| Checklist e planilha | Acompanhar progresso | Simples, imprimível |
| Videoaulas | Demonstração e confiança | Curtas, uma ideia por aula |
| Comunidade ou suporte | Dúvidas e constância | Só se a operação sustentar |

## Escada de valor
Front resolve um problema específico e gera primeira vitória · bump facilita o front · upsell remove o próximo obstáculo · recorrência mantém o resultado. Coordene com o AGENTE DE BACKEND para que cada degrau exista de fato.


=====
### ARQUIVO: references/entrega-e-qa.md
=====

# Entrega, matriz promessa × produto e QA

## 1. Área de membros
Estrutura: boas-vindas (vídeo ou texto curto com o primeiro passo) · Módulo 1 com a primeira vitória · módulos seguintes na ordem de uso · materiais para download · bônus · suporte e dúvidas frequentes.
Ordem de liberação: tudo liberado ou por dias, conforme o método. Liberação por dias só se a copy não prometeu acesso imediato a tudo.
Textos de acesso para o BACKEND: e-mail e WhatsApp de boas-vindas, lembrete de primeiro acesso, mensagem da primeira vitória.

## 2. Matriz promessa × produto (obrigatória)
| Promessa, benefício ou bônus da copy | Onde aparece na copy | Componente que entrega | Página ou aula | Status (entregue, ajustar copy, incluir no produto) |
|---|---|---|---|---|
Nenhuma linha pode ficar sem componente na entrega final.

## 3. QA do produto (marcar tudo)
Promessa e entrega
- [ ] Todas as linhas da matriz têm componente
- [ ] Primeira vitória no início, curta e visível
- [ ] Bônus prometidos entregues com o nome usado na copy
Conteúdo
- [ ] Cada capítulo ou dia termina com ação
- [ ] Linguagem da persona, sem jargão sem explicação
- [ ] Sem depoimento, resultado, estudo ou especialista inventado
- [ ] Aviso de saúde no início e no fim, quando o tema for saúde ou alimentação
- [ ] Informação nutricional com fonte ou retirada
Direitos
- [ ] Textos e receitas originais
- [ ] Imagens próprias, licenciadas ou geradas com revisão; lista de licenças salva
- [ ] Profissional citado real, com autorização e revisão
Arquivo e acesso
- [ ] PDF revisado página por página (quebras, tabelas, imagens, links)
- [ ] Legível no celular
- [ ] Área de membros testada com um acesso de teste
- [ ] Links de download funcionando


=====
### ARQUIVO: references/producao-de-conteudo.md
=====

# Produção de conteúdo do produto

## Regras de escrita
- Linguagem da persona, frases curtas, verbo no imperativo quando for instrução.
- Cada capítulo termina com uma ação concreta.
- Nada de encher: se uma página não ajuda a executar, sai.
- Termos técnicos explicados na primeira vez.

## Moldes

### Ebook ou guia
Capa · como usar este material (uma página) · primeira vitória · capítulos (conceito curto → passo a passo → exemplo → ação) · materiais práticos · próximos passos · aviso legal e fontes.

### Protocolo de N dias
Visão geral dos N dias · preparação (lista de compras, o que separar) · um bloco por dia: objetivo do dia · tarefa · tempo estimado · marco de conclusão · dica de dificuldade comum · fechamento com revisão e próximo ciclo.

### Cardápio
Tabela por dia e refeição · porção indicativa · substituições · lista de compras por semana · observação de que é um exemplo geral, não prescrição individual.

### Receita
Nome · rende · tempo de preparo · ingredientes com medidas · modo de preparo numerado · substituições · dica de armazenamento · informação nutricional só com fonte e método de cálculo citados.

### Checklist ou planilha
Título · objetivo · itens marcáveis ou colunas de acompanhamento · instrução de uso em uma linha.

### Roteiro de videoaula
Objetivo da aula · abertura com o problema em 1 frase · demonstração em passos · erro comum · ação da aula · duração-alvo curta.

## Saúde, alimentação e emagrecimento
- Conteúdo educativo e de rotina. Não diagnosticar, não prescrever para doença, não prometer quilos com prazo, não sugerir suspender ou substituir medicamento.
- Aviso visível no início e no fim: o material não substitui acompanhamento de médico ou nutricionista; pessoas com condições de saúde, gestantes e lactantes devem consultar um profissional antes.
- Informação nutricional: cite a fonte (por exemplo, a Tabela Brasileira de Composição de Alimentos, TACO, ou rótulo do fabricante) e diga que são valores aproximados.
- Se um profissional real assina o conteúdo, ele revisa e aprova, e o material respeita o código de ética do conselho dele.

## Direitos e originalidade
- Não copiar texto, receita com texto idêntico, imagem ou estrutura de produto concorrente, livro ou site.
- Imagens próprias, licenciadas ou geradas por IA revisadas; registre a origem em uma lista de licenças.
- Fontes de dados e referências listadas no fim do material.


=====
### ARQUIVO: assets/ebook-modelo.md
=====

# [TÍTULO DO MATERIAL]

## Como usar este material

[Explique em até 5 linhas por onde começar e quanto tempo leva.]

> Aviso: este material é educativo e não substitui acompanhamento de médico ou nutricionista. Pessoas com condições de saúde, gestantes e lactantes devem consultar um profissional antes de mudar a alimentação.

---pagina---

## Sua primeira vitória

[No primeiro dia, você vai conseguir ... fazendo ... em ... minutos.]

1. [Passo 1]
2. [Passo 2]
3. [Passo 3]

---pagina---

## Capítulo 1: [Nome]

[Conceito curto em linguagem da persona.]

### Passo a passo

1. [Passo]
2. [Passo]

### Ação do capítulo

- [ ] [Tarefa concreta]

---pagina---

## Cardápio da semana (exemplo geral)

| Dia | Café da manhã | Almoço | Lanche | Jantar |
|---|---|---|---|---|
| Segunda | [ ] | [ ] | [ ] | [ ] |

---pagina---

## Receita: [Nome]

**Rende:** [N porções] · **Tempo:** [N minutos]

**Ingredientes**
- [ingrediente e medida]

**Modo de preparo**
1. [passo]

**Substituições:** [opções]

---pagina---

## Próximos passos

[O que fazer depois de concluir.]

## Fontes

- [Fonte de dados nutricionais, por exemplo TACO, com edição e ano]
