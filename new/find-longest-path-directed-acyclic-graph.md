# 有向无环图

中的最长路径

> 原文： [https://www.geeksforgeeks.org/find-longest-path-directed-acyclic-graph/](https://www.geeksforgeeks.org/find-longest-path-directed-acyclic-graph/)

给定一个加权的`D`关联的**一个**循环`G`raph（DAG）及其源顶点 s，在其中找到从 s 到所有其他顶点的最长距离。 给定图。

一般图的最长路径问题不像最短路径问题那么容易，因为最长路径问题没有[最佳子结构属性](https://www.geeksforgeeks.org/dynamic-programming-set-2-optimal-substructure-property/)。 实际上，[最长路径问题是一般图形](http://en.wikipedia.org/wiki/Longest_path_problem)的 NP-Hard。 但是，最长路径问题对于有向无环图具有线性时间解。 这个想法类似于[线性时间解，用于有向无环图中的最短路径。](https://www.geeksforgeeks.org/shortest-path-for-directed-acyclic-graphs/) ，我们使用[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)。

我们将到所有顶点的距离初始化为负无穷大，到源的距离初始化为 0，然后找到图的[拓扑排序](https://www.geeksforgeeks.org/topological-sorting/)。 图的拓扑排序表示图的线性排序（请参见下文，图（b）是图（a）的线性表示）。 一旦我们有了拓扑顺序（或线性表示），我们便按拓扑顺序逐一处理所有顶点。 对于每个要处理的顶点，我们使用当前顶点的距离来更新其相邻的距离。

下图显示了寻找最长路径的分步过程。

![LongestPath](img/5436e86149d255fbbf9b3dd661ae97b2.png)

以下是找到最长距离的完整算法。

**1）**初始化 dist [] = {NINF，NINF，…。}，并且 dist [s] = 0，其中 s 是源顶点。 这里的 NINF 表示负无穷大。

**2）**创建所有顶点的拓扑顺序。

**3）**按照拓扑顺序对每个顶点 u 进行跟踪。

…...对 u 的每个相邻顶点 v 执行以下操作

………………if（dist [v] < dist [u] + weight（u，v））

…………………………dist [v] = dist [u] +权重（u，v）

以下是上述算法的 C ++实现。

```

// A C++ program to find single source longest distances 
// in a DAG 
#include <iostream> 
#include <limits.h> 
#include <list> 
#include <stack> 
#define NINF INT_MIN 
using namespace std; 

// Graph is represented using adjacency list. Every  
// node of adjacency list contains vertex number of  
// the vertex to which edge connects. It also  
// contains weight of the edge  
class AdjListNode {  
    int v;  
    int weight;  

public:  
    AdjListNode(int _v, int _w)  
    {  
        v = _v;  
        weight = _w;  
    }  
    int getV() { return v; }  
    int getWeight() { return weight; }  
};  

// Class to represent a graph using adjacency list  
// representation  
class Graph {  
    int V; // No. of vertices'  

    // Pointer to an array containing adjacency lists  
    list<AdjListNode>* adj;  

    // A function used by longestPath  
    void topologicalSortUtil(int v, bool visited[],  
                             stack<int>& Stack);  

public:  
    Graph(int V); // Constructor  
    ~Graph(); // Destructor 

    // function to add an edge to graph  
    void addEdge(int u, int v, int weight);  

    // Finds longest distances from given source vertex  
    void longestPath(int s);  
};  

Graph::Graph(int V) // Constructor  
{  
    this->V = V;  
    adj = new list<AdjListNode>[V];  
}  

Graph::~Graph() // Destructor  
{  
    delete [] adj;  
}  

void Graph::addEdge(int u, int v, int weight)  
{  
    AdjListNode node(v, weight);  
    adj[u].push_back(node); // Add v to u's list  
}  

// A recursive function used by longestPath. See below  
// link for details  
// https:// www.geeksforgeeks.org/topological-sorting/  
void Graph::topologicalSortUtil(int v, bool visited[],  
                                stack<int>& Stack)  
{  
    // Mark the current node as visited  
    visited[v] = true;  

    // Recur for all the vertices adjacent to this vertex  
    list<AdjListNode>::iterator i;  
    for (i = adj[v].begin(); i != adj[v].end(); ++i) {  
        AdjListNode node = *i;  
        if (!visited[node.getV()])  
            topologicalSortUtil(node.getV(), visited, Stack);  
    }  

    // Push current vertex to stack which stores topological  
    // sort  
    Stack.push(v);  
}  

// The function to find longest distances from a given vertex.  
// It uses recursive topologicalSortUtil() to get topological  
// sorting.  
void Graph::longestPath(int s)  
{  
    stack<int> Stack;  
    int dist[V];  

    // Mark all the vertices as not visited  
    bool* visited = new bool[V];  
    for (int i = 0; i < V; i++)  
        visited[i] = false;  

    // Call the recursive helper function to store Topological  
    // Sort starting from all vertices one by one  
    for (int i = 0; i < V; i++)  
        if (visited[i] == false)  
            topologicalSortUtil(i, visited, Stack);  

    // Initialize distances to all vertices as infinite and  
    // distance to source as 0  
    for (int i = 0; i < V; i++)  
        dist[i] = NINF;  
    dist[s] = 0;  

    // Process vertices in topological order  
    while (Stack.empty() == false) {  
        // Get the next vertex from topological order  
        int u = Stack.top();  
        Stack.pop();  

        // Update distances of all adjacent vertices  
        list<AdjListNode>::iterator i;  
        if (dist[u] != NINF) {  
            for (i = adj[u].begin(); i != adj[u].end(); ++i)  
                if (dist[i->getV()] < dist[u] + i->getWeight())  
                    dist[i->getV()] = dist[u] + i->getWeight();  
        }  
    }  

    // Print the calculated longest distances  
    for (int i = 0; i < V; i++)  
        (dist[i] == NINF) ? cout << "INF " : cout << dist[i] << " "; 

    delete [] visited; 
}  

// Driver program to test above functions  
int main()  
{  
    // Create a graph given in the above diagram.  
    // Here vertex numbers are 0, 1, 2, 3, 4, 5 with  
    // following mappings:  
    // 0=r, 1=s, 2=t, 3=x, 4=y, 5=z  
    Graph g(6);  
    g.addEdge(0, 1, 5);  
    g.addEdge(0, 2, 3);  
    g.addEdge(1, 3, 6);  
    g.addEdge(1, 2, 2);  
    g.addEdge(2, 4, 4);  
    g.addEdge(2, 5, 2);  
    g.addEdge(2, 3, 7);  
    g.addEdge(3, 5, 1);  
    g.addEdge(3, 4, -1);  
    g.addEdge(4, 5, -2);  

    int s = 1;  
    cout << "Following are longest distances from "
            "source vertex "
         << s << " \n";  
    g.longestPath(s);  

    return 0;  
} 

```

输出：

```
Following are longest distances from source vertex 1
INF 0 2 9 8 10
```

**时间复杂度**：拓扑排序的时间复杂度为 O（V + E）。 找到拓扑顺序后，该算法将处理所有顶点，并且对于每个顶点，它将为所有相邻顶点运行一个循环。 图中的相邻顶点总数为 O（E）。 因此，内部循环运行 O（V + E）次。 因此，该算法的总时间复杂度为 O（V + E）。

**练习**：上述解决方案可以打印最长距离，也可以将代码扩展到打印路径。

Micro Focus

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

