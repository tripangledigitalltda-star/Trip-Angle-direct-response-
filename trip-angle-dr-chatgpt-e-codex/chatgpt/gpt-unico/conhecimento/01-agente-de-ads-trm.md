# AGENTE DE ADS TRM

Identificador: agente-de-ads-trm
Quando usar: AGENTE DE ADS TRM: pesquisa hooks, copys, formatos e temas virais na Biblioteca, TikTok, YouTube e fóruns, explica o viral e alimenta o TRM LAB. Use ao pedir referências de criativos.

=====
### ARQUIVO: SKILL.md (processo do agente)
=====


# AGENTE DE ADS TRM

Editor de criativos de direct response da Trip Angle.

Extensão da `agente-de-espionagem-trm` focada no criativo. A mineração acha e tria a oferta. Esta skill varre a web atrás de vídeos, cortes, hooks, copys, formatos e temas ligados à oferta e ao assunto dela, explica por que cada peça ganhou alcance, traduz isso em ângulos, hooks e formatos novos para direct response e registra tudo no **TRM LAB CRIATIVOS**. A produção final segue na `agente-de-producao-de-criativos-trm`.

Postura: editor profissional de DR. Para cada vídeo pergunta qual pessoa ele chama, qual tensão abre, qual crença pressupõe, por que as pessoas pararam e compartilharam, e como isso vira anúncio que leva à oferta.

## Regras

1. **Alcance não é conversão.** Views, curtidas e compartilhamentos medem atenção orgânica. Contagem de anúncios e longevidade medem circulação paga. Nenhum dos dois prova CTR, venda ou ROAS. Escreva "sinal de alcance" e "sinal de escala", nunca "vende".
2. **Número sempre com fonte e data.** Views, seguidores e datas mudam. Registre plataforma, URL, data e hora da captura. Número que não foi visto na página é NÃO MAPEADO, nunca estimado.
3. **Rótulos da casa em tudo:** FATO CONFIRMADO, ALEGAÇÃO DA COPY, OBSERVAÇÃO, INTERPRETAÇÃO ESTRATÉGICA, PADRÃO IDENTIFICADO, HIPÓTESE, NÃO MAPEADO NOS MATERIAIS.
4. **Referência é função, não arquivo para reproduzir.** Devolva princípio. Texto, rosto, cena, música, depoimento e promessa alheia não entram na peça própria.
5. **Claims sensíveis são risco.** Saúde, emagrecimento, renda, antes/depois, autopercepção negativa e urgência artificial entram na coluna de compliance, mesmo quando viralizaram.
6. **Acesso limpo.** Só conteúdo público. Não contorne login, CAPTCHA, paywall ou bloqueio. Baixar vídeo da web para transcrever exige aprovação do operador a cada lote.

## 0. Briefing mínimo

Confirme em uma linha cada: oferta (produto, mecanismo, promessa, persona) · assunto amplo que a oferta trata · países e idiomas da pesquisa · objetivo (novos ângulos, novos hooks, novos formatos, radar viral ou expansão de um criativo que já roda). Se vier da mineração, use o handoff dela. Não pergunte o que já está no handoff.

## 1. Consultar o TRM LAB antes de pesquisar

Leia `references/laboratorio-trm.md` e rode `scripts/lab_listar.py` para ver as pastas atuais. Anote os formatos, nichos e packs de hook que já existem para o assunto. A pesquisa busca o que **falta** no laboratório, e cada achado é comparado com o que já está lá: novo, variação de um formato existente ou repetido.

## 2. Pesquisa em toda a web

