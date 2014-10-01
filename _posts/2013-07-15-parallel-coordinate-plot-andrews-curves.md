---
layout: post
title:  (转) 调和曲线图和轮廓图的比较
categories: [统计]
tags: [调和曲线图, 轮廓图, 平行坐标图, 安德鲁曲线图]
---

原文地址：[http://cos.name/2009/03/parallel-coordinates-and-andrews-curve/#more-704](http://cos.name/2009/03/parallel-coordinates-and-andrews-curve/#more-704)

作者：[魏太云](http://taiyun.cos.name	)

多元数据的可视化方法很多，譬如散点图、星图、雷达图、脸谱图、协同图等，大致可分为以下几类：

1. 基于点（如二维、三维散点图）；
2. 基于线（如轮廓图、调和曲线图）；
3. 基于平面图形（如星图、雷达图、蛛网图）；
4. 基于三维曲面（如三维曲面图）。

其思想是将高维数据映射到低维空间（三维以下）内，尽量使信息损失最少，同时又能利于肉眼辨识。调和曲线图和轮廓图(即平行坐标图)都是多元数据的可视化方法，它们基于“线”的形式，将多元数据表示出来，对于聚类分析有很好的帮助。

## 轮廓图

轮廓图的思想非常简单、直观，它是在横坐标上取$$p$$个点，依次表示各个指标(即变量)；横坐标上则对应各个指标的值(或者经过标准化变换后的值)，然后将每一组数据对应的点依次连接即可。

`lattice`包中的`parallel()`函数可以轻松绘出轮廓图。利用`iris`数据，以下代码可以画出其轮廓图。

{% highlight r %}
library(lattice)
data(iris)
parallel(~iris[1:4], iris, groups = Species,
    horizontal.axis = FALSE, scales = list(x = list(rot = 90)))
{% endhighlight %}

![Iris 数据的轮廓图(Parallel Coordinate Plots)](https://cssdpq.bn1.livefilestore.com/y2pvkki2cktl093Pl_BxKM-ZZ8RQ_u-6xQnlTubo23_SXYLGCCLvKy0HTC_tR7UpgB_1h5cVOsZCiZvi7rLWzq2ydWmMGy9_4byGLUhP5db-MQ/Iris%20%E6%95%B0%E6%8D%AE%E7%9A%84%E8%BD%AE%E5%BB%93%E5%9B%BE(Parallel%20Coordinate%20Plots).png?psid=1)

<p style="text-align: center">图1 Iris 数据的轮廓图(Parallel Coordinate Plots)</p>

观察上图，可以发现同一品种的鸢尾花的轮廓图粗略地聚集在一起。

## 调和曲线图

调和曲线图的思想和傅立叶变换十分相似，是根据三角变换方法将$$p$$维空间的点映射到二维平面上的曲线上。假设$$X_r$$是$$p$$维数据的第$$r$$个观测值，即

$$X_r^T=(x_{r1},\dotsc,x_{rp})$$

则对应的调和曲线是

$$f_r(t)=\frac{x_{r1}}{\sqrt{2}} +x_{r2}\sin t+x_{r3}\cos t+x_{r4}\sin 2 t+x_{r5} \cos 2 t+\cdots$$

其中$$-\pi\leqslant t\leqslant \pi$$.

同样利用`iris`数据，下面代码(主要取自《统计建模与R软件》，尚未优化)可以画出其调和曲线图

{% highlight r %}
x = as.matrix(iris[1:4])
t = seq(-pi, pi, pi/30)
m = nrow(x)
n = ncol(x)
f = matrix(0, m, length(t))
for (i in 1:m) {
    f[i, ] = x[i, 1]/sqrt(2)
    for (j in 2:n) {
        if (j%%2 == 0)
            f[i, ] = f[i, ] + x[i, j] * sin(j/2 * t)
        else f[i, ] = f[i, ] + x[i, j] * cos(j%/%2 * t)
    }
}
plot(c(-pi, pi), c(min(f), max(f)), type = "n", main = "The Unison graph of Iris",
    xlab = "t", ylab = "f(t)")
for (i in 1:m) lines(t, f[i, ], col = c("red", "green3",
    "blue")[unclass(iris$Species[i])])
legend(x = -3, y = 15, c("setosa", "versicolor", "virginica"),
    lty = 1, col = c("red", "green3", "blue"))
{% endhighlight %}

![Iris 数据的调和曲线图](https://cssdpq.bn1.livefilestore.com/y2pi1WtDEA1hzK6vfvFjDtdWP9FS4yzejGHptqXptD2HA1txjcmsmQ74JW_wF-AeYh1Yo0JpecJafME8aKbO5FF3eAyxPV_kSs2HAA-2jH6ZdI/Iris%20%E6%95%B0%E6%8D%AE%E7%9A%84%E8%B0%83%E5%92%8C%E6%9B%B2%E7%BA%BF%E5%9B%BE.png?psid=1)

<p style="text-align: center">图2 Iris 数据的调和曲线图</p>

观察上图，同样可以发现同一品种鸢尾花数据的调和曲线图基本上扭在一起。同第一幅图比较后，发现第二幅图更加清楚明白，事实上Andrews证明了调和曲线图有许多良好性质。

## 讨论

轮廓图和调和曲线图有着相近的功能，而技巧大有不同。轮廓图简单却现得粗糙，调和曲线图公式复杂却十分精细。从这一个侧面可以发现直观的统计思想固然重要，但存在很多种不可能通过直观思想得到的、而又非常精细、美妙的方法，此时倍受众多统计学家责难的数学显得优雅而又强大。

<hr />

> **谢益辉**：正好我前一段时间也写过一个调和曲线图的R函数，发出来分享一下：
{% highlight r %}
andrews.curve = function(x, n = 101, type = "l", lty = 1, 
    lwd = 1, pch = NA, xlab = "t", ylab = "f(t)", ...) {
    p = ncol(x)
    if (is.null(p)) 
        stop("'x' must be a matrix or data.frame!")
    if (p < 1) 
        stop("'x' must have at least one column!")
    theta = matrix(seq(-pi, pi, length.out = n), nrow = n, ncol = 1)
    if (p == 1) {
        a = matrix(x/sqrt(2), nrow = n, ncol = nrow(x), byrow = TRUE)
    }
    if (p > 1) {
        b = matrix(rep(1:(p/2), each = 2, length.out = p - 1), 
            nrow = 1, ncol = p - 1)
        a = cbind(1/sqrt(2), sin(theta %*% b + matrix(rep(c(0, 
            pi/2), length.out = p - 1), nrow = n, ncol = p - 
            1, byrow = TRUE))) %*% t(x)
    }
    matplot(theta, a, type = type, lty = lty, lwd = lwd, pch = pch, 
        xlab = xlab, ylab = ylab, ...)
}
{% endhighlight %}

> 里面都是以矩阵的形式做的运算，不过我没有测试，不知道速度会不会快一些。对于调和曲线图，观测$$X_i$$和$$X_j$$的欧式距离正好是曲线垂直距离的积分，这是数学性质和图形性质能够结合的关键。
<hr />
> **魏太云**：快很多呢，没有一个显式循环，十分方便:)。调和曲线图的确很好地将数学融进了图形，可谓鬼斧神工啊。
<hr />
> **fasterr**：`andrews.curve(x, col=c(‘red’, ‘green3′, ‘blue’))`可是画出来的不是很一样：《统计建模与R软件》版的调和曲线的颜色比较友好，相近族类的颜色一样、不同类的颜色不同。
> `andrews.curve()`绘制的曲线颜色是是交替的（一次red，一次green3, 一次blue，依次循环使用），而不是颜色按类聚集，这样画出来的色彩整体很凌乱（颜色重叠后就更变味了）。
> 传入什么控制参数`andrews.curve()`也能得到一样的效果么？