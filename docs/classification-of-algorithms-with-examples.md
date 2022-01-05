# 算法分类举例

> 原文:[https://www . geeksforgeeks . org/带示例的算法分类/](https://www.geeksforgeeks.org/classification-of-algorithms-with-examples/)

算法的分类方式有很多，下面展示了其中的几种:

1.  Implementation method
2.  Design method
3.  Other classifications

**实施方式分类:**

**1。递归或迭代**

*   A [recursive algorithm](https://www.geeksforgeeks.org/recursive-functions/) is an algorithm that calls itself repeatedly until the basic conditions are met. It is a common method in functional programming language, such as [C, C++](https://www.geeksforgeeks.org/difference-between-c-and-c/), etc.
*   Iterative algorithms use structures such as loops, and sometimes other data structures such as stacks and queues are used to solve problems.
*   Some problems are suitable for recursion and some for iteration. For example, [Hanoi Tower Problem](https://www.geeksforgeeks.org/c-program-for-tower-of-hanoi/) is easy to understand in recursive implementation. Each recursive version has an iterative version, and vice versa.

**2。程序性或声明性(非程序性)-**

*   在声明式编程语言中，我们说我们想要什么，而不必说如何去做。
*   对于过程编程，我们必须指定获得结果的确切步骤。例如， [SQL](https://www.geeksforgeeks.org/sql-tutorial/) 更多的是声明性的，而不是过程性的，因为查询没有指定产生结果的步骤。过程语言的例子包括 C、PHP 和 PERL。

**3。串行或并行或分布式-**

*   Generally speaking, when discussing algorithms, we assume that the computer executes one instruction at a time. These are called serial algorithms.
*   Parallel algorithm uses computer architecture to process several instructions at a time. They divide the problem into subproblems and provide them to several processors or threads. Iterations are usually parallel.
*   If parallel algorithms are distributed on different machines, then we call them distributed algorithms.

**4。确定性或非确定性-**

*   Deterministic algorithms solve problems through predefined processes, while nondeterministic algorithms guess the best solution at each step by using heuristic algorithms.

**5。精确或近似-**

*   The algorithm that we can find the optimal solution is called exact algorithm. In computer science, if we don't have the optimal solution, we give an approximate algorithm.
*   Approximation algorithm is generally associated with [NP-hard problem.](https://www.geeksforgeeks.org/difference-between-np-hard-and-np-complete-problem/)

**按设计方法分类:**

对算法进行分类的另一种方式是通过它们的设计方法。

**1。贪婪法-**

*   [Greedy algorithm](https://www.geeksforgeeks.org/greedy-algorithms/) works in stages.
*   At each stage, a good decision was made at that point, without worrying about the future consequences.
*   Generally speaking, this means choosing some of the best local products. It assumes that the local optimal selection is also beneficial to the global optimal solution.

**2。分治-**

[分治策略通过以下方式解决问题:](https://www.geeksforgeeks.org/divide-and-conquer-introduction/)

1.  划分:将问题分成子问题，子问题本身是同一类型问题的较小实例。
2.  递归:递归求解这些子问题。
3.  征服:适当结合他们的答案。

示例:合并排序和二分搜索法算法。

**3。动态编程-**

*   [Dynamic programming](https://www.geeksforgeeks.org/dynamic-programming/) (DP) works with rote learning. The difference between DP [and divide and conquer](https://www.geeksforgeeks.org/divide-and-conquer-introduction/) is that in the latter case, there is no dependency between subproblems, while in DP, subproblems will overlap. DP reduces the exponential complexity to polynomial complexity (O(n2), O(n3), etc.) by memorizing [maintaining the table of solved subproblems]. ) For many questions.
*   The difference between dynamic programming and recursion lies in the memory of recursive call. When the subproblem is independent, if there is no repetition, there is no memory.
*   Help, so dynamic planning is not the solution to all problems.
*   By using [to remember](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/) [maintain the solved subproblem table], dynamic programming reduces the complexity from exponential to polynomial.

**4。线性规划-**

*   In linear programming, there are inequalities in input and some linear functions that maximize (or minimize) input.
*   Many problems (such as the maximum flow of a directed graph) can be discussed by linear programming.

**5。约简【变换与征服】**

*   In this method, we solve a difficult problem by transforming it into a known problem. For this problem, we have an asymptotically optimal algorithm. In this method, the goal is to find a simplified algorithm whose complexity is not dominated by the final simplified algorithm. For example, the selection algorithm for finding intermediate values in a list involves sorting the list first, and then finding out the intermediate elements in the sorted list. These technologies are also called transformation and conquest.

**其他分类:**

**1。按研究领域分类-**

*   In computer science, every field has its own problems and needs efficient algorithms. Examples: search algorithm, sorting algorithm, merging algorithm, numerical algorithm, graphic algorithm, string algorithm, geometric algorithm, combination algorithm, machine learning, cryptography, parallel algorithm, data compression algorithm, parsing technology and so on.

**2。按复杂性分类-**

*   In this classification, the algorithm classifies according to its input size and the time it takes to find a solution. Some algorithms need linear time complexity (O(n)), some algorithms need exponential time, and some algorithms never stop. Please note that some problems may have multiple algorithms with different complexities.

**3。随机算法-**

*   Some algorithms make random choices. For some problems, the fastest solution must involve randomness. Example: [Quick sort.](https://www.geeksforgeeks.org/quick-sort/)