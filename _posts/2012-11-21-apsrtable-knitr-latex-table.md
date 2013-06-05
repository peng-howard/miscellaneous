---
layout: post
title: apsrtable在knitr中生成LaTeX表格
categories: [LaTeX, r]
tags: [LaTeX, knitr, apsrtable, 表格]
---

原文地址：<http://cos.name/cn/topic/108631>

`apsrtable()`里有个`Sweave`参数，若设为`TRUE`，则生成`tabular`环境，若为默认的`FALSE`，则为`table`环境。

{% highlight latex %}
\begin{table}[htbp]
\caption{some text}
\label{tb:ex}
\centering
<<results='asis'>>=
apsrtable(mod1, mod2, mod3, Sweave = TRUE)
@
\end{table}
{% endhighlight %}

> Yihui: 这大概就是最好的办法了吧……这参数名干嘛非得叫`Sweave`，明明意思是`tabular.only`。