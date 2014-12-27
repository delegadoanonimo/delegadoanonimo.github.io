---
layout:     post
title:      "2DFE: Um editor de n&iacute;veis para jogos 2D simples"
titleToShare: "jellyard-2dfe"
subtitle:   "A geleia dura no frio, sombrio e desolador mundo das startups"
description: "2DFE &eacute; um editor de n&iacute;veis para desenvolvimento de jogos 2D simples (especialmente plataformas) e foi desenvolvimento originalmente para a Jellyhard."
keywords: "Desenvolvimento de jogos, Game development, Indie Game development, Games 2D, N&iacute;veis, Level editor, editor de fase, Jellyhard"
date:       2014-12-14 06:00:00
dateShort:  "2014-12-14"
author:     "Marcelo Palladino"
header-img: "img/2014-12/post-bg-jellyard-2dfe.jpg"
tags:
- Desenvolvimento de jogos,
- Game development,
- Indie Game development,
- Games 2D,
- N&iacute;veis,
- Level editor,
- editor de fase
- Jellyhard
---

<p>

    Este ano me envolvi como nunca no mundo frio, sombrio e desolador mundo das startups. Eu e mais tr&ecirc;s colegas criamos e
    mantivemos uma <a href="http://www.jellyhard.com.br" target="_blank">iniciativa</a> para desenvolvimento de jogos multiplataforma com foco na experi&ecirc;ncia do jogador.
    Neste momento estamos concluindo o primeiro projeto da empresa e h&aacute; v&aacute;rias coisas interessantes a
    serem compartilhadas sobre gerenciamento de projetos, ciclo de vida de desenvolvimento e cria&ccedil;&atilde;o de software em startups.
    Com certeza vou voltar neste tema, mas hoje quero compartilhar algo mais pr&aacute;tico que criamos durante o projeto.
</p>

<p>
    O jogo &eacute; um runner game. O jogador controla um personagem que anda da esquerda para direita e tem responder aos desafios
    usando reflexo e mem&oacute;ria. H&aacute; in&uacute;meros jogos assim por a&iacute;, mas o diferencial do
    jellyborn (t&iacute;tulo de trabalho) est&aacute; na hist&oacute;ria que est&aacute; sendo contada. N&atilde;o vai haver spoliers aqui, sen&atilde;o nosso game designer me mata. hahaha
</p>

<p>
    Do ponto de vista da infraestrutura para desenvolvimento do jogo,
    o primeiro grande desafio foi oferecer aos designers uma forma r&aacute;pida de fazer o level design. Neste tipo de jogo
    conta muito a cad&ecirc;ncia dos desafios e o posicionamento dos elementos em rela&ccedil;&atilde;o &agrave; velocidade do
    personagem principal. Ent&atilde;o era vital que tiv&eacute;ssemos algo que nos permitisse testar ideias de level design rapidamente.
</p>

<h2 class="section-heading">O editor</h2>

<p>
    Com base em nossas escolhas para desenvolvimento (escolhemos usar a <a href="http://libgdx.badlogicgames.com/" target="_blank">libGDX</a>, a qual ter&aacute; uma s&eacute;rie de posts dedicados &agrave; ela),
    resolvi criar um pequeno editor especializado e utilizar o arquivo resultante como base para cria&ccedil;&atilde;o e
    posicionamento dos elementos do jogo.
</p>

<img src="{{ site.url }}/img/2014-12/2dfe_2.jpg" alt="2DFE durante a edi&ccedil;&atilde;o de um n&iacute;vel" class="img-responsive center-block">

<p>
    A primeira decis&atilde;o do projeto foi entender que os elementos poderiam ser adicionados ao editor de forma flex&iacute;vel e
    sem qualquer tipo de programa&ccedil;&atilde;o. Para este fim, no diret&oacute;rio do editor existe uma pasta chamada
    <b>Elements</b> que pode ser utilizada para fazer o editor entender os elementos que podem ser selecionados.
</p>

<p>
    Cada <b>subpasta</b> &eacute; uma categoria e os elementos s&atilde;o definidos pelas <b>imagens</b> dentro destas pastas.
</p>

<img src="{{ site.url }}/img/2014-12/2dfe_1.jpg" alt="Jellyhard Jellyborn rodando" class="img-responsive center-block">


<p>
    Abaixo voc&ecirc; pode ver o conte&uacute;do da pasta Elements do projeto Jellyborn. Se voc&ecirc; a comparar com a
    figura acima que mostra o editor, fica bem claro o que est&aacute; acontecendo.
</p>

<img src="{{ site.url }}/img/2014-12/2dfe_3.jpg" alt="Pasta Elements do projeto jellyborn" class="img-responsive center-block">

<h2 class="section-heading">Par&acirc;metros</h2>

<img src="{{ site.url }}/img/2014-12/2dfe_4.jpg" alt="Par&acirc;metros de um elemento selecionado" class="img-responsive center-block">

<p>
    Os par&acirc;metros tamb&eacute;m servem para flexibilizar o editor. Eles podem ser qualquer coisa! Trata-se de
    um dicion&aacute;rio simples de chave/valor com o objetivo de permitir que o level designer possa ser feito de
    forma flex&iacute;vel em total acordo com o modelo de dom&iacute;nio que foi criado para o jogo. Na figura acima h&aacute;
    um exemplo do Jellyborn de utiliza&ccedil;&atilde;o de um proj&eacute;til cujos par&acirc;metros s&atilde;o a velocidade em X e
    um fator de proximidade em rela&ccedil;&atilde;o ao jogador para disparar o lan&ccedil;amento.
</p>

<h2 class="section-heading">Muito o que fazer</h2>

<p>
    H&aacute; muito o que fazer no editor para torn&aacute;-lo um software descente. Para a <a href="http://www.jellyhard.com.br" target="_blank">Jellyhard</a> ele foi uma ferramenta de momento
    criado para resolver um problema do projeto. N&atilde;o era o foco do desenvolvimento, entende? Nosso objetivo era entregar o
    jogo e a ferramenta ajudou bastante. Por isso resolvi compartilhar a ideia e os fontes.
    Logo publicarei algumas coisas usando a <a href="http://libgdx.badlogicgames.com/" target="_blank">libGDX</a> e o 2DFE para continuar isso aqui de alguma forma.
</p>

<p>
    Os fontes do editor podem ser encontrados <a href="https://github.com/mfpalladino/2DFE" target="_blank">aqui</a>.
</p>

<p>
    At&eacute; mais!
</p>

<a href="https://github.com/mfpalladino/2DFE" title="C&oacute;digo fonte utilizado no artigo" target="_blank"><img src="{{ site.url }}/img/Octocat.jpg" alt="C&oacute;digo fonte utilizado no artigo" class="img-responsive center-block" style="cursor:pointer;"></a> 