# 使用 DFS 的图的两个顶点之间的最小边数

> 原文： [https://www.geeksforgeeks.org/minimum-number-of-edges-between-two-vertices-of-a-graph-using-dfs/](https://www.geeksforgeeks.org/minimum-number-of-edges-between-two-vertices-of-a-graph-using-dfs/)

给定无向图 **G（V，E）**，其中`N`个顶点，`M`边。 我们需要找到给定顶点对**（u，v）**之间的最小边数。
我们已经使用 [BFS 方法](https://www.geeksforgeeks.org/minimum-number-of-edges-between-two-vertices-of-a-graph/)讨论了这个问题，这里我们将使用 DFS 方法。

**示例**：

> **输入**：对于以下给定的图，找到顶点对（0，4）之间的最小边数。
> 
> ![](img/6f66b6e4cb161a70fac008a69a34cb48.png)
> 
> **输出**：1
> 从 0 到 4 共有 3 条路径：
> 0-> 1-> 2-> 4
> 0-> 1- > 2-> 3-> 4
> 0-> 4
> 只有第三条路径才能使边的数量最少。

**方法**：在这种方法中，我们将以 [DFS](http://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 的方式遍历图形，从给定顶点开始，探索从该顶点到目标顶点的所有路径。

我们将使用两个变量， **edge_count** 和 **min_num_of_edges** 。 在探索这些顶点之间的所有路径时， **edge_count** 将存储其中的边总数，如果边数小于最小边数，我们将更新 **min_num_of_edges** 。

下面是上述方法的实现：

## C ++

```

// C++ program to find minimum
// number of edges between any two
// vertices of the graph

#include <bits/stdc++.h>
using namespace std;

// Class to represent a graph
class Graph {

    // No. of vertices
    int V;

    // Pointer to an array containing
    // adjacency lists
    list<int>* adj;

    // A function used by minEdgeDFS
    void minEdgeDFSUtil(vector<bool>& visited,
                        int src, int des, int& min_num_of_edges,
                        int& edge_count);

public:
    // Constructor
    Graph(int V);

    // Function to add an edge to graph
    void addEdge(int src, int des);

    // Prints the minimum number of edges
    void minEdgeDFS(int u, int v);
};

Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}

void Graph::addEdge(int src, int des)
{
    adj[src].push_back(des);
    adj[des].push_back(src);
}

// Utility function for finding minimum number
// of edges using DFS
void Graph::minEdgeDFSUtil(vector<bool>& visited,
                           int src, int des, int& min_num_of_edges,
                           int& edge_count)
{
    // For keeping track of visited
    // nodes in DFS
    visited[src] = true;

    // If we have found the destination vertex
    // then check whether count of total number of edges
    // is less than the minimum number of edges or not
    if (src == des) {
        if (min_num_of_edges > edge_count)
            min_num_of_edges = edge_count;
    }

    // If current vertex is not destination
    else {

        // Recur for all the vertices
        // adjacent to current vertex
        list<int>::iterator i;

        for (i = adj[src].begin(); i != adj[src].end(); i++) {
            int v = *i;

            if (!visited[v]) {
                edge_count++;

                minEdgeDFSUtil(visited, v, des, min_num_of_edges,
                               edge_count);
            }
        }
    }

    // Decrement the count of number of edges
    // and mark current vertex as unvisited
    visited[src] = false;
    edge_count--;
}

// Function to print minimum number of edges
// It uses recursive minEdgeDFSUtil
void Graph::minEdgeDFS(int u, int v)
{
    // To keep track of all the
    // visited vertices
    vector<bool> visited(V, false);

    // To store minimum number of edges
    int min_num_of_edges = INT_MAX;

    // To store total number of
    // edges in each path
    int edge_count = 0;

    minEdgeDFSUtil(visited, u, v, min_num_of_edges,
                   edge_count);

    // Print the minimum number of edges
    cout << min_num_of_edges;
}

// Driver Code
int main()
{
    // Create a graph
    Graph g(5);
    g.addEdge(0, 1);
    g.addEdge(0, 4);
    g.addEdge(1, 2);
    g.addEdge(2, 4);
    g.addEdge(2, 3);
    g.addEdge(3, 4);

    int u = 0;
    int v = 3;
    g.minEdgeDFS(u, v);

    return 0;
}

```

## 爪哇

```

// Java program to find minimum 
// number of edges between any two 
// vertices of the graph 
import java.io.*;
import java.util.*;

class GFG 
{

    static int min_num_of_edges = 0, edge_count = 0;

    // Class to represent a graph
    static class Graph
    {

        // No. of vertices
        int V;

        // Pointer to an array containing
        // adjacency lists
        Vector<Integer>[] adj;

        // A function used by minEdgeDFS

        // Utility function for finding minimum number
        // of edges using DFS
        private void minEdgeDFSUtil(boolean[] visited, 
                                    int src, int des) 
        {

            // For keeping track of visited
            // nodes in DFS
            visited[src] = true;

            // If we have found the destination vertex
            // then check whether count of total number of edges
            // is less than the minimum number of edges or not
            if (src == des)
            {
                if (min_num_of_edges > edge_count)
                    min_num_of_edges = edge_count;
            }

            // If current vertex is not destination
            else
            {
                for (int i : adj[src]) 
                {
                    int v = i;

                    if (!visited[v]) 
                    {
                        edge_count++;
                        minEdgeDFSUtil(visited, v, des);
                    }
                }
            }

            // Decrement the count of number of edges
            // and mark current vertex as unvisited
            visited[src] = false;
            edge_count--;
        }

        // Constructor
        @SuppressWarnings("unchecked")
        Graph(int V) {
            this.V = V;
            adj = new Vector[V];

            for (int i = 0; i < V; i++)
                adj[i] = new Vector<>();
        }

        // Function to add an edge to graph
        void addEdge(int src, int des) 
        {
            adj[src].add(des);
            adj[des].add(src);
        }

        // Function to print minimum number of edges
        // It uses recursive minEdgeDFSUtil
        void minEdgeDFS(int u, int v)
        {

            // To keep track of all the
            // visited vertices
            boolean[] visited = new boolean[this.V];
            Arrays.fill(visited, false);

            // To store minimum number of edges
            min_num_of_edges = Integer.MAX_VALUE;

            // To store total number of
            // edges in each path
            edge_count = 0;

            minEdgeDFSUtil(visited, u, v);

            // Print the minimum number of edges
            System.out.println(min_num_of_edges);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Create a graph
        Graph g = new Graph(5);
        g.addEdge(0, 1);
        g.addEdge(0, 4);
        g.addEdge(1, 2);
        g.addEdge(2, 4);
        g.addEdge(2, 3);
        g.addEdge(3, 4);

        int u = 0;
        int v = 3;
        g.minEdgeDFS(u, v);
    }
}

// This code is contributed by
// sanjeev2552

```

## Python3

```

# Python3 program to find minimum 
# number of edges between any two 
# vertices of the graph 

# Class to represent a graph 
class Graph:  

    def __init__(self, V):
        self.V = V
        self.adj = [[] for i in range(V)]

    def addEdge(self, src, des): 

        self.adj[src].append(des) 
        self.adj[des].append(src) 

    # Utility function for finding 
    # minimum number of edges using DFS 
    def minEdgeDFSUtil(self, visited, src, des, min_num_of_edges, edge_count): 

        # For keeping track of visited nodes in DFS 
        visited[src] = True

        # If we have found the destination vertex 
        # then check whether count of total number of edges 
        # is less than the minimum number of edges or not 
        if src == des: 
            if min_num_of_edges > edge_count: 
                min_num_of_edges = edge_count 

        # If current vertex is not destination 
        else:  

            # Recur for all the vertices 
            # adjacent to current vertex 
            for v in self.adj[src]:  

                if not visited[v]:  
                    edge_count += 1

                    min_num_of_edges, edge_count = \
                    self.minEdgeDFSUtil(visited, v, des, min_num_of_edges, edge_count) 

        # Decrement the count of number of edges 
        # and mark current vertex as unvisited 
        visited[src] = False
        edge_count -= 1
        return min_num_of_edges, edge_count

    # Function to print minimum number of 
    # edges. It uses recursive minEdgeDFSUtil 
    def minEdgeDFS(self, u, v): 

        # To keep track of all the 
        # visited vertices 
        visited = [False] * self.V 

        # To store minimum number of edges 
        min_num_of_edges = float('inf') 

        # To store total number of 
        # edges in each path 
        edge_count = 0

        min_num_of_edges, edge_count = \
        self.minEdgeDFSUtil(visited, u, v, min_num_of_edges, edge_count) 

        # Print the minimum number of edges 
        print(min_num_of_edges) 

# Driver Code 
if __name__ == "__main__": 

    # Create a graph 
    g = Graph(5) 
    g.addEdge(0, 1) 
    g.addEdge(0, 4) 
    g.addEdge(1, 2) 
    g.addEdge(2, 4) 
    g.addEdge(2, 3) 
    g.addEdge(3, 4) 

    u, v = 0, 3
    g.minEdgeDFS(u, v) 

# This code is contributed by Rituraj Jain

```

## C＃

```

// C# program to find minimum 
// number of edges between any two 
// vertices of the graph 
using System;
using System.Collections;

class GFG{ 

static int min_num_of_edges = 0, 
                 edge_count = 0; 

// Class to represent a graph 
class Graph 
{ 

    // No. of vertices 
    public int V; 

    // Pointer to an array containing 
    // adjacency lists 
    public ArrayList []adj; 

    // A function used by minEdgeDFS 

    // Utility function for finding 
    // minimum number of edges using DFS 
    public void minEdgeDFSUtil(bool[] visited, 
                               int src, int des) 
    { 

        // For keeping track of visited 
        // nodes in DFS 
        visited[src] = true; 

        // If we have found the destination 
        // vertex then check whether count
        // of total number of edges is less 
        // than the minimum number of edges or not 
        if (src == des) 
        { 
            if (min_num_of_edges > edge_count) 
                min_num_of_edges = edge_count; 
        } 

        // If current vertex is not destination 
        else
        { 
            foreach(int i in adj[src]) 
            { 
                int v = i; 

                if (!visited[v]) 
                { 
                    edge_count++; 
                    minEdgeDFSUtil(visited, v, des); 
                } 
            } 
        } 

        // Decrement the count of number of edges 
        // and mark current vertex as unvisited 
        visited[src] = false; 
        edge_count--; 
    } 

    public Graph(int V) 
    { 
        this.V = V; 
        adj = new ArrayList[V]; 

        for(int i = 0; i < V; i++) 
            adj[i] = new ArrayList(); 
    } 

    // Function to add an edge to graph 
    public void addEdge(int src, int des) 
    { 
        adj[src].Add(des); 
        adj[des].Add(src); 
    } 

    // Function to print minimum number of edges 
    // It uses recursive minEdgeDFSUtil 
    public void minEdgeDFS(int u, int v) 
    { 

        // To keep track of all the 
        // visited vertices 
        bool[] visited = new bool[this.V]; 
        Array.Fill(visited, false); 

        // To store minimum number of edges 
        min_num_of_edges = Int32.MaxValue; 

        // To store total number of 
        // edges in each path 
        edge_count = 0; 

        minEdgeDFSUtil(visited, u, v); 

        // Print the minimum number of edges 
        Console.Write(min_num_of_edges); 
    } 
} 

// Driver Code 
public static void Main(string[] args) 
{ 

    // Create a graph 
    Graph g = new Graph(5); 
    g.addEdge(0, 1); 
    g.addEdge(0, 4); 
    g.addEdge(1, 2); 
    g.addEdge(2, 4); 
    g.addEdge(2, 3); 
    g.addEdge(3, 4); 

    int u = 0; 
    int v = 3; 

    g.minEdgeDFS(u, v); 
} 
} 

// This code is contributed by rutvik_56

```

**Output:** 

```
2

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。