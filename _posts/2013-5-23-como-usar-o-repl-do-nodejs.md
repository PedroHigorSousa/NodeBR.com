---
layout: post
title : Como usar o REPL do Node.js
description: Como o REPL (Read–eval–print loop) do Node.js pode ser utilizado
author:
  name: Rafael Henrique Moreira
  email: rafadev7@gmail.com
  url: http://rafadev.com/
  github: rafadev7
  twitter: rafadev7
tags : [conceito, REPL]
---
O Node.js vem com um REPL ([Read-Eval-Print Loop][]), que é um programa simples e interativo que lê expressões ou trechos de programa, avalia (ou executa) e imprime o resultado. Este é o consolo do Node.js e qualquer código JavaScript válido que pode ser escrito em um script pode ser passado para o REPL. Ele pode ser extremamente útil para experimentar o Node.js, debugar códgio, e descobrir alguns dos comportamentos mais excêntricos do JavaScript.

Para rodar é simples, basta rodar o node no console sem inserir um nome de arquivo na frente: <code>node</code>. Lembrando que para rodar um servidor node você teria que passar o arquivo do servidor como parâmetro, por exemplo: <code>node servidor.js</code>.

Executando o node usando o comando <code>node</code> leva você para um simples console <code>></code> onde você pode escrever qualquer comando JavaScript que desejar. Como na maioria dos prompts você pode usar as setas para cima e para baixo para pelo seu histórico de comandos e modificar comandos anteriores. No REPL você também pode usar a tecla Tab para fazer o REPL tentar auto-completar o comando.

Sempre que você digitar um comando o REPL vai imprimir o valor de retorno do comando. Se você quer reusar o resultado do comando anterior você pode usar a variável especial <code>_</code>.

Por exemplo:

{% highlight javascript %}
node
> 1+1
2
> _+1
3
{% endhighlight %}

Uma coisa importante para observar é onde os valores de retorno do REPL estão interessados:

{% highlight javascript %}
> x = 10
10
> var y = 5
> x
10
> y
5
{% endhighlight %}

Quando a palavra-chave <code>var</code> não é usada o valor da expressão é armazenado e retornado.
Quando a palavra-chave <code>var</code> é usada o valor da expressão é armazenado, mas não retornado.

Se você precisa acessar qualquer módulo embutido, ou qualquer módulo de terceiros, ele pode ser acessado com a função <code>require</code>, assim como é feito num script Node.

{% highlight javascript %}
node
> path = require('path')
{ resolve: [Function],
  normalize: [Function],
  join: [Function],
  dirname: [Function],
  basename: [Function],
  extname: [Function],
  exists: [Function],
  existsSync: [Function] }
> path.basename("/a/b/c.txt")
'c.txt'
{% endhighlight %}

Note novamente que sem a palavra-chave <code>var</code>, o conteúdo do objeto é retornado imediatamente e imprimido no <code>stdout</code>.

O node possui alguns módulos embutidos, como o módulo <code>console</code> que contém funções úteis e pode ser usado sem precisar ser importado. Ao se digitar <code>console</code> no REPL do node ele retorna todas as funções públicas deste módulo.

{% highlight javascript %}
> console
{ log: [Function],
  info: [Function],
  warn: [Function],
  error: [Function],
  dir: [Function],
  time: [Function],
  timeEnd: [Function],
  trace: [Function],
  assert: [Function] }
{% endhighlight %}

E ao se utilizar a função <code>log</code> deste módulo nós temos:

{% highlight javascript %}
> console.log("Imprima este texto")
Imprima este texto
undefined
{% endhighlight %}

É interessante observar que o texto foi impresso no console, conforme o esperado, porém a função <code>console.log("Imprima este texto")</code> não tem valor de retorno, e por isso o REPL imprime undefined na linha seguinte. 

[Read-Eval-Print Loop]: http://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop