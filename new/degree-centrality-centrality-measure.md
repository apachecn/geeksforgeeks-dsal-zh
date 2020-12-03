# 学位中心度（中心度）

> 原文： [https://www.geeksforgeeks.org/degree-centrality-centrality-measure/](https://www.geeksforgeeks.org/degree-centrality-centrality-measure/)

***度***
在图论中，图的顶点的度（或价）是入射到该顶点的边数，循环数为 2。[1] 顶点的程度![ v](img/0cee31e9a8eb7995804b7f41d3845812.png "Rendered by QuickLaTeX.com")表示为![ \deg(v)](img/23b3cacf06da31721004ac0b9f0d0567.png "Rendered by QuickLaTeX.com")或![ \deg v](img/247bc1d98e6c904c2ee121d320b12bf7.png "Rendered by QuickLaTeX.com")。 以![\Delta ](img/af3a9a417b4b5ca5d36b52c478070cf3.png "Rendered by QuickLaTeX.com")（G）表示的图 G 的最大度和以![\delta ](img/ce7b15c54a2188b2b8529beda0739b50.png "Rendered by QuickLaTeX.com")（G）表示的图的最小度是其顶点的最大和最小度。 在右边的图中，最大次数是 5，最小次数是 0。在规则图中，所有次数都是相同的，因此我们可以说图的次数。

**程度中心性**
历史上首先也是概念上最简单的是程度中心性，它定义为入射到节点上的链接数（即节点具有的联系数）。 可以根据节点捕获网络中任何流（例如病毒或某些信息）的直接风险来解释该程度。 在有向网络（联系有方向）的情况下，我们通常定义度中心度的两个独立度量，即度和度。 因此，“入度”是指向该节点的关系的数量的计数，而“出度”是该节点指向其他节点的关系的数量。 当关系与诸如友谊或合作之类的积极方面相关联时，经常将度数解释为一种流行形式，而将度数解释为合群。

对于具有![|V| ](img/81c8e3a613489be835f65f60edfd760f.png "Rendered by QuickLaTeX.com")顶点和![|E|](img/e51a37aa424237f472ffaf7960dd903e.png "Rendered by QuickLaTeX.com")边的给定图![G:=(V,E)](img/35fd59b45bd6e5b55589cd4526181960.png "Rendered by QuickLaTeX.com")，顶点![v](img/4e5b6a045192ef6498ad9dc76f6749da.png "Rendered by QuickLaTeX.com")的度中心定义为

![C_{D}(v)=\deg(v)](img/5c085fc7db251fb695735d8351c2993b.png "Rendered by QuickLaTeX.com")
对于图中所有节点的度中心度，在图的密集邻接矩阵表示中采用![\Theta(V^2)](img/d63b3dcad11caba9a6f8fec730abbca9.png "Rendered by QuickLaTeX.com")，对于边，在稀疏矩阵表示中采用![\Theta(E)](img/44d1cc30483caa80ab0c43b6667eaae9.png "Rendered by QuickLaTeX.com")。

节点级别的中心性定义可以扩展到整个图，在这种情况下，我们所说的是图中心化。 令![v*](img/b147be2121aa0e71e3050c682b33412f.png "Rendered by QuickLaTeX.com")为![G](img/96d783c7d76e5834a097a794b3cf074e.png "Rendered by QuickLaTeX.com")中具有最高度中心度的节点。 令![X:=(Y,Z)](img/0941caa4615058c25fb8cb3fb594e9fb.png "Rendered by QuickLaTeX.com")为使以下数量最大化的![|Y|](img/3642523848f27f19602aa4ab912ff314.png "Rendered by QuickLaTeX.com")节点连接图（其中![y*](img/cbc1248677a4e00498d52a68b468738f.png "Rendered by QuickLaTeX.com")为![X](img/59b7a374463461b94c69694c7948bf35.png "Rendered by QuickLaTeX.com")中度中心度最高的节点）：

![H=\sum _{{j=1}}^{{|Y|}}[C_{D}(y*)-C_{D}(y_{j})]](img/cc930ce3852614c85cbd671c2f43019d.png "Rendered by QuickLaTeX.com")
相应地，图![G](img/96d783c7d76e5834a097a794b3cf074e.png "Rendered by QuickLaTeX.com")的度中心化如下：

![C_D(G)= \frac{\displaystyle{\sum^{|V|}_{i=1}{[C_D(v*)-C_D(v_i)]}}}{H}](img/32b219800288e0f925c819be6c26d99f.png "Rendered by QuickLaTeX.com")
当图形![X](img/59b7a374463461b94c69694c7948bf35.png "Rendered by QuickLaTeX.com")包含一个所有其他节点都连接到的中心节点时（星形图），![H](img/41c87913a4bc754bd8374b4893df33f9.png "Rendered by QuickLaTeX.com")的值将最大化。

![{H=(n-1)\cdot ((n-1)-1)=n^{2}-3n+2}](img/232af6d9990b75d2ae6c788c1f45f078.png "Rendered by QuickLaTeX.com")。

以下是用于计算图及其各个节点的度中心性的代码。

```

import networkx as nx 

def degree_centrality(G, nodes): 
    r"""Compute the degree centrality for nodes in a bipartite network. 

    The degree centrality for a node `v` is the fraction of nodes  
    connected to it. 

    Parameters 
    ---------- 
    G : graph 
       A bipartite network 

    nodes : list or container 
      Container with all nodes in one bipartite node set. 

    Returns 
    ------- 
    centrality : dictionary 
       Dictionary keyed by node with bipartite degree centrality as the value. 

    Notes 
    ----- 
    The nodes input parameter must contain all nodes in one bipartite node set, 
    but the dictionary returned contains all nodes from both bipartite node 
    sets. 

    For unipartite networks, the degree centrality values are  
    normalized by dividing by the maximum possible degree (which is  
    `n-1` where `n` is the number of nodes in G).  

    In the bipartite case, the maximum possible degree of a node in a 
    bipartite node set is the number of nodes in the opposite node set 
    [1]_.  The degree centrality for a node `v` in the bipartite 
    sets `U` with `n` nodes and `V` with `m` nodes is 

    .. math:: 

        d_{v} = \frac{deg(v)}{m}, \mbox{for} v \in U , 

        d_{v} = \frac{deg(v)}{n}, \mbox{for} v \in V , 

    where `deg(v)` is the degree of node `v`.         

    """
    top = set(nodes) 
    bottom = set(G) - top 
    s = 1.0/len(bottom) 
    centrality = dict((n,d*s) for n,d in G.degree_iter(top)) 
    s = 1.0/len(top) 
    centrality.update(dict((n,d*s) for n,d in G.degree_iter(bottom))) 
    return centrality 

```

上面的函数是使用 networkx 库调用的，安装该库后，您最终可以使用它，并且以下代码必须用 python 编写，以实现节点的度中心性。

```

import networkx as nx 
G=nx.erdos_renyi_graph(100,0.5) 
d=nx.degree_centrality(G) 
print(d) 

```

结果如下：

```

{0: 0.5252525252525253, 1: 0.4444444444444445, 2: 0.5454545454545455, 3: 0.36363636363636365,  
4: 0.42424242424242425, 5: 0.494949494949495, 6: 0.5454545454545455, 7: 0.494949494949495,  
8: 0.5555555555555556, 9: 0.5151515151515152, 10: 0.5454545454545455, 11: 0.5151515151515152,  
12: 0.494949494949495, 13: 0.4444444444444445, 14: 0.494949494949495, 15: 0.4141414141414142,  
16: 0.43434343434343436, 17: 0.5555555555555556, 18: 0.494949494949495, 19: 0.5151515151515152,  
20: 0.42424242424242425, 21: 0.494949494949495, 22: 0.5555555555555556, 23: 0.5151515151515152,  
24: 0.4646464646464647, 25: 0.4747474747474748, 26: 0.4747474747474748, 27: 0.494949494949495,  
28: 0.5656565656565657, 29: 0.5353535353535354, 30: 0.4747474747474748, 31: 0.494949494949495,  
32: 0.43434343434343436, 33: 0.4444444444444445, 34: 0.5151515151515152, 35: 0.48484848484848486, 
 36: 0.43434343434343436, 37: 0.4040404040404041, 38: 0.5656565656565657, 39: 0.5656565656565657,  
40: 0.494949494949495, 41: 0.5252525252525253, 42: 0.4545454545454546, 43: 0.42424242424242425,  
44: 0.494949494949495, 45: 0.595959595959596, 46: 0.5454545454545455, 47: 0.5050505050505051, 
 48: 0.4646464646464647, 49: 0.48484848484848486, 50: 0.5353535353535354, 51: 0.5454545454545455, 
 52: 0.5252525252525253, 53: 0.5252525252525253, 54: 0.5353535353535354, 55: 0.6464646464646465,  
56: 0.4444444444444445, 57: 0.48484848484848486, 58: 0.5353535353535354, 59: 0.494949494949495,  
60: 0.4646464646464647, 61: 0.5858585858585859, 62: 0.494949494949495, 63: 0.48484848484848486,  
64: 0.4444444444444445, 65: 0.6262626262626263, 66: 0.5151515151515152, 67: 0.4444444444444445,  
68: 0.4747474747474748, 69: 0.5454545454545455, 70: 0.48484848484848486, 71: 0.5050505050505051, 
 72: 0.4646464646464647, 73: 0.4646464646464647, 74: 0.5454545454545455, 75: 0.4444444444444445, 
 76: 0.42424242424242425, 77: 0.4545454545454546, 78: 0.494949494949495, 79: 0.494949494949495,  
80: 0.4444444444444445, 81: 0.48484848484848486, 82: 0.48484848484848486, 83: 0.5151515151515152, 
 84: 0.494949494949495, 85: 0.5151515151515152, 86: 0.5252525252525253, 87: 0.4545454545454546,  
88: 0.5252525252525253, 89: 0.5353535353535354, 90: 0.5252525252525253, 91: 0.4646464646464647,  
92: 0.4646464646464647, 93: 0.5555555555555556, 94: 0.5656565656565657, 95: 0.4646464646464647, 
 96: 0.494949494949495, 97: 0.494949494949495, 98: 0.5050505050505051, 99: 0.5050505050505051} 

```

以上结果是描述每个节点的度中心值的字典。 以上是我关于集中度度量的文章系列的扩展。 保持联网！！！

**参考文献**
您可以在以下位置阅读有关此内容的更多信息

[https://en.wikipedia.org/wiki/Centrality#Degree_centrality](https://en.wikipedia.org/wiki/Centrality#Degree_centrality)
[http://networkx.readthedocs.io/en/networkx-1.10/index.html](http://networkx.readthedocs.io/en/networkx-1.10/index.html)

本文由 [**Jayant Bisht**](https://www.linkedin.com/in/jayant-bisht-978085114/) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

注意怪胎！ 通过 [**Python 编程基础**](https://practice.geeksforgeeks.org/courses/Python-Foundation?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=GFG_Article_Bottom_Python_Foundation) 课程加强基础，并学习基础知识。

首先，您的面试准备将通过 [**Python DS**](https://practice.geeksforgeeks.org/courses/Data-Structures-With-Python?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=GFG_Article_Bottom_Python_DS) 课程来增强您的数据结构概念。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。