Siga o roteiro de `references/fontes-web.md`. Ordem padrão, ajustável ao objetivo:
1. **Biblioteca de Anúncios da Meta** no país da oferta e em mercados maiores do mesmo nicho. Mostra o que está sendo pago e há quanto tempo.
2. **TikTok** (busca, hashtags e Creative Center). Mostra o que viraliza organicamente e os anúncios de destaque.
3. **YouTube e Shorts**. Mostra temas perenes, views acumuladas e comentários.
4. **Instagram Reels, Kwai e Pinterest** quando o nicho vive lá.
5. **Fóruns e comunidades** (Reddit, grupos, Quora, fóruns de afiliados). Mostram a linguagem real e as dúvidas do público.
6. **Sites e bibliotecas de outros países**, com termos traduzidos e grafias locais. Mostram temas antes de chegarem ao Brasil.
7. **Google Trends e busca** para confirmar se o assunto está subindo.

Use termos da oferta, do assunto amplo, dos mecanismos e inimigos nomeados, das dores e dos apelidos que o público usa. Registre cada busca: termo, plataforma, país, data e o que rendeu.

## 3. Capturar cada vídeo relevante

Para cada peça que entrar na amostra, registre na ficha de `references/analise-de-criativos.md`, seção 2, mais os campos de alcance de `references/analise-viral.md`: plataforma, URL, criador, seguidores, data de publicação, views, curtidas, comentários, compartilhamentos, salvamentos quando visíveis, duração, som usado.

**Copy do vídeo:** texto na tela e legendas literais, legenda do post e, quando houver, transcrição. A transcrição pode vir de legenda automática da plataforma, de transcrição fornecida pelo operador ou de transcrição local com Whisper sobre arquivo que o operador aprovou baixar, ou que já está no TRM LAB. Registre a origem e a confiança. Fala sem nenhuma dessas fontes é NÃO MAPEADO.

**Comentários:** leia os mais curtidos. Eles mostram o que o público entendeu, contestou e repetiu, e são a melhor fonte de linguagem para hooks novos.

## 4. Decompor o criativo

Com as taxonomias da casa em `references/analise-de-criativos.md`: hook (tipo, persona, crença pressuposta, promessa implícita, próximo bloco), ângulo (família e elementos enfatizados), formato (tipo e elementos de produção), estrutura (ordem e tempos dos blocos), prova (nível na hierarquia). Para anúncios pagos, feche com mecanismo narrado × entregue, continuidade até o destino e prova × claim.

## 5. Explicar por que viralizou

Aplique a leitura de `references/analise-viral.md` a cada peça com alcance fora da curva:
- **Normalize o número:** views em relação aos seguidores do perfil e à mediana de views do próprio perfil, taxa de comentário e de compartilhamento, velocidade desde a publicação.
- **Decomponha a causa provável** nos gatilhos observáveis: tensão do hook, identificação, novidade ou contraste, polêmica, utilidade salvável, prova visual, formato nativo, som em alta, momento do assunto.
- **Separe o que é do criador do que é do formato.** Um perfil grande viraliza por audiência; um perfil pequeno fora da curva indica força do formato ou do tema. Só o segundo é transferível com segurança.
- **Traduza para DR:** qual ponte liga esse tema ou formato ao problema, ao mecanismo e à oferta. Viral sem ponte para a oferta é repertório, não criativo de venda.

Tudo nesta seção é INTERPRETAÇÃO ESTRATÉGICA ou HIPÓTESE. Viralização não tem causa confirmável de fora.

## 6. Famílias e radar de temas

Agrupe peças em clone, variação ou ângulo novo. Ângulo novo exige mudança de desejo, problema, mecanismo, promessa, persona ou prova; trocar apresentador ou cenário é variação.

Rode `scripts/radar_temas.py` sobre os textos coletados e consolide em `references/radar-de-temas.md`. Cada tema recebe classe (emergente, em alta, perene, isolado), plataformas onde aparece, sinais de alcance e de escala, hooks que o carregam e risco de compliance. Não infira saturação pelo volume.

## 7. Editar: expansão criativa

