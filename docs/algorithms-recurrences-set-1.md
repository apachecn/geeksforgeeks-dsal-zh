# 算法|重现|集合 1

> 原文:[https://www.geeksforgeeks.org/algorithms-recurrences-set-1/](https://www.geeksforgeeks.org/algorithms-recurrences-set-1/)

*   **Question 1:** Which of the following is the value of T<sup>3</sup>(n) where T<sup>3</sup>(n) is defined as T<sup>3</sup>(n) = 5*T<sup>3</sup>(n-1) – 4*T<sup>3</sup>(n-2)
    1.  C<sub>1</sub>* 5<sup>n</sup>+C<sub>2</sub>* 4<sup>n</sup>
    2.  C<sub>1</sub>+C<sub>2</sub>* 4<sup>n</sup>
    3.  C<sub>1</sub>* 2<sup>n</sup>+C<sub>2</sub>* 4<sup>n</sup>
    4.  C<sub>1</sub>* 5<sup>n</sup>+C<sub>2</sub>*(-4)<sup>n</sup>

    **回答:** 2

    **解释:**递归函数(方程)似乎有一种奇怪的形式。让我们改变变量 T <sup>2</sup> (n)得到一个熟悉形式的方程；所以，我们让 A(n)= T<sup>3</sup>(n)；然后我们有:

    ![A(n) = 5*A(n - 1) - 4*A(n - 2)](img/a397d8a24ab8a17bfbf34fd7419e9c20.png "Rendered by QuickLaTeX.com")

    我们的新微分方程的特征方程是:

    ![r^{2} - 5*r + 4 = 0   \Rightarrow  (r-4)(r-1) = 0](img/ff5006abf2c0b8cc8349c221eca700c6.png "Rendered by QuickLaTeX.com")

    所以，这个方程的齐次解应该是:

    ![A(n) = C_{1} *  1^{n} + C_{2} * 4^{n} = C_{1} + C_{2} * 4^{n}](img/81d3d054311fe0b7c16f9e72a8d70465.png "Rendered by QuickLaTeX.com")

    正如我们已经定义的 A(n) = T <sup>3</sup> (n)，最终答案是:

    ![T^{3}(n) = C_{1} + C_{2} *   4^{n}  = C_{1} + C_{2} * 4^{n}](img/3701610f19578eab39cc8bdf15cd8059.png "Rendered by QuickLaTeX.com")

*   **Question 2:** Determine the value of initial condition F(1) in a way that we can have F(n) = (n+2)! as the solution to the following given recursive function:

    ```
     **F(n) = (n+1) * F(n-1) + (n+1)！**
    ```

    1.  three
    2.  four
    3.  six
    4.  Two

    **回答:** 3

    **解释:**通过使用迭代技术求解给定的递归函数，我们将拥有:

    ![F(n) = (n+1) * F(n - 1) + (n+1)! = (n+1) * (n*F(n-2) + n!) + (n+1)! =(n+1)*(n)*F(n-2) + 2* (n+1)!](img/027a4e530b561da97585b9e9a8fb4a73.png "Rendered by QuickLaTeX.com")

    如果我们继续这些推导，我们很容易猜到答案应该是以下形式:

    ![F(n) = (n+1)(n)(n - 1)* ... *(n - k + 2)F(n - k) + k * (n+1)! ](img/75648ea56ca0edf76101f81c6ee58af1.png "Rendered by QuickLaTeX.com")

    迭代法的最后一步(停止点)是当我们到达初始条件 F(1)时；因此，我们假设 k = n-1，非递归形式为:

    ![F (n) = (n + 1)*(n)*(n - 1)*...*(3) * F(1) + (n - 1) * (n+1)! ](img/316b695c31a3d93a22733408a515704c.png "Rendered by QuickLaTeX.com")

    ![ = (n + 1)*(n)*(n - 1)*...*(3) * (2 * \frac{1}{2}) * F(1) + (n - 1) * (n+1)! ](img/d9194d824ded3946cefdd4b208d42d85.png "Rendered by QuickLaTeX.com")

    ![  = (n+1)! * ( \frac{F(1)}{2}) + (n - 1) * (n+1)! = (n+1)! * (\frac{F(1)}{2} + (n - 1)) ](img/9a10c3358c16f2888e2a85ad4f75a21b.png "Rendered by QuickLaTeX.com")

    根据所讨论的给定函数 F(n ),以及到目前为止我们所得到的:

    ![ F(n) = (n+2)! = (n+1)! * (n+2) = (n+1)! * (\frac{F(1)}{2} + (n - 1))](img/c881398c9fe7e6c20b917ef201d88d89.png "Rendered by QuickLaTeX.com")

    最后，正如我们将看到的，F(1)的值是:

    ![ F(1) = 2*(n + 2) - 2*(n - 1) = 6 ](img/8541554ddc71e5457ea662cf8edd29d4.png "Rendered by QuickLaTeX.com")

*   **Question 3:** What is the time Complexity of T(n) = 4* T(n/2) + n * log(n!).
    1.  θ（n * log n）
    2.  θ(n〔t0〕2〔t1〕
    3.  θ(n〔t0〕2〔t1〕* log n)
    4.  θ(n<sup>2</sup>*日志 <sup>2</sup> n)

    **回答:** 4

    **说明:**我们知道**日志(n！)∈ θ( n * log n )** 。

    现在，等价的问题是分析新递归函数的顺序:

    ![ T(n) = 4 * T(\frac{n}{2}) + n^{2} * log(n) ](img/ea7122c432b53771655662e92b17514e.png "Rendered by QuickLaTeX.com")

    这个我们可以通过[掌握定理](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)来解决。为了在这里应用主定理，我们有 **f(n) = n <sup>2</sup> * log(n)** ，参数 **a** (子问题数) **b** (约化因子) **C** 分别等于 4、2、2；所以，θ( n <sup>log <sub>b</sub> a</sup> )是θ( n <sup>2</sup> )的，它与θ( n <sup>**C** = 2</sup> )处于同一复杂度等级；因此，给定的递归函数是属于 master 定理的情况 2。

    根据主定理，T(n)的顺序如下:

    ![ T(n) \in \theta(n^{2} * log^{2}n ) ](img/1948704272ff17c024e4fc69888bbb30.png "Rendered by QuickLaTeX.com")

*   **Question 4:** Which one gives the best estimation of T(n) complexity?

    ```
    t(n)=![ 3^{log_{3}6}](img/8f927ea713d260b948f53da12fd299f7.png "Rendered by QuickLaTeX.com")* t(n/2)+n<sup>【2】</sup>【n+1】。
    ```

    1.  θ(n2*n* log n)
    2.  o(n)*【n+1】*日志 n)
    3.  θ(■t0)
    4.  θ(■t0)
    5.  o(n)2*n。

    **回答:** 3

    **说明:**我们知道![a^{log_{b}C} = C^{log_{b}a}](img/3d2672a1579bc219fa90d7145ecbc586.png "Rendered by QuickLaTeX.com")，和![n^{2}*\sqrt(n+1) \in \theta (n^{2 + \frac{1}{2}}) \in \theta (n^{\frac{5}{2}}) ](img/3d53a036d68fb49a92547052e924ac4f.png "Rendered by QuickLaTeX.com")；因此，我们可以将递归函数简化如下:

    ![T(n) = 3^{log_{3}6} * T(\frac{n}{2}) + n * \sqrt(n+1) = 6* T(\frac{n}{2}) + \theta ( n^{\frac{5}{2}} )](img/bf3765957f320071ec190b4085b42156.png "Rendered by QuickLaTeX.com")

    属于 **[主定理](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)** 的情况 3；所以， **T(n)** 的渐近复杂度是:

    ![T(n) \in \theta ( n^{log_{2}6} ) ](img/6f95cf6694bb8f7e51de5e84f65f8a45.png "Rendered by QuickLaTeX.com")

*   **Question 5:** Which asymptotic boundary is not correct for T (n) = T (n/4) + T (3n/4) + n ?
    1.  O( n <sup>log <sub>4/3</sub> 2</sup>
    2.  Ω（ n ）
    3.  O( n * log(n))
    4.  以上都不是

    **回答:** 4

    **说明:**通过 **[主定理](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)** ，我们可以指定与前两个选项(A)和(B)所示相同的边界:

    1.  ![T(n) = T(\frac{n}{4}) + T(\frac{3n}{4}) + n     \leq   2*T(\frac{3n}{4})+n   \Rightarrow  T(n) \in  O (n^{ log_{4/3}2}) ](img/4d2debeadbc4fe45c90489783780f38b.png "Rendered by QuickLaTeX.com")
    2.  ![T(n) = T(\frac{n}{4}) + T(\frac{3n}{4}) + n      \geq   2*T(\frac{n}{4})+n   \Rightarrow  T(n) \in  \Omega (n) ](img/0a33e4bc412dbe7525dc23493e05484f.png "Rendered by QuickLaTeX.com")

    我们可以通过**递归树**的方法找出第三个选项的正确性。我们画一棵树，就可以很容易地猜出 **T(n)** 的合适边界:

    ![RecurrenceTree_of_T(n)](img/e107dadc93b055af8acb09194707914b.png)

    递归树的分枝长度不能小于 **h <sub>r</sub>** ，也不能大于**h<sub>L</sub>**；因此可以推断出以下估计:

    1.  ![T(n)  \leq n * h_{r} = n * log_{\frac{4}{3}}n  \Rightarrow T(n)  \in O( n*log(n) ) ](img/789d223588525a54a345fc7a4539ae55.png "Rendered by QuickLaTeX.com")
    2.  ![T(n)  \geq n * h_{L} = n * log_{4}n  \Rightarrow T(n)  \in  \Omega ( n*log(n) ) ](img/3c54d24cae8b3e7c1db4762e188db167.png "Rendered by QuickLaTeX.com")

    在根据上面提到的两个边界，我们还有 **T(n) ∈ θ( n*log(n) )** 。

    我们知道如果 **T(n) ∈ O(n * log(n))** ，那么它也一定是**O(n<sup>log<sub>4/3</sub>n</sup>)**；所以如果我们先评估了第三个选项，我们实际上也会推断出选项(A)的正确性。然而，递归树只是给出了如何猜测合适边界的想法。由于有人可能会给出错误的猜测，这种方法也需要验证或证明它不会违反所使用的符号的定义。这种验证(证明)可以通过对 T(n)的迭代替换归纳获得，同时考虑符号定义。