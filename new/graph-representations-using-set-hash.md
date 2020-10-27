# 使用集合和哈希的图形表示

在[中，我们介绍了使用向量数组的 Graph 实现。 设置 1](https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-1-dfs-of-unweighted-and-undirected/) 。 在这篇文章中，使用了一种不同的实现，该实现可用于使用[集](https://www.geeksforgeeks.org/set-in-cpp-stl/)实现图。 该实现是针对图的[邻接表表示。](https://www.geeksforgeeks.org/graph-and-its-representations/)

集合在两个方面不同于向量：它以排序的方式存储元素，并且不允许重复的元素。 因此，该方法不能用于包含平行边的图形。 由于集合在内部实现为二进制搜索树，因此**可以在 O（logV）时间**中搜索两个顶点之间的边，其中 V 是图中顶点的数量。

以下是具有 5 个顶点的无向图和无权图的示例。
![8](img/1ef79a5320e6115e8c3ada572164793e.png)

以下是使用[集](https://www.geeksforgeeks.org/set-in-cpp-stl/)的数组的该图的邻接表表示。
![9](img/31ac6919c21cd0a1137f19937ea23758.png)

以下是使用集的无向图的邻接表表示的代码：

```
// A C++ program to demonstrate adjacency list
// representation of graphs using sets
#include <bits/stdc++.h>
using namespace std;
[
struct Graph {
int V;
set< int , greater< int > >* adjList;
};
// A utility function that creates a graph of V vertices
Graph* createGraph( int V)
{
Graph* graph = new Graph;
graph->V = V;
// Create an array of sets representing
// adjacency lists.  Size of the array will be V
graph->adjList = new set< int , greater< int > >[V];
return graph;
}
// Adds an edge to an undirected graph
void [HT G52] int src, int dest)
{
// Add an edge from src to dest.  A new
// element is inserted to the adjacent
// list of src.
graph->adjList[src].insert(dest);
// Since graph is undirected, add an edge
] // from dest to src also
graph->adjList[dest].insert(src);
}
// A utility function to print the adjacency
// list representation of graph
void printGraph(Graph* graph)
{
for ( int i = 0; i < graph->V; ++i) {
set< int , greater< int > > lst = graph->adjList[i];
cout << endl << "Adjacency list of vertex "
<< i << endl;
[
for ( auto itr = lst.begin(); itr != lst.end(); ++itr)
cout << *itr << " " ;
[          cout << endl;
}
}
// Searches for a given edge in the graph
void searchEdge(Graph* graph, int src, int dest)
{
auto itr = graph->adjList[src].find(dest);
if (itr == graph->adjList[src].end())
cout << endl << "Edge from " << src
<< " to " << dest << " not found."
<< endl;
else
cout << endl << "Edge from " << src
<< " to " << dest << " found."
<< endl;
}
// Driver code
int main()
{
// Create the graph given in the above figure
int [HT G160]
struct Graph* graph = createGraph(V);
addEdge(graph, 0, 1);
addEdge(graph, 0, 4);
addEdge(graph, 1, 2);
addEdge(graph, 1, 3);
addEdge(graph, 1, 4);
addEdge(graph, 2, 3);
addEdge(graph, 3, 4);
// Print the adjacency list representation of
// the above graph
printGraph(graph);
// Search the given edge in the graph
searchEdge(graph, 2, 1);
searchEdge(graph, 0, 3);
return 0;
}
```

输出：

```
Adjacency list of vertex 0
4 1

Adjacency list of vertex 1
4 3 2 0

Adjacency list of vertex 2
3 1

Adjacency list of vertex 3
4 2 1

Adjacency list of vertex 4
3 1 0

Edge from 2 to 1 found.

Edge from 0 to 3 not found.

```

*优点*：可以在 O（log V）中进行诸如从顶点 u 到顶点 v 是否存在边之类的查询。

*缺点*：

*   与矢量实现中的 O（1）相比，添加边需要 O（log V）。
*   包含平行边的图形无法通过此方法实现。

**使用 unordered_set（或散列）的边缘搜索操作的进一步优化**：
可以使用内部使用散列的 [unordered_set](https://www.geeksforgeeks.org/unorderd_set-stl-uses/) 将边缘搜索操作进一步优化为 O（1）。

```
// A C++ program to demonstrate adjacency list
// representation of graphs using sets
#include <bits/stdc++.h>
using namespace std;
[
struct Graph {
int V;
unordered_set< int >* adjList;
};
// A utility function that creates a graph of
// V vertices
Graph* createGraph( int V)
{
Graph* graph = new Graph;
graph->V = V;
// Create an array of sets representing
// adjacency lists. Size of the array will be V
graph->adjList = new unordered_set< int >[V];
return graph;
}
// Adds an edge to an undirected graph
void addEdge(Graph* graph, int src, int dest)
{
// Add an edge from src to dest. A new
// element is inserted to the adjacent
// list of src.
graph->adjList[src].insert(dest);
// Since graph is undirected, add an edge
// from dest to src also
graph->adjList[dest].insert(src);
}
// A utility function to print the adjacency
// list representation of graph
void printGraph(Graph* graph)
{
for ( int i = 0; i < graph->V; ++i) {
unordered_set< int > lst = graph->adjList[i];
cout << endl << "Adjacency list of vertex "
<< i << endl;
for ( auto itr = lst.begin(); itr != lst.end(); ++itr)
cout << *itr << " " ;
cout << endl;
[HTG10 3] }
}
// Searches for a given edge in the graph
void searchEdge(Graph* graph, int src, int dest)
{
auto itr = graph->adjList[src].find(dest);
if (itr == graph->adjList[src].end())
cout << endl << "Edge from " << src
<< " to " << dest << " not found."
<< endl;
else
cout << endl << "Edge from " << src
<< " to " << dest << " found."
<< endl;
}
// Driver code
int main()
]
{
// Create the graph given in the above figure
int V = 5;
struct Graph* graph = createGraph(V);
addEdge(graph, 0, 1);
addEdge(graph, 0, 4);
addEdge(graph, 1, 2);
addEdge(graph, 1, 3);
addEdge(graph, 1, 4);
addEdge(graph, 2, 3);
addEdge(graph, 3, 4);
// Print the adjacency list representation of
// the above graph
printGraph(graph);
// Search the given edge in the graph
searchEdge(graph, 2, 1);
searchEdge(graph, 0, 3);
return 0;
}
```

输出：

```
Adjacency list of vertex 0
4 1 

Adjacency list of vertex 1
4 3 2 0 

Adjacency list of vertex 2
3 1 

Adjacency list of vertex 3
4 2 1 

Adjacency list of vertex 4
3 1 0 

Edge from 2 to 1 found.

Edge from 0 to 3 not found.

```

*优点*：

*   可以在 O（1）中进行查询，例如是否存在从顶点 u 到顶点 v 的边。
*   加边需要 O（1）。

*缺点*：

*   包含平行边的图形无法通过此方法实现。
*   边缘不以任何顺序存储。

**注意**：**[邻接矩阵表示](https://www.geeksforgeeks.org/graph-and-its-representations/)** 对于边缘搜索是最优化的，但是对于大的稀疏图，邻接矩阵的空间要求相对较高。 此外，邻接矩阵还有其他缺点，例如 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 和 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 变得昂贵，因为我们无法快速获取节点的所有相邻节点。

本文由 [**vaibhav29498**](https://auth.geeksforgeeks.org/profile.php?user=vaibhav29498) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

