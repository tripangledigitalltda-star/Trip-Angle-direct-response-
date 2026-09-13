# AGENTE DE ADS TRM

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