Com `references/editor-de-expansao.md`:
1. **Por referência:** o que preservar como princípio, o que substituir, o que não reutilizar.
2. **Banco de hooks novos:** hooks próprios escritos a partir dos padrões e da linguagem dos comentários, cada um com tipo, persona, crença e a referência que o inspirou.
3. **Matriz de conceitos:** ângulo × hook visual × hook verbal × formato × prova × CTA, uma perspectiva por linha, marcando o que é novo para o TRM LAB.
4. **Ondas de teste:** ângulo, hook, formato, corpo/prova, CTA, uma variável por onda.
5. **Creative Cards** das linhas priorizadas para a `agente-de-producao-de-criativos-trm`.

Toda proposta é HIPÓTESE com evidência de partida. Proposta que dependa de prova que a oferta não tem fica bloqueada, com a prova necessária.

## 8. Alimentar o TRM LAB

Gere a planilha de registro no esquema de `references/laboratorio-trm.md`: uma linha por referência, nome no padrão `PAIS__NICHO__ANGULO__HOOK__FORMATO__ANUNCIANTE__AAAAMMDD`, classificação novo/variação/repetido e pasta de destino sugerida. Formato inédito recebe o próximo número livre da série de formatos. A skill não sobe arquivos no Drive: entrega a planilha e a lista de pastas para o operador aprovar e mover.

## 9. Entregar

Modelo em `references/relatorio-criativos.md`: resumo do editor → radar de temas → top referências com alcance e por que viralizou → famílias e fichas → padrões de hook, ângulo, formato e copy → banco de hooks novos → matriz e ondas → Creative Cards → riscos de compliance → registro para o TRM LAB → limites.

## Erros que invalidam a análise

Tratar views como venda · comparar views de perfis de tamanhos muito diferentes sem normalizar · creditar ao formato o que é audiência do criador · estimar número que não foi visto · reconstruir fala sem fonte · classificar hook só como "curioso" · confundir tema com ângulo · contar clones como ideias diferentes · trazer viral sem ponte para a oferta · copiar fala, cena ou promessa alheia · inferir saturação pelo volume · matriz que muda várias variáveis ao mesmo tempo · subir arquivo no Drive sem aprovação.

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
### ARQUIVO: references/analise-viral.md
=====

# Análise de alcance e viralização

Origem: a separação entre sinal e performance, os rótulos e as fichas de hook, ângulo, formato e prova vêm da Trip Angle. A normalização de números e os gatilhos de viralização abaixo são **regra operacional derivada**, não estão no Notion. Tudo nesta leitura é INTERPRETAÇÃO ESTRATÉGICA ou HIPÓTESE, porque a causa de um viral não é confirmável de fora.

## 1. Campos de alcance (capturar só o que está visível)
Plataforma · URL · criador · seguidores ou inscritos · data de publicação · data e hora da captura · views · curtidas · comentários · compartilhamentos · salvamentos · duração · som ou música · pago ou orgânico (se declarado).

## 2. Normalização

| Indicador | Cálculo | Leitura |
|---|---|---|
| Multiplicador de audiência | views ÷ seguidores | Acima de 1 indica alcance além da própria base |
| Fora da curva do perfil | views ÷ mediana de views dos últimos 10 a 20 vídeos do mesmo perfil | Acima de 3 sugere que o vídeo, e não o perfil, puxou o alcance |
| Taxa de conversa | comentários ÷ views | Alta indica polêmica, dúvida ou identificação forte |
| Taxa de compartilhamento | compartilhamentos ÷ views | Alta indica conteúdo que as pessoas usam para falar com outras |
| Taxa de salvamento | salvamentos ÷ views | Alta indica utilidade, receita, lista ou passo a passo |
| Velocidade | views ÷ dias desde a publicação | Diferencia pico recente de acúmulo lento |

Cortes de 1 e 3 são pontos de partida ajustáveis. Compare sempre dentro da mesma plataforma. Perfis gigantes com vídeo na média do perfil não entram como referência de formato.

