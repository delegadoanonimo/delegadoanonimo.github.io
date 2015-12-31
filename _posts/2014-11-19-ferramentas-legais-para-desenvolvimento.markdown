---
layout:     post
title:      "Ferramentas legais para desenvolvimento WEB: JSFiddle"
titleToShare: "ferramentas-legais-para-desenvolvimento"
subtitle:   "JSFiddle, meu amigo zumbi (não, péra...)"
description: "Falando sobre ferramentas para desenvolvimento WEB e JSFiddle."
keywords: "JSFiddle, CSS3, Ferramentas para desenvolvimento, HTML5, HTML, JavaScript, JScript"
date:       2014-11-19 07:33:00
dateShort:  "2014-11-19"
author:     "Marcelo Palladino"
header-img: "img/2014-12/post-bg-ferramentaslegaisparadesenvolvimento1.jpg"
tags:
- CSS3
- HTML
- JavaScript
- Ferramentas
---

<p>
    É comum durante qualquer tipo de desenvolvimento de software a necessidade de testar rapidamente alguma ideia. No backend eu (quase sempre) costumo fazer uso de testes de unidade e integração para validar minhas soluções em relação aos requisitos e guiar meu desenvolvimento.
</p>

<p>
    No front, dependendo do caso, também gosto de utilizar testes de unidade. Criando funções utilitárias,
    classes e plugins jquery, por exemplo, um teste de unidade poupa um tempão de idas e vindas no browser, além de também apoiar meu desenvolvimento. Algumas vezes, no entanto, tenho a necessidade de enxergar rapidamente alguma coisa enquanto ainda estou pensando em como resolver algo.
</p>

<p>Um dia destes tive que usar HTML e CSS3 para montar algo parecido com a figura abaixo em uma tabela de dados.</p>

<img src="{{ site.url }}/img/2014-12/ferramentaslegaisparadesenvolvimento1-lista.png" alt="Lista" class="img-responsive center-block">

<p>
    O requisito ainda previa uma animação para as barras conforme determinada condição,
    então eu tinha que ter uma forma rápida de testar algumas coisas que pensava em fazer.
    Para estas ocasiões tenho utilizado o JSFiddle (<a target="_blank" href="http://jsfiddle.net/">http://jsfiddle.net/</a>)
</p>

<img src="{{ site.url }}/img/2014-12/ferramentaslegaisparadesenvolvimento1-jsfiddle.png" alt="Página do JSFiddle" class="img-responsive center-block">

<p>
    Este tipo de ferramenta é incrível, pois dá a change de testar rapidamente a marcação HTML, o javascript e o CSS. Você simplesmente escreve o código no painel apropriado e manda rodar para visualizar o resultado. Simples e objetivo, sem a necessidade de criar projeto, executar em servidor local ou qualquer outra coisa do gênero. Bem ágil mesmo...
</p>

<p>
    O JSFiddle tem um suporte (bem) mais ou menos para zen coding, e permite carregar os mais recentes frameworks e recursos externos 'para dentro' do seu fiddle.
</p>

<p>
    É possível escrever código em coffeescript e SCSS, mas ele não suporta LESS e TypeScript, o que eu lamento muito. Tá, eu sei que existem algumas gambiarras para 'usar' LESS, mas não é uma parada legal prá caramba de de ser feita.
</p>

<p>
    Também há como validar o código JS (JSHint), identar o código (TidyUp) além de uma surpreendente possibilidade de colaboração (collaboration), o que é ótimo para quem está pareando remotamente.
    Por fim, ainda há a possibilidade de tornar seus fiddles pÚblicos e forkar outros, no melhor estilo código aberto.
</p>

<h2 class="section-heading">Um pouco de mão na massa</h2>

<p>
    Então "bóra" lá fazer um teste rápido no JSFiddle. No painel HTML, coloque o seguinte código:
</p>

{% highlight html linenos %}
<span class="coolBar let-a"></span>  
<span class="coolBar let-b"></span>  
<span class="coolBar let-c"></span>  
{% endhighlight %}

<p>
    No painel de Javascript:
</p>

{% highlight javascript linenos %}
$('.let-a').width(100);
$('.let-b').width(130);
$('.let-c').width(160);
{% endhighlight %}

<p>
    No painel de CSS:
</p>

{% highlight css linenos %}
.coolBar {
    height: 20px;
    display: block;
    text-align: right;
    font-size: 14px;
    color: #FFF;
    margin-top:1px;
}
.coolBar:before {
    margin-right: 5px;
    margin-top: 3px;
    display: inline-block;
}
.coolBar:after {
    border-top: 10px solid transparent;
    border-bottom: 10px solid transparent;
    border-left: 14px solid transparent;
    height: 0;
    display: block;
    content: "";
    float: right;
    margin-right: -15px;
}
.coolBar.let-a {
    background: #017C35;
    width: 0;
    -webkit-transition: width .3s;
    -moz-transition: width .3s;
    -o-transition: width .3s;
    transition: width .3s;
}
.coolBar.let-a:before {
    content: "A";
}
.coolBar.let-a:after {
    border-left-color: #017C35;
}
.coolBar.let-b {
    background: #05AA34;
    width: 0;
    -webkit-transition: width .5s;
    -moz-transition: width .5s;
    -o-transition: width .5s;
    transition: width .5s;
}
.coolBar.let-b:before {
    content: "B";
}
.coolBar.let-b:after {
    border-left-color: #05AA34;
}
.coolBar.let-c {
    background: #99D013;
    width: 0;
    -webkit-transition: width .8s;
    -moz-transition: width .8s;
    -o-transition: width .8s;
    transition: width .8s;
}
.coolBar.let-c:before {
    content: "C";
}
.coolBar.let-c:after {
    border-left-color: #99D013;
}
{% endhighlight %}

<p>
    Perceba que eu usei o Jquery na parte de JavaScript. Sendo assim, é necessário configurar o fiddle para carregá-lo. Isso é feito na parte de framework & extensions. Agora é só clicar em Run e ver o resultado...
</p>

<img src="{{ site.url }}/img/2014-12/ferramentaslegaisparadesenvolvimento1-jsfiddle-run.png" alt="Página do JSFiddle mostrando resultado" class="img-responsive center-block">

<p>
    Este fiddle pode ser encontrado no seguinte endereço:
    <a target="_blank" href="http://jsfiddle.net/mfpalladino/2n5fhrzk/">http://jsfiddle.net/mfpalladino/2n5fhrzk/</a>.
</p>

<h2 class="section-heading">O que vem por aí?</h2>

<p>
Nos próximos artigos vou dar sequência falando sobre alternativas ao JSFiddle. Você conhece alguma ferramenta obscura que gostaria de compartilhar e ver comentada aqui? Tem algum recurso do JSFiddle que você utiliza, que é animal e que não foi comentado? Manda nos comentários e continuamos o papo lá.
</p>

<p>
Até mais!
</p>