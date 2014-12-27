---
layout:     post
title:      "SMS as a Service em .NET com Twilio"
titleToShare: "sms-as-a-service-com-twilio"
subtitle:   "Everything as a service..."
description: "Falando sobre como enviar SMS com .NET e C# usando o Twilio."
keywords: "SMS, C#, .NET, Twilio, Nuget"
date:       2014-11-25 10:33:00
dateShort:  "2014-11-25"
author:     "Marcelo Palladino"
header-img: "img/2014-12/post-bg-sms-as-a-service-com-twilio.jpg"
tags:
- ASP.NET MVC,
- C#,
- Cloud,
- Services,
- Servi&ccedil;os,
- SMS,
- Twilio
---

<p>
    Um dia destes esbarrei em um servi&ccedil;o bacaninha que gostaria de compartilhar aqui.
</p>

<p>
    O problema envolvia criar um aplicativo que, baseado em algumas regras, enviasse alarmes
    via SMS para os usu&aacute;rios. H&aacute; uma porrada de softwares
    que s&atilde;o vendidos como servi&ccedil;o e que se responsabilizam pela entrega de mensagens SMS.
    Acabei implementando alguns (o usu&aacute;rio tinha a op&ccedil;&atilde;o de escolher qual utilizar dentro de um painel de administra&ccedil;&atilde;o da coisa toda), mas um deles se destacou dos demais devido &agrave; facilidade de contrata&ccedil;&atilde;o/cobran&ccedil;a, qualidade da documenta&ccedil;&atilde;o e, principalmente, pela eleg&acirc;ncia da implementa&ccedil;&atilde;o do REST. Trata-se do Twilio.
</p>

<p><a href="https://www.twilio.com/" target="_blank">https://www.twilio.com/</a></p>

<img src="{{ site.url }}/img/2014-12/twilio_1.png" alt="P&aacute;gina inicial do Twilio" class="img-responsive center-block">

<h2 class="section-heading">Sobre o servi&ccedil;o</h2>

<p>
    Antes de falar sobre qualquer aspecto de implementa&ccedil;&atilde;o (que &eacute; bem simples para a maioria dos casos), vale citar alguns pontos que achei bem interessantes no servi&ccedil;o.
</p>

<p>
    1-Suporte internacional. Com o twilio sua aplica&ccedil;&atilde;o pode disparar mensagens para qualquer n&uacute;mero de telefone no mundo. Algumas op&ccedil;&otilde;es de servi&ccedil;o no Brasil suportam apenas n&uacute;meros nacionais...
</p>

<p>
    2-&Oacute;timo log de mensagens e dashboard para acompanhamento do servi&ccedil;o. No log voc&ecirc; consegue visualizar o custo de cada mensagem, se a ela foi quebrada em mais de um SMS, se houve erro na entrega e assim por diante.
</p>

<img src="{{ site.url }}/img/2014-12/twilio_2.png" alt="Log de mensagens enviadas" class="img-responsive center-block">


<p>
    3-Simplifica&ccedil;&atilde;o de contrata&ccedil;&atilde;o e cobran&ccedil;a: Voc&ecirc; cria a conta e, a partir da&iacute;, &eacute; poss&iacute;vel dar uma carga de &ldquo;20&rdquo; at&eacute; &ldquo;2000&rdquo; d&oacute;lares nela usando o paypal, por exemplo.
</p>


<img src="{{ site.url }}/img/2014-12/twilio_3.png" alt="Visualiza&ccedil;&atilde;o dos detalhes de cobran&ccedil;a" class="img-responsive center-block">

<p>
    Ainda nesta parte de cobran&ccedil;a, o servi&ccedil;o possui algumas possibilidades uteis, como a notifica&ccedil;&atilde;o por email quando o saldo estiver abaixo de X d&oacute;lares e a auto recarga para evitar que o servi&ccedil;o pare por falta de saldo. Esta &uacute;ltima funcionalidade &eacute; excelente e dos servi&ccedil;os que implementei, o twilio era um dos &uacute;nicos que fazia isso. Alguns servi&ccedil;os no Brasil exigem, acredite se quiser, liga&ccedil;&otilde;es telef&ocirc;nicas e at&eacute; pagamento de boletos (como &uacute;nica op&ccedil;&atilde;o) para iniciar a brincadeira. A&iacute; &eacute; osso...
</p>

<p>
    4-Suporte a credenciais para testes. Isso parece simples, mas a julgar por outros servi&ccedil;os, a solu&ccedil;&atilde;o do twilio &eacute; &oacute;tima. Quando voc&ecirc; faz a contrata&ccedil;&atilde;o, o servi&ccedil;o lhe oferece duas credenciais: uma de produ&ccedil;&atilde;o e outra para testes. As credenciais de testes funcionam exatamente igual as de produ&ccedil;&atilde;o, mas n&atilde;o geram cobran&ccedil;a. Isso &eacute; &oacute;timo para execu&ccedil;&atilde;o de testes de integra&ccedil;&atilde;o.
</p>

