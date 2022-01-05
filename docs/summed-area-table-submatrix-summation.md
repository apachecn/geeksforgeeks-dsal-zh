# 总面积表-子矩阵求和

> 原文:[https://www . geesforgeks . org/summered-area-table-submatrix-summary/](https://www.geeksforgeeks.org/summed-area-table-submatrix-summation/)

给定大小为 M×N 的矩阵，有大量的查询来寻找子矩阵和。查询的输入是子矩阵的左上和右下索引，子矩阵的和是找出。

如何对矩阵进行预处理，使子矩阵和查询能够在 O(1)时间内完成。

示例:

```
tli :  Row number of top left of query submatrix
tlj :  Column number of top left of query submatrix
rbi :  Row number of bottom right of query submatrix
rbj :  Column number of bottom right of query submatrix

Input: mat[M][N] = {{1, 2, 3, 4, 6},
                    {5, 3, 8, 1, 2},
                    {4, 6, 7, 5, 5},
                    {2, 4, 8, 9, 4} };
Query1: tli = 0, tlj = 0, rbi = 1, rbj = 1
Query2: tli = 2, tlj = 2, rbi = 3, rbj = 4
Query3: tli = 1, tlj = 2, rbi = 3, rbj = 3;

Output:
Query1: 11  // Sum between (0, 0) and (1, 1)
Query2: 38  // Sum between (2, 2) and (3, 4)
Query3: 38  // Sum between (1, 2) and (3, 3)

```

**朴素算法:**
我们可以循环所有的查询，在 O (q*(N*M))最坏的情况下计算每个查询，这对于大范围的数字来说太大了。

```
// Pseudo code of Naive algorithm.
Arr[][] = input_matrix
For each query:
    Input tli, tlj, rbi, rbj
    sum = 0
    for i from tli to tbi (inclusive):
        for j  from tlj to rbj(inclusive):
            sum += Arr[i][j]
    print(sum) 

```

**优化解决方案:**
[合计面积表](https://en.wikipedia.org/wiki/Summed_area_table)可以将这类查询缩减为 O(M*N)的预处理时间，每个查询将在 O(1)中执行。
面积求和表是一种数据结构和算法，用于快速有效地生成网格矩形子集的值的和。
求和区域表中任意点(x，y)的值只是(x，y)上方和左侧所有值的总和，包括:
![qww](img/ed40a2419daeb3ffc78969a01fb2389a.png)

优化的解决方案在下面的帖子中实现。
**[实施优化方案](https://www.geeksforgeeks.org/submatrix-sum-queries/)**

本文由 **Shubham Saxena** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。