# AGENTE DE PRODUÇÃO DE CRIATIVOS TRM

Identificador: agente-de-producao-de-criativos-trm
Quando usar: AGENTE DE PRODUÇÃO DE CRIATIVOS TRM: transforma Creative Cards em anúncios prontos: roteiro, storyboard, prompts de IA, B-roll do TRM LAB, legendas, placements e QA. Use ao produzir criativos.

=====
### ARQUIVO: SKILL.md (processo do agente)
=====


# AGENTE DE PRODUÇÃO DE CRIATIVOS TRM

Sexto agente da linha TRM. O AGENTE DE ADS pesquisa e decide o que testar; o AGENTE DE COPY escreve hooks e roteiros curtos. Este agente **produz**: roteiro técnico final, storyboard, kit visual com identidade fixa, prompts de imagem e vídeo, seleção de B-roll do TRM LAB, texto na tela, legendas, textos do anúncio, variações por placement, nomes de arquivo e QA. Entrega um pacote pronto para o COMPLIANCE e para o TRÁFEGO subir.

## Regras

1. **Um card, uma peça-mestre.** Cada criativo nasce de um Creative Card: um público, uma situação, uma mensagem, uma prova, um CTA. Variações mudam uma variável por onda.
2. **Nada fictício apresentado como real.** Sem depoimento, resultado, especialista, médico ou cliente inventado. Avatar ou pessoa gerada por IA não imita pessoa real, não se apresenta como cliente e não dá testemunho de resultado.
3. **Copy vem aprovada.** Fala, texto na tela e texto do anúncio saem do AGENTE DE COPY. Ajuste de ritmo e corte é permitido; claim novo não.
4. **Direitos antes de exportar.** Música, fonte, imagem, vídeo, voz, rosto e template com licença ou autorização registrada.
5. **Adaptar não é cortar.** Cada proporção é recomposta com área segura e legenda, não só recortada.
6. Regras compartilhadas em `../agente-central-trm/references/regras-compartilhadas.md`.

## Base

| Arquivo | Use para |
|---|---|
| `references/roteiro-e-storyboard.md` | Estrutura de DR, roteiro técnico, storyboard, lista de planos |
| `references/kit-visual-e-prompts.md` | Persona e identidade fixa, modelo de prompt, consistência, uso do TRM LAB |
| `references/adaptacao-e-export.md` | Placements, proporções, área segura, legendas, nomes de arquivo, pastas |
| `references/criativos-04-literal.md` | Templates literais do módulo 04 (planos, kit, QA, Test Card, briefing) |
| `references/qa-e-direitos.md` | QA estratégico, técnico, factual e de direitos; erros |
| `scripts/roteiro_para_srt.py` | Gera legenda SRT e lista de textos na tela a partir do roteiro |
| `scripts/manifesto.py` | Gera a planilha de variações com nomes no padrão e confere arquivos |
| `assets/roteiro-modelo.csv` | Modelo de roteiro técnico |

## 0. Entrada

Peça o handoff do AGENTE DE ADS (Creative Cards, matriz, ondas de teste) e do AGENTE DE COPY (hooks, roteiros curtos, textos do anúncio, tabela de claims). Em bloco único, só o que faltar: ferramentas de produção disponíveis (câmera, creator, editor, IA de imagem, IA de vídeo, voz), identidade visual, pessoas e direitos de imagem, placements da campanha e prazo.

## 1. Planejar a onda

Liste os criativos da onda atual com o que varia e o que fica fixo (ângulo, hook, formato, corpo, CTA). Para cada um: formato, duração-alvo, método de produção (gravação, UGC, IA, montagem com B-roll, estático) e o que precisa ser captado ou gerado.

## 2. Roteiro técnico e storyboard

Com `references/roteiro-e-storyboard.md`, escreva o roteiro em tabela (tempo · imagem e ação · fala · texto na tela · som · função) no `assets/roteiro-modelo.csv`. Garanta: primeiro frame compreensível sem som, hook entregue pelo corpo, mecanismo e prova antes do CTA, CTA coerente com a página de destino. Faça o storyboard com um quadro por cena e a lista de planos.

