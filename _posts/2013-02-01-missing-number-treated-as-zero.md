---
layout: post
title: 导致“Missing number, treated as zero”的原因
categories: [LaTeX]
tags: []
---

从<http://web.mit.edu/ghudson/dev/nokrb/third/tetex/texmf/doc/help/faq/uktug-faq/FAQ271.html>给出的结果看，遇到如下的情况时：

    ! Missing number, treated as zero.
    
                       \relax
    l.21 \begin{Ventry}{Return values}

很可能添加`calc`宏包的支持就可能可以解决问题，至少我确实解决了。