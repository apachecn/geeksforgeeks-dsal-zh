# 无向图中的最大独立集

> 原文： [https://www.geeksforgeeks.org/maximal-independent-set-in-an-undirected-graph/](https://www.geeksforgeeks.org/maximal-independent-set-in-an-undirected-graph/)

给定一个由顶点 **V** 和边 **E []** 定义的无向图，任务是在无向图中找到**最大独立顶点集**。

> **独立集：**图形中的独立集是一组顶点，它们之间不直接相互连接。

**注意：**假设至少有一种方法可以从图中的任何顶点遍历到另一个顶点，即图中具有一个[连接的组件](https://www.geeksforgeeks.org/connected-components-in-an-undirected-graph/)。

**示例：**

> **输入：** V = 3，E = {（1，2），（2，3）}
> **输出：** {1，3}
> **解释 ：**
> 由于 1 和 3 之间没有边，并且由于它是 1 的邻居，因此我们不能对其添加 2，因此这是最大独立集。
> 
> **输入：** V = 8，
> E = {（1、2），（1、3），（2、4），（5、6），（6、7），（4 ，8）}
> **输出：** {2，3，5，7，8}

**方法：**
此问题是 [NP-硬问题](https://www.geeksforgeeks.org/np-completeness-set-1/)，只能在指数时间内解决（截至目前）。
请按照以下步骤解决问题：

*   遍历图形的顶点，并使用回溯检查顶点是否可以包含在**最大独立集**中。
*   每个顶点都有两种可能性，无论是否可以将其包含在最大独立集中。
*   首先，考虑所有顶点和边。 一一选择一个顶点。 从图形中删除该顶点，将其从最大独立集中排除，然后递归地遍历其余图形以找到最大独立集。
*   否则，请考虑最大独立集中的选定顶点，并从中删除所有与其相邻的顶点。 继续查找可能的最大独立集（不包括其邻居）。
*   对所有顶点重复此过程，并打印获得的最大独立集。

下面是上述方法的实现：

## Python3

```

# Python Program to implement 
# the above approach 

# Recursive Function to find the 
# Maximal Independent Vertex Set     
def graphSets(graph): 

    # Base Case - Given Graph  
    # has no nodes 
    if(len(graph) == 0): 
        return [] 

    # Base Case - Given Graph 
    # has 1 node 
    if(len(graph) == 1): 
        return [list(graph.keys())[0]] 

    # Select a vertex from the graph 
    vCurrent = list(graph.keys())[0] 

    # Case 1 - Proceed removing 
    # the selected vertex 
    # from the Maximal Set 
    graph2 = dict(graph) 

    # Delete current vertex  
    # from the Graph 
    del graph2[vCurrent] 

    # Recursive call - Gets  
    # Maximal Set, 
    # assuming current Vertex  
    # not selected 
    res1 = graphSets(graph2) 

    # Case 2 - Proceed considering 
    # the selected vertex as part 
    # of the Maximal Set 

    # Loop through its neighbours 
    for v in graph[vCurrent]: 

        # Delete neighbor from  
        # the current subgraph 
        if(v in graph2): 
            del graph2[v] 

    # This result set contains VFirst, 
    # and the result of recursive 
    # call assuming neighbors of vFirst 
    # are not selected 
    res2 = [vCurrent] + graphSets(graph2) 

    # Our final result is the one  
    # which is bigger, return it 
    if(len(res1) > len(res2)): 
        return res1 
    return res2 

# Driver Code 
V = 8

# Defines edges 
E = [ (1, 2), 
      (1, 3), 
      (2, 4), 
      (5, 6), 
      (6, 7), 
      (4, 8)] 

graph = dict([]) 

# Constructs Graph as a dictionary  
# of the following format- 

# graph[VertexNumber V]  
# = list[Neighbors of Vertex V] 
for i in range(len(E)): 
    v1, v2 = E[i] 

    if(v1 not in graph): 
        graph[v1] = [] 
    if(v2 not in graph): 
        graph[v2] = [] 

    graph[v1].append(v2) 
    graph[v2].append(v1) 

# Recursive call considering  
# all vertices in the maximum  
# independent set 
maximalIndependentSet = graphSets(graph) 

# Prints the Result  
for i in maximalIndependentSet: 
    print(i, end =" ") 

```

**Output:**

```
2 3 8 5 7

```

***时间复杂度：** O（2 <sup>N</sup> ）
**辅助空间：** O（N）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。