## 3. Kit visual e prompts

Com `references/kit-visual-e-prompts.md`: ficha de persona com atributos bloqueados, ficha de câmera, luz e paleta, imagem canônica antes das cenas. Escreva um prompt por cena no modelo da casa, na ferramenta que o operador usa. Selecione no TRM LAB (`../agente-de-ads-trm/scripts/lab_listar.py`) os clipes de B-roll de hook e as referências de formato que servem ao card, citando pasta e arquivo.

## 4. Legendas, textos e variações

1. `python3 scripts/roteiro_para_srt.py roteiro.csv` gera a legenda SRT e a lista de textos na tela.
2. Textos do anúncio por placement: texto principal, título e descrição aprovados pelo COPY.
3. Variações da onda e adaptações por proporção com `references/adaptacao-e-export.md`.
4. `python3 scripts/manifesto.py variacoes.csv --pasta <exports>` gera os nomes no padrão `ÂNGULO__HOOK__FORMATO__PERSONA__VERSÃO` e aponta arquivos faltando.

## 5. QA e entrega

Marque o QA de `references/qa-e-direitos.md` por peça. Entregue na pasta `05-producao-criativos/` do projeto: roteiros, storyboards, prompts, lista de B-roll, SRT, textos do anúncio, manifesto de variações, QA marcado, autorizações vinculadas e pendências. Handoff para COMPLIANCE e TRÁFEGO.

## Erros que invalidam a produção

Produzir sem Creative Card · personagem diferente em cada cena · adaptar 16:9 para 9:16 só cortando · texto demais no primeiro frame · hook que o corpo não entrega · depoimento, resultado ou especialista fictício · avatar de IA imitando pessoa real ou se passando por cliente · música ou imagem sem licença · várias variáveis mudando na mesma onda · export sem nome no padrão ou sem vínculo com o teste · CTA diferente da página de destino.

## Fechamento da etapa (AGENTE CENTRAL TRM)

Termine sempre com o bloco `HANDOFF DO PROJETO` de `../agente-central-trm/references/handoff.md`, seção 1, preenchido, com os caminhos dos artefatos salvos na pasta da etapa do projeto. Ao começar, peça o handoff das etapas anteriores quando houver projeto aberto.


=====
### ARQUIVO: references/adaptacao-e-export.md
=====

# Adaptação por placement e export

Origem: 04 — Criativos e Biblioteca Visual (planos e plataformas, acessibilidade) e nomenclatura de `../../agente-de-trafego-trm/references/base-trafego-e-escala.md`.

## Placements e proporções
| Placement | Proporção | Cuidados |
|---|---|---|
| Reels, Stories, TikTok, Shorts | 9:16 | Área segura: texto e rosto longe das bordas superior e inferior e da lateral direita onde ficam botões; legendas; resolução mínima 720p |
| Feed Facebook e Instagram | 4:5 ou 1:1 | Recompor, não esticar; texto legível em tela pequena |
| In-stream e YouTube | 16:9 | Marca e mensagem cedo; estrutura ABCD (Atenção, Branding, Conexão, Direção) |
A Meta adapta assets por placement, mas o operador revisa a prévia de cada um. Confirme as especificações atuais da plataforma antes do export final.

## Recompor em vez de cortar
Grave ou gere com margem. Para cada proporção, reposicione o sujeito, reescreva a posição do texto na tela e confira a área segura. Quando não houver margem, use fundo estendido ou desfocado em vez de cortar rosto, produto ou texto.

## Legendas e acessibilidade
Legendas sincronizadas em todo vídeo · não depender só de cor · contraste mínimo 4,5:1 · sem texto pequeno · testar sem som · no máximo duas linhas por legenda.

## Textos do anúncio
| Campo | Regra |
|---|---|
| Texto principal | Primeira linha carrega o hook; aprovado pelo COPY |
| Título | Promessa ou benefício da página de destino |
| Descrição | Complemento opcional |
| CTA do botão | Coerente com a ação da página |

