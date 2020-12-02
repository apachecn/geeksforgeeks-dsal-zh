# 克隆有向无环图

> 原文： [https://www.geeksforgeeks.org/clone-directed-acyclic-graph/](https://www.geeksforgeeks.org/clone-directed-acyclic-graph/)

有向无环图（DAG）是不包含循环且有向边的图。 我们获得了一个 DAG，我们需要对其进行克隆，即创建另一个具有其顶点副本和连接它们的边的图形。

例子：

```
Input :

0 - - - > 1 - - - -> 4
|        /  \        ^   
|       /    \       |  
|      /      \      |
|     /        \     |  
|    /          \    |
|   /            \   |
v  v              v  |
2 - - - - - - - - -> 3

Output : Printing the output of the cloned graph gives: 
0-1
1-2
2-3
3-4
1-3
1-4
0-2

```

克隆 DAG 而不将图形本身存储在哈希（或 Python 中的字典）中。 要进行克隆，我们基本上对节点进行深度优先遍历，以原始节点的值作为参数，并递归地初始化具有相同值的新相邻节点，直到完全遍历原始图为止。 下面是克隆 DAG 的递归方法（在 Python 中）。 我们使用 Python 中的动态列表，对列表的追加操作会在固定时间内进行，因此可以快速高效地初始化图形。

```

# Python program to clon a directed acyclic graph. 

# Class to create a new graph node 
class Node(): 

    # key is the value of the node 
    # adj will be holding a dynamic 
    # list of all Node type neighboring 
    # nodes 
    def __init__(self, key = None, adj = None): 
        self.key = key 
        self.adj = adj 

# Function to print a graph, depth-wise, recursively 
def printGraph(startNode, visited): 

    # Visit only those nodes who have any 
    # neighboring nodes to be traversed 
    if startNode.adj is not None: 

        # Loop through the neighboring nodes 
        # of this node. If source node not already 
        # visited, print edge from source to 
        # neighboring nodes. After visiting all 
        # neighbors of source node, mark its visited 
        # flag to true 
        for i in startNode.adj: 
            if visited[startNode.key] == False : 
                print("edge %s-%s:%s-%s"%(hex(id(startNode)), hex(id(i)), startNode.key, i.key)) 
                if visited[i.key] == False: 
                    printGraph(i, visited) 
                    visited[i.key] = True

# Function to clone a graph. To do this, we start 
# reading the original graph depth-wise, recursively 
# If we encounter an unvisited node in original graph, 
# we initialize a new instance of Node for 
# cloned graph with key of original node 
def cloneGraph(oldSource, newSource, visited): 
    clone = None
    if visited[oldSource.key] is False and oldSource.adj is not None: 
        for old in oldSource.adj: 

            # Below check is for backtracking, so new 
            # nodes don't get initialized everytime 
            if clone is None or(clone is not None and clone.key != old.key): 
                clone = Node(old.key, []) 
            newSource.adj.append(clone) 
            cloneGraph(old, clone, visited) 

            # Once, all neighbors for that particular node 
            # are created in cloned graph, code backtracks 
            # and exits from that node, mark the node as 
            # visited in original graph, and traverse the 
            # next unvisited 
            visited[old.key] = True
    return newSource 

# Creating DAG to be cloned 
# In Python, we can do as many assignments of 
# variables in one single line by using commas 
n0, n1, n2 = Node(0, []), Node(1, []), Node(2, []) 
n3, n4 = Node(3, []), Node(4) 
n0.adj.append(n1) 
n0.adj.append(n2) 
n1.adj.append(n2) 
n1.adj.append(n3) 
n1.adj.append(n4) 
n2.adj.append(n3) 
n3.adj.append(n4) 

# flag to check if a node is already visited. 
# Stops indefinite looping during recursion 
visited = [False]* (5) 
print("Graph Before Cloning:-") 
printGraph(n0, visited) 

visited = [False]* (5) 
print("\nCloning Process Starts") 
clonedGraphHead = cloneGraph(n0, Node(n0.key, []), visited) 
print("Cloning Process Completes.") 

visited = [False]*(5) 
print("\nGraph After Cloning:-") 
printGraph(clonedGraphHead, visited) 

```

输出：

```
Graph Before Cloning:-
edge 0x7fa03dd43878-0x7fa03dd43908:0-1
edge 0x7fa03dd43908-0x7fa03dd43950:1-2
edge 0x7fa03dd43950-0x7fa03dd43998:2-3
edge 0x7fa03dd43998-0x7fa03dd439e0:3-4
edge 0x7fa03dd43908-0x7fa03dd43998:1-3
edge 0x7fa03dd43908-0x7fa03dd439e0:1-4
edge 0x7fa03dd43878-0x7fa03dd43950:0-2

Cloning Process Starts
Cloning Process Completes.

Graph After Cloning:-
edge 0x7fa03dd43a28-0x7fa03dd43a70:0-1
edge 0x7fa03dd43a70-0x7fa03dd43ab8:1-2
edge 0x7fa03dd43ab8-0x7fa03dd43b00:2-3
edge 0x7fa03dd43b00-0x7fa03dd43b48:3-4
edge 0x7fa03dd43a70-0x7fa03dd43b90:1-3
edge 0x7fa03dd43a70-0x7fa03dd43bd8:1-4
edge 0x7fa03dd43a28-0x7fa03dd43c20:0-2

```

通过将相邻边附加到顶点来创建 DAG 的时间为 O（1）。 图的克隆需要 O（E + V）时间。

本文由 **Raveena** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

## 推荐文章：

*   [克隆无向图](https://www.geeksforgeeks.org/clone-an-undirected-graph/)

