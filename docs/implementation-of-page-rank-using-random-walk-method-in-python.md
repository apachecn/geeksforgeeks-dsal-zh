# Python 中使用随机游走方法实现页面排名

> 原文:[https://www . geeksforgeeks . org/python 中使用随机漫步方法实现页面排名/](https://www.geeksforgeeks.org/implementation-of-page-rank-using-random-walk-method-in-python/)

**前提:** [页面排名算法及实现](https://www.geeksforgeeks.org/page-rank-algorithm-implementation/)[随机游走](https://www.geeksforgeeks.org/random-walk-implementation-python/)

在社交网络中，页面排名是一个非常重要的话题。基本上，页面排名只不过是根据网页的重要性和搜索相关性对网页进行排名。所有搜索引擎都使用页面排名。谷歌是最好的例子，使用网页排名使用网络图。

**随机游走法**–在随机游走法中，我们将从图中统一随机选择 1 个节点。选择节点后，我们将查看它的邻居，随机选择一个邻居，并继续这些迭代，直到达到收敛。经过 N 次迭代后，一个点将出现，此后每个节点的点都不会发生变化。这种情况叫收敛。

**算法:**下面是实现随机游走方法的步骤。

1.  创建一个有 N 个节点的有向图。
2.  现在进行随机漫步。
3.  现在，在随机漫步过程中，根据点获得排序的节点。
4.  最后，将其与内置的 PageRank 方法进行比较。

下面是实现点分布算法的 python 代码。

## 蟒蛇 3

```
import networkx as nx
import random
import numpy as np

# Add directed edges in graph
def add_edges(g, pr):
    for each in g.nodes():
        for each1 in g.nodes():
            if (each != each1):
                ra = random.random()
                if (ra < pr):
                    g.add_edge(each, each1)
                else:
                    continue
    return g

# Sort the nodes
def nodes_sorted(g, points):
    t = np.array(points)
    t = np.argsort(-t)
    return t

# Distribute points randomly in a graph
def random_Walk(g):
    rwp = [0 for i in range(g.number_of_nodes())]
    nodes = list(g.nodes())
    r = random.choice(nodes)
    rwp[r] += 1
    neigh = list(g.out_edges(r))
    z = 0

    while (z != 10000):
        if (len(neigh) == 0):
            focus = random.choice(nodes)
        else:
            r1 = random.choice(neigh)
            focus = r1[1]
        rwp[focus] += 1
        neigh = list(g.out_edges(focus))
        z += 1
    return rwp

# Main
# 1\. Create a directed graph with N nodes
g = nx.DiGraph()
N = 15
g.add_nodes_from(range(N))

# 2\. Add directed edges in graph
g = add_edges(g, 0.4)

# 3\. perform a random walk
points = random_Walk(g)

# 4\. Get nodes rank according to their random walk points
sorted_by_points = nodes_sorted(g, points)
print("PageRank using Random Walk Method")
print(sorted_by_points)

# p_dict is dictionary of tuples
p_dict = nx.pagerank(g)
p_sort = sorted(p_dict.items(), key=lambda x: x[1], reverse=True)

print("PageRank using inbuilt pagerank method")
for i in p_sort:
    print(i[0], end=", ")
```

**输出:**

```
PageRank using Random Walk Method
[ 9 10  4  6  3  8 13 14  0  7  1  2  5 12 11]
PageRank using inbuilt pagerank method
9, 10, 6, 3, 4, 8, 13, 0, 14, 7, 1, 2, 5, 12, 11, 

```