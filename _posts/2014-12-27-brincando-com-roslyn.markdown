---
layout:     post
title:      "Brincando com Rozlyn"
titleToShare: "brincando-com-roslyn"
subtitle:   "N&atilde;o, p&eacute;ra... (de novo!)"
description: "Colocando a m&atilde;o na massa e brincando um pouco com as APIs do Roslyn."
keywords: "Roslyn, Visual Studio 2015, C# 6"
date:       2014-12-27 08:52:00
dateShort:  "2014-12-27"
author:     "Marcelo Palladino"
header-img: "img/2014-12/post-bg-brincando-com-roslyn.jpg"
header-img-url: "http://xkcd.com/303/"
tags:
- Roslyn
- Visual Studio 2015
- CSharp 6
---

<p>
    Desde de <b>2002</b> (ou um pouco antes para quem &eacute; velho e usou as vers&otilde;es beta), a cada nova vers&atilde;o do Visual Studio somos apresentados a recursos que melhoram a plataforma enormemente.
    Em <b>2005</b> foram os tipos gen&eacute;ricos, em <b>2007</b> tivemos o linq, <b>2010</b> apresentou o dynamic e <b>2012</b> facilitou nossas vidas com uma
    forma diferente (mais f&aacute;cil e direta) de criar software ass&iacute;ncrono (async).
</p>

<p>
    Agora em <b>2014</b> estamos sendo bombardeamos novamente com uma porrada de novidades que vir&atilde;o com o Visual Studio 2015.
    A plataforma est&aacute; ficando cada vez mais madura, aberta e multiplataforma. Temos coisas novas no C#, no ASP.NET e no desenvolvimento de
    aplicativos e etc.
</p>

<p>
    A cereja no bolo para mim &eacute; a nova plataforma de compila&ccedil;&atilde;o do
    .NET, que fornece compiladores C# e Visual Basic que podem ser utilizados como servi&ccedil;o pelos desenvolvedores, 
    o <b>.NET compiler platform (Roslyn).</b>
</p>

<h2 class="section-heading">M&atilde;o na massa</h2>

<p>
    B&oacute;ra ent&atilde;o fazer alguma coisa. Para sua informa&ccedil;&atilde;o, estou usando o
    <a href="http://www.visualstudio.com/en-us/downloads/visual-studio-2015-downloads-vs.aspx" target="_blank">Visual Studio 2015 Preview</a> (14.0.22310.1 DP) enquanto escrevo este artigo. Para come&ccedil;ar, vou criar uma
    Console Application.
</p>

<img src="{{ site.url }}/img/2014-12/playwithroslyn_0.png" alt="Criando uma aplica&ccedil;&atilde;o console" class="img-responsive center-block">

<p>
    Uma vez que aplica&ccedil;&atilde;o est&aacute; criada, vou adicionar o Roslyn ao projeto
    utilizando o Nuget (lembre-se que como o Roslyn &eacute; um Prerelease, isso
    deve ser considerado isso na pesquisa (-Prerelease option)).
</p>

```
Install-Package -Prerelease Microsoft.CodeAnalysis.CSharp
```

<p>
    Para come&ccedil;ar a brincadeira nesta &eacute;poca de mega sena da virada,
    digamos que o c&oacute;digo que deve ser compilado seja parecido com a classe abaixo.
</p>

