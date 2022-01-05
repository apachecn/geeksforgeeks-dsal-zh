# 在 STL 中使用优先级队列的 Prim 算法

> 原文:[https://www . geesforgeks . org/prims-algorithm-use-priority _ queue-STL/](https://www.geeksforgeeks.org/prims-algorithm-using-priority_queue-stl/)

给定一个无向图、连通图和加权图，用 Prim 算法求图的最小生成树。

```
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

我们已经在下面讨论了 Prim 的 MST 实现。

*   [Prim 的邻接矩阵表示算法(在时间复杂度为 O 的 C/C++中)( v <sup>2</sup> )](https://www.geeksforgeeks.org/greedy-algorithms-set-5-prims-minimum-spanning-tree-mst-2/)
*   [用于邻接表表示的 Prim 算法(在时间复杂度为 O(ELogV)的 C 中)](https://www.geeksforgeeks.org/greedy-algorithms-set-5-prims-mst-for-adjacency-list-representation/)

第二个实现在时间复杂度方面更好，但是非常复杂，因为我们已经实现了自己的优先级队列。STL 提供[优先级 _ 队列](http://geeksquiz.com/priority-queue-container-adaptors-the-c-standard-template-library-stl/)，但提供的优先级队列不支持减键操作。在 Prim 的算法中，我们需要一个[优先级队列](http://geeksquiz.com/binary-heap/)以及以下对优先级队列的操作:

*   ExtractMin:从所有那些还没有包含在 MST 中的顶点中，我们需要得到具有最小键值的顶点。
*   减少关键点:提取顶点后，我们需要更新其相邻顶点的关键点，如果新的关键点较小，则在数据结构中更新该关键点。

这里讨论的算法可以修改，这样就不需要递减键了。其思想是，不要将所有顶点都插入优先级队列，而只插入那些不是 MST 的顶点，并且已经通过包含在 MST 中的顶点被访问过的顶点。我们在 MST[]中的一个单独的布尔数组中跟踪包含在 MST 中的顶点。

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
   In Dijkstra's algorithm, we didn't need this array as
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

下面是上述思想的 C++实现。

## C++

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
    // its key as 0.
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

          //Different key values for same vertex may exist in the priority queue.
          //The one with the least key value is always processed first.
          //Therefore, ignore the rest.
          if(inMST[u] == true){
            continue;
        }

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

时间复杂度:O(E Log V))

**使用加权图的向量数组表示的更快实现**[](https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-2-weighted-graph/)****:****

## **C++**

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
    // its key as 0.
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

          //Different key values for same vertex may exist in the priority queue.
          //The one with the least key value is always processed first.
          //Therefore, ignore the rest.
          if(inMST[u] == true){
            continue;
        }

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

**注意:像 [Dijkstra 的 priority_queue 实现](https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-using-priority_queue-stl/)一样，我们可能对同一个顶点有多个条目，因为在 if 条件下我们没有(也不能)使 isMST[v] = true。**

## **C++**

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

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// If v is not in MST and weight of (u,v) is smaller
// than current key of v

if (inMST[v] == false && key[v] > weight)
{

  // Updating key of v
  key[v] = weight;
  pq.add(new Pair<Integer, Integer>(key[v], v));
  parent[v] = u;
}

// This code is contributed by avanitrachhadiya2155
```

## **蟒蛇 3**

```
# If v is not in MST and weight of (u,v) is smaller
# than current key of v

if (inMST[v] == False and key[v] > weight) :

  # Updating key of v
  key[v] = weight
  pq.append([key[v], v])
  parent[v] = u

  # This code is contributed by divyeshrabadiya07.
```

## **C#**

```
// If v is not in MST and weight of (u,v) is smaller
// than current key of v

if (inMST[v] == false && key[v] > weight)
{
  // Updating key of v
  key[v] = weight;
  pq.Add(new Tuple<int,int>(key[v], v));
  parent[v] = u;
}

// This code is contributed by divyesh072019.
```

## **java 描述语言**

```
<script>

// If v is not in MST and weight of (u,v)
// is smaller than current key of v
if (inMST[v] == false && key[v] > weight)
{

    // Updating key of v
    key[v] = weight;
    value = [key[v], v];
    pq.push(value);
    parent[v] = u;
}

// This code is contributed by suresh07

</script>
```

**但是正如迪杰斯特拉算法中所解释的，时间复杂度仍然是 0(E Log V)，因为在优先级队列中最多有 O(E)个顶点，并且 O(Log E)与 O(Log V)相同。**

**与 Dijkstra 的实现不同，布尔数组 inMST[]在这里是必需的，因为新插入的项的键值可以小于提取的项的键值。所以一定不要考虑提取的项目。**

**本文由 **Shubham Agrawal** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息**