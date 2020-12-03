# 图

的两个顶点之间的最小边数

> 原文： [https://www.geeksforgeeks.org/minimum-number-of-edges-between-two-vertices-of-a-graph/](https://www.geeksforgeeks.org/minimum-number-of-edges-between-two-vertices-of-a-graph/)

您将获得一个具有 N 个顶点和 M 个边的无向图 G（V，E）。 我们需要找到给定的一对顶点（u，v）之间的最小边数。

**示例**：

```
Input : For given graph G. Find minimum number
        of edges between (1, 5).
```

![](img/3b5b85b2d29e360f2965840445327224.png)

```
Output : 2
Explanation: (1, 2) and (2, 5) are the only
edges resulting into shortest path between 1
and 5.
```

这个想法是从给定的输入顶点（u）之一执行 BFS。 在执行 BFS 时，请维护一个 distance [n]数组，并将其对所有顶点初始化为零。 现在，假设在 BFS 期间，顶点 x 从队列中弹出，并且我们将所有相邻的未访问顶点（i）推回队列，同时我们应该更新 **distance [i] = distance [x] + 1;** 。

最后，distance [v]给出 u 和 v 之间的最小边数。

**算法**：

```
int minEdgeBFS(int u, int v, int n)
{
    // visited[n] for keeping track of visited
    // node in BFS
    bool visited[n] = {0};

    // Initialize distances as 0
    int distance[n] = {0};

    // queue to do BFS.
    queue  Q;
    distance[u] = 0;

    Q.push(u);
    visited[u] = true;
    while (!Q.empty())
    {
        int x = Q.front();
        Q.pop();

        for (int i=0; i<edges[x].size(); i++)
        {
            if (visited[edges[x][i]])
                continue;

            // update distance for i
            distance[edges[x][i]] = distance[x] + 1;
            Q.push(edges[x][i]);
            visited[edges[x][i]] = 1;
        }
    }
    return distance[v];
}
```

## C++

```cpp

// C++ program to find minimum edge
// between given two vertex of Graph
#include<bits/stdc++.h>
using namespace std;

// function for finding minimum no. of edge
// using BFS
int minEdgeBFS(vector <int> edges[], int u,
                              int v, int n)
{
    // visited[n] for keeping track of visited
    // node in BFS
    vector<bool> visited(n, 0);

    // Initialize distances as 0
    vector<int> distance(n, 0);

    // queue to do BFS.
    queue <int> Q;
    distance[u] = 0;

    Q.push(u);
    visited[u] = true;
    while (!Q.empty())
    {
        int x = Q.front();
        Q.pop();

        for (int i=0; i<edges[x].size(); i++)
        {
            if (visited[edges[x][i]])
                continue;

            // update distance for i
            distance[edges[x][i]] = distance[x] + 1;
            Q.push(edges[x][i]);
            visited[edges[x][i]] = 1;
        }
    }
    return distance[v];
}

// function for addition of edge
void addEdge(vector <int> edges[], int u, int v)
{
   edges[u].push_back(v);
   edges[v].push_back(u);
}

// Driver function
int main()
{
    // To store adjacency list of graph
    int n = 9;
    vector <int> edges[9];
    addEdge(edges, 0, 1);
    addEdge(edges, 0, 7);
    addEdge(edges, 1, 7);
    addEdge(edges, 1, 2);
    addEdge(edges, 2, 3);
    addEdge(edges, 2, 5);
    addEdge(edges, 2, 8);
    addEdge(edges, 3, 4);
    addEdge(edges, 3, 5);
    addEdge(edges, 4, 5);
    addEdge(edges, 5, 6);
    addEdge(edges, 6, 7);
    addEdge(edges, 7, 8);
    int u = 0;
    int v = 5;
    cout << minEdgeBFS(edges, u, v, n);
    return 0;
}

```

## Java

```java

// Java program to find minimum edge
// between given two vertex of Graph

import java.util.LinkedList;
import java.util.Queue;
import java.util.Vector;

class Test
{
    // Method for finding minimum no. of edge
    // using BFS
    static int minEdgeBFS(Vector <Integer> edges[], int u,
                                  int v, int n)
    {
        // visited[n] for keeping track of visited
        // node in BFS
        Vector<Boolean> visited = new Vector<Boolean>(n);

        for (int i = 0; i < n; i++) {
            visited.addElement(false);
        }

        // Initialize distances as 0
        Vector<Integer> distance = new Vector<Integer>(n);

        for (int i = 0; i < n; i++) {
            distance.addElement(0);
        }

        // queue to do BFS.
        Queue<Integer> Q = new LinkedList<>();
        distance.setElementAt(0, u);

        Q.add(u);
        visited.setElementAt(true, u);
        while (!Q.isEmpty())
        {
            int x = Q.peek();
            Q.poll();

            for (int i=0; i<edges[x].size(); i++)
            {
                if (visited.elementAt(edges[x].get(i)))
                    continue;

                // update distance for i
                distance.setElementAt(distance.get(x) + 1,edges[x].get(i));
                Q.add(edges[x].get(i));
                visited.setElementAt(true,edges[x].get(i));
            }
        }
        return distance.get(v);
    }

    // method for addition of edge
    static void addEdge(Vector <Integer> edges[], int u, int v)
    {
       edges[u].add(v);
       edges[v].add(u);
    }

    // Driver method
    public static void main(String args[])
    {
        // To store adjacency list of graph
        int n = 9;
        Vector <Integer> edges[] = new Vector[9];

        for (int i = 0; i < edges.length; i++) {
            edges[i] = new Vector<>();
        }

        addEdge(edges, 0, 1);
        addEdge(edges, 0, 7);
        addEdge(edges, 1, 7);
        addEdge(edges, 1, 2);
        addEdge(edges, 2, 3);
        addEdge(edges, 2, 5);
        addEdge(edges, 2, 8);
        addEdge(edges, 3, 4);
        addEdge(edges, 3, 5);
        addEdge(edges, 4, 5);
        addEdge(edges, 5, 6);
        addEdge(edges, 6, 7);
        addEdge(edges, 7, 8);
        int u = 0;
        int v = 5;
        System.out.println(minEdgeBFS(edges, u, v, n));
    }
}
// This code is contributed by Gaurav Miglani

```

## Python

```py

# Python3 program to find minimum edge 
# between given two vertex of Graph
import queue 

# function for finding minimum 
# no. of edge using BFS 
def minEdgeBFS(edges, u, v, n):

    # visited[n] for keeping track 
    # of visited node in BFS 
    visited = [0] * n 

    # Initialize distances as 0 
    distance = [0] * n

    # queue to do BFS. 
    Q = queue.Queue()
    distance[u] = 0

    Q.put(u) 
    visited[u] = True
    while (not Q.empty()):
        x = Q.get() 

        for i in range(len(edges[x])):
            if (visited[edges[x][i]]):
                continue

            # update distance for i 
            distance[edges[x][i]] = distance[x] + 1
            Q.put(edges[x][i]) 
            visited[edges[x][i]] = 1
    return distance[v]

# function for addition of edge 
def addEdge(edges, u, v):
    edges[u].append(v) 
    edges[v].append(u)

# Driver  Code
if __name__ == '__main__':

    # To store adjacency list of graph 
    n = 9
    edges = [[] for i in range(n)]
    addEdge(edges, 0, 1) 
    addEdge(edges, 0, 7) 
    addEdge(edges, 1, 7) 
    addEdge(edges, 1, 2) 
    addEdge(edges, 2, 3) 
    addEdge(edges, 2, 5) 
    addEdge(edges, 2, 8) 
    addEdge(edges, 3, 4) 
    addEdge(edges, 3, 5) 
    addEdge(edges, 4, 5) 
    addEdge(edges, 5, 6) 
    addEdge(edges, 6, 7) 
    addEdge(edges, 7, 8) 
    u = 0
    v = 5
    print(minEdgeBFS(edges, u, v, n))

# This code is contributed by PranchalK

```

## C#

```cs

// C# program to find minimum edge 
// between given two vertex of Graph 
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Method for finding minimum no. of edge 
// using BFS 
static int minEdgeBFS(ArrayList []edges, int u,
                                  int v, int n) 
{ 

    // visited[n] for keeping track of visited 
    // node in BFS 
    ArrayList visited = new ArrayList(); 
    for(int i = 0; i < n; i++)
    {
        visited.Add(false); 
    } 

    // Initialize distances as 0 
    ArrayList distance = new ArrayList(); 
    for(int i = 0; i < n; i++)
    {
        distance.Add(0); 
    } 

    // queue to do BFS. 
    Queue Q = new Queue(); 

    distance[u] = 0; 

    Q.Enqueue(u); 

    visited[u] = true;

    while (Q.Count != 0) 
    { 
        int x = (int)Q.Dequeue(); 

        for(int i = 0; i < edges[x].Count; i++) 
        { 
            if ((bool)visited[(int)edges[x][i]]) 
                continue; 

            // Update distance for i 
            distance[(int)edges[x][i]] = (int)distance[x] + 1; 
            Q.Enqueue((int)edges[x][i]); 
            visited[(int)edges[x][i]] = true; 
        } 
    } 
    return (int)distance[v]; 
} 

// Method for addition of edge 
static void addEdge(ArrayList []edges, 
                    int u, int v) 
{ 
    edges[u].Add(v); 
    edges[v].Add(u); 
} 

// Driver code
public static void Main(string []args) 
{ 

    // To store adjacency list of graph 
    int n = 9; 
    ArrayList []edges = new ArrayList[9]; 

    for(int i = 0; i < 9; i++) 
    {
        edges[i] = new ArrayList(); 
    } 

    addEdge(edges, 0, 1); 
    addEdge(edges, 0, 7); 
    addEdge(edges, 1, 7); 
    addEdge(edges, 1, 2); 
    addEdge(edges, 2, 3); 
    addEdge(edges, 2, 5); 
    addEdge(edges, 2, 8); 
    addEdge(edges, 3, 4); 
    addEdge(edges, 3, 5); 
    addEdge(edges, 4, 5); 
    addEdge(edges, 5, 6); 
    addEdge(edges, 6, 7); 
    addEdge(edges, 7, 8); 

    int u = 0; 
    int v = 5; 

    Console.Write(minEdgeBFS(edges, u, v, n)); 
} 
} 

// This code is contributed by rutvik_56

```

**输出**：

```
3
```

本文由 [Shivam Pradhan（anuj_charm）](https://www.facebook.com/anuj.charm)提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

