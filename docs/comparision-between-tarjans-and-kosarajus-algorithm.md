# 塔尔扬算法和小泽一郎算法的比较

> 原文:[https://www . geeksforgeeks . org/comparison-by-tarjans-and-kosarajus-algorithm/](https://www.geeksforgeeks.org/comparision-between-tarjans-and-kosarajus-algorithm/)

[**<u>塔尔扬算法</u>**](https://www.geeksforgeeks.org/tarjan-algorithm-find-strongly-connected-components/) **:** 塔尔扬算法是一种高效的图算法，用于在线性时间复杂度上仅使用一个 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)来寻找有向图中的 [**强连通分量**(**SCC**)](https://www.geeksforgeeks.org/strongly-connected-components/)。

**工作:**

*   Perform DFS traversal on nodes to remove subtrees of strongly connected components when they are encountered.
*   Then assign two values:
    *   The first value is the counter value when the node is first discovered.
    *   The second value stores the lowest reachable node value from the initial node, which is not a part of another **SCC** .
*   When nodes are explored, they are pushed into a [stack](https://www.geeksforgeeks.org/stack-data-structure/) .
*   If a node has unexplored child nodes, explore them and update the assignment separately.

下面是使用塔尔扬算法找到给定图形的 SCC 的程序:

## c++

```
// C++ program to find the SCC using
// Tarjan's algorithm (single DFS)
#include <iostream>
#include <list>
#include <stack>
#define NIL -1
using namespace std;

// A class that represents
// an directed graph
class Graph {
    // No. of vertices
    int V;

    // A dynamic array of adjacency lists
    list<int>* adj;

    // A Recursive DFS based function
    // used by SCC()
    void SCCUtil(int u, int disc[],
                 int low[], stack<int>* st,
                 bool stackMember[]);

public:
    // Member functions
    Graph(int V);
    void addEdge(int v, int w);
    void SCC();
};

// Constructor
Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}

// Function to add an edge to the graph
void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w);
}

// Recursive function to finds the SCC
// using DFS traversal
void Graph::SCCUtil(int u, int disc[],
                    int low[], stack<int>* st,
                    bool stackMember[])
{
    static int time = 0;

    // Initialize discovery time
    // and low value
    disc[u] = low[u] = ++time;
    st->push(u);
    stackMember[u] = true;

    // Go through all vertices
    // adjacent to this
    list<int>::iterator i;

    for (i = adj[u].begin();
         i != adj[u].end(); ++i) {
        // v is current adjacent of 'u'
        int v = *i;

        // If v is not visited yet,
        // then recur for it
        if (disc[v] == -1) {
            SCCUtil(v, disc, low,
                    st, stackMember);

            // Check if the subtree rooted
            // with 'v' has connection to
            // one of the ancestors of 'u'
            low[u] = min(low[u], low[v]);
        }

        // Update low value of 'u' only of
        // 'v' is still in stack
        else if (stackMember[v] == true)
            low[u] = min(low[u], disc[v]);
    }

    // head node found, pop the stack
    // and print an SCC

    // Store stack extracted vertices
    int w = 0;

    // If low[u] and disc[u]
    if (low[u] == disc[u]) {
        // Until stack st is empty
        while (st->top() != u) {
            w = (int)st->top();

            // Print the node
            cout << w << " ";
            stackMember[w] = false;
            st->pop();
        }
        w = (int)st->top();
        cout << w << "\n";
        stackMember[w] = false;
        st->pop();
    }
}

// Function to find the SCC in the graph
void Graph::SCC()
{
    // Stores the discovery times of
    // the nodes
    int* disc = new int[V];

    // Stores the nodes with least
    // discovery time
    int* low = new int[V];

    // Checks whether a node is in
    // the stack or not
    bool* stackMember = new bool[V];

    // Stores all the connected ancestors
    stack<int>* st = new stack<int>();

    // Initialize disc and low,
    // and stackMember arrays
    for (int i = 0; i < V; i++) {
        disc[i] = NIL;
        low[i] = NIL;
        stackMember[i] = false;
    }

    // Recursive helper function to
    // find the SCC in DFS tree with
    // vertex 'i'
    for (int i = 0; i < V; i++) {

        // If current node is not
        // yet visited
        if (disc[i] == NIL) {
            SCCUtil(i, disc, low,
                    st, stackMember);
        }
    }
}

// Driver Code
int main()
{
    // Given a graph
    Graph g1(5);
    g1.addEdge(1, 0);
    g1.addEdge(0, 2);
    g1.addEdge(2, 1);
    g1.addEdge(0, 3);
    g1.addEdge(3, 4);

    // Function Call to find SCC using
    // Tarjan's Algorithm
    g1.SCC();

    return 0;
}
```

**输出:**

```
4
3
1 2 0
```