{% highlight c# linenos %}
public class MyInnocentLuckyNumbersGenerator
{
    public System.Collections.Generic.IEnumerable<int> GetLucky()
    {
        var r = new System.Random((int)System.DateTime.Now.Ticks);
        for (int i = 1; i <= 6; i++)
            yield return r.Next(1, 60);
    }
}
{% endhighlight %}


<p>
    Certo. Agora na classe <code>Program</code> da aplica&ccedil;&atilde;o que estou fazendo as brincadeiras, vou criar um 
    um m&eacute;todo (<code>CodeToCompile</code>) cuja responsabilidade &eacute; retornar a <code>string</code> com o c&oacute;digo que deve ser compilado.
</p>

{% highlight c# linenos %}
private static string CodeToCompile()
{
    return @"
        public class MyInnocentLuckyNumbersGenerator
        {
            public System.Collections.Generic.IEnumerable<int> GetLucky()
            {
                var r = new System.Random((int)System.DateTime.Now.Ticks);
                for (int i = 1; i <= 6; i++)
                    yield return r.Next(1, 60);
            }
        }";
}
{% endhighlight %}

<p>
    Feito isso, vou colocar o Roslyn para trabalhar com base nesta string que cont&eacute;m o c&oacute;digo de uma classe.
</p>

{% highlight c# linenos %}
static void Main(string[] args)
{
    var syntaxTree = Microsoft.CodeAnalysis.CSharp.SyntaxFactory.ParseSyntaxTree(CodeForCompile());

    var compilation = Microsoft.CodeAnalysis.CSharp.CSharpCompilation
        .Create("PlayWithRoslyn.OnTheFlyAssembly")
        .AddSyntaxTrees(syntaxTree);

    foreach (var compilationDiagnostic in compilation.GetDiagnostics())
        System.Console.WriteLine(compilationDiagnostic);
}
{% endhighlight %}

<p>
    No m&eacute;todo <code>main</code>, a primeira linha gera a &aacute;rvore de syntax com base no c&oacute;digo que
    deve ser compilado. Depois cria o que &eacute; chamado de compila&ccedil;&atilde;o (passando o nome do assembly como par&acirc;metro),
    adiciona a &aacute;rvore de syntax e, por fim, o c&oacute;digo faz um loop nos diagn&oacute;sticos gerados pela compila&ccedil;&atilde;o escrevendo na sa&iacute;da padr&atilde;o cada um deles. 
</p>

<p>
    A sa&iacute;da gerada pela execu&ccedil;&atilde;o do programa &eacute; parecida com a figura abaixo.
</p>

<img src="{{ site.url }}/img/2014-12/playwithroslyn_1.png" alt="Diagn&oacute;sticos da compila&ccedil;&atilde;o com Roslyn." class="img-responsive center-block">

<p>
    <b>O que aconteceu?</b> Pela an&aacute;lise dos diagn&oacute;sticos pode-se perceber que falta uma refer&ecirc;ncia. Neste caso especificamente falta referenciar a <b>mscorlib</b>. Vou adicionar a refer&ecirc;ncia e analisar a sa&iacute;da novamente.
</p>

{% highlight c# linenos %}
static void Main(string[] args)
{
    var syntaxTree = Microsoft.CodeAnalysis.CSharp.SyntaxFactory.ParseSyntaxTree(CodeForCompile());

    var mscorlibReference = Microsoft.CodeAnalysis.MetadataReference
        .CreateFromAssembly(typeof(string).Assembly);

    var compilation = Microsoft.CodeAnalysis.CSharp.CSharpCompilation
        .Create("PlayWithRoslyn.OnTheFlyAssembly")
        .AddReferences(mscorlibReference)
        .AddSyntaxTrees(syntaxTree);

    foreach (var compilationDiagnostic in compilation.GetDiagnostics())
        System.Console.WriteLine(compilationDiagnostic);
}
{% endhighlight %}

<p>
    O c&oacute;digo &eacute; bem direto. Ele pega a refer&ecirc;ncia com base em um assembly (que foi encontrado com base em um tipo) e adiciona na compila&ccedil;&atilde;o (<code>AddReferences</code>). 
</p>

<p>
    A nova sa&iacute;da ainda apresenta um problema, mas ficou bem melhor.
</p>

<img src="{{ site.url }}/img/2014-12/playwithroslyn_2.png" alt="Diagn&oacute;sticos da compila&ccedil;&atilde;o com Roslyn (segunda tentativa)." class="img-responsive center-block">

<p>
O problema agora se refere ao tipo do projeto gerado pela compila&ccedil;&atilde;o. A compila&ccedil;&atilde;o est&aacute; esperando um ponto de entrada, o que para este exemplo n&atilde;o encaixa muito bem. Sendo assim, vou fazer uma terceira modifica&ccedil;&atilde;o que far&aacute; com que a compila&ccedil;&atilde;o gere uma <b>class library</b>.
</p>

{% highlight c# linenos %}
static void Main(string[] args)
{
    var syntaxTree = Microsoft.CodeAnalysis.CSharp.SyntaxFactory.ParseSyntaxTree(CodeToCompile());
    var mscorlibReference = Microsoft.CodeAnalysis.MetadataReference
        .CreateFromAssembly(typeof(string).Assembly);

    var compilationOptions = new Microsoft.CodeAnalysis.CSharp
        .CSharpCompilationOptions(Microsoft.CodeAnalysis.OutputKind.DynamicallyLinkedLibrary);

    var compilation = Microsoft.CodeAnalysis.CSharp.CSharpCompilation
        .Create("PlayWithRoslyn.OnTheFlyAssembly")
        .WithOptions(compilationOptions)
        .AddReferences(mscorlibReference)
        .AddSyntaxTrees(syntaxTree);

    foreach (var compilationDiagnostic in compilation.GetDiagnostics())
        System.Console.WriteLine(compilationDiagnostic);
}
{% endhighlight %}

<p>
O construtor da classe <code>CSharpCompilationOptions</code> recebe uma pancada (e bota pancada nisso!) de par&acirc;metros, mas o &uacute;nico obrigat&oacute;rio &eacute; o <code>outputKind</code>, que define o tipo de sa&iacute;da da compila&ccedil;&atilde;o. Sendo assim, a terceira vers&atilde;o do c&oacute;digo cria uma inst&acirc;ncia para definir as op&ccedil;&otilde;es e a passa para a compila&ccedil;&atilde;o. Com isso, a lista de diagn&oacute;sticos estar&aacute; vazia na pr&oacute;xima execu&ccedil;&atilde;o do programa.
</p>

<p>
Bom, era isso. No pr&oacute;ximo artigo desta s&eacute;rie vou continuar exatamente deste ponto e estender um pouco este exemplo.
</p>

<p>
    At&eacute; mais!
</p>

<a href="https://github.com/mfpalladino/PlayWithRoslyn" title="C&oacute;digo fonte utilizado no artigo" target="_blank"><img src="{{ site.url }}/img/Octocat.jpg" alt="C&oacute;digo fonte utilizado no artigo" class="img-responsive center-block" style="cursor:pointer;"></a> 
