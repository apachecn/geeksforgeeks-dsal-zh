# 最小化为无向图

的所有顶点着色的成本

> 原文： [https://www.geeksforgeeks.org/minimize-cost-to-color-all-the-vertices-of-an-undirected-graph/](https://www.geeksforgeeks.org/minimize-cost-to-color-all-the-vertices-of-an-undirected-graph/)

给定一个[无向图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，该图由`N`个顶点和`M`个边组成，其中节点值在 **[1，N]** 范围内，并且 数组 **colored []** 指定的顶点是有色的，任务是找到给定图的所有顶点的最小颜色。 着色顶点的成本由 **vCost** 决定，在两个顶点之间添加新边的成本由 **eCost** 决定。 如果顶点是有色的，那么从该顶点可以到达的所有顶点也将变为有色。

**示例**：

> **输入**：N = 3，M = 1，vCost = 3，eCost = 2，有色[] = {1}，source [] = {1} Destination [] = {2}
> [ **输出**：2
> **说明**：
> 顶点 1 着色，并且其边缘带有 2。
> 因此，顶点 2 也着色。
> 以 eCost 的代价在 2 和 3 之间添加一条边。 < vCost。
> 因此，输出为 2。
> 
> **输入**：N = 4，M = 2，vCost = 3，eCost = 7，有色[] = {1，3}，source [] = {1，2} destination [] = {4， 3}
> **输出**：0
> **说明**：
> 顶点 1 着色，并且其边缘为 4。因此，顶点 4 也着色。
> 顶点 2 已着色，并且其边缘带有 3。因此，顶点 3 也已着色。
> 由于所有顶点均已着色，因此成本为 0。

**方法**：
的想法是，**使用 [DFS 遍历](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)计算无色顶点的子图**的数量。
为使未着色的**未着色** [**子图**](https://www.geeksforgeeks.org/find-all-cliques-of-size-k-in-an-undirected-graph/) 的着色成本降至最低，需要执行以下任一操作：

*   为子图着色
*   在任何有色和无色顶点之间添加一条边。

根据 ***eCost** 和 **vCost*** 的最小值，需要选择以上两个步骤之一。
如果未着色子图的数量由`X`给出，则为所有顶点着色的总成本由 ***X×min（eCost，vCost）**给出 ]* 。

请按照以下步骤查找未着色子图的数量：

1.  在所有有色顶点上执行 DFS 遍历，并将它们标记为已访问以将其标识为有色。
2.  在步骤 1 的 [DFS](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 之后未访问的顶点是未着色的顶点。
3.  对于每个未着色的顶点，使用 [DFS 标记从该顶点可以访问的所有顶点。](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)
4.  在步骤 3 出现 [DFS](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 的未着色顶点的数量是子图 **X 的数量。**
5.  通过公式 ***X×min（eCost，vCost）计算为所有顶点着色的总成本。***

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to implement DFS Traversal
// to marks all the vertices visited
// from vertex U
void DFS(int U, int* vis, vector<int> adj[])
{
    // Mark U as visited
    vis[U] = 1;

    // Traverse the adjacency list of U
    for (int V : adj[U]) {
        if (vis[V] == 0)
            DFS(V, vis, adj);
    }
}

// Function to find the minimum cost
// to color all the vertices of graph
void minCost(int N, int M, int vCost,
             int eCost, int sorc[],
             vector<int> colored,
             int destination[])
{
    // To store adjacency list
    vector<int> adj[N + 1];

    // Loop through the edges to
    // create adjacency list
    for (int i = 0; i < M; i++) {

        adj[sorc[i]].push_back(destination[i]);
        adj[destination[i]].push_back(sorc[i]);
    }

    // To check if a vertex of the
    // graph is visited
    int vis[N + 1] = { 0 };

    // Mark visited to all the vertices
    // that can be reached by
    // colored vertices
    for (int i = 0; i < colored.size(); i++) {

        // Perform DFS
        DFS(colored[i], vis, adj);
    }

    // To store count of uncolored
    // sub-graphs
    int X = 0;

    // Loop through vertex to count
    // uncolored sub-graphs
    for (int i = 1; i <= N; i++) {

        // If vertex not visited
        if (vis[i] == 0) {

            // Increase count of
            // uncolored sub-graphs
            X++;

            // Perform DFS to mark
            // visited to all vertices
            // of current sub-graphs
            DFS(i, vis, adj);
        }
    }

    // Calculate minimum cost to color
    // all vertices
    int mincost = X * min(vCost, eCost);

    // Print the result
    cout << mincost << endl;
}

// Driver Code
int main()
{

    // Given number of
    // vertices and edges
    int N = 3, M = 1;

    // Given edges
    int sorc[] = { 1 };
    int destination[] = { 2 };

    // Given cost of coloring
    // and adding an edge
    int vCost = 3, eCost = 2;

    // Given array of
    // colored vertices
    vector<int> colored = { 1};

    minCost(N, M, vCost, eCost,
            sorc, colored, destination);

    return 0;
}

```

## Java

```java

// Java program to implement 
// the above approach 
import java.util.*;

class GFG{

// Function to implement DFS Traversal
// to marks all the vertices visited
// from vertex U
static void DFS(int U, int[] vis,
                ArrayList<ArrayList<Integer>> adj)
{

    // Mark U as visited
    vis[U] = 1;

    // Traverse the adjacency list of U
    for(Integer V : adj.get(U))
    {
        if (vis[V] == 0)
            DFS(V, vis, adj);
    }
}

// Function to find the minimum cost
// to color all the vertices of graph
static void minCost(int N, int M, int vCost,
                    int eCost, int sorc[],
                    ArrayList<Integer> colored,
                    int destination[])
{

    // To store adjacency list
    ArrayList<ArrayList<Integer>> adj = new ArrayList<>();

    for(int i = 0; i < N + 1; i++)
        adj.add(new ArrayList<Integer>());

    // Loop through the edges to
    // create adjacency list
    for(int i = 0; i < M; i++) 
    {
        adj.get(sorc[i]).add(destination[i]);
        adj.get(destination[i]).add(sorc[i]);
    }

    // To check if a vertex of the
    // graph is visited
    int[] vis = new int[N + 1];

    // Mark visited to all the vertices
    // that can be reached by
    // colored vertices
    for(int i = 0; i < colored.size(); i++) 
    {

        // Perform DFS
        DFS(colored.get(i), vis, adj);
    }

    // To store count of uncolored
    // sub-graphs
    int X = 0;

    // Loop through vertex to count
    // uncolored sub-graphs
    for(int i = 1; i <= N; i++)
    {

        // If vertex not visited
        if (vis[i] == 0) 
        {

            // Increase count of
            // uncolored sub-graphs
            X++;

            // Perform DFS to mark
            // visited to all vertices
            // of current sub-graphs
            DFS(i, vis, adj);
        }
    }

    // Calculate minimum cost to color
    // all vertices
    int mincost = X * Math.min(vCost, eCost);

    // Print the result
    System.out.println(mincost);
}

// Driver code
public static void main(String[] args)
{

    // Given number of
    // vertices and edges
    int N = 3, M = 1;

    // Given edges
    int sorc[] = {1};
    int destination[] = {2};

    // Given cost of coloring
    // and adding an edge
    int vCost = 3, eCost = 2;

    // Given array of
    // colored vertices
    ArrayList<Integer> colored = new ArrayList<>();
    colored.add(1);

    minCost(N, M, vCost, eCost, sorc,
            colored, destination);
}
}

// This code is contributed by offbeat

```

## Python3

```

# Python3 program to implement
# the above approach

# Function to implement DFS Traversal
# to marks all the vertices visited
# from vertex U
def DFS(U, vis, adj):

    # Mark U as visited
    vis[U] = 1

    # Traverse the adjacency list of U
    for V in adj[U]:
        if (vis[V] == 0):
            DFS(V, vis, adj)

# Function to find the minimum cost
# to color all the vertices of graph
def minCost(N, M, vCost, eCost, sorc,
            colored, destination):

    # To store adjacency list
    adj = [[] for i in range(N + 1)]

    # Loop through the edges to
    # create adjacency list
    for i in range(M):
        adj[sorc[i]].append(destination[i])
        adj[destination[i]].append(sorc[i])

    # To check if a vertex of the
    # graph is visited
    vis = [0] * (N + 1)

    # Mark visited to all the vertices
    # that can be reached by
    # colored vertices
    for i in range(len(colored)):

        # Perform DFS
        DFS(colored[i], vis, adj)

    # To store count of uncolored
    # sub-graphs
    X = 0

    # Loop through vertex to count
    # uncolored sub-graphs
    for i in range(1, N + 1):

        # If vertex not visited
        if (vis[i] == 0):

            # Increase count of
            # uncolored sub-graphs
            X += 1

            # Perform DFS to mark
            # visited to all vertices
            # of current sub-graphs
            DFS(i, vis, adj)

    # Calculate minimum cost to color
    # all vertices
    mincost = X * min(vCost, eCost)

    # Print the result
    print(mincost)

# Driver Code
if __name__ == '__main__':

    # Given number of
    # vertices and edges
    N = 3
    M = 1

    # Given edges
    sorc = [1]
    destination = [2]

    # Given cost of coloring
    # and adding an edge
    vCost = 3
    eCost = 2

    # Given array of
    # colored vertices
    colored = [1]

    minCost(N, M, vCost, eCost,
            sorc, colored, destination)

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program to implement 
// the above approach 
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to implement DFS Traversal
// to marks all the vertices visited
// from vertex U
static void DFS(int U, int[] vis, ArrayList adj)
{

    // Mark U as visited
    vis[U] = 1;

    // Traverse the adjacency list of U
    foreach(int V in (ArrayList)adj[U])
    {
        if (vis[V] == 0)
            DFS(V, vis, adj);
    }
}

// Function to find the minimum cost
// to color all the vertices of graph
static void minCost(int N, int M, int vCost,
                    int eCost, int []sorc,
                    ArrayList colored,
                    int []destination)
{

    // To store adjacency list
    ArrayList adj = new ArrayList();

    for(int i = 0; i < N + 1; i++)
        adj.Add(new ArrayList());

    // Loop through the edges to
    // create adjacency list
    for(int i = 0; i < M; i++) 
    {
        ((ArrayList)adj[sorc[i]]).Add(destination[i]);
        ((ArrayList)adj[destination[i]]).Add(sorc[i]);
    }

    // To check if a vertex of the
    // graph is visited
    int[] vis = new int[N + 1];

    // Mark visited to all the vertices
    // that can be reached by
    // colored vertices
    for(int i = 0; i < colored.Count; i++) 
    {

        // Perform DFS
        DFS((int)colored[i], vis, adj);
    }

    // To store count of uncolored
    // sub-graphs
    int X = 0;

    // Loop through vertex to count
    // uncolored sub-graphs
    for(int i = 1; i <= N; i++)
    {

        // If vertex not visited
        if (vis[i] == 0) 
        {

            // Increase count of
            // uncolored sub-graphs
            X++;

            // Perform DFS to mark
            // visited to all vertices
            // of current sub-graphs
            DFS(i, vis, adj);
        }
    }

    // Calculate minimum cost to color
    // all vertices
    int mincost = X * Math.Min(vCost, eCost);

    // Print the result
    Console.Write(mincost);
}

// Driver code
public static void Main(string[] args)
{

    // Given number of
    // vertices and edges
    int N = 3, M = 1;

    // Given edges
    int []sorc = {1};
    int []destination = {2};

    // Given cost of coloring
    // and adding an edge
    int vCost = 3, eCost = 2;

    // Given array of
    // colored vertices
    ArrayList colored = new ArrayList();
    colored.Add(1);

    minCost(N, M, vCost, eCost, 
            sorc, colored, 
            destination);
}
}

// This code is contributed by rutvik_56

```

**Output:** 

```
2
```

***时间复杂度**：O（N + M）*
***辅助空间**：O（N）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。