# 图中最远节点距离的最小值

> 原文:[https://www . geesforgeks . org/图中最远节点的最小距离值/](https://www.geeksforgeeks.org/minimum-value-of-distance-of-farthest-node-in-a-graph/)

给定一个具有 **N** 个节点和 **N-1** 条边的非循环无向图，其形式为 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**其中每一行由两个数字 **L 和 R** 组成，表示 **L 和 R** 之间的边。对于树中的每个节点 **X** ，让 **dis(X)** 表示从 **X** 到最远节点的边数。任务是找到给定图形的 **dis(x)** 的最小值。

**示例:**

> **输入:** N = 6，arr[][] = { {1，4}，{2，3}，{3，4}，{4，5}，{5，6} }
> 输出:2
> T6】解释:
> 以下是上述信息的图表:
> 
> ![](img/fc16f9c3fc5220964c13895ca1fa15e9.png)
> 
> 从上图中我们可以看到，距离顶点 0 最远的节点在距离 3 处。通过对图中的所有节点重复 DFS 遍历，我们从源节点到最远节点的最大距离[]为:
> distance[] = {3，4，3，2，3，4}，距离中的最小值就是需要的结果。
> 
> **输入:** N = 6，arr[][] = { {1，2}，{1，3}，{1，4}，{2，5}，{2，6} }
> **输出:** 2
> **解释:**
> 上图从每个节点到最远节点的距离[]为:
> 距离[] = {3，4，3，2，3，4}，距离的最小值为 1。

**方法:**
思路是用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来解决这个问题。以下是步骤:

1.  对于任何节点(比如 **a** )使用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)遍历图，节点与自身的距离为 0。
2.  对于节点 **a** 的每次递归调用，保持更新递归节点与节点 **a** 在[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中的距离(说**距离【】**)。
3.  通过对节点 a 的每次递归调用取距离的最大值，给出节点 **a** 和它的**最远的**节点之间的边数。
4.  对图中所有节点重复上述步骤，并不断更新距离[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) ( **距离[]** )中每个节点最远的节点距离。
5.  数组**距离[]** 的最小值就是想要的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Distance vector to find the distance of
// a node to it's farthest node
vector<int> dist;

// To keep the track of visited array
// while DFS Traversal
vector<int> vis;

// Function for DFS traversal to update
// the distance vector
void dfs(int u, vector<int> Adj[], int s)
{
    // Mark the visited array for vertex u
    vis[u] = true;

    // Traverse the adjacency list for u
    for (auto& it : Adj[u]) {

        // If the any node is not visited,
        // then recursively call for next
        // vertex with distance increment
        // by 1
        if (vis[it] == false) {
            dfs(it, Adj, s + 1);
        }
    }

    // Update the maximum distance for the
    // farthest vertex from node u
    dist[u] = max(dist[u], s);
}

// Function to find the minimum of the
// farthest vertex for every vertex in
// the graph
void minFarthestDistance(int arr[][2], int n)
{

    // Resize distance vector
    dist.resize(n + 1, 0);

    // To create adjacency list for graph
    vector<int> Adj[n + 1];

    // Create Adjacency list for every
    // edge given in arr[][]
    for (int i = 0; i < n - 1; i++) {
        Adj[arr[i][0]].push_back(arr[i][1]);
        Adj[arr[i][1]].push_back(arr[i][0]);
    }

    // DFS Traversal for every node in the
    // graph to update the distance vector
    for (int i = 1; i <= n; i++) {

        // Clear and resize vis[] before
        // DFS traversal for every vertex
        vis.clear();
        vis.resize(n + 1, false);

        // DFS Traversal for vertex i
        dfs(i, Adj, 0);
    }

    cout << *min_element(dist.begin() + 1,
                         dist.end());
}

// Driver Code
int main()
{
    // Number of Nodes
    int N = 6;
    int arr[][2] = { { 1, 4 }, { 2, 3 }, { 3, 4 },
                     { 4, 5 }, { 5, 6 } };

    minFarthestDistance(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Distance vector to find the distance
// of a node to it's farthest node
static int[] dist;

// To keep the track of visited array
// while DFS Traversal
static boolean[] vis;

// Function for DFS traversal to update
// the distance vector
static void dfs(int u, Vector<Integer>[] Adj, int s)
{

    // Mark the visited array for vertex u
    vis[u] = true;

    // Traverse the adjacency list for u
    for (int it : Adj[u])
    {

        // If the any node is not visited,
        // then recursively call for next
        // vertex with distance increment
        // by 1
        if (vis[it] == false)
        {
            dfs(it, Adj, s + 1);
        }
    }

    // Update the maximum distance for
    // the farthest vertex from node u
    dist[u] = Math.max(dist[u], s);
}

// Function to find the minimum of the
// farthest vertex for every vertex in
// the graph
static void minFarthestDistance(int[][] arr, int n)
{

    // Resize distance vector
    dist = new int[n + 1];
    Arrays.fill(dist, 0);

    // To create adjacency list for graph
    @SuppressWarnings("unchecked")
    Vector<Integer>[] Adj = new Vector[n + 1];

    for(int i = 0; i < n + 1; i++)
    {
        Adj[i] = new Vector<>();
    }

    // Create Adjacency list for every
    // edge given in arr[][]
    for(int i = 0; i < n - 1; i++)
    {
        Adj[arr[i][0]].add(arr[i][1]);
        Adj[arr[i][1]].add(arr[i][0]);
    }

    // DFS Traversal for every node in the
    // graph to update the distance vector
    for(int i = 1; i <= n; i++)
    {

        // Clear and resize vis[] before
        // DFS traversal for every vertex
        vis = new boolean[n + 1];
        Arrays.fill(vis, false);

        // DFS Traversal for vertex i
        dfs(i, Adj, 0);
    }

    int min = Integer.MAX_VALUE;
    for(int i = 1; i < dist.length; i++)
    {
        if (dist[i] < min)
            min = dist[i];
    }
    System.out.println(min);
}

// Driver Code
public static void main(String[] args)
{

    // Number of Nodes
    int N = 6;
    int[][] arr = { { 1, 4 }, { 2, 3 },
                    { 3, 4 }, { 4, 5 },
                    { 5, 6 } };

    minFarthestDistance(arr, N);
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function for DFS traversal to update
# the distance vector
def dfs(u, s):

    global vis, Adj, dist

    # Mark the visited array for vertex u
    vis[u] = True

    # Traverse the adjacency list for u
    for it in Adj[u]:

        # If the any node is not visited,
        # then recursively call for next
        # vertex with distance increment
        # by 1
        if (vis[it] == False):
            dfs(it, s + 1)

    # Update the maximum distance for the
    # farthest vertex from node u
    dist[u] = max(dist[u], s)

# Function to find the minimum of the
# farthest vertex for every vertex in
# the graph
def minFarthestDistance(arr, n):

    global dist, vis, Adj

    # Create Adjacency list for every
    # edge given in arr[][]
    for i in range(n - 1):
        Adj[arr[i][0]].append(arr[i][1])
        Adj[arr[i][1]].append(arr[i][0])

    # DFS Traversal for every node in the
    # graph to update the distance vector
    for i in range(1, n + 1):

        # Clear and resize vis[] before
        # DFS traversal for every vertex
        # vis.clear()
        for j in range(n + 1):
            vis[j] = False

        # vis.resize(n + 1, false)

        # DFS Traversal for vertex i
        dfs(i, 0)

    print(min(dist[i] for i in range(1, n + 1)))

# Driver Code
if __name__ == '__main__':

    dist = [0 for i in range(1001)]
    vis = [False for i in range(1001)]
    Adj = [[] for i in range(1001)]

    # Number of Nodes
    N = 6
    arr = [ [ 1, 4 ], [ 2, 3 ],
            [ 3, 4 ], [ 4, 5 ], [ 5, 6 ] ]

    minFarthestDistance(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Distance vector to find the distance
  // of a node to it's farthest node
  static int[] dist;

  // To keep the track of visited array
  // while DFS Traversal
  static bool[] vis;

  // Function for DFS traversal to update
  // the distance vector
  static void dfs(int u, List<List<int>> Adj, int s)
  {

    // Mark the visited array for vertex u
    vis[u] = true;

    // Traverse the adjacency list for u
    foreach(int it in Adj[u])
    {

      // If the any node is not visited,
      // then recursively call for next
      // vertex with distance increment
      // by 1
      if (vis[it] == false)
      {
        dfs(it, Adj, s + 1);
      }
    }

    // Update the maximum distance for
    // the farthest vertex from node u
    dist[u] = Math.Max(dist[u], s);       
  }

  // Function to find the minimum of the
  // farthest vertex for every vertex in
  // the graph
  static void minFarthestDistance(int[,] arr, int n)
  {

    // Resize distance vector
    dist = new int[n + 1];
    Array.Fill(dist, 0);

    // To create adjacency list for graph
    List<List<int>> Adj = new List<List<int>>();
    for(int i = 0; i < n + 1; i++)
    {
      Adj.Add(new List<int>());
    }

    // Create Adjacency list for every
    // edge given in arr[][]
    for(int i = 0; i < n - 1; i++)
    {
      Adj[arr[i, 0]].Add(arr[i, 1]);
      Adj[arr[i, 1]].Add(arr[i, 0]);
    }

    // DFS Traversal for every node in the
    // graph to update the distance vector
    for(int i = 1; i <= n; i++)
    {

      // Clear and resize vis[] before
      // DFS traversal for every vertex
      vis = new bool[n + 1];
      Array.Fill(vis, false);

      // DFS Traversal for vertex i
      dfs(i, Adj, 0);
    }
    int min = Int32.MaxValue;
    for(int i = 1; i < dist.Length; i++)
    {
      if (dist[i] < min)
      {
        min = dist[i];
      }

    }
    Console.WriteLine(min);  
  }

  // Driver Code
  static public void Main ()
  {

    // Number of Nodes
    int N = 6;
    int[,] arr = { { 1, 4 }, { 2, 3 },{ 3, 4 },
                  { 4, 5 }, { 5, 6 } };
    minFarthestDistance(arr, N);
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Distance vector to find the distance
// of a node to it's farthest node
let dist=[];

// To keep the track of visited array
// while DFS Traversal
let vis=[];

// Function for DFS traversal to update
// the distance vector
function dfs(u,Adj,s)
{
    // Mark the visited array for vertex u
    vis[u] = true;

    // Traverse the adjacency list for u
    for (let it=0;it<Adj[u].length;it++)
    {

        // If the any node is not visited,
        // then recursively call for next
        // vertex with distance increment
        // by 1
        if (vis[Adj[u][it]] == false)
        {
            dfs(Adj[u][it], Adj, s + 1);
        }
    }

    // Update the maximum distance for
    // the farthest vertex from node u
    dist[u] = Math.max(dist[u], s);
}

// Function to find the minimum of the
// farthest vertex for every vertex in
// the graph
function minFarthestDistance(arr,n)
{
    // Resize distance vector
    dist = new Array(n + 1);
    for(let i=0;i<(n+1);i++)
    {
        dist[i]=0;
    }

    // To create adjacency list for graph

    let Adj = new Array(n + 1);

    for(let i = 0; i < n + 1; i++)
    {
        Adj[i] = [];
    }

    // Create Adjacency list for every
    // edge given in arr[][]
    for(let i = 0; i < n - 1; i++)
    {
        Adj[arr[i][0]].push(arr[i][1]);
        Adj[arr[i][1]].push(arr[i][0]);
    }

    // DFS Traversal for every node in the
    // graph to update the distance vector
    for(let i = 1; i <= n; i++)
    {

        // Clear and resize vis[] before
        // DFS traversal for every vertex
        vis = new Array(n + 1);
        for(let i=0;i<(n+1);i++)
        {
            vis[i]=false;
        }

        // DFS Traversal for vertex i
        dfs(i, Adj, 0);
    }

    let min = Number.MAX_VALUE;
    for(let i = 1; i < dist.length; i++)
    {
        if (dist[i] < min)
            min = dist[i];
    }
    document.write(min);
}

// Driver Code
// Number of Nodes
let N = 6;
let arr=[[ 1, 4 ], [ 2, 3 ],
                    [ 3, 4 ], [ 4, 5 ],
                    [ 5, 6 ]];
minFarthestDistance(arr, N);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(V*(V+E))，其中 V 为顶点数，E 为边数。
**辅助空间:** O(V + E)