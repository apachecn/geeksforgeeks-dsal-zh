# 堆一堆的时间复杂度

> 原文:[https://www . geeksforgeeks . org/时间-构建堆的复杂性/](https://www.geeksforgeeks.org/time-complexity-of-building-a-heap/)

考虑以下构建输入数组 a 的堆的算法

```
BUILD-HEAP(A) 
    heapsize := size(A); 
    for i := floor(heapsize/2) downto 1 
        do HEAPIFY(A, i); 
    end for 
END

```

快速浏览一下上面的算法，运行时间是![O(nlg(n))](img/0e90feccc7d9b3839949061208750e8f.png "Rendered by QuickLaTeX.com")，因为每次调用 **Heapify** 都要花费![O(lg(n))](img/c26fb598ebdcc1ddf3eb71986043967f.png "Rendered by QuickLaTeX.com")和 **Build-Heap** 进行![O(n)](img/d5229a9c6f59029cbbb0f53974c9a9de.png "Rendered by QuickLaTeX.com")这样的调用。
这个上限虽然正确，但并不是渐近紧的。

我们可以通过观察 **Heapify** 的运行时间依赖于树‘h’的高度(等于 lg(n)，其中 n 是节点数)并且大多数子树的高度都很小，从而推导出一个更紧的界限。
随着我们沿着树向上移动，高度“h”增加。**构建堆**的第 3 行从最后一个内部节点(heapsize/2)的索引(高度=1)到根(1)的索引(高度= lg(n))运行一个循环。因此， **Heapify** 对于每个节点花费不同的时间，这就是![O(h)](img/5ea649628e229a0c734485ed62358dae.png "Rendered by QuickLaTeX.com")。

为了找到构建堆的时间复杂度，我们必须知道高度为 h 的节点数量
为此，我们使用了这样一个事实，即大小为 n 的堆最多有高度为 h 的![\left \lceil \frac{n}{2^{h+1}} \right \rceil ](img/f1480712396aef5de95d97d53fe81586.png "Rendered by QuickLaTeX.com")个节点

现在为了推导时间复杂度，我们将**构建-堆**的总成本表示为-

(1) ![ \begin{flalign*} T(n) &= \sum_{h = 0}^{lg(n)}\left \lceil \frac{n}{2^{h+1}} \right \rceil * O(h)\\ &= O(n * \sum_{h = 0}^{lg(n)}\frac{h}{2^{h}})\\ &= O(n * \sum_{h = 0}^{\infty}\frac{h}{2^{h}})\\ \end{flalign*} ](img/cbd2925ff24ada11e6e75a2b986de743.png "Rendered by QuickLaTeX.com")

步骤 2 使用 Big-Oh 符号的属性来忽略上限函数和常数 2( ![2^{h+1} = 2.2^h](img/14f0bceb6dd1248dcd9aa1909190ad6d.png "Rendered by QuickLaTeX.com"))。类似地，在第三步中，求和的上限可以增加到无穷大，因为我们使用的是大-哦符号。

无限 G.P 之和(x < 1)

(2) ![ \begin{align*} \sum_{n = 0}^{\infty}{x}^{n} = \frac{1}{1-x} \end{align*} ](img/8c2f41a655a02f1d252a05e5857c0b40.png "Rendered by QuickLaTeX.com")

微分两边，乘以 x，我们得到

(3) ![ \begin{align*} \sum_{n = 0}^{\infty}n{x}^{n} = \frac{x}{(1-x)^{2}} \end{align*} ](img/0fefa5a19ec94df082bd6d10219bd4a9.png "Rendered by QuickLaTeX.com")

将(3)中得到的结果放回推导(1)中，我们得到

(4) ![ \begin{flalign*} &= O(n * \frac{\frac{1}{2}}{(1 - \frac{1}{2})^2})\\ &= O(n * 2)\\ &= O(n)\\ \end{flalign*} ](img/7e3bb5625ab8141c14374aab08c29e7f.png "Rendered by QuickLaTeX.com")

因此证明了建立二进制堆的时间复杂度是![O(n)](img/d5229a9c6f59029cbbb0f53974c9a9de.png "Rendered by QuickLaTeX.com")。

**参考:**T2[http://www.cs.sfu.ca/CourseCentral/307/petra/2009/SLN_2.pdf](http://www.cs.sfu.ca/CourseCentral/307/petra/2009/SLN_2.pdf)

本文由**奇拉·曼瓦尼**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。