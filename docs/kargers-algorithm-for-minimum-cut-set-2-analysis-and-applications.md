# 最小割集 2 的卡尔格算法(分析与应用)

> 原文:[https://www . geeksforgeeks . org/kar gers-最小割集算法-2-分析和应用/](https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-2-analysis-and-applications/)

我们已经在下面介绍和讨论了第 1 集的[卡尔格算法](https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-1-introduction-and-implementation/)。

```
1)  Initialize contracted graph CG as copy of original graph
2)  While there are more than 2 vertices.
      a) Pick a random edge (u, v) in the contracted graph.
      b) Merge (or contract) u and v into a single vertex (update 
         the contracted graph).
      c) Remove self-loops
3) Return cut represented by two vertices.
```

如前一篇文章所述，[卡尔格算法](https://www.geeksforgeeks.org/kargers-algorithm-for-minimum-cut-set-1-introduction-and-implementation/)并不总是能找到最小割。在这篇文章中，讨论了找到最小割的概率。

***卡尔格算法产生的割为最小割的概率大于等于 1/(n <sup>2</sup> )***

**证明:**
假设给定图有唯一的最小割，且最小割中有 C 条边，边为{e <sub>1</sub> ，e <sub>2</sub> ，e <sub>3</sub> ，..e <sub>c</sub> }。当且仅当集合{e <sub>1</sub> 、e <sub>2</sub> 、e <sub>3</sub> 中没有边时，卡尔格算法才会产生此最小割，..e <sub>c</sub> 在上述算法的主 while 循环中迭代删除。
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

***第一次迭代选择最小割边的概率:***

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

***第二次迭代选择最小割边的概率:***

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

***在所有迭代中选择最小割边的概率:***

```

P[S1' ∩  S2' ∩ S3'  ∩.......... ∩ Sn-2']

>= [1 - 2/n] * [1 - 2/(n-1)] * [1 - 2/(n-2)] * [1 - 2/(n-3)] *...
                              ... * [1 - 2/(n - (n-4)] * [1 - 2/(n - (n-3)]

>= [(n-2)/n] * [(n-3)/(n-1)] * [(n-4)/(n-2)] * .... 2/4 * 2/3

>= 2/(n * (n-1))
>= 1/n2 
```

**如何增加成功概率？**
以上基本算法成功的概率很少。例如，对于有 10 个节点的图，找到最小割的概率大于或等于 1/100。通过重复运行基本算法并返回找到的所有切割的最小值，可以增加概率。

**应用程序:**
**1)** 在战争情况下，一方会有兴趣找到破坏敌方通信网络的最小数量的链路。

**2)** 最小割问题可用于研究网络的可靠性(可失效的最小边数)。

**3)** 网络优化研究(求最大流量)。

**4)** 聚类问题(像关联规则一样的边)匹配问题(有向图中最小割的 [NC](https://en.wikipedia.org/wiki/NC_%28complexity%29) 算法将导致二分图中最大匹配的 [NC](https://en.wikipedia.org/wiki/NC_%28complexity%29) 算法)

**5)** 匹配问题(有向图中最小割的 NC 算法将导致二分图中最大匹配的 NC 算法)

**资料来源:**
[https://www . YouTube . com/watch？v =-uuivvyhpas](https://www.youtube.com/watch?v=-UuivvyHPas)
[http://disi . unal . edu . co/~ ghernandezp/PSC/readings/02/mincut . pdf](http://disi.unal.edu.co/~gjhernandezp/psc/lectures/02/MinCut.pdf)

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。