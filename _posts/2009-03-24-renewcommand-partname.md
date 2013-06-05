---
layout: post
title: renewcommand partname时的问题
categories: [LaTeX]
tags: [LaTeX, Beamer]
---


在documentclass为book时解决方法如下：

{% highlight latex %}
\documentclass[a4paper]{book}
\usepackage{ctex,CJKnumb}
\renewcommand\thepart{}\renewcommand\partname{第\CJKnumber{\arabic{part}}部分}
\begin{document}
\begin{CJK*}{GBK}{xihei}
\part[asfd]{test asdf}
asdf asdfasfd
\end{CJK*}
\end{document}
{% endhighlight %}

在documentclass为beamer时解决方法如下(该方法由黄正华老师提供，但要注意选择不同的theme时，要根据实际情况改变partpage中beamercolorbox的具体参数，换句话说，这个解决方法与上面的方法不同，它不具有通用性)：

{% highlight latex %}
\documentclass[CJK]{beamer}
\usepackage{CJK,CJKnumb}
\usetheme{Madrid}
\begin{document}
\begin{CJK*}{GBK}{kai}
\renewcommand\partname{第\CJKnumber{\value{part}}部分}
\defbeamertemplate*{part page}{mypartpage}[1][] { \begin{centering} {\usebeamerfont{part name}\usebeamercolor[fg]{part name}\partname} \vskip1em\par \begin{beamercolorbox}[rounded=true,shadow=true,sep=8pt,center,#1]{part title} \usebeamerfont{part title}\insertpart\par \end{beamercolorbox} \end{centering} }
\setbeamertemplate{part page}[mypartpage][]
\title{test}
\date{}
\part[asfd]{test asdf}
\frame{\partpage}
\end{CJK*}
\end{document}
{% endhighlight %}