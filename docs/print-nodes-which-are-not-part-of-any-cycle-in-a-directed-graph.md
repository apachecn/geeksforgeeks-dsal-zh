# 打印有向图中不属于任何循环的节点

> 原文:[https://www . geesforgeks . org/print-nodes-哪些节点不是有向图中任何周期的一部分/](https://www.geeksforgeeks.org/print-nodes-which-are-not-part-of-any-cycle-in-a-directed-graph/)

给定由值为**【0，N–1】**的节点组成的有向[图](https://www.geeksforgeeks.org/introduction-to-graphs/) G **N** 节点和 **E** 边，以及表示顶点 **u** 和 **v** 之间的[有向边的类型为{ **u** 、 **v** 的](https://www.geeksforgeeks.org/minimum-number-of-edges-between-two-vertices-of-a-graph/) [2D 数组**边】【2】**。任务是在给定的图 **G** 中找到不属于任何循环的节点。](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)

**示例:**

> **输入:** N = 4，E = 4，边[][2] = { {0，2}，{0，1}，{2，3}，{3，0} }
> 输出:1
> T6】解释:T8】
> 
> ![](img/05763e3c10b44e507101abddf59104bf.png)
> 
> 从上面给定的图中，节点 0 -> 2 -> 3 -> 0 之间存在一个循环。
> 任何周期都不发生的节点为 1。
> 因此，打印 1。
> 
> **输入:** N = 6，E = 7，Edges[][2] = { {0，1}，{0，2}，{1，3}，{2，1}，{2，5}，{3，0}，{4，5 } }
> T3】输出:4 5
> T6】解释:T8】
> 
> ![](img/ab490d759b83e56607641da5d3338540.png)
> 
> 从上面给定的图中，节点之间存在循环:
> 1) 0 - > 1 - > 3 - > 0。
> 2)0->2->1->3->0。
> 任何周期都不发生的节点是 4 和 5。
> 因此，打印 4 和 5。

**天真方法:**最简单的方法是[为给定图中的每个节点检测有向图](https://www.geeksforgeeks.org/detect-cycle-in-a-graph/)中的一个循环，并且只打印那些不属于给定图中任何循环的节点。
***时间复杂度:** O(V * (V + E))，其中 V 为顶点数，E 为边数。*
***辅助空间:** O(V)*

**高效方法:**为了优化上述方法，其思想是每当给定图中有任何周期时，将中间节点存储为**访问周期节点**。要实现这一部分，请使用辅助数组**循环数组[]** ，该数组将在执行 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)时存储中间循环节点。以下是步骤:

