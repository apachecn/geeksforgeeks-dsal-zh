# 数字系统:数字的循环性

> 原文:[https://www . geesforgeks . org/number-system-cycle-of-numbers/](https://www.geeksforgeeks.org/number-system-cyclicity-of-numbers/)

[数字系统](https://www.geeksforgeeks.org/number-system-in-maths/)是借助一组符号和规则在[数字线上](https://www.geeksforgeeks.org/representation-of-rational-numbers-on-the-number-line-class-8-maths/)表示数字的方法。这些符号的范围从 0 到 9，称为数字。数字系统用于进行数学计算，从伟大的科学计算到计算，如给孩子的玩具数量或盒子里剩余的巧克力数量。数字系统根据其数字的基础值包含多种类型。

**<u>数的循环性</u> :** 任何数的循环性主要集中在其单位数上。当上升到任何[幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)时，每个单位数字都有自己的重复模式。这个概念在解决智能问题时非常有用。数字的循环性的概念可以通过计算所有从 0 到 9 的一位数的单位位数来学习。这些数字可大致分为以下三类:

**1。数字 0、1、5 和 6:** 这里，当这些数字中的每一个都被提升到任意幂时，最终答案的单位数字就是数字本身。

**示例:**

```
1\. 5 ^ 2 = 25: Unit digit is 5, the number itself.
2\. 1 ^ 6 = 1: Unit digit is 1, the number itself.
3\. 0 ^ 4 = 0: Unit digit is 0, the number itself.
4\. 6 ^ 3 = 216: Unit digit is 6, the number itself.
```

以下是基于上述概念的一些问题:

**问题 1:** 找到 416 <sup>345</sup> 的单位数字。

**答案:**只需找到 6 <sup>345</sup> 即可给出 6 作为单位数字，因此 416 <sup>345</sup> 的单位数字为 6。

**问题 2:** 找到 235 <sup>34566</sup> 的单位数字。

**答案:**找到 5 <sup>34566</sup> 会给出 5 作为单位数字，因此 235 <sup>34566</sup> 的单位数字是 5。

**2。数字 4 和 9:** 这两个数字 4 和 9 都有两个不同数字作为单位数字的循环性。

**示例:**

```
1\. 4 ^ 2 = 16: Unit digit is 6.
2\. 4 ^ 3 = 64: Unit digit is 4.
3\. 4 ^ 4 = 256: Unit digit is 6.
4\. 4 ^ 5 = 1024: Unit digit is 4.
5\. 9 ^ 2 = 81: Unit digit is 1.
6\. 9 ^ 3 = 729: Unit digit is 9.
```

可以观察到单位数字 6 和 4 以奇偶顺序重复。所以，4 的循环度是 2。9 的情况也类似。

可以概括如下:

*   4 <sup>奇数</sup> = 4:如果 4 是奇数的幂，那么单位数字就是 4。
*   4 <sup>偶数</sup> = 6:如果 4 的幂是偶数，那么单位数字就是 6。
*   9 <sup>奇数</sup> = 9:如果 9 是奇数的幂，那么单位数字就是 9。
*   9 <sup>偶数</sup> = 1:如果 9 的幂是偶数，那么单位数字就是 1。

以下是基于上述概念的一些问题:

**问题 1:** 找到 414 <sup>23</sup> 的单位数字。

**回答:** 23 是奇数，所以 4 <sup>奇数</sup> =4，因此单位数字是 4。

**问题 2:** 找到 29 <sup>82</sup> 的单位数字。

**回答:** 82 是偶数，所以 9 <sup>偶数</sup> =1，因此单位数字为 1。

**3。数字 2、3、7 和 8:** 这些数字具有四个不同数字的循环性。

**示例:**

```
1\. 2 ^ 1 = 2: Unit digit is 2.
2\. 2 ^ 2 = 4: Unit digit is 4.
3\. 2 ^ 3 = 8: Unit digit is 8.
4\. 2 ^ 4 = 16: Unit digit is 6.
5\. 2 ^ 5 = 32: Unit digit is 2.
6\. 2 ^ 6 = 64: Unit digit is 4.
```

可以观察到单位数字 2、4、8、6 在四个数字的周期之后重复它们自己。同样的，

*   3 的循环性有 4 个不同的数字:3，9，7，1。
*   7 的循环性有 4 个不同的数字:7，9，3，1。
*   8 的循环性有 4 个不同的数字:8，4，2，4。

以下是基于上述概念的一些问题:

**问题 1:** 找到 257 <sup>345</sup> 的单位数字。

**回答:** 345 % 4 = 1，所以 7 <sup>1</sup> ，因此单位数字是 7。

**问题 2:** 找到 423 <sup>43</sup> 的单位数字。

**回答:** 43 % 4 = 3，所以 3 <sup>3</sup> ，因此 7 是单位数字。

**问题 3:** 找到 28 <sup>146</sup> 的单位数字。

**回答:** 146 % 4 = 2，所以 8 <sup>2</sup> ，因此单位数字是 4。

**<u>周期性表</u> :** 以上讨论的概念可以概括为:

<figure class="table">

| **号** | **周期性** | **动力循环** |
| --- | --- | --- |
| one | one | one |
| Two | four | 2, 4, 8, 6 |
| three | four | 3, 9, 7, 1 |
| four | Two | 4, 6 |
| five | one | five |
| six | one | six |
| seven | four | 7, 9, 3, 1 |
| eight | four | 8, 4, 2, 6 |
| nine | Two | 9, 1 |
| Ten | one | Zero |

</figure>