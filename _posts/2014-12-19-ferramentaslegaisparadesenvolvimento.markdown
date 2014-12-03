---
layout:     post
title:      "Ferramentas legais para desenvolvimento WEB: JSFiddle"
titleToShare: "ferramentaslegaisparadesenvolvimento"
subtitle:   "JSFiddle, meu amigo zumbi (n&atilde;o, p&eacute;ra...)"
date:       2014-12-19 07:33:00
dateShort:  "2014-12-19"
author:     "Marcelo Palladino"
header-img: "img/post-bg-ferramentaslegaisparadesenvolvimento1.jpg"
tags:
- CSS3,
- Ferramentas,
- HTML,
- JavaScript,
- JSFiddle
---

<p>
    &Eacute; comum durante qualquer tipo de desenvolvimento de software a necessidade de testar rapidamente alguma ideia. No backend eu (quase sempre) costumo fazer uso de testes de unidade e integra&ccedil;&atilde;o para validar minhas solu&ccedil;&otilde;es em rela&ccedil;&atilde;o aos requisitos e guiar meu desenvolvimento.
</p>

<p>
    No front, dependendo do caso, tamb&eacute;m gosto de utilizar testes de unidade. Criando fun&ccedil;&otilde;es utilit&aacute;rias,
    classes e plugins jquery, por exemplo, um teste de unidade poupa um temp&atilde;o de idas e vindas no browser, al&eacute;m de tamb&eacute;m apoiar meu desenvolvimento. Algumas vezes, no entanto, tenho a necessidade de enxergar rapidamente alguma coisa enquanto ainda estou pensando em como resolver algo.
</p>

<p>Um dia destes tive que usar HTML e CSS3 para montar algo parecido com a figura abaixo em uma tabela de dados.</p>

<img src="{{ site.url }}/img/ferramentaslegaisparadesenvolvimento1-lista.png" alt="Lista" class="img-responsive center-block">

<p>
    O requisito ainda previa uma anima&ccedil;&atilde;o para as barras conforme determinada condi&ccedil;&atilde;o,
    ent&atilde;o eu tinha que ter uma forma r&aacute;pida de testar algumas coisas que pensava em fazer.
    Para estas ocasi&otilde;es tenho utilizado o JSFiddle (<a target="_blank" href="http://jsfiddle.net/">http://jsfiddle.net/</a>)
</p>

<img src="{{ site.url }}/img/ferramentaslegaisparadesenvolvimento1-jsfiddle.png" alt="P&aacute;gina do JSFiddle" class="img-responsive center-block">

<p>
    Este tipo de ferramenta &eacute; incr&iacute;vel, pois d&aacute; a change de testar rapidamente a marca&ccedil;&atilde;o HTML, o javascript e o CSS. Voc&ecirc; simplesmente escreve o c&oacute;digo no painel apropriado e manda rodar para visualizar o resultado. Simples e objetivo, sem a necessidade de criar projeto, executar em servidor local ou qualquer outra coisa do g&ecirc;nero. Bem &aacute;gil mesmo...
</p>

<p>
    O JSFiddle tem um suporte (bem) mais ou menos para zen coding, e permite carregar os mais recentes frameworks e recursos externos &quot;para dentro&quot; do seu fiddle.
</p>

<p>
    &Eacute; poss&iacute;vel escrever c&oacute;digo em coffeescript e SCSS, mas ele n&atilde;o suporta LESS e TypeScript, o que eu lamento muito. T&aacute;, eu sei que existem algumas gambiarras para &quot;usar&quot; LESS, mas n&atilde;o &eacute; uma parada legal pr&aacute; caramba de de ser feita.
</p>

<p>
    Tamb&eacute;m h&aacute; como validar o c&oacute;digo JS (JSHint), identar o c&oacute;digo (TidyUp) al&eacute;m de uma surpreendente possibilidade de colabora&ccedil;&atilde;o (collaboration), o que &eacute; &oacute;timo para quem est&aacute; pareando remotamente.
    Por fim, ainda h&aacute; a possibilidade de tornar seus fiddles p&uacute;blicos e forkar outros, no melhor estilo c&oacute;digo aberto.
</p>

<h2 class="section-heading">Um pouco de m&atilde;o na massa</h2>

<p>
    Ent&atilde;o &quot;b&oacute;ra&quot; l&aacute; fazer um teste r&aacute;pido no JSFiddle. No painel HTML, coloque o seguinte c&oacute;digo:
</p>

<p>CODE</p>
<p>

{% highlight html linenos %}
<span class="coolBar let-a"></span>  
<span class="coolBar let-b"></span>  
<span class="coolBar let-c"></span>  
{% endhighlight %}

</p>
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
    Perceba que eu usei o Jquery na parte de JavaScript. Sendo assim, &eacute; necess&aacute;rio configurar o fiddle para carreg&aacute;-lo. Isso &eacute; feito na parte de framework &amp; extensions. Agora &eacute; s&oacute; clicar em Run e ver o resultado...
</p>

<img src="{{ site.url }}/img/ferramentaslegaisparadesenvolvimento1-jsfiddle-run.png" alt="P&aacute;gina do JSFiddle mostrando resultado" class="img-responsive center-block">

<p>
    Este fiddle pode ser encontrado no seguinte endere&ccedil;o:
    <a target="_blank" href="http://jsfiddle.net/mfpalladino/2n5fhrzk/">http://jsfiddle.net/mfpalladino/2n5fhrzk/</a>.
</p>

<h2 class="section-heading">O que vem por a&iacute;?</h2>

<p>
Nos pr&oacute;ximos artigos vou dar sequ&ecirc;ncia falando sobre alternativas ao JSFiddle. Voc&ecirc; conhece alguma ferramenta obscura que gostaria de compartilhar e ver comentada aqui? Tem algum recurso do JSFiddle que voc&ecirc; utiliza, que &eacute; animal e que n&atilde;o foi comentado? Manda nos coment&aacute;rios e continuamos o papo l&aacute;.
</p>

<p>
At&eacute; mais!
</p>