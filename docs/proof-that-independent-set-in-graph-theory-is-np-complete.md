# 证明图论中的独立集是 NP 完全

> 原文： [https://www.geeksforgeeks.org/proof-that-independent-set-in-graph-theory-is-np-complete/](https://www.geeksforgeeks.org/proof-that-independent-set-in-graph-theory-is-np-complete/)

**前提**：[NP 完整性](https://www.geeksforgeeks.org/np-completeness-set-1/)和[独立集](https://en.wikipedia.org/wiki/Independent_set_(graph_theory))。

图 **G =（V，E）**的独立集`S`是一组顶点，使得 S 中没有两个顶点彼此相邻。 它由不相邻的顶点组成。

**问题**：给定一个图 G（V，E）和一个整数 k，问题是要确定该图是否包含大小为> = k 的一组独立顶点。

**说明**：

问题的一个实例是为此问题指定的输入。 独立集问题的一个实例是图 G（V，E）和一个正整数 k，问题是检查 G 中是否存在大小为 k 的独立集。由于 NP 完全问题的定义是 NP 和 NP 都难的问题，证明问题是 NP-Complete 的证明包括两部分：

1.  问题本身在 NP 类中。

2.  NP 类中的所有其他问题都可以用多项式时间简化。

    （B 是可简化为 C 的多项式时间，表示为![B$\leqslant_P$C](img/704e99eabfa939687e3f42fed6bce836.png "Rendered by QuickLaTeX.com")）

如果仅满足第二条件，则该问题称为 **NP-Hard** 。

但是不可能将每个 NP 问题都简化为另一个 NP 问题以始终显示其 NP 完整性。 这就是为什么如果我们想证明问题是 NP-Complete，我们只显示问题在 NP 中，并且任何 NP-Complete 问题都可归结为 NP，那么我们就完成了，即如果 B 是 NP-Complete 并且![B$\leqslant_P$C](img/704e99eabfa939687e3f42fed6bce836.png "Rendered by QuickLaTeX.com") NP 中的 C，则 C 为 NP-Complete。

1.  **Independent Set is NP**

    If any problem is in NP, then, given a ‘certificate’, which is a solution to the problem and an instance of the problem (a graph G and a positive integer k, in this case), we will be able to verify (check whether the solution given is correct or not) the certificate in polynomial time.

    The certificate is a subset V’ of the vertices, which comprises the vertices belonging to the independent set. We can validate this solution by checking that each pair of vertices belonging to the solution are non-adjacent, by simply verifying that they don’t share an edge with each other. This can be done in polynomial time, that is O(V +E) using the following strategy of graph G(V, E):

    ```
    flag=true
    For every pair {u, v} in the subset V’:
        Check that these two don’t
        have an edge between them
        If there is an edge,
        set flag to false and break
    If flag is true:
        Solution is correct
    Else:
        Solution is incorrect

    ```

2.  **Independent Set is NP-Hard.**

    In order to prove that the Independent Set problem is NP-Hard, we will perform a reduction from a known NP-Hard problem to this problem. We will carry out a reduction from which the Clique Problem can be reduced to the Independent Set problem.

    Every instance of the clique problem consisting of the graph G (V, E) and an integer k can be converted to the required graph G’ (V’, E’) and k’ of the Independent Set problem. We will construct the graph G’ in the following way:

    > V’= V，即图 G 的所有顶点是图 G’的一部分。

    > E’=边 E 的补码，即原始图 G 中不存在的边。

    图 G'是 G 的互补图。计算互补图 G'所需的时间需要遍历所有顶点和边。 其时间复杂度为`O(V + E)`。

    现在，我们将证明计算独立集合的问题确实归结为集团的计算。 减少可以通过以下两个命题证明：

    *   让我们假设图 G 包含大小为 k 的集团。 团的存在意味着 G 中有 k 个顶点，其中每个顶点通过边与其余顶点相连。 这进一步表明，由于这些边包含在 G 中，因此它们不会出现在 G'中。 结果，这 k 个顶点在 G'中彼此不相邻，因此形成了大小为 k 的独立集。

    *   我们假设互补图 G’具有大小为 k’的一组独立顶点。 这些顶点均不与任何其他顶点共享边。 当我们对图进行补充以获得 G 时，这 k 个顶点将共享一条边，因此彼此相邻。 因此，图 G 的大小为 k。

![](img/8b87a1b82133978cebe3a7faf8ad3ac4.png)

因此，如果在 G’（互补图）中有大小为 k 的团簇，我们可以说在图形 G 中有一个独立的大小 k 集。 因此，独立集合问题的任何实例都可以简化为集团问题的实例。 因此，独立集合是 **NP-Hard。**

**结论**：

*由于独立集问题既是 NP 又是 NP-Hard，因此它是一个 NP-完全问题。*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。