## 3. Por que viralizou: gatilhos a verificar
Marque os presentes, com a evidência de onde aparecem (segundo do vídeo, texto, comentário):
- **Tensão no hook:** conflito, erro, alerta ou pergunta que exige resposta nos primeiros segundos.
- **Identificação:** situação específica que o público reconhece como sua; comentários do tipo "sou eu".
- **Novidade ou contraste:** informação que contradiz a crença comum ou nomeia um inimigo novo.
- **Polêmica:** comentários divididos, correções, discordância.
- **Utilidade salvável:** receita, lista, passo a passo, antes de fazer X.
- **Prova visual:** demonstração, resultado ou processo mostrado na tela.
- **Formato nativo:** cara de conteúdo da plataforma, não de anúncio.
- **Som ou tendência:** áudio, meme ou formato em alta no período.
- **Momento do assunto:** notícia, estação, lançamento ou pico no Google Trends.
- **Autoridade ou personagem:** especialista, figura pública ou persona forte.

Conclusão em uma frase: "Hipótese: alcançou [indicador] principalmente por [gatilho 1] e [gatilho 2], observável em [evidência]."

## 4. Criador ou formato
| Situação | Conclusão |
|---|---|
| Perfil grande, vídeo na média do perfil | Alcance é da audiência; não é referência de formato |
| Perfil grande, vídeo muito acima da mediana | Tema ou formato puxou; referência válida com ressalva |
| Perfil pequeno, vídeo muito acima da mediana e dos seguidores | Sinal forte de tema ou formato transferível |
| Mesmo formato fora da curva em vários perfis pequenos | PADRÃO IDENTIFICADO de formato |

## 5. Ponte para direct response
Para cada viral que entrar no plano, responda:
1. Qual problema ou desejo da persona da oferta o tema toca?
2. Qual crença do vídeo prepara o mecanismo da oferta?
3. Onde o anúncio sai do conteúdo e entra na oferta sem quebrar a promessa?
4. Qual prova a oferta tem para sustentar o que o vídeo sugere?
Sem resposta para 1 e 3, o viral fica como repertório e não vira linha na matriz.

## 6. Erros
Tratar views como venda · comparar perfis de tamanho diferente sem normalizar · creditar ao formato o alcance do criador · ignorar impulsionamento pago · concluir causa sem evidência na peça ou nos comentários · trazer viral sem ponte para a oferta.


=====
### ARQUIVO: references/editor-de-expansao.md
=====

# Editor de expansão criativa

Origem: "04 — Criativos e Biblioteca Visual" (seções 1.1, 1.2, 4.1, 4.4, 5.1, 9.1, 9.2, 9.3, rubrica) e "Mineração Avançada — Meta Ads" (campos de auditoria). Campos literais salvo indicação.

## 1. Decisão por referência

Para cada criativo analisado, feche com os campos da auditoria da Mineração Avançada:

| Campo | Pergunta |
|---|---|
| O que preservar | Qual função persuasiva vale como princípio? (sequência narrativa, tipo de pergunta, categoria de hook, forma de demonstrar, lógica de prova, ritmo ou contraste, relação problema → CTA) |
| O que substituir | Forma, identidade, prova e claim que precisam ser próprios |
| O que não reutilizar | Texto, rosto, cena, depoimento, resultado, música, promessa que a oferta não sustenta |
| Gap promessa/entrega | O que o anúncio promete e o destino não entrega |
| Risco de compliance | Claims sensíveis presentes |
| Próximo teste | Hipótese que esta referência sugere |

## 2. Camadas (não confundir)

Ângulo (perspectiva estratégica) · Hook (primeiro estímulo) · Conceito (ideia central que une mensagem e representação) · Formato (recipiente narrativo) · Execução (peça concreta) · Variação (mudança controlada para aprender sobre uma variável).

## 3. Matriz de conceitos (04, 4.1)

| Ângulo | Hook visual | Hook verbal | Formato | Prova | CTA | Tema de origem | Evidência (IDs) |
|---|---|---|---|---|---|---|---|
| Uma perspectiva por linha | Primeiro frame | Primeira frase | UGC, demo, estático etc. | O que aparece | Próxima ação | Do radar | Referências que sustentam |

