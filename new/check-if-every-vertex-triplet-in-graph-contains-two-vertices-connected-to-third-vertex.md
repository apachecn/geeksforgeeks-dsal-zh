# 检查图形中的每个顶点三元组是否包含连接到第三个顶点的两个顶点

> 原文： [https://www.geeksforgeeks.org/check-if-every-vertex-triplet-in-graph-contains-two-vertices-connected-to-third-vertex/](https://www.geeksforgeeks.org/check-if-every-vertex-triplet-in-graph-contains-two-vertices-connected-to-third-vertex/)

给定[无向图](https://www.geeksforgeeks.org/detect-cycle-undirected-graph/)，其中 **N** 个顶点且 **K** 个边，任务是检查图中三个顶点的每个组合是否存在两个顶点，其中 连接到第三顶点。 换句话说，对于每个顶点三元组**（a，b，c）**，如果在 **a** 和 **c** 之间存在一条路径，那么也应该存在一个 **b** 和 **c** 之间的路径。

**示例：**

> **输入：** N = 4，K = 3
> 边沿：1-> 2，2-> 3，3-> 4
> [ **输出：**是
> **说明：**
> 由于连接了整个图形，因此上述条件始终有效。
> 
> **输入：** N = 5，K = 3
> 边：1-> 3，3-> 4，2-> 5\.
> **输出：**否
> **解释：**
> 如果我们考虑三元组（1、2、3），则顶点 1 和 3 之间有一条路径，但顶点 2 和 3 之间没有任何路径。

**方法：**请按照以下步骤解决问题–

*   [通过](https://www.geeksforgeeks.org/algorithms-gq/graph-traversals-gq/) [DFS 遍历技术](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)从任何组件遍历图形，并维护两个变量以存储组件最小值和组件最大值。
*   将每个分量的最大值和最小值存储在向量中。
*   现在，如果任意两个分量的最小值和最大值间隔中都有一个交集，则将存在一个有效的（a

 **下面是上述方法的实现

## C ++

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

## 爪哇

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

## Python3

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

**Output:** 

```
Yes

```

**时间复杂度：** O（N + E）
**辅助空间：** O（N）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。**