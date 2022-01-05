# 检查给定图形中是否存在从 U 到 V 的具有较小个体重量的替代路径

> 原文:[https://www . geesforgeks . org/check-if-alternate-path-exists-from-u-v-with-small-individual-weight-in-a-graph/](https://www.geeksforgeeks.org/check-if-alternate-path-exists-from-u-to-v-with-smaller-individual-weight-in-a-given-graph/)

给定一个有向加权图，图中有 **N** 个顶点和 **M** 条边以及一条边 **(U，V)** 。任务是发现从 **U** 到 **V** 是否存在交替路径，交替路径中边的个体权重小于直接路径的权重。如果存在打印**是**否则打印**否**。

**示例**

> 对于给定的有向图:
> 
> ![](img/cb3adeb8fc94faef663159cc0ac054d8.png)
> 
> **输入:** N = 7，M = 10，U = 3，V = 6。
> **输出:**否
> **说明:**
> 对于给定的边{3，6}，权重= 16。没有从 3 到 6 的替代路径。因此答案是否定的
> 
> **输入:** N = 7，M = 10，U = 1，V = 6。
> **输出:**是
> **解释:**
> = >对于给定的边{1，6}，权重= 5。
> = >从 1 = {1，5，6}到单个重量{12，2}大于 5 的 6 的交替路径。因此这条路不能考虑。
> = >从 1 = {1，2，4，5，6}到 6 的交替路径，单个权重{5，1，1，2}不小于 5。因此这条路不能考虑。
> = >从 1 = {1，4，5，6}到 6 的替代路径，单个权重{3，1，2}小于 5。因此这条路可以考虑。
> = >因此答案是肯定的

**进场:**

*   使用[深度优先搜索遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)遍历给定的[有向图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)和起始顶点 **U** 。
*   在 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/)期间，如果任何边的权重大于有向边，则该路径不包括在内。
*   如果我们到达顶点 **V** ，遍历路径中每条边的权重小于有向边的权重，则存在一条替代路径。
*   否则顶点 **U** 和顶点 **V** 之间除了直接路径没有路径。

下面是上述方法的实现:

## C++14

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Edge class
class Edge
{
    public:
        int u;
        int v;
        int w;

        // Edge constructor to
        // initialize edge (u, v) with
        // weight w
        Edge(int u, int v, int w)
        {
            this->u = u;
            this->v = v;
            this->w = w;
        }
};

class GFG{

public:

    // Array to mark already
    // visited vertices
    bool *visited;

    // Adjacency list representation
    // of the graph
    vector<Edge *> *graph;

    // GfG class constructor
    GFG(int size)
    {
        visited = new bool[size];
        graph = new vector<Edge *>[size];
    }

    // Depth First Search to traverse
    // all vertices with weight less
    // than weight of the dfs root
    void dfs(int S, int W)
    {

        // Marking the vertex visited
        visited[S] = true;

        // Traversing adjacent vertex
        for(Edge *uv : graph[S])
        {
            int ver = uv->v;
            int w = uv->w;

            if (!visited[ver] && w < W)
                dfs(ver, W);
        }
    }
};

// Driver code
int main()
{

    // Number of vertices
    int N = 7;

    // Number of edges
    int M = 10;

    // Edge to be checked
    int U_V[] = {3, 6};

    // Creating GfG object
    GFG *obj = new GFG(8);

    // Creating edges
    Edge *e0 = new Edge(1, 2, 5);
    Edge *e1 = new Edge(1, 4, 3);
    Edge *e2 = new Edge(1, 5, 12);
    Edge *e3 = new Edge(1, 6, 5);
    Edge *e4 = new Edge(4, 5, 1);
    Edge *e5 = new Edge(5, 6, 2);
    Edge *e6 = new Edge(5, 3, 1);
    Edge *e7 = new Edge(3, 6, 16);
    Edge *e8 = new Edge(4, 7, 1);
    Edge *e9 = new Edge(2, 4, 1);

    // Adding edges to the graph
    obj->graph[1].push_back(e0);
    obj->graph[1].push_back(e1);
    obj->graph[1].push_back(e2);
    obj->graph[1].push_back(e3);
    obj->graph[4].push_back(e4);
    obj->graph[5].push_back(e5);
    obj->graph[5].push_back(e6);
    obj->graph[3].push_back(e7);
    obj->graph[4].push_back(e8);
    obj->graph[2].push_back(e9);

    // DFS traversal from
    // vertex U
    obj->dfs(U_V[0], 16);

    // If there is alternate
    // path then print YES,
    // else NO
    if (obj->visited[U_V[1]])
    {
        cout << "NO" << endl;
    }
    else
    {
        cout << "YES" << endl;
    }
}

// This code is contributed by sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach

import java.util.*;

