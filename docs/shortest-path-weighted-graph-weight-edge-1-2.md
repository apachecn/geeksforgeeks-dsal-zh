# 边的权重为 1 或 2 的加权图中的最短路径

> 原文:[https://www . geesforgeks . org/最短路径-加权-图-权重-边-1-2/](https://www.geeksforgeeks.org/shortest-path-weighted-graph-weight-edge-1-2/)

给定一个有向图，其中每条边的权重为 1 或 2，找到从给定源顶点到给定目标顶点的最短路径。预期时间复杂度为 O(V+E)。
一个**简单的解决方案**就是使用[迪克斯特拉的最短路径算法](https://www.geeksforgeeks.org/greedy-algorithms-set-7-dijkstras-algorithm-for-adjacency-list-representation/)，我们可以在 O(E + VLogV)时间内得到一条最短路径。

**O(v+ E)时间如何做？**思路是用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 。关于 BFS 的一个重要观察是，BFS 使用的路径在任意两个顶点之间的边数总是最少的。所以如果所有边的权重相同，我们可以用 BFS 来寻找最短路径。对于这个问题，我们可以修改图，将权重 2 的所有边分成权重 1 的两条边。在修改后的图中，我们可以使用 BFS 来寻找最短路径。

**需要多少个新的中间顶点？**我们需要为每个源顶点添加一个新的中间顶点。原因很简单，如果我们在 u 和 v 之间添加一个中间顶点 x，如果我们在 y 和 z 之间添加同一个顶点，那么新的路径 u 到 z 和 y 到 v 被添加到图中，这可能在原始图中已经注意到了。因此，在有 V 个顶点的图中，我们需要 V 个额外的顶点。

下面是上述思想的 C++实现。在下面的实现中，在图中创建了 2*V 个顶点，对于每条边(u，V)，我们将它分成两条边(u，u+V)和(u+V，w)。这样，我们确保为每个源顶点添加不同的中间顶点。

## C/C++

```
// Program to shortest path from a given source vertex ‘s’ to
// a given destination vertex ‘t’.  Expected time complexity
// is O(V+E).
#include<bits/stdc++.h>
using namespace std;

// This class represents a directed graph using adjacency
// list representation
class Graph
{
    int V;    // No. of vertices
    list<int> *adj;    // adjacency lists
public:
    Graph(int V);  // Constructor
    void addEdge(int v, int w, int weight); // adds an edge

    // finds shortest path from source vertex ‘s’ to
    // destination vertex ‘d’.
    int findShortestPath(int s, int d);

    // print shortest path from a source vertex ‘s’ to
    // destination vertex ‘d’.
    int printShortestPath(int parent[], int s, int d);
};

Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[2*V];
}

void Graph::addEdge(int v, int w, int weight)
{
    // split all edges of weight 2 into two
    // edges of weight 1 each.  The intermediate
    // vertex number is maximum vertex number + 1,
    // that is V.
    if (weight==2)
    {
        adj[v].push_back(v+V);
        adj[v+V].push_back(w);
    }
    else // Weight is 1
        adj[v].push_back(w); // Add w to v’s list.
}

// To print the shortest path stored in parent[]
int Graph::printShortestPath(int parent[], int s, int d)
{
    static int level = 0;

    // If we reached root of shortest path tree
    if (parent[s] == -1)
    {
        cout << "Shortest Path between " << s << " and "
             << d << " is "  << s << " ";
        return level;
    }

    printShortestPath(parent, parent[s], d);

    level++;
    if (s < V)
        cout << s << " ";

    return level;
}

// This function mainly does BFS and prints the
// shortest path from src to dest. It is assumed
// that weight of every edge is 1
int Graph::findShortestPath(int src, int dest)
{
    // Mark all the vertices as not visited
    bool *visited = new bool[2*V];
    int *parent = new int[2*V];

    // Initialize parent[] and visited[]
    for (int i = 0; i < 2*V; i++)
    {
        visited[i] = false;
        parent[i] = -1;
    }

    // Create a queue for BFS
    list<int> queue;

    // Mark the current node as visited and enqueue it
    visited[src] = true;
    queue.push_back(src);

    // 'i' will be used to get all adjacent vertices of a vertex
    list<int>::iterator i;

    while (!queue.empty())
    {
        // Dequeue a vertex from queue and print it
        int s = queue.front();

        if (s == dest)
            return printShortestPath(parent, s, dest);

        queue.pop_front();

        // Get all adjacent vertices of the dequeued vertex s
        // If a adjacent has not been visited, then mark it
        // visited and enqueue it
        for (i = adj[s].begin(); i != adj[s].end(); ++i)
        {
            if (!visited[*i])
            {
                visited[*i] = true;
                queue.push_back(*i);
                parent[*i] = s;
            }
        }
    }
}

// Driver program to test methods of graph class
int main()
{
    // Create a graph given in the above diagram
    int V = 4;
    Graph g(V);
    g.addEdge(0, 1, 2);
    g.addEdge(0, 2, 2);
    g.addEdge(1, 2, 1);
    g.addEdge(1, 3, 1);
    g.addEdge(2, 0, 1);
    g.addEdge(2, 3, 2);
    g.addEdge(3, 3, 2);

    int src = 0, dest = 3;
    cout << "\nShortest Distance between " << src
         << " and " << dest << " is "
         << g.findShortestPath(src, dest);

    return 0;
}
```