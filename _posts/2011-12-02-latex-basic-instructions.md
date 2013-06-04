---
layout: post
title: 底层命令解释
categories: [LaTeX]
tags: [LaTeX, basic instructions]
---

- [判断某个命令是否已经用过](http://bbs.ctex.org/viewthread.php?tid=68913)

> 1. 判断是否已经定义用`\ifdefined`或者`\ifcsname`，如果没有eTeX支持也可以用`\ifx\foo\undefined`或者 LaTeX 内核的`\@ifundefined`。  
> 1. 判断是否用过一遍，可以在\foo的定义中设置一个全局变量，然后在后面检测。

- [`\let`和`\xdef`有什么区别？](http://bbs.ctex.org/viewthread.php?tid=65712)

> `\xdef`把定义中的内容完全展开，用来定义一个宏；`\let`让新宏与旧宏意义相同。`\xdef`就是`\global\edef`。`\let`没有`\global`的意思。

{% highlight latex %}
\def\a{foo}
\def\b{\a}
\edef\c{\b} 得到的是 \c -> foo
\let\d\b    得到的是 \d -> \a
{% endhighlight %}

一个外链：[What is the difference between \let and \edef](http://tex.stackexchange.com/questions/8163/what-is-the-difference-between-let-and-edef)

- [\renewcommand`*`的作用](http://bbs.ctex.org/viewthread.php?tid=4520)

> `\renewcommand`所带参数可以包含用\par或空行表示的新段落；  
> `\renewcommand*`不行

- [`\string`的作用](http://bbs.ctex.org/viewthread.php?tid=64550)

> 将一个命令输出为带斜杠的字符串。

- [`\expandafter`的作用](http://bbs.ctex.org/viewthread.php?tid=4520>)

> 让制控命令顺序颠倒过来，后面的命令先起作用，下边是一个证明的例子：

{% highlight latex %}
\def\test{9999}
\makeatletter
\def\testt#1#2#3#4{\@alph{#1}\@Alph{#2}\@Roman{#3}\@roman{#4}}
\makeatother
\expandafter\testt\test
{% endhighlight %}

如果不加\expandafter的话：

{% highlight latex %}
\testt\test
{% endhighlight %}

就会出错。