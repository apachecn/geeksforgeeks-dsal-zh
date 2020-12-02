# 证明集团决策问题是 NP 完全的| 设置 2

> 原文： [https://www.geeksforgeeks.org/proof-that-clique-decision-problem-is-np-complete-set-2/](https://www.geeksforgeeks.org/proof-that-clique-decision-problem-is-np-complete-set-2/)

**先决条件：** [NP 完整性](https://www.geeksforgeeks.org/np-completeness-set-1/)，[集团问题](https://en.wikipedia.org/wiki/Clique_problem)。

图形中的集团是一组顶点，其中每个顶点与其他每个顶点共享一条边。 因此，图中的集团是一个完整图的子图。
**问题：**给定一个图 G（V，E）和一个整数 K，问题在于确定该图是否包含大小为 **K** 的集团。

**说明：**
问题的一个实例是为此问题指定的输入。 集团问题的一个实例是图 G（V，E）和正整数 K，问题是检查 G 中是否存在大小为 K 的集团。由于 NP 完全问题，按照定义，是一个问题 NP 和 NP 都是硬性的，关于问题是 NP 完全的陈述的证明包括两个部分：

> 1.  问题本身在 NP 类中
> 2.  在 NP 类中的所有其他问题都可以在多项式时间上得到。
>     （B 是可简化为 C 的多项式时间，表示为 ![B$\leqslant_P$C](img/704e99eabfa939687e3f42fed6bce836.png "Rendered by QuickLaTeX.com") ）。

如果仅满足第二条件，则该问题称为 **NP-Hard** 。

但是不可能将每个 NP 问题都简化为另一个 NP 问题以始终显示其 NP 完整性。 这就是为什么如果我们想证明问题是 NP-Complete，我们只是证明问题出在 **NP** 中，并且任何 **NP-Complete** 问题都可以解决，那么我们就完成了 ，即如果 **NP** 中的 **C** 的 **B** 是 **NP 完整的**和![B$\leqslant_P$C](img/704e99eabfa939687e3f42fed6bce836.png "Rendered by QuickLaTeX.com")，则 **C** 是 ** NP 完成**。

在本文中，我们将借助于[独立集](https://www.geeksforgeeks.org/proof-that-independent-set-in-graph-theory-is-np-complete/)问题（即 NP 完全）证明群体检测问题是 NP 完全的。 借助[布尔可满足性问题](https://www.geeksforgeeks.org/2-satisfiability-2-sat-problem/)，请参见[证明集团决策问题是 NP-完全](https://www.geeksforgeeks.org/proof-that-clique-decision-problem-is-np-complete/)的证明。

1.  **Clique Problem is in NP**
    If any problem is in NP, then, given a *‘certificate’*, which is a solution to the problem and an instance of the problem (a graph G and a positive integer K, in this case), we will be able to verify (check whether the solution given is correct or not) the certificate in polynomial time.

    证书是顶点的**子集 V'**，其中包括属于集团的顶点。 我们可以通过检查属于该解决方案的每对顶点是否相邻来验证此解决方案，只需简单地验证它们彼此共享一条边即可。 可以在多项式时间内，即 **O（V + E）**，使用以下策略来完成图形 **G（V，E）**：

    ```
    flag=true
    For every pair {u, v} in the subset V’:
        Check that these two
             vertices {u, v} share an edge
        If there is no edge,
          set flag to false and break
    If flag is true:
        Solution is correct
    Else:
        Solution is incorrect 

    ```

2.  **Clique Problem is NP-Hard**
    To prove that the clique problem is NP-Hard, we take the help of a problem that is already NP-Hard and show that this problem can be reduced to the Clique problem.
    For this, we consider the ***Independent Set problem***, which is **NP-Complete** (and hence **NP-Hard**). Every instance of the independent set problem consisting of the graph **G (V, E)** and an integer **K** can be converted to the required graph **G’ (V’, E’)** and **K’** of the Clique problem. We will construct the graph G’ by the following modifications:
    **V’ =V,** that is all the vertices of graph G are a part of the graph G’
    **E’** = complement of the edges E, that is, the edges not present in the original graph G.
    The graph **G’** is the complementary graph of G. The time required to compute the complementary graph **G’** requires a traversal over all the vertices and edges.
    ***Time complexity:** O (V+E)*

    现在我们将证明，计算集团的问题确实可以归结为独立集合的计算。 减少可以通过以下两个命题证明：

    *   让我们假设图 G 包含大小为 **K** 的集团。 集团的存在意味着 **G** 中存在 **K** 个顶点，其中每个顶点通过一条边与其余顶点相连。 这进一步表明，由于这些边缘包含在 **G** 中，因此它们不会出现在 **G'**中。 结果，这些 K 个顶点在 **G'**中彼此不相邻，因此形成了*大小为 **K*** 的独立集合。
    *   我们假设互补图 **G’**具有一组独立的顶点，其大小为 **K’**。 这些顶点均不与任何其他顶点共享边。 当我们对图进行补充以获得 **G，**时，这些 **K** 顶点将共享边，因此彼此相邻。 因此，图 **G** 的大小为 **K** 。

[![](img/1186b42d7b762cc6ee1db050f736a800.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200514000635/Untitled-Diagram-103.jpg)

因此，可以说，如果 **G'[** （互补图）。 因此，集团问题的任何实例都可以简化为独立集问题的实例。 因此，集团问题是 **NP-Hard。**

**结论：**

> 因此，集团决策问题是 NP 完全的



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。