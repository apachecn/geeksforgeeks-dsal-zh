# 汉明距离的概念

> 原文:[https://www.geeksforgeeks.org/concepts-of-hamming-distance/](https://www.geeksforgeeks.org/concepts-of-hamming-distance/)

[**【海明距离】**](https://www.geeksforgeeks.org/hamming-distance-between-two-integers/) **问题:**一般来说，假设错误少的可能性大于错误多的。这种“T8”最坏情况下的“T9”编码方法本身就很有吸引力。然而，它与一个简单的概率模型密切相关，在该模型中，每个符号独立地以固定的概率 **p < 1/2** 将错误引入消息。为了谈谈**的错误数**[**海明距离**](https://www.geeksforgeeks.org/hamming-distance-between-two-integers/) 的介绍。

**<u>定义</u> :** 两个整数之间的[汉明距离](https://www.geeksforgeeks.org/hamming-distance-two-strings/)是对应位不同的位置数。它不依赖于 **xi** 和**一**的实际值，而只取决于它们是否相等。

**<u>命题</u> :** 函数 d 是一个度量。也就是说，每 x，y，z ∈ A <sub>N</sub> :

*   0 ≤ d(x，y) ≤ N
*   d(x，y) = 0 当且仅当 x = y
*   d(x，y) = d(y，x)
*   d(x，z) ≤ d(x，y) + d(y，z)(三角不等式)

<u>**解码**</u> 规则:以下是规则:

*   让 **C** 成为字母表 **A** 上的长度代码 **N** 。
*   最近邻解码规则规定每**x∈A<sub>N</sub>T3】解码到最接近 **x** 的 **cx ∈ C** 。**
*   即 **D(x) = cx** 其中 **cx** 是这样的: **d(x，cx) = minc ∈ C{d(x，c)}** 。
*   如果在此最小距离处存在多个 **c** ，则 **D** 返回 **⊥** 。
*   代码距离和错误检测和纠正。
*   直观地说，如果所有代码字都相距很远，那么代码会更好。

> **<u>形式化概念</u> :**
> 让 C 成为一个代码。代码的距离用 d(C)表示，定义如下:
> d(C) = min{d(c1，c2) | c1，c2 ∈ C，c1 6= c2}
> 
> 一个 **(N，M)**-距离 d 的代码叫做一个 **(N，M，d)-代码**。数值 N，M，d 被称为代码的参数。