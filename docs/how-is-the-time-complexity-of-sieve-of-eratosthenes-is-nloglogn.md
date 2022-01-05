# 厄拉多塞筛的时间复杂度如何是 n*log(log(n))？

> 原文:[https://www . geeksforgeeks . org/exhaust-is-nloglogn/](https://www.geeksforgeeks.org/how-is-the-time-complexity-of-sieve-of-eratosthenes-is-nloglogn/)

**先决条件:** [筛厄拉多塞](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

**什么是厄拉多塞算法的[筛？](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)**
为了分析一下，我们取一个数字 **n** ，任务是打印小于 n 的素数，所以根据厄拉多塞筛的定义，对于每个素数，都要检查素数的倍数，并标记为复合。这个过程一直持续到最高质数的值 **p** 小于 **n** 。

**了解厄拉多塞的[筛的 n*log(log n)时间复杂度](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)**

1.  If it is assumed that the time taken to mark a number as composite is constant, then the number of times the loop runs is equal to:

    [![](img/ab09098c68db690af22ceb3e3b38e2a5.png "\frac{n}{2} + \frac{n}{3} + \frac{n}{5} + \frac{n}{7} + ...... p")](https://www.codecogs.com/eqnedit.php?latex=\frac{n}{2}&space;+&space;\frac{n}{3}&space;+&space;\frac{n}{5}&space;+&space;\frac{n}{7}&space;+&space;......&space;p)

2.  从上式中取 n 个公，上式可改写为:
    [![](img/10d1a269d87d338292b425b9469d680d.png "n*(\frac{1}{2} + \frac{1}{3} + \frac{1}{5} + \frac{1}{7} + ...... p)")](https://www.codecogs.com/eqnedit.php?latex=n*(\frac{1}{2}&space;+&space;\frac{1}{3}&space;+&space;\frac{1}{5}&space;+&space;\frac{1}{7}&space;+&space;......&space;p))
3.  It can be proved as below with the help of **Harmonic Progression of the sum of primes**:
    [![](img/1e43ea2478ab77c5c3d4bb8f7eb49886.png "\frac{1}{2} + \frac{1}{3} + \frac{1}{5} + \frac{1}{7} + ..... = log(log(n))")](https://www.codecogs.com/eqnedit.php?latex=\frac{1}{2}&space;+&space;\frac{1}{3}&space;+&space;\frac{1}{5}&space;+&space;\frac{1}{7}&space;+&space;.....&space;=&space;log(log(n)))

    **素数和的调和级数证明:**
    为了理解证明，前提是[调和级数](https://www.geeksforgeeks.org/program-to-find-sum-of-harmonic-series/)和**泰勒级数展开**。

    *   让我们举一个等式:
        [![](img/717916271c9a57834a3b4bb12d345244.png "log(\frac{1}{1-x})")](https://www.codecogs.com/eqnedit.php?latex=log(\frac{1}{1-x}))
    *   上述方程的泰勒级数展开式由下式给出:
        [![](img/eb3e06b5d8edc251707b43342e8cea0c.png "x + \frac{x^{2}}{2} + \frac{x^{3}}{3} + ...")](https://www.codecogs.com/eqnedit.php?latex=x&space;+&space;\frac{x^{2}}{2}&space;+&space;\frac{x^{3}}{3}&space;+&space;...)
    *   Putting **x = 1** in the above equation, we get the relation:

        [![](img/3363d5d4cd585241f30104eb74bead6a.png "\sum_{1}^{n} \frac{1}{r} = log(n )")](https://www.codecogs.com/eqnedit.php?latex=\sum_{1}^{n}&space;\frac{1}{r}&space;=&space;log(n&space;))

        让我们把上面的等式标记为 **1** 。

    *   From [Euler’s product formula](https://en.wikipedia.org/wiki/Euler_product),

        [![](img/302e4e2a744a68e88bf7a9503371e961.png "\sum_{1}^\infty {\frac{1}{r^{s}}} = \prod \frac{1}{1 - p^{-s}}")](https://www.codecogs.com/eqnedit.php?latex=\sum_{1}^\infty&space;{\frac{1}{r^{s}}}&space;=&space;\prod&space;\frac{1}{1&space;-&space;p^{-s}})

    *   On substituting **s = 1** in the above equation, we get

        [![](img/cc9966f1478c22d2c2f18898b9e3d821.png "\sum_{1}^\infty {\frac{1}{r^{1}}} = \prod \frac{1}{1 - p^{-1}}")](https://www.codecogs.com/eqnedit.php?latex=\sum_{1}^\infty&space;{\frac{1}{r^{1}}}&space;=&space;\prod&space;\frac{1}{1&space;-&space;p^{-1}})

    *   将**原木**应用于两侧:
        ul
        [T5](https://www.codecogs.com/eqnedit.php?latex=log(\sum_{1}^\infty&space;{\frac{1}{r^{1}}})&space;=&space;log(\prod&space;\frac{1}{1&space;-&space;p^{-1}}))
    *   On **simplifying** the above equation, it becomes:

        [![](img/fc989f54f08ee599a14dc83e4a5df05a.png "log(\sum_{1}^\infty {\frac{1}{r^{1}}}) = \sum log( \frac{1}{1 - p^{-1}})")](https://www.codecogs.com/eqnedit.php?latex=log(\sum_{1}^\infty&space;{\frac{1}{r^{1}}})&space;=&space;\sum&space;log(&space;\frac{1}{1&space;-&space;p^{-1}}))

    *   在上式中， **1 > p <sup>-1</sup> > -1**
    *   因此，我们可以对上述方程的右侧使用泰勒级数展开。
        [![](img/e8bb83ea5dc851743a12ec206b0d09b0.png "log(\frac{1}{1-x}) = \sum_{1}^{\infty} \frac{1}{n*p^{n}}")](https://www.codecogs.com/eqnedit.php?latex=log(\frac{1}{1-x})&space;=&space;\sum_{1}^{\infty}&space;\frac{1}{n*p^{n}})
    *   On substituting this in the above equation, we get:

        [![](img/94fe6dcbd50566d4486f07d98c296e1a.png "log(\sum_{1}^{n}\frac{1}{r}) = \sum \sum_{1}^{n} \frac{1}{n*p^{n}}")](https://www.codecogs.com/eqnedit.php?latex=log(\sum_{1}^{n}\frac{1}{r})&space;=&space;\sum&space;\sum_{1}^{n}&space;\frac{1}{n*p^{n}})

        其中 p 是素数。

    *   On expanding the inner summation;

        [![](img/c4316e5ce0c9f9d03b141e8982004ea0.png "\sum_{1}^{n} \frac{1}{n*p^{n}} = \frac{1}{p} + \frac{1}{2p^{2}} + \frac{1}{3p^{3}} + ....")](https://www.codecogs.com/eqnedit.php?latex=\sum_{1}^{n}&space;\frac{1}{n*p^{n}}&space;=&space;\frac{1}{p}&space;+&space;\frac{1}{2p^{2}}&space;+&space;\frac{1}{3p^{3}}&space;+&space;....)

    *   以上级数是收敛的。所以，以上级数可以近似为:
        [![](img/63cfb08290b7a7970572ff3800fb7722.png "\frac{1}{p}")](https://www.codecogs.com/eqnedit.php?latex=\frac{1}{p})
    *   Therefore, on substituting and rewriting the equation; we get

        [![](img/0d38a7dc7bd0c97a32b61c77737ca3f4.png "log(\sum_{1}^{\infty }\frac{1}{n}) = \sum \frac{1}{p}")](https://www.codecogs.com/eqnedit.php?latex=log(\sum_{1}^{\infty&space;}\frac{1}{n})&space;=&space;\sum&space;\frac{1}{p})

        其中 p 是质数。

    *   **从初始方程 **1** 中，我们最终可以得出:
        [![](img/c39f53ff8b8cae12014649db81b0f403.png "\sum \frac{1}{p} = log(log(n))")](https://www.codecogs.com/eqnedit.php?latex=\sum&space;\frac{1}{p}&space;=&space;log(log(n))) 
        其中 p 为素数之和。**
4.  在等式中代入这个，我们得到时间复杂度为:
    [![](img/4c62d05aa2d9f3ffe957e1c27cc86b1b.png "O(n*(log(log(n))))")](https://www.codecogs.com/eqnedit.php?latex=O(n*(log(log(n)))))

**因此厄拉多塞筛的时间复杂度为 n*log(log(n))**

**参考:** [素数倒数之和的散度](https://en.wikipedia.org/wiki/Divergence_of_the_sum_of_the_reciprocals_of_the_primes#Proof_that_the_series_exhibits_log-log_growth)