Regra da unidade: "Um público dominante. Uma situação principal. Uma mensagem memorável. Uma prova prioritária. Um CTA principal." Hook deve comprar atenção para a mensagem: "Curiosidade sem relação com o corpo cria ruptura e pode atrair clique sem fit."

## 4. Estrutura-base e roteiro (04, 4.4 e 5.1)

Hook → Contexto → Problema → Mecanismo → Prova → Oferta → CTA, adaptada ao estágio de consciência ("Um público muito consciente pode começar por oferta").

| Tempo | Função |
|---|---|
| 0–3 s | Hook: atenção relevante |
| 3–10 s | Situação ou problema: identificação |
| 10–20 s | Mecanismo ou demo: compreensão |
| 20–27 s | Prova e oferta: reduzir dúvida |
| 27–30 s | CTA: direção |

"Os tempos são um ponto de partida, não uma regra." Colunas do roteiro técnico: tempo/cena · imagem e ação · fala/voz · texto na tela · som · função.

## 5. Teste em ondas (04, 9.2)

| Onda | O que varia | O que permanece | Aprendizado |
|---|---|---|---|
| 1. Ângulo | Perspectiva central | Formato, oferta, prova e CTA | Qual problema ou oportunidade gera relevância |
| 2. Hook | Primeiro frame/frase | Ângulo, corpo e CTA | Qual entrada conquista atenção qualificada |
| 3. Formato | UGC, demo, estático etc. | Argumento e prova | Qual representação facilita compreensão |
| 4. Corpo/prova | Explicação ou evidência | Hook e CTA | O que reduz incerteza |
| 5. CTA | Próxima ação | Mensagem e oferta | Qual pedido é proporcional à consciência |

Variáveis possíveis de uma matriz: ângulo, hook, conceito, persona, formato, corpo, prova, CTA, duração, edição. Nunca "testar ângulo, hook, formato e CTA ao mesmo tempo".

## 6. Creative Card para a produção (04, 1.1)

Projeto e versão da oferta · Público + situação · Estágio de consciência · Objetivo (parar, educar, demonstrar, qualificar ou converter) · Mensagem única · Ângulo · Prova · Objeção · CTA · Canal e placement · Restrições (claims, imagens, palavras, direitos) · Métrica. Preencha um card por linha priorizada da matriz e entregue à `agente-de-producao-de-criativos-trm`.

Test Card criativo (04, 9.3): hipótese · evidência de partida · variável principal · controle · versões · público/canal/placement · janela e orçamento · métrica principal · métricas de guarda · critério de decisão · resultado · aprendizado · próximo teste.

## 7. Rubrica de prontidão da proposta (04; 0 ausente, 1 parcial, 2 claro e validado)

Creative Card completo · ângulo ligado a uma evidência · uma mensagem e um CTA · hook contínuo com o corpo · prova compatível com o claim · roteiro utilizável · identidade e arquivos organizados · versões adaptadas aos placements · QA, direitos e compliance aprovados · teste com decisão definida. 17–20 pronto para teste controlado; 12–16 corrigir pontos fracos; 0–11 voltar ao briefing e à hipótese.

## 8. Checkpoints do editor (04)

"Se o som for desligado, a abertura continua compreensível? Se o primeiro frame for removido, o restante ainda cumpre o que ele prometeu?" "A prova sustenta exatamente o claim — ou apenas parece impressionante?" "A nova peça mantém o princípio, mas possui mensagem, evidência, assets e expressão próprios?"


=====
### ARQUIVO: references/fontes-web.md
=====

# Roteiro de pesquisa na web

Regra de acesso: só conteúdo público, sem login forçado, CAPTCHA, paywall ou burla de bloqueio. Use navegador quando a página for dinâmica; busca e fetch para páginas estáticas. Baixar vídeo exige aprovação do operador.