*   初始化一个大小为 **N** 的辅助数组 **cyclePart[]** ，这样如果 **cyclePart[i] = 0** ，那么 **i <sup>th</sup>** 节点在任何循环中都不存在。
*   初始化一个大小为 **N** 的辅助数组 **recStack[]** ，这样它将通过将被访问节点标记为 **true** 来将该节点存储在[递归](https://www.geeksforgeeks.org/recursion/)堆栈中。
*   对每个未访问的节点在给定的图上执行 DFS 遍历，并执行以下操作:
    *   现在在给定的图中找到一个循环，每当找到一个循环时，将**循环中的节点标记为**真**，因为该节点是循环的一部分。**
    *   如果任何**节点**在[递归](https://www.geeksforgeeks.org/recursion/)调用中被访问并且是 **recStack【节点】**也为真，则该节点是循环的一部分，然后将该节点标记为**真**。
*   执行 **DFS 遍历**后，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **循环【】**并打印所有标记为 **false** 的节点，因为这些节点不是任何循环的一部分。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

class Graph {

    // No. of vertices
    int V;

    // Stores the Adjacency List
    list<int>* adj;
    bool printNodesNotInCycleUtil(
        int v, bool visited[], bool* rs,
        bool* cyclePart);

public:
    // Constructor
    Graph(int V);

    // Member Functions
    void addEdge(int v, int w);
    void printNodesNotInCycle();
};

// Function to initialize the graph
Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}

// Function that adds directed edges
// between node v with node w
void Graph::addEdge(int v, int w)
{
    adj[v].push_back(w);
}

// Function to perform DFS Traversal
// and return true if current node v
// formes cycle
bool Graph::printNodesNotInCycleUtil(
    int v, bool visited[],
    bool* recStack, bool* cyclePart)
{

    // If node v is unvisited
    if (visited[v] == false) {

        // Mark the current node as
        // visited and part of
        // recursion stack
        visited[v] = true;
        recStack[v] = true;

        // Traverse the Adjacency
        // List of current node v
        for (auto& child : adj[v]) {

            // If child node is unvisited
            if (!visited[child]
                && printNodesNotInCycleUtil(
                       child, visited,
                       recStack, cyclePart)) {

                // If child node is a part
                // of cycle node
                cyclePart[child] = 1;
                return true;
            }

            // If child node is visited
            else if (recStack[child]) {
                cyclePart[child] = 1;
                return true;
            }
        }
    }

    // Remove vertex from recursion stack
    recStack[v] = false;
    return false;
}

// Function that print the nodes for
// the given directed graph that are
// not present in any cycle
void Graph::printNodesNotInCycle()
{

    // Stores the visited node
    bool* visited = new bool[V];

    // Stores nodes in recursion stack
    bool* recStack = new bool[V];

    // Stores the nodes that are
    // part of any cycle
    bool* cyclePart = new bool[V];

    for (int i = 0; i < V; i++) {
        visited[i] = false;
        recStack[i] = false;
        cyclePart[i] = false;
    }

    // Traverse each node
    for (int i = 0; i < V; i++) {

        // If current node is unvisited
        if (!visited[i]) {

            // Perform DFS Traversal
            if (printNodesNotInCycleUtil(
                    i, visited, recStack,
                    cyclePart)) {

                // Mark as cycle node
                // if it return true
                cyclePart[i] = 1;
            }
        }
    }

    // Traverse the cyclePart[]
    for (int i = 0; i < V; i++) {

        // If node i is not a part
        // of any cycle
        if (cyclePart[i] == 0) {
            cout << i << " ";
        }
    }
}

// Function that print the nodes for
// the given directed graph that are
// not present in any cycle
void solve(int N, int E,
           int Edges[][2])
{

    // Initialize the graph g
    Graph g(N);

    // Create a directed Graph
    for (int i = 0; i < E; i++) {
        g.addEdge(Edges[i][0],
                  Edges[i][1]);
    }

    // Function Call
    g.printNodesNotInCycle();
}

// Driver Code
int main()
{
    // Given Number of nodes
    int N = 6;

    // Given Edges
    int E = 7;

    int Edges[][2] = { { 0, 1 }, { 0, 2 },
                       { 1, 3 }, { 2, 1 },
                       { 2, 5 }, { 3, 0 },
                                 { 4, 5 } };

    // Function Call
    solve(N, E, Edges);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
import java.lang.*;
class GFG
{

  static ArrayList<ArrayList<Integer>> adj;
  static int V;

  // Function to perform DFS Traversal
  // and return true if current node v
  // formes cycle
  static boolean printNodesNotInCycleUtil(
    int v, boolean visited[],
    boolean[] recStack, boolean[] cyclePart)
  {

    // If node v is unvisited
    if (visited[v] == false)
    {

      // Mark the current node as
      // visited and part of
      // recursion stack
      visited[v] = true;
      recStack[v] = true;

      // Traverse the Adjacency
      // List of current node v
      for (Integer child : adj.get(v))
      {

        // If child node is unvisited
        if (!visited[child]
            && printNodesNotInCycleUtil(
              child, visited,
              recStack, cyclePart))
        {

          // If child node is a part
          // of cycle node
          cyclePart[child] = true;
          return true;
        }

        // If child node is visited
        else if (recStack[child])
        {
          cyclePart[child] = true;
          return true;
        }
      }
    }

    // Remove vertex from recursion stack
    recStack[v] = false;
    return false;
  }

  static void printNodesNotInCycle()
  {

    // Stores the visited node
    boolean[] visited = new boolean[V];

    // Stores nodes in recursion stack
    boolean[] recStack = new boolean[V];

    // Stores the nodes that are
    // part of any cycle
    boolean[] cyclePart = new boolean[V];

    // Traverse each node
    for (int i = 0; i < V; i++)
    {

      // If current node is unvisited
      if (!visited[i])
      {

        // Perform DFS Traversal
        if (printNodesNotInCycleUtil(
          i, visited, recStack,
          cyclePart)) {

          // Mark as cycle node
          // if it return true
          cyclePart[i] = true;
        }
      }
    }

    // Traverse the cyclePart[]
    for (int i = 0; i < V; i++)
    {

      // If node i is not a part
      // of any cycle
      if (!cyclePart[i])
      {
        System.out.print(i+" ");
      }
    }
  }

  // Function that print the nodes for
  // the given directed graph that are
  // not present in any cycle
  static void solve(int N, int E,
                    int Edges[][])
  {

    adj = new ArrayList<>();

    for(int i = 0; i < N; i++)
      adj.add(new ArrayList<>());

    // Create a directed Graph
    for (int i = 0; i < E; i++)
    {
      adj.get(Edges[i][0]).add(Edges[i][1]);
    }

    // Function Call
    printNodesNotInCycle();
  }

  // Driver function
  public static void main (String[] args)
  {

    // Given Number of nodes
    V = 6;

    // Given Edges
    int E = 7;

    int Edges[][] = { { 0, 1 }, { 0, 2 },
                     { 1, 3 }, { 2, 1 },
                     { 2, 5 }, { 3, 0 },
                     { 4, 5 } };

    // Function Call
    solve(V, E, Edges);

  }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

class Graph:

    # Function to initialize the graph
    def __init__(self, V):

        self.V = V
        self.adj = [[] for i in range(self.V)]

    # Function that adds directed edges
    # between node v with node w
    def addEdge(self, v, w):

        self.adj[v].append(w);

    # Function to perform DFS Traversal
    # and return True if current node v
    # formes cycle
    def printNodesNotInCycleUtil(self, v, visited,recStack, cyclePart):

        # If node v is unvisited
        if (visited[v] == False):

            # Mark the current node as
            # visited and part of
            # recursion stack
            visited[v] = True;
            recStack[v] = True;

            # Traverse the Adjacency
            # List of current node v
            for child in self.adj[v]:

                # If child node is unvisited
                if (not visited[child] and self.printNodesNotInCycleUtil(child, visited,recStack, cyclePart)):

                    # If child node is a part
                    # of cycle node
                    cyclePart[child] = 1;
                    return True;

                # If child node is visited
                elif (recStack[child]):
                    cyclePart[child] = 1;
                    return True;

        # Remove vertex from recursion stack
        recStack[v] = False;
        return False;

    # Function that print the nodes for
    # the given directed graph that are
    # not present in any cycle
    def printNodesNotInCycle(self):

        # Stores the visited node
        visited = [False for i in range(self.V)];

        # Stores nodes in recursion stack
        recStack = [False for i in range(self.V)];

        # Stores the nodes that are
        # part of any cycle
        cyclePart = [False for i in range(self.V)]

        # Traverse each node
        for i in range(self.V):

            # If current node is unvisited
            if (not visited[i]):

                # Perform DFS Traversal
                if(self.printNodesNotInCycleUtil(
                        i, visited, recStack,
                        cyclePart)):

                    # Mark as cycle node
                    # if it return True
                    cyclePart[i] = 1;

        # Traverse the cyclePart[]
        for i in range(self.V):

            # If node i is not a part
            # of any cycle
            if (cyclePart[i] == 0) :
                print(i,end=' ')

# Function that print the nodes for
# the given directed graph that are
# not present in any cycle
def solve( N, E, Edges):

    # Initialize the graph g
    g = Graph(N);

    # Create a directed Graph
    for i in range(E):

        g.addEdge(Edges[i][0],
                  Edges[i][1]);  

    # Function Call
    g.printNodesNotInCycle();   

    # Driver Code
if __name__=='__main__':

    # Given Number of nodes
    N = 6;

    # Given Edges
    E = 7;

    Edges = [ [ 0, 1 ], [ 0, 2 ],
                       [ 1, 3 ], [ 2, 1 ],
                       [ 2, 5 ], [ 3, 0 ],
                                 [ 4, 5 ] ];

    # Function Call
    solve(N, E, Edges);

# This code is contributed by rutvik_56
```

**Output:** 

```
4 5
```

***时间复杂度:** O(V + E)*
***空间复杂度:** O(V)*