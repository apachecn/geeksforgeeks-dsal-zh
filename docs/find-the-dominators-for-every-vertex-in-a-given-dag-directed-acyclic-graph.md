# 找出给定 DAG(有向无环图)中每个顶点的支配者

> 原文:[https://www . geesforgeks . org/find-给定 dag 有向无环图中每个顶点的支配者/](https://www.geeksforgeeks.org/find-the-dominators-for-every-vertex-in-a-given-dag-directed-acyclic-graph/)

给定一个具有 **V** 顶点和 **E** 边的[有向无环图](https://en.wikipedia.org/wiki/Directed_acyclic_graph)，任务是找到图的每个顶点的支配顶点集。

> **什么是图论中的支配者:**
> 在[控制流图中](https://www.geeksforgeeks.org/control-flow-software-testing/)一个顶点 **V1** 是另一个顶点 **V2** 的支配者，如果从源顶点(本例中为顶点‘0’)到顶点 **V2** 的所有路径都经过 **V1** 。根据定义，每个顶点都是自己的支配者之一。

**示例:**

> ***输入:** V = 5，E = 5，adj[][] = {{0，1}，{0，2}，{1，3}，{2，3}，{3， 4}}*
> ***输出:***
> *支配集顶点:0–>0*
> *支配集顶点:1–>0 1*
> *支配集顶点:2–>0 2*
> T19】支配集顶点:3–>0 3
> 支配集顶点:4 \
> *1 2*
> *\/*
> *3*
> *|*
> *4*
> *这里的 0 是入口节点，所以它的支配者本身就是 0。*
> *在(0，1)之间只存在一条路径，所以 1 的支配者是 0，1。*
> *在(0，2)之间只存在一条路径，所以 2 的支配者是 0，2。*
> *在只有 0，3 的(0，3)之间有两条路径是相同的。*
> *从(0，4)开始有 2 条路径(0 1 3 4)和(0 2 3 4)具有 0，3 和 4 的共性。*
> 
> ***输入:** V = 4，E = 3，adj[][] = {{0，1}，{0，2}，{3，2}}*
> ***输出:***
> *支配集顶点:0–>0*
> *支配集顶点:1–>0 1*
> T16】支配集顶点:2–>0 2T11

**方法:**想法是执行 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 并维护一组每个顶点的所有支配者。按照以下步骤解决问题:

*   初始化[位集](https://www.geeksforgeeks.org/c-bitset-and-its-application/)数据结构的一个向量，比如 **b** 来存储顶点的所有支配者的集合。
*   对于每个节点 **i** ，在**b【I】**中设置的位将代表 **i.** 的支配顶点集
*   为了找到每个顶点的支配者，找到[有向无环图](https://en.wikipedia.org/wiki/Directed_acyclic_graph)中的所有路径是很重要的。
*   使用 [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 到[遍历图形，找到图形中的所有路径](https://www.geeksforgeeks.org/find-paths-given-source-destination/)。
*   从[根节点](https://www.geeksforgeeks.org/find-distance-root-given-node-binary-tree/)开始遍历，即 **0**
*   执行 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 时，对于每个顶点 **i**
    *   [如果节点尚未被访问](https://www.geeksforgeeks.org/find-all-reachable-nodes-from-every-node-present-in-a-given-set/)，设置**b【I】**的所有位，并标记被访问的节点
    *   将位集 **b[i]** 中的主导顶点集存储为其父顶点集的[交集](https://www.geeksforgeeks.org/intersection-function-python/)。将 **b[i]** 更新为 **b[i] & b【母公司】**。
    *   将 **b[i][i]** 的值更新为 **1** ，因为每个节点都是自己的支配者。
    *   [递归](https://www.geeksforgeeks.org/recursion/)，对 **i** 的子节点调用 **DFS** 。
*   执行上述步骤后，打印顶点的主顶点，即**b【I】**中设置位的[位置。](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Declare bitsets for each
// vertex to store the set of
// dominant vertices
vector<bitset<100> > b(100);

// Visited array to check if
// a vertex has been visited or not
int vis[100] = {};

// Function to find set of dominator
// vertices for a particular node
void findDominator(vector<vector<int> > graph,
                   bitset<100> par, int node)
{
    // If node is unvisited
    if (vis[node] == 0) {
        // Set all bits of b[pos]
        b[node] = ~b[node];

        // Update vis[node] to 1
        vis[node] = 1;
    }

    // Update b[node] with bitwise and
    // of parent's dominant vertices
    b[node] &= par;

    // Node is itself is a
    // dominant vertex of node
    b[node][node] = 1;

    // Traverse the neighbours of node
    for (int i = 0; i < (int)graph[node].size(); i++) {

        // Recursive function call to
        //  children nodes of node
        findDominator(graph, b[node], graph[node][i]);
    }
}

// Function to build the graph
void buildGraph(vector<pair<int, int> > adj, int E, int V)
{
    // Vector of vector to store
    // the adjancy matrix
    vector<vector<int> > graph(V + 1);

    // Build the adjacency matrix
    for (int i = 0; i < E; i++) {
        graph[adj[i].first].push_back(adj[i].second);
    }

    // Bitset for node 0
    bitset<100> g;

    // Node 0 itself is a dominant
    // vertex of itself
    g[0] = 1;

    // Update visited of source
    // node as true
    vis[0] = 1;

    // DFS from source vertex
    findDominator(graph, g, 0);
}

// Function to find dominant set of vertices
void dominantVertices(int V, int E,
                      vector<pair<int, int> > adj)
{
    // Function call to build the graph
    // and dominant vertices
    buildGraph(adj, E, V);

    // Print set of dominating vertices
    for (int i = 0; i < V; i++) {
        cout << i << " -> ";
        for (int j = 0; j < V; j++) {
            if (b[i][j] == 1)
                cout << j << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    // Given Input
    int V = 5, E = 5;
    vector<pair<int, int> > adj = {
        { 0, 1 }, { 0, 2 }, { 1, 3 }, { 2, 3 }, { 3, 4 }
    };

    // Function Call
    dominantVertices(V, E, adj);

    return 0;
}
```

**Output**

```
0 -> 0 
1 -> 0 1 
2 -> 0 2 
3 -> 0 3 
4 -> 0 3 4 
```

***时间复杂度:**O(V<sup>3</sup>)*
***辅助空间:** O(V <sup>2</sup> )*