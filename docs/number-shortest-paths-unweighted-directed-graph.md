# 未加权有向图中最短路径的数量

> 原文:[https://www . geesforgeks . org/number-最短路径-未加权-有向图/](https://www.geeksforgeeks.org/number-shortest-paths-unweighted-directed-graph/)

给定一个未加权的有向图，它可以是循环的或非循环的。打印从给定顶点到每个顶点的最短路径数。例如，考虑下图。顶点 0 到顶点 0 有一条最短路径(从每个顶点到自身都有一条最短路径)，顶点 0 到顶点 2 (0->2)有一条最短路径，从顶点 0 到顶点 6 有 4 条不同的最短路径:
1。0- > 1- > 3- > 4- > 6
2。0->1->3->5->6
3。0->2->3->4->6
4。0->2->3->5->6

![](img/2957de24448a243ad1993424b59e0978.png)

想法是用 [BFS](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/) 。我们使用两个称为 dist[]和 path[]的数组，dist[]表示从源顶点到每个顶点的最短距离，path[]表示从源顶点到每个顶点的不同最短路径的数量。最初，dist[]中的所有元素除了源顶点等于 0 之外都是无穷大，因为到源顶点的距离本身是 0，路径[]中的所有元素除了源顶点等于 1 之外都是 0，因为每个顶点都有一条到自身的最短路径。之后，我们开始使用 BFS 方式遍历图表。
然后，对于每个顶点 X 的每个邻居 Y，做:
1)如果 dist[Y] > dist[X]+1，则将 dist[Y]减少到 dist[X]+1，并将顶点 X 的路径数分配给顶点 Y 的路径数。
2)否则，如果 dist[Y] = dist[X] + 1，则将顶点 X 的路径数与顶点 Y 的路径数相加。
例如:
让我们看一下下图。源顶点为 0。假设我们在顶点 2 上遍历，我们检查它的所有邻居，只有 3 个，因为当我们遍历顶点 1，dist[3] = 2 和路径[3] = 1 时，已经访问了顶点 3。第二个条件为真，所以意味着找到了额外的最短路径，所以我们把顶点 3 的路径数加上顶点 2 的路径数。
当我们在顶点 5 上遍历时，会出现相同的情况:

![](img/1a7ade280bb2d188f22f2de91cda7c74.png)

## C++

