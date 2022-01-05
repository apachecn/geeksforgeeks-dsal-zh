# 算法设计技术

> 原文:[https://www.geeksforgeeks.org/algorithms-design-techniques/](https://www.geeksforgeeks.org/algorithms-design-techniques/)

**什么是算法？**

算法是在有限的步骤中为有限大小的输入解决特定问题的过程。
算法可以通过多种方式进行分类。它们是:

1.  实现方法
2.  设计法
3.  其他分类

本文讨论了每种分类方法中的不同算法。

**按实现方法分类:**在这种类型的分类中，算法主要可以分为三大类。他们是:

1.  **递归或迭代:**一种[递归算法](https://www.geeksforgeeks.org/recursion/)是一种反复调用自身直到达到基本条件的算法，而迭代算法使用[循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)和/或[数据结构](https://www.geeksforgeeks.org/data-structures/)如[栈](https://www.geeksforgeeks.org/stack-data-structure/)、[队列](https://www.geeksforgeeks.org/queue-data-structure/)来解决任何问题。每个递归解决方案都可以实现为迭代解决方案，反之亦然。
    **示例:** [汉诺塔](https://www.geeksforgeeks.org/c-program-for-tower-of-hanoi/)递归实现，而[股票跨度](https://www.geeksforgeeks.org/the-stock-span-problem/)问题迭代实现。
2.  **精确或近似:**能够为任何问题找到最优解的算法称为精确算法。对于所有这些问题，在不可能找到最佳解决方案的地方，使用近似算法。近似算法是一种将结果作为问题的子结果的平均结果的算法。
    **示例:**对于 [NP-Hard 问题](https://www.geeksforgeeks.org/np-completeness-set-1/)，使用近似算法。[排序算法](https://www.geeksforgeeks.org/sorting-algorithms/)是确切的算法。
3.  **串行或并行或分布式算法:**在串行算法中，一次执行一条指令，而并行算法是我们将问题分成子问题，并在不同的处理器上执行的算法。如果并行算法分布在不同的机器上，那么它们被称为分布式算法。

**按设计方法分类:**在这类分类中，算法主要分为三大类。他们是:

1.  **贪心法:**在[贪心法](https://www.geeksforgeeks.org/greedy-algorithms/)中，每走一步都要做出选择*局部最优*的决定，不考虑未来的后果。
    **举例:** [分数背包](https://www.geeksforgeeks.org/fractional-knapsack-problem/)[活动选择](https://www.geeksforgeeks.org/activity-selection-problem-greedy-algo-1/)。
2.  **分而治之:**[分而治之](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/)策略涉及到将问题划分为子问题，递归求解，然后重组得到最终答案。
    **例:** [合并排序](https://www.geeksforgeeks.org/merge-sort/)[快速排序](https://www.geeksforgeeks.org/quick-sort/)。
3.  **动态规划:**[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的做法类似于[分治](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/)。不同的是，每当我们有相同结果的递归函数调用时，我们尝试以表的形式将结果存储在数据结构中，并从表中检索结果，而不是再次调用它们。因此，降低了整体时间复杂度。“动态”是指我们动态决定是调用函数还是从表中检索值。
    **举例:** [0-1 背包](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)、[子集和问题](https://www.geeksforgeeks.org/subset-sum-problem-dp-25/)。
4.  **线性规划:**线性规划中，在输入和最大化或最小化输入的一些线性函数方面存在不等式。
    **例:**有向图最大流量
5.  **约简(变换与征服):**在这种方法中，我们通过将一个困难的问题转化为我们有最优解的已知问题来解决它。基本上，目标是找到一种简化算法，其复杂性不受最终简化算法的支配。
    **示例:**查找列表中中间值的选择算法首先对列表进行排序，然后找出排序后的列表中的中间元素。这些技术也被称为*改造和征服。*

**其他分类:**除了将算法分为上述大类之外，还可以将算法分为其他大类，如:

1.  **随机化算法:**为更快的解做出随机选择的算法被称为[随机化算法](https://www.geeksforgeeks.org/randomized-algorithms/)。
    **例:** [随机化快速排序算法](https://www.geeksforgeeks.org/quicksort-using-random-pivoting/)。
2.  **按复杂度分类:**算法，根据解决输入大小的任何问题所需的时间进行分类。这种分析被称为[时间复杂度分析](https://www.geeksforgeeks.org/understanding-time-complexity-simple-examples/)。
    **例:**有些算法取 O(n)，有些则取指数时间。
3.  **按研究区域分类:**在 CS 中，每个领域都有自己的问题，需要高效的算法。
    **示例:**排序算法、搜索算法、机器学习等。
4.  **分支定界枚举和回溯:**这些大多用于人工智能。