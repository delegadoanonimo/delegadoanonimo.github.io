---
layout:     post
title:      "O que é dívida técnica?"
titleToShare: "o-que-e-divida-tecnica"
subtitle:   "Devo, não nego..."
description: "Falando sobre Dívida Técnica em desenvolvimento de software."
keywords: "Código ruim, Dívida técnica, Qualidade de software, Steve McConnell, Ward Cunnigham"
date:       2014-11-28 08:48:00
dateShort:  "2014-11-28"
author:     "Fabricio Panhan"
header-img: "img/2014-12/post-bg-o-que-e-divida-tecnica.jpg"
tags:
- Qualidade de software
- Clean code
---

<p>
    Fala aí escovadores de bits! Hoje é dia de Black Friday e esperamos ansiosos para gastar algumas dilmas, mas quando chega a fatura do cartão de crédito começa o terror, agora imagine que você precisa colocar uma funcionalidade emergencial no software. Você tem duas maneiras de faz&ecirc;-la, a primeira é rápida e "meia boca" onde você tem certeza que um dia no futuro pode ocorrer algum problema. A outra maneira é você planejar uma arquitetura limpa e concisa que pode perdurar durante a vida inteira do software, mas você vai demorar além do prazo dado. E agora? Quando a fatura chegar será um terror?
</p>

<h2 class="section-heading">Explicando...</h2>

<p>
    Escolhendo a maneira rápida, há uma grande possibilidade de você contrair
    uma dívida técnica. Dívida técnica foi uma metáfora criada em
    1992 por Ward Cunnigham <a href="{{page.url}}#referencia01">[1]</a> que nos ajuda a pensar sobre esse dilema (qualidade vs. prazo)
    e alguns outros dilemas. Como uma dívida financeira, a dívida técnica incorre em
    pagamentos de juros, que vêm sob a forma de esforço extra que temos de fazer no
    desenvolvimento de software devido à escolha rápida e "meia boca".
    Podemos optar por continuar a pagar os juros, ou podemos pagar o montante total na
    refatoração do código "meia boca". <a href="{{page.url}}#referencia02">[2]</a> "Entregar um código sem
    pensar muito é como entrar em uma dívida. Um pouco de dívida acelera o desenvolvimento,
    desde que ela seja paga prontamente com uma refatoração. Alguns objetos fazem o custo
    desta operação tolerável. O perigo ocorre quando a dívida não é paga.
    A cada minuto gasto em código não-muito-certo conta como juros sobre essa dívida."
    (livre tradução) <a href="{{page.url}}#referencia03">[3]</a>
</p>

<p>
    Cunnigham propôs essa metáfora de maneira sutil, quase como uma provocação,
    mas com o passar dos anos ela foi gerando discussões, inclusive aqui com os delegados e hoje em dia a
    definição usada é de Carolyn Seaman e Yuepo Guo em seu artigo Mensuring and Monitoring
    Technical Debt. 'Dívida técnica é uma metáfora para artefatos imaturos,
    incompletos ou inadequados no ciclo de vida de desenvolvimento de software.' <a href="{{page.url}}#referencia04">[4]</a>
</p>

<h2 class="section-heading">Classificação</h2>

<p>
    Segundo Steve McConnell <a href="{{page.url}}#referencia05">[5]</a>, um velho conhecido dos delegados,
    a dívida pode ser classificada em dois tipos dependendo do modo em que são contraídas, estes tipos são: dívida técnica sem intenção e dívida técnica intencional.
</p>

<h3 class="section-subheading">Dívida Técnica sem intenção</h3>

<p>
    Ocorre quando a d&amp;iacute;vida é adquirida sem que o time perceba, ou seja, por algum descuido ou pela complexidade, alguns problemas são introduzidos acidentalmente. Este tipo de d&amp;iacute;vida não é resultado de uma estratégia, gerando assim, um impacto negativo.
</p>

<p>
    Alguns exemplos do surgimento desta dívida são: "O layout não funciona no IE 6.0" (quem é o maluco que usa o IE 6?), "Código ruim feito por desenvolvedor inexperiente", "Um cliente pediu uma funcionalidade para o sistema, que não foi totalmente detalhada corretamente e quando a solução chega ao cliente não era exatamente o que ele esperava".
</p>

<h3 class="section-subheading">Dívida Técnica intencional</h3>

<p>
    Ocorre quando a dívida técnica a ser adquirida já é conhecida e por algum motivo o time decide adquiri-la de maneira consciente. Isso pode ocorrer para uma entrega mais rápida, deixando de lado os esforços futuros. Este tipo de dívida é resultado de uma estratégia.
</p>

<p>
Alguns exemplos são: "Uma equipe não tem tempo suficiente para a entrega de uma solução definitiva, então ela escreve um código que mantém as duas bases sincronizadas e as junta depois que essa versão for enviada.", "Uma equipe faz um código que resolve o problema, então se opta por usar este código e deixa para depois a sua refatoração."
</p>

<h2 class="section-heading">Pagando a dívida</h2>

<h3 class="section-subheading">Dívida Técnica a curto prazo</h3>

<p>
Bem como uma dívida comum a dívida técnica pode ser paga num curto prazo e, geralmente, o pagamento deste tipo de dívida técnica é feito para suprir as necessidades imediatas. Outra característica desse tipo de dívida é que ela é paga com certa frequência a fim de reabilitar o crédito para aquisição de novas dívidas.
</p>

<h3 class="section-subheading">Dívida Técnica a longo prazo</h3>

<p>
As dívidas técnicas a longo prazo são adquiridas, em geral, de forma estratégica, com um planejamento a fim de suprir necessidades de grande valor de negócio, como por exemplo, o lançamento de um certo produto a fim de ganhar espaço no mercado, ou deixar de fazer os testes unitários, que no futuro precise ser paga.
</p>

<p>
Nos próximos posts vamos discutir mais como identificar uma dívida técnica e como criar indicadores para podermos planejar os nossos pagamentos.
</p>

<p>
Não se esqueçam de comentar!
</p>

<div class="references">
    <small><b>Referências</b></small>
    <ul>
        <li><a name="referencia01">[1]</a> Ward Cunningham's OOPSLA '92 Experience Report that first mentions technical debt. <a target="_blank" href="http://c2.com/doc/oopsla92.html">http://c2.com/doc/oopsla92.html</a></li> 
        <li><a name="referencia02">[2]</a> Technical Debt, Martin Fowler, 26 de fevereiro de 2009, <a target="_blank" href="http://martinfowler.com/bliki/TechnicalDebt.html">http://martinfowler.com/bliki/TechnicalDebt.html</a></li> 
        <li><a name="referencia03">[3]</a> Vídeo de Ward Cunnigham sobre dívida técnica, transcrito por June Kim e Lawrence Wang, postado em 22 de Janeiro de 2011, <a target="_blank" href="http://c2.com/cgi/wiki?WardExplainsDebtMetaphor">http://c2.com/cgi/wiki?WardExplainsDebtMetaphor</a></li> 
        <li><a name="referencia04">[4]</a> Measuring and Monitoring Technical Debt, Carolyn Seaman and Yuepu Guo, Advances in Computers, Vol. 82, 25-46, 2011</li> 
        <li><a name="referencia05">[5]</a> Technical Debt, Steve McConnell , <a target="_blank" href="http://www.construx.com/10x_Software_Development/Technical_Debt/">http://www.construx.com/10x_Software_Development/Technical_Debt/</a></li> 
    </ul>
</div>