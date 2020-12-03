# 从 indeg 为 0 的顶点打印 DAG 中所有可能的路径

> 原文： [https://www.geeksforgeeks.org/print-all-possible-paths-in-a-dag-from-vertex-whose-indegree-is-0/](https://www.geeksforgeeks.org/print-all-possible-paths-in-a-dag-from-vertex-whose-indegree-is-0/)

给定一个有向无环图（DAG），它具有 **N 个**顶点和 **M 个**边，任务是打印从入度为零的顶点开始的所有路径。

> 顶点的度数是顶点进入边的总数。

**示例**：

> **输入**：N = 6，edges [] = {{5，0}，{5，2}，{4，0}，{4，1}，{2，3}，{3， 1}}
> **输出**：所有可能的路径：
> 4 0
> 4 1
> 5 0
> 5 2 3 1
> **说明**：
> 给定的图形可以表示为：
> ![](img/7d0dd3600bc879e60d2864710a2aab68.png) 
> 有两个顶点的度数分别为零，即顶点 5 和 4，在探索了这些顶点之后，我们得到了下降路径 ：
> 4-> 0
> 4-> 1
> 5-> 0
> 5-> 2-> 3-> 1
> **输入**：N = 6，边[] = {{0，5}}
> **输出**：所有可能的路径：
> 0 5
> **说明 **：
> 图中只有一条可能的路径。

**方法**：

`0`

`0`

4.  创建一个布尔数组 **indeg0** ，该数组为 indeg 为零的所有那些顶点存储一个真值。
5.  在所有 indeg 为 0 的顶点上应用 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 。
6.  打印从入度为 0 的顶点到出度为零的顶点开始的所有路径。

> **插图**：
> 对于上图：
> indeg0 [] = {False，False，False，False，True，True}
> 由于 indeg [4] = True，因此请应用 DFS 在顶点 4 上并打印所有终止于 0 度顶点的路径，如下所示：
> **4-> 0
> 4-> 1**
> 同样 indeg [5] = True ，因此将 DFS 应用于顶点 5 并打印终止于 0 度顶点的所有路径如下：
> **5-> 0
> 5-> 2-> 3-> 1**

这是上述方法的实现：

## Python

```py

# Python program to print all 
# possible paths in a DAG 

# Recursive function to print all paths 
def dfs(s): 
    # Append the node in path 
    # and set visited 
    path.append(s) 
    visited[s] = True

    # Path started with a node 
    # having in-degree 0 and 
    # current node has out-degree 0, 
    # print current path 
    if outdeg0[s] and indeg0[path[0]]: 
        print(*path) 

    # Recursive call to print all paths 
    for node in adj[s]: 
        if not visited[node]: 
            dfs(node) 

    # Remove node from path 
    # and set unvisited 
    path.pop() 
    visited[s] = False

def print_all_paths(n): 
    for i in range(n): 

        # for each node with in-degree 0 
        # print all possible paths 
        if indeg0[i] and adj[i]: 
            path = [] 
            visited = [False] * (n + 1) 
            dfs(i) 

# Driver code 
from collections import defaultdict 

n = 6
# set all nodes unvisited 
visited = [False] * (n + 1) 
path = [] 

# edges = (a, b): a -> b 
edges = [(5, 0), (5, 2), (2, 3), 
         (4, 0), (4, 1), (3, 1)] 

# adjacency list for nodes 
adj = defaultdict(list) 

# indeg0 and outdeg0 arrays 
indeg0 = [True]*n 
outdeg0 = [True]*n 

for edge in edges: 
    u, v = edge[0], edge[1] 
    # u -> v 
    adj[u].append(v) 

    # set indeg0[v] <- false 
    indeg0[v] = False

    # set outdeg0[u] <- false 
    outdeg0[u] = False

print('All possible paths:') 
print_all_paths(n) 

```

**Output:**

```
All possible paths:
4 0
4 1
5 0
5 2 3 1

```

***时间复杂度**：O（N + E） <sup>2</sup>*
***辅助空间**：O（N）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。