## Nomes de arquivo e anúncio
Padrão da base de tráfego: `ÂNGULO__HOOK__FORMATO__PERSONA__VERSÃO`, acrescido de `__PROPORÇÃO` no arquivo exportado. Exemplo: `ANG_MECANISMO__HOOK_PERGUNTA__UGC__MULHER40__V01__9x16.mp4`. Códigos em maiúsculas, sem acento, sem espaço.

## Manifesto de variações (colunas)
nome · angulo · hook · formato · persona · versao · proporcao · duracao_s · variavel_da_onda · controle (sim/não) · arquivo · texto_principal · titulo · cta · url_destino · status_qa · autorizacoes


=====
### ARQUIVO: references/criativos-04-literal.md
=====

# Criativos e Biblioteca Visual — templates literais (04)

## Entregáveis obrigatórios
1 Creative Card · 2 Swipe diagnóstico · 3 Matriz de conceitos (ângulo × hook × formato × prova) · 4 Roteiro/storyboard (cena, fala, texto, som, duração) · 5 Kit visual · 6 Ativo mestre · 7 Pacote de adaptações · 8 Checklist de QA e compliance · 9 Test Card · 10 Registro de aprendizado.

## Como usar o módulo
1 Escolha uma oferta real · 2 Abra o briefing do módulo 03 · 3 Pesquise referências com objetivo definido · 4 Selecione uma hipótese de ângulo e uma prova · 5 Estruture conceito, hook e formato · 6 Roteiro/storyboard · 7 Ativo mestre · 8 Derivações por canal (não redimensionamento automático) · 9 QA e compliance · 10 Pacote aprovado ao módulo 05.

## Ficha de decomposição de referência (swipe diagnóstico)
URL e data · país, idioma, canal · oferta e público aparente · estágio de consciência · ângulo · primeiro frame · hook verbal · texto na tela · formato e duração · corpo do argumento · mecanismo/prova · objeção tratada · CTA · elementos de produção · o que é observável · o que é só interpretação · hipótese reutilizável.
Pode reaproveitar: sequência narrativa; tipo de pergunta; categoria de hook; forma de demonstrar; lógica de prova; ritmo ou contraste; relação problema–CTA. Não copie: texto integral; identidade/personagem/rosto; cenas e composição reconhecíveis; depoimento ou resultado; logo, música, vídeo, PI; promessa que sua oferta não sustenta. Fontes: Meta Ad Library, TikTok Creative Center, YouTube ABCD, concorrentes, avaliações/comentários/calls/suporte.

## Formatos — funciona bem para / risco
UGC/creator-led — identificação, experiência / fingir espontaneidade · Talking head — autoridade, mecanismo, objeções / monólogo sem apoio · Demonstração — produto, interface, processo / mostrar sem explicar · Screen recording — SaaS, tutoriais / texto pequeno, dados sensíveis · Estático — uma ideia, contraste, oferta direta / excesso de texto · Carrossel — etapas, lista / primeiro cartão sem motivo · Testimonial/case — prova, objeções / resultado sem contexto ou permissão · Animação/motion — conceito abstrato, mecanismo, dados / estética que distrai.
Formatos registrados na base 06: UGC testemunhal + demonstração de objeto; UGC de alerta/sintoma + livro; unboxing demonstrativo; especialista para câmera + análise; professor para câmera; testemunho de ritual simples; testemunho religioso + oração; professor/storytelling longo; storytelling de figura pública; storytelling histórico com objeto; rotina noturna/UGC 10 min; storytelling de linhagem. Estrutura-padrão: hook → problema → explicação/mecanismo → prova ou autoridade → oferta → CTA.

## Lista de planos e plataformas
Plano principal; B-roll obrigatório; demonstração; closes de produto/interface; reações; tela final; captação de áudio; versões sem texto e sem música; autorizações de pessoas, locais e marcas. TikTok 9:16 ≥720p com safe zone; Shorts vertical social-first; YouTube ABCD (Atenção, Branding, Conexão, Direção); Meta adapta assets por placement. Adaptação: Reels/Stories 9:16 com área segura e legendas; feeds quadrado/vertical; in-stream 16:9; display múltiplas proporções. Acessibilidade: legendas sincronizadas, não depender só de cor, contraste 4,5:1, sem texto pequeno, testar sem som.

