# 随机化算法|集合 2(分类和应用)

> 原文:[https://www . geesforgeks . org/随机化-算法-集合-2-分类-应用/](https://www.geeksforgeeks.org/randomized-algorithms-set-2-classification-and-applications/)

我们强烈建议将以下帖子作为先决条件。

[随机化算法|集合 1(介绍和分析)](https://www.geeksforgeeks.org/randomized-algorithms-set-1-introduction-and-analysis/)

## **分类**

随机化算法分为两类。

**拉斯维加斯:**这些算法总能产生正确或最优的结果。这些算法的时间复杂度基于随机值，时间复杂度被评估为期望值。例如，随机快速排序总是对输入数组进行排序，并且[预期快速排序的最坏情况时间复杂度为 0(nLogn)](https://www.geeksforgeeks.org/randomized-algorithms-set-1-introduction-and-analysis/)。

**蒙特卡罗:**以一定概率产生正确或最优的结果。这些算法具有确定性的运行时间，并且通常更容易找出最坏情况下的时间复杂度。例如[卡尔格算法的这种实现方式](https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-1-introduction-and-implementation/)产生概率大于或等于 1/n 的最小割 <sup>2</sup> (n 是顶点数)并且具有最坏情况下的时间复杂度为 O(E)。另一个例子是[原始性测试的费梅法](https://www.geeksforgeeks.org/primality-test-set-2-fermet-method/)。

**理解分类的示例:**

```
Consider a binary array where exactly half elements are 0
and half are 1\. The task is to find index of any 1\.  
```

这个任务的一个拉斯维加斯算法是不断挑选一个随机元素，直到我们找到一个 1。同样的蒙特卡罗算法是继续选择一个随机元素，直到我们找到 1 或者我们已经尝试了最大允许次数，比如说 k.
拉斯维加斯算法总是找到 1 的索引，但是时间复杂度被确定为期望值。[预期成功前的试验次数](https://www.geeksforgeeks.org/expected-number-of-trials-before-success/)为 2，因此预期时间复杂度为 0(1)。
蒙特卡罗算法以概率[1 –( 1/2)<sup>k</sup>找到 1。蒙特卡罗的时间复杂度是确定性的

## **应用及范围:**

*   考虑一个基本上做排序的工具。让工具被很多用户使用，很少有用户总是对已经排序的数组使用工具。如果工具使用简单的(非随机的)快速排序，那么这几个用户总是会面临最坏的情况。另一方面，如果工具使用随机化快速排序，那么就没有用户总是得到最坏的情况。每个人都有期待的时间。
*   随机化算法在密码学中有着巨大的应用。
*   [负载平衡](https://www.geeksforgeeks.org/load-balancing-on-servers-random-algorithm/)。
*   数论应用:[素性检验](https://en.wikipedia.org/wiki/Solovay%E2%80%93Strassen_primality_test)
*   数据结构:散列、排序、搜索、[顺序统计](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)和计算几何。
*   代数恒等式:多项式和[矩阵恒等式验证](https://en.wikipedia.org/wiki/Randomized_algorithm#Verifying_matrix_multiplication)。交互式证明系统。
*   数学规划:线性规划的快速算法，将线性规划解舍入为整数规划解
*   图算法:最小生成树，最短路径，[最小割](https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-1-introduction-and-implementation/)。
*   计数和枚举:矩阵永久计数组合结构。
*   并行和分布式计算:避免死锁分布式共识。
*   概率存在证明:表明从一个合适的概率空间中抽取的对象中，一个组合对象以非零概率出现。
*   去随机化:首先设计一个随机算法，然后论证它可以去随机化以产生一个确定性算法。

**来源:**T2[http://theory.stanford.edu/people/pragh/amstalk.pdf](http://theory.stanford.edu/people/pragh/amstalk.pdf)T5[https://en.wikipedia.org/wiki/Randomized_algorithm](https://en.wikipedia.org/wiki/Randomized_algorithm)

本文由 **Ashish Sharma** 供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论