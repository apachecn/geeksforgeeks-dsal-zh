# 证明:为什么没有平方为 2 的有理数？

> 原文:[https://www . geesforgeks . org/proof-why-有-无-有理数-谁的平方是-2/](https://www.geeksforgeeks.org/proof-why-there-is-no-rational-number-whose-square-is-2/)

本文主要讨论平方为 2 的有理数不存在的证明。在开始证明之前，让我们先熟悉一下基本术语-

[**有理数**](https://www.geeksforgeeks.org/rational-numbers/) **:**
一个可以用 p/q 形式表示的数，其中 p 和 q 为整数，q ≠ 0，称为有理数。例如 0，1，-1，5/2 等。

**问题陈述:**
没有平方为 2 的有理数。

**解决方案:**
我们先从上述问题陈述的证明开始。本文中的证明将使用一种叫做[矛盾证明](https://www.geeksforgeeks.org/mathematics-introduction-to-proofs/)的数学技术来完成。

**矛盾证明-**
它是一种数学技术，首先假设需要证明的命题是假的，然后用假命题推导出一个结果，出来要么与假设相矛盾，要么与其他任何公知的数学结果相矛盾。从而，证明了命题的有效性。这就是为什么这项技术被称为矛盾证明。

**证明-**
在这个证明中，使用了矛盾证明技术，首先假设存在一个有理数，其平方等于 2，然后使用这个假设推导出一个结果，这个结果将与我们的假设相矛盾。所以。让我们从证据开始-

1.假设存在一个有理数，X = p/q，其[的平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)等于 2，这样 p 和 q 就是它们最简单的形式，即它们没有任何[公因数](https://www.geeksforgeeks.org/print-kth-common-factor-two-numbers/)。

```
X2 = 2 (Assumption)
(p/q)2 = 2 (Since X is a rational number)
```

2.这意味着，

```
p2/q2 = 2
p2 = 2q2 ---(1)
```

3.从上面的等式可以看出，p <sup>2</sup> 是一个[偶数](https://www.geeksforgeeks.org/count-ways-express-even-number-n-sum-even-integers/)，因为它可以用 2k 的形式表示，其中 k = q <sup>2</sup> 。现在已知奇数的[平方总是奇数](https://www.geeksforgeeks.org/prove-that-the-square-of-an-odd-integer-is-always-odd/)，这意味着 p 不能是奇数[整数，](https://www.geeksforgeeks.org/prove-that-the-square-of-an-odd-integer-is-always-odd/)因此 p 也是偶数。因此，p 可以 2k 的形式表示，其中 k 是某个整数，即

```
p = 2k, for some integer k ---(2)
```

3.现在，将等式(1)中等式(2)的 p 值代入后，得到以下等式-

```
(2k)2 = 2q2
4k2 = 2q2 ---(3)
```

3.将两边除以 2，在等式(3)中，得到以下等式-

```
2k2 = q2
q2 = 2k2 ---(4)
```

4.再次，可以说 q <sup>2</sup> 是偶数，由于已知奇数的平方总是奇数，因此 q 不能是奇数。这意味着 q 也是一个偶数。

5.现在，从上面的讨论中，可以得出结论，p 和 q 都是偶数，即它们的公因数至少为 2，但是这种说法与这个证明开始时的假设相矛盾，即 p 和 q 都是它们最简单的形式，即它们没有任何公因数。

这个矛盾意味着**存在有理数，X = p/q 的平方等于 2 使得 p 和 q 以最简单的形式存在的假设是错误的**。从而证明不存在平方等于 2 的有理数。