```
// CPP program to count number of shortest
// paths from a given source to every other
// vertex using BFS.
#include <bits/stdc++.h>
using namespace std;

// Traverses graph in BFS manner. It fills
// dist[] and paths[]
void BFS(vector<int> adj[], int src, int dist[],
                           int paths[], int n)
{
    bool visited[n];
    for (int i = 0; i < n; i++)
        visited[i] = false;
    dist[src] = 0;
    paths[src] = 1;

    queue <int> q;
    q.push(src);
    visited[src] = true;
    while (!q.empty())
    {
        int curr = q.front();
        q.pop();

        // For all neighbors of current vertex do:
        for (auto x : adj[curr])
        {
            // if the current vertex is not yet
            // visited, then push it to the queue.
            if (visited[x] == false)
            {
                q.push(x);
                visited[x] = true;
            }

            // check if there is a better path.
            if (dist[x] > dist[curr] + 1)
            {
                dist[x] = dist[curr] + 1;
                paths[x] = paths[curr];
            }

            // additional shortest paths found
            else if (dist[x] == dist[curr] + 1)
                paths[x] += paths[curr];
        }
    }
}

// function to find number of different
// shortest paths form given vertex s.
// n is number of vertices.
void findShortestPaths(vector<int> adj[],
                       int s, int n)
{
    int dist[n], paths[n];
    for (int i = 0; i < n; i++)
        dist[i] = INT_MAX;
    for (int i = 0; i < n; i++)
        paths[i] = 0;
    BFS(adj, s, dist, paths, n);
    cout << "Numbers of shortest Paths are: ";
    for (int i = 0; i < n; i++)
        cout << paths[i] << " ";
}

// A utility function to add an edge in a
// directed graph.
void addEdge(vector<int> adj[], int u, int v)
{
    adj[u].push_back(v);
}

// Driver code
int main()
{
    int n = 7; // Number of vertices
    vector <int> adj[n];
    addEdge(adj, 0, 1);
    addEdge(adj, 0, 2);
    addEdge(adj, 1, 2);
    addEdge(adj, 1, 3);
    addEdge(adj, 2, 3);
    addEdge(adj, 3, 4);
    addEdge(adj, 3, 5);
    addEdge(adj, 4, 6);
    addEdge(adj, 5, 6);
    findShortestPaths(adj, 0, 7);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of shortest
// paths from a given source to every other
// vertex using BFS.
import java.io.*;
import java.util.*;

class GFG
{

    // Traverses graph in BFS manner.
    // It fills dist[] and paths[]
    static void BFS(Vector<Integer>[] adj, int src,
                  int dist[], int paths[], int n)
    {
        boolean[] visited = new boolean[n];
        for (int i = 0; i < n; i++)
            visited[i] = false;
        dist[src] = 0;
        paths[src] = 1;

        Queue<Integer> q = new LinkedList<>();
        q.add(src);
        visited[src] = true;
        while (!q.isEmpty())
        {
            int curr = q.peek();
            q.poll();

            // For all neighbors of current vertex do:
            for (int x : adj[curr])
            {

                // if the current vertex is not yet
                // visited, then push it to the queue.
                if (visited[x] == false)
                {
                    q.add(x);
                    visited[x] = true;
                }

                // check if there is a better path.
                if (dist[x] > dist[curr] + 1)
                {
                    dist[x] = dist[curr] + 1;
                    paths[x] = paths[curr];
                }

                // additional shortest paths found
                else if (dist[x] == dist[curr] + 1)
                    paths[x] += paths[curr];
            }
        }
    }

    // function to find number of different
    // shortest paths form given vertex s.
    // n is number of vertices.
    static void findShortestPaths(Vector<Integer> adj[],
                                           int s, int n)
    {
        int[] dist = new int[n], paths = new int[n];

        for (int i = 0; i < n; i++)
            dist[i] = Integer.MAX_VALUE;

        for (int i = 0; i < n; i++)
            paths[i] = 0;

        BFS(adj, s, dist, paths, n);

        System.out.print("Numbers of shortest Paths are: ");
        for (int i = 0; i < n; i++)
            System.out.print(paths[i] + " ");
    }

    // A utility function to add an edge in a
    // directed graph.
    static void addEdge(Vector<Integer> adj[],
                                 int u, int v)
    {
        adj[u].add(v);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 7; // Number of vertices

        Vector<Integer>[] adj = new Vector[n];
        for (int i = 0; i < n; i++)
            adj[i] = new Vector<>();

        addEdge(adj, 0, 1);
        addEdge(adj, 0, 2);
        addEdge(adj, 1, 2);
        addEdge(adj, 1, 3);
        addEdge(adj, 2, 3);
        addEdge(adj, 3, 4);
        addEdge(adj, 3, 5);
        addEdge(adj, 4, 6);
        addEdge(adj, 5, 6);
        findShortestPaths(adj, 0, 7);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to count number of shortest
# paths from a given source to every other
# vertex using BFS.
from collections import deque
from sys import maxsize as INT_MAX

# Traverses graph in BFS manner. It fills
# dist[] and paths[]
def BFS(adj: list, src: int, dist: list, paths: list, n: int):
    visited = [False] * n
    dist[src] = 0
    paths[src] = 1

    q = deque()
    q.append(src)
    visited[src] = True
    while q:
        curr = q[0]
        q.popleft()

        # For all neighbors of current vertex do:
        for x in adj[curr]:

            # if the current vertex is not yet
            # visited, then push it to the queue.
            if not visited[x]:
                q.append(x)
                visited[x] = True

            # check if there is a better path.
            if dist[x] > dist[curr] + 1:
                dist[x] = dist[curr] + 1
                paths[x] = paths[curr]

            # additional shortest paths found
            elif dist[x] == dist[curr] + 1:
                paths[x] += paths[curr]

# function to find number of different
# shortest paths form given vertex s.
# n is number of vertices.
def findShortestPaths(adj: list, s: int, n: int):
    dist = [INT_MAX] * n
    paths = [0] * n
    BFS(adj, s, dist, paths, n)
    print("Numbers of shortest Paths are:", end=" ")
    for i in paths:
        print(i, end=" ")

# A utility function to add an edge in a
# directed graph.
def addEdge(adj: list, u: int, v: int):
    adj[u].append(v)

# Driver Code
if __name__ == "__main__":

    n = 7 # Number of vertices
    adj = [0] * n
    for i in range(n):
        adj[i] = []
    addEdge(adj, 0, 1)
    addEdge(adj, 0, 2)
    addEdge(adj, 1, 2)
    addEdge(adj, 1, 3)
    addEdge(adj, 2, 3)
    addEdge(adj, 3, 4)
    addEdge(adj, 3, 5)
    addEdge(adj, 4, 6)
    addEdge(adj, 5, 6)
    findShortestPaths(adj, 0, 7)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to count number of shortest
// paths from a given source to every other
// vertex using BFS.
using System;
using System.Collections.Generic;

class GFG
{

    // Traverses graph in BFS manner.
    // It fills dist[] and paths[]
    static void BFS(List<int>[] adj, int src,
                int []dist, int []paths, int n)
    {
        bool[] visited = new bool[n];
        for (int i = 0; i < n; i++)
            visited[i] = false;
        dist[src] = 0;
        paths[src] = 1;

        List<int> q = new List<int>();
        q.Add(src);
        visited[src] = true;
        while (q.Count != 0)
        {
            int curr = q[0];
            q.RemoveAt(0);

            // For all neighbors of current vertex do:
            foreach (int x in adj[curr])
            {

                // if the current vertex is not yet
                // visited, then push it to the queue.
                if (visited[x] == false)
                {
                    q.Add(x);
                    visited[x] = true;
                }

                // check if there is a better path.
                if (dist[x] > dist[curr] + 1)
                {
                    dist[x] = dist[curr] + 1;
                    paths[x] = paths[curr];
                }

                // additional shortest paths found
                else if (dist[x] == dist[curr] + 1)
                    paths[x] += paths[curr];
            }
        }
    }

    // function to find number of different
    // shortest paths form given vertex s.
    // n is number of vertices.
    static void findShortestPaths(List<int> []adj,
                                        int s, int n)
    {
        int[] dist = new int[n], paths = new int[n];

        for (int i = 0; i < n; i++)
            dist[i] = int.MaxValue;

        for (int i = 0; i < n; i++)
            paths[i] = 0;

        BFS(adj, s, dist, paths, n);

        Console.Write("Numbers of shortest Paths are: ");
        for (int i = 0; i < n; i++)
            Console.Write(paths[i] + " ");
    }

    // A utility function to add an edge in a
    // directed graph.
    static void addEdge(List<int> []adj,
                                int u, int v)
    {
        adj[u].Add(v);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 7; // Number of vertices

        List<int>[] adj = new List<int>[n];
        for (int i = 0; i < n; i++)
            adj[i] = new List<int>();

        addEdge(adj, 0, 1);
        addEdge(adj, 0, 2);
        addEdge(adj, 1, 2);
        addEdge(adj, 1, 3);
        addEdge(adj, 2, 3);
        addEdge(adj, 3, 4);
        addEdge(adj, 3, 5);
        addEdge(adj, 4, 6);
        addEdge(adj, 5, 6);
        findShortestPaths(adj, 0, 7);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to count number of shortest
// paths from a given source to every other
// vertex using BFS.

// Traverses graph in BFS manner.
    // It fills dist[] and paths[]
function  BFS(adj,src,dist,paths,n)
{
    let visited = new Array(n);
        for (let i = 0; i < n; i++)
            visited[i] = false;
        dist[src] = 0;
        paths[src] = 1;

        let q = [];
        q.push(src);
        visited[src] = true;
        while (q.length!=0)
        {
            let curr = q[0];
            q.shift();

            // For all neighbors of current vertex do:
            for (let x of adj[curr].values())
            {

                // if the current vertex is not yet
                // visited, then push it to the queue.
                if (visited[x] == false)
                {
                    q.push(x);
                    visited[x] = true;
                }

                // check if there is a better path.
                if (dist[x] > dist[curr] + 1)
                {
                    dist[x] = dist[curr] + 1;
                    paths[x] = paths[curr];
                }

                // additional shortest paths found
                else if (dist[x] == dist[curr] + 1)
                    paths[x] += paths[curr];
            }
        }
}

// function to find number of different
    // shortest paths form given vertex s.
    // n is number of vertices.
function findShortestPaths(adj,s,n)
{
    let dist = new Array(n), paths = new Array(n);

        for (let i = 0; i < n; i++)
            dist[i] = Number.MAX_VALUE;

        for (let i = 0; i < n; i++)
            paths[i] = 0;

        BFS(adj, s, dist, paths, n);

        document.write("Numbers of shortest Paths are: ");
        for (let i = 0; i < n; i++)
            document.write(paths[i] + " ");
}

// A utility function to add an edge in a
    // directed graph.
function addEdge(adj,u,v)
{
    adj[u].push(v);
}

// Driver Code
let n = 7; // Number of vertices

let adj = new Array(n);
for (let i = 0; i < n; i++)
    adj[i] = [];

addEdge(adj, 0, 1);
addEdge(adj, 0, 2);
addEdge(adj, 1, 2);
addEdge(adj, 1, 3);
addEdge(adj, 2, 3);
addEdge(adj, 3, 4);
addEdge(adj, 3, 5);
addEdge(adj, 4, 6);
addEdge(adj, 5, 6);
findShortestPaths(adj, 0, 7);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Numbers of shortest Paths are: 1 1 1 2 2 2 4
```

**时间复杂度:O(V + E)**