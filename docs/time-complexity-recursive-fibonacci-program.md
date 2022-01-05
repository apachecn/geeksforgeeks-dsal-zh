# 递归斐波那契程序的时间复杂度

> 原文:[https://www . geesforgeks . org/时间-复杂性-递归-斐波那契-程序/](https://www.geeksforgeeks.org/time-complexity-recursive-fibonacci-program/)

[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)是以下整数序列中的数 0，1，1，2，3，5，8，13……
数学上斐波那契数可以用下面的递归公式来写。

```
For seed values F(0) = 0 and F(1) = 1
F(n) = F(n-1) + F(n-2)

```

在继续阅读本文之前，请确保您熟悉[程序中讨论的斐波那契数列](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的递归方法

**递归斐波那契程序分析:**
我们知道斐波那契的递归方程是![T(n)](img/5a3721c914e82a59126415e55f9b2e5c.png "Rendered by QuickLaTeX.com") = ![T(n-1)](img/c264d5bbf33368a2aa7bf0465491a382.png "Rendered by QuickLaTeX.com") + ![T(n-2)](img/7bb89bac84faa87ca9e7f1d366ce7e8a.png "Rendered by QuickLaTeX.com") + ![O(1)](img/db6b8ec76c84546c6b00e1bc2a0fdbd1.png "Rendered by QuickLaTeX.com")。
这意味着，计算 fib(n)所花费的时间等于计算 fib(n-1)和 fib(n-2)所花费的时间之和。这也包括执行前面加法的恒定时间。

在求解上述递归方程时，我们得到斐波那契的上限为![O(2^n)](img/5bd5792b97ac09c3011b71e9309734ec.png "Rendered by QuickLaTeX.com")，但这不是严格的上限。斐波那契可以用数学方法表示为线性递归函数，这一事实可以用来找到紧上界。
现在斐波那契定义为

![F(n)](img/89e94a6914ebc89f595445c8579ba1c1.png "Rendered by QuickLaTeX.com") = ![F(n-1)](img/a63c6734bb610343aed2e237eb9a4317.png "Rendered by QuickLaTeX.com") + ![F(n-2)](img/5e4ea037cade6268c17d8a119853547f.png "Rendered by QuickLaTeX.com")

该功能的特征方程为
![x^2](img/3b3caf003c0c35a6060949f498dfb13d.png "Rendered by QuickLaTeX.com")=![x](img/54a2a70f5ead0a1cc327fc74b8d5495e.png "Rendered by QuickLaTeX.com")+![1](img/f83b22229dcf34c56119bc8d5e5e3117.png "Rendered by QuickLaTeX.com")
![x^2](img/3b3caf003c0c35a6060949f498dfb13d.png "Rendered by QuickLaTeX.com")–![x](img/54a2a70f5ead0a1cc327fc74b8d5495e.png "Rendered by QuickLaTeX.com")–![1](img/f83b22229dcf34c56119bc8d5e5e3117.png "Rendered by QuickLaTeX.com")=![0](img/0aff7f9122f65c54857e9214dcfdbb64.png "Rendered by QuickLaTeX.com")

通过二次公式求解，我们可以得到根为
![x](img/54a2a70f5ead0a1cc327fc74b8d5495e.png "Rendered by QuickLaTeX.com")=(![1](img/f83b22229dcf34c56119bc8d5e5e3117.png "Rendered by QuickLaTeX.com")+![\sqrt{5}](img/88e781bfaeb7953ec6fa9e61588b726f.png "Rendered by QuickLaTeX.com"))/![2](img/b8fbaaf9242360e81ed136b06f3e35b4.png "Rendered by QuickLaTeX.com")/![x](img/54a2a70f5ead0a1cc327fc74b8d5495e.png "Rendered by QuickLaTeX.com")=(![1](img/f83b22229dcf34c56119bc8d5e5e3117.png "Rendered by QuickLaTeX.com")–![\sqrt{5}](img/88e781bfaeb7953ec6fa9e61588b726f.png "Rendered by QuickLaTeX.com"))/![2](img/b8fbaaf9242360e81ed136b06f3e35b4.png "Rendered by QuickLaTeX.com")

现在我们知道线性递归函数的解被给出为
![F(n)](img/89e94a6914ebc89f595445c8579ba1c1.png "Rendered by QuickLaTeX.com") = ![($\alpha_1)^n](img/c00b1f4e935367f94b88f3ec4aa47bf4.png "Rendered by QuickLaTeX.com") + ![($\alpha_2)^n](img/790989014c07fecd0ee97180dd8694b9.png "Rendered by QuickLaTeX.com")

其中![$\alpha_1](img/a9291118f388684f9a6b4321dedea45b.png "Rendered by QuickLaTeX.com")和![$\alpha_2](img/83dbb391bff006d60687468d6cfa7c95.png "Rendered by QuickLaTeX.com")是特征方程的根。
所以对于我们的斐波那契函数![F(n)](img/89e94a6914ebc89f595445c8579ba1c1.png "Rendered by QuickLaTeX.com") = ![F(n-1)](img/a63c6734bb610343aed2e237eb9a4317.png "Rendered by QuickLaTeX.com") + ![F(n-2)](img/5e4ea037cade6268c17d8a119853547f.png "Rendered by QuickLaTeX.com")解将是

![F(n)](img/89e94a6914ebc89f595445c8579ba1c1.png "Rendered by QuickLaTeX.com") = ![((1+$\sqrt{5})/2)^n](img/322ad5a1b074bb1cfcf0543d0ab8644b.png "Rendered by QuickLaTeX.com") + ![((1-\sqrt{5})/2)^n](img/bad5c24578d886de5b07c0452b500ff8.png "Rendered by QuickLaTeX.com")
显然![T(n)](img/5a3721c914e82a59126415e55f9b2e5c.png "Rendered by QuickLaTeX.com")和![F(n)](img/89e94a6914ebc89f595445c8579ba1c1.png "Rendered by QuickLaTeX.com")是渐近相同的，因为这两个函数都表示同一事物。
因此可以说
![T(n)](img/5a3721c914e82a59126415e55f9b2e5c.png "Rendered by QuickLaTeX.com") = ![O(((1+$\sqrt{5})/2)^n+((1-\sqrt{5})/2)^n)](img/9271ed2b9681507de9b3ebdbadc9988e.png "Rendered by QuickLaTeX.com")
或者我们可以写在下面(利用[大 O 记数法](https://www.geeksforgeeks.org/analysis-of-algorithms-set-3asymptotic-notations/)的性质我们可以降低阶项)
![T(n)](img/5a3721c914e82a59126415e55f9b2e5c.png "Rendered by QuickLaTeX.com")=![O(((1+$\sqrt{5})/2)^n](img/f55e77ecda8f497378c4dbe84842b0a3.png "Rendered by QuickLaTeX.com")
![T(n)](img/5a3721c914e82a59126415e55f9b2e5c.png "Rendered by QuickLaTeX.com")=![O(1.6180)^n](img/c5ab9a8f739cba61144452b83a64ff1c.png "Rendered by QuickLaTeX.com")
这就是斐波那契的紧上界。\

**好玩事实:**
1.6180 也叫黄金比例。你可以在这里阅读更多关于黄金分割的内容:[数学中的黄金分割](https://www.mathsisfun.com/numbers/golden-ratio.html)

本文由 [**维奈乔希**](https://auth.geeksforgeeks.org/profile.php?user=Vineet Joshi) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。