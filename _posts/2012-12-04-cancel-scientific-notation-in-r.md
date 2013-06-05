---
layout: post
title: R中如何取消科学计数法
categories: [r]
tags: []
---

原文地址：<http://bbs.pinggu.org/thread-1403060-1-1.html>

> R应该会自动的把太大和太小的数用科学计数法来表示，一般的数应该就是直接表示吧。

{% highlight r %}
> 10^seq(1:5)
[1] 1e+01 1e+02 1e+03 1e+04 1e+05
> options(scipen=200)
> 10^seq(1:5)
[1]     10    100   1000  10000 100000
{% endhighlight %}