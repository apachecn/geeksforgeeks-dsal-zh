# Prim 的算法使用 STL

中的 priority_queue

> 原文： [https://www.geeksforgeeks.org/prims-algorithm-using-priority_queue-stl/](https://www.geeksforgeeks.org/prims-algorithm-using-priority_queue-stl/)

给定一个无向，连通和加权的图，请使用 Prim 的算法查找该图的最小生成树（MST）。

```
![](img/576b7bbdf820c1b3c849c6d34f16d7b4.png "Fig-1")

Input : Adjacency List representation
        of above graph
Output :  Edges in MST
          0 - 1
          1 - 2
          2 - 3
          3 - 4
          2 - 5
          5 - 6
          6 - 7
          2 - 8

Note :  There are two possible MSTs, the other
        MST includes edge 0-7 in place of 1-2\. 

```

我们在下面讨论了 Prim 的 MST 实现。

*   [Prim 的邻接矩阵表示算法（在 C / C ++中，时间复杂度为 O（v <sup>2</sup> ）](https://www.geeksforgeeks.org/greedy-algorithms-set-5-prims-minimum-spanning-tree-mst-2/)

*   [Prim 的邻接表表示算法（在 C 中，时间复杂度为 O（ELogV））](https://www.geeksforgeeks.org/greedy-algorithms-set-5-prims-mst-for-adjacency-list-representation/)

第二种实现方式是时间复杂度更好，但是由于我们已经实现了自己的优先级队列，因此实现起来确实很复杂。 STL 提供 [priority_queue](http://geeksquiz.com/priority-queue-container-adaptors-the-c-standard-template-library-stl/) ，但提供的优先级队列不支持减小键操作。 在 Prim 的算法中，我们需要[优先级队列](http://geeksquiz.com/binary-heap/)及以下对优先级队列的操作：

*   ExtractMin：从尚未包含在 MST 中的所有那些顶点中，我们需要获得具有最小键值的顶点。

*   DecreaseKey：提取顶点后，我们需要更新其相邻顶点的关键点，如果新关键点较小，则在数据结构中进行更新。

此处讨论的算法 [](https://www.geeksforgeeks.org/greedy-algorithms-set-5-prims-mst-for-adjacency-list-representation/) 可以修改，这样就不再需要减小密钥。 这样做的想法是，不将所有顶点插入优先级队列中，而仅插入那些不是 MST 且已通过 MST 中包含的顶点进行访问的顶点。 我们在 MST []中的单独布尔数组中跟踪 MST 中包含的顶点。

```
1) Initialize keys of all vertices as infinite and 
   parent of every vertex as -1.

2) Create an empty priority_queue pq.  Every item
   of pq is a pair (weight, vertex). Weight (or 
   key) is used used as first item  of pair
   as first item is by default used to compare
   two pairs.

3) Initialize all vertices as not part of MST yet.
   We use boolean array inMST[] for this purpose.
   This array is required to make sure that an already
   considered vertex is not included in pq again. This
   is where Ptim's implementation differs from Dijkstra.
   In Dijkstr's algorithm, we didn't need this array as
   distances always increase. We require this array here 
   because key value of a processed vertex may decrease
   if not checked.

4) Insert source vertex into pq and make its key as 0.

5) While either pq doesn't become empty 
    a) Extract minimum key vertex from pq. 
       Let the extracted vertex be u.

    b) Include u in MST using inMST[u] = true.

    c) Loop through all adjacent of u and do 
       following for every vertex v.

           // If weight of edge (u,v) is smaller than
           // key of v and v is not already in MST
           If inMST[v] = false && key[v] > weight(u, v)

               (i) Update key of v, i.e., do
                     key[v] = weight(u, v)
               (ii) Insert v into the pq 
               (iv) parent[v] = u

6) Print MST edges using parent array.

```

以下是上述想法的 C ++实现。

```

// STL implementation of Prim's algorithm for MST 
#include<bits/stdc++.h> 
using namespace std; 
# define INF 0x3f3f3f3f 

// iPair ==>  Integer Pair 
typedef pair<int, int> iPair; 

// This class represents a directed graph using 
// adjacency list representation 
class Graph 
{ 
    int V;    // No. of vertices 

    // In a weighted graph, we need to store vertex 
    // and weight pair for every edge 
    list< pair<int, int> > *adj; 

public: 
    Graph(int V);  // Constructor 

    // function to add an edge to graph 
    void addEdge(int u, int v, int w); 

    // Print MST using Prim's algorithm 
    void primMST(); 
}; 

// Allocates memory for adjacency list 
Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list<iPair> [V]; 
} 

void Graph::addEdge(int u, int v, int w) 
{ 
    adj[u].push_back(make_pair(v, w)); 
    adj[v].push_back(make_pair(u, w)); 
} 

// Prints shortest paths from src to all other vertices 
void Graph::primMST() 
{ 
    // Create a priority queue to store vertices that 
    // are being preinMST. This is weird syntax in C++. 
    // Refer below link for details of this syntax 
    // http://geeksquiz.com/implement-min-heap-using-stl/ 
    priority_queue< iPair, vector <iPair> , greater<iPair> > pq; 

    int src = 0; // Taking vertex 0 as source 

    // Create a vector for keys and initialize all 
    // keys as infinite (INF) 
    vector<int> key(V, INF); 

    // To store parent array which in turn store MST 
    vector<int> parent(V, -1); 

    // To keep track of vertices included in MST 
    vector<bool> inMST(V, false); 

    // Insert source itself in priority queue and initialize 
    // its key as 0\. 
    pq.push(make_pair(0, src)); 
    key[src] = 0; 

    /* Looping till priority queue becomes empty */
    while (!pq.empty()) 
    { 
        // The first vertex in pair is the minimum key 
        // vertex, extract it from priority queue. 
        // vertex label is stored in second of pair (it 
        // has to be done this way to keep the vertices 
        // sorted key (key must be first item 
        // in pair) 
        int u = pq.top().second; 
        pq.pop(); 

        inMST[u] = true;  // Include vertex in MST 

        // 'i' is used to get all adjacent vertices of a vertex 
        list< pair<int, int> >::iterator i; 
        for (i = adj[u].begin(); i != adj[u].end(); ++i) 
        { 
            // Get vertex label and weight of current adjacent 
            // of u. 
            int v = (*i).first; 
            int weight = (*i).second; 

            //  If v is not in MST and weight of (u,v) is smaller 
            // than current key of v 
            if (inMST[v] == false && key[v] > weight) 
            { 
                // Updating key of v 
                key[v] = weight; 
                pq.push(make_pair(key[v], v)); 
                parent[v] = u; 
            } 
        } 
    } 

    // Print edges of MST using parent array 
    for (int i = 1; i < V; ++i) 
        printf("%d - %d\n", parent[i], i); 
} 

// Driver program to test methods of graph class 
int main() 
{ 
    // create the graph given in above fugure 
    int V = 9; 
    Graph g(V); 

    //  making above shown graph 
    g.addEdge(0, 1, 4); 
    g.addEdge(0, 7, 8); 
    g.addEdge(1, 2, 8); 
    g.addEdge(1, 7, 11); 
    g.addEdge(2, 3, 7); 
    g.addEdge(2, 8, 2); 
    g.addEdge(2, 5, 4); 
    g.addEdge(3, 4, 9); 
    g.addEdge(3, 5, 14); 
    g.addEdge(4, 5, 10); 
    g.addEdge(5, 6, 2); 
    g.addEdge(6, 7, 1); 
    g.addEdge(6, 8, 6); 
    g.addEdge(7, 8, 7); 

    g.primMST(); 

    return 0; 
} 

```

时间复杂度：O（E Log V））

**使用权重图**：的矢量表示的[向量数组的更快实现](https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-2-weighted-graph/)

```

// STL implementation of Prim's algorithm for MST 
#include<bits/stdc++.h> 
using namespace std; 
# define INF 0x3f3f3f3f 

// iPair ==> Integer Pair 
typedef pair<int, int> iPair; 

// To add an edge 
void addEdge(vector <pair<int, int> > adj[], int u, 
                                     int v, int wt) 
{ 
    adj[u].push_back(make_pair(v, wt)); 
    adj[v].push_back(make_pair(u, wt)); 
} 

// Prints shortest paths from src to all other vertices 
void primMST(vector<pair<int,int> > adj[], int V) 
{ 
    // Create a priority queue to store vertices that 
    // are being preinMST. This is weird syntax in C++. 
    // Refer below link for details of this syntax 
    // http://geeksquiz.com/implement-min-heap-using-stl/ 
    priority_queue< iPair, vector <iPair> , greater<iPair> > pq; 

    int src = 0; // Taking vertex 0 as source 

    // Create a vector for keys and initialize all 
    // keys as infinite (INF) 
    vector<int> key(V, INF); 

    // To store parent array which in turn store MST 
    vector<int> parent(V, -1); 

    // To keep track of vertices included in MST 
    vector<bool> inMST(V, false); 

    // Insert source itself in priority queue and initialize 
    // its key as 0\. 
    pq.push(make_pair(0, src)); 
    key[src] = 0; 

    /* Looping till priority queue becomes empty */
    while (!pq.empty()) 
    { 
        // The first vertex in pair is the minimum key 
        // vertex, extract it from priority queue. 
        // vertex label is stored in second of pair (it 
        // has to be done this way to keep the vertices 
        // sorted key (key must be first item 
        // in pair) 
        int u = pq.top().second; 
        pq.pop(); 

        inMST[u] = true; // Include vertex in MST 

        // Traverse all adjacent of u 
        for (auto x : adj[u]) 
        { 
            // Get vertex label and weight of current adjacent 
            // of u. 
            int v = x.first; 
            int weight = x.second; 

            // If v is not in MST and weight of (u,v) is smaller 
            // than current key of v 
            if (inMST[v] == false && key[v] > weight) 
            { 
                // Updating key of v 
                key[v] = weight; 
                pq.push(make_pair(key[v], v)); 
                parent[v] = u; 
            } 
        } 
    } 

    // Print edges of MST using parent array 
    for (int i = 1; i < V; ++i) 
        printf("%d - %d\n", parent[i], i); 
} 

// Driver program to test methods of graph class 
int main() 
{ 
    int V = 9; 
    vector<iPair > adj[V]; 

    // making above shown graph 
    addEdge(adj, 0, 1, 4); 
    addEdge(adj, 0, 7, 8); 
    addEdge(adj, 1, 2, 8); 
    addEdge(adj, 1, 7, 11); 
    addEdge(adj, 2, 3, 7); 
    addEdge(adj, 2, 8, 2); 
    addEdge(adj, 2, 5, 4); 
    addEdge(adj, 3, 4, 9); 
    addEdge(adj, 3, 5, 14); 
    addEdge(adj, 4, 5, 10); 
    addEdge(adj, 5, 6, 2); 
    addEdge(adj, 6, 7, 1); 
    addEdge(adj, 6, 8, 6); 
    addEdge(adj, 7, 8, 7); 

    primMST(adj, V); 

    return 0; 
} 

```

注意：像 [Dijkstra 的 priority_queue 实现](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-priority_queue-stl/)一样，我们可能在同一个顶点上有多个条目，因为在 if 条件下我们不（也不能）使 isMST [v] = true。

```

// If v is not in MST and weight of (u,v) is smaller 
 // than current key of v 
 if (inMST[v] == false && key[v] > weight) 
 { 
      // Updating key of v 
      key[v] = weight; 
      pq.push(make_pair(key[v], v)); 
      parent[v] = u; 
} 

```

但正如 Dijkstra 算法所解释的那样，时间复杂度仍为 O（E Log V），因为优先级队列中最多会有 O（E）个顶点，并且 O（Log E）与 O（Log V）相同。

与 Dijkstra 的实现不同，此处必须使用 inMST []布尔数组，因为新插入的项的键值可以小于提取的项的键值。 因此，我们绝不能考虑提取的项目。

本文由 **Shubham Agrawal** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