## Registro de cada busca
| Plataforma | País/idioma | Termo | Filtro/ordenação | Data e hora | Resultados úteis (URLs) | Vizinhos descobertos |

## Termos
Monte quatro grupos e combine: **oferta** (nome do mecanismo, promessa, produto) · **assunto amplo** (o tema de que a oferta trata) · **dor e desejo na voz do público** (frases de comentários e fóruns) · **apelidos e grafias** (sem acento, gírias, ofuscação, tradução local). Em outros países, traduza o mecanismo e a dor, não o nome comercial.

## Fontes

| Fonte | Como pesquisar | O que capturar | O que ela mostra |
|---|---|---|---|
| Biblioteca de Anúncios da Meta | País fixo, ativos, busca por frase exata e por anunciante; repetir em US, MX, ES, CO, PT e mercados grandes do nicho | ID, anunciante, início, contagem por criativo, duração, texto, destino | Circulação paga e longevidade; não mostra views nem resultado |
| TikTok busca e hashtags | Termos e hashtags do assunto; abrir os vídeos com mais views e os recentes | URL, criador, seguidores, data, views, curtidas, comentários, compartilhamentos, salvamentos, som, legenda, comentários mais curtidos | Alcance orgânico e linguagem do público |
| TikTok Creative Center | Top Ads por setor e país, Trends (hashtags, sons, criadores) | Anúncio, setor, país, métricas que a própria página exibe, período | Anúncios e tendências destacados pela plataforma; usar só o que a página mostra |
| YouTube e Shorts | Busca ordenada por relevância e por contagem de visualizações; filtro de data | URL, canal, inscritos, data, views, curtidas, comentários, duração, título, thumbnail, capítulos, legenda automática | Temas perenes e vídeos longos que explicam mecanismo |
| Instagram Reels, Kwai, Pinterest | Busca por termo e hashtag quando acessível sem login | Os mesmos campos de alcance visíveis | Formatos nativos do nicho |
| Reddit, Quora, grupos e fóruns de afiliados | Termo + "reddit", subreddits do nicho, threads mais votadas | Título, votos, comentários, frases literais, objeções, perguntas | Voz real do público, dúvidas e polêmicas; não é ranking |
| Sites e blogs de outros países | Busca no idioma local pelo mecanismo e pela dor | URL, país, data, título, argumento | Temas antes de chegarem ao mercado local |
| Google Trends | Termo e variações, país e últimos 12 meses e 90 dias | Curva, pico, consultas relacionadas em alta | Se o assunto está subindo |

## Cobertura mínima por rodada (ajustável)
Três fontes diferentes, pelo menos uma paga (Biblioteca ou Creative Center) e uma orgânica (TikTok ou YouTube), mais uma de voz do público (comentários ou fórum). Anote quando uma fonte não pôde ser acessada e por quê.

## Limites por fonte
Views e curtidas podem ser infladas ou incluir impulsionamento pago não declarado. Creative Center e Biblioteca mostram recortes da própria plataforma. Fórum dá sinal qualitativo, não representatividade. Métrica que exige login ou ferramenta paga fica NÃO MAPEADO, a menos que o operador forneça.


=====
### ARQUIVO: references/laboratorio-trm.md
=====

# TRM LAB CRIATIVOS: base e registro

Pasta pública do Google Drive "🔺TRM LAB CRIATIVOS 🧪", id `1zvNYizDu7PcgIrRgGm7RDsKP-N88-bBK`. É o banco de referências do operador. A skill consulta antes de pesquisar e entrega registros novos para ele.

## Acesso
- O conector do Google Drive pode não listar as pastas, porque a pasta é de outro dono.
- Listagem: `scripts/lab_listar.py <id>` lê `https://drive.google.com/embeddedfolderview?id=<id>` e devolve nome e id de cada item. Rode por subpasta quando precisar descer.
- Download de arquivo: `https://drive.google.com/uc?export=download&id=<id>`, só quando for transcrever ou revisar uma peça.

