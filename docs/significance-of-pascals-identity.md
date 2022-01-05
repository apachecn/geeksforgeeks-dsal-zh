# 帕斯卡身份的意义

> 原文:[https://www . geesforgeks . org/significance-of-Pascal-identity/](https://www.geeksforgeeks.org/significance-of-pascals-identity/)

我们非常了解[帕斯卡的身份](http://en.wikipedia.org/wiki/Pascal's_rule)，即**n<sub>c</sub>T5<sub>r</sub>T8】= n-1<sub>c</sub>T11<sub>r</sub>T14】+n-1<sub>c</sub>T17<sub>r-1</sub>T20】T21】**

好奇的读者可能已经观察到，帕斯卡恒等式有助于在求解二项式系数时建立递归关系。用简单代数证明上述恒等式相当容易。在这里我试图解释它的实际意义。

从计数技巧上重述一下，**n<sub>c</sub>T3<sub>r</sub>T6**意味着从**nT15】元素中选择**T9】rT11】元素。让我们从这些 ***n*** 元素中挑选一个特殊元素 ***k*** ，我们剩下**(*n–1*)**元素。****

我们可以将这些**T1】rT3】元素选择**n<sub>c</sub>T7<sub>r</sub>T10**分为两类，**

1)包含元素 ***k*** 的组。

2)组*不包含元素 ***k*** 。*

先考虑第一组，特殊元素 ***k*** 在所有 ***r*** 选择中。由于 ***k*** 是 ***r*** 元素的一部分，我们需要从剩余的(***n-1***元素中选择(***r–1***)元素，有**n-1<sub>c</sub>**<sub>t39】r-1</sub>T33】的方式

考虑第二组，特殊元素 ***k*** 并不存在于所有 ***r*** 选择中，即我们必须从可用(***n–1***)元素中选择所有***r***元素(因为我们必须从 ***n*** 中排除元素 ***k*** )。这可以通过**n-1<sub>c</sub><sub><sub>r</sub></sub>**的方式来完成。

现在很明显，这两者之和是从 ***n*** 元素中选择 ***r*** 元素。

可以有很多方法来证明上述事实。帕斯卡恒等式可能有许多应用。请分享你的知识。

——**[文基](http://www.linkedin.com/in/ramanawithu)** 。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。