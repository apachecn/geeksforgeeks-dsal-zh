# 哈密顿圈是 NP 完全的证明

> 原文:[https://www . geesforgeks . org/proof-Hamiltonian-cycle-is-NP-complete/](https://www.geeksforgeeks.org/proof-that-hamiltonian-cycle-is-np-complete/)

**先决条件:**[NP-完全性](https://www.geeksforgeeks.org/np-completeness-set-1/)[哈密顿圈](https://www.geeksforgeeks.org/hamiltonian-cycle-backtracking-6/)。

**哈密顿圈:**无向图 G =(V，E)中恰好遍历每个顶点一次的圈。

**问题陈述:**给定一个图 G(V，E)，问题是确定该图是否包含由属于 V 的所有顶点组成的哈密顿圈。
**解释–**
问题的一个实例是指定给问题的输入。独立集问题的一个例子是图 G (V，E)，问题是检查图在 G 中是否可以有哈密顿圈
由于 NP-Complete 问题，顾名思义，是一个既有 NP 又有 NP-hard 的问题，所以证明问题是 NP-Complete 的陈述由两部分组成:

> 1.  The problem itself lies in NP class.
> 2.  All other problems in NP class can be reduced to that by polynomial time.
>     (b is a polynomial time reducible to c, expressed as ![B$\leqslant_P$C](img/704e99eabfa939687e3f42fed6bce836.png "Rendered by QuickLaTeX.com"))

如果仅满足第二个条件，则问题称为 **NP-Hard** 。

但是不可能把每一个 NP 问题都化为另一个 NP 问题来一直展示它的 NP 完全性。这就是为什么如果我们想展示一个问题是 NP-Complete，我们只是展示这个问题在 **NP** 中，如果有 **NP-Complete** 问题可以简化为这个，那么我们就完成了，即如果 B 是 NP-Complete，而![B$\leqslant_P$C](img/704e99eabfa939687e3f42fed6bce836.png "Rendered by QuickLaTeX.com")是 NP 中的 C，那么 C 就是 NP-Complete。

1.  **哈密顿圈在 NP 中**
    如果有任何问题在 NP 中，那么，给定一个*‘证书’*，这是问题的解和问题的一个实例(在这种情况下是一个图 G 和一个正整数 k)，我们将能够在多项式时间内验证(检查给出的解是否正确)证书。
    证书是图中形成哈密顿圈的顶点序列。我们可以通过验证所有顶点都属于该图，并且属于该解的每对顶点都是相邻的来验证该解。这可以在多项式时间内完成，即 **O(V +E)** 对图 G(V，E)使用以下策略:

    ```
    flag=true
    For every pair {u, v} in the subset V’:
        Check that these two have an edge between them
        If there is no edge, set flag to false and break
    If flag is true:
        Solution is correct
    Else:
        Solution is incorrect

    ```

2.  **Hamiltonian Cycle is NP Hard**
    In order to prove the Hamiltonian Cycle is NP-Hard, we will have to reduce a known NP-Hard problem to this problem. We will carry out a reduction from the [Hamiltonian Path problem](https://www.geeksforgeeks.org/proof-hamiltonian-path-np-complete/) to the Hamiltonian Cycle problem.
    Every instance of the Hamiltonian Path problem consisting of a graph **G =(V, E)** as the input can be converted to Hamiltonian Cycle problem consisting of graph **G’ = (V’, E’)**. We will construct the graph G’ in the following way:
    *   **V'** =添加原始图 G 的顶点 V，并添加一个额外的顶点 **V <sub>新的</sub>** ，这样图的所有连接的顶点都连接到这个顶点。顶点数增加 1， **V' =V+1** 。
    *   **E'** =添加原始图 G 的边 E，并在新添加的顶点和图的原始顶点之间添加新的边。边数增加顶点数 V，即 **E'=E+V** 。

    新的图 G’可以在多项式时间内获得，通过给新的顶点添加新的边，这需要 O(V)时间。这种减少可以通过以下两种说法来证明:

    *   让我们假设图 G 包含覆盖图的 **V** 顶点的哈密尔顿路径，从一个随机的顶点开始说 **V <sub>开始</sub>T5】并在 Vend 结束，现在既然我们将所有的顶点连接到图 G 中任意的新顶点 **V <sub>new</sub>** 。
        我们通过使用边**V<sub>end</sub>T14】到**V<sub>new</sub>T18】和 V <sub>new</sub> 到 V <sub>start</sub> 分别将原来的哈密顿路径扩展到一个哈密顿圈。图形**G’**现在包含遍历所有顶点一次的闭合循环。******
    *   我们假设图**G’**具有通过所有顶点的*哈密顿圈*，包括 **V <sub>新</sub>** 。现在将其转换为*哈密顿路径*，我们移除循环中顶点 **V <sub>新</sub>** 对应的边。得到的路径将覆盖图的顶点 V，并且只覆盖它们一次。

![](img/d9b00fa90d6075f95e8f88f1c7cab58a.png)

因此我们可以说图**G’**包含一个*哈密顿圈*if 图 **G** 包含一个*哈密顿路径*。因此，*哈密顿圈*问题的任何实例都可以简化为*哈密顿路径*问题的实例。因此*哈密顿圈*是 **NP-Hard** 。

**结论:**既然，*哈密顿圈*既是，一个**NP-问题**又是 **NP-Hard** 。所以是一个 **NP-Complete** 问题。