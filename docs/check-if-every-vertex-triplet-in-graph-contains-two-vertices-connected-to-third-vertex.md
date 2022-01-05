# 检查图中的每个顶点三元组是否包含两个连接到第三个顶点的顶点

> 原文:[https://www . geesforgeks . org/check-如果图中的每个顶点都包含三个顶点-连接到第三个顶点/](https://www.geeksforgeeks.org/check-if-every-vertex-triplet-in-graph-contains-two-vertices-connected-to-third-vertex/)

给定一个具有 **N** 顶点和 **K** 边的[无向图](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/)，任务是检查对于图中三个顶点的每一个组合，是否存在连接到第三个顶点的两个顶点。换句话说，对于每个顶点三元组 **(a，b，c)** ，如果 **a** 和 **c** 之间存在路径，那么 **b** 和 **c** 之间也应该存在路径。

**示例:**

> **输入:** N = 4，K = 3
> 边:1 - > 2，2 - > 3，3 - > 4
> **输出:** YES
> **说明:**
> 由于整个图形是连通的，上述条件始终有效。
> 
> **输入:** N = 5，K = 3
> 边:1 - > 3，3 - > 4，2 - > 5。
> **输出:**否
> **解释:**
> 如果我们考虑三元组(1，2，3)，那么顶点 1 和 3 之间有路径，但是顶点 2 和 3 之间没有路径。

**方法:**按照以下步骤解决问题–

*   [通过](https://www.geeksforgeeks.org/algorithms-gq/graph-traversals-gq/) [DFS 遍历技术](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)从任意组件遍历图形，并维护两个变量来存储组件最小值和组件最大值。
*   将每个分量的最大值和最小值存储在一个向量中。
*   现在，如果任何两个分量在其最小值和最大值区间有交集，那么将存在一个有效的(a < b < c)三元组。因此，两个组件都应该连接。否则，图形无效。

下面是上述方法的实现

## C++

```
// C++ program of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to add edge into
// the graph
void addEdge(vector<int> adj[],
             int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

void DFSUtil(int u, vector<int> adj[],
             vector<bool>& visited,
             int& componentMin,
             int& componentMax)
{
    visited[u] = true;

    // Finding the maximum and
    // minimum values in each component
    componentMax = max(componentMax, u);
    componentMin = min(componentMin, u);

    for (int i = 0; i < adj[u].size(); i++)
        if (visited[adj[u][i]] == false)
            DFSUtil(adj[u][i], adj, visited,
                    componentMin, componentMax);
}

// Function for checking whether
// the given graph is valid or not
bool isValid(vector<pair<int, int> >& v)
{
    int MAX = -1;
    bool ans = 0;
    // Checking for intersecting intervals
    for (auto i : v) {
        // If intersection is found
        if (i.first <= MAX) {

            // Graph is not valid
            ans = 1;
        }

        MAX = max(MAX, i.second);
    }

    return (ans == 0 ? 1 : 0);
}

// Function for the DFS Traversal
void DFS(vector<int> adj[], int V)
{
    std::vector<pair<int, int> > v;
    // Traversing for every vertex
    vector<bool> visited(V, false);
    for (int u = 1; u <= V; u++) {
        if (visited[u] == false) {
            int componentMax = u;
            int componentMin = u;

            DFSUtil(u, adj, visited,
                    componentMin, componentMax);

            // Storing maximum and minimum
            // values of each component
            v.push_back({ componentMin,
                          componentMax });
        }
    }

    bool check = isValid(v);

    if (check)
        cout << "Yes";
    else
        cout << "No";

    return;
}

// Driver code
int main()
{
    int N = 4, K = 3;

    vector<int> adj[N + 1];

    addEdge(adj, 1, 2);
    addEdge(adj, 2, 3);
    addEdge(adj, 3, 4);

    DFS(adj, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the
// above approach
import java.util.*;
import java.lang.*;

class GFG{

static class pair
{
    int first, second;
    pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to add edge into
// the graph
static void addEdge(ArrayList<ArrayList<Integer>> adj,
                    int u, int v)
{
    adj.get(u).add(v);
    adj.get(v).add(u);
}

static void DFSUtil(int u,
                    ArrayList<ArrayList<Integer>> adj,
                    boolean[] visited,
                    int componentMin,
                    int componentMax)
{
    visited[u] = true;

    // Finding the maximum and
    // minimum values in each component
    componentMax = Math.max(componentMax, u);
    componentMin = Math.min(componentMin, u);

    for(int i = 0; i < adj.get(u).size(); i++)
        if (visited[adj.get(u).get(i)] == false)
            DFSUtil(adj.get(u).get(i), adj, visited,
                    componentMin, componentMax);
}

// Function for checking whether
// the given graph is valid or not
static boolean isValid(ArrayList<pair> v)
{
    int MAX = -1;
    boolean ans = false;

    // Checking for intersecting intervals
    for(pair i : v)
    {

        // If intersection is found
        if (i.first <= MAX)
        {

            // Graph is not valid
            ans = true;
        }
        MAX = Math.max(MAX, i.second);
    }
    return (ans == false ? true : false);
}

// Function for the DFS Traversal
static void DFS(ArrayList<ArrayList<Integer>> adj,
                int V)
{
   ArrayList<pair> v = new ArrayList<>();

   // Traversing for every vertex
   boolean[] visited = new boolean[V + 1];

    for(int u = 1; u <= V; u++)
    {
        if (visited[u] == false)
        {
            int componentMax = u;
            int componentMin = u;

            DFSUtil(u, adj, visited,
                    componentMin,
                    componentMax);

            // Storing maximum and minimum
            // values of each component
            v.add(new pair(componentMin,
                           componentMax));
        }
    }

    boolean check = isValid(v);

    if (check)
        System.out.println("Yes");
    else
        System.out.println("No");

    return;
}

// Driver code
public static void main (String[] args)
{
    int N = 4, K = 3;

    ArrayList<ArrayList<Integer>> adj = new ArrayList<>();

    for(int i = 0; i <= N + 1; i++)
        adj.add(new ArrayList<>());

    addEdge(adj, 1, 2);
    addEdge(adj, 2, 3);
    addEdge(adj, 3, 4);

    DFS(adj, N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program of the
# above approach

# Function to add edge into
# the graph
def addEdge(adj, u, v):

    adj[u].append(v)
    adj[v].append(u)
    return adj

def DFSUtil(u, adj, visited,
            componentMin, componentMax):

    visited[u] = True

    # Finding the maximum and
    # minimum values in each component
    componentMax = max(componentMax, u)
    componentMin = min(componentMin, u)

    for i in range(len(adj[u])):
        if (visited[adj[u][i]] == False):
            visited, componentMax, componentMin = DFSUtil(
                adj[u][i], adj, visited, componentMin,
                componentMax)

    return visited, componentMax, componentMin

# Function for checking whether
# the given graph is valid or not
def isValid(v):

    MAX = -1
    ans = False

    # Checking for intersecting intervals
    for i in v:
        if len(i) != 2:
            continue

        # If intersection is found
        if (i[0] <= MAX):

            # Graph is not valid
            ans = True

        MAX = max(MAX, i[1])

    return (True if ans == False else False)

# Function for the DFS Traversal
def DFS(adj, V):

    v = [[]]

    # Traversing for every vertex
    visited = [False for i in range(V + 1)]

    for u in range(1, V + 1):
        if (visited[u] == False):
            componentMax = u
            componentMin = u

            visited, componentMax, componentMin = DFSUtil(
                u, adj, visited, componentMin,
                componentMax)

            # Storing maximum and minimum
            # values of each component
            v.append([componentMin, componentMax])

    check = isValid(v)

    if (check):
        print('Yes')
    else:
        print('No')

    return

# Driver code
if __name__=="__main__":

    N = 4
    K = 3

    adj = [[] for i in range(N + 1)]

    adj = addEdge(adj, 1, 2)
    adj = addEdge(adj, 2, 3)
    adj = addEdge(adj, 3, 4)

    DFS(adj, N)

# This code is contributed by rutvik_56
```

## C#

```
// C# program of the
// above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to add edge into
// the graph
static void addEdge(ArrayList adj,
                    int u, int v)
{
    ((ArrayList)adj[u]).Add(v);
    ((ArrayList)adj[v]).Add(u);
}

static void DFSUtil(int u, ArrayList adj,
                    bool[] visited,
                    int componentMin,
                    int componentMax)
{
    visited[u] = true;

    // Finding the maximum and
    // minimum values in each component
    componentMax = Math.Max(componentMax, u);
    componentMin = Math.Min(componentMin, u);

    for(int i = 0; i < ((ArrayList)adj[u]).Count; i++)
        if (visited[(int)((ArrayList)adj[u])[i]] == false)
            DFSUtil((int)((ArrayList)adj[u])[i], adj, visited,
                    componentMin, componentMax);
}

// Function for checking whether
// the given graph is valid or not
static bool isValid(ArrayList v)
{
    int MAX = -1;
    bool ans = false;

    // Checking for intersecting intervals
    foreach(pair i in v)
    {

        // If intersection is found
        if (i.first <= MAX)
        {

            // Graph is not valid
            ans = true;
        }
        MAX = Math.Max(MAX, i.second);
    }
    return (ans == false ? true : false);
}

// Function for the DFS Traversal
static void DFS(ArrayList adj,
                int V)
{
   ArrayList v = new ArrayList();

   // Traversing for every vertex
   bool[] visited = new bool[V + 1];

    for(int u = 1; u <= V; u++)
    {
        if (visited[u] == false)
        {
            int componentMax = u;
            int componentMin = u;

            DFSUtil(u, adj, visited,
                    componentMin,
                    componentMax);

            // Storing maximum and minimum
            // values of each component
            v.Add(new pair(componentMin,
                           componentMax));
        }
    }

    bool check = isValid(v);

    if (check)
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");

    return;
}

// Driver code
public static void Main(string[] args)
{
    int N = 4;

    ArrayList adj = new ArrayList();

    for(int i = 0; i <= N + 1; i++)
        adj.Add(new ArrayList());

    addEdge(adj, 1, 2);
    addEdge(adj, 2, 3);
    addEdge(adj, 3, 4);

    DFS(adj, N);
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>

// JavaScript program of the
// above approach

class pair
{
    constructor(first, second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to add edge into
// the graph
function addEdge(adj,u, v)
{
    (adj[u]).push(v);
    (adj[v]).push(u);
}

function DFSUtil(u, adj, visited, componentMin, componentMax)
{
    visited[u] = true;

    // Finding the maximum and
    // minimum values in each component
    componentMax = Math.max(componentMax, u);
    componentMin = Math.min(componentMin, u);

    for(var i = 0; i < (adj[u]).length; i++)
        if (visited[(adj[u])[i]] == false)
            DFSUtil((adj[u])[i], adj, visited,
                    componentMin, componentMax);
}

// Function for checking whether
// the given graph is valid or not
function isValid(v)
{
    var MAX = -1;
    var ans = false;

    // Checking for intersecting intervals
    for(var i of v)
    {

        // If intersection is found
        if (i.first <= MAX)
        {

            // Graph is not valid
            ans = true;
        }
        MAX = Math.max(MAX, i.second);
    }
    return (ans == false ? true : false);
}

// Function for the DFS Traversal
function DFS(adj, V)
{
   var v = [];

   // Traversing for every vertex
   var visited = Array(V+1).fill(false);

    for(var u = 1; u <= V; u++)
    {
        if (visited[u] == false)
        {
            var componentMax = u;
            var componentMin = u;

            DFSUtil(u, adj, visited,
                    componentMin,
                    componentMax);

            // Storing maximum and minimum
            // values of each component
            v.push(new pair(componentMin,
                           componentMax));
        }
    }

    var check = isValid(v);

    if (check)
        document.write("Yes");
    else
        document.write("No");

    return;
}

// Driver code
var N = 4;

var adj = [];

for(var i = 0; i <= N + 1; i++)
    adj.push(new Array());

addEdge(adj, 1, 2);
addEdge(adj, 2, 3);
addEdge(adj, 3, 4);

DFS(adj, N);

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(N+E)
T3】辅助空间: O(N)