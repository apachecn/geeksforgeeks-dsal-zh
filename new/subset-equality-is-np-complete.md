# 子集相等为 NP 完整

> 原文： [https://www.geeksforgeeks.org/subset-equality-is-np-complete/](https://www.geeksforgeeks.org/subset-equality-is-np-complete/)

**<u>子集相等问题</u>**：给定非负整数值的集合`S`，问题是要确定集合 **S 是否存在分区** 分为两组`X`和`Y`，这样，`X`中的整数和等于`Y`中的整数和 ]。

**<u>解释</u>**：

问题的一个实例是为此问题指定的输入。 **子集相等性问题**的一个实例是集合`S`。 由于 [NP 完全问题](https://www.geeksforgeeks.org/np-completeness-set-1/)是 **NP** 和 **NP-hard** 中都存在的问题，因此证明问题为 NP-完全的陈述的证据包括 分两部分：

> 1.  问题本身在 **NP 类** 中。
> 2.  NP 类中的所有其他问题都可以通过多项式时间归约。

如果仅满足**第二条件**，则该问题称为 **NP-Hard** 。

但是不可能将每个 NP 问题都简化为另一个 NP 问题以始终显示其 NP 完整性。 因此，要表明问题是 NP-Complete，则证明问题出在 **NP** 中，并且可以将任何 **NP-Complete 问题**还原为该问题，即，如果 B 是 NP-Complete 且 B≤P <sup>C</sup> ，然后对于 NP 中的 C，则 C 为 NP 完全。 因此，可以得出以下结论**：子集相等问题**是 NP-完全的：

1.  **子集相等性在 NP** 中

2.  **子集相等为 NP-Hard**

这两个命题可以证明为**子集相等问题**是**子集和问题**的特例，其中子集`X`和[HTG6`S`中的 Y 可以设置为：![sum = \frac{1}{2}\sum_{x\epsilon S}x](img/5f9c98681e7c0bfbb37e346edcd4e25a.png "Rendered by QuickLaTeX.com")

由于子集和为 **NP-完全**，因此子集相等问题也变为 **NP-完整**。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。