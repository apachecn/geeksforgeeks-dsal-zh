# 证明:为什么两个正数的均方根总是大于它们的几何平均值？

> 原文:[https://www . geesforgeks . org/proof-为什么两个正数的均方根总是大于它们的几何平均值/](https://www.geeksforgeeks.org/proof-why-the-root-mean-square-of-two-positive-numbers-is-always-greater-than-their-geometric-mean/)

本文主要讨论两个正数的均方根总是大于其几何平均值的证明。在进入证明的细节之前，让我们首先讨论基本术语:

[**【均方根值】**](https://www.geeksforgeeks.org/program-to-calculate-root-mean-square/) **:**
考虑一些数字，A <sub>1</sub> ，A <sub>2</sub> ，A <sub>3</sub> ，A <sub>4</sub> ，…。A <sub>N</sub> ，这些数的均方根将等于这些数的平方的[算术平均值](https://www.geeksforgeeks.org/arithmetic-mean/#:~:text=Arithmetic%20mean%2C%20also%20called%20the,mean%20is%20important%20in%20statistics.)的[平方根](https://www.geeksforgeeks.org/square-root-of-an-integer/)，即

```
For A1, A2, A3 ... AN, the RMS value equals to-
Root Mean Square (RMS) = √(((A1)2 + (A2)2 + (A3)2 +...+ (AN)2)/N)

For two numbers, A and B, their RMS value equals to- 
Root Mean Square (RMS) = √((A2 + B2)/2)
```

均方根也称为二次均值，应用范围非常广泛。在统计学中，它经常被用作术语[标准差](https://www.geeksforgeeks.org/mathematics-mean-variance-and-standard-deviation/)的替代。它也用于许多与物理相关的概念，如电学等。

[**几何平均(GM)**](https://www.geeksforgeeks.org/geometric-mean-two-methods/)【T4:
考虑一些数字，A <sub>1</sub> ，A <sub>2</sub> ，A <sub>3</sub> ，A <sub>4</sub> ，…。A <sub>N</sub> ，这些数的几何平均数将等于所有这些数相乘的第 N 个平方根，即

```
For A1, A2, A3 ... AN, the GM value equals to-
Geometric Mean (GM) = n√(A1 * A2 * A3 * ... * AN)

For two numbers, A and B, the GM value equals to-
Geometric Mean (GM) = √(A * B)
```

用来求几何序列的[平均值](https://www.geeksforgeeks.org/calculate-the-average-variance-and-standard-deviation-in-r-programming/)或均值，帮助我们研究分析很多现实生活中的概念，比如细菌的生长，投资等。

**问题陈述:**
两个正数的均方根总是大于同两个数的几何平均值。

**解:**
考虑 A 和 B 两个数，这样 A、B > 0 且 A ≠ B

1.考虑两个正数之差的平方公式-

```
(A - B)2 = A2 - 2AB + B2 --- (1)
```

2.众所周知，一个数的平方总是大于或等于零。但是这里我们有 A ≠ B，所以可以写成-

```
(A - B)2 > 0
```

3.使用等式 1 中定义的属性展开上述等式的左侧-

```
A2 - 2AB + B2 > 0
```

4.做了一些重组后-

```
A2 + B2 > 2AB
```

5.将上面的等式代入 2-

```
((A2 + B2)/2) > (A * B)
```

6.因为两边都大于 0，即正。对两边求平方后，得到以下等式-

```
√((A<sup>2 + B2)/2) ></sup> √(A * B)
```

注意**左手边是均方根，右手边等于 A 和 B** 的几何平均值。这证明了两个正数的均方根总是大于几何平均值。