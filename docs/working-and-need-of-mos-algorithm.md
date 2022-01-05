# 莫算法的工作与需求

> 原文:[https://www . geeksforgeeks . org/工作和需求的 mos 算法/](https://www.geeksforgeeks.org/working-and-need-of-mos-algorithm/)

[**莫氏算法**](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/) 是一个通用算法。它可以用于许多需要在[静态数组](https://www.geeksforgeeks.org/return-local-array-c-function/)中处理[范围查询](https://www.geeksforgeeks.org/array-data-structure/array-range-queries/)的问题，即数组值在查询之间不变。在每个查询中，对于给定的范围**【a，b】**，其思想是基于 **a** 和 **b** 位置之间的数组元素来计算值。由于数组是[静态的](https://www.geeksforgeeks.org/static-variables-in-c/)，查询可以任意顺序处理，**莫氏算法**以特殊顺序处理查询，保证算法高效工作。

它保持阵列的**活动范围**，并且关于**活动范围**的查询结果在每个时刻都是已知的。该算法逐个处理查询，并且总是通过插入和移除元素来移动活动范围的端点。

***时间复杂度:*** *O(N√N*f(N))* 、*其中数组有 **N** 元素，有 **N** 查询，每次插入和移除一个元素需要 ***O(f(N))*** 时间。*

*莫算法的诀窍在于处理查询的顺序:*

**   The array is divided into blocks of k = O(√N) elements. Before processing the queries **[a] <sub>2</sub> and b <sub>2</sub>** , one query **[A] <sub>1</sub> and b <sub>is processed first.</sub>***   Therefore, all queries with left end points in a certain block are processed in turn and sorted according to their right end points.*   Using this sequence, the algorithm only performs *o (n √ n)* operation, because the left end point moves *o (n)* times *o (√ n)* steps, and the right end point moves *o (√ n)* times *o.**   Therefore, the two endpoints moved by *o (n √ n)* steps in total during the algorithm.*

***示例:**考虑一个问题，其中给定了一组查询，每个查询对应于数组中的一个范围，任务是为每个查询计算该范围中**不同**元素的数量。在莫的算法中，查询总是以相同的方式排序，但这取决于如何维护查询答案的问题。*

**   In this problem, the idea is to maintain an array ***count []** *, where **count [x]** represents the number of times an element **x** appears in the activity range.*****   When moving from one query to another, the activity range changes. For example, if the current range is {4, **2,5,4,2** , 4,3,3,4}, the next range is {4,2, **5,4,2,4,3** , 3,4}. (The range is marked in bold)*   There will be three steps: the left end point moves one step to the right, and the right end point moves two steps to the right.*   After each step, the array **count []** needs to be updated.*   After adding an element **x** , the value of **count [x]** will be increased by **1** , and if **count [x] = 1** will also increase the answer to the query by **1** .*   Similarly, after an element **x** is removed, the value of **count [X]** is reduced by **1** , and if **count [X] = 0** later, the answer to the query is also reduced by **1.***   In this problem, the time required to execute each step is *o (1)* , so the total time complexity of the algorithm is *o (n √ n)* .T65】***