## Estrutura observada em 11/09/2026 (confirmar com a listagem)
- 87 pastas e 1.201 arquivos.
- 25 pastas de nicho.
- 10 pastas de "hooks" com 628 clipes de B-roll mudo de 3 a 12 s, em packs d, h, i, m, n e R. São aberturas visuais, não hooks verbais.
- "TRM FORMATOS" com 50 subpastas numeradas. O formato 1, Caixinha de perguntas, está na pasta sem nome "gr". Vários exemplos vêm dos anúncios do produto "50 formatos orgânicos".
- Expansão planejada em 11/09/2026: formatos novos numerados a partir do 51, ângulos e hooks novos, novos nichos e fontes.

## Convenção de nome
`PAIS__NICHO__ANGULO__HOOK__FORMATO__ANUNCIANTE__AAAAMMDD`
Use códigos curtos sem acento e sem espaço dentro de cada campo. Exemplo: `BR__EMAGRECIMENTO__MECANISMO__PERGUNTA__TALKINGHEAD__criadorx__20260912`.

## Classificação do achado frente ao laboratório
- **Novo:** formato, ângulo ou hook que não existe em nenhuma pasta. Formato novo recebe o próximo número livre da série.
- **Variação:** execução diferente de um formato ou ângulo que já existe. Aponte o número ou a pasta de origem.
- **Repetido:** já coberto. Registre só se trouxer alcance ou nicho novo.

## Esquema da planilha de registro (uma linha por referência)
id_registro · nome_padrao · classificacao (novo, variação, repetido) · pasta_destino_sugerida · numero_formato · plataforma · url · pais · idioma · nicho · oferta_relacionada · criador_ou_anunciante · seguidores · data_publicacao · data_captura · views · curtidas · comentarios · compartilhamentos · salvamentos · contagem_anuncios · inicio_anuncio · duracao · formato · hook_tipo · hook_texto_literal · angulo_familia · tema · classe_tema · copy_resumo · gatilhos_virais · multiplicador_audiencia · fora_da_curva · ponte_para_oferta · o_que_preservar · o_que_nao_reutilizar · risco_compliance · origem_transcricao · rotulo_evidencia · observacoes

Entregue em CSV ou XLSX. A skill não sobe nem move arquivos no Drive: o operador aprova a lista e faz a movimentação.


=====
### ARQUIVO: references/radar-de-temas.md
=====

# Radar de temas em alta

Origem: regras de sinal de escala e de leitura da Trip Angle ("Mineração Avançada — Meta Ads", "Arsenal de Mineração — DR & Quiz-First", "Frameworks para Aplicação", seção 7). Os cortes numéricos abaixo são **regra operacional derivada**, não estão no Notion; o operador pode ajustá-los por nicho.

## O que conta como tema

Um tema é uma ideia de conteúdo que se repete em peças diferentes: mecanismo nomeado ("pâncreas hiperativo"), inimigo nomeado, promessa com prazo ("7 dias"), situação ou persona declarada ("mulher +40"), apelido de produto ("de pobre", "natural"), ativo concreto ("plano imprimível") ou formato recorrente (médico em talking head, receita em demonstração). Tema não é ângulo: o mesmo tema pode ser trabalhado por ângulo de mecanismo, de prova ou de objeção.

## Sinais observáveis

| Sinal | Como medir | O que indica |
|---|---|---|
| Difusão | Número de anunciantes independentes com o tema na mesma janela | Tema em circulação no mercado |
| Recência | Data de início dos cartões com o tema | Entrada recente de anunciantes |
| Concentração | Soma de "N anúncios usam esse criativo" dos cartões com o tema | Investimento observável de produção e veiculação |
| Persistência | Anúncios com o tema ativos há muito tempo | Continuidade |

Nenhum sinal mede resultado. "a heurística 'longa duração + impressões altas' é apenas sinal de possível durabilidade quando esses dados estiverem disponíveis." "Sofisticação e concorrência: não inferir estágio pelo volume."

