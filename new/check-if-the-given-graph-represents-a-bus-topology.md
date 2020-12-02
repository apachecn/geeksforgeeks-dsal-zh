# 检查给定的图形是否表示总线拓扑

> 原文： [https://www.geeksforgeeks.org/check-if-the-given-graph-represents-a-bus-topology/](https://www.geeksforgeeks.org/check-if-the-given-graph-represents-a-bus-topology/)

给定图形 **G** ，检查其是否表示总线拓扑。

下图显示了一种总线拓扑：
![](img/dcba898b8132ead7bd204436a3a4e787.png)

**示例：**

```
Input: 

Output:  YES

Input: 

Output:  NO

```

如果满足以下两个条件，则 V 顶点的图形表示总线拓扑：

1.  除陈述末尾结点外，每个结点的度数均为 2，而起点和结点的结点为度数 1。
2.  边数=顶点数– 1。

想法是遍历图并检查它是否满足以上两个条件。 如果是，则表示总线拓扑。

下面是上述方法的实现：

## CPP

```

// CPP program to check if the given graph 
// represents a bus topology 
#include <bits/stdc++.h> 
using namespace std; 

// A utility function to add an edge in an 
// undirected graph. 
void addEdge(vector<int> adj[], int u, int v) 
{ 
    adj[u].push_back(v); 
    adj[v].push_back(u); 
} 

// A utility function to print the adjacency list 
// representation of graph 
void printGraph(vector<int> adj[], int V) 
{ 
    for (int v = 0; v < V; ++v) { 
        cout << "\n Adjacency list of vertex "
             << v << "\n head "; 
        for (auto x : adj[v]) 
            cout << "-> " << x; 
        printf("\n"); 
    } 
} 

/* Function to return true if the graph represented 
   by the adjacency list represents a bus topology 
   else return false */
bool checkBusTopologyUtil(vector<int> adj[], int V, int E) 
{ 

    // Number of edges should be equal 
    // to (Number of vertices - 1) 
    if (E != (V - 1)) 
        return false; 

    // a single node is termed as a bus topology 
    if (V == 1) 
        return true; 

    int* vertexDegree = new int[V + 1]; 
    memset(vertexDegree, 0, sizeof vertexDegree); 

    // calculate the degree of each vertex 
    for (int i = 1; i <= V; i++) { 
        for (auto v : adj[i]) { 
            vertexDegree[v]++; 
        } 
    } 

    // countDegree2 - number of vertices with degree 2 
    // countDegree1 - number of vertices with degree 1 
    int countDegree2 = 0, countDegree1 = 0; 
    for (int i = 1; i <= V; i++) { 
        if (vertexDegree[i] == 2) { 
            countDegree2++; 
        } 
        else if (vertexDegree[i] == 1) { 
            countDegree1++; 
        } 
        else { 
            // if any node has degree other 
            // than 1 or 2, it is 
            // NOT a bus topology 
            return false; 
        } 
    } 

    // if both necessary conditions as discussed, 
    // satisfy return true 
    if (countDegree1 == 2 && countDegree2 == (V - 2)) { 
        return true; 
    } 
    return false; 
} 

// Function to check if the graph represents a bus topology 
void checkBusTopology(vector<int> adj[], int V, int E) 
{ 
    bool isBus = checkBusTopologyUtil(adj, V, E); 
    if (isBus) { 
        cout << "YES" << endl; 
    } 
    else { 
        cout << "NO" << endl; 
    } 
} 

// Driver code 
int main() 
{ 
    // Graph 1 
    int V = 5, E = 4; 
    vector<int> adj1[V + 1]; 
    addEdge(adj1, 1, 2); 
    addEdge(adj1, 1, 3); 
    addEdge(adj1, 3, 4); 
    addEdge(adj1, 4, 5); 
    checkBusTopology(adj1, V, E); 

    // Graph 2 
    V = 4, E = 4; 
    vector<int> adj2[V + 1]; 
    addEdge(adj2, 1, 2); 
    addEdge(adj2, 1, 3); 
    addEdge(adj2, 3, 4); 
    addEdge(adj2, 4, 2); 
    checkBusTopology(adj2, V, E); 

    return 0; 
} 

```