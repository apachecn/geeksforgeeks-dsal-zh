# 优化的最长路径是 NP 完整

> 原文： [https://www.geeksforgeeks.org/optimized-longest-path-is-np-complete/](https://www.geeksforgeeks.org/optimized-longest-path-is-np-complete/)

**<u>优化的最长路径问题</u>**：优化的最长路径问题指出，给定图形`G`的一组顶点`V`和边线[`E`，任务是证明在一组节点 **V <sub>s</sub> 和 V <sub>e 之间至少有 K</sub>** 长度的路径。

**<u>问题陈述</u>**：给定一个图 **G（V，E，K）**和一组节点 **V <sub>s</sub> 和 V <sub>e</sub>** ，其结点序列的长度为**≥K** 。

**<u>解释</u>**：
问题的一个实例是为此问题指定的输入。 最优化最长路径问题的一个例子是 **G（V，E，V <sub>s</sub> ，V <sub>e</sub> ，K）**。 由于 [NP 完全问题](https://www.geeksforgeeks.org/np-completeness-set-1/)是 [**NP** 和 **NP-Hard**](https://www.geeksforgeeks.org/difference-between-np-hard-and-np-complete-problem/) 中都存在的问题，因此证明 问题是 NP-Complete 由两部分组成：

> 1.  问题本身在 NP 类中。
> 2.  NP 类中的所有其他问题都可以用多项式时间简化。
>     （B 是可简化为 C 的多项式时间，表示为 B≤P <sup>C</sup> ）

如果仅满足第二条件，则该问题称为 **NP-Hard** 。

但是不可能将每个 NP 问题都简化为另一个 NP 问题以始终显示其 NP 完整性。 这就是为什么如果我们想证明问题是 NP-Complete，我们只显示问题在 NP 中，并且任何 NP-Complete 问题都可以归结为问题，那么我们就可以完成，即如果 B 是 NP-Complete 且 B≤P <sup>C</sup> 对于 NP 中的 C，则 C 为 NP 完全。 因此，我们可以使用以下两个命题来验证**优化的最长路径问题**是 NP 完全的：

*   **<u>优化最长路径问题在 NP 中</u>**：
    如果 NP 中存在任何问题，请给出“证书”，这是对问题的解决方案，也是问题的一个实例 然后可以验证（检查给定的解是否正确）多项式时间内的证书。 这可以通过路径`P`完成，该路径由一组顶点< V <sub>1</sub> ，V <sub>2</sub> ，V <sub>3</sub> 组成 ，….V <sub>n</sub> >。 验证路径是否完全连接 V <sub>1</sub> 和 V <sub>n</sub> ，并且路径的长度最大为`K`。

*   **优化的最长路径问题是 NP-Hard**：
    为了证明最长路径是 NP-Hard，请推论出从已知的 NP-Hard 到问题。 进行还原，将无方向性的[哈密顿路径问题](https://www.geeksforgeeks.org/proof-hamiltonian-path-np-complete/)简化为最长路径问题。 无向哈密顿路径使用输入图 **G（V <sub>1</sub> ，V <sub>n</sub> ）**，其中图 G 具有节点 V <sub>1</sub> 和 V <sub>n</sub> 。 无向哈密顿路径是沿着图的无向路径，从一个顶点开始，到遍历所有节点的另一点终止。

    现在，使`K`为`G`中的节点数。 可以通过以下方式将无向哈密顿路径的每个实例转换为最长路径：
    对于输入 G（V <sub>1</sub> ，V <sub>n</sub> ），输出 G（V <sub>1</sub> ，V <sub>n</sub> ，k）。 通过简单地计算 G 中的顶点数，该约简花费了多项式时间。该约简可以通过以下两个命题证明：

    1.  假设原始图 **G（V，E）**具有节点 **V <sub>1</sub> 和 V <sub>n</sub>** 具有无向的哈密顿路径， 遍历所有顶点，因此 **G（V，E，K）**是正确的，因为`G`中的任何两个节点将通过长度等于其节点的路径连接，即`K`因此，最长路径问题成立。
    2.  Let us assume the graph **G'(V, E, V<sub>s</sub>, V<sub>e</sub>, K)** has a Lpath of length`K`from V<sub>s</sub> to V<sub>e</sub>, which implies **G’** contains a simple path of length`K`from V<sub>s</sub> to V<sub>e</sub>.
        But, G contains K vertices, hence traverses all vertices starting at V<sub>s</sub> and ending at V<sub>e</sub> forming a hamiltonian path, **G'(V<sub>s</sub>, V<sub>e</sub>)**.

        [![](img/3fb2cd740c16f9c057a0c39f8b73c492.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200922163129/ttyytft.jpg)

        令 V <sub>1</sub> B 和 V <sub>n</sub> D D
        现在，`G`具有无向哈密顿路径≡BCAD 为 **K = 4** 。
        因此，G 包含 B 和 D 之间长度= 4 的优化路径。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。