# 3-着色为 NP 完成

> 原文:[https://www.geeksforgeeks.org/3-coloring-is-np-complete/](https://www.geeksforgeeks.org/3-coloring-is-np-complete/)

**先决条件:**[NP-完全性](https://www.geeksforgeeks.org/np-completeness-set-1/)[图形着色](https://www.geeksforgeeks.org/graph-coloring-applications/)

**<u>图 K-着色问题</u> :** 无向图的 K-着色问题是将颜色分配给图的节点，使得没有两个相邻的顶点具有相同的颜色，**最多使用 K** 种颜色来完成对图的着色。

**<u>问题陈述</u> :** 给定一个图 **G(V，E)** 和一个整数 K = 3，任务是确定该图是否可以使用**最多 3 种**颜色进行着色，使得没有两个相邻顶点被赋予相同的颜色。

**<u>解释</u>** :
问题的一个实例是指定给问题的输入。**3-着色问题**的一个实例是无向图 **G (V，E)** ，任务是检查每个顶点 **V** 是否存在可能的颜色分配，仅使用 3 种不同的颜色，每个相邻的颜色不同。由于 NP-Complete 问题是同时存在于 **NP** 和 **NP-hard** 中的问题，因此证明问题是 NP-Complete 的陈述由两部分组成:

> 1.  The problem itself lies in **NP class** .
> 2.  All other problems in NP class can be reduced to that by polynomial time. (b can be reduced to c by polynomial time and expressed as b ≤ p <sup>c</sup> )

如果**第二个条件**仅被满足，那么问题被称为 **NP-Hard** 。

但是不可能把每一个 NP 问题都化为另一个 NP 问题来一直展示它的 NP 完全性。因此，要证明一个问题是 NP-Complete，那么证明这个问题是在 **NP** 中，任何 **NP-Complete 问题**都可以简化为这个问题，即如果 B 是 NP-Complete，B≤P <sup>C</sup> 那么对于 NP 中的 C，那么 C 就是 NP-Complete。因此，使用以下两个命题可以得出**图 K-着色问题**是 NP-完全的结论:

**3-着色问题在 NP 中:**
如果 NP 中有任何问题，那么，给一个证书，它是问题的解决方案和问题的实例(A 图 **G(V，E)** 和颜色的分配 **{c <sub>1</sub> ，c <sub>2</sub> ，c <sub>3</sub> }** ，其中每个顶点从这三种颜色中被分配一种颜色 **{c <sub>1 c <sub>2</sub> ，c <sub>3</sub> }</sub>** ，则可以验证(检查给出的解是否正确)该证书在多项式时间内。 这可以通过以下方式实现:

> 对于图形 G 中的每条边{u，v}，验证颜色 c(u)！= c(v)

因此，可以在图的多项式时间内相对于它的边 0(V+E)检查赋值的正确性。

**3-着色问题是 NP-Hard:**
为了证明 3-着色问题是 NP-Hard，执行从已知的 NP-Hard 问题到该问题的约简。进行一个简化，从 3-SAT 问题可以简化为 3-着色问题。让我们假设 3-SAT 问题有一个关于 n 个变量的 m 个子句的 3-SAT 公式，由 **x <sub>1</sub> 、x <sub>2</sub> 、…、x <sub>n</sub>** 表示。然后，可以通过以下方式从公式中构建图表:

1.  对于每个变量**x<sub>I</sub>T3】在图中构造一个顶点**v<sub>I</sub>T7】和一个顶点 **v <sub>i'</sub>** 表示变量 **x <sub>i</sub>** 的否定。****
2.  对于 m 中的每个子句 c，添加对应于值 c1，c1，…，c5 的 5 个顶点。
3.  另外添加了三个不同颜色的顶点，分别表示值“真”、“假”和“底”。
4.  在这三个附加顶点 **T，F，B** 之间添加边，形成一个三角形。
5.  在顶点**v<sub>I</sub>T3】和**v<sub>I’</sub>T7】和 Base (B)之间添加边，形成三角形。****

**以下约束对于图 G 是正确的:**

1.  对于每对顶点**v<sub>I</sub>T3】和**v<sub>I’</sub>T7】，其中一个被赋予真值，另一个被赋予假值。****
2.  对于 m 子句中的每个子句 c，至少有一个文字必须持有真值，该值才为真。

因此，可以通过输入节点 u、V、w 为公式中的每个子句**c =(u V V w)**构建一个小的 OR- gadget 图，并将 gadget 的输出节点连接到 False 和 Base 特殊节点。

让我们考虑公式 **f = (u' V v V w')** 和 **(u V v V w')**

[![](img/91ed583a31e66c2205093ea691708066.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200918133430/Gaph11.jpg)

**现在可以用下面两个命题来证明约简:**
我们假设 3-SAT 公式有一个令人满意的赋值，那么在每个子句中，至少有一个文字 **x <sub>i</sub>** 必须为真，因此，相应的**v<sub>I</sub>T10】可以赋给一个 true 颜色，**v<sub>I’</sub>T14】赋给 FALSE。现在，扩展一下，对于每个子句，对应的 OR-gadget 图可以是 3 色的。因此，图形可以是 3 色的。****

让我们考虑图 G 是 3-可着色的，所以如果顶点 vi 被指定为真彩色，相应地变量 x <sub>i</sub> 被指定为真。这将形成一个法律真相分配。此外，对于任何子句 **C <sub>j</sub> = (x V y V z)** ，不可能所有三个文字 x，y，z 都为假。因为在这种情况下， **C <sub>j</sub>** 的 OR-gadget 图的输出必须被着色为 False。这是一个矛盾，因为输出连接到 Base 和 False。因此，3-SAT 条款有一个令人满意的分配。

**<u>结论</u> :** 因此，3-着色是一个 **NP-Complete** 问题。