## Kit de identidade e prompt
Kit: marca; persona (idade aparente, traços, cabelo, pele, corpo, voz, roupa, papel); realismo (documental, creator, editorial, publicitário, 3D, ilustração); ambiente; câmera; luz; composição; continuidade; restrições.
Modelo: "Criar [tipo de asset] para [objetivo/placement]. Mostrar [persona com identidade fixa] realizando [ação] em [ambiente]. Composição [plano/posição/espaço], câmera [lente/ângulo], luz [descrição], paleta [cores], acabamento [realismo/estilo]. Manter [elementos de continuidade]. Evitar [restrições]."
Consistência: mesma referência de personagem; atributos bloqueados; uma dimensão por vez; ficha de lente/luz/paleta; imagem canônica antes das cenas; revisar mãos, texto, objetos, reflexos, anatomia, logos.
Pastas: 00_BRIEF · 01_REFERENCIAS · 02_ASSETS-MESTRE · 03_ROTEIROS · 04_EDICOES · 05_EXPORTS · 06_APROVADOS · 07_RESULTADOS.

## QA (marcar tudo)
Estratégica: [ ] corresponde ao Creative Card · [ ] consciência correta · [ ] uma mensagem · [ ] hook e corpo contínuos · [ ] prova corresponde ao claim · [ ] CTA combina com destino.
Visual/técnica: [ ] primeiro frame compreensível · [ ] texto legível no celular · [ ] legenda/voz/som revisados · [ ] resolução/proporção/duração · [ ] área segura · [ ] sem artefatos de IA · [ ] URL e tracking correspondem à versão · [ ] export assistido do início ao fim.
Factual: [ ] números com fonte · [ ] depoimentos genuínos e autorizados · [ ] demonstração representa uso real · [ ] comparação justa · [ ] urgência e escassez verdadeiras · [ ] limitações não escondidas.
Direitos: [ ] licenças (música, fonte, imagem, vídeo, template) · [ ] autorizações (voz, rosto, local, marca) · [ ] contrato de creator · [ ] dados pessoais ocultados · [ ] avatar não imita pessoa real · [ ] arquivo de autorização vinculado.

## Test Card criativo
Hipótese · Evidência de partida · Variável principal · Controle · Versões · Público/canal/placement · Janela e orçamento · Métrica principal · Métricas de guarda · Critério de decisão · Resultado · Aprendizado · Próximo teste.

## Briefing para 05 — Tráfego
ID e nome do criativo · versão da oferta · hipótese e variável · público e consciência · ângulo, hook, formato, duração · placement e arquivo · URL de destino · evento e métrica · controle e variantes · claims e restrições · janela, orçamento, regra de pausa · decisão esperada.

## Sprint de 10 dias
D1 Creative Card · D2 Swipe diagnóstico · D3 Matriz priorizada · D4 Seleção de execuções · D5 Plano de produção · D6–7 Ativos mestres · D8 Pacote por placement · D9 Aprovação documentada · D10 Test Card + briefing 05. Rubrica 0–2 × 10: 17–20 pronto para teste; 12–16 corrigir; 0–11 voltar ao briefing.

## Exemplo (clínicas) — três conceitos, uma onda
A Situação: hook visual "notificações acumulam em três telas", verbal "Quantos contatos ficam sem resposta porque ninguém sabe quem vem primeiro?", UGC + B-roll. B Objeção: "Automatizar triagem não significa automatizar a conversa", talking head + demo. C Demonstração: "Veja o que acontece nos primeiros 30 segundos após um novo contato", screen recording. Manter oferta, CTA e duração; variar só os três ângulos.


=====
### ARQUIVO: references/kit-visual-e-prompts.md
=====

# Kit visual, prompts e TRM LAB