// To ignore the unchecked warning
@SuppressWarnings("unchecked")

// GfG class
public class GfG {

    // Array to mark already
    // visited vertices
    static private boolean visited[];

    // Adjacency list representation
    // of the graph
    static private ArrayList<Edge> graph[];

    // GfG class constructor
    public GfG(int size)
    {
        visited = new boolean[size];
        graph = new ArrayList[size];
    }

    // Edge class
    static class Edge {
        int u;
        int v;
        int w;

        // Edge constructor to
        // initialize edge (u, v) with
        // weight w
        Edge(int u, int v, int w)
        {
            this.u = u;
            this.v = v;
            this.w = w;
        }
    }

    // Helper method to
    // initialize graph
    static private void helperInitialize(int size)
    {
        for (int i = 0; i < size; i++) {
            graph[i] = new ArrayList<Edge>();
        }
    }

    // Depth First Search to traverse
    // all vertices with weight less
    // than weight of the dfs root
    static private void dfs(int S, int W)
    {

        // Marking the vertex visited
        visited[S] = true;

        // Traversing adjacent vertex
        for (Edge uv : graph[S]) {
            int ver = uv.v;
            int w = uv.w;
            if (!visited[ver] && w < W)
                dfs(ver, W);
        }
    }

    // Driver function
    public static void main(String[] args)
    {

        // Number of vertices
        int N = 7;

        // Number of edges
        int M = 10;

        // Edge to be checked
        int U_V[] = { 3, 6 };

        // Creating GfG object
        GfG obj = new GfG(8);

        // Initializing graph
        helperInitialize(8);

        // Creating edges
        Edge e0 = new Edge(1, 2, 5);
        Edge e1 = new Edge(1, 4, 3);
        Edge e2 = new Edge(1, 5, 12);
        Edge e3 = new Edge(1, 6, 5);
        Edge e4 = new Edge(4, 5, 1);
        Edge e5 = new Edge(5, 6, 2);
        Edge e6 = new Edge(5, 3, 1);
        Edge e7 = new Edge(3, 6, 16);
        Edge e8 = new Edge(4, 7, 1);
        Edge e9 = new Edge(2, 4, 1);

        // Adding edges to the graph
        graph[1].add(e0);
        graph[1].add(e1);
        graph[1].add(e2);
        graph[1].add(e3);
        graph[4].add(e4);
        graph[5].add(e5);
        graph[5].add(e6);
        graph[3].add(e7);
        graph[4].add(e8);
        graph[2].add(e9);

        // DFS traversal from
        // vertex U
        dfs(U_V[0], 16);

        // If there is alternate
        // path then print YES,
        // else NO
        if (visited[U_V[1]]) {
            System.out.print("No");
        }
        else {
            System.out.print("Yes");
        }
    }
}
```

## 蟒蛇 3

```
# Python3 program for above approach

class Edge:
        # Edge constructor to
        # initialize edge (u, v) with
        # weight w
    def __init__(self, u, v, w):
        self.u = u
        self.v = v
        self.w = w

# Depth First Search to traverse
# all vertices with weight less
# than weight of the dfs root
def dfs(S, W):
    global visited,graph

    # Marking the vertex visited
    visited[S] = True

    # Traversing adjacent vertex
    for uv in graph[S]:
        ver = uv.v
        w = uv.w

        if (not visited[ver] and w < W):
            dfs(ver, W)

# Driver code
if __name__ == '__main__':

    # Number of vertices
    N = 7

    # Number of edges
    M = 10

    # Edge to be checked
    U_V = [3, 6]

    # Creating GfG object
    visited, graph = [False for i in range(8)], [[] for i in range(8)]

    # Creating edges
    e0 = Edge(1, 2, 5)
    e1 = Edge(1, 4, 3)
    e2 = Edge(1, 5, 12)
    e3 = Edge(1, 6, 5)
    e4 = Edge(4, 5, 1)
    e5 = Edge(5, 6, 2)
    e6 = Edge(5, 3, 1)
    e7 = Edge(3, 6, 16)
    e8 = Edge(4, 7, 1)
    e9 = Edge(2, 4, 1)

    # Adding edges to the graph
    graph[1].append(e0)
    graph[1].append(e1)
    graph[1].append(e2)
    graph[1].append(e3)
    graph[4].append(e4)
    graph[5].append(e5)
    graph[5].append(e6)
    graph[3].append(e7)
    graph[4].append(e8)
    graph[2].append(e9)

    # DFS traversal from
    # vertex U
    dfs(U_V[0], 16)

    # If there is alternate
    # path then prYES,
    # else NO
    if (visited[U_V[1]]):
        print("NO")
    else :
        print("YES")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

// GfG class
class GfG
{

    // Array to mark already
    // visited vertices
    static private bool []visited;

