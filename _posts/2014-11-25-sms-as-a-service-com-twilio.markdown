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
- ASP.NET MVC
- CSharp
- Ferramentas
---

<p>
    Um dia destes esbarrei em um serviço bem bacana que gostaria de compartilhar aqui.
</p>

<p>
    O problema envolvia criar um aplicativo que, baseado em algumas regras, enviasse alarmes
    via SMS para os usuários. Há uma porrada de softwares
    que são vendidos como serviço e que se responsabilizam pela entrega de mensagens SMS.
    Acabei implementando alguns (o usuário tinha a opção de escolher qual utilizar dentro de um painel de administração da coisa toda), mas um deles se destacou dos demais devido à facilidade de contratação/cobrança, qualidade da documentação e, principalmente, pela elegância da implementação do REST. Trata-se do Twilio.
</p>

<p><a href="https://www.twilio.com/" target="_blank">https://www.twilio.com/</a></p>

<img src="{{ site.url }}/img/2014-12/twilio_1.png" alt="Página inicial do Twilio" class="img-responsive center-block">

<h2 class="section-heading">Sobre o serviço</h2>

<p>
    Antes de falar sobre qualquer aspecto de implementação (que é bem simples para a maioria dos casos), vale citar alguns pontos que achei bem interessantes no serviço.
</p>

<p>
    1-Suporte internacional. Com o twilio sua aplicação pode disparar mensagens para qualquer nÚmero de telefone no mundo. Algumas opções de serviço no Brasil suportam apenas números nacionais...
</p>

<p>
    2-Ótimo log de mensagens e dashboard para acompanhamento do serviço. No log você consegue visualizar o custo de cada mensagem, se a ela foi quebrada em mais de um SMS, se houve erro na entrega e assim por diante.
</p>

<img src="{{ site.url }}/img/2014-12/twilio_2.png" alt="Log de mensagens enviadas" class="img-responsive center-block">


<p>
    3-Simplificação de contratação e cobrança: Você cria a conta e, a partir daí, é possível dar uma carga de '20' até '2000' dólares nela usando o paypal, por exemplo.
</p>


<img src="{{ site.url }}/img/2014-12/twilio_3.png" alt="Visualização dos detalhes de cobrança" class="img-responsive center-block">

<p>
    Ainda nesta parte de cobrança, o serviço possui algumas possibilidades uteis, como a notificação por email quando o saldo estiver abaixo de X dólares e a auto recarga para evitar que o serviço pare por falta de saldo. Esta Última funcionalidade é excelente e dos serviços que implementei, o twilio era um dos Únicos que fazia isso. Alguns serviços no Brasil exigem, acredite se quiser, ligações telefônicas e até pagamento de boletos (como Única opção) para iniciar a brincadeira. Aí é osso...
</p>

<p>
    4-Suporte a credenciais para testes. Isso parece simples, mas a julgar por outros serviços, a solução do twilio é ótima. Quando você faz a contratação, o serviço lhe oferece duas credenciais: uma de produção e outra para testes. As credenciais de testes funcionam exatamente igual as de produção, mas não geram cobrança. Isso é ótimo para execução de testes de integração.
</p>

<img src="{{ site.url }}/img/2014-12/twilio_4.png" alt="Credenciais para ambientes de produção e testes" class="img-responsive center-block">


<h2 class="section-heading">Um pouco de mão na massa</h2>

<p>
    Poderia falar ainda mais sobre o serviço dos caras, como o ótimo suporte técnico, por exemplo, mas vou parar por aqui para poder colocar a mão na massa. Partindo do princípio que você tem os dados para executar as chamadas (sid, token e nÚmero de telefone), podemos enviar uma mensagem SMS de forma bem simples:
</p>

<p>
    1-Crie uma aplicação ASP.NET MVC simples e adicone o pacote Twilio via nuget.
</p>


<img src="{{ site.url }}/img/2014-12/twilio_5.png" alt="Instalando o pacote do Twilio" class="img-responsive center-block">

<p>
    2-Depois disso, crie uma view para receber os dados referentes às credenciais do twilio,
    o nÚmero de telefone que vai receber a mensagem e a mensagem propriamente dita. Eu dei uma limpada na aplicação padrão, então o formulário para este teste ficou simples assim:
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


<img src="{{ site.url }}/img/2014-12/twilio_6.png" alt="Uma chamada do serviço com dados válidos" class="img-responsive center-block">

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
    Note que o método SendMessage do Twilio retorna uma instância da classe Message, que dentre outras coisas, retorna a exceção (se houver).
</p>

<img src="{{ site.url }}/img/2014-12/twilio_7.png" alt="Log do twilio mostrando os detalhes da mensagem enviada" class="img-responsive center-block">

<img src="{{ site.url }}/img/2014-12/twilio_8.png" alt="Mensagem no log do Twilio" class="img-responsive center-block">


<p>
    Bem, esta foi uma introdução bem rápida ao serviço. Talvez eu escreva um novo artigo explorando outros aspectos do serviço. O que você acha? O código do
    artigo pode ser encontrado <a href="https://github.com/mfpalladino/twiliosample" target="_blank">aqui</a>.
</p>


<p>
    Até mais!
</p>

<a href="https://github.com/mfpalladino/twiliosample" title="Código fonte utilizado no artigo" target="_blank"><img src="{{ site.url }}/img/Octocat.jpg" alt="Código fonte utilizado no artigo" class="img-responsive center-block" style="cursor:pointer;"></a> 