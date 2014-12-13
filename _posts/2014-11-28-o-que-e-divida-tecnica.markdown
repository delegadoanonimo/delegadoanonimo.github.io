---
layout:     post
title:      "O que &eacute; d&iacute;vida t&eacute;cnica?"
titleToShare: "o-que-e-divida-tecnica"
subtitle:   "Devo, n&atilde;o nego..."
description: "Falando sobre D&iacute;vida T&eacute;cnica em desenvolvimento de software."
keywords: "C&oacute;digo ruim, D&iacute;vida t&eacute;cnica, Qualidade de software, Steve McConnell, Ward Cunnigham"
date:       2014-11-28 08:48:00
dateShort:  "2014-11-28"
author:     "Fabricio Panhan"
header-img: "img/2014-12/post-bg-o-que-e-divida-tecnica.jpg"
tags:
- C&oacute;digo ruim,
- D&iacute;vida t&eacute;cnica,
- Qualidade,
- Steve McConnell,
- Ward Cunnigham
---

<p>
    Fala a&iacute; escovadores de bits! Hoje &eacute; dia de Black Friday e esperamos ansiosos para gastar algumas dilmas, mas quando chega a fatura do cart&atilde;o de cr&eacute;dito come&ccedil;a o terror, agora imagine que voc&ecirc; precisa colocar uma funcionalidade emergencial no software. Voc&ecirc; tem duas maneiras de faz&ecirc;-la, a primeira &eacute; r&aacute;pida e &quot;meia boca&quot; onde voc&ecirc; tem certeza que um dia no futuro pode ocorrer algum problema. A outra maneira &eacute; voc&ecirc; planejar uma arquitetura limpa e concisa que pode perdurar durante a vida inteira do software, mas voc&ecirc; vai demorar al&eacute;m do prazo dado. E agora? Quando a fatura chegar ser&aacute; um terror?
</p>

<h2 class="section-heading">Explicando...</h2>

<p>
    Escolhendo a maneira r&aacute;pida, h&aacute; uma grande possibilidade de voc&ecirc; contrair
    uma d&iacute;vida t&eacute;cnica. D&iacute;vida t&eacute;cnica foi uma met&aacute;fora criada em
    1992 por Ward Cunnigham <a href="{{page.url}}#referencia01">[1]</a> que nos ajuda a pensar sobre esse dilema (qualidade vs. prazo)
    e alguns outros dilemas. Como uma d&iacute;vida financeira, a d&iacute;vida t&eacute;cnica incorre em
    pagamentos de juros, que v&ecirc;m sob a forma de esfor&ccedil;o extra que temos de fazer no
    desenvolvimento de software devido &agrave; escolha r&aacute;pida e &quot;meia boca&quot;.
    Podemos optar por continuar a pagar os juros, ou podemos pagar o montante total na
    refatora&ccedil;&atilde;o do c&oacute;digo &quot;meia boca&quot;. <a href="{{page.url}}#referencia02">[2]</a> &quot;Entregar um c&oacute;digo sem
    pensar muito &eacute; como entrar em uma d&iacute;vida. Um pouco de d&iacute;vida acelera o desenvolvimento,
    desde que ela seja paga prontamente com uma refatora&ccedil;&atilde;o. Alguns objetos fazem o custo
    desta opera&ccedil;&atilde;o toler&aacute;vel. O perigo ocorre quando a d&iacute;vida n&atilde;o &eacute; paga.
    A cada minuto gasto em c&oacute;digo n&atilde;o-muito-certo conta como juros sobre essa d&iacute;vida.&quot;
    (livre tradu&ccedil;&atilde;o) <a href="{{page.url}}#referencia03">[3]</a>
</p>

<p>
    Cunnigham prop&ocirc;s essa met&aacute;fora de maneira sutil, quase como uma provoca&ccedil;&atilde;o,
    mas com o passar dos anos ela foi gerando discuss&otilde;es, inclusive aqui com os delegados e hoje em dia a
    defini&ccedil;&atilde;o usada &eacute; de Carolyn Seaman e Yuepo Guo em seu artigo Mensuring and Monitoring
    Technical Debt. &ldquo;D&iacute;vida t&eacute;cnica &eacute; uma met&aacute;fora para artefatos imaturos,
    incompletos ou inadequados no ciclo de vida de desenvolvimento de software.&rdquo; <a href="{{page.url}}#referencia04">[4]</a>
</p>

<h2 class="section-heading">Classifica&ccedil;&atilde;o</h2>

<p>
    Segundo Steve McConnell <a href="{{page.url}}#referencia05">[5]</a>, um velho conhecido dos delegados,
    a d&iacute;vida pode ser classificada em dois tipos dependendo do modo em que s&atilde;o contra&iacute;das, estes tipos s&atilde;o: d&iacute;vida t&eacute;cnica sem inten&ccedil;&atilde;o e d&iacute;vida t&eacute;cnica intencional.
</p>

<h3 class="section-subheading">D&iacute;vida T&eacute;cnica sem inten&ccedil;&atilde;o</h3>

