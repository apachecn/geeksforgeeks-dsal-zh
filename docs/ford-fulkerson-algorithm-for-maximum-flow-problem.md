# 求解最大流问题的福特-富尔克森算法

> 原文:[https://www . geeksforgeeks . org/Ford-fulkerson-最大流量算法-问题/](https://www.geeksforgeeks.org/ford-fulkerson-algorithm-for-maximum-flow-problem/)

给定一个表示每个边都有容量的流网络的图。同样给定图中的两个顶点*源*s’和*汇*“t ”,找到从 s 到 t 的最大可能流量，约束如下:
**a)** 边上的流量不超过边的给定容量。
**b)** 除了 s 和 t，每个顶点的来流都等于出流。

例如，考虑以下来自 CLRS 书籍的图表。

![ford_fulkerson1](img/568b1131326471bed1ddb97bf1399c90.png)

上图中最大可能流量为 23。

![ford_fulkerson2](img/0cc230058968c39cad925949a53ee714.png)

先决条件: [**最大流量问题介绍**](https://www.geeksforgeeks.org/max-flow-problem-introduction/)

```
Ford-Fulkerson Algorithm 
The following is simple idea of Ford-Fulkerson algorithm:
1) Start with initial flow as 0.
2) While there is a augmenting path from source to sink. 
           Add this path-flow to flow.
3) Return flow.
```

**时间复杂度:**上述算法的时间复杂度为 O(max_flow * E)。当有一个增加的路径时，我们运行一个循环。在最坏的情况下，我们可能在每次迭代中增加 1 个单元流。因此时间复杂度变成了 O(max_flow * E)。

**如何实现上述简单算法？**
让我们首先定义理解实现所需的残差图的概念。

流网络的 ***【剩余图】*** 是表示额外可能流的图。如果残差图中有一条从源到宿的路径，那么就有可能增加流量。剩余图的每条边都有一个值叫做 ***【剩余容量】*** ，它等于边的原始容量减去电流。剩余容量基本上是边缘的当前容量。
现在来说说实现细节。如果剩余图的两个顶点之间没有边，剩余容量为 0。我们可以将剩余图初始化为原始图，因为没有初始流量，初始剩余容量等于原始容量。为了找到一条增广路径，我们可以对剩余图进行 BFS 或离散傅立叶变换。我们在下面的实现中使用了 BFS。利用 BFS，我们可以发现是否有从源头到下沉的路径。BFS 还构建了父[]数组。使用父[]数组，我们遍历找到的路径，并通过找到路径上的最小剩余容量来找到通过该路径的可能流量。我们稍后将发现的路径流添加到总流中。

重要的是，我们需要更新剩余图中的剩余容量。我们从沿着路径的所有边中减去路径流，然后沿着反向边添加路径流我们需要沿着反向边添加路径流，因为以后可能需要反向发送流(例如，参见下面的链接)。
[https://www . geeksforgeeks . org/max-flow-problem-introduction/](https://www.geeksforgeeks.org/max-flow-problem-introduction/)

下面是福特-富尔克森算法的实现。为了简单起见，图被表示为 2D 矩阵。

## C++

```
// C++ program for implementation of Ford Fulkerson
// algorithm
#include <iostream>
#include <limits.h>
#include <queue>
#include <string.h>
using namespace std;

// Number of vertices in given graph
#define V 6

/* Returns true if there is a path from source 's' to sink
  't' in residual graph. Also fills parent[] to store the
  path */
bool bfs(int rGraph[V][V], int s, int t, int parent[])
{
    // Create a visited array and mark all vertices as not
    // visited
    bool visited[V];
    memset(visited, 0, sizeof(visited));

    // Create a queue, enqueue source vertex and mark source
    // vertex as visited
    queue<int> q;
    q.push(s);
    visited[s] = true;
    parent[s] = -1;

    // Standard BFS Loop
    while (!q.empty()) {
        int u = q.front();
        q.pop();

        for (int v = 0; v < V; v++) {
            if (visited[v] == false && rGraph[u][v] > 0) {
                // If we find a connection to the sink node,
                // then there is no point in BFS anymore We
                // just have to set its parent and can return
                // true
                if (v == t) {
                    parent[v] = u;
                    return true;
                }
                q.push(v);
                parent[v] = u;
                visited[v] = true;
            }
        }
    }

    // We didn't reach sink in BFS starting from source, so
    // return false
    return false;
}

// Returns the maximum flow from s to t in the given graph
int fordFulkerson(int graph[V][V], int s, int t)
{
    int u, v;

    // Create a residual graph and fill the residual graph
    // with given capacities in the original graph as
    // residual capacities in residual graph
    int rGraph[V]
              [V]; // Residual graph where rGraph[i][j]
                   // indicates residual capacity of edge
                   // from i to j (if there is an edge. If
                   // rGraph[i][j] is 0, then there is not)
    for (u = 0; u < V; u++)
        for (v = 0; v < V; v++)
            rGraph[u][v] = graph[u][v];

    int parent[V]; // This array is filled by BFS and to
                   // store path

    int max_flow = 0; // There is no flow initially

    // Augment the flow while there is path from source to
    // sink
    while (bfs(rGraph, s, t, parent)) {
        // Find minimum residual capacity of the edges along
        // the path filled by BFS. Or we can say find the
        // maximum flow through the path found.
        int path_flow = INT_MAX;
        for (v = t; v != s; v = parent[v]) {
            u = parent[v];
            path_flow = min(path_flow, rGraph[u][v]);
        }

        // update residual capacities of the edges and
        // reverse edges along the path
        for (v = t; v != s; v = parent[v]) {
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
    int graph[V][V]
        = { { 0, 16, 13, 0, 0, 0 }, { 0, 0, 10, 12, 0, 0 },
            { 0, 4, 0, 0, 14, 0 },  { 0, 0, 9, 0, 0, 20 },
            { 0, 0, 0, 7, 0, 4 },   { 0, 0, 0, 0, 0, 0 } };

    cout << "The maximum possible flow is "
         << fordFulkerson(graph, 0, 5);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for implementation of Ford Fulkerson
// algorithm
import java.io.*;
import java.lang.*;
import java.util.*;
import java.util.LinkedList;

class MaxFlow {
    static final int V = 6; // Number of vertices in graph

    /* Returns true if there is a path from source 's' to
      sink 't' in residual graph. Also fills parent[] to
      store the path */
    boolean bfs(int rGraph[][], int s, int t, int parent[])
    {
        // Create a visited array and mark all vertices as
        // not visited
        boolean visited[] = new boolean[V];
        for (int i = 0; i < V; ++i)
            visited[i] = false;

        // Create a queue, enqueue source vertex and mark
        // source vertex as visited
        LinkedList<Integer> queue
            = new LinkedList<Integer>();
        queue.add(s);
        visited[s] = true;
        parent[s] = -1;

        // Standard BFS Loop
        while (queue.size() != 0) {
            int u = queue.poll();

            for (int v = 0; v < V; v++) {
                if (visited[v] == false
                    && rGraph[u][v] > 0) {
                    // If we find a connection to the sink
                    // node, then there is no point in BFS
                    // anymore We just have to set its parent
                    // and can return true
                    if (v == t) {
                        parent[v] = u;
                        return true;
                    }
                    queue.add(v);
                    parent[v] = u;
                    visited[v] = true;
                }
            }
        }

        // We didn't reach sink in BFS starting from source,
        // so return false
        return false;
    }

    // Returns tne maximum flow from s to t in the given
    // graph
    int fordFulkerson(int graph[][], int s, int t)
    {
        int u, v;

        // Create a residual graph and fill the residual
        // graph with given capacities in the original graph
        // as residual capacities in residual graph

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

        int max_flow = 0; // There is no flow initially

        // Augment the flow while there is path from source
        // to sink
        while (bfs(rGraph, s, t, parent)) {
            // Find minimum residual capacity of the edhes
            // along the path filled by BFS. Or we can say
            // find the maximum flow through the path found.
            int path_flow = Integer.MAX_VALUE;
            for (v = t; v != s; v = parent[v]) {
                u = parent[v];
                path_flow
                    = Math.min(path_flow, rGraph[u][v]);
            }

            // update residual capacities of the edges and
            // reverse edges along the path
            for (v = t; v != s; v = parent[v]) {
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
    public static void main(String[] args)
        throws java.lang.Exception
    {
        // Let us create a graph shown in the above example
        int graph[][] = new int[][] {
            { 0, 16, 13, 0, 0, 0 }, { 0, 0, 10, 12, 0, 0 },
            { 0, 4, 0, 0, 14, 0 },  { 0, 0, 9, 0, 0, 20 },
            { 0, 0, 0, 7, 0, 4 },   { 0, 0, 0, 0, 0, 0 }
        };
        MaxFlow m = new MaxFlow();

        System.out.println("The maximum possible flow is "
                           + m.fordFulkerson(graph, 0, 5));
    }
}
```

## 计算机编程语言

```
# Python program for implementation
# of Ford Fulkerson algorithm
from collections import defaultdict

# This class represents a directed graph
# using adjacency matrix representation
class Graph:

    def __init__(self, graph):
        self.graph = graph  # residual graph
        self. ROW = len(graph)
        # self.COL = len(gr[0])

    '''Returns true if there is a path from source 's' to sink 't' in
    residual graph. Also fills parent[] to store the path '''

    def BFS(self, s, t, parent):

        # Mark all the vertices as not visited
        visited = [False]*(self.ROW)

        # Create a queue for BFS
        queue = []

        # Mark the source node as visited and enqueue it
        queue.append(s)
        visited[s] = True

         # Standard BFS Loop
        while queue:

            # Dequeue a vertex from queue and print it
            u = queue.pop(0)

            # Get all adjacent vertices of the dequeued vertex u
            # If a adjacent has not been visited, then mark it
            # visited and enqueue it
            for ind, val in enumerate(self.graph[u]):
                if visited[ind] == False and val > 0:
                      # If we find a connection to the sink node,
                    # then there is no point in BFS anymore
                    # We just have to set its parent and can return true
                    queue.append(ind)
                    visited[ind] = True
                    parent[ind] = u
                    if ind == t:
                        return True

        # We didn't reach sink in BFS starting
        # from source, so return false
        return False

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

# This code is contributed by Neelam Yadav
```

## C#

```
// C# program for implementation
// of Ford Fulkerson algorithm
using System;
using System.Collections.Generic;

public class MaxFlow {
    static readonly int V = 6; // Number of vertices in
                               // graph

    /* Returns true if there is a path
    from source 's' to sink 't' in residual
    graph. Also fills parent[] to store the
    path */
    bool bfs(int[, ] rGraph, int s, int t, int[] parent)
    {
        // Create a visited array and mark
        // all vertices as not visited
        bool[] visited = new bool[V];
        for (int i = 0; i < V; ++i)
            visited[i] = false;

        // Create a queue, enqueue source vertex and mark
        // source vertex as visited
        List<int> queue = new List<int>();
        queue.Add(s);
        visited[s] = true;
        parent[s] = -1;

        // Standard BFS Loop
        while (queue.Count != 0) {
            int u = queue[0];
            queue.RemoveAt(0);

            for (int v = 0; v < V; v++) {
                if (visited[v] == false
                    && rGraph[u, v] > 0) {
                    // If we find a connection to the sink
                    // node, then there is no point in BFS
                    // anymore We just have to set its parent
                    // and can return true
                    if (v == t) {
                        parent[v] = u;
                        return true;
                    }
                    queue.Add(v);
                    parent[v] = u;
                    visited[v] = true;
                }
            }
        }

        // We didn't reach sink in BFS starting from source,
        // so return false
        return false;
    }

    // Returns tne maximum flow
    // from s to t in the given graph
    int fordFulkerson(int[, ] graph, int s, int t)
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
        int[, ] rGraph = new int[V, V];

        for (u = 0; u < V; u++)
            for (v = 0; v < V; v++)
                rGraph[u, v] = graph[u, v];

        // This array is filled by BFS and to store path
        int[] parent = new int[V];

        int max_flow = 0; // There is no flow initially

        // Augment the flow while there is path from source
        // to sink
        while (bfs(rGraph, s, t, parent)) {
            // Find minimum residual capacity of the edhes
            // along the path filled by BFS. Or we can say
            // find the maximum flow through the path found.
            int path_flow = int.MaxValue;
            for (v = t; v != s; v = parent[v]) {
                u = parent[v];
                path_flow
                    = Math.Min(path_flow, rGraph[u, v]);
            }

            // update residual capacities of the edges and
            // reverse edges along the path
            for (v = t; v != s; v = parent[v]) {
                u = parent[v];
                rGraph[u, v] -= path_flow;
                rGraph[v, u] += path_flow;
            }

            // Add path flow to overall flow
            max_flow += path_flow;
        }

        // Return the overall flow
        return max_flow;
    }

    // Driver code
    public static void Main()
    {
        // Let us create a graph shown in the above example
        int[, ] graph = new int[, ] {
            { 0, 16, 13, 0, 0, 0 }, { 0, 0, 10, 12, 0, 0 },
            { 0, 4, 0, 0, 14, 0 },  { 0, 0, 9, 0, 0, 20 },
            { 0, 0, 0, 7, 0, 4 },   { 0, 0, 0, 0, 0, 0 }
        };
        MaxFlow m = new MaxFlow();

        Console.WriteLine("The maximum possible flow is "
                          + m.fordFulkerson(graph, 0, 5));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript program for implementation of Ford
// Fulkerson algorithm

// Number of vertices in graph
let V = 6;

// Returns true if there is a path from source
// 's' to sink 't' in residual graph. Also
// fills parent[] to store the path
function bfs(rGraph, s, t, parent)
{

    // Create a visited array and mark all
    // vertices as not visited
    let visited = new Array(V);
    for(let i = 0; i < V; ++i)
        visited[i] = false;

    // Create a queue, enqueue source vertex
    // and mark source vertex as visited
    let queue  = [];
    queue.push(s);
    visited[s] = true;
    parent[s] = -1;

    // Standard BFS Loop
    while (queue.length != 0)
    {
        let u = queue.shift();

        for(let v = 0; v < V; v++)
        {
            if (visited[v] == false &&
                rGraph[u][v] > 0)
            {

                // If we find a connection to the sink
                // node, then there is no point in BFS
                // anymore We just have to set its parent
                // and can return true
                if (v == t)
                {
                    parent[v] = u;
                    return true;
                }
                queue.push(v);
                parent[v] = u;
                visited[v] = true;
            }
        }
    }

    // We didn't reach sink in BFS starting
    // from source, so return false
    return false;
}

// Returns tne maximum flow from s to t in
// the given graph
function fordFulkerson(graph, s, t)
{
    let u, v;

    // Create a residual graph and fill the
    // residual graph with given capacities
    // in the original graph as residual
    // capacities in residual graph

    // Residual graph where rGraph[i][j]
    // indicates residual capacity of edge
    // from i to j (if there is an edge.
    // If rGraph[i][j] is 0, then there is
    // not)
    let rGraph = new Array(V);

    for(u = 0; u < V; u++)
    {
        rGraph[u] = new Array(V);
        for(v = 0; v < V; v++)
            rGraph[u][v] = graph[u][v];
     }

    // This array is filled by BFS and to store path
    let parent = new Array(V);

    // There is no flow initially
    let max_flow = 0;

    // Augment the flow while there
    // is path from source to sink
    while (bfs(rGraph, s, t, parent))
    {

        // Find minimum residual capacity of the edhes
        // along the path filled by BFS. Or we can say
        // find the maximum flow through the path found.
        let path_flow = Number.MAX_VALUE;
        for(v = t; v != s; v = parent[v])
        {
            u = parent[v];
            path_flow = Math.min(path_flow,
                                 rGraph[u][v]);
        }

        // Update residual capacities of the edges and
        // reverse edges along the path
        for(v = t; v != s; v = parent[v])
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

// Driver code

// Let us create a graph shown in the above example
let graph = [ [ 0, 16, 13, 0, 0, 0 ],
              [ 0, 0, 10, 12, 0, 0 ],
              [ 0, 4, 0, 0, 14, 0 ], 
              [ 0, 0, 9, 0, 0, 20 ],
              [ 0, 0, 0, 7, 0, 4 ],  
              [ 0, 0, 0, 0, 0, 0 ] ];
document.write("The maximum possible flow is " +
               fordFulkerson(graph, 0, 5));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
The maximum possible flow is 23
```

福特富尔克森算法的上述实现称为 [**埃德蒙兹-卡普算法**](http://en.wikipedia.org/wiki/Edmonds%E2%80%93Karp_algorithm) 。埃德蒙兹-卡普的想法是在福特富尔克森实现中使用 BFS，因为 BFS 总是选择一条边数最少的路径。当使用 BFS 时，最坏情况时间复杂度可以降低到 0(VE<sup>2</sup>)。上面的实现使用邻接矩阵表示，尽管其中 BFS 花费 O(V <sup>2</sup> )时间，但是上面的实现的时间复杂度是 O(EV <sup>3</sup> )(关于时间复杂度的证明，请参考 [CLRS 书](http://www.flipkart.com/introduction-algorithms-3rd/p/itmczynzhyhxv2gs?pid=9788120340077&affid=sandeepgfg))
这是一个重要的问题，因为它出现在许多实际情况中。例如，在给定流量限制的情况下最大化传输，在计算机网络中最大化分组流。
[Dinc 的最大流算法。](https://www.geeksforgeeks.org/dinics-algorithm-maximum-flow/)

**练习:**
修改上面的实现，使其在 O(VE <sup>2</sup> 时间内运行。

**参考文献:**
[http://www . Stanford . edu/class/cs97si/08-network-flow-problems . pdf](http://www.stanford.edu/class/cs97si/08-network-flow-problems.pdf)
[Clifford Stein、Thomas H. Cormen、Charles E. Leiserson、罗纳德·L·李维斯特](http://www.flipkart.com/introduction-algorithms-3rd/p/itmczynzhyhxv2gs?pid=9788120340077&affid=sandeepgfg)
算法导论第三版如果发现有不正确的地方，请写评论，或者想分享以上讨论话题的更多信息。