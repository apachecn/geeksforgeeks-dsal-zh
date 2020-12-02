# Karger 的“最小切割”算法| 第 2 组（分析和应用）

> 原文： [https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-2-analysis-and-applications/](https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-2-analysis-and-applications/)

下面我们介绍和讨论了集合 1 中的 [Karger 算法](https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-1-introduction-and-implementation/)。

```
1)  Initialize contracted graph CG as copy of original graph
2)  While there are more than 2 vertices.
      a) Pick a random edge (u, v) in the contracted graph.
      b) Merge (or contract) u and v into a single vertex (update 
         the contracted graph).
      c) Remove self-loops
3) Return cut represented by two vertices.
```

如前一篇文章所述， [Karger 的算法](https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-1-introduction-and-implementation/)并非总能找到最小切割。 在这篇文章中，讨论了找到最小切割的可能性。

***由 Karger 算法产生的剪切为 Min-Cut 的概率大于或等于 1 /（n <sup>2</sup> ）***

**证明**：
假设给定图形具有唯一的 Min-Cut，并且 Min-Cut 中存在 C 边，且边为{e <sub>1</sub> e e <sub>2</sub> ，e <sub>3</sub> ，.. e <sub>c</sub> }。 当且仅当集合{e <sub>1</sub> ，e <sub>2</sub> ，e <sub>3</sub> ，.. e 中的任何一个边都没有时，Karger 算法才会产生此 Min-Cut。 <sub>c</sub> }在上述算法的主 while 循环中被删除。
[![KargerProbability](img/e8d8284397f976edd3dbeee36b304968.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/KargerProbability.png)

```
c is number of edges in min-cut
m is total number of edges
n is total number of vertices

S1 = Event that one of the edges in {e1, e2, 
     e3, .. ec} is chosen in 1st iteration.
S2 = Event that one of the edges in {e1, e2, 
     e3, .. ec} is chosen in 2nd iteration.
S3 = Event that one of the edges in {e1, e2, 
     e3, .. ec} is chosen in 3rd iteration.

..................
..................

The cut produced by Karger's algorithm would be a min-cut if none of the above
events happen.

So the required probability is P[S1' ∩ S2' ∩ S3' ∩  ............]
```

***在第一次迭代中选择最小切割边的概率**：*

```
Let us calculate  P[S1']
P[S1]  = c/m
P[S1'] = (1 - c/m)

Above value is in terms of m (or edges), let us convert 
it in terms of n (or vertices) using below 2 facts.. 

1) Since size of min-cut is c, degree of all vertices must be greater 
than or equal to c. 

2) As per Handshaking Lemma, sum of degrees of all vertices = 2m

From above two facts, we can conclude below.
  n*c <= 2m m>= nc/2

  P[S1] <= c (cn 2) <="2/n" p[s1] <= c (cn 2) <="2/n" p[s<sub>1<sup>'</sup>] >= (1-2/n) ------------(1)=>=>=></sub>
```

***在第二次迭代中选择最小切割边的可能性**：*

```

P[S1' ∩  S2'] = P[S2' | S1' ] * P[S1']

In the above expression, we know value of P[S1'] >= (1-2/n)

P[S2' | S1'] is conditional probability that is, a min cut is 
not chosen in second iteration given that it is not chosen in first iteration

Since there are total (n-1) edges left now and number of cut edges is still c,
we can replace n by n-1 in inequality (1).  So we get.
  P[S2' | S1' ] >= (1 - 2/(n-1)) 

  P[S1' ∩  S2'] >= (1-2/n) x (1-2/(n-1))
```

***在所有迭代中选择最小切割边的概率**：*

```

P[S1' ∩  S2' ∩ S3'  ∩.......... ∩ Sn-2']

>= [1 - 2/n] * [1 - 2/(n-1)] * [1 - 2/(n-2)] * [1 - 2/(n-3)] *...
                              ... * [1 - 2/(n - (n-4)] * [1 - 2/(n - (n-3)]

>= [(n-2)/n] * [(n-3)/(n-1)] * [(n-4)/(n-2)] * .... 2/4 * 2/3

>= 2/(n * (n-1))
>= 1/n2 
```

**如何增加成功的可能性？**
上述基本算法成功的可能性很小。 例如，对于具有 10 个节点的图，找到最小切割的概率大于或等于 1/100。 可以通过重复运行基本算法并返回找到的所有削减的最小值来增加概率。

**应用程序**：
**1）**在战争情况下，一个政党有兴趣寻找破坏敌人通信网络的最小链接数。

**2）**最小割问题可用于研究网络的可靠性（可能出现故障的最小边缘数量）。

**3）**网络优化研究（查找最大流量）。

**4）**聚类问题（类似于关联规则的边）匹配问题（针对有向图的最小割的 [NC](https://en.wikipedia.org/wiki/NC_%28complexity%29) 算法将导致最大匹配的 [NC](https://en.wikipedia.org/wiki/NC_%28complexity%29) 算法 在二部图中）

**5）**匹配问题（有向图中最小割的 NC 算法将导致二部图中最大匹配的 NC 算法）

**来源**：
[https://www.youtube.com/watch?v=-UuivvyHPas](https://www.youtube.com/watch?v=-UuivvyHPas)
[http://disi.unal.edu.co /~gjhernandezp/psc/lectures/02/MinCut.pdf]( http://disi.unal.edu.co/~gjhernandezp/psc/lectures/02/MinCut.pdf)

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

