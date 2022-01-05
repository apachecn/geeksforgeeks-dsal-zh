# 指派问题的匈牙利算法|集合 2(实现)

> 原文:[https://www . geesforgeks . org/Hungarian-赋值算法-问题集-2-实现/](https://www.geeksforgeeks.org/hungarian-algorithm-for-assignment-problem-set-2-implementation/)

给定一个 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**arr**大小 **N*N** 其中**arr【I】【j】**表示由 **i <sup>第</sup>** 号工人完成 **j <sup>第</sup>第**号工作的费用。任何工人都可以被指派做任何工作。任务是分配工作，这样一个工人可以精确地完成一项工作，使分配的总成本最小化。

**例**

> **输入:** arr[][] = {{3，5}，{10，1}}
> **输出:** 4
> **解释:**最佳分配是将作业 1 分配给第一个工人，作业 2 分配给第二个工人。
> 因此，最优成本为 3 + 1 = 4。
> 
> **输入:** arr[][] = {{2500，4000，3500}，{4000，6000，3500}，{2000，4000，2500}}
> **输出:** 4
> **解释:**最优分配是将作业 2 分配给第一个工人，作业 3 分配给第二个工人，作业 1 分配给第三个工人。
> 因此，最优成本为 4000 + 3500 + 2000 = 9500。

本文中讨论了解决这个问题的不同方法。

**方法:**思路是用[匈牙利算法](https://www.geeksforgeeks.org/hungarian-algorithm-assignment-problem-set-1-introduction/)解决这个问题。算法如下:

1.  对于矩阵的每一行，[找到最小的元素](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)并从其行中的每个元素中减去它。
2.  对所有列重复步骤 1。
3.  使用最小数量的水平线和垂直线覆盖矩阵中的所有零。
4.  **最优性测试**:如果覆盖线的最小数量为 **N** ，则可以进行最优分配。否则，如果行数小于 **N** ，则找不到最佳分配，必须继续执行步骤 5。
5.  确定未被任何线覆盖的最小条目。从每个未覆盖的行中减去该条目，然后将其添加到每个覆盖的列中。返回步骤 3。

考虑一个例子来理解这种方法:

> 让 2D 阵列成为:
> 
> 2500 4000 3500
> 4000 6000 3500
> 2000 4000 2500
> 
> **第一步:**减去每行的最小值。从第 1、2 和 3 行分别减去 2500、3500 和 2000。
> 
> 0 1500 1000
> 500 2500 0
> 0 2000 500
> 
> **第二步:**减去每列的最小值。从第 1、2 和 3 列分别减去 0、1500 和 0。
> 
> 0 0 1000
> 500 1000 0
> 0 500 500
> 
> **步骤 3:** 用最小数量的水平线和垂直线覆盖所有的零。
> 
> ![](img/461c95476ddc98629aa70f3733cbef6b.png)
> 
> **步骤 4:** 由于我们需要 3 行来覆盖所有的零，所以找到了最佳分配。
> 
> 2500**4000**3500
> 4000 6000**3500**T5**2000**4000 2500
> 
> 所以最优成本是 4000 + 3500 + 2000 = 9500

实现上述算法的思路是使用 **dlib 库**中定义的 **max_cost_assignment()** 函数。该函数是匈牙利算法(也称为库恩-蒙克斯算法)的实现，运行于*0(N<sup>3</sup>)*时间。它解决了最优分配问题。

下面是上述方法的实现:

## 计算机编程语言

```
# Python program for the above approach
import dlib

# Function to find out the best
# assignment of people to jobs so that
# total cost of the assignment is minimized
def minCost(arr):

    # Call the max_cost_assignment() function
    # and store the assignment
    assignment = dlib.max_cost_assignment(arr)

    # Print the optimal cost
    print(dlib.assignment_cost(arr, assignment))

# Driver Code

# Given 2D array
arr = dlib.matrix([[3, 5], [10, 1]])

# Function Call
minCost(arr)
```

**Output**

```
4
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*