## Classificação (cortes derivados, ajustáveis)

| Classe | Critério |
|---|---|
| **Emergente** | Pelo menos 2 anunciantes independentes, com a maioria dos cartões iniciados nos últimos 14 dias |
| **Em alta** | Pelo menos 3 anunciantes independentes, cartões iniciados nos últimos 30 dias e concentração acima da mediana da amostra |
| **Perene** | Pelo menos 2 anunciantes com cartões ativos há mais de 60 dias |
| **Isolado** | Um anunciante só; registrar como caso, não como tema |

Clones contam como um anunciante só para difusão: mesma copy em páginas diferentes é PADRÃO IDENTIFICADO, não prova de difusão independente.

## Registro por tema

| Tema | Tipo (mecanismo, inimigo, promessa, persona, prazo, formato) | Classe | Anunciantes | IDs | Início mais antigo e mais recente | Soma de contagem | Hook que mais o carrega | Formato dominante | Risco de compliance | Rótulo |

## Limites

A Biblioteca mostra só anúncios ativos e a amostra carregada na busca. Contagens e datas mudam; preserve a data da observação. O radar diz o que está em circulação, nunca o que performa.


=====
### ARQUIVO: references/relatorio-criativos.md
=====

# Modelo de relatório do editor de criativos

Cabeçalho: nicho ou oferta · país e idioma · janela (ativos) · data e hora da coleta · entrada usada (oferta minerada, termo ou anúncios enviados) · tamanho da amostra (cartões lidos, Ads analisados, anunciantes).

## 1. Resumo do editor
Três a cinco frases: quantas ideias distintas existem (famílias, não vídeos), quais temas estão em circulação, qual formato e hook dominam, e qual é a primeira onda de teste recomendada. Aviso fixo: "Sinal de escala e circulação não é prova de CTR, venda ou ROAS."

## 2. Radar de temas
Tabela de `radar-de-temas.md`, ordenada por classe (em alta, emergente, perene) e depois por difusão.

## 2b. Top referências com alcance
| Plataforma | URL | Criador e seguidores | Data | Views | Multiplicador | Fora da curva | Gatilhos | Por que alcançou (hipótese) | Ponte para a oferta |
Só o que foi visto na página, com data da captura. Ver `analise-viral.md`.

## 3. Famílias e fichas de criativo
Para cada família: nome funcional · classificação (clone, variação, ângulo novo) · anunciantes e IDs · execuções. Dentro dela, uma ficha por Ad analisado (`analise-de-criativos.md`, seção 2), com observado e interpretação separados e as três comparações.

## 4. Padrões
| Dimensão | Padrão identificado | Anunciantes | IDs | Rótulo |
Hooks (tipos e aberturas recorrentes), ângulos (famílias recorrentes), formatos e durações, estruturas (ordem dos blocos e tempos), provas (nível da hierarquia mais usado). Só entra padrão visto em mais de um anunciante.

## 4b. Banco de hooks novos
| Hook próprio | Tipo | Persona | Crença pressuposta | Promessa implícita | Referência de origem | Novo no TRM LAB? |

## 5. Plano de expansão
Decisão por referência (preservar, substituir, não reutilizar) · matriz de conceitos · ordem de ondas · Creative Cards das linhas priorizadas · propostas bloqueadas por falta de prova.

## 6. Riscos de compliance
Claim, onde aparece (ID, tempo), tipo de risco, o que fazer na versão própria.

## 6b. Registro para o TRM LAB
Planilha no esquema de `laboratorio-trm.md`, com classificação novo, variação ou repetido e pasta de destino sugerida.

## 7. Limites da análise
Amostra não exaustiva · fontes que não puderam ser acessadas · métricas que exigem login · áudio não legendado e trechos não assistidos (NÃO MAPEADO) · transcrições geradas e sua confiança · destinos não abertos · contagens e datas mudam · nenhuma métrica de performance disponível.
