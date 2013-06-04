---
layout: post
title: Math version `bold' is not defined
categories: [LaTeX]
tags: [Mathtime, LaTeX]
---

使用Y & Y Mathtime字体，用XeLaTeX编译，提示：

    “Error: Math version `bold' is not defined.”

我的解决，在导言区添加：
{% highlight latex %}
\DeclareMathVersion{bold}
{% endhighlight %}