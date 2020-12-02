# 检查给定的树图是否为线性图

> 原文： [https://www.geeksforgeeks.org/check-if-a-given-tree-graph-is-linear-or-not/](https://www.geeksforgeeks.org/check-if-a-given-tree-graph-is-linear-or-not/)

给定一个树，检查它是否是线性的。

```
    1
  /    \
 2      3
 Linear as we can
 form a lime 2 1 3
```

```
    1
  /    \
 2      3
      /   \
     4     5
Not linear
```

**示例**：

```
Input : 3
1 2
1 3
Output :
YES
Explanation:
The Tree formed is 2-1-3 which is a linear one.

Input :
4
1 2
2 3
4 2
Output :
NO
```

**方法**：仅当 n-2 个节点的 indegree == 2 或节点数 n == 1 时，给定的树才是线性的。

## Java

```java

// A Java Program to check whether a graph is 
// Linear or not
import java.io.*;
import java.util.*;

// This class represents a undirected graph 
// using adjacency list representation
class Graph {
    private int V; // No. of vertices

    // Adjacency List
    private LinkedList<Integer> adj[];

    // Constructor
    Graph(int v)
    {
        V = v;
        adj = new LinkedList[v];
        for (int i = 0; i < v; ++i)
            adj[i] = new LinkedList<Integer>();
    }

    // Function to add an edge into the graph
    void addEdge(int v, int w)
    {
        adj[v].add(w);
        adj[w].add(v);
    }

    // Returns true if the graph is linear, 
    // else false.
    boolean isLinear()
    {
        // If the number of vertice is 1 then
        // the tree is always Linear
        if (V == 1)
            return true;
        int count = 0;

        // Counting the number of vertices
        // with indegree 2
        for (int i = 0; i < V; i++) {
            if (adj[i].size() == 2)
                count++;
        }
        if (count == V - 2)
            return true;
        else
            return false;
    }

    // Driver method
    public static void main(String args[])
    {
        // Create a graph given in the above example
        Graph g1 = new Graph(3);
        g1.addEdge(0, 1);
        g1.addEdge(0, 2);
        if (g1.isLinear())
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

```

## Python3

```

# A Python3 Program to check whether a 
# graph is Linear or not

# This class represents a undirected 
# graph using adjacency list representation
class Graph:

    def __init__(self, v):

          # No. of vertices
        self.V = v 

        # Adjacency List
        self.adj = [[] for i in range(v)]

    # Function to add an edge into
    # the graph
    def addEdge(self, v, w):

        self.adj[v].append(w)
        self.adj[w].append(v)

    # Returns true if the graph is 
    # linear, else false.
    def isLinear(self):

        # If the number of vertice is 
          # 1 then the tree is always Linear
        if (self.V == 1):
            return True

        count = 0

        # Counting the number of vertices
        # with indegree 2
        for i in range(self.V):
            if (len(self.adj[i]) == 2):
                count += 1

        if (count == self.V - 2):
            return True
        else:
            return False

# Driver code
if __name__=='__main__':

    # Create a graph given in the
    # above example
    g1 = Graph(3)
    g1.addEdge(0, 1)
    g1.addEdge(0, 2)

    if (g1.isLinear()):
        print("YES")
    else:
        print("NO")

# This code is contributed by rutvik_56

```

## C#

```cs

// A C# Program to check whether a graph is 
// Linear or not
using System;
using System.Collections.Generic;

// This class represents a undirected graph 
// using adjacency list representation
public class Graph 
{
    private int V; // No. of vertices

    // Adjacency List
    private List<int> []adj;

    // Constructor
    Graph(int v)
    {
        V = v;
        adj = new List<int>[v];
        for (int i = 0; i < v; ++i)
            adj[i] = new List<int>();
    }

    // Function to add an edge into the graph
    void addEdge(int v, int w)
    {
        adj[v].Add(w);
        adj[w].Add(v);
    }

    // Returns true if the graph is linear, 
    // else false.
    bool isLinear()
    {
        // If the number of vertice is 1 then
        // the tree is always Linear
        if (V == 1)
            return true;
        int count = 0;

        // Counting the number of vertices
        // with indegree 2
        for (int i = 0; i < V; i++) 
        {
            if (adj[i].Count == 2)
                count++;
        }
        if (count == V - 2)
            return true;
        else
            return false;
    }

    // Driver Code
    public static void Main(String []args)
    {
        // Create a graph given in the above example
        Graph g1 = new Graph(3);
        g1.addEdge(0, 1);
        g1.addEdge(0, 2);
        if (g1.isLinear())
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code is contributed by 29AjayKumar

```

**输出**：

```
YES
```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。