# Modelos do AGENTE DE FUNIL TRM

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