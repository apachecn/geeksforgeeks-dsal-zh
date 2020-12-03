# 图及其表示

> 原文： [https://www.geeksforgeeks.org/graph-and-its-representations/](https://www.geeksforgeeks.org/graph-and-its-representations/)

图是一种数据结构，由以下两个部分组成：

**1\.** 一组有限的顶点，也称为节点。

**2\.** 形式有限的一组有序对，其形式为（u，v），称为边。 该对有序，因为在有向图（二向图）的情况下（u，v）与（v，u）不同。 形式为（u，v）的对表示从顶点 u 到顶点 v 有一条边。这些边可能包含权重/值/成本。

图用于表示许多现实生活中的应用程序：图用于表示网络。 网络可以包括城市或电话网络或电路网络中的路径。 图形还用于诸如 linkedIn，Facebook 之类的社交网络中。 例如，在 Facebook 中，每个人都用一个顶点（或节点）表示。 每个节点都是一个结构，并包含诸如个人 ID，姓名，性别和语言环境之类的信息。 有关图表的更多应用，请参见此的[。](http://en.wikipedia.org/wiki/Graph_theory#Applications)

以下是具有 5 个顶点的无向图的示例。

![](img/bf0ecf4aed9c34e052191baf40164fa2.png "graph_representation1")

以下两个是图形的最常用表示形式。

**1\.** 邻接矩阵

**2\.** 邻接列表

也有其他表示，例如，事件矩阵和事件列表。 图形表示的选择取决于具体情况。 这完全取决于要执行的操作类型和易用性。

**邻接矩阵**：

邻接矩阵是 2D 数组，大小为 V x V，其中 V 是图形中的顶点数。 假设 2D 数组为 adj [] []，则槽 adj [i] [j] = 1 表示从顶点 i 到顶点 j 有一条边。 无向图的邻接矩阵始终是对称的。 邻接矩阵也用于表示加权图。 如果 adj [i] [j] = w，则从顶点 i 到顶点 j 的权重为 w 的边。

上面的示例图的邻接矩阵为：

![Adjacency Matrix Representation](img/e6ce2df9f47474d523e582301bb05396.png "adjacency_matrix_representation")

*优点：*表示更易于实现和遵循。 移除边需要`O(1)`时间。 诸如从顶点“ u”到顶点“ v”是否存在边的查询是有效的，可以执行`O(1)`。

*缺点：*占用更多空间`O(V ^ 2)`。 即使图是稀疏的（包含较少的边数），它也会占用相同的空间。 添加一个顶点是`O(V ^ 2)`时间。

有关相邻矩阵的 Python 实现示例，请参见此的[。](https://ide.geeksforgeeks.org/9je5j6jJ13)

**邻接列表**：

使用列表数组。 数组的大小等于顶点数。 令数组为 array []。 入口数组[i]表示与第**，*，*，**个顶点相邻的顶点列表。 该表示也可以用于表示加权图。 边的权重可以表示为成对列表。 以下是上图的邻接列表表示。

![Adjacency List Representation of Graph](img/2c37d703328bcef494fbd4617b0f46df.png "adjacency_list_representation")

请注意，在以下实现中，我们使用动态数组（Java 中为 C++ / ArrayList 中的向量）表示邻接列表，而不是链接列表。 向量实现具有缓存友好性的优点。

## C++

```cpp

// A simple representation of graph using STL 
#include<bits/stdc++.h> 
using namespace std; 

// A utility function to add an edge in an 
// undirected graph. 
void addEdge(vector<int> adj[], int u, int v) 
{ 
    adj[u].push_back(v); 
    adj[v].push_back(u); 
} 

// A utility function to print the adjacency list 
// representation of graph 
void printGraph(vector<int> adj[], int V) 
{ 
    for (int v = 0; v < V; ++v) 
    { 
        cout << "\n Adjacency list of vertex "
             << v << "\n head "; 
        for (auto x : adj[v]) 
           cout << "-> " << x; 
        printf("\n"); 
    } 
} 

// Driver code 
int main() 
{ 
    int V = 5; 
    vector<int> adj[V]; 
    addEdge(adj, 0, 1); 
    addEdge(adj, 0, 4); 
    addEdge(adj, 1, 2); 
    addEdge(adj, 1, 3); 
    addEdge(adj, 1, 4); 
    addEdge(adj, 2, 3); 
    addEdge(adj, 3, 4); 
    printGraph(adj, V); 
    return 0; 
} 

```

## C

```c

// A C Program to demonstrate adjacency list  
// representation of graphs 
#include <stdio.h> 
#include <stdlib.h> 

// A structure to represent an adjacency list node 
struct AdjListNode 
{ 
    int dest; 
    struct AdjListNode* next; 
}; 

// A structure to represent an adjacency list 
struct AdjList 
{ 
    struct AdjListNode *head;  
}; 

// A structure to represent a graph. A graph 
// is an array of adjacency lists. 
// Size of array will be V (number of vertices  
// in graph) 
struct Graph 
{ 
    int V; 
    struct AdjList* array; 
}; 

// A utility function to create a new adjacency list node 
struct AdjListNode* newAdjListNode(int dest) 
{ 
    struct AdjListNode* newNode = 
     (struct AdjListNode*) malloc(sizeof(struct AdjListNode)); 
    newNode->dest = dest; 
    newNode->next = NULL; 
    return newNode; 
} 

// A utility function that creates a graph of V vertices 
struct Graph* createGraph(int V) 
{ 
    struct Graph* graph =  
        (struct Graph*) malloc(sizeof(struct Graph)); 
    graph->V = V; 

    // Create an array of adjacency lists.  Size of  
    // array will be V 
    graph->array =  
      (struct AdjList*) malloc(V * sizeof(struct AdjList)); 

    // Initialize each adjacency list as empty by  
    // making head as NULL 
    int i; 
    for (i = 0; i < V; ++i) 
        graph->array[i].head = NULL; 

    return graph; 
} 

// Adds an edge to an undirected graph 
void addEdge(struct Graph* graph, int src, int dest) 
{ 
    // Add an edge from src to dest.  A new node is  
    // added to the adjacency list of src.  The node 
    // is added at the beginning 
    struct AdjListNode* newNode = newAdjListNode(dest); 
    newNode->next = graph->array[src].head; 
    graph->array[src].head = newNode; 

    // Since graph is undirected, add an edge from 
    // dest to src also 
    newNode = newAdjListNode(src); 
    newNode->next = graph->array[dest].head; 
    graph->array[dest].head = newNode; 
} 

// A utility function to print the adjacency list  
// representation of graph 
void printGraph(struct Graph* graph) 
{ 
    int v; 
    for (v = 0; v < graph->V; ++v) 
    { 
        struct AdjListNode* pCrawl = graph->array[v].head; 
        printf("\n Adjacency list of vertex %d\n head ", v); 
        while (pCrawl) 
        { 
            printf("-> %d", pCrawl->dest); 
            pCrawl = pCrawl->next; 
        } 
        printf("\n"); 
    } 
} 

// Driver program to test above functions 
int main() 
{ 
    // create the graph given in above fugure 
    int V = 5; 
    struct Graph* graph = createGraph(V); 
    addEdge(graph, 0, 1); 
    addEdge(graph, 0, 4); 
    addEdge(graph, 1, 2); 
    addEdge(graph, 1, 3); 
    addEdge(graph, 1, 4); 
    addEdge(graph, 2, 3); 
    addEdge(graph, 3, 4); 

    // print the adjacency list representation of the above graph 
    printGraph(graph); 

    return 0; 
} 

```

## Java

```java

// Java code to demonstrate Graph representation 
// using ArrayList in Java 

import java.util.*; 

class Graph { 

    // A utility function to add an edge in an 
    // undirected graph 
    static void addEdge(ArrayList<ArrayList<Integer> > adj, 
                        int u, int v) 
    { 
        adj.get(u).add(v); 
        adj.get(v).add(u); 
    } 

    // A utility function to print the adjacency list 
    // representation of graph 
    static void printGraph(ArrayList<ArrayList<Integer> > adj) 
    { 
        for (int i = 0; i < adj.size(); i++) { 
            System.out.println("\nAdjacency list of vertex" + i); 
            System.out.print("head"); 
            for (int j = 0; j < adj.get(i).size(); j++) { 
                System.out.print(" -> "+adj.get(i).get(j)); 
            } 
            System.out.println(); 
        } 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        // Creating a graph with 5 vertices 
        int V = 5; 
        ArrayList<ArrayList<Integer> > adj  
                    = new ArrayList<ArrayList<Integer> >(V); 

        for (int i = 0; i < V; i++) 
            adj.add(new ArrayList<Integer>()); 

        // Adding edges one by one 
        addEdge(adj, 0, 1); 
        addEdge(adj, 0, 4); 
        addEdge(adj, 1, 2); 
        addEdge(adj, 1, 3); 
        addEdge(adj, 1, 4); 
        addEdge(adj, 2, 3); 
        addEdge(adj, 3, 4); 

        printGraph(adj); 
    } 
} 

```

## Python

```py

""" 
A Python program to demonstrate the adjacency 
list representation of the graph 
"""

# A class to represent the adjacency list of the node 
class AdjNode: 
    def __init__(self, data): 
        self.vertex = data 
        self.next = None

# A class to represent a graph. A graph 
# is the list of the adjacency lists. 
# Size of the array will be the no. of the 
# vertices "V" 
class Graph: 
    def __init__(self, vertices): 
        self.V = vertices 
        self.graph = [None] * self.V 

    # Function to add an edge in an undirected graph 
    def add_edge(self, src, dest): 
        # Adding the node to the source node 
        node = AdjNode(dest) 
        node.next = self.graph[src] 
        self.graph[src] = node 

        # Adding the source node to the destination as 
        # it is the undirected graph 
        node = AdjNode(src) 
        node.next = self.graph[dest] 
        self.graph[dest] = node 

    # Function to print the graph 
    def print_graph(self): 
        for i in range(self.V): 
            print("Adjacency list of vertex {}\n head".format(i), end="") 
            temp = self.graph[i] 
            while temp: 
                print(" -> {}".format(temp.vertex), end="") 
                temp = temp.next
            print(" \n") 

# Driver program to the above graph class 
if __name__ == "__main__": 
    V = 5
    graph = Graph(V) 
    graph.add_edge(0, 1) 
    graph.add_edge(0, 4) 
    graph.add_edge(1, 2) 
    graph.add_edge(1, 3) 
    graph.add_edge(1, 4) 
    graph.add_edge(2, 3) 
    graph.add_edge(3, 4) 

    graph.print_graph() 

# This code is contributed by Kanav Malhotra 

```

## C#

```cs

// C# code to demonstrate Graph representation  
// using LinkedList in C#  
using System; 
using System.Collections.Generic; 

class Graph 
{ 
    // A utility function to add an edge in an  
    // undirected graph  
    static void addEdge(LinkedList<int>[] adj, 
                        int u, int v) 
    { 
        adj[u].AddLast(v); 
        adj[v].AddLast(u); 
    } 

    // A utility function to print the adjacency list  
    // representation of graph  
    static void printGraph( LinkedList<int>[]  adj) 
    { 
        for (int i = 0; i < adj.Length; i++) 
        { 
            Console.WriteLine("\nAdjacency list of vertex " + i); 
            Console.Write("head"); 

            foreach (var item in adj[i]) 
            {  
                Console.Write(" -> " + item); 
            } 
            Console.WriteLine(); 
        } 
    } 

    // Driver Code  
    public static void Main(String[] args) 
    { 
        // Creating a graph with 5 vertices  
        int V = 5; 
        LinkedList<int>[] adj = new LinkedList<int>[V]; 

        for (int i = 0; i < V; i++) 
            adj[i] = new LinkedList<int>(); 

        // Adding edges one by one  
        addEdge(adj, 0, 1); 
        addEdge(adj, 0, 4); 
        addEdge(adj, 1, 2); 
        addEdge(adj, 1, 3); 
        addEdge(adj, 1, 4); 
        addEdge(adj, 2, 3); 
        addEdge(adj, 3, 4); 

        printGraph(adj); 

        Console.ReadKey(); 
    } 
} 

// This code is contributed by techno2mahi 

```

Output:

```

 Adjacency list of vertex 0
 head -> 1-> 4

 Adjacency list of vertex 1
 head -> 0-> 2-> 3-> 4

 Adjacency list of vertex 2
 head -> 1-> 3

 Adjacency list of vertex 3
 head -> 1-> 2-> 4

 Adjacency list of vertex 4
 head -> 0-> 1-> 3

```

*优点：*节省空间 O（| V | + | E |）。 在最坏的情况下，图中可能有 C（V，2）个边，因此会占用`O(V ^ 2)`空间。 添加顶点更容易。

*缺点：*诸如从顶点 u 到顶点 v 是否存在边的查询效率不高，可以执行 O（V）。

参考：

[http://en.wikipedia.org/wiki/Graph_%28abstract_data_type%29](http://en.wikipedia.org/wiki/Graph_%28abstract_data_type%29)

**相关文章**：

[使用 STL 进行竞争性编程的图形表示 | 系列 1（无权重和无向 DFS）](https://www.geeksforgeeks.org/graph-representation-using-stl-for-competitive-programming-set-1-dfs-of-unweighted-and-undirected/)

[使用 STL 进行竞争性编程的图形实现 | 系列 2（加权图）](https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-2-weighted-graph/)

本文由 [Aashish Barnwal](https://www.facebook.com/barnwal.aashish) 编写，并由 GeeksforGeeks 小组审阅。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

