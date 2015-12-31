---
layout:     post
title:      "Brincando com Rozlyn"
titleToShare: "brincando-com-roslyn"
subtitle:   "Não, péra... (de novo!)"
description: "Colocando a mão na massa e brincando um pouco com as APIs do Roslyn."
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
    Desde de <b>2002</b> (ou um pouco antes para quem é velho e usou as versões beta), a cada nova versão do Visual Studio somos apresentados a recursos que melhoram a plataforma enormemente.
    Em <b>2005</b> foram os tipos genéricos, em <b>2007</b> tivemos o linq, <b>2010</b> apresentou o dynamic e <b>2012</b> facilitou nossas vidas com uma
    forma diferente (mais fácil e direta) de criar software assíncrono (async).
</p>

<p>
    Agora em <b>2014</b> estamos sendo bombardeamos novamente com uma porrada de novidades que virão com o Visual Studio 2015.
    A plataforma está ficando cada vez mais madura, aberta e multiplataforma. Temos coisas novas no C#, no ASP.NET e no desenvolvimento de
    aplicativos e etc.
</p>

<p>
    A cereja no bolo para mim é a nova plataforma de compilação do
    .NET, que fornece compiladores C# e Visual Basic que podem ser utilizados como serviço pelos desenvolvedores, 
    o <b>.NET compiler platform (Roslyn).</b>
</p>

<h2 class="section-heading">Mão na massa</h2>

<p>
    Bóra então fazer alguma coisa. Para sua informação, estou usando o
    <a href="http://www.visualstudio.com/en-us/downloads/visual-studio-2015-downloads-vs.aspx" target="_blank">Visual Studio 2015 Preview</a> (14.0.22310.1 DP) enquanto escrevo este artigo. Para começar, vou criar uma
    Console Application.
</p>

<img src="{{ site.url }}/img/2014-12/playwithroslyn_0.png" alt="Criando uma aplicação console" class="img-responsive center-block">

<p>
    Uma vez que aplicação está criada, vou adicionar o Roslyn ao projeto
    utilizando o Nuget (lembre-se que como o Roslyn é um Prerelease, isso
    deve ser considerado isso na pesquisa (-Prerelease option)).
</p>

```
Install-Package -Prerelease Microsoft.CodeAnalysis.CSharp
```

<p>
    Para começar a brincadeira nesta época de mega sena da virada,
    digamos que o código que deve ser compilado seja parecido com a classe abaixo.
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
    Certo. Agora na classe <code>Program</code> da aplicação que estou fazendo as brincadeiras, vou criar um 
    um método (<code>CodeToCompile</code>) cuja responsabilidade é retornar a <code>string</code> com o código que deve ser compilado.
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
    Feito isso, vou colocar o Roslyn para trabalhar com base nesta string que contém o código de uma classe.
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
    No método <code>main</code>, a primeira linha gera a árvore de syntax com base no código que
    deve ser compilado. Depois cria o que é chamado de compilação (passando o nome do assembly como parâmetro),
    adiciona a árvore de syntax e, por fim, o código faz um loop nos diagnósticos gerados pela compilação escrevendo na saída padrão cada um deles. 
</p>

<p>
    A saída gerada pela execução do programa é parecida com a figura abaixo.
</p>

<img src="{{ site.url }}/img/2014-12/playwithroslyn_1.png" alt="Diagnósticos da compilação com Roslyn." class="img-responsive center-block">

<p>
    <b>O que aconteceu?</b> Pela análise dos diagnósticos pode-se perceber que falta uma referência. Neste caso especificamente falta referenciar a <b>mscorlib</b>. Vou adicionar a referência e analisar a saída novamente.
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
    O código é bem direto. Ele pega a referência com base em um assembly (que foi encontrado com base em um tipo) e adiciona na compilação (<code>AddReferences</code>). 
</p>

<p>
    A nova saída ainda apresenta um problema, mas ficou bem melhor.
</p>

<img src="{{ site.url }}/img/2014-12/playwithroslyn_2.png" alt="Diagnósticos da compilação com Roslyn (segunda tentativa)." class="img-responsive center-block">

<p>
O problema agora se refere ao tipo do projeto gerado pela compilação. A compilação está esperando um ponto de entrada, o que para este exemplo não encaixa muito bem. Sendo assim, vou fazer uma terceira modificação que fará com que a compilação gere uma <b>class library</b>.
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
O construtor da classe <code>CSharpCompilationOptions</code> recebe uma pancada (e bota pancada nisso!) de parâmetros, mas o Único obrigatório é o <code>outputKind</code>, que define o tipo de saída da compilação. Sendo assim, a terceira versão do código cria uma instância para definir as opções e a passa para a compilação. Com isso, a lista de diagnósticos estará vazia na próxima execução do programa.
</p>

<p>
Bom, era isso. No próximo artigo desta série vou continuar exatamente deste ponto e estender um pouco este exemplo.
</p>

<p>
    Até mais!
</p>

<a href="https://github.com/mfpalladino/PlayWithRoslyn" title="Código fonte utilizado no artigo" target="_blank"><img src="{{ site.url }}/img/Octocat.jpg" alt="Código fonte utilizado no artigo" class="img-responsive center-block" style="cursor:pointer;"></a> 