    // Adjacency list representation
    // of the graph
    static private List<Edge> []graph;

    // GfG class constructor
    public GfG(int size)
    {
        visited = new bool[size];
        graph = new List<Edge>[size];
    }

    // Edge class
    class Edge
    {
        public int u;
        public int v;
        public int w;

        // Edge constructor to
        // initialize edge (u, v) with
        // weight w
        public Edge(int u, int v, int w)
        {
            this.u = u;
            this.v = v;
            this.w = w;
        }
    }

    // Helper method to
    // initialize graph
    static private void helperInitialize(int size)
    {
        for (int i = 0; i < size; i++)
        {
            graph[i] = new List<Edge>();
        }
    }

    // Depth First Search to traverse
    // all vertices with weight less
    // than weight of the dfs root
    static private void dfs(int S, int W)
    {

        // Marking the vertex visited
        visited[S] = true;

        // Traversing adjacent vertex
        foreach (Edge uv in graph[S])
        {
            int ver = uv.v;
            int w = uv.w;
            if (!visited[ver] && w < W)
                dfs(ver, W);
        }
    }

    // Driver function
    public static void Main(String[] args)
    {

        // Edge to be checked
        int []U_V = { 3, 6 };

        // Creating GfG object
        GfG obj = new GfG(8);

        // Initializing graph
        helperInitialize(8);

        // Creating edges
        Edge e0 = new Edge(1, 2, 5);
        Edge e1 = new Edge(1, 4, 3);
        Edge e2 = new Edge(1, 5, 12);
        Edge e3 = new Edge(1, 6, 5);
        Edge e4 = new Edge(4, 5, 1);
        Edge e5 = new Edge(5, 6, 2);
        Edge e6 = new Edge(5, 3, 1);
        Edge e7 = new Edge(3, 6, 16);
        Edge e8 = new Edge(4, 7, 1);
        Edge e9 = new Edge(2, 4, 1);

        // Adding edges to the graph
        graph[1].Add(e0);
        graph[1].Add(e1);
        graph[1].Add(e2);
        graph[1].Add(e3);
        graph[4].Add(e4);
        graph[5].Add(e5);
        graph[5].Add(e6);
        graph[3].Add(e7);
        graph[4].Add(e8);
        graph[2].Add(e9);

        // DFS traversal from
        // vertex U
        dfs(U_V[0], 16);

        // If there is alternate
        // path then print YES,
        // else NO
        if (visited[U_V[1]])
        {
            Console.Write("No");
        }
        else
        {
            Console.Write("Yes");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Array to mark already
    // visited vertices
let visited = new Array(100);

// Adjacency list representation
    // of the graph
let graph=new Array(100);

 // Edge class
class Edge
{
    constructor(u,v,w)
    {
        this.u = u;
            this.v = v;
            this.w = w;
    }
}

// Helper method to
    // initialize graph
function  helperInitialize(size)
{
    for (let i = 0; i < size; i++) {
            graph[i] = [];
        }
}

// Depth First Search to traverse
    // all vertices with weight less
    // than weight of the dfs root
function dfs(S,W)
{
    // Marking the vertex visited
        visited[S] = true;

        // Traversing adjacent vertex
        for (let uv=0;uv<graph[S].length;uv++) {
            let ver = graph[S][uv].v;
            let w = graph[S][uv].w;
            if (!visited[ver] && w < W)
                dfs(ver, W);
        }
}

// Driver function
// Number of vertices
        let N = 7;

        // Number of edges
        let M = 10;

        // Edge to be checked
        let U_V = [ 3, 6 ];

        // Initializing graph
        helperInitialize(8);

        // Creating edges
        let e0 = new Edge(1, 2, 5);
        let e1 = new Edge(1, 4, 3);
        let e2 = new Edge(1, 5, 12);
        let e3 = new Edge(1, 6, 5);
        let e4 = new Edge(4, 5, 1);
        let e5 = new Edge(5, 6, 2);
        let e6 = new Edge(5, 3, 1);
        let e7 = new Edge(3, 6, 16);
        let e8 = new Edge(4, 7, 1);
        let e9 = new Edge(2, 4, 1);

        // Adding edges to the graph
        graph[1].push(e0);
        graph[1].push(e1);
        graph[1].push(e2);
        graph[1].push(e3);
        graph[4].push(e4);
        graph[5].push(e5);
        graph[5].push(e6);
        graph[3].push(e7);
        graph[4].push(e8);
        graph[2].push(e9);

        // DFS traversal from
        // vertex U
        dfs(U_V[0], 16);

        // If there is alternate
        // path then print YES,
        // else NO
        if (visited[U_V[1]]) {
            document.write("No");
        }
        else {
            document.write("Yes");
        }

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N + M)，其中 N =顶点数& M =边数。