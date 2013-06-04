---
layout: post
title: CTeX 2.9.0.152下Beamer中使用theorem环境出错的解决方法
categories: [LaTeX]
tags: [Beamer, theorem]
---

原文地址：<http://hi.baidu.com/zjunmm/blog/item/0915d010d7ce2d175aaf53d1.html>

CTeX 2.9.0.152 下在 Beamer 中使用 `theorem`, `definitioin` 环境会出错：


    ! Undefined control sequence.
    \trans@languagepath ->\languagename
                                        ,English
    l.226 \end{frame}

解决方法有两种：

* 在导言区添加 `\usepackage[english]{babel}`;
* 在线升级到最新版本。
