# 使用最短路径更快算法检测图形中的负周期

> 原文： [https://www.geeksforgeeks.org/detect-a-negative-cycle-in-a-graph-using-shortest-path-faster-algorithm/](https://www.geeksforgeeks.org/detect-a-negative-cycle-in-a-graph-using-shortest-path-faster-algorithm/)

给定[图](https://www.geeksforgeeks.org/introduction-to-graphs/)`G`，其中包含 **[0，N – 1]** 个节点，一个源`S`和一个数组 **类型为[ **u，v，w** }的 Edges [] [3]** ，表示节点`u`和`v`之间存在有向边 重量`w`，任务是检查给定来源是否存在[负循环](https://www.geeksforgeeks.org/detect-negative-cycle-graph-bellman-ford/)。 如果发现是真的，则打印**“是”** 。 否则，打印**“否”** 。

> **负循环**是一个循环，其中该循环中其所有权重的总和为**负**。

**示例**：

> **输入**：N = 4，M = 4，Edges [] [] = {{0，1，1}，{1，2，-1}，{2，3，-1}，{ 3，0，-1}}，S = 0
> **输出**：`Yes`
> **说明**：
> 
> ![](img/63ccd7daab13844978f1f6ba6201088b.png)
> 
> 从源节点 0 开始，图形包含的循环为 0-> 1-> 2-> 3->0。
> 上述路径中的权重总和是 1 – 1 – 1 – 1 = -2。
> 因此，该图包含负周期。
> 
> **输入**：N = 4，M = 5，Edges [] [] = {{0，2，-2}，{1，0，4}，{1，2，-3}，{ 2，3}，{3，1}}，W [] = {-2，4，-3，2，-1}，S = 1
> **输出**：`Yes`
> **说明**：
> 
> ![](img/e380566989f5a88db96715bd14752511.png)
> 
> 从源节点 1 开始，图形包含的循环为 1-> 2-> 3->1。
> 上述路径中的权重总和是-3 + 2 – 1 = -2。
> 因此，该图包含负周期。

**方法**：这个想法是使用[最短路径更快算法（SPFA）](https://www.geeksforgeeks.org/shortest-path-faster-algorithm/)查找是否存在负循环，并且该负循环可以从图中的源顶点到达。 请按照以下步骤解决问题：

*   将数组 **dis []** 初始化为大数值，将 **vis []** 初始化为 false，将 **cnt []** 初始化为存储顶点松弛次数的计数 。

*   [使用](https://www.geeksforgeeks.org/algorithms-gq/graph-traversals-gq/) [SPFA 算法](https://www.geeksforgeeks.org/shortest-path-faster-algorithm/)遍历图形。

*   每当顶点松弛时，增加每个顶点的计数。

> 术语**松弛**表示如果通过包含通过顶点`v`的路径可以改善与顶点`v`连接的所有顶点的成本，则更新这些成本。

*   停止算法并在 **N <sup>th</sup>** 时间某个顶点放松后立即打印**是**，因为只有`N`顶点 即从`0`到 **N – 1** 。

*   否则，打印**“否”** 。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

bool sfpa(int V, int src, int Edges[][3],
          int M)
{
    // Stores the adjcency list of
    // the given graph
    vector<pair<int, int> > g[V];

    // Create Adjacency List
    for (int i = 0; i < M; i++) {

        int u = Edges[i][0];
        int v = Edges[i][1];
        int w = Edges[i][2];

        g[u].push_back({ v, w });
    }

    // Stores the distance of all
    // reachable vertex from source
    vector<int> dist(V, INT_MAX);

    // Check if vertex is present
    // in queue or not
    vector<bool> inQueue(V, false);

    // Counts the relaxation for
    // each vertex
    vector<int> cnt(V, 0);

    // Distance from src to src is 0
    dist[src] = 0;

    // Create a queue
    queue<int> q;

    // Push source in the queue
    q.push(src);

    // Mark source as visited
    inQueue[src] = true;

    while (!q.empty()) {

        // Front vertex of Queue
        int u = q.front();
        q.pop();

        inQueue[u] = false;

        // Relaxing all edges of
        // vertex from the Queue
        for (pair<int, int> x : g[u]) {

            int v = x.first;
            int cost = x.second;

            // Update the dist[v] to
            // minimum distance
            if (dist[v] > dist[u] + cost) {

                dist[v] = dist[u] + cost;

                // If vertex v is in Queue
                if (!inQueue[v]) {
                    q.push(v);
                    inQueue[v] = true;
                    cnt[v]++;

                    // Negative cycle
                    if (cnt[v] >= V)
                        return true;
                }
            }
        }
    }

    // No cycle found
    return false;
}

// Driver Code
int main()
{
    // Number of vertices
    int N = 4;

    // Given source node src
    int src = 0;

    // Number of Edges
    int M = 4;

    // Given Edges with weight
    int Edges[][3] = { { 0, 1, 1 },
                       { 1, 2, -1 },
                       { 2, 3, -1 },
                       { 3, 0, -1 } };

    // If cycle is present
    if (sfpa(N, src, Edges, M) == true)
        cout << "Yes" << endl;
    else
        cout << "No" << endl;

    return 0;
}

```

## Java

```java

// Java program for 
// the above approach
import java.util.*;
class GFG{

static class pair
{ 
  int first, second; 
  public pair(int first, 
              int second)  
  { 
    this.first = first; 
    this.second = second; 
  }    
} 

static boolean sfpa(int V, int src, 
                    int Edges[][], int M)
{
  // Stores the adjcency list of
  // the given graph
  Vector<pair> []g = new Vector[V];
  for (int i = 0; i < V; i++) 
  {
    g[i] = new Vector<pair>();
  }

  // Create Adjacency List
  for (int i = 0; i < M; i++) 
  {
    int u = Edges[i][0];
    int v = Edges[i][1];
    int w = Edges[i][2];
    g[u].add(new pair(v, w));
  }

  // Stores the distance of all
  // reachable vertex from source
  int []dist = new int[V];
  Arrays.fill(dist, Integer.MAX_VALUE);

  // Check if vertex is present
  // in queue or not
  boolean []inQueue = new boolean[V];

  // Counts the relaxation for
  // each vertex
  int []cnt = new int[V];

  // Distance from src 
  // to src is 0
  dist[src] = 0;

  // Create a queue
  Queue<Integer> q = new LinkedList<>();

  // Push source in the queue
  q.add(src);

  // Mark source as visited
  inQueue[src] = true;

  while (!q.isEmpty()) 
  {
    // Front vertex of Queue
    int u = q.peek();
    q.remove();

    inQueue[u] = false;

    // Relaxing all edges of
    // vertex from the Queue
    for (pair x : g[u]) 
    {
      int v = x.first;
      int cost = x.second;

      // Update the dist[v] to
      // minimum distance
      if (dist[v] > dist[u] + cost) 
      {
        dist[v] = dist[u] + cost;

        // If vertex v is in Queue
        if (!inQueue[v]) 
        {
          q.add(v);
          inQueue[v] = true;
          cnt[v]++;

          // Negative cycle
          if (cnt[v] >= V)
            return true;
        }
      }
    }
  }

  // No cycle found
  return false;
}

// Driver Code
public static void main(String[] args)
{
  // Number of vertices
  int N = 4;

  // Given source node src
  int src = 0;

  // Number of Edges
  int M = 4;

  // Given Edges with weight
  int Edges[][] = {{0, 1, 1},
                   {1, 2, -1},
                   {2, 3, -1},
                   {3, 0, -1}};

  // If cycle is present
  if (sfpa(N, src, Edges, M) == true)
    System.out.print("Yes" + "\n");
  else
    System.out.print("No" + "\n");
}
}

// This code is contributed by 29AjayKumar

```

## Python

```py

# Python3 program for the above approach
import sys

def sfpa(V, src, Edges, M):

    # Stores the adjcency list of
    # the given graph
    g = [[] for i in range(V)]

    # Create Adjacency List
    for i in range(M):
        u = Edges[i][0]
        v = Edges[i][1]
        w = Edges[i][2]

        g[u].append([v, w])

    # Stores the distance of all
    # reachable vertex from source
    dist = [sys.maxsize for i in range(V)]

    # Check if vertex is present
    # in queue or not
    inQueue = [False for i in range(V)]

    # Counts the relaxation for
    # each vertex
    cnt = [0 for i in range(V)]

    # Distance from src to src is 0
    dist[src] = 0

    # Create a queue
    q = []

    # Push source in the queue
    q.append(src)

    # Mark source as visited
    inQueue[src] = True

    while (len(q)):

        # Front vertex of Queue
        u = q[0]
        q.remove(q[0])

        inQueue[u] = False

        # Relaxing all edges of
        # vertex from the Queue
        for x in g[u]:
            v = x[0]
            cost = x[1]

            # Update the dist[v] to
            # minimum distance
            if (dist[v] > dist[u] + cost):
                dist[v] = dist[u] + cost

                # If vertex v is in Queue
                if (inQueue[v] == False):
                    q.append(v)
                    inQueue[v] = True
                    cnt[v] += 1

                    # Negative cycle
                    if (cnt[v] >= V):
                        return True

    # No cycle found
    return False

# Driver Code
if __name__ == '__main__':

    # Number of vertices
    N = 4

    # Given source node src
    src = 0

    # Number of Edges
    M = 4

    # Given Edges with weight
    Edges = [ [ 0, 1, 1 ],
              [ 1, 2, -1 ],
              [ 2, 3, -1 ],
              [ 3, 0, -1 ] ]

    # If cycle is present
    if (sfpa(N, src, Edges, M) == True):
        print("Yes")
    else:
        print("No")

# This code is contributed by SURENDRA_GANGWAR

```

## C#

```cs

// C# program for 
// the above approach
using System;
using System.Collections.Generic;
class GFG{

class pair
{ 
  public int first, second; 
  public pair(int first, 
              int second)  
  { 
    this.first = first; 
    this.second = second; 
  }    
} 

static bool sfpa(int V, int src, 
                 int [,]Edges, int M)
{
  // Stores the adjcency list of
  // the given graph
  List<pair> []g = new List<pair>[V];
  for (int i = 0; i < V; i++) 
  {
    g[i] = new List<pair>();
  }

  // Create Adjacency List
  for (int i = 0; i < M; i++) 
  {
    int u = Edges[i, 0];
    int v = Edges[i, 1];
    int w = Edges[i, 2];
    g[u].Add(new pair(v, w));
  }

  // Stores the distance of all
  // reachable vertex from source
  int []dist = new int[V];
  for (int i = 0; i < V; i++) 
    dist[i] = int.MaxValue;

  // Check if vertex is present
  // in queue or not
  bool []inQueue = new bool[V];

  // Counts the relaxation for
  // each vertex
  int []cnt = new int[V];

  // Distance from src 
  // to src is 0
  dist[src] = 0;

  // Create a queue
  Queue<int> q = new Queue<int>();

  // Push source in the queue
  q.Enqueue(src);

  // Mark source as visited
  inQueue[src] = true;

  while (q.Count != 0) 
  {
    // Front vertex of Queue
    int u = q.Peek();
    q.Dequeue();

    inQueue[u] = false;

    // Relaxing all edges of
    // vertex from the Queue
    foreach (pair x in g[u]) 
    {
      int v = x.first;
      int cost = x.second;

      // Update the dist[v] to
      // minimum distance
      if (dist[v] > dist[u] + cost) 
      {
        dist[v] = dist[u] + cost;

        // If vertex v is in Queue
        if (!inQueue[v]) 
        {
          q.Enqueue(v);
          inQueue[v] = true;
          cnt[v]++;

          // Negative cycle
          if (cnt[v] >= V)
            return true;
        }
      }
    }
  }

  // No cycle found
  return false;
}

// Driver Code
public static void Main(String[] args)
{
  // Number of vertices
  int N = 4;

  // Given source node src
  int src = 0;

  // Number of Edges
  int M = 4;

  // Given Edges with weight
  int [,]Edges = {{0, 1, 1},
                  {1, 2, -1},
                  {2, 3, -1},
                  {3, 0, -1}};

  // If cycle is present
  if (sfpa(N, src, Edges, M) == true)
    Console.Write("Yes" + "\n");
  else
    Console.Write("No" + "\n");
}
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
Yes

```

**时间复杂度**：`O(N * M)`，其中 N 是顶点数，M 是边数。

**辅助空间**：O（N + M）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。