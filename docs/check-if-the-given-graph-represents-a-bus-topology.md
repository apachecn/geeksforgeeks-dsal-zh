# 检查给定的图形是否代表总线拓扑

> 原文:[https://www . geesforgeks . org/check-如果给定的图表示总线拓扑/](https://www.geeksforgeeks.org/check-if-the-given-graph-represents-a-bus-topology/)

给定一个图形 **G** ，检查它是否代表总线拓扑。
总线拓扑如下图所示:

![](img/dcba898b8132ead7bd204436a3a4e787.png)

**例:**

```
Input: 
```

![](img/263916f98b63bd1af6657e02c81383df.png)

```
Output:  YES

Input: 
```

![](img/049f779e6c0f9ba06ebff95623604cc8.png)

```
Output:  NO
```

如果 V 顶点的图满足以下两个条件，则表示总线拓扑:

1.  除了开始和结束节点外，每个节点都有 2 级，而开始和结束节点都有 1 级。
2.  边数=顶点数–1。

思路是遍历图，检查是否满足以上两个条件。如果是，则表示总线拓扑。
以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to check if the given graph
// represents a bus topology
#include <bits/stdc++.h>
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
    for (int v = 0; v < V; ++v) {
        cout << "\n Adjacency list of vertex "
             << v << "\n head ";
        for (auto x : adj[v])
            cout << "-> " << x;
        printf("\n");
    }
}

/* Function to return true if the graph represented
   by the adjacency list represents a bus topology
   else return false */
bool checkBusTopologyUtil(vector<int> adj[], int V, int E)
{

    // Number of edges should be equal
    // to (Number of vertices - 1)
    if (E != (V - 1))
        return false;

    // a single node is termed as a bus topology
    if (V == 1)
        return true;

    int* vertexDegree = new int[V + 1];
    memset(vertexDegree, 0, sizeof vertexDegree);

    // calculate the degree of each vertex
    for (int i = 1; i <= V; i++) {
        for (auto v : adj[i]) {
            vertexDegree[v]++;
        }
    }

    // countDegree2 - number of vertices with degree 2
    // countDegree1 - number of vertices with degree 1
    int countDegree2 = 0, countDegree1 = 0;
    for (int i = 1; i <= V; i++) {
        if (vertexDegree[i] == 2) {
            countDegree2++;
        }
        else if (vertexDegree[i] == 1) {
            countDegree1++;
        }
        else {
            // if any node has degree other
            // than 1 or 2, it is
            // NOT a bus topology
            return false;
        }
    }

    // if both necessary conditions as discussed,
    // satisfy return true
    if (countDegree1 == 2 && countDegree2 == (V - 2)) {
        return true;
    }
    return false;
}

// Function to check if the graph represents a bus topology
void checkBusTopology(vector<int> adj[], int V, int E)
{
    bool isBus = checkBusTopologyUtil(adj, V, E);
    if (isBus) {
        cout << "YES" << endl;
    }
    else {
        cout << "NO" << endl;
    }
}

