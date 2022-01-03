# 词典最小的拓扑顺序

> 原文： [https://www.geeksforgeeks.org/lexicographically-smallest-topological-ordering/](https://www.geeksforgeeks.org/lexicographically-smallest-topological-ordering/)

给定一个有向图，该图的`N`个顶点和`M`的边可能包含循环，任务是找到该图在字典上最小的拓扑顺序，否则将打印`-1`（如果图形具有循环）。

从语法上最小的拓扑顺序是指，如果图形中的两个顶点没有任何传入边，则编号较小的顶点应在该顺序中首先出现。

例如，在下面的图像中，许多拓扑排序都是可能的，例如 **5 2 3 4 0 1，5 0 2 4 3 1** 。

但最小的顺序是 **4 5 0 2 3 1** 。

**示例**：

> **输入**：
> ![](img/f5310c221503609e7aaf34f0f690639b.png)
> **输出**：4 5 0 2 3 1
> 即使 5 4 0 2 3 1 也是有效的拓扑
> 给定图的排序，但在字典上不是
> 最小。

**方法**：我们将使用 [Kahn 的算法](https://www.geeksforgeeks.org/topological-sorting-indegree-based-solution/)对拓扑进行修改。 我们将使用[多集](http://www.geeksforgeeks.org/multiset-in-cpp-stl/)而不是使用队列来存储顶点，以确保每次选择顶点时，顶点都是最小的。 总时间复杂度更改为![O(VlogV+E)](img/b4b6ba30aec1344806ba640ad8cbf85d.png "Rendered by QuickLaTeX.com")

下面是上述方法的实现：

```

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Class to represent a graph 
class Graph { 
    int V; // No. of vertices' 

    // Pointer to an array containing 
    // adjacency listsList 
    list<int>* adj; 

public: 
    Graph(int V); // Constructor 

    // Function to add an edge to graph 
    void addEdge(int u, int v); 

    // Function to print the required topological 
    // sort of the given graph 
    void topologicalSort(); 
}; 

// Constructor 
Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<int>[V]; 
} 

// Function to add an edge to the graph 
void Graph::addEdge(int u, int v) 
{ 
    adj[u].push_back(v); 
} 

// Function to print the required topological 
// sort of the given graph 
void Graph::topologicalSort() 
{ 
    // Create a vector to store indegrees of all 
    // the vertices 
    // Initialize all indegrees to 0 
    vector<int> in_degree(V, 0); 

    // Traverse adjacency lists to fill indegrees of 
    // vertices 
    // This step takes O(V+E) time 
    for (int u = 0; u < V; u++) { 
        list<int>::iterator itr; 
        for (itr = adj[u].begin(); itr != adj[u].end(); itr++) 
            in_degree[*itr]++; 
    } 

    // Create a set and inserting all vertices with 
    // indegree 0 
    multiset<int> s; 
    for (int i = 0; i < V; i++) 
        if (in_degree[i] == 0) 
            s.insert(i); 

    // Initialize count of visited vertices 
    int cnt = 0; 

    // Create a vector to store result (A topological 
    // ordering of the vertices) 
    vector<int> top_order; 

    // One by one erase vertices from setand insert 
    // adjacents if indegree of adjacent becomes 0 
    while (!s.empty()) { 

        // Extract vertex with minimum number from multiset 
        // and add it to topological order 
        int u = *s.begin(); 
        s.erase(s.begin()); 
        top_order.push_back(u); 

        // Iterate through all its neighbouring nodes 
        // of erased node u and decrease their in-degree 
        // by 1 
        list<int>::iterator itr; 
        for (itr = adj[u].begin(); itr != adj[u].end(); itr++) 

            // If in-degree becomes zero, add it to queue 
            if (--in_degree[*itr] == 0) 
                s.insert(*itr); 

        cnt++; 
    } 

    // Check if there was a cycle 
    if (cnt != V) { 
        cout << -1; 
        return; 
    } 

    // Print topological order 
    for (int i = 0; i < top_order.size(); i++) 
        cout << top_order[i] << " "; 
} 

// Driver code 
int main() 
{ 
    // Create the graph 
    Graph g(6); 
    g.addEdge(5, 2); 
    g.addEdge(5, 0); 
    g.addEdge(4, 0); 
    g.addEdge(4, 1); 
    g.addEdge(2, 3); 
    g.addEdge(3, 1); 

    // Find the required topological order 
    g.topologicalSort(); 

    return 0; 
} 

```

**Output:**

```
4 5 0 2 3 1

```

![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。