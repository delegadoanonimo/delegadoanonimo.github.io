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
- Roslyn
- Visual Studio 2015
- CSharp 6
---

<h2 class="section-heading">Auto Property initializers</h2>

<p>
O C# 3 trouxe um recurso muito interessante chamado Auto Property. Seu objetivo era facilitar a criação daquele tipo de propriedade que apenas expõe um estado. Antes das propriedades auto implementadas era comum códigos como o fragmento abaixo.
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
Este mesmo código com a propriedade auto implementada fica mais expressivo, deixando para o código gerado pelo compilador a parte meramente burocrática de utilizar uma variável ali.
</p>

{% highlight c# linenos %}
public Guid Id { get; protected set; }
{% endhighlight %}

<p>
Bem melhor, não é? Agora digamos que esta propriedade tivesse um valor inicial. Para inicializá-la, tinhamos que implementar um construtor para fazer o serviço.
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
O C# 6 trouxe um recurso para facilitar este trabalho. A ideia é fornecer uma forma mais fluída de inicializar propriedades auto implementadas, novamente deixando a parte burocrática para o código gerado pelo compilador.
</p>

{% highlight c# linenos %}
class Charp6Entity
{
    public Guid Id { get; protected set; } = Guid.NewGuid();
}
{% endhighlight %}

<p>
BEEEEMMMM melhor, hein! Apesar de ser um simples açucar sintático, quando analisamos historicamente vemos claramente que a linguagem proporcionou que o código ficasse bem mais expressivo com o tempo, não é?
</p>

<p>
Vale ressaltar que este tipo de inicialização também funciona muito bem com propriedades somente leitura.
</p>

{% highlight c# linenos %}
class Charp6Entity
{
    public string Tip { get; } = "Getter-only auto-properties also works...";
}
{% endhighlight %}

<h2 class="section-heading">Estruturas com construtores sem parâmetros</h2>

<p>
Até esta versão, não era possível declarar um construtor sem parâmetros em uma estrutura. No C# 6 isso é plenamente possível.
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
Para entender este recurso é primordial pensar um pouco sobre o código abaixo vai funcionar:
</p>

{% highlight c# linenos %}
var cpf = default(Cpf);
{% endhighlight %}

<p>
Isso cria uma instância da estrutura sem a necessidade de passar os parâmetros. Ou seja, até aqui não tinhamos como declarar um construtor padrão para estruturas em c#, o que nos impedia de ter uma forma alternativa de criar uma instância da estrutura sem passar todos os parâmetros. O que temos no c# 6 é uma maneira de dizer na estrutura como ela deve ser inicializada sem os parâmetros.
</p>

<p>
é importante ter mente que default(T) continua com o mesmo comportamento de antes. Ele não vai desencadear uma chamada para seu construtor sem parâmetros.
</p>

<h2 class="section-heading">Dictionary initializers</h2>

<p>
Se não me engano, também foi o C# 3 que trouxe uma forma mais simples de inicializar um dictionary.
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
Assim como nas propriedades auto implementadas, a inicialização de dicionários também ficou mais expressiva no c# 6.
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
Desta vez o nÚmero de caracteres envolvidos não mudou. Apenas trocamos o par de chaves pelo pelos colchetes que definem a chave do item no dicionário. No entanto, para quem olha o código fica bem mais claro que estamos trabalhando com um dicionário.
</p>

<h2 class="section-heading">Utilizando membros de classes estáticas</h2>

<p>
    Considere a utilização do método estático no código abaixo.
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
No C# 6 existe a possibilidade de declarar o tipo estático com using com a finalidade de suprimir seu nome no momento da utilização do membro estático.
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
Me parece que o ponto aqui é escrever menos código. No entanto, eu, particularmente, pretendo ter um pouco de cautela para jogar este açucar no meu código. Pensando sobre isso e baseado em nada (é sempre importante dizer), acho que remover o contexto da chamada do método tem potencial para tornar o código mais obscuro e difícil de entender. Classes puramente estáticas para mim já são consideradas um mal sinal. Podem existir situações nas quais elas são Úteis, mas já me deparei com alguns exemplos nos quais estas classes eram bolsões de métodos de tudo que é tipo.
</p>

<p>
Vou extrapolar para um exemplo meio radical aqui, mas vai servir para mostrar o meu receio quanto à utilização desmedida desse recurso. Vejamos uma aplicação de um Factory clássico.
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
Sua utilização poderia ficar assim:
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
Tá, eu apelei e declarei a variável de uma forma que dado o nome do método, fica impossível saber o que Create está retornando. Agora, quem nunca viu uma variável declarada assim? Pode ser besteira minha, coisa de velho rabugento e/ou falta de contexto para entender melhor isso, mas inicialmente não curti tanto assim.
</p>

<h2 class="section-heading">Null propagation</h2>

<p>
Para compensar minha &lsquo;rabugice&rsquo; em relação à importação de tipos estáticos, vamos falar sobre este ótimo recurso (um dos mais votados no user's voice) que veio com a versão 6 do C#. Considere o código abaixo.
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
Percebeu a utilização do "?."? Isso substitui aquele "if" burocrático. Muito mais limpo, não é? Novamente se trata de deixar a burocracia para o código gerado pelo compilador. Obviamente não existe mágica. O código que faz as checagens está lá. Basta verificar em qualquer descompilador de .NET.
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
Vale dizer também que a lista de recursos para o C# 6 ainda não está fechada e você pode acompanhar seu status 
<a href="http://roslyn.codeplex.com/wikipage?title=Language%20Feature%20Status&referringTitle=Home" target="_blank">aqui</a>.
</p>

<p>
    Até mais!
</p>

<a href="https://github.com/mfpalladino/csharp6news" title="Código fonte utilizado no artigo" target="_blank"><img src="{{ site.url }}/img/Octocat.jpg" alt="Código fonte utilizado no artigo" class="img-responsive center-block" style="cursor:pointer;"></a> 