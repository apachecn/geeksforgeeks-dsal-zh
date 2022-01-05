# 使用 BFS 计数树中给定级别的节点数。

> 原文:[https://www . geesforgeks . org/count-number-nodes-给定级别-use-bfs/](https://www.geeksforgeeks.org/count-number-nodes-given-level-using-bfs/)

给定一个表示为无向图的树。计算给定级别 l 的节点数。可以假设顶点 0 是树的根。

**示例:**

```
Input :   7
          0 1
          0 2
          1 3
          1 4 
          1 5
          2 6
          2
Output :  4

Input : 6
        0 1
        0 2
        1 3
        2 4
        2 5
        2
Output : 3
```

[BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 是一种遍历算法，从选定的节点(源或起始节点)开始遍历，并逐层遍历图形，从而探索相邻节点(直接连接到源节点的节点)。然后，向下一级邻居节点移动。
顾名思义，遍历图广度如下:
**1。**首先水平移动，访问当前图层的所有节点。
**2。**移至下一层。

在这段代码中，当访问每个节点时，该节点的级别设置为其父节点级别的增量，即级别[子] =级别[父] + 1。每个节点的级别就是这样确定的。根节点位于树中的零级。

**说明:**

```
     0         Level 0
   /   \ 
  1     2      Level 1
/ |\    |
3 4 5   6      Level 2
```

给定一棵有 7 个节点和 6 条边的树，其中节点 0 位于 0 级。级别 1 可以更新为:级别[1] =级别[0] +1，因为 0 是 1 的父节点。类似地，其他节点的级别可以通过在其父节点的级别上添加 1 来更新。
level[2] = level[0] + 1，即 level[2] = 0 + 1 = 1。
等级[3] =等级[1] + 1，即等级[3] = 1 + 1 = 2。
等级[4] =等级[1] + 1，即等级[4] = 1 + 1 = 2。
等级[5] =等级[1] + 1，即等级[5] = 1 + 1 = 2。
等级[6] =等级[2] + 1，即等级[6] = 1 + 1 = 2。
那么，处于级别 l(即 l=2)的节点数的计数是 4(节点:- 3，4，5，6)

## C++

```
// C++ Program to print
// count of nodes
// at given level.
#include <iostream>
#include <list>

using namespace std;

// This class represents
// a directed graph
// using adjacency
// list representation
class Graph {
    // No. of vertices
    int V;

    // Pointer to an
    // array containing
    // adjacency lists
    list<int>* adj;

public:
    // Constructor
    Graph(int V);

    // function to add
    // an edge to graph
    void addEdge(int v, int w);

    // Returns count of nodes at
    // level l from given source.
    int BFS(int s, int l);
};

Graph::Graph(int V)
{
    this->V = V;
    adj = new list<int>[V];
}

void Graph::addEdge(int v, int w)
{
    // Add w to v’s list.
    adj[v].push_back(w);

    // Add v to w's list.
    adj[w].push_back(v);
}

int Graph::BFS(int s, int l)
{
    // Mark all the vertices
    // as not visited
    bool* visited = new bool[V];
    int level[V];

    for (int i = 0; i < V; i++) {
        visited[i] = false;
        level[i] = 0;
    }

    // Create a queue for BFS
    list<int> queue;

    // Mark the current node as
    // visited and enqueue it
    visited[s] = true;
    queue.push_back(s);
    level[s] = 0;

    while (!queue.empty()) {

        // Dequeue a vertex from
        // queue and print it
        s = queue.front();
        queue.pop_front();

        // Get all adjacent vertices
        // of the dequeued vertex s.
        // If a adjacent has not been
        // visited, then mark it
        // visited and enqueue it
        for (auto i = adj[s].begin();
                  i != adj[s].end(); ++i) {
            if (!visited[*i]) {

                // Setting the level
                // of each node with
                // an increment in the
                // level of parent node
                level[*i] = level[s] + 1;
                visited[*i] = true;
                queue.push_back(*i);
            }
        }
    }

    int count = 0;
    for (int i = 0; i < V; i++)
        if (level[i] == l)
            count++;   
    return count; 
}

// Driver program to test
// methods of graph class
int main()
{
    // Create a graph given
    // in the above diagram
    Graph g(6);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);
    g.addEdge(2, 5);

    int level = 2;

    cout << g.BFS(0, level);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print
// count of nodes
// at given level.
import java.util.*;

// This class represents
// a directed graph
// using adjacency
// list representation
class Graph
{

  // No. of vertices
  int V;

  // Pointer to an
  // array containing
  // adjacency lists
  Vector<Integer>[] adj;

  // Constructor
  @SuppressWarnings("unchecked")
  Graph(int V)
  {
    adj = new Vector[V];
    for (int i = 0; i < adj.length; i++)
    {
      adj[i] = new Vector<>();
    }
    this.V = V;
  }

  void addEdge(int v, int w)
  {

    // Add w to v’s list.
    adj[v].add(w);

    // Add v to w's list.
    adj[w].add(v);
  }

  int BFS(int s, int l)
  {

    // Mark all the vertices
    // as not visited
    boolean[] visited = new boolean[V];
    int[] level = new int[V];

    for (int i = 0; i < V; i++)
    {
      visited[i] = false;
      level[i] = 0;
    }

    // Create a queue for BFS
    Queue<Integer> queue = new LinkedList<>();

    // Mark the current node as
    // visited and enqueue it
    visited[s] = true;
    queue.add(s);
    level[s] = 0;
    int count = 0;
    while (!queue.isEmpty())
    {

      // Dequeue a vertex from
      // queue and print it
      s = queue.peek();
      queue.poll();

      Vector<Integer> list = adj[s];
      // Get all adjacent vertices
      // of the dequeued vertex s.
      // If a adjacent has not been
      // visited, then mark it
      // visited and enqueue it
      for (int i : list)
      {
        if (!visited[i])
        {
          visited[i] = true;
          level[i] = level[s] + 1;
          queue.add(i);
        }
      }

      count = 0;
      for (int i = 0; i < V; i++)
        if (level[i] == l)
          count++;
    }
    return count;
  }
}
class GFG {

  // Driver code
  public static void main(String[] args)
  {

    // Create a graph given
    // in the above diagram
    Graph g = new Graph(6);
    g.addEdge(0, 1);
    g.addEdge(0, 2);
    g.addEdge(1, 3);
    g.addEdge(2, 4);
    g.addEdge(2, 5);
    int level = 2;
    System.out.print(g.BFS(0, level));
  }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to print
# count of nodes at given level.
from collections import deque

adj = [[] for i in range(1001)]

def addEdge(v, w):

    # Add w to v’s list.
    adj[v].append(w)

    # Add v to w's list.
    adj[w].append(v)

def BFS(s, l):

    V = 100

    # Mark all the vertices
    # as not visited
    visited = [False] * V
    level = [0] * V

    for i in range(V):
        visited[i] = False
        level[i] = 0

    # Create a queue for BFS
    queue = deque()

    # Mark the current node as
    # visited and enqueue it
    visited[s] = True
    queue.append(s)
    level[s] = 0

    while (len(queue) > 0):

        # Dequeue a vertex from
        # queue and print
        s = queue.popleft()
        #queue.pop_front()

        # Get all adjacent vertices
        # of the dequeued vertex s.
        # If a adjacent has not been
        # visited, then mark it
        # visited and enqueue it
        for i in adj[s]:
            if (not visited[i]):

                # Setting the level
                # of each node with
                # an increment in the
                # level of parent node
                level[i] = level[s] + 1
                visited[i] = True
                queue.append(i)

    count = 0
    for i in range(V):
        if (level[i] == l):
            count += 1

    return count

# Driver code
if __name__ == '__main__':

    # Create a graph given
    # in the above diagram
    addEdge(0, 1)
    addEdge(0, 2)
    addEdge(1, 3)
    addEdge(2, 4)
    addEdge(2, 5)

    level = 2

    print(BFS(0, level))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print count of nodes
// at given level.
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

// This class represents
// a directed graph
// using adjacency
// list representation
class Graph{

// No. of vertices    
private int _V;

LinkedList<int>[] _adj;

public Graph(int V)
{
    _adj = new LinkedList<int>[V];

    for(int i = 0; i < _adj.Length; i++)
    {
        _adj[i] = new LinkedList<int>();
    }
    _V = V;
}

public void AddEdge(int v, int w)
{

    // Add w to v’s list.
    _adj[v].AddLast(w);
}

public int BreadthFirstSearch(int s,int l)
{

    // Mark all the vertices
    // as not visited
    bool[] visited = new bool[_V];
    int[] level = new int[_V];

    for(int i = 0; i < _V; i++)
    {
        visited[i] = false;
        level[i] = 0;
    }

    // Create a queue for BFS
    LinkedList<int> queue = new LinkedList<int>();

    // Mark the current node as
    // visited and enqueue it
    visited[s] = true;
    level[s] = 0;
    queue.AddLast(s);        

    while(queue.Any())
    {

        // Dequeue a vertex from
        // queue and print it
        s = queue.First();

        // Console.Write( s + " " );
        queue.RemoveFirst();

        LinkedList<int> list = _adj[s];

        foreach(var val in list)            
        {
            if (!visited[val])
            {
                visited[val] = true;
                level[val] = level[s] + 1;
                queue.AddLast(val);
            }
        }
    }

    int count = 0;
    for(int i = 0; i < _V; i++)
        if (level[i] == l)
            count++;

    return count;
}
}

// Driver code
class GFG{

static void Main(string[] args)
{

    // Create a graph given
    // in the above diagram
    Graph g = new Graph(6);

    g.AddEdge(0, 1);
    g.AddEdge(0, 2);
    g.AddEdge(1, 3);
    g.AddEdge(2, 4);
    g.AddEdge(2, 5);

    int level = 2;

    Console.WriteLine(g.BreadthFirstSearch(0, level));
}
}

// This code is contributed by anvudemy1
```

## java 描述语言

```
<script>

// JavaScript Program to print
// count of nodes
// at given level.

    let V;
   // Pointer to an
  // array containing
 // adjacency lists
    let adj=new Array(1001);
    for(let i=0;i<adj.length;i++)
    {
        adj[i]=[];
    }

    function addEdge(v,w)
    {
    // Add w to v’s list.
    adj[v].push(w);

    // Add v to w's list.
    adj[w].push(v);
    }

    function BFS(s,l)
    {
        V=100;
     // Mark all the vertices
    // as not visited
    let visited = new Array(V);
    let level = new Array(V);

    for (let i = 0; i < V; i++)
    {
      visited[i] = false;
      level[i] = 0;
    }

    // Create a queue for BFS
    let queue = [];

    // Mark the current node as
    // visited and enqueue it
    visited[s] = true;
    queue.push(s);
    level[s] = 0;
    let count = 0;
    while (queue.length!=0)
    {

      // Dequeue a vertex from
      // queue and print it
      s = queue[0];
      queue.shift();

      let list = adj[s];
      // Get all adjacent vertices
      // of the dequeued vertex s.
      // If a adjacent has not been
      // visited, then mark it
      // visited and enqueue it
      for (let i=0;i<list.length;i++)
      {
        if (!visited[list[i]])
        {
          visited[list[i]] = true;
          level[list[i]] = level[s] + 1;
          queue.push(list[i]);
        }
      }

      count = 0;
      for (let i = 0; i < V; i++)
        if (level[i] == l)
          count++;
    }
    return count;
  }

// Driver code

// Create a graph given
    // in the above diagram
addEdge(0, 1)
addEdge(0, 2)
addEdge(1, 3)
addEdge(2, 4)
addEdge(2, 5)

let level = 2;
document.write(BFS(0, level));

// This code is contributed by unknown2108

</script>
```

**输出:**

```
 3
```