Origem: 04 — Criativos e Biblioteca Visual (kit de identidade e prompt) e estrutura do TRM LAB CRIATIVOS.

## Kit de identidade
Marca · persona (idade aparente, traços, cabelo, pele, corpo, voz, roupa, papel no vídeo) · realismo (documental, creator, editorial, publicitário, 3D, ilustração) · ambiente · câmera · luz · composição · continuidade · restrições.

## Modelo de prompt da casa
"Criar [tipo de asset] para [objetivo/placement]. Mostrar [persona com identidade fixa] realizando [ação] em [ambiente]. Composição [plano/posição/espaço], câmera [lente/ângulo], luz [descrição], paleta [cores], acabamento [realismo/estilo]. Manter [elementos de continuidade]. Evitar [restrições]."
Para vídeo, acrescente: duração da tomada, movimento de câmera, ação do começo ao fim da tomada e o que não pode mudar entre tomadas.

## Consistência
Mesma referência de personagem em todas as cenas · atributos bloqueados · mudar uma dimensão por vez · ficha fixa de lente, luz e paleta · gerar a imagem canônica antes das cenas · revisar mãos, texto, objetos, reflexos, anatomia e logos.

## Limites para pessoas geradas por IA
- Não imita pessoa real, celebridade, médico ou influenciador identificável.
- Não se apresenta como cliente, paciente ou especialista, nem dá depoimento de resultado.
- Não mostra antes e depois corporal nem resultado de saúde.
- Sinalize conteúdo gerado ou alterado por IA quando a plataforma ou a lei exigir.

## TRM LAB como fonte de produção
- Pastas de "hooks" têm clipes de B-roll mudo de 3 a 12 s, organizados por tipo (identificação, prova social, segredo, transformação, quebra de padrão e outros). Use como abertura visual ou cobertura, sempre com a fala e o texto próprios.
- "TRM FORMATOS" tem exemplos numerados de formatos. Cite o número do formato no card para manter a linhagem.
- Liste pastas com `python3 agente-de-ads-trm/scripts/lab_listar.py <id-da-pasta>` e registre na lista de B-roll: pasta · arquivo · id · cena onde entra · segundos usados.
- Antes de usar clipe de terceiros do laboratório em anúncio pago, confirme origem e direito de uso. Sem confirmação, use só como referência de enquadramento.

## Pastas da produção
00_BRIEF · 01_REFERENCIAS · 02_ASSETS-MESTRE · 03_ROTEIROS · 04_EDICOES · 05_EXPORTS · 06_APROVADOS · 07_RESULTADOS.


=====
### ARQUIVO: references/qa-e-direitos.md
=====

# QA e direitos (marcar tudo por peça)

Origem: 04 — Criativos e Biblioteca Visual.

## Estratégica
- [ ] Corresponde ao Creative Card
- [ ] Consciência correta
- [ ] Uma mensagem
- [ ] Hook e corpo contínuos
- [ ] Prova corresponde ao claim
- [ ] CTA combina com o destino

## Visual e técnica
- [ ] Primeiro frame compreensível
- [ ] Texto legível no celular
- [ ] Legenda, voz e som revisados
- [ ] Resolução, proporção e duração corretas
- [ ] Área segura respeitada
- [ ] Sem artefatos de IA (mãos, texto, objetos, reflexos, anatomia, logos)
- [ ] URL e tracking correspondem à versão
- [ ] Export assistido do início ao fim

## Factual
- [ ] Números com fonte
- [ ] Depoimentos genuínos e autorizados
- [ ] Demonstração representa uso real
- [ ] Comparação justa
- [ ] Urgência e escassez verdadeiras
- [ ] Limitações não escondidas

## Direitos
- [ ] Licenças de música, fonte, imagem, vídeo e template
- [ ] Autorizações de voz, rosto, local e marca
- [ ] Contrato de creator
- [ ] Dados pessoais ocultados
- [ ] Avatar não imita pessoa real
- [ ] Arquivo de autorização vinculado

