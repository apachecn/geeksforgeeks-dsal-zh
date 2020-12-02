# 逐步打印 DFS 遍历（也回溯）

> 原文： [https://www.geeksforgeeks.org/print-the-dfs-traversal-step-wise-backtracking-also/](https://www.geeksforgeeks.org/print-the-dfs-traversal-step-wise-backtracking-also/)

给定[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，任务是打印图的 DFS 遍历，该图包括每个步骤，包括回溯。

![](img/77f2192443b4a705822ef0fe6af1f4bf.png)

```
1st step:- 0 -> 1
2nd step:- 1 -> 5
3rd step:- 5 -> 1 (backtracking step)
4th step:- 1 -> 6...
and so on till all the nodes are visited.

Dfs step-wise(including backtracking) is:
0 1 5 1 6 7 8 7 6 1 0 2 4 2 9 3 10

```

**注意**：刚刚在上图中添加了边缘之间的权重，它在 DFS 遍历中没有任何作用。

![](img/2d27ed151c265904449bc33d2524394b.png)

**方法：此处将使用** [DFS](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 和[回溯](http://www.geeksforgeeks.org/backtracking-algorithms/)。 首先，使用 DFS 同时访问每个节点，并跟踪先前使用的边缘和父节点。 如果某个节点的所有相邻节点都已被访问过，则使用上次使用的边缘回溯并打印该节点。 继续执行步骤，在每一步，父节点将成为当前节点。 继续上述步骤，找到图形的完整 DFS 遍历。

下面是上述方法的实现：

## C++

```cpp

// C++ program to print the complete
// DFS-traversal of graph
// using back-tracking
#include <bits/stdc++.h>
using namespace std;
const int N = 1000;
vector<int> adj[N];

// Function to print the complete DFS-traversal
void dfsUtil(int u, int node, bool visited[],
             vector<pair<int, int> > road_used, int parent, int it)
{
    int c = 0;

    // Check if all th node is visited or not
    // and count unvisited nodes
    for (int i = 0; i < node; i++)
        if (visited[i])
            c++;

    // If all the node is visited return;
    if (c == node)
        return;

    // Mark not visited node as visited
    visited[u] = true;

    // Track the current edge
    road_used.push_back({ parent, u });

    // Print the node
    cout << u << " ";

    // Check for not visited node and proceed with it.
    for (int x : adj[u]) {

        // call the DFs function if not visited
        if (!visited[x])
            dfsUtil(x, node, visited, road_used, u, it + 1);
    }

    // Backtrack through the last
    // visited nodes
    for (auto y : road_used)
        if (y.second == u)
            dfsUtil(y.first, node, visited,
                    road_used, u, it + 1);
}

// Function to call the DFS function
// which prints the DFS-travesal stepwise
void dfs(int node)
{

    // Create a array of visited ndoe
    bool visited[node];

    // Vector to track last visited road
    vector<pair<int, int> > road_used;

    // Initialize all the node with false
    for (int i = 0; i < node; i++)
        visited[i] = false;

    // call the function
    dfsUtil(0, node, visited, road_used, -1, 0);
}

// Function to insert edges in Graph
void insertEdge(int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Driver Code
int main()
{
    // number of nodes and edges in the graph
    int node = 11, edge = 13;

    // Function call to create the graph
    insertEdge(0, 1);
    insertEdge(0, 2);
    insertEdge(1, 5);
    insertEdge(1, 6);
    insertEdge(2, 4);
    insertEdge(2, 9);
    insertEdge(6, 7);
    insertEdge(6, 8);
    insertEdge(7, 8);
    insertEdge(2, 3);
    insertEdge(3, 9);
    insertEdge(3, 10);
    insertEdge(9, 10);

    // Call the function to print
    dfs(node);

    return 0;
}

```

## Python3

```

# Python3 program to print the 
# complete DFS-traversal of graph
# using back-tracking
N = 1000
adj = [[] for i in range(N)]

# Function to prthe complete DFS-traversal
def dfsUtil(u, node,visited, 
            road_used, parent, it):
    c = 0

    # Check if all th node is visited 
    # or not and count unvisited nodes
    for i in range(node):
        if (visited[i]):
            c += 1

    # If all the node is visited return
    if (c == node):
        return

    # Mark not visited node as visited
    visited[u] = True

    # Track the current edge
    road_used.append([parent, u])

    # Print the node
    print(u, end = " ")

    # Check for not visited node
    # and proceed with it.
    for x in adj[u]:

        # Call the DFs function 
        # if not visited
        if (not visited[x]):
            dfsUtil(x, node, visited, 
                    road_used, u, it + 1)

    # Backtrack through the last
    # visited nodes
    for y in road_used:
        if (y[1] == u):
            dfsUtil(y[0], node, visited,
                    road_used, u, it + 1)

# Function to call the DFS function
# which prints the DFS-travesal stepwise
def dfs(node):

    # Create a array of visited ndoe
    visited = [False for i in range(node)]

    # Vector to track last visited road
    road_used = []

    # Initialize all the node with false
    for i in range(node):
        visited[i] = False

    # Call the function
    dfsUtil(0, node, visited, 
            road_used, -1, 0)

# Function to insert edges in Graph
def insertEdge(u, v):

    adj[u].append(v)
    adj[v].append(u)

# Driver Code
if __name__ == '__main__':

    # Number of nodes and edges in the graph
    node = 11
    edge = 13

    # Function call to create the graph
    insertEdge(0, 1)
    insertEdge(0, 2)
    insertEdge(1, 5)
    insertEdge(1, 6)
    insertEdge(2, 4)
    insertEdge(2, 9)
    insertEdge(6, 7)
    insertEdge(6, 8)
    insertEdge(7, 8)
    insertEdge(2, 3)
    insertEdge(3, 9)
    insertEdge(3, 10)
    insertEdge(9, 10)

    # Call the function to print
    dfs(node)

# This code is contributed by mohit kumar 29

```

**Output:** 

```
0 1 5 1 6 7 8 7 6 1 0 2 4 2 9 3 10

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。