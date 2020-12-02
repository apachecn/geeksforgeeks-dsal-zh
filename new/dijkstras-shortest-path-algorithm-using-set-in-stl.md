# Dijkstra 使用 STL 中设置的最短路径算法

> 原文： [https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-set-in-stl/](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-set-in-stl/)

给定一个图和图中的一个源顶点，找到从源到给定图中所有顶点的最短路径。

```
![](img/576b7bbdf820c1b3c849c6d34f16d7b4.png "Fig-1")

Input : Source = 0
Output : 
     Vertex   Distance from Source
        0                0
        1                4
        2                12
        3                19
        4                21
        5                11
        6                9
        7                8
        8                14
```

我们已经讨论了 Dijkstra 最短 Path 的实现。

*   [Dijkstra 的邻接矩阵表示算法（在 C / C ++中，时间复杂度为 O（v <sup>2</sup> ）](https://www.geeksforgeeks.org/greedy-algorithms-set-6-dijkstras-shortest-path-algorithm/)
*   [Dijkstra 的邻接表表示算法（在 C 中，时间复杂度为 O（ELogV））](https://www.geeksforgeeks.org/greedy-algorithms-set-7-dijkstras-algorithm-for-adjacency-list-representation/)

第二种实现方式是时间复杂度更好，但是由于我们已经实现了自己的优先级队列，因此实现起来确实很复杂。 STL 提供 [priority_queue](http://geeksquiz.com/priority-queue-container-adaptors-the-c-standard-template-library-stl/) ，但提供的优先级队列不支持减少键和删除操作。 在 Dijkstra 的算法中，我们需要一个优先级队列，以及下面对优先级队列的操作：

*   ExtractMin：从尚未找到最短距离的所有那些顶点中，我们需要获得具有最小距离的顶点。
*   DecreaseKey：提取顶点后，我们需要更新其相邻顶点的距离，如果新距离较小，则在数据结构中更新该距离。

以上操作可以通过 c ++ STL 的 [set 数据结构轻松实现，set 将其所有键按排序顺序保留，因此最小距离顶点将始终在开始处，我们可以从那里提取它，这是 ExtractMin 操作 如果任何顶点的距离变小，则更新相应的其他相邻顶点，然后删除其先前的条目并插入新的更新条目，即 DecreaseKey 操作。](http://geeksquiz.com/set-associative-containers-the-c-standard-template-library-stl/)

下面是基于集合数据结构的算法。

```
1) Initialize distances of all vertices as infinite.

2) Create an empty set.  Every item of set is a pair
  (weight, vertex). Weight (or distance) is used used
  as first item  of pair as first item is by default 
  used to compare two pairs.

3) Insert source vertex into the set and make its
   distance as 0.

4) While Set doesn't become empty, do following
    a) Extract minimum distance vertex from Set. 
       Let the extracted vertex be u.
    b) Loop through all adjacent of u and do 
       following for every vertex v.

           // If there is a shorter path to v
           // through u. 
           If dist[v] > dist[u] + weight(u, v)

               (i) Update distance of v, i.e., do
                     dist[v] = dist[u] + weight(u, v)
               (i) If v is in set, update its distance
                   in set by removing it first, then
                   inserting with new distance
               (ii) If v is not in set, then insert
                    it in set with new distance

5) Print distance array dist[] to print all shortest
   paths. 
```

以下是上述想法的 C ++实现。

```

// Program to find Dijkstra's shortest path using STL set 
#include<bits/stdc++.h> 
using namespace std; 
# define INF 0x3f3f3f3f 

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

    // prints shortest path from s 
    void shortestPath(int s); 
}; 

// Allocates memory for adjacency list 
Graph::Graph(int V) 
{ 
    this->V = V; 
    adj = new list< pair<int, int> >[V]; 
} 

void Graph::addEdge(int u, int v, int w) 
{ 
    adj[u].push_back(make_pair(v, w)); 
    adj[v].push_back(make_pair(u, w)); 
} 

// Prints shortest paths from src to all other vertices 
void Graph::shortestPath(int src) 
{ 
    // Create a set to store vertices that are being 
    // prerocessed 
    set< pair<int, int> > setds; 

    // Create a vector for distances and initialize all 
    // distances as infinite (INF) 
    vector<int> dist(V, INF); 

    // Insert source itself in Set and initialize its 
    // distance as 0\. 
    setds.insert(make_pair(0, src)); 
    dist[src] = 0; 

    /* Looping till all shortest distance are finalized 
       then setds will become empty */
    while (!setds.empty()) 
    { 
        // The first vertex in Set is the minimum distance 
        // vertex, extract it from set. 
        pair<int, int> tmp = *(setds.begin()); 
        setds.erase(setds.begin()); 

        // vertex label is stored in second of pair (it 
        // has to be done this way to keep the vertices 
        // sorted distance (distance must be first item 
        // in pair) 
        int u = tmp.second; 

        // 'i' is used to get all adjacent vertices of a vertex 
        list< pair<int, int> >::iterator i; 
        for (i = adj[u].begin(); i != adj[u].end(); ++i) 
        { 
            // Get vertex label and weight of current adjacent 
            // of u. 
            int v = (*i).first; 
            int weight = (*i).second; 

            //  If there is shorter path to v through u. 
            if (dist[v] > dist[u] + weight) 
            { 
                /*  If distance of v is not INF then it must be in 
                    our set, so removing it and inserting again 
                    with updated less distance.   
                    Note : We extract only those vertices from Set 
                    for which distance is finalized. So for them,  
                    we would never reach here.  */
                if (dist[v] != INF) 
                    setds.erase(setds.find(make_pair(dist[v], v))); 

                // Updating distance of v 
                dist[v] = dist[u] + weight; 
                setds.insert(make_pair(dist[v], v)); 
            } 
        } 
    } 

    // Print shortest distances stored in dist[] 
    printf("Vertex   Distance from Source\n"); 
    for (int i = 0; i < V; ++i) 
        printf("%d \t\t %d\n", i, dist[i]); 
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

    g.shortestPath(0); 

    return 0; 
} 

```

输出：

```
Vertex   Distance from Source
0 		 0
1 		 4
2 		 12
3 		 19
4 		 21
5 		 11
6 		 9
7 		 8
8 		 14

```

时间复杂度：C ++中的设置通常使用自平衡二进制搜索树来实现。 因此，设置操作（如插入，删除）的时间复杂度为对数，而上述解决方案的时间复杂度为 O（ELogV））。
 **[Dijkstra 使用 STL 的 priority_queue 的最短路径算法](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-priority_queue-stl/)** 
本文由 [Utkarsh Trivedi](http://qa.geeksforgeeks.org/user/utkarsh111) 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

