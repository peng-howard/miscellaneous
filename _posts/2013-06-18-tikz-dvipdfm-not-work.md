---
layout: post
title: (转贴) latex+dvipdfmx编译pgf图形无效的解决方法
categories: [LaTeX]
tags: [LaTeX, pgf]
---

原文地址：<http://bbs.ctex.org/forum.php?mod=viewthread&tid=76106&extra=&page=1>

> 最好的方法是升级expl3宏包

{% highlight latex %}
\documentclass[cs4size,openany,twoside,UTF8]{ctexbook}
\usepackage[]{graphicx}

\def\pgfsysdriver{pgfsys-dvipdfm.def}

\usepackage{tikz}

\begin{document}
\begin{tikzpicture}
\draw (2,2) circle (10ex);
\end{tikzpicture}
\end{document}
{% endhighlight %}