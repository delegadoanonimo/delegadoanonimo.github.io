---
layout:     post
title:      "Algumas novidades do C# 6"
titleToShare: "algumas-novidades-csharp6"
subtitle:   "Mais meio tom para cima"
description: "Mais meio tom para cima: Testando algumas novidades da linguagem no C# 6."
keywords: "Roslyn, Visual Studio 2015, C# 6"
date:       2015-01-02 06:00:00
dateShort:  "2015-01-02"
author:     "Marcelo Palladino"
header-img: "img/2015-01/post-bg-algumas-novidades-csharp6.jpg"
header-img-url: "http://www.dotnettoad.com/index.php?/archives/20-when-not-to-use-the-goto-keyword.html"
tags:
- Roslyn,
- Visual Studio 2015,
- C# 6
---

<h2 class="section-heading">Auto Property initializers</h2>

<p>
O C# 3 trouxe um recurso muito interessante chamado Auto Property. Seu objetivo era facilitar a cria&ccedil;&atilde;o daquele tipo de propriedade que apenas exp&otilde;e um estado. Antes das propriedades auto implementadas era comum c&oacute;digos como o fragmento abaixo.
</p>

{% highlight c# linenos %}
class Charp2Entity
{
    private Guid _id;

    public Guid Id
    {
        get { return _id; }
        protected set { _id = value; }
    }
}
{% endhighlight %}

<p>
Este mesmo c&oacute;digo com a propriedade auto implementada fica mais expressivo, deixando para o c&oacute;digo gerado pelo compilador a parte meramente burocr&aacute;tica de utilizar uma vari&aacute;vel ali.
</p>

{% highlight c# linenos %}
public Guid Id { get; protected set; }
{% endhighlight %}

<p>
Bem melhor, n&atilde;o &eacute;? Agora digamos que esta propriedade tivesse um valor inicial. Para inicializ&aacute;-la, tinhamos que implementar um construtor para fazer o servi&ccedil;o.
</p>

{% highlight c# linenos %}
class Charp3Entity
{
    public Charp3Entity()
    {
        Id = Guid.NewGuid();
    }

    public Guid Id { get; protected set; }
}
{% endhighlight %}

<p>
O C# 6 trouxe um recurso para facilitar este trabalho. A ideia &eacute; fornecer uma forma mais flu&iacute;da de inicializar propriedades auto implementadas, novamente deixando a parte burocr&aacute;tica para o c&oacute;digo gerado pelo compilador.
</p>

{% highlight c# linenos %}
class Charp6Entity
{
    public Guid Id { get; protected set; } = Guid.NewGuid();
}
{% endhighlight %}

<p>
BEEEEMMMM melhor, hein! Apesar de ser um simples a&ccedil;ucar sint&aacute;tico, quando analisamos historicamente vemos claramente que a linguagem proporcionou que o c&oacute;digo ficasse bem mais expressivo com o tempo, n&atilde;o &eacute;?
</p>

<p>
Vale ressaltar que este tipo de inicializa&ccedil;&atilde;o tamb&eacute;m funciona muito bem com propriedades somente leitura.
</p>

{% highlight c# linenos %}
class Charp6Entity
{
    public string Tip { get; } = "Getter-only auto-properties also works...";
}
{% endhighlight %}

<h2 class="section-heading">Estruturas com construtores sem par&acirc;metros</h2>

<p>
At&eacute; esta vers&atilde;o, n&atilde;o era poss&iacute;vel declarar um construtor sem par&acirc;metros em uma estrutura. No C# 6 isso &eacute; plenamente poss&iacute;vel.
</p>

{% highlight c# linenos %}
struct Cpf
{
    public Cpf()
    {
        IsValid = false;
        Number = string.Empty;
    }
}
{% endhighlight %}


<p>
Para entender este recurso &eacute; primordial pensar um pouco sobre o c&oacute;digo abaixo vai funcionar:
</p>

{% highlight c# linenos %}
var cpf = default(Cpf);
{% endhighlight %}

<p>
Isso cria uma inst&acirc;ncia da estrutura sem a necessidade de passar os par&acirc;metros. Ou seja, at&eacute; aqui n&atilde;o tinhamos como declarar um construtor padr&atilde;o para estruturas em c#, o que nos impedia de ter uma forma alternativa de criar uma inst&acirc;ncia da estrutura sem passar todos os par&acirc;metros. O que temos no c# 6 &eacute; uma maneira de dizer na estrutura como ela deve ser inicializada sem os par&acirc;metros.
</p>

<p>
&Eacute; importante ter mente que default(T) continua com o mesmo comportamento de antes. Ele n&atilde;o vai desencadear uma chamada para seu construtor sem par&acirc;metros.
</p>

<h2 class="section-heading">Dictionary initializers</h2>

<p>
Se n&atilde;o me engano, tamb&eacute;m foi o C# 3 que trouxe uma forma mais simples de inicializar um dictionary.
</p>

{% highlight c# linenos %}
class Charp2Style
{
    public Charp2Style()
    {
        Dictionary<string, Person> kids = new Dictionary<string, Person>();
        kids.Add("1", new Person("Lucas"));
        kids.Add("2", new Person("Caio"));
    }

}
{% endhighlight %}

{% highlight c# linenos %}
class Charp3Style
{
    public Charp3Style()
    {
        var simpleDictionary = new Dictionary<string, Person>
        {
            { "1", new Person("Lucas") },
            { "2", new Person("Caio") }
        };
    }
}
{% endhighlight %}

<p>
Assim como nas propriedades auto implementadas, a inicializa&ccedil;&atilde;o de dicion&aacute;rios tamb&eacute;m ficou mais expressiva no c# 6.
</p>

{% highlight c# linenos %}
class Charp6Style
{
    public Charp6Style()
    {
        var simpleDictionary = new Dictionary<string, Person>
        {
            ["1"] = new Person("Lucas"),
            ["2"] = new Person("Caio")
        };
    }
}
{% endhighlight %}

<p>
Desta vez o n&uacute;mero de caracteres envolvidos n&atilde;o mudou. Apenas trocamos o par de chaves pelo pelos colchetes que definem a chave do item no dicion&aacute;rio. No entanto, para quem olha o c&oacute;digo fica bem mais claro que estamos trabalhando com um dicion&aacute;rio.
</p>

<h2 class="section-heading">Utilizando membros de classes est&aacute;ticas</h2>

<p>
    Considere a utiliza&ccedil;&atilde;o do m&eacute;todo est&aacute;tico no c&oacute;digo abaixo.
</p>

{% highlight c# linenos %}
namespace csharp6news
{
    using System;

    class UsingStaticMembers
    {
        class BeforeCSharp6Style
        {
            public BeforeCSharp6Style()
            {
                Console.WriteLine("Linha 1");
                Console.WriteLine("Linha 2");
                Console.WriteLine("Linha 3");
            }
        }
    }
}
{% endhighlight %}

<p>
No C# 6 existe a possibilidade de declarar o tipo est&aacute;tico com using com a finalidade de suprimir seu nome no momento da utiliza&ccedil;&atilde;o do membro est&aacute;tico.
</p>

{% highlight c# linenos %}
namespace csharp6news_1
{
    using System.Console; //key point...

    class UsingStaticMembers
    {
        class CSharp6Style
        {
            public CSharp6Style()
            {
                WriteLine("Linha 1");
                WriteLine("Linha 2");
                WriteLine("Linha 3");
            }
        }
    }
}
{% endhighlight %}

<p>
Me parece que o ponto aqui &eacute; escrever menos c&oacute;digo. No entanto, eu, particularmente, pretendo ter um pouco de cautela para jogar este a&ccedil;ucar no meu c&oacute;digo. Pensando sobre isso e baseado em nada (&eacute; sempre importante dizer), acho que remover o contexto da chamada do m&eacute;todo tem potencial para tornar o c&oacute;digo mais obscuro e dif&iacute;cil de entender. Classes puramente est&aacute;ticas para mim j&aacute; s&atilde;o consideradas um mal sinal. Podem existir situa&ccedil;&otilde;es nas quais elas s&atilde;o &uacute;teis, mas j&aacute; me deparei com alguns exemplos nos quais estas classes eram bols&otilde;es de m&eacute;todos de tudo que &eacute; tipo.
</p>

<p>
Vou extrapolar para um exemplo meio radical aqui, mas vai servir para mostrar o meu receio quanto &agrave; utiliza&ccedil;&atilde;o desmedida desse recurso. Vejamos uma aplica&ccedil;&atilde;o de um Factory cl&aacute;ssico.
</p>

{% highlight c# linenos %}
namespace csharp6news_1
{
    interface IComposer
    {
    }

    class Composer : IComposer
    {
        public Composer(string name)
        {
            Name = name;
        }

        public string Name { get; private set; }
    }

    static class ComposerFactory
    {
        public static IComposer Create()
        {
            return new Composer("Wolfgang Amadeus Mozart");
        }
    }
}
{% endhighlight %}

<p>
Sua utiliza&ccedil;&atilde;o poderia ficar assim:
</p>

{% highlight c# linenos %}
namespace csharp6news_1
{
    using ComposerFactory; //importando a classe estatica

    class UsingStaticMembers
    {
        class CSharp6Style
        {
            public CSharp6Style()
            {
                var c = Create();
            }
        }
    }
}
{% endhighlight %}

<p>
T&aacute;, eu apelei e declarei a vari&aacute;vel de uma forma que dado o nome do m&eacute;todo, fica imposs&iacute;vel saber o que Create est&aacute; retornando. Agora, quem nunca viu uma vari&aacute;vel declarada assim? Pode ser besteira minha, coisa de velho rabugento e/ou falta de contexto para entender melhor isso, mas inicialmente n&atilde;o curti tanto assim.
</p>

<h2 class="section-heading">Null propagation</h2>

<p>
Para compensar minha &lsquo;rabugice&rsquo; em rela&ccedil;&atilde;o &agrave; importa&ccedil;&atilde;o de tipos est&aacute;ticos, vamos falar sobre este &oacute;timo recurso (um dos mais votados no user's voice) que veio com a vers&atilde;o 6 do C#. Considere o c&oacute;digo abaixo.
</p>

{% highlight c# linenos %}
string OldStyle()
{
    if (_person != null && _person.Address != null)
        return _person.Address.ToString();

    return string.Empty;
}
{% endhighlight %}

<p>Agora considere a mesma coisa sendo feita com null propagation:</p>

{% highlight c# linenos %}
string CSharp6Style()
{
    return _person?.Address?.ToString() ?? string.Empty;
}
{% endhighlight %}

<p>
Percebeu a utiliza&ccedil;&atilde;o do &quot;?.&quot;? Isso substitui aquele &quot;if&quot; burocr&aacute;tico. Muito mais limpo, n&atilde;o &eacute;? Novamente se trata de deixar a burocracia para o c&oacute;digo gerado pelo compilador. Obviamente n&atilde;o existe m&aacute;gica. O c&oacute;digo que faz as checagens est&aacute; l&aacute;. Basta verificar em qualquer descompilador de .NET.
</p>

{% highlight c# linenos %}
private string CSharp6Style()
{
    NullPropagation.Person person = this._person;
    string str;
    if (person == null)
    {
        str = (string) null;
    }
    else
    {
        NullPropagation.Address address = person.Address;
        str = address != null ? address.ToString() : (string) null;
    }
    return str;
}
{% endhighlight %}

<p>
Bom, ainda restam algumas coisas para dizer sobre este tema, algo que provavelmente vai ser feito em um artigo futuro.
Vale dizer tamb&eacute;m que a lista de recursos para o C# 6 ainda n&atilde;o est&aacute; fechada e voc&ecirc; pode acompanhar seu status 
<a href="http://roslyn.codeplex.com/wikipage?title=Language%20Feature%20Status&referringTitle=Home" target="_blank">aqui</a>.
</p>

<p>
    At&eacute; mais!
</p>

<a href="https://github.com/mfpalladino/csharp6news" title="C&oacute;digo fonte utilizado no artigo" target="_blank"><img src="{{ site.url }}/img/Octocat.jpg" alt="C&oacute;digo fonte utilizado no artigo" class="img-responsive center-block" style="cursor:pointer;"></a> 