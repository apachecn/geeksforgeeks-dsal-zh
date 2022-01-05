# 图形及其表示

> 原文:[https://www . geeksforgeeks . org/graph-and-it-presentations/](https://www.geeksforgeeks.org/graph-and-its-representations/)

图是由以下两个部分组成的数据结构:
**1。**一组有限的顶点，也称为节点。
T4【2】。称为边的形式(u，v)的有序对的有限集合。对是有序的，因为在有向图(di-graph)的情况下(u，v)与(v，u)不同。形式(u，v)的对表示从顶点 u 到顶点 v 有一条边。这些边可能包含权重/值/成本。
图形用于表示许多现实生活中的应用:图形用于表示网络。网络可以包括城市或电话网络或电路网络中的路径。图表也用于社交网络，如脸书的领英。例如，在脸书，每个人都用一个顶点(或节点)来表示。每个节点都是一个结构，包含诸如个人 id、姓名、性别和地区等信息。更多图形应用见[本](http://en.wikipedia.org/wiki/Graph_theory#Applications)。
下面是一个有 5 个顶点的无向图的例子。

![](img/bf0ecf4aed9c34e052191baf40164fa2.png)

以下两个是最常用的图形表示。
**1。**邻接矩阵
**2。**邻接表
还有其他类似的表示，关联矩阵和关联列表。图形表示的选择取决于具体情况。这完全取决于要执行的操作类型和易用性。
**邻接矩阵:**
邻接矩阵是一个大小为 V x V 的 2D 数组，其中 V 是图中的顶点数。设 2D 数组为 adj[][]，槽 adj[i][j] = 1 表示从顶点 I 到顶点 j 有一条边，无向图的邻接矩阵总是对称的。邻接矩阵也用于表示加权图。如果 adj[i][j] = w，则从顶点 I 到顶点 j 有一条边，权重为 w

上述示例图的邻接矩阵为:

![Adjacency Matrix Representation](img/e6ce2df9f47474d523e582301bb05396.png)

*优点:*表示更容易实现和遵循。移除边需要 0(1)时间。像从顶点“u”到顶点“v”是否有边这样的查询是有效的，可以用 O(1)来完成。
*缺点:*消耗 O(V^2).更多空间即使图是稀疏的(包含较少数量的边)，它也会消耗相同的空间。添加顶点是 O(V^2 时间。
邻接矩阵的 Python 实现示例请参见[本](https://ide.geeksforgeeks.org/9je5j6jJ13)。
**邻接表:**
使用列表数组。数组的大小等于顶点的数量。让数组成为数组[]。条目数组[i]表示与第***i*** 个顶点相邻的顶点列表。这种表示也可以用来表示加权图。边的权重可以表示成对的列表。下面是上图的邻接表表示。

![Adjacency List Representation of Graph](img/2c37d703328bcef494fbd4617b0f46df.png)

请注意，在下面的实现中，我们使用动态数组(C++中的 vector/Java 中的 ArrayList)来表示邻接表，而不是链表。向量实现具有缓存友好的优点。

## C

```
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

```
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
  struct AdjListNode* check = NULL;
  struct AdjListNode* newNode = newAdjListNode(dest);

  if(graph->array[src].head == NULL)
  {
    newNode->next = graph->array[src].head;
    graph->array[src].head = newNode;
  }
  else
  {

      check = graph->array[src].head;
    while(check->next != NULL)
    {
      check = check->next;
    }
    //graph->array[src].head = newNode;
    check->next = newNode;
  }

    // Since graph is undirected, add an edge from
    // dest to src also
    newNode = newAdjListNode(src);
  if(graph->array[dest].head == NULL)
  {
    newNode->next = graph->array[dest].head;
    graph->array[dest].head = newNode;
  }
  else
  {
    check = graph->array[dest].head;
    while(check->next != NULL)
    {
      check = check->next;
    }
    check->next = newNode;
  }

    //newNode = newAdjListNode(src);
    //newNode->next = graph->array[dest].head;
    //graph->array[dest].head = newNode;
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

## Java 语言(一种计算机语言，尤用于创建网站)

```
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

## 蟒蛇 3

```
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

```
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

## java 描述语言

```
<script>
// Javascript code to demonstrate Graph representation
// using ArrayList in Java

// A utility function to add an edge in an
    // undirected graph
function addEdge(adj,u,v)
{
    adj[u].push(v);
        adj[v].push(u);
}

// A utility function to print the adjacency list
    // representation of graph
function printGraph(adj)
{
    for (let i = 0; i < adj.length; i++) {
            document.write("<br>Adjacency list of vertex" + i+"<br>");
            document.write("head");
            for (let j = 0; j < adj[i].length; j++) {
                document.write(" -> "+adj[i][j]);
            }
            document.write("<br>");
        }
}

// Driver Code
// Creating a graph with 5 vertices
        let V = 5;
        let adj= [];

        for (let i = 0; i < V; i++)
            adj.push([]);

        // Adding edges one by one
        addEdge(adj, 0, 1);
        addEdge(adj, 0, 4);
        addEdge(adj, 1, 2);
        addEdge(adj, 1, 3);
        addEdge(adj, 1, 4);
        addEdge(adj, 2, 3);
        addEdge(adj, 3, 4);

        printGraph(adj);

// This code is contributed by avanitrachhadiya2155
</script>
```

输出:

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

*优点:*节省空间 O(|V|+|E|)。在最坏的情况下，图中可能有 C(V，2)个边，从而消耗 O(V^2 空间。添加顶点更容易。
*缺点:*像从顶点 u 到顶点 V 是否有边这样的查询效率不高，可以做 O(V)。

参考:
[【http://en.wikipedia.org/wiki/Graph_%28abstract_data_type%29】](http://en.wikipedia.org/wiki/Graph_%28abstract_data_type%29)
**相关帖子:**
[使用 STL 进行竞争性编程的图表示|集合 1(未加权和无向的 DFS)](https://www.geeksforgeeks.org/graph-representation-using-stl-for-competitive-programming-set-1-dfs-of-unweighted-and-undirected/)
[使用 STL 进行竞争性编程的图实现|集合 2(加权图)](https://www.geeksforgeeks.org/graph-implementation-using-stl-for-competitive-programming-set-2-weighted-graph/)
本文由[aashis Barnwal](https://www.facebook.com/barnwal.aashish)编辑，GeeksforGeeks 团队审阅。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。