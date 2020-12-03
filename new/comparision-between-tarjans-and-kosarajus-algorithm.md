# Tarjan 算法和 Kosaraju 算法

的比较

> 原文： [https://www.geeksforgeeks.org/comparision-between-tarjans-and-kosarajus-algorithm/](https://www.geeksforgeeks.org/comparision-between-tarjans-and-kosarajus-algorithm/)

[**<u>Tarjan 算法</u>**](https://www.geeksforgeeks.org/tarjan-algorithm-find-strongly-connected-components/) ****：Tarjan 算法是一种有效的图形算法，可用于查找 [**强连接的组件 通过使用线性时间复杂度中仅使用一个**](https://www.geeksforgeeks.org/strongly-connected-components/) **[DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)的有向图中的** （ **SCC** ）。

**工作**：

*   在节点上执行 DFS 遍历，以便在遇到强连接组件的子树时将其删除。

*   然后分配两个值：

    *   第一个值是第一次浏览节点时的计数器值。

    *   第二值存储从初始节点可到达的最低节点值，该节点不是另一个 **SCC** 的一部分。

*   探索节点时，将它们压入[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)中。

*   如果有节点的任何未开发子节点，则对其进行探索，并分别更新分配的值。

下面是使用 Tarjan 算法查找给定图形的 SCC 的程序：

## C++

```cpp

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

**Output:**

```
4
3
1 2 0

```

[**<u>Kosaraju 的算法</u>**](https://www.geeksforgeeks.org/strongly-connected-components/) ****：Kosaraju 的算法也是[深度优先搜索](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) 基于算法 用于在线性时间复杂度的有向图中找到 **SCC** 。 该算法的基本概念是，如果我们能够最初从顶点`u`开始到达顶点`v`，那么我们应该能够到达顶点`u`]从顶点`v`，开始，如果是这种情况，我们可以说并得出结论，`u`和`v`的顶点是紧密相连的 ，它们位于紧密相连的子图中。

**工作**：

*   在给定的图形上执行 DFS 遍历，并跟踪每个节点的完成时间。 可以通过使用[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)来执行此过程。

*   当在图形上运行 DFS 遍历的过程完成时，将源顶点放在堆栈上。 这样，完成时间最高的节点将位于堆栈的顶部。

*   [通过使用](https://www.geeksforgeeks.org/transpose-graph/)[邻接表](https://www.geeksforgeeks.org/graph-and-its-representations/)反转原始图。

*   然后在反向图上执行另一个 DFS 遍历，将源顶点作为堆栈顶部的顶点。 当在反转图上运行的 DFS 完成时，所有被访问的节点将形成一个紧密连接的组件。

*   如果剩余任何节点或不访问任何节点，则表示图中存在多个强连接的组件。

*   因此，从堆栈顶部弹出顶点，直到找到有效的未访问节点。 在所有当前未访问的节点中，这将具有最高的完成时间。

下面是使用 Kosaraju 的算法查找给定图形的 SCC 的程序：

## C++

```cpp

// C++ program to print the SCC of the 
// graph using Kosaraju's Algorithm 
#include <iostream> 
#include <list> 
#include <stack> 
using namespace std; 

class Graph { 
    // No. of vertices 
    int V; 

    // An array of adjacency lists 
    list<int>* adj; 

    // Member Functions 
    void fillOrder(int v, bool visited[], 
                   stack<int>& Stack); 
    void DFSUtil(int v, bool visited[]); 

public: 
    Graph(int V); 
    void addEdge(int v, int w); 
    void printSCCs(); 
    Graph getTranspose(); 
}; 

// Constructor of class 
Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 

// Recursive function to print DFS 
// starting from v 
void Graph::DFSUtil(int v, bool visited[]) 
{ 
    // Mark the current node as 
    // visited and print it 
    visited[v] = true; 
    cout << v << " "; 

    // Recur for all the vertices 
    // adjacent to this vertex 
    list<int>::iterator i; 

    // Traverse Adjacency List of node v 
    for (i = adj[v].begin(); 
         i != adj[v].end(); ++i) { 

        // If child node *i is unvisited 
        if (!visited[*i]) 
            DFSUtil(*i, visited); 
    } 
} 

// Function to get the transpose of 
// the given graph 
Graph Graph::getTranspose() 
{ 
    Graph g(V); 
    for (int v = 0; v < V; v++) { 
        // Recur for all the vertices 
        // adjacent to this vertex 
        list<int>::iterator i; 
        for (i = adj[v].begin(); 
             i != adj[v].end(); ++i) { 
            // Add to adjacency list 
            g.adj[*i].push_back(v); 
        } 
    } 

    // Return the reversed graph 
    return g; 
} 

// Function to add an Edge to the given 
// graph 
void Graph::addEdge(int v, int w) 
{ 
    // Add w to v’s list 
    adj[v].push_back(w); 
} 

// Function that fills stack with vertices 
// in increasing order of finishing times 
void Graph::fillOrder(int v, bool visited[], 
                      stack<int>& Stack) 
{ 
    // Mark the current node as 
    // visited and print it 
    visited[v] = true; 

    // Recur for all the vertices 
    // adjacent to this vertex 
    list<int>::iterator i; 

    for (i = adj[v].begin(); 
         i != adj[v].end(); ++i) { 

        // If child node *i is unvisited 
        if (!visited[*i]) { 
            fillOrder(*i, visited, Stack); 
        } 
    } 

    // All vertices reachable from v 
    // are processed by now, push v 
    Stack.push(v); 
} 

// Function that finds and prints all 
// strongly connected components 
void Graph::printSCCs() 
{ 
    stack<int> Stack; 

    // Mark all the vertices as 
    // not visited (For first DFS) 
    bool* visited = new bool[V]; 
    for (int i = 0; i < V; i++) 
        visited[i] = false; 

    // Fill vertices in stack according 
    // to their finishing times 
    for (int i = 0; i < V; i++) 
        if (visited[i] == false) 
            fillOrder(i, visited, Stack); 

    // Create a reversed graph 
    Graph gr = getTranspose(); 

    // Mark all the vertices as not 
    // visited (For second DFS) 
    for (int i = 0; i < V; i++) 
        visited[i] = false; 

    // Now process all vertices in 
    // order defined by Stack 
    while (Stack.empty() == false) { 

        // Pop a vertex from stack 
        int v = Stack.top(); 
        Stack.pop(); 

        // Print SCC of the popped vertex 
        if (visited[v] == false) { 
            gr.DFSUtil(v, visited); 
            cout << endl; 
        } 
    } 
} 

// Driver Code 
int main() 
{ 
    // Given Graph 
    Graph g(5); 
    g.addEdge(1, 0); 
    g.addEdge(0, 2); 
    g.addEdge(2, 1); 
    g.addEdge(0, 3); 
    g.addEdge(3, 4); 

    // Function Call to find the SCC 
    // using Kosaraju's Algorithm 
    g.printSCCs(); 

    return 0; 
} 

```

**Output:**

```
0 1 2 
3 
4

```

**<u>时间复杂度</u>**：

Tarjan 算法和 Kosaraju 算法的时间复杂度为 **O（V + E）**，其中`V`表示一组顶点，`E`表示图形的边集。 Tarjan 的算法的常数因子比 Kosaraju 的算法低得多。 在 Kosaraju 的算法中，图形的[遍历至少 2 次，因此常数因子可以是两倍。 在执行第二个 DFS 时，我们可以使用 Kosaraju 的算法打印正在进行的 **SCC** 。 在执行 Tarjan 算法时，找到 **SCC** 子树的头后，需要花费更多时间来打印 **SCC** 。](https://www.geeksforgeeks.org/algorithms-gq/graph-traversals-gq/)

**<u>总结</u>**：

两种方法具有相同的线性时间复杂度，但是 **SCC** 计算的技术或过程完全不同。 Tarjan 的方法仅取决于 **DFS** 中的节点记录来对图进行分区，而 Kosaraju 的方法在图上执行两个 DFS（如果要保持原始图不变，则执行 3 DFS），并且非常相似 查找图的拓扑排序的方法。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。