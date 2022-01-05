# 中间中心性(中心性测度)

> 原文:[https://www . geesforgeks . org/介数-中心性-中心性-测度/](https://www.geeksforgeeks.org/betweenness-centrality-centrality-measure/)

在图论中，中间中心性是基于最短路径的图中中心性的度量。对于连通图中的每一对顶点，顶点之间至少存在一条最短路径，使得该路径通过的边的数量(对于未加权的图)或边的权重之和(对于加权的图)最小。每个顶点的介数中心度是通过该顶点的最短路径数。

介数中心性在网络理论中有着广泛的应用:它代表了节点之间的距离。例如，在电信网络中，具有较高介数中心性的节点将对网络有更多的控制，因为更多的信息将通过该节点。中间中心性被设计为中心性的一般度量:它适用于网络理论中的广泛问题，包括与社会网络、生物学、运输和科学合作有关的问题。

***定义***

节点 v 的介数中心由以下表达式给出:

![ g(v)=\sum _{{s\neq v\neq t}}{\frac  {\sigma _{{st}}(v)}{\sigma _{{st}}}}](img/ed3a525b9694eb7878ae5ac3af43de8a.png "Rendered by QuickLaTeX.com")

其中![ \sigma_{st}](img/e4aece61033f804c7049e530e4bcecde.png "Rendered by QuickLaTeX.com")是从节点![s](img/27afaf2b0e3eaea3d7e963f3f9a730e2.png "Rendered by QuickLaTeX.com")到节点![ t](img/c9c2148481ddde233dd09ea71ac06c48.png "Rendered by QuickLaTeX.com")的最短路径总数，![ \sigma_{st}(v)](img/780b1a229426e9b739788b26d42b1168.png "Rendered by QuickLaTeX.com")是经过![ v](img/0cee31e9a8eb7995804b7f41d3845812.png "Rendered by QuickLaTeX.com")的路径数。

请注意，节点的介数中心性与求和指数所暗示的节点对的数量成比例。因此，可以通过除以不包括![ v](img/0cee31e9a8eb7995804b7f41d3845812.png "Rendered by QuickLaTeX.com")的节点对的数量来重新调整计算，使得![g\in [0,1]](img/3b5cb87b61e4d3d0e18e8dfd60f385c0.png "Rendered by QuickLaTeX.com")。有向图的划分由![ (N-1)(N-2)](img/8c4dd24fd05b798d088fadef41231cd1.png "Rendered by QuickLaTeX.com")完成，无向图的划分由![ (N-1)(N-2)/2](img/183eb681d707128041e16ee48d8c836d.png "Rendered by QuickLaTeX.com")完成，其中![ N](img/d73551c7c27f3005e675d3aaad33ae32.png "Rendered by QuickLaTeX.com")是巨型组件中的节点数。请注意，这将扩展到最高可能值，即每个最短路径都穿过一个节点。通常情况并非如此，可以在不损失精度的情况下执行规范化

![{\mbox{normal}}(g(v))={\frac  {g(v)-\min(g)}{\max(g)-\min(g)}}](img/5e910222fcd769882cf7784175cb4868.png "Rendered by QuickLaTeX.com")
导致:

![ \max(normal)=1](img/cc81ca78e8b56722ab03cecb5c070574.png "Rendered by QuickLaTeX.com")
![ \min(normal)=0](img/54234953da5ca2d03d398f6d7323b8f9.png "Rendered by QuickLaTeX.com")
请注意，这将始终是从较小范围到较大范围的缩放，因此不会丢失精度。

***【加权网络】***
在加权网络中，连接节点的链路不再被视为二元交互，而是根据它们的容量、影响、频率等按比例加权。，这就在拓扑效应之外，增加了网络内部异质性的另一个维度。加权网络中节点的强度由其相邻边的权重之和给出。

![ s_{{i}}=\sum _{{j=1}}^{{N}}a_{{ij}}w_{{ij}}](img/a0a95caf85bb442f2fd73799d3ff6573.png "Rendered by QuickLaTeX.com")
![ a_{ij}](img/eaf82fc986502804443cc4bedca91fef.png "Rendered by QuickLaTeX.com")和![ w_{ij}](img/8fa70ae99a1cef5303db163235193d31.png "Rendered by QuickLaTeX.com")分别是节点![ i](img/3a2ba36c8e4291c2cd213ceabc5973ae.png "Rendered by QuickLaTeX.com")和![ j](img/679ee478a61eaab867b75af9fc9fad1d.png "Rendered by QuickLaTeX.com")之间的邻接矩阵和权重矩阵。类似于无标度网络中的幂律度分布，给定节点的强度也遵循幂律分布。

![ s(k)\approx k^{\beta }](img/5563227959b13ea64ec87a7161aada41.png "Rendered by QuickLaTeX.com")
对具有介数![ b](img/8446b80aee76e02e980458eb46a4cd27.png "Rendered by QuickLaTeX.com")的顶点的强度的平均值![ s(b)](img/f247014c37531c2d920e0aca4d653768.png "Rendered by QuickLaTeX.com")的研究表明，函数行为可以通过缩放形式来近似

![ s(b)\approx b^{{\alpha }}](img/ce225fccd49629c2390034557e988802.png "Rendered by QuickLaTeX.com")

下面是计算图及其各个节点的介数中心性的代码。

```
def betweenness_centrality(G, k=None, normalized=True, weight=None,
                           endpoints=False, seed=None):
    r"""Compute the shortest-path betweenness centrality for nodes.

    Betweenness centrality of a node $v$ is the sum of the
    fraction of all-pairs shortest paths that pass through $v$

    .. math::

       c_B(v) =\sum_{s,t \in V} \frac{\sigma(s, t|v)}{\sigma(s, t)}

    where $V$ is the set of nodes, $\sigma(s, t)$ is the number of
    shortest $(s, t)$-paths,  and $\sigma(s, t|v)$ is the number of
    those paths  passing through some  node $v$ other than $s, t$.
    If $s = t$, $\sigma(s, t) = 1$, and if $v \in {s, t}$,
    $\sigma(s, t|v) = 0$ [2]_.

    Parameters
    ----------
    G : graph
      A NetworkX graph.

    k : int, optional (default=None)
      If k is not None use k node samples to estimate betweenness.
      The value of k <= n where n is the number of nodes in the graph.
      Higher values give better approximation.

    normalized : bool, optional
      If True the betweenness values are normalized by `2/((n-1)(n-2))`
      for graphs, and `1/((n-1)(n-2))` for directed graphs where `n`
      is the number of nodes in G.

    weight : None or string, optional (default=None)
      If None, all edge weights are considered equal.
      Otherwise holds the name of the edge attribute used as weight.

    endpoints : bool, optional
      If True include the endpoints in the shortest path counts.

    Returns
    -------
    nodes : dictionary
       Dictionary of nodes with betweenness centrality as the value.

    Notes
    -----
    The algorithm is from Ulrik Brandes [1]_.
    See [4]_ for the original first published version and [2]_ for details on
    algorithms for variations and related metrics.

    For approximate betweenness calculations set k=#samples to use
    k nodes ("pivots") to estimate the betweenness values. For an estimate
    of the number of pivots needed see [3]_.

    For weighted graphs the edge weights must be greater than zero.
    Zero edge weights can produce an infinite number of equal length
    paths between pairs of nodes.

    """
    betweenness = dict.fromkeys(G, 0.0)  # b[v]=0 for v in G
    if k is None:
        nodes = G
    else:
        random.seed(seed)
        nodes = random.sample(G.nodes(), k)
    for s in nodes:

        # single source shortest paths
        if weight is None:  # use BFS
            S, P, sigma = _single_source_shortest_path_basic(G, s)
        else:  # use Dijkstra's algorithm
            S, P, sigma = _single_source_dijkstra_path_basic(G, s, weight)

        # accumulation
        if endpoints:
            betweenness = _accumulate_endpoints(betweenness, S, P, sigma, s)
        else:
            betweenness = _accumulate_basic(betweenness, S, P, sigma, s)

    # rescaling
    betweenness = _rescale(betweenness, len(G), normalized=normalized,
                           directed=G.is_directed(), k=k)
    return betweenness
```

上面的函数是使用 networkx 库调用的，一旦安装了这个库，您就可以最终使用它，下面的代码必须用 python 编写，以实现节点的介数中心性。

```
>>> import networkx as nx
>>> G=nx.erdos_renyi_graph(50,0.5)
>>> b=nx.betweenness_centrality(G)
>>> print(b)
```

它的结果是:

```
{0: 0.01220586070437195, 1: 0.009125402885768874, 2: 0.010481510111098788, 3: 0.014645690907182346, 
4: 0.013407129955492722, 5: 0.008165902336070403, 6: 0.008515486873573529, 7: 0.0067362883337957575, 
8: 0.009167651113672941, 9: 0.012386122359980324, 10: 0.00711685931010503, 11: 0.01146358835858978, 
12: 0.010392276809830674, 13: 0.0071149912635190965, 14: 0.011112503660641336, 15: 0.008013362669468532,
 16: 0.01332441710128969, 17: 0.009307485134691016, 18: 0.006974541084171777, 19: 0.006534636068324543, 
20: 0.007794762718607258, 21: 0.012297442232146375, 22: 0.011081427155225095, 23: 0.018715475770172643,
 24: 0.011527827410298818, 25: 0.012294312339823964, 26: 0.008103941622217354, 27: 0.011063824792934858,
 28: 0.00876321613116331, 29: 0.01539738650994337, 30: 0.014968892689224241, 31: 0.006942569786325711,
 32: 0.01389881951343378, 33: 0.005315473883526104, 34: 0.012485048548223817, 35: 0.009147849010405877,
 36: 0.00755662592209711, 37: 0.007387027127423285, 38: 0.015993065123210606, 39: 0.0111516804297535,
 40: 0.010720274864419366, 41: 0.007769933231367805, 42: 0.009986222659285306, 43: 0.005102869708942402,
 44: 0.007652686310399397, 45: 0.017408689421606432, 46: 0.008512679806690831, 47: 0.01027761151708757, 
48: 0.008908600658162324, 49: 0.013439198921385216}
```

上面的结果是描述每个节点介数中心值的字典。以上是我关于中心性度量的文章系列的扩展。保持联系！！！

***参考文献***
你可以在

*   [https://en.wikipedia.org/wiki/Betweenness_centrality](https://en.wikipedia.org/wiki/Betweenness_centrality)*   [http://networkx.readthedocs.io/en/networkx-1.10/index.html](http://networkx.readthedocs.io/en/networkx-1.10/index.html)

    。

    本文由 [**贾扬特**](https://auth.geeksforgeeks.org/profile.php?user=Jayant Bisht) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。