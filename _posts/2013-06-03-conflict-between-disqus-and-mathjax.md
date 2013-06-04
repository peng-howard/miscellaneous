---
layout: post
title: Disqus与Mathjax可能有冲突
categories: [feelings]
tags: [Disqus, Mathjax, kramdown]
---

在系统中添加Mathjax支持的时候，发现如果LaTeX公式与Disqus评论系统同时存在，会导致如下的错误

> This page is forcing your browser to use legacy mode, which is not compatible with Disqus. Please see our troubleshooting guide to get more information about this error.

这个错误在IE8.0中出现，但在Firefox 21中却不存在，初步怀疑是Mathjax调用Mootools 1.4.5而导致，具体见<http://wordpress.org/support/topic/disqus-browser-legacy-error>。