<p>
    Ocorre quando a d&amp;iacute;vida &amp;eacute; adquirida sem que o time perceba, ou seja, por algum descuido ou pela complexidade, alguns problemas s&amp;atilde;o introduzidos acidentalmente. Este tipo de d&amp;iacute;vida n&amp;atilde;o &amp;eacute; resultado de uma estrat&amp;eacute;gia, gerando assim, um impacto negativo.
</p>

<p>
    Alguns exemplos do surgimento desta d&iacute;vida s&atilde;o: &quot;O layout n&atilde;o funciona no IE 6.0&quot; (quem &eacute; o maluco que usa o IE 6?), &quot;C&oacute;digo ruim feito por desenvolvedor inexperiente&quot;, &quot;Um cliente pediu uma funcionalidade para o sistema, que n&atilde;o foi totalmente detalhada corretamente e quando a solu&ccedil;&atilde;o chega ao cliente n&atilde;o era exatamente o que ele esperava&quot;.
</p>

<h3 class="section-subheading">D&iacute;vida T&eacute;cnica intencional</h3>

<p>
    Ocorre quando a d&iacute;vida t&eacute;cnica a ser adquirida j&aacute; &eacute; conhecida e por algum motivo o time decide adquiri-la de maneira consciente. Isso pode ocorrer para uma entrega mais r&aacute;pida, deixando de lado os esfor&ccedil;os futuros. Este tipo de d&iacute;vida &eacute; resultado de uma estrat&eacute;gia.
</p>

<p>
Alguns exemplos s&atilde;o: &quot;Uma equipe n&atilde;o tem tempo suficiente para a entrega de uma solu&ccedil;&atilde;o definitiva, ent&atilde;o ela escreve um c&oacute;digo que mant&eacute;m as duas bases sincronizadas e as junta depois que essa vers&atilde;o for enviada.&quot;, &quot;Uma equipe faz um c&oacute;digo que resolve o problema, ent&atilde;o se opta por usar este c&oacute;digo e deixa para depois a sua refatora&ccedil;&atilde;o.&quot;
</p>

<h2 class="section-heading">Pagando a d&iacute;vida</h2>

<h3 class="section-subheading">D&iacute;vida T&eacute;cnica a curto prazo</h3>

<p>
Bem como uma d&iacute;vida comum a d&iacute;vida t&eacute;cnica pode ser paga num curto prazo e, geralmente, o pagamento deste tipo de d&iacute;vida t&eacute;cnica &eacute; feito para suprir as necessidades imediatas. Outra caracter&iacute;stica desse tipo de d&iacute;vida &eacute; que ela &eacute; paga com certa frequ&ecirc;ncia a fim de reabilitar o cr&eacute;dito para aquisi&ccedil;&atilde;o de novas d&iacute;vidas.
</p>

<h3 class="section-subheading">D&iacute;vida T&eacute;cnica a longo prazo</h3>

<p>
As d&iacute;vidas t&eacute;cnicas a longo prazo s&atilde;o adquiridas, em geral, de forma estrat&eacute;gica, com um planejamento a fim de suprir necessidades de grande valor de neg&oacute;cio, como por exemplo, o lan&ccedil;amento de um certo produto a fim de ganhar espa&ccedil;o no mercado, ou deixar de fazer os testes unit&aacute;rios, que no futuro precise ser paga.
</p>

<p>
Nos pr&oacute;ximos posts vamos discutir mais como identificar uma d&iacute;vida t&eacute;cnica e como criar indicadores para podermos planejar os nossos pagamentos.
</p>

<p>
N&atilde;o se esque&ccedil;am de comentar!
</p>

<div class="references">
    <small><b>Refer&ecirc;ncias</b></small>

    <ul>
        <li><a name="referencia01">[1]</a> Ward Cunningham's OOPSLA '92 Experience Report that first mentions technical debt. <a target="_blank" href="http://c2.com/doc/oopsla92.html">http://c2.com/doc/oopsla92.html</a></li> 
        <li><a name="referencia02">[2]</a> Technical Debt, Martin Fowler, 26 de fevereiro de 2009, <a target="_blank" href="http://martinfowler.com/bliki/TechnicalDebt.html">http://martinfowler.com/bliki/TechnicalDebt.html</a></li> 
        <li><a name="referencia03">[3]</a> V&iacute;deo de Ward Cunnigham sobre d&iacute;vida t&eacute;cnica, transcrito por June Kim e Lawrence Wang, postado em 22 de Janeiro de 2011, <a target="_blank" href="http://c2.com/cgi/wiki?WardExplainsDebtMetaphor">http://c2.com/cgi/wiki?WardExplainsDebtMetaphor</a></li> 
        <li><a name="referencia04">[4]</a> Measuring and Monitoring Technical Debt, Carolyn Seaman and Yuepu Guo, Advances in Computers, Vol. 82, 25-46, 2011</li> 
        <li><a name="referencia05">[5]</a> Technical Debt, Steve McConnell , <a target="_blank" href="http://www.construx.com/10x_Software_Development/Technical_Debt/">http://www.construx.com/10x_Software_Development/Technical_Debt/</a></li> 
    </ul>
</div>