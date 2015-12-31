---
layout:     post
title:      "2DFE: Um editor de níveis para jogos 2D simples"
titleToShare: "jellyard-2dfe"
subtitle:   "A geleia dura no frio, sombrio e desolador mundo das startups"
description: "2DFE é um editor de níveis para desenvolvimento de jogos 2D simples (especialmente plataformas) e foi desenvolvimento originalmente para a Jellyhard."
keywords: "Desenvolvimento de jogos, Game development, Indie Game development, Games 2D, Níveis, Level editor, editor de fase, Jellyhard"
date:       2014-12-14 06:00:00
dateShort:  "2014-12-14"
author:     "Marcelo Palladino"
header-img: "img/2014-12/post-bg-jellyard-2dfe.jpg"
tags:
- Desenvolvimento de jogos
- Jellyhard
- Startup
---

<p>

    Este ano me envolvi como nunca no mundo frio, sombrio e desolador mundo das startups. Eu e mais três colegas criamos e
    mantivemos uma <a href="http://www.jellyhard.com.br" target="_blank">iniciativa</a> para desenvolvimento de jogos multiplataforma com foco na experiência do jogador.
    Neste momento estamos concluindo o primeiro projeto da empresa e há várias coisas interessantes a
    serem compartilhadas sobre gerenciamento de projetos, ciclo de vida de desenvolvimento e criação de software em startups.
    Com certeza vou voltar neste tema, mas hoje quero compartilhar algo mais prático que criamos durante o projeto.
</p>

<p>
    O jogo é um runner game. O jogador controla um personagem que anda da esquerda para direita e tem responder aos desafios
    usando reflexo e memória. Há inúmeros jogos assim por aí, mas o diferencial do
    jellyborn (título de trabalho) está na história que está sendo contada. Não vai haver spoliers aqui, caso contrário nosso game designer me mata. hahaha
</p>

<p>
    Do ponto de vista da infraestrutura para desenvolvimento do jogo,
    o primeiro grande desafio foi oferecer aos designers uma forma rápida de fazer o level design. Neste tipo de jogo
    conta muito a cadência dos desafios e o posicionamento dos elementos em relação à velocidade do
    personagem principal. Então era vital que tivéssemos algo que nos permitisse testar ideias de level design rapidamente.
</p>

<h2 class="section-heading">O editor</h2>

<p>
    Com base em nossas escolhas para desenvolvimento (escolhemos usar a <a href="http://libgdx.badlogicgames.com/" target="_blank">libGDX</a>, a qual terá uma série de posts dedicados à ela),
    resolvi criar um pequeno editor especializado e utilizar o arquivo resultante como base para criação e
    posicionamento dos elementos do jogo.
</p>

<img src="{{ site.url }}/img/2014-12/2dfe_2.jpg" alt="2DFE durante a edição de um nível" class="img-responsive center-block">

<p>
    A primeira decisão do projeto foi entender que os elementos poderiam ser adicionados ao editor de forma flexível e
    sem qualquer tipo de programação. Para este fim, no diretório do editor existe uma pasta chamada
    <b>Elements</b> que pode ser utilizada para fazer o editor entender os elementos que podem ser selecionados.
</p>

<p>
    Cada <b>subpasta</b> é uma categoria e os elementos são definidos pelas <b>imagens</b> dentro destas pastas.
</p>

<img src="{{ site.url }}/img/2014-12/2dfe_1.jpg" alt="Jellyhard Jellyborn rodando" class="img-responsive center-block">


<p>
    Abaixo você pode ver o conteúdo da pasta Elements do projeto Jellyborn. Se você a comparar com a
    figura acima que mostra o editor, fica bem claro o que está acontecendo.
</p>

<img src="{{ site.url }}/img/2014-12/2dfe_3.jpg" alt="Pasta Elements do projeto jellyborn" class="img-responsive center-block">

<h2 class="section-heading">Parâmetros</h2>

<img src="{{ site.url }}/img/2014-12/2dfe_4.jpg" alt="Parâmetros de um elemento selecionado" class="img-responsive center-block">

<p>
    Os parâmetros também servem para flexibilizar o editor. Eles podem ser qualquer coisa! Trata-se de
    um dicionário simples de chave/valor com o objetivo de permitir que o level designer possa ser feito de
    forma flexível em total acordo com o modelo de domínio que foi criado para o jogo. Na figura acima há
    um exemplo do Jellyborn de utilização de um projétil cujos parâmetros são a velocidade em X e
    um fator de proximidade em relação ao jogador para disparar o lançamento.
</p>

<h2 class="section-heading">Muito o que fazer</h2>

<p>
    Há muito o que fazer no editor para torná-lo um software descente. Para a <a href="http://www.jellyhard.com.br" target="_blank">Jellyhard</a> ele foi uma ferramenta de momento
    criado para resolver um problema do projeto. Não era o foco do desenvolvimento, entende? Nosso objetivo era entregar o
    jogo e a ferramenta ajudou bastante. Por isso resolvi compartilhar a ideia e os fontes.
    Logo publicarei algumas coisas usando a <a href="http://libgdx.badlogicgames.com/" target="_blank">libGDX</a> e o 2DFE para continuar isso aqui de alguma forma.
</p>

<p>
    Os fontes do editor podem ser encontrados <a href="https://github.com/mfpalladino/2DFE" target="_blank">aqui</a>.
</p>

<p>
    Até mais!
</p>

<a href="https://github.com/mfpalladino/2DFE" title="Código fonte utilizado no artigo" target="_blank"><img src="{{ site.url }}/img/Octocat.jpg" alt="Código fonte utilizado no artigo" class="img-responsive center-block" style="cursor:pointer;"></a> 