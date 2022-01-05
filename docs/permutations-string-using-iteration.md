# 使用迭代的字符串的所有排列

> 原文:[https://www . geesforgeks . org/置换-字符串-使用-迭代/](https://www.geeksforgeeks.org/permutations-string-using-iteration/)

排列，也称为“排列数”或“顺序”，是将有序列表 S 的元素重新排列成与 S 本身一一对应的关系。长度为 n 的字符串有 n！排列(来源: [Mathword](http://mathworld.wolfram.com/Permutation.html) )

以下是字符串 ABC 的排列。
中航 ACB 北汽 BCA CBA CAB

我们已经讨论了打印排列的不同递归方法【这里的 T0】和【这里的 T2】。

**如何迭代打印所有排列？**
一个**简单的解决方案**使用 n-1 个元素的排列来生成 n 个元素的排列。

例如，让我们看看如何使用大小为 2 的置换生成大小为 3 的置换。

两个元素的排列是 1 2 和 2 1。
三个元素的排列可以通过在大小为 2 的所有排列中的不同位置插入 3 来获得。
在 1 2 的不同位置插入 3 会导致 1 2 3、1 3 2 和 3 1 2。
在 2 1 的不同位置插入 3 会导致 2 1 3、2 3 1 和 3 2 1。

为了生成大小为 4 的置换，我们考虑大小为 3 的所有上述六个置换，并在每个置换的不同位置插入 4。

一个有效的解决方案是使用[约翰逊和特罗特算法](https://www.geeksforgeeks.org/johnson-trotter-algorithm/)迭代生成所有置换。

[Johnson and Trotter algorithm](https://www.geeksforgeeks.org/johnson-trotter-algorithm/)