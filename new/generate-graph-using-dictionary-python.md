# 使用 Python 中的字典生成图形

> 原文： [https://www.geeksforgeeks.org/generate-graph-using-dictionary-python/](https://www.geeksforgeeks.org/generate-graph-using-dictionary-python/)

先决条件– [图](https://www.geeksforgeeks.org/graph-and-its-representations/)
要在内置库中使用图绘制– [在 Python](https://www.geeksforgeeks.org/graph-plotting-in-python-set-1/) 中绘制图
在本文中，我们将介绍如何在[中使用 python 实现图。 字典中的](http://quiz.geeksforgeeks.org/python-set-4-dictionary-keywords-python/)数据结构。
所使用的字典的键是我们图的节点，而对应的值是每个节点的列表，它们通过一条边连接。
此简单图具有六个节点（a-f）和五个弧：

```
a -> c
b -> c
b -> e
c -> a
c -> b
c -> d
c -> e
d -> c
e -> c
e -> b

```

它可以由以下 Python 数据结构表示。 这是一本字典，其键是图形的节点。 对于每个键，对应的值是一个列表，其中包含通过该节点的直接弧连接的节点。

```
graph = { "a" : ["c"],
          "b" : ["c", "e"],
          "c" : ["a", "b", "d", "e"],
          "d" : ["c"],
          "e" : ["c", "b"],
          "f" : []
        } 

```

**以上示例的图形表示**：[

![python](img/d9ad3ae8e0a8572d36c4e9825088daff.png)

[defaultdict](https://docs.python.org/2/library/collections.html#collections.defaultdict) ：通常，如果您尝试使用字典中当前不在的键来获取项，则 Python 字典会引发 KeyError。 defaultdict 允许如果在字典中找不到键，则创建新条目，而不是引发 KeyError。 此新条目的类型由 defaultdict 的参数给出。
**Python 函数生成图形**：

```
# definition of function
def generate_edges(graph):
    edges = []

    # for each node in graph
    for node in graph:

        # for each neighbour node of a single node
        for neighbour in graph[node]:
            # if edge exists then append
            edges.append((node, neighbour))
    return edges

```

## Python

```py

# Python program for 
# validation of a graph

# import dictionary for graph
from collections import defaultdict

# function for adding edge to graph
graph = defaultdict(list)
def addEdge(graph,u,v):
    graph[u].append(v)

# definition of function
def generate_edges(graph):
    edges = []

    # for each node in graph
    for node in graph:

        # for each neighbour node of a single node
        for neighbour in graph[node]:

            # if edge exists then append
            edges.append((node, neighbour))
    return edges

# declaration of graph as dictionary
addEdge(graph,'a','c')
addEdge(graph,'b','c')
addEdge(graph,'b','e')
addEdge(graph,'c','d')
addEdge(graph,'c','e')
addEdge(graph,'c','a')
addEdge(graph,'c','b')
addEdge(graph,'e','b')
addEdge(graph,'d','c')
addEdge(graph,'e','c')

# Driver Function call 
# to print generated graph
print(generate_edges(graph)) 

```

输出：

```
[('a', 'c'), ('c', 'd'), ('c', 'e'), ('c', 'a'), ('c', 'b'), 
('b', 'c'), ('b', 'e'), ('e', 'b'), ('e', 'c'), ('d', 'c')]

```

由于我们以无向图为例，因此我们两次打印出相同的边，即（'a'，'c'）和（'c'，'a'）。 我们可以通过使用有向图来克服这一问题。
以下是 python 中关于图形的更多程序：

1.  **要生成从一个节点到另一节点的路径**：
    使用 Python 字典，我们可以在 Graph 中找到从一个节点到另一节点的路径。 这个想法类似于图形中的 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 。
    在该函数中，路径最初是一个空列表。 在开始时，如果开始节点与结束节点匹配，则函数将返回路径。 否则，代码将前进并击中起始节点的所有值，并使用递归搜索路径。

## Python

```py

# Python program to generate the first
# path of the graph from the nodes provided

graph = {
    'a': ['c'],
    'b': ['d'],
    'c': ['e'],
    'd': ['a', 'd'],
    'e': ['b', 'c']
}

# function to find path

def find_path(graph, start, end, path=[]):
    path = path + [start]
    if start == end:
        return path
    for node in graph[start]:
        if node not in path:
            newpath = find_path(graph, node, end, path)
            if newpath:
                return newpath

# Driver function call to print the path
print(find_path(graph, 'd', 'c'))

```

1.  输出：

```
['d', 'a', 'c']

```

2.  **程序生成从一个节点到另一节点的所有可能路径。** ：
    在上面讨论的程序中，我们生成了第一个可能的路径。 现在，让我们生成从开始节点到结束节点的所有可能路径。 基本功能与上述代码的功能相同。 产生差异的地方不是立即返回第一条路径，而是将该路径保存在以下示例中名为“路径”的列表中。 最后，在遍历所有可能的方式之后，它返回路径列表。 如果没有从起点到终点的路径，则返回 None。

## Python

```py

# Python program to generate the all possible
# path of the graph from the nodes provided
graph ={
'a':['c'],
'b':['d'],
'c':['e'],
'd':['a', 'd'],
'e':['b', 'c']
}

# function to generate all possible paths
def find_all_paths(graph, start, end, path =[]):
  path = path + [start]
  if start == end:
    return [path]
  paths = []
  for node in graph[start]:
    if node not in path:
      newpaths = find_all_paths(graph, node, end, path)
    for newpath in newpaths:
      paths.append(newpath)
  return paths

# Driver function call to print all 
# generated paths
print(find_all_paths(graph, 'd', 'c'))

```

1.  输出：

```
[['d', 'a', 'c'], ['d', 'a', 'c']]

```

2.  **程序生成最短路径。** ：
    为使所有路径都最短，我们使用了一些不同的方法，如下所示。 在这种情况下，当我们获得从起始节点到结束节点的路径时，我们将路径的长度与一个名为 shortest 的变量进行比较，该变量使用 None 值初始化。 如果生成的路径的长度小于最短的长度，则如果最短的值不为 None，则将新生成的路径设置为最短的值。 同样，如果没有路径，则返回 None

## Python

```py

# Python program to generate shortest path

graph ={
'a':['c'],
'b':['d'],
'c':['e'],
'd':['a', 'd'],
'e':['b', 'c']
}

# function to find the shortest path
def find_shortest_path(graph, start, end, path =[]):
        path = path + [start]
        if start == end:
            return path
        shortest = None
        for node in graph[start]:
            if node not in path:
                newpath = find_shortest_path(graph, node, end, path)
                if newpath:
                    if not shortest or len(newpath) < len(shortest):
                        shortest = newpath
        return shortest

# Driver function call to print
# the shortest path
print(find_shortest_path(graph, 'd', 'c'))

```

1.  输出：

```
['d', 'a', 'c']

```

本文由 [**Shivam Pradhan（anuj_charm）**](https://www.facebook.com/anuj.charm) 和 [**Rishabh Bansal**](https://www.linkedin.com/in/rishabh-bansal-9b4b71108/) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。
如果发现任何不正确的内容，或者想共享有关上述主题的更多信息，请发表评论。

注意怪胎！ 通过 [**Python 编程基础**](https://practice.geeksforgeeks.org/courses/Python-Foundation?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=GFG_Article_Bottom_Python_Foundation) 课程加强基础，并学习基础知识。

首先，您的面试准备将通过 [**Python DS**](https://practice.geeksforgeeks.org/courses/Data-Structures-With-Python?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=GFG_Article_Bottom_Python_DS) 课程来增强您的数据结构概念。