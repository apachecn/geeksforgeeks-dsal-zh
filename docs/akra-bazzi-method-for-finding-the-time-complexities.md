# 求时间复杂度的阿卡拉-宝宝方法

> 原文:[https://www . geesforgeks . org/akra-bazzi-寻找时间的方法-复杂性/](https://www.geeksforgeeks.org/akra-bazzi-method-for-finding-the-time-complexities/)

[大师定理](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)是一种解决时间复杂性重现的流行方法，形式如下:

> ![T(n) = aT(\frac{n}{b}) + f(n) ](img/5e12c87852aac6aa180bf88ded3bb4c4.png "Rendered by QuickLaTeX.com")

对 a，b 和 f(n)有约束。递推关系式限制了马斯特定理的可用性。下面是三个不能用 master 定理直接解决的循环:

1.  ![\large{T(n) = 3T(\frac{n}{5}) + 2T(\frac{n}{5}) + \theta(n)}](img/df2ddc06ffaaa816e31953c52490e6ac.png "Rendered by QuickLaTeX.com")
2.  ![\large{T(n) = \frac{1}{3}T(\frac{n}{3}) + \theta(\frac{1}{n})}](img/160bed47a067c696c46fbe58a5c9931a.png "Rendered by QuickLaTeX.com")
3.  ![\large{T(n) = 9T(\frac{n}{3}+\log n) + \theta(n)}](img/00abcc390f3ce6dd5477847854a534ea.png "Rendered by QuickLaTeX.com")

**<u>阿卡拉-宝宝法</u> :** 本文探讨了另一种解决此类复发的方法，该方法是由**穆罕默德·阿卡拉**和**卢埃·宝宝**在 **1998** 中开发的。阿卡拉-宝宝方法可以应用于下列形式的重现:

> ![T(n)=\sum_{i=1}^{k} a_{i} T(b_{i}n+h_{i}(n))+g(n)](img/ed69f8bfcfcc1cb10c19afd4ad4ef766.png "Rendered by QuickLaTeX.com")

其中，![a_{i}   ](img/c0b2abc1a6f4a50b3a674330a13c178b.png "Rendered by QuickLaTeX.com")和![b_{i}   ](img/b694c1dc0086a492fffc79c8c4a54b87.png "Rendered by QuickLaTeX.com")是常数，这样:

> 1.  ![\ a_{i}>0](img/ededd1d8c5741140727e099d039a72de.png "Rendered by QuickLaTeX.com")
> 2.  ![\ 0<b_{i}<1 \textnormal{ i.e. in the range (0, 1)}](img/12baae9a448e6102b031dcc8823c38d7.png "Rendered by QuickLaTeX.com")
> 3.  ![\ g(n)\ \epsilon\ O(n^{c}) \textnormal{ i.e. }g(n) \textnormal{ must have a polynomial upperbound}](img/71f14557f6c78493623abf39f7f61669.png "Rendered by QuickLaTeX.com")
> 4.  ![\ h_{i}(x)\ \epsilon\ O(\large\frac{n}{(logn)^{2}}\normalsize)](img/ff26c6c3258882e3548296cc52e4ed43.png "Rendered by QuickLaTeX.com")

接下来，找到 p，这样

> ![\large{\sum_{i=1}^k a_ib_i^p=1}   ](img/e7ca493b427ba07bb7ce83d66f909801.png "Rendered by QuickLaTeX.com")

然后

> ![\large{T(n)\epsilon\ \theta(n^{p}(1+\int_{1}^{n}\frac{g(u)}{u^{p+1}}du))}](img/1275000f4ae1439774efe168489671f4.png "Rendered by QuickLaTeX.com")

**示例**
让我们考虑上面讨论的三个循环，并使用以下方法解决它们:

**实施例 1。**

![\large{T(n) = 3T(\frac{n}{5}) + 2T(\frac{n}{5}) + \theta(n)}](img/df2ddc06ffaaa816e31953c52490e6ac.png "Rendered by QuickLaTeX.com")

这里

> 1.  a <sub>1</sub> = 3
> 
> <sub>1</sub>
> 
> ![\large \frac{1}{5}](img/a113a332a7f4c2270123b829200b2363.png "Rendered by QuickLaTeX.com")
> 4.  a <sub>2</sub> = 2
> 5.  b <sub>2</sub> = ![\large \frac{1}{5}](img/a113a332a7f4c2270123b829200b2363.png "Rendered by QuickLaTeX.com")
> 
> <sub>1</sub>
> 
> <sub>2</sub> 
> 
> 8.  G(n) = \theta(n), that is

在这个问题中，h <sub>1</sub> (n)和 h <sub>2</sub> (n)不存在。
这里 p=1 满足

> ![3*\large {\frac{1}{5}^p}\normalsize +2*\large {\frac{1}{5}^p}\normalsize=1.](img/9f1b27805b3f1fbc6e8b58969f38db95.png "Rendered by QuickLaTeX.com")

最后，

> => ![n^{1}(1+\int_{1}^{n}\large\frac{u}{u^{1+1}}\normalsize du)](img/2d2ecd65251bca7bfa0bb7298e90fe95.png "Rendered by QuickLaTeX.com")
> 
> => ![n(1+\log{n}-\log{1})](img/71f626aebde252f10036b0b54d5fb019.png "Rendered by QuickLaTeX.com")
> 
> => ![n+n\log{n}](img/8e3530871bf9debaf368c1f2888dc0a9.png "Rendered by QuickLaTeX.com")
> 
> => ![\theta(n\log{n})](img/f93cd656510417d871b9403feaa05cce.png "Rendered by QuickLaTeX.com")

**例 2。**

![\large{T(n) = \frac{1}{3}T(\frac{n}{3}) + \theta(\frac{1}{n^{2}})}](img/1d0284e975d6e63f7880e9fa60e5f298.png "Rendered by QuickLaTeX.com")

这里

> 1.  a = ![\large \frac{1}{3} ](img/a7c70f0d3cc60e18945d020116bcb83e.png "Rendered by QuickLaTeX.com")
> 2.  b = ![\large \frac{1}{3}        ](img/879bd8a69a9df937841324a6a02128a1.png "Rendered by QuickLaTeX.com")
> 3.  g(n)= ![\theta(n^2)  ](img/39f442cd6cb5718131f4f91a43f12ff7.png "Rendered by QuickLaTeX.com")
> 4.  B is in the range (0,1)
> 5.  G (n) = \ theta (n 2), that is, in o (n <sup>c</sup> , where c can be 1.

在这个问题中 h(n)不存在。
这里 p =–1 满足

> ![\large\frac{1}{2}\normalsize*\large\frac{1}{2}^p\normalsize=1](img/8b428eae3f758d078b16db9867575254.png "Rendered by QuickLaTeX.com")

最后，

> => ![n^{-1}(1+\int_{1}^{n}\large\frac{\frac{1}{u}}{u^{-1+1}}\normalsize du)](img/e3bb742a5ffecd68d09135088897cc84.png "Rendered by QuickLaTeX.com")
> 
> => ![\large\frac{1}{n}\normalsize(1+\int_{1}^{n}\large\frac{1}{u}\normalsize du)](img/c707536c5067bb5f9ec091ae00df214d.png "Rendered by QuickLaTeX.com")
> 
> => ![\large\frac{1}{n}\normalsize(1+[\log u]_{1}^{n})](img/cfb35ba4c3147e6c404c47fa8d16c88c.png "Rendered by QuickLaTeX.com")
> 
> => ![\large\frac{1}{n}\normalsize(1+\log n)](img/95f813fe6e1850b113488832db29383c.png "Rendered by QuickLaTeX.com")
> 
> => ![\theta(\large\frac{\log n}{n}\normalsize)](img/57eacb7f88b40337b7963115ec41a0ca.png "Rendered by QuickLaTeX.com")

**例 3。**

![\large{T(n) = 9T(\frac{n}{3}+\log n) + \theta(n)}](img/00abcc390f3ce6dd5477847854a534ea.png "Rendered by QuickLaTeX.com")

这里

> 1.  a = 9
> 2.  b = ![\large\frac{1}{3}         ](img/c8cc4ec6a394ed491ecb91b5384ef176.png "Rendered by QuickLaTeX.com")
> 3.  g(n)= \θ(n) ![\theta(n)](img/5ef7819472951bfb19db25cbf39587ae.png "Rendered by QuickLaTeX.com")
> 4.  B is in the range (0,1)
> 5.  G (n) = ![\theta(n)    ](img/0cf65f518bd15e6929bc764bf0a65232.png "Rendered by QuickLaTeX.com") that is, o (n) <sup>c</sup> , where c can be 1.
> 6.  H (n) = ![\log{n}   ](img/c4803ec4001e60013f5dc031b68331a5.png "Rendered by QuickLaTeX.com"), that is, ![O(\large\frac{n}{(logn)^{2}}\normalsize)        ](img/fcae01d943d784b0dd0fbeb7a739569a.png "Rendered by QuickLaTeX.com")

这里 p=2 满足

> ![9*\large\frac{1}{3}^p\normalsize=1](img/6cab242da348fe00623d67171a6e8f87.png "Rendered by QuickLaTeX.com")

最后，

> => ![n^{2}(1+\int_{1}^{n}\large\frac{u}{u^{2+1}}\normalsize du)](img/bc41d17b660215e259d1c00a8f0588ee.png "Rendered by QuickLaTeX.com")
> 
> => ![n^{2}(1+\int_{1}^{n}\large\frac{1}{u^{2}}\normalsize du)](img/505d0ab25a40d541bfef68c520a7a05e.png "Rendered by QuickLaTeX.com")
> 
> => ![n^{2}(1+[-\large\frac{1}{u}\normalsize]_{1}^{n})](img/7f094fce742783c34cc8e79ce534beba.png "Rendered by QuickLaTeX.com")
> 
> => ![n^{2}(2-\large\frac{1}{n}\normalsize)](img/11b2fc0b63ddac15f38be560bc58419d.png "Rendered by QuickLaTeX.com")
> 
> => ![2n^{2}-n](img/5d7a381b1d7c03c84bb4542581787df9.png "Rendered by QuickLaTeX.com")
> 
> => ![\theta(n^{2})](img/ea18d87905ee3d97e95fb6238623b667.png "Rendered by QuickLaTeX.com")

**优势:**

*   适用于许多分治算法。
*   对递归格式的约束比 Master 定理小。
*   对于复杂的递推关系，可以用数值方法计算 p。

**缺点:**

*   当 g(n)的增长不是有界多项式时不起作用。例如 **g(N) = 2 <sup>N</sup>** 。
*   不处理天花板和地板功能。