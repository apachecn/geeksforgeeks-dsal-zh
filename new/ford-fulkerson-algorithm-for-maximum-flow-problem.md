# 用于最大流量问题的 Ford-Fulkerson 算法

> 原文： [https://www.geeksforgeeks.org/ford-fulkerson-algorithm-for-maximum-flow-problem/](https://www.geeksforgeeks.org/ford-fulkerson-algorithm-for-maximum-flow-problem/)

给定一个表示流网络的图形，其中每个边都有容量。 还给定图中的两个顶点*源*'s'和*接收器*'t'，请找到具有以下约束的从 s 到 t 的最大可能流量：

**a）**边缘上的流量不超过边缘的给定容量。

**b）**除 s 和 t 之外，每个顶点的流入流量等于流出流量。

例如，请考虑以下 CLRS 书中的图表。
[![ford_fulkerson1](img/568b1131326471bed1ddb97bf1399c90.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/ford_fulkerson11.png) 
上图中的最大可能流量为 23。
[![ford_fulkerson2](img/0cc230058968c39cad925949a53ee714.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/ford_fulkerson2.png)

先决条件： **[最大流量问题简介](https://www.geeksforgeeks.org/max-flow-problem-introduction/)**

```
Ford-Fulkerson Algorithm 
The following is simple idea of Ford-Fulkerson algorithm:
1) Start with initial flow as 0.
2) While there is a augmenting path from source to sink. 
           Add this path-flow to flow.
3) Return flow.
```

**时间复杂度**：上述算法的时间复杂度为 O（max_flow * E）。 我们在存在扩展路径的情况下运行循环。 在最坏的情况下，每次迭代可能会增加 1 个单位流。 因此，时间复杂度变为 O（max_flow * E）。

**如何实现以上简单算法？**
让我们首先定义残差图的概念，这是理解实现所必需的。 流量网络的
***残留图*** 是表示其他可能流量的图。 如果残差图中存在从源到汇的路径，则可以增加流量。 残差图的每个边都有一个称为 ***剩余容量*** 的值，该值等于边的原始容量减去电流。 剩余容量基本上是边缘的当前容量。
现在让我们讨论实现细节。 如果残差图的两个顶点之间没有边，则残差能力为 0。 我们可以将残差图初始化为原始图，因为没有初始流量，并且初始残差容量等于原始容量。 要找到增广路径，我们可以对残差图进行 BFS 或 DFS。 我们在以下实现中使用了 BFS。 使用 BFS，我们可以找出从源到接收器的路径。 BFS 还建立了 parent []数组。 使用 parent []数组，我们遍历找到的路径，并通过找到路径上的最小剩余容量来查找通过该路径的可能流。 稍后，我们将找到的路径流添加到总体流中。
重要的是，我们需要更新残差图中的残差容量。 我们从沿路径的所有边缘减去路径流，然后沿反向边缘添加路径流。我们需要沿反向边缘添加路径流，因为以后可能需要反向发送流（例如，请参见以下链接）。

[https://www.geeksforgeeks.org/max-flow-problem-introduction/](https://www.geeksforgeeks.org/max-flow-problem-introduction/)

以下是 Ford-Fulkerson 算法的实现。 为了简单起见，图形表示为 2D 矩阵。

## C ++

```

// C++ program for implementation of Ford Fulkerson algorithm 
#include <iostream> 
#include <limits.h> 
#include <string.h> 
#include <queue> 
using namespace std; 

// Number of vertices in given graph 
#define V 6 

/* Returns true if there is a path from source 's' to sink 't' in 
  residual graph. Also fills parent[] to store the path */
bool bfs(int rGraph[V][V], int s, int t, int parent[]) 
{ 
    // Create a visited array and mark all vertices as not visited 
    bool visited[V]; 
    memset(visited, 0, sizeof(visited)); 

    // Create a queue, enqueue source vertex and mark source vertex 
    // as visited 
    queue <int> q; 
    q.push(s); 
    visited[s] = true; 
    parent[s] = -1; 

    // Standard BFS Loop 
    while (!q.empty()) 
    { 
        int u = q.front(); 
        q.pop(); 

        for (int v=0; v<V; v++) 
        { 
            if (visited[v]==false && rGraph[u][v] > 0) 
            { 
                q.push(v); 
                parent[v] = u; 
                visited[v] = true; 
            } 
        } 
    } 

    // If we reached sink in BFS starting from source, then return 
    // true, else false 
    return (visited[t] == true); 
} 

// Returns the maximum flow from s to t in the given graph 
int fordFulkerson(int graph[V][V], int s, int t) 
{ 
    int u, v; 

    // Create a residual graph and fill the residual graph with 
    // given capacities in the original graph as residual capacities 
    // in residual graph 
    int rGraph[V][V]; // Residual graph where rGraph[i][j] indicates  
                     // residual capacity of edge from i to j (if there 
                     // is an edge. If rGraph[i][j] is 0, then there is not)   
    for (u = 0; u < V; u++) 
        for (v = 0; v < V; v++) 
             rGraph[u][v] = graph[u][v]; 

    int parent[V];  // This array is filled by BFS and to store path 

    int max_flow = 0;  // There is no flow initially 

    // Augment the flow while tere is path from source to sink 
    while (bfs(rGraph, s, t, parent)) 
    { 
        // Find minimum residual capacity of the edges along the 
        // path filled by BFS. Or we can say find the maximum flow 
        // through the path found. 
        int path_flow = INT_MAX; 
        for (v=t; v!=s; v=parent[v]) 
        { 
            u = parent[v]; 
            path_flow = min(path_flow, rGraph[u][v]); 
        } 

        // update residual capacities of the edges and reverse edges 
        // along the path 
        for (v=t; v != s; v=parent[v]) 
        { 
            u = parent[v]; 
            rGraph[u][v] -= path_flow; 
            rGraph[v][u] += path_flow; 
        } 

        // Add path flow to overall flow 
        max_flow += path_flow; 
    } 

    // Return the overall flow 
    return max_flow; 
} 

// Driver program to test above functions 
int main() 
{ 
    // Let us create a graph shown in the above example 
    int graph[V][V] = { {0, 16, 13, 0, 0, 0}, 
                        {0, 0, 10, 12, 0, 0}, 
                        {0, 4, 0, 0, 14, 0}, 
                        {0, 0, 9, 0, 0, 20}, 
                        {0, 0, 0, 7, 0, 4}, 
                        {0, 0, 0, 0, 0, 0} 
                      }; 

    cout << "The maximum possible flow is " << fordFulkerson(graph, 0, 5); 

    return 0; 
} 

```

## 爪哇

```

// Java program for implementation of Ford Fulkerson algorithm 
import java.util.*; 
import java.lang.*; 
import java.io.*; 
import java.util.LinkedList; 

class MaxFlow 
{ 
    static final int V = 6;    //Number of vertices in graph 

    /* Returns true if there is a path from source 's' to sink 
      't' in residual graph. Also fills parent[] to store the 
      path */
    boolean bfs(int rGraph[][], int s, int t, int parent[]) 
    { 
        // Create a visited array and mark all vertices as not 
        // visited 
        boolean visited[] = new boolean[V]; 
        for(int i=0; i<V; ++i) 
            visited[i]=false; 

        // Create a queue, enqueue source vertex and mark 
        // source vertex as visited 
        LinkedList<Integer> queue = new LinkedList<Integer>(); 
        queue.add(s); 
        visited[s] = true; 
        parent[s]=-1; 

        // Standard BFS Loop 
        while (queue.size()!=0) 
        { 
            int u = queue.poll(); 

            for (int v=0; v<V; v++) 
            { 
                if (visited[v]==false && rGraph[u][v] > 0) 
                { 
                    queue.add(v); 
                    parent[v] = u; 
                    visited[v] = true; 
                } 
            } 
        } 

        // If we reached sink in BFS starting from source, then 
        // return true, else false 
        return (visited[t] == true); 
    } 

    // Returns tne maximum flow from s to t in the given graph 
    int fordFulkerson(int graph[][], int s, int t) 
    { 
        int u, v; 

        // Create a residual graph and fill the residual graph 
        // with given capacities in the original graph as 
        // residual capacities in residual graph 

        // Residual graph where rGraph[i][j] indicates 
        // residual capacity of edge from i to j (if there 
        // is an edge. If rGraph[i][j] is 0, then there is 
        // not) 
        int rGraph[][] = new int[V][V]; 

        for (u = 0; u < V; u++) 
            for (v = 0; v < V; v++) 
                rGraph[u][v] = graph[u][v]; 

        // This array is filled by BFS and to store path 
        int parent[] = new int[V]; 

        int max_flow = 0;  // There is no flow initially 

        // Augment the flow while tere is path from source 
        // to sink 
        while (bfs(rGraph, s, t, parent)) 
        { 
            // Find minimum residual capacity of the edhes 
            // along the path filled by BFS. Or we can say 
            // find the maximum flow through the path found. 
            int path_flow = Integer.MAX_VALUE; 
            for (v=t; v!=s; v=parent[v]) 
            { 
                u = parent[v]; 
                path_flow = Math.min(path_flow, rGraph[u][v]); 
            } 

            // update residual capacities of the edges and 
            // reverse edges along the path 
            for (v=t; v != s; v=parent[v]) 
            { 
                u = parent[v]; 
                rGraph[u][v] -= path_flow; 
                rGraph[v][u] += path_flow; 
            } 

            // Add path flow to overall flow 
            max_flow += path_flow; 
        } 

        // Return the overall flow 
        return max_flow; 
    } 

    // Driver program to test above functions 
    public static void main (String[] args) throws java.lang.Exception 
    { 
        // Let us create a graph shown in the above example 
        int graph[][] =new int[][] { {0, 16, 13, 0, 0, 0}, 
                                     {0, 0, 10, 12, 0, 0}, 
                                     {0, 4, 0, 0, 14, 0}, 
                                     {0, 0, 9, 0, 0, 20}, 
                                     {0, 0, 0, 7, 0, 4}, 
                                     {0, 0, 0, 0, 0, 0} 
                                   }; 
        MaxFlow m = new MaxFlow(); 

        System.out.println("The maximum possible flow is " + 
                           m.fordFulkerson(graph, 0, 5)); 

    } 
} 

```

## 蟒蛇

```

# Python program for implementation of Ford Fulkerson algorithm 

from collections import defaultdict 

#This class represents a directed graph using adjacency matrix representation 
class Graph: 

    def __init__(self,graph): 
        self.graph = graph # residual graph 
        self. ROW = len(graph) 
        #self.COL = len(gr[0]) 

    '''Returns true if there is a path from source 's' to sink 't' in 
    residual graph. Also fills parent[] to store the path '''
    def BFS(self,s, t, parent): 

        # Mark all the vertices as not visited 
        visited =[False]*(self.ROW) 

        # Create a queue for BFS 
        queue=[] 

        # Mark the source node as visited and enqueue it 
        queue.append(s) 
        visited[s] = True

         # Standard BFS Loop 
        while queue: 

            #Dequeue a vertex from queue and print it 
            u = queue.pop(0) 

            # Get all adjacent vertices of the dequeued vertex u 
            # If a adjacent has not been visited, then mark it 
            # visited and enqueue it 
            for ind, val in enumerate(self.graph[u]): 
                if visited[ind] == False and val > 0 : 
                    queue.append(ind) 
                    visited[ind] = True
                    parent[ind] = u 

        # If we reached sink in BFS starting from source, then return 
        # true, else false 
        return True if visited[t] else False

    # Returns tne maximum flow from s to t in the given graph 
    def FordFulkerson(self, source, sink): 

        # This array is filled by BFS and to store path 
        parent = [-1]*(self.ROW) 

        max_flow = 0 # There is no flow initially 

        # Augment the flow while there is path from source to sink 
        while self.BFS(source, sink, parent) : 

            # Find minimum residual capacity of the edges along the 
            # path filled by BFS. Or we can say find the maximum flow 
            # through the path found. 
            path_flow = float("Inf") 
            s = sink 
            while(s !=  source): 
                path_flow = min (path_flow, self.graph[parent[s]][s]) 
                s = parent[s] 

            # Add path flow to overall flow 
            max_flow +=  path_flow 

            # update residual capacities of the edges and reverse edges 
            # along the path 
            v = sink 
            while(v !=  source): 
                u = parent[v] 
                self.graph[u][v] -= path_flow 
                self.graph[v][u] += path_flow 
                v = parent[v] 

        return max_flow 

# Create a graph given in the above diagram 

graph = [[0, 16, 13, 0, 0, 0], 
        [0, 0, 10, 12, 0, 0], 
        [0, 4, 0, 0, 14, 0], 
        [0, 0, 9, 0, 0, 20], 
        [0, 0, 0, 7, 0, 4], 
        [0, 0, 0, 0, 0, 0]] 

g = Graph(graph) 

source = 0; sink = 5

print ("The maximum possible flow is %d " % g.FordFulkerson(source, sink)) 

#This code is contributed by Neelam Yadav 

```

## C＃

```

// C# program for implementation  
// of Ford Fulkerson algorithm 
using System; 
using System.Collections.Generic; 

public class MaxFlow 
{ 
    static readonly int V = 6; //Number of vertices in graph 

    /* Returns true if there is a path 
    from source 's' to sink 't' in residual 
    graph. Also fills parent[] to store the 
    path */
    bool bfs(int [,]rGraph, int s, int t, int []parent) 
    { 
        // Create a visited array and mark  
        // all vertices as not visited 
        bool []visited = new bool[V]; 
        for(int i = 0; i < V; ++i) 
            visited[i] = false; 

        // Create a queue, enqueue source vertex and mark 
        // source vertex as visited 
        List<int> queue = new List<int>(); 
        queue.Add(s); 
        visited[s] = true; 
        parent[s] = -1; 

        // Standard BFS Loop 
        while (queue.Count != 0) 
        { 
            int u = queue[0]; 
                queue.RemoveAt(0); 

            for (int v = 0; v < V; v++) 
            { 
                if (visited[v] == false && rGraph[u, v] > 0) 
                { 
                    queue.Add(v); 
                    parent[v] = u; 
                    visited[v] = true; 
                } 
            } 
        } 

        // If we reached sink in BFS  
        // starting from source, then 
        // return true, else false 
        return (visited[t] == true); 
    } 

    // Returns tne maximum flow 
    // from s to t in the given graph 
    int fordFulkerson(int [,]graph, int s, int t) 
    { 
        int u, v; 

        // Create a residual graph and fill  
        // the residual graph with given  
        // capacities in the original graph as 
        // residual capacities in residual graph 

        // Residual graph where rGraph[i,j]  
        // indicates residual capacity of  
        // edge from i to j (if there is an  
        // edge. If rGraph[i,j] is 0, then  
        // there is not) 
        int [,]rGraph = new int[V, V]; 

        for (u = 0; u < V; u++) 
            for (v = 0; v < V; v++) 
                rGraph[u, v] = graph[u, v]; 

        // This array is filled by BFS and to store path 
        int []parent = new int[V]; 

        int max_flow = 0; // There is no flow initially 

        // Augment the flow while tere is path from source 
        // to sink 
        while (bfs(rGraph, s, t, parent)) 
        { 
            // Find minimum residual capacity of the edhes 
            // along the path filled by BFS. Or we can say 
            // find the maximum flow through the path found. 
            int path_flow = int.MaxValue; 
            for (v = t; v != s; v = parent[v]) 
            { 
                u = parent[v]; 
                path_flow = Math.Min(path_flow, rGraph[u,v]); 
            } 

            // update residual capacities of the edges and 
            // reverse edges along the path 
            for (v = t; v != s; v = parent[v]) 
            { 
                u = parent[v]; 
                rGraph[u,v] -= path_flow; 
                rGraph[v,u] += path_flow; 
            } 

            // Add path flow to overall flow 
            max_flow += path_flow; 
        } 

        // Return the overall flow 
        return max_flow; 
    } 

    // Driver code 
    public static void Main () 
    { 
        // Let us create a graph shown in the above example 
        int [,]graph =new int[,] { {0, 16, 13, 0, 0, 0}, 
                                    {0, 0, 10, 12, 0, 0}, 
                                    {0, 4, 0, 0, 14, 0}, 
                                    {0, 0, 9, 0, 0, 20}, 
                                    {0, 0, 0, 7, 0, 4}, 
                                    {0, 0, 0, 0, 0, 0} 
                                }; 
        MaxFlow m = new MaxFlow(); 

        Console.WriteLine("The maximum possible flow is " + 
                        m.fordFulkerson(graph, 0, 5)); 

    } 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
The maximum possible flow is 23
```

福特·富尔克森算法的上述实现称为 **[Edmonds-Karp 算法](http://en.wikipedia.org/wiki/Edmonds%E2%80%93Karp_algorithm)** 。 Edmonds-Karp 的想法是在 Ford Fulkerson 实现中使用 BFS，因为 BFS 总是选择一条边数最少的路径。 使用 BFS 时，最坏情况下的时间复杂度可以降低为 O（VE <sup>2</sup> ）。 尽管在 BFS 花费 O（V <sup>2</sup> ）时间的情况下，上述实现仍使用邻接矩阵表示，但上述实现的时间复杂度为 O（EV <sup>3</sup> ）（请参阅 [CLRS 书](http://www.flipkart.com/introduction-algorithms-3rd/p/itmczynzhyhxv2gs?pid=9788120340077&affid=sandeepgfg) （用于证明时间复杂度）

这是一个重要的问题，因为它在许多实际情况下都会出现。 例如，在给定的流量限制下最大化传输，在计算机网络中最大化数据包流。

[Dinc 的最大流量算法。](https://www.geeksforgeeks.org/dinics-algorithm-maximum-flow/)

**练习**：
修改以上实现，使其在 O（VE <sup>2</sup> ）时间内运行。

**参考**：
[http://www.stanford.edu/class/cs97si/08-network-flow-problems.pdf](http://www.stanford.edu/class/cs97si/08-network-flow-problems.pdf)
[算法导论 3 Clifford Stein，Thomas H. Cormen，Charles E. Leiserson 和 Ronald L. Rivest 撰写的版本](http://www.flipkart.com/introduction-algorithms-3rd/p/itmczynzhyhxv2gs?pid=9788120340077&affid=sandeepgfg)

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

