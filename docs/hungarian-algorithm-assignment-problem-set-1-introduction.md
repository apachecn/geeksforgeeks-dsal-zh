# 指派问题的匈牙利算法|集合 1(简介)

> 原文:[https://www . geesforgeks . org/Hungarian-算法-赋值-问题-集合-1-简介/](https://www.geeksforgeeks.org/hungarian-algorithm-assignment-problem-set-1-introduction/)

假设有 n 个代理和 n 个任务。任何代理都可以被分配来执行任何任务，所产生的成本可能会因代理任务的分配而异。要求执行所有任务时，每个任务只分配一个座席，每个座席只分配一个任务，这样可以使分配的总成本最小化。

**例:**你在一家芯片厂商做经理，目前有 3 个人在路上会见客户。你的销售人员在斋浦尔、浦那和班加罗尔，你希望他们飞往另外三个城市:德里、孟买和喀拉拉邦。下表显示了各城市之间的机票价格(印度卢比):

[![hungarian1](img/ec790db6f64fbb6c5e14e6d292501698.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/hungarian1.png)

问题是:为了尽量减少公平，你会把每个销售人员安排在哪里？

可能的分配:成本= 11000 印度卢比

[![hungerain2](img/299f5bd9c9c1453c6a348ee622bd09ff.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/hungerain2.png)

其他可能的分配:成本= **9500** INR，这是 **3 中最好的！**可能的任务。

[![hungarian4](img/5824ba3bc484d4cfd0f586ee860ea427.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/hungarian4.png)

**蛮力解**就是考虑每一个可能的赋值都隐含着一个复杂的**ω(n！)**。

**匈牙利算法，也称为 Munkres 赋值算法**，利用以下多项式运行时复杂度定理(**最坏情况 O(n <sup>3</sup> )** )和保证最优性:
*如果一个数被添加到成本矩阵的任何一行或一列的所有条目中或从其中减去，那么所得成本矩阵的最优赋值也是原始成本矩阵的最优赋值。*

我们利用上面的定理，把原来的权重矩阵降为零。我们尝试将任务分配给代理，使得每个代理只做一个任务，并且在每种情况下产生的惩罚是**零**。

**算法核心(假设方阵):**

1.  对于矩阵的每一行，找到最小的元素，并将其从该行的每个元素中减去。
2.  对所有列执行相同的操作(与步骤 1 相同)。
3.  使用最小数量的水平线和垂直线覆盖矩阵中的所有零。
4.  *最优性测试:*如果覆盖线的最小数量是 n，那么一个最优分配是可能的，我们就完成了。否则，如果行数小于 n，我们还没有找到最佳分配，必须继续执行步骤 5。
5.  确定未被任何线覆盖的最小条目。从每个未覆盖的行中减去该条目，然后将其添加到每个覆盖的列中。返回步骤 3。

**以上简单例子的解释:**

```

Below is the cost matrix of example given in above diagrams.
 2500  4000  3500
 4000  6000  3500
 2000  4000  2500

Step 1: Subtract minimum of every row.
2500, 3500 and 2000 are subtracted from rows 1, 2 and 
3 respectively.

   0   1500  1000
  500  2500   0
   0   2000  500

Step 2: Subtract minimum of every column.
0, 1500 and 0 are subtracted from columns 1, 2 and 3 
respectively.

   0    0   1000
  500  1000   0
   0   500  500

Step 3: Cover all zeroes with minimum number of 
horizontal and vertical lines.
![example](img/461c95476ddc98629aa70f3733cbef6b.png)

Step 4:  Since we need 3 lines to cover all zeroes,
we have found the optimal assignment. 
 2500  4000  3500
 4000  6000  3500
 2000  4000  2500

So the optimal cost is 4000 + 3500 + 2000 = 9500

```

**第一次尝试没有得到最优值的例子:**
在上面的例子中，第一次检查最优性确实给了我们解决方案。如果我们覆盖的行数小于 n 怎么办？

```

cost matrix:
 1500  4000  4500
 2000  6000  3500
 2000  4000  2500

Step 1: Subtract minimum of every row.
1500, 2000 and 2000 are subtracted from rows 1, 2 and 
3 respectively.

  0    2500  3000
  0    4000  1500
  0    2000   500

Step 2: Subtract minimum of every column.
0, 2000 and 500 are subtracted from columns 1, 2 and 3 
respectively.

  0     500  2500
  0    2000  1000 
  0      0      0 

Step 3: Cover all zeroes with minimum number of 
horizontal and vertical lines.
![example2](img/6ba188f67551e1590096d3ddb1334da8.png)

Step 4:  Since we only need 2 lines to cover all zeroes,
we have NOT found the optimal assignment. 

Step 5:  We subtract the smallest uncovered entry 
from all uncovered rows. Smallest entry is 500.
 -500    0   2000
 -500  1500   500
   0     0      0

Then we add the smallest entry to all covered columns, we get
   0     0   2000
   0   1500   500
  500    0      0

Now we return to Step 3:. Here we cover again using
lines. and go to Step 4:. Since we need 3 lines to 
cover, we found the optimal solution.
 1500  4000  4500
 2000  6000  3500
 2000  4000  2500

So the optimal cost is 4000 + 2000 + 2500 = 8500

```

在下一篇文章中，我们将讨论上述算法的实现。实现需要更多的步骤，因为我们需要找到最小的行数来覆盖使用程序的所有 0。

 **参考文献:**
[http://www . math . Harvard . edu/archive/20 _ spring _ 05/讲义/作业 _ 间接费用. pdf](http://www.math.harvard.edu/archive/20_spring_05/handouts/assignment_overheads.pdf)
[https://www.youtube.com/watch?v=dQDZNHwuuOY](https://www.youtube.com/watch?v=dQDZNHwuuOY)

本文由 **Yash Varyani** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。