<img src="{{ site.url }}/img/2014-12/twilio_4.png" alt="Credenciais para ambientes de produ&ccedil;&atilde;o e testes" class="img-responsive center-block">


<h2 class="section-heading">Um pouco de m&atilde;o na massa</h2>

<p>
    Poderia falar ainda mais sobre o servi&ccedil;o dos caras, como o &oacute;timo suporte t&eacute;cnico, por exemplo, mas vou parar por aqui para poder colocar a m&atilde;o na massa. Partindo do princ&iacute;pio que voc&ecirc; tem os dados para executar as chamadas (sid, token e n&uacute;mero de telefone), podemos enviar uma mensagem SMS de forma bem simples:
</p>

<p>
    1-Crie uma aplica&ccedil;&atilde;o ASP.NET MVC simples e adicone o pacote Twilio via nuget.
</p>


<img src="{{ site.url }}/img/2014-12/twilio_5.png" alt="Instalando o pacote do Twilio" class="img-responsive center-block">

<p>
    2-Depois disso, crie uma view para receber os dados referentes &agrave;s credenciais do twilio,
    o n&uacute;mero de telefone que vai receber a mensagem e a mensagem propriamente dita. Eu dei uma limpada na aplica&ccedil;&atilde;o padr&atilde;o, ent&atilde;o o formul&aacute;rio para este teste ficou simples assim:
</p>

{% highlight css linenos %}
<style>
    fieldset {
        width: 400px;
    }

    label {
        display: block;
    }

    input[type="text"] {
        width: 300px;
    }

    input[type="submit"] {
        display: block;
        margin-top: 20px;
    }
</style>
{% endhighlight %}


{% highlight html linenos %}
<form method="POST" action="@Url.Action("SendSms")">
    <fieldset>
        <legend>Informe os dados para enviar o SMS atraves do twilio</legend>
 
        <label>Chave de identificacao:</label>
        <input name="sid" type="text" />
 
        <label>Token:</label>
        <input name="token" type="text" />
 
        <label>Numero de telefone "de":</label>
        <input name="fromPhoneNumber" type="text" />
 
        <label>Numero de telefone "para":</label>
        <input name="toPhoneNumber" type="text" />
 
        <label>Mensagem:</label>
        <textarea name="message" rows="4" cols="100"></textarea>
 
        <input type="submit" value="Enviar" />
 
        @ViewBag.SendSmsResultMessage
 
    </fieldset>
</form>
{% endhighlight %}


<img src="{{ site.url }}/img/2014-12/twilio_6.png" alt="Uma chamada do servi&ccedil;o com dados v&aacute;lidos" class="img-responsive center-block">

<p>
    3-No controller, a coisa toda se resume a isso:
</p>

{% highlight csharp linenos %}
using System;
using System.Web.Mvc;
using Twilio;

namespace TwilioSample.Controllers
{
    public class HomeController : Controller
    {
        public ActionResult Index()
        {
            ViewBag.SendSmsResultMessage = TempData.ContainsKey("SendSmsResultMessage") ? TempData["SendSmsResultMessage"] : String.Empty;
            return View();
        }

        [HttpPost]
        public ActionResult SendSms(string sid, string token, string fromPhoneNumber, string toPhoneNumber, string message)
        {
            var twilioClient = new TwilioRestClient(sid, token);
            var sendMessageResult = twilioClient.SendMessage(fromPhoneNumber, toPhoneNumber, message, "");

            if (sendMessageResult.RestException == null)
                TempData["SendSmsResultMessage"] = "Mensagem enviada com sucesso!";
            else
                TempData["SendSmsResultMessage"] = "Houve um erro durante a tentativa de enviar a mensagem: " + sendMessageResult.RestException.Message;

            return RedirectToAction("Index");
        }
    }
}
{% endhighlight %}

<p>
    Note que o m&eacute;todo SendMessage do Twilio retorna uma inst&acirc;ncia da classe Message, que dentre outras coisas, retorna a exce&ccedil;&atilde;o (se houver).
</p>

<img src="{{ site.url }}/img/2014-12/twilio_7.png" alt="Log do twilio mostrando os detalhes da mensagem enviada" class="img-responsive center-block">

<img src="{{ site.url }}/img/2014-12/twilio_8.png" alt="Mensagem no log do Twilio" class="img-responsive center-block">


<p>
    Bem, esta foi uma introdu&ccedil;&atilde;o bem r&aacute;pida ao servi&ccedil;o. Talvez eu escreva um novo artigo explorando outros aspectos do servi&ccedil;o. O que voc&ecirc; acha? O c&oacute;digo do
    artigo pode ser encontrado <a href="https://github.com/mfpalladino/twiliosample" target="_blank">aqui</a>.
</p>


<p>
    At&eacute; mais!
</p>

<a href="https://github.com/mfpalladino/twiliosample" title="C&oacute;digo fonte utilizado no artigo" target="_blank"><img src="{{ site.url }}/img/Octocat.jpg" alt="C&oacute;digo fonte utilizado no artigo" class="img-responsive center-block" style="cursor:pointer;"></a> 