// Driver code
int main()
{
    // Graph 1
    int V = 5, E = 4;
    vector<int> adj1[V + 1];
    addEdge(adj1, 1, 2);
    addEdge(adj1, 1, 3);
    addEdge(adj1, 3, 4);
    addEdge(adj1, 4, 5);
    checkBusTopology(adj1, V, E);

    // Graph 2
    V = 4, E = 4;
    vector<int> adj2[V + 1];
    addEdge(adj2, 1, 2);
    addEdge(adj2, 1, 3);
    addEdge(adj2, 3, 4);
    addEdge(adj2, 4, 2);
    checkBusTopology(adj2, V, E);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to check if the given graph
// represents a bus topology
import java.io.*;
import java.util.*;

class GFG
{

  // A utility function to add an edge in an
  // undirected graph.
  static void addEdge(ArrayList<ArrayList<Integer>> adj, int u, int v)
  {
    adj.get(u).add(v);
    adj.get(v).add(u);
  }

  // A utility function to print the adjacency list
  // representation of graph
  static void printGraph(ArrayList<ArrayList<Integer>> adj, int V)
  {
    for (int v = 0; v < V; ++v)
    {
      System.out.print("\n Adjacency list of vertex " + v + "\n head ");
      for (int x : adj.get(v))
      {
        System.out.print( "-> " + x);
      }
      System.out.println();
    }
  }

  /* Function to return true if the graph represented
    by the adjacency list represents a bus topology
    else return false */
  static boolean checkBusTopologyUtil(ArrayList<ArrayList<Integer>> adj, int V, int E)
  {
    // Number of edges should be equal
    // to (Number of vertices - 1)
    if (E != (V - 1))
    {
      return false;
    }

    // a single node is termed as a bus topology
    if (V == 1)
    {
      return true;
    }
    int[] vertexDegree = new int[V + 1];

    // calculate the degree of each vertex
    for (int i = 1; i <= V; i++)
    {
      for (int v : adj.get(i))
      {
        vertexDegree[v]++;
      }
    }

    // countDegree2 - number of vertices with degree 2
    // countDegree1 - number of vertices with degree 1
    int countDegree2 = 0, countDegree1 = 0;

    for (int i = 1; i <= V; i++)
    {
      if (vertexDegree[i] == 2)
      {
        countDegree2++;
      }
      else if (vertexDegree[i] == 1)
      {
        countDegree1++;
      }
      else
      {

        // if any node has degree other
        // than 1 or 2, it is
        // NOT a bus topology
        return false;
      }
    }

    // if both necessary conditions as discussed,
    // satisfy return true
    if (countDegree1 == 2 && countDegree2 == (V - 2))
    {
      return true;
    }
    return false;
  }

  // Function to check if the graph represents a bus topology
  static void checkBusTopology(ArrayList<ArrayList<Integer>> adj, int V, int E)
  {
    boolean isBus = checkBusTopologyUtil(adj, V, E);
    if (isBus)
    {
      System.out.println("YES");
    }
    else
    {
      System.out.println("NO");
    }
  }

  // Driver code
  public static void main (String[] args)
  {

    // Graph 1
    int V = 5, E = 4;
    ArrayList<ArrayList<Integer>> adj1=
      new ArrayList<ArrayList<Integer>>();
    for(int i = 0; i < V + 1; i++)
    {
      adj1.add(new ArrayList<Integer>());
    }
    addEdge(adj1, 1, 2);
    addEdge(adj1, 1, 3);
    addEdge(adj1, 3, 4);
    addEdge(adj1, 4, 5);
    checkBusTopology(adj1, V, E);

    // Graph 2
    V = 4;
    E = 4;
    ArrayList<ArrayList<Integer>> adj2 =
      new ArrayList<ArrayList<Integer>>();
    for(int i = 0; i < (V + 1); i++)
    {
      adj2.add(new ArrayList<Integer>());
    }
    addEdge(adj2, 1, 2);
    addEdge(adj2, 1, 3);
    addEdge(adj2, 3, 4);
    addEdge(adj2, 4, 2);
    checkBusTopology(adj2, V, E);
  }
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program to check if the given graph
# represents a bus topology

# A utility function to add an edge in an
# undirected graph.
def addEdge(adj, u, v):
    adj[u].append(v)
    adj[v].append(u)

# A utility function to print the adjacency list
# representation of graph
def printGraph(adj, V):

    for v in range(V):
        print("Adjacency list of vertex ",v,"\n head ")
        for x in adj[v]:
            print("-> ",x,end=" ")
        printf()

# /* Function to return true if the graph represented
# by the adjacency list represents a bus topology
# else return false */
def checkBusTopologyUtil(adj, V, E):

    # Number of edges should be equal
    # to (Number of vertices - 1)
    if (E != (V - 1)):
        return False

    # a single node is termed as a bus topology
    if (V == 1):
        return True

    vertexDegree = [0]*(V + 1)

    # calculate the degree of each vertex
    for i in range(V + 1):
        for v in adj[i]:
            vertexDegree[v] += 1

    # countDegree2 - number of vertices with degree 2
    # countDegree1 - number of vertices with degree 1
    countDegree2,countDegree1 = 0,0
    for i in range(1, V + 1):
        if (vertexDegree[i] == 2):
            countDegree2 += 1

        elif (vertexDegree[i] == 1):
            countDegree1 += 1

        else:
            # if any node has degree other
            # than 1 or 2, it is
            # NOT a bus topology
            return False

    # if both necessary conditions as discussed,
    # satisfy return true
    if (countDegree1 == 2 and countDegree2 == (V - 2)):
        return True

    return False

# Function to check if the graph represents a bus topology
def checkBusTopology(adj, V, E):

    isBus = checkBusTopologyUtil(adj, V, E)
    if (isBus):
        print("YES")

    else:
        print("NO" )

# Driver code

# Graph 1
V, E = 5, 4
adj1 = [[] for i in range(V + 1)]
addEdge(adj1, 1, 2)
addEdge(adj1, 1, 3)
addEdge(adj1, 3, 4)
addEdge(adj1, 4, 5)
checkBusTopology(adj1, V, E)

# Graph 2
V, E = 4, 4
adj2 = [[] for i in range(V + 1)]
addEdge(adj2, 1, 2)
addEdge(adj2, 1, 3)
addEdge(adj2, 3, 4)
addEdge(adj2, 4, 2)
checkBusTopology(adj2, V, E)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to check if the given graph
// represents a bus topology
using System;
using System.Collections.Generic;

public class GFG{

  // A utility function to add an edge in an
  // undirected graph.
  static void addEdge(List<List<int>> adj, int u, int v)
  {
    adj[u].Add(v);
    adj[v].Add(u);
  }

  // A utility function to print the adjacency list
  // representation of graph
  static void printGraph(List<List<int>> adj, int V)
  {
    for (int v = 0; v < V; ++v)
    {
      Console.WriteLine("\n Adjacency list of vertex " + v + "\n head ");
      foreach (int x in adj[v])
      {
        Console.Write( "-> " + x);
      }
      Console.WriteLine();
    }
  }

  /* Function to return true if the graph represented
    by the adjacency list represents a bus topology
    else return false */
    static bool checkBusTopologyUtil(List<List<int>> adj, int V, int E)
    {
        // Number of edges should be equal
        // to (Number of vertices - 1)
        if (E != (V - 1))
        {
            return false;
        }
        // a single node is termed as a bus topology
    if (V == 1)
    {
      return true;
    }
    int[] vertexDegree = new int[V + 1];

    // calculate the degree of each vertex
    for (int i = 1; i <= V; i++)
    {
      foreach (int v in adj[i])
      {
        vertexDegree[v]++;
      }
    }

    // countDegree2 - number of vertices with degree 2
    // countDegree1 - number of vertices with degree 1
    int countDegree2 = 0, countDegree1 = 0;

    for (int i = 1; i <= V; i++)
    {
      if (vertexDegree[i] == 2)
      {
        countDegree2++;
      }
      else if (vertexDegree[i] == 1)
      {
        countDegree1++;
      }
      else
      {

        // if any node has degree other
        // than 1 or 2, it is
        // NOT a bus topology
        return false;
      }
    }

    // if both necessary conditions as discussed,
    // satisfy return true
    if (countDegree1 == 2 && countDegree2 == (V - 2))
    {
      return true;
    }
    return false;
    }

    // Function to check if the graph represents a bus topology
    static void checkBusTopology(List<List<int>> adj, int V, int E)
    {
        bool isBus = checkBusTopologyUtil(adj, V, E);
        if (isBus)
        {
            Console.WriteLine("YES");
        }
        else
        {
        Console.WriteLine("NO");
    }
  }

  // Driver code
    static public void Main ()
    {

        // Graph 1
        int V = 5, E = 4;
        List<List<int>> adj1 = new List<List<int>>();
        for(int i = 0; i < V + 1; i++)
        {
            adj1.Add(new List<int>());
        }
        addEdge(adj1, 1, 2);
        addEdge(adj1, 1, 3);
        addEdge(adj1, 3, 4);
        addEdge(adj1, 4, 5);
        checkBusTopology(adj1, V, E);

        // Graph 2
        V = 4;
        E = 4;
        List<List<int>> adj2 = new List<List<int>>();
        for(int i = 0; i < V + 1; i++)
        {
            adj2.Add(new List<int>());
        }
        addEdge(adj2, 1, 2);
        addEdge(adj2, 1, 3);
        addEdge(adj2, 3, 4);
        addEdge(adj2, 4, 2);
        checkBusTopology(adj2, V, E);
    }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// JavaScript program to check if the given graph
// represents a bus topology

 // A utility function to add an edge in an
  // undirected graph.
function addEdge(adj,u,v)
{
    adj[u].push(v);
    adj[v].push(u);
}

 // A utility function to print the adjacency list
  // representation of graph
function printGraph(adj,V)
{
    for (let v = 0; v < V; ++v)
    {
      document.write("\n Adjacency list of vertex " +
      v + "\n head ");
      for (let x=0;x<adj[v].length;x++)
      {
        document.write( "-> " + adj[v][x]);
      }
      document.write("<br>");
    }
}

/* Function to return true if the graph represented
    by the adjacency list represents a bus topology
    else return false */
function checkBusTopologyUtil(adj,V,E)
{
    // Number of edges should be equal
    // to (Number of vertices - 1)
    if (E != (V - 1))
    {
      return false;
    }

    // a single node is termed as a bus topology
    if (V == 1)
    {
      return true;
    }
    let vertexDegree = new Array(V + 1);
     for(let i=0;i<vertexDegree.length;i++)
    {
        vertexDegree[i]=0;
    }
    // calculate the degree of each vertex
    for (let i = 1; i <= V; i++)
    {
      for (let v=0;v<adj[i].length;v++)
      {
        vertexDegree[adj[i][v]]++;
      }
    }

    // countDegree2 - number of vertices with degree 2
    // countDegree1 - number of vertices with degree 1
    let countDegree2 = 0, countDegree1 = 0;

    for (let i = 1; i <= V; i++)
    {
      if (vertexDegree[i] == 2)
      {
        countDegree2++;
      }
      else if (vertexDegree[i] == 1)
      {
        countDegree1++;
      }
      else
      {

        // if any node has degree other
        // than 1 or 2, it is
        // NOT a bus topology
        return false;
      }
    }

    // if both necessary conditions as discussed,
    // satisfy return true
    if (countDegree1 == 2 && countDegree2 == (V - 2))
    {
      return true;
    }
    return false;
}

// Function to check if the graph represents a bus topology
function checkBusTopology(adj,V,E)
{
    let isBus = checkBusTopologyUtil(adj, V, E);
    if (isBus)
    {
      document.write("YES<br>");
    }
    else
    {
      document.write("NO<br>");
    }
}

// Driver code

// Graph 1
    let V = 5, E = 4;
    let adj1=[];
    for(let i = 0; i < V + 1; i++)
    {
      adj1.push([]);
    }
    addEdge(adj1, 1, 2);
    addEdge(adj1, 1, 3);
    addEdge(adj1, 3, 4);
    addEdge(adj1, 4, 5);
    checkBusTopology(adj1, V, E);

    // Graph 2
    V = 4;
    E = 4;
    let adj2 = [];
    for(let i = 0; i < (V + 1); i++)
    {
      adj2.push([]);
    }
    addEdge(adj2, 1, 2);
    addEdge(adj2, 1, 3);
    addEdge(adj2, 3, 4);
    addEdge(adj2, 4, 2);
    checkBusTopology(adj2, V, E);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
YES
NO
```

**时间复杂度:** O(E)，其中 E 为图中的边数。
**辅助空间** : O(1)。