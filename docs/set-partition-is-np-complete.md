# 设置分区为 NP 完成

> 原文:[https://www.geeksforgeeks.org/set-partition-is-np-complete/](https://www.geeksforgeeks.org/set-partition-is-np-complete/)

**<u>集合划分问题</u> :** 集合划分问题将一组数字划分为两个子集，使得这两个子集的总和相同。设 **S** 为一组数，A 为和 **S1** 的数的子集，则存在另一个包含其余元素**(S–A)**和 **S2** ， **S1 等于 S2** 。

**<u>问题陈述</u> :** 给定一组 **S** 的 **N** 个数字，任务是确定该组是否包含两个 **S** 的分区，两个分区的和完全相同。

**<u>解释</u> :**
问题的一个实例是指定给问题的输入。集合划分问题的一个实例是集合 **S** ，任务是检查是否存在两个不重叠的 **S** 的划分，其元素之和为**之和**。由于 NP-Complete 问题是同时存在于 **NP** 和 **NP-hard** 中的问题，因此证明问题是 NP-Complete 的陈述由两部分组成:

> 1.  The problem itself lies in NP class.
> 2.  All other problems in NP class can be reduced to that by polynomial time. (b can be reduced to c by polynomial time and expressed as b ≤ p <sup>c</sup> )

如果**第二个条件**仅被满足，那么问题被称为 **NP-Hard** 。

但是不可能把每一个 NP 问题都化为另一个 NP 问题来一直展示它的 NP 完全性。因此，要证明一个问题是 NP-Complete，那么证明这个问题在 NP 中，任何 NP-Complete 问题都可以化简为 NP-Complete，即如果 B 是 NP-Complete，B ≤ P <sup>C</sup> 对于 NP 中的 C，那么 C 就是 NP-Complete。因此，使用以下两个命题可以得出结论:**集合划分问题**是 NP 完全的:

**集合划分问题在 NP 中:**
如果有任何问题在 NP 中，那么，给定一个‘证书’，这是问题的一个解决方案和问题的一个实例(一个集合 **S** 和两个划分 **A** 和**A’**，在这种情况下)，可以证明证书在多项式时间内。这可以通过以下方式实现:

1.  对于 **A** 中的每个元素 **x** 和**A‘**中的**x‘**，确认属于 **S** 的所有元素都被覆盖。
2.  让 **S1** 为 0， **S2** 为 0
3.  对于 **A** 中的每个元素 **x** ，将该值添加到 **S1** 中。
4.  对于**A‘**中的每个元素**x’**，将该值添加到 **S2** 中。
5.  核实 **S1** 与 **S2** 相同。

该算法在数字集的大小上花费线性时间。

**集合划分问题是 NP-Hard:**
为了证明独立集合问题是 NP-Hard，执行从已知 NP-Hard 问题到该问题的约简。进行归约，从[子集和问题](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)可以归约为[集合划分问题](https://www.geeksforgeeks.org/partition-problem-dp-18/)。子集问题以一组数字 **S** 和一个目标和 **t** 的形式提供输入，问题的目的是找到和 **t** 相同和的属于 **S** 的子集 **T** 。让我们成为 **S** 的成员之和。现在，将**S ' = S ∨{ S 2t }**送入集合划分问题。

现在证明计算集合划分的问题确实归结为子集和的计算。这种简化可以通过以下两个命题来证明:

现在，让我们考虑一组数字 **T** ，其总和相当于 **t** (子集和)，那么 **S** (假设 **O** )中剩余的元素将具有总和**O = S–T**。让我们假设原始集合等于**T ' = T∩(s–2t)**，其和等于 **t'** 。
现在以下观察成立:

> O = s–T
> O–T = s–2t，O 和 T 之和的差
> T ' = T+(s–2t)
> = s–T
> = O，T '和 O 之和相等。

因此，原始集合可以被分成两个子集，每个子集都是和**(s–t)**。因此，满足集合划分问题。
现在假设存在**S‘**=**S ∨{ S 2t }**的等和划分 **(A，A’)**。每个分区的总和由下式给出:

> ![a = \frac{s + (s - 2*t)}{2} = (s - t)](img/6158735e5341c6fc2c1f6de904095952.png "Rendered by QuickLaTeX.com")

考虑包含元素**{ s–2t }**的分区为 **A'** 。让**A = A '-{ s–2t }**。 **A** 中的元素之和由下式给出:

> a = s–t –{ s–2t }
> = t

另外，**S’–S = { S–2t }**。所以 **A** 是 **S** 的子集，和等于 **t** 。

因此，满足子集和问题。