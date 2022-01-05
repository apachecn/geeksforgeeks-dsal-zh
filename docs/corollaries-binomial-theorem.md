# 二项式定理的推论

> 原文:[https://www.geeksforgeeks.org/corollaries-binomial-theorem/](https://www.geeksforgeeks.org/corollaries-binomial-theorem/)

表达式![(a+b)^n](img/d1e459c610e39886c76ac529beb5bc9d.png "Rendered by QuickLaTeX.com")表示![(a+b)(a+b)(a+b) ... n](img/1894e70f5b78c7b71c99aa34476409bc.png "Rendered by QuickLaTeX.com")次。
这可以被评估为涉及 k = 0 到 n 的![a^k b^{n-k}](img/dbdf649161a61c55ad424a0863453ab9.png "Rendered by QuickLaTeX.com")项的总和，其中第一项可以从 n 个位置中选择，第二项可以从(n-1)个位置中选择，![k^{th}](img/ff8e88536ac0e9a371d678c2de821c23.png "Rendered by QuickLaTeX.com")项可以从(n-(k-1)个位置中选择，等等。这表示为![(a+b)^n = \sum\limits_{k=0}^n ^nC_k a^{n-k} b^k](img/e19b1813d4b5cd0e0bb6a26c7e3a1d6f.png "Rendered by QuickLaTeX.com")。
使用组合符号的二项式展开是

> ![(a+b)^n = ^nC_0 a^n b^0 + ^nC_1 a^{n-1} b^1 + ^nC_2 a^{n-2} b^2 .. + ^nC_{n-k} a^k b^{n-k} .. +^nC_n a^0 b^n](img/7901976b6b8068fe017a810c19cf582b.png "Rendered by QuickLaTeX.com")

*   上述二项式展开式中各项![a^k](img/686c4a98fce232ae52de0a8b79542284.png "Rendered by QuickLaTeX.com") ![b^{n-k}](img/bfbb9c5ddaa0012c5f275d24c9397481.png "Rendered by QuickLaTeX.com")的度数为 n 阶
*   展开式中的项数是 n+1。
*   ![^nC_k = n!/k!(n-k)!](img/ba8794a2000671b7a8c6ce9ec737123f.png "Rendered by QuickLaTeX.com")
    同理![^nC_{n-k} = n!/(n-k)!(n-(n-k))! = n!/(n-k)!k!](img/4073775bbf5a16b1a098012ec30c30a5.png "Rendered by QuickLaTeX.com")
    由此可以得出![^nC_k = ^nC_{n-k}](img/f24caa042b6f4afaf1f8d284ff0c2b24.png "Rendered by QuickLaTeX.com")。

在二项式展开式中代入 a = 1，b = x，对于任意正整数 n，我们得到
![(1+x)^n = ^nC_0 + ^nC_1 x^1 + ^nC_2 x^2 ..+ ^nC_n x^n](img/3a813c8698655b9bb707c43f6ddb20b8.png "Rendered by QuickLaTeX.com")。

**推论 1:**

> ![\sum\limits_{k=0}^n ^nC_k = 2^n](img/ad11952561aeeda9b3b1b963c362de02.png "Rendered by QuickLaTeX.com")

对于任何非负整数 n。

将上述二项式展开式中的 x 替换为 1，我们得到
![^nC_0 + ^nC_1 + ^nC_2 .. + ^nC_n = (1+1)^n = 2^n](img/becdd5abd9ccbb210c47e0f7b63788f2.png "Rendered by QuickLaTeX.com")。

**推论 2:**

> ![\sum\limits_{k=0}^n ^nC_k = 0](img/e119b874d5d2bc83acfb22907f8fcd13.png "Rendered by QuickLaTeX.com")

对于任何正整数 n。

用-1 代替上述二项式展开式中的 x，我们得到
![^nC_0 + ^nC_1 (-1) + ^nC_2 (-1)^2 .. + ^nC_n (-1)^n = (1+(-1))^n = 0](img/5b547e27a733cb28b10eb41e97580675.png "Rendered by QuickLaTeX.com")。

**推论 3:**

将上述二项式展开式中的 x 替换为 2，得到
![^nC_0 + ^nC_1 2 + ^nC_2 2^2 .. + ^nC_n 2^n = (1+2)^n = 3^n](img/2133d7e8cb7745ad49b3e4ab97e5ef41.png "Rendered by QuickLaTeX.com")

总的来说，可以说

> ![\sum\limits_{k=0}^n (2^k) ^nC_k = 3^n](img/34c9054c549353936ad9588b2ec6da9e.png "Rendered by QuickLaTeX.com")

此外，可以将推论 1 和推论 2 结合起来得到另一个结果，

![^nC_0 + ^nC_1 (-1) + ^nC_2 (-1)^2 .. + ^nC_n (-1)^n = (1+(-1))^n = 0](img/5b547e27a733cb28b10eb41e97580675.png "Rendered by QuickLaTeX.com")

![^nC_0 + ^nC_2 + .. = ^nC_1 + ^nC_3 + ...](img/42e0f041c10612533d7b752b8d66018d.png "Rendered by QuickLaTeX.com")
偶数项系数之和=奇数项系数之和。

从![\sum\limits_{k=0}^n ^nC_k = 2^n](img/ad11952561aeeda9b3b1b963c362de02.png "Rendered by QuickLaTeX.com")开始，

2( ![^nC_0 + ^nC_2 + ..) = 2^n](img/bb488f1d4a8588eba132bd98b213abf8.png "Rendered by QuickLaTeX.com")

![^nC_0 + ^nC_2 + .. = 2^{n-1}](img/5e99ac39b6d46612c106835509675a13.png "Rendered by QuickLaTeX.com")

> ![^nC_0 + ^nC_2 + .. = ^nC_1 + ^nC_3 + .. = 2^{n-1}](img/637bf2e776421fdc25fc9c2b5cf28d59.png "Rendered by QuickLaTeX.com")

**计数**
展开![(a+b)^n](img/d1e459c610e39886c76ac529beb5bc9d.png "Rendered by QuickLaTeX.com")中的项的系数对应于第 n 行帕斯卡三角形的项

| ![(a+b)^0](img/cf92c7ca10aa4aa227e884b7ec1ea027.png "Rendered by QuickLaTeX.com") | one | one |
| ![(a+b)^1](img/e17020a0319c2ac5f9ba36771f691db0.png "Rendered by QuickLaTeX.com") | ![a+b](img/a940a1af847ff463b2a6a4f72c7a61c0.png "Rendered by QuickLaTeX.com") | ![1 \ 1](img/a2d5047f28351b485d222201ecda3749.png "Rendered by QuickLaTeX.com") |
| ![(a+b)^2](img/e94a8feba484704f4d17160e1d7db0af.png "Rendered by QuickLaTeX.com") | ![a^2+2ab+b^2](img/5ed59fc9339c36bbef2360af1b800637.png "Rendered by QuickLaTeX.com") | ![1 \ 2 \ 1](img/8c84e80c32f25b3e272814528cbf0bc7.png "Rendered by QuickLaTeX.com") |
| ![(a+b)^3](img/051783c8067080d1723a2c4b6f8de79f.png "Rendered by QuickLaTeX.com") | ![a^3+3a^2b+3ab^2+b^3](img/ecb40003762bdd951c8a779af350316a.png "Rendered by QuickLaTeX.com") | ![1 \ 3 \ 3 \ 1](img/dafba4b0d3753c9c7aefc4f6cadf5810.png "Rendered by QuickLaTeX.com") |