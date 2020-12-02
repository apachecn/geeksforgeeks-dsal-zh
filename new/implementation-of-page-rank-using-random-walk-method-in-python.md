# 在 Python 中使用随机游走方法实现页面排名

> 原文： [https://www.geeksforgeeks.org/implementation-of-page-rank-using-random-walk-method-in-python/](https://www.geeksforgeeks.org/implementation-of-page-rank-using-random-walk-method-in-python/)

**先决条件**：[页面等级算法和实现](https://www.geeksforgeeks.org/page-rank-algorithm-implementation/)，[随机游走](https://www.geeksforgeeks.org/random-walk-implementation-python/)

在社交网络中，页面排名是一个非常重要的主题。 基本上，页面排名不过是根据网页的重要性和搜索相关性对网页进行排名的方式。 所有搜索引擎都使用页面排名。 Google 是使用网页图表使用网页排名的最佳示例。

**随机游动方法** –在随机游动方法中，我们将从图中均匀地随机选择 1 个节点。 选择节点后，我们将查看其邻居并随机地均匀选择一个邻居，并继续进行这些迭代，直到达到收敛为止。 在 N 次迭代之后，将出现一个点，之后每个节点的 In points 都将保持不变。 这种情况称为收敛。

**算法**：以下是实现随机游走方法的步骤。

1.  创建具有 N 个节点的有向图。
2.  现在执行随机行走。
3.  现在，在随机行走过程中获得按点排序的节点。
4.  最后，将其与内置的 PageRank 方法进行比较。

以下是用于实施积分分配算法的 python 代码。

## Python

```py

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

**输出**：

```
PageRank using Random Walk Method
[ 9 10  4  6  3  8 13 14  0  7  1  2  5 12 11]
PageRank using inbuilt pagerank method
9, 10, 6, 3, 4, 8, 13, 0, 14, 7, 1, 2, 5, 12, 11, 

```

注意怪胎！ 通过 [**Python 编程基础**](https://practice.geeksforgeeks.org/courses/Python-Foundation?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=GFG_Article_Bottom_Python_Foundation) 课程加强基础，并学习基础知识。

首先，您的面试准备将通过 [**Python DS**](https://practice.geeksforgeeks.org/courses/Data-Structures-With-Python?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=GFG_Article_Bottom_Python_DS) 课程来增强您的数据结构概念。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。