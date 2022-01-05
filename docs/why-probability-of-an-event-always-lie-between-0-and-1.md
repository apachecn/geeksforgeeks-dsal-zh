# 为什么一个事件的概率总是介于 0 和 1 之间？

> 原文:[https://www . geeksforgeeks . org/why-一个事件的概率-总是介于-0 和-1 之间/](https://www.geeksforgeeks.org/why-probability-of-an-event-always-lie-between-0-and-1/)

[概率](https://www.geeksforgeeks.org/probability-gq/)指事件发生的程度。当一个事件发生，比如扔一个球，从一副牌中选一张牌，等等，那么一定有某种概率与那个事件有关。

**互斥事件:**
给定两个事件 a 和 b，如果这两个事件没有共同点，即 a∪b =∅，那么这些事件相交的概率也将等于零，即**p(a∪b)= 0**。此类事件被称为[互斥事件](https://www.geeksforgeeks.org/mathematics-probability/)。

**样本空间:**
它是一个实验的所有可能结果的集合。在本文中，我们将使用“S”来表示[样本空间](https://www.geeksforgeeks.org/chance-and-probability/)。

现在，有三个与概率相关的重要公理，将真正帮助我们证明上述说法。让我们来看看这些公理-

> 1.  The probability of an event will always be greater than or equal to zero, that is, P(A) > = 0 for any event a. 。
> 2.  The probability of sample space will always be equal to 1, that is, P(S) = 1.
> 3.  Given some mutually exclusive events, the probabilities of all these mutually exclusive events combinations will always be equal to the sum of the probabilities of individual events, namely p (a <sub>1</sub> ∪ a <sub>2</sub> ∪ a <sub>3</sub> ∪ a <sub>4</sub> ... ∪.

**问题陈述:**
这里的任务是证明 A 的概率永远在 0 和 1 之间，即 **0 < = P(A) < = 1** 。

**解决方案:**考虑事件 a，以下是上述问题陈述的证明步骤-

*   根据公理 1，事件发生的概率总是大于或等于 0。

```
P(A) >= 0 (According to Axiom 1)  --- (1)
```

*   样本空间的概率等于 A 和(S–A)相交的概率，即

```
S = A + (S - A)
P(S) = P(A + (S - A))
```

*   因为 A 和(S–A)是两个互斥的事件。所以，根据公理 3，它可以写成-

```
P(A + (S - A)) = P(A) + P(S - A)
```

*   这意味着，

```
P(S) = P(A) + P(S - A)) --- (2)
```

*   现在，从公理 1 可以说，P(S–A)将始终大于或等于零，即**P(S–A)>= 0**。
*   如果某个积极的东西被添加到一个给定的值中，它的值将总是增加。既然，P(S–A)> = 0，可以说 P(A)不能大于 P(S)。否则，等式(2)不成立。
*   这意味着-

```
P(S) >= P(A)
```

*   根据公理 2，样本空间的概率总是等于 1。所以，这意味着-

```
1 >= P(A)
   or
P(A) >= 1 --- (3)
```

*   从等式(1)和(3)可以看出-

```
0 <= P(A) <= 1
```

这证明了一个事件的概率永远在 **0** 和 **1** 之间。