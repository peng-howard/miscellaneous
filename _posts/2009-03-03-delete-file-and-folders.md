---
layout: post
title: 无法删除文件或文件夹的处理
categories: [PC skills]
tags: []
---

在删除文件或文件夹时，windows系统错误提示：`无法删除****，找不到指定文件，请确定指定的路径及文件名是否正确`的解决方法……

经常有人会碰到这个问题，网上找了很多版本的解决方法都没有用，用一些360文件粉碎，优化大师粉碎也不行，但这一个方法需非常有效，一试就成功，收藏下来。

具体方法如下，请一步步进行，一定可以解决你的难题。

1. 启用一个cmd；
1. 到要删除的文件(夹)的上一层目录下；
1. 运行命令：`dir /x`，然后记下要删除的文件(夹)对应行的第三列(记作 比如：`alixixi~com`)；
1. 如果是文件，输入：`del alixixi~com`(就是刚才记得东西)，是文件夹就输入：`rd alixixi~com`；

大功告成！