## Erros que mais geram retrabalho (04)
Abrir a ferramenta antes do briefing · confundir imagem bonita com criativo estratégico · copiar anúncio sem entender o princípio · testar ângulo, hook, formato e CTA ao mesmo tempo · usar personagem diferente em cada cena · adaptar 16:9 para 9:16 apenas cortando · colocar texto demais no primeiro frame · criar hook que o corpo não entrega · usar depoimento, resultado ou especialista fictício · ignorar licenças e autorizações · medir apenas CTR · não registrar versão, hipótese e resultado · escalar peça sem revisar a entrega da oferta · acumular exports sem nome e sem vínculo com testes.


=====
### ARQUIVO: references/roteiro-e-storyboard.md
=====

# Roteiro e storyboard

Origem: 04 — Criativos e Biblioteca Visual da Trip Angle (seções 1.2, 4.4, 5.1 e lista de planos).

## Estrutura-base de resposta direta
1 Hook: ganha atenção relevante · 2 Contexto: para quem e em qual situação · 3 Problema: organiza a tensão · 4 Mecanismo: explica causa ou solução · 5 Prova: reduz incerteza · 6 Oferta: apresenta o próximo caminho · 7 CTA: indica ação e consequência. "Um público muito consciente pode começar por oferta; um público consciente do problema pode precisar de contexto e mecanismo."

## Roteiro técnico (colunas obrigatórias)
| Tempo/cena | Imagem e ação | Fala/voz | Texto na tela | Som | Função |
|---|---|---|---|---|---|
| 0–3 s | | | | | Hook: atenção relevante |
| 3–10 s | | | | | Situação ou problema: identificação |
| 10–20 s | | | | | Mecanismo ou demo: compreensão |
| 20–27 s | | | | | Prova e oferta: reduzir dúvida |
| 27–30 s | | | | | Produto ou ação: CTA |
"Os tempos são um ponto de partida, não uma regra." Vídeos mais longos repetem o miolo (mecanismo e prova) sem mudar a mensagem.

## Regra da unidade
Um público dominante · uma situação principal · uma mensagem memorável · uma prova prioritária · um CTA principal. Várias cenas podem existir; argumentos concorrentes não.

## Checkpoints do roteiro
- Se o som for desligado, a abertura continua compreensível?
- Se o primeiro frame for removido, o restante cumpre o que ele prometeu?
- O hook usa as primeiras palavras e o primeiro visual para chamar a persona do card?
- O CTA diz a ação e o que acontece depois, igual à página de destino?

## Storyboard
Um quadro por linha do roteiro: número · tempo · enquadramento (plano geral, médio, close, detalhe, tela) · ação · texto na tela e posição · transição. Pode ser rascunho ou imagem gerada por IA a partir da imagem canônica.

## Lista de planos a captar ou gerar
Plano principal · B-roll obrigatório · demonstração · closes de produto ou interface · reações · tela final · captação de áudio · versões sem texto e sem música · autorizações de pessoas, locais e marcas.

## Formatos e risco comum
UGC/creator: fingir espontaneidade · Talking head: monólogo sem apoio visual · Demonstração: mostrar sem explicar · Screen recording: texto pequeno e dados expostos · Estático: excesso de texto · Carrossel: primeiro cartão sem motivo para avançar · Testimonial: resultado sem contexto ou permissão · Animação: estética que distrai.


=====
### ARQUIVO: assets/roteiro-modelo.csv
=====

```csv
inicio_s,fim_s,imagem_acao,fala,texto_tela,som,funcao
0,3,"[primeiro frame: persona na situação]","[hook falado]","[hook em texto curto]","[som ambiente]","Hook"
3,10,"[cena da situação ou problema]","[fala]","[texto]","[trilha]","Situação ou problema"
10,20,"[demonstração ou explicação do mecanismo]","[fala]","[texto]","[trilha]","Mecanismo"
20,27,"[prova disponível e oferta]","[fala]","[texto]","[trilha]","Prova e oferta"
27,30,"[tela final com ação]","[CTA falado]","[CTA em texto]","[trilha]","CTA"

```