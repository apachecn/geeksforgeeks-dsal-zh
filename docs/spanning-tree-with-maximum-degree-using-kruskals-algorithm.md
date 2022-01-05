# 最大度生成树(使用克鲁斯卡尔算法)

> 原文:[https://www . geeksforgeeks . org/使用 kruskals 算法的最大度生成树/](https://www.geeksforgeeks.org/spanning-tree-with-maximum-degree-using-kruskals-algorithm/)

给定一个由 **n 个**顶点和 **m 个**边组成的无向未加权连通图。任务是找到这个图的任何生成树，使得所有顶点上的最大度是最大可能的。打印输出边的顺序并不重要，边也可以反向打印，即(u，v)也可以打印为(v，u)。

**示例:**

```
Input:
        1
       / \
      2   5
       \ /
        3
        |
        4
Output:
3 2
3 5
3 4
1 2
The maximum degree over all vertices 
is of vertex 3 which is 3 and is 
maximum possible.

Input:
        1
       /
      2 
     / \ 
    5   3
        |
        4
Output:
2 1
2 5
2 3
3 4
```

**前提:** [Kruskal 算法求最小生成树](https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/)

**方法:**利用 Kruskal 算法寻找最小生成树，可以解决给定的问题。
我们找到图中度数最大的顶点。首先，我们将执行入射到该顶点的所有边的并集，然后执行正常的克鲁斯卡尔算法。这给了我们最优生成树。

## C++

```
#include<bits/stdc++.h>
using namespace std;

// par and sz will store the parent
// and rank of particular node
// in the Union Find Algorithm
vector<int> par,sz;

// Find function of Union Find Algorithm
int find(int x)
{
    if(par[x]!=x)
        par[x]=find(par[x]);
    return par[x];
}

// Union function of Union Find Algorithm
void Union(int u, int v)
{
    int x = find(u);
    int y = find(v);
    if (x == y)
        return;
    if (sz[x] > sz[y])
        par[y] = x;
    else if (sz[x] < sz[y])
        par[x] = y;
    else {
        par[x] = y;
        sz[y]++;
    }
}

// Function to find the required spanning tree
void findSpanningTree(vector<int> deg,int n,int m,vector<vector<int>> g)
{
    par.resize(n+1);
    sz.resize(n+1);
    // Initialising parent of a node
    // by itself
    for (int i = 1; i <= n; i++)
        par[i] = i;

    // Variable to store the node
    // with maximum degree
    int max = 1;

    // Finding the node with maximum degree
    for (int i = 2; i <= n; i++)
        if (deg[i] > deg[max])
            max = i;

    // Union of all edges incident
    // on vertex with maximum degree
    for (int v : g[max]) {
        cout << max << " " << v << '\n';
        Union(max, v);
    }

    // Carrying out normal Kruskal Algorithm
    for (int u = 1; u <= n; u++) {
        for (int v : g[u]) {
            int x = find(u);
            int y = find(v);
            if (x == y)
                continue;
            Union(x, y);
            cout << u << " " << v << '\n';
        }
    }   
}

int main()
{
    // Number of nodes
    int n = 5;

    // Number of edges
    int m = 5;

    // store the graph
    vector<vector<int>> g(n+1);

    // store the degree
    // of each node in the graph
    vector<int> deg(n+1);

    // add edges and update degrees
    g[1].push_back(2);
    g[2].push_back(1);
    deg[1]++;
    deg[2]++;
    g[1].push_back(5);
    g[5].push_back(1);
    deg[1]++;
    deg[5]++;
    g[2].push_back(3);
    g[3].push_back(2);
    deg[2]++;
    deg[3]++;
    g[5].push_back(3);
    g[3].push_back(5);
    deg[3]++;
    deg[5]++;
    g[3].push_back(4);
    g[4].push_back(3);
    deg[3]++;
    deg[4]++;

    findSpanningTree(deg, n, m, g);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
public class GFG {

    // par and rank will store the parent
    // and rank of particular node
    // in the Union Find Algorithm
    static int par[], rank[];

    // Find function of Union Find Algorithm
    static int find(int x)
    {
        if (par[x] != x)
            par[x] = find(par[x]);
        return par[x];
    }

    // Union function of Union Find Algorithm
    static void union(int u, int v)
    {
        int x = find(u);
        int y = find(v);
        if (x == y)
            return;
        if (rank[x] > rank[y])
            par[y] = x;
        else if (rank[x] < rank[y])
            par[x] = y;
        else {
            par[x] = y;
            rank[y]++;
        }
    }

    // Function to find the required spanning tree
    static void findSpanningTree(int deg[], int n,
                                 int m, ArrayList<Integer> g[])
    {
        par = new int[n + 1];
        rank = new int[n + 1];

        // Initialising parent of a node
        // by itself
        for (int i = 1; i <= n; i++)
            par[i] = i;

        // Variable to store the node
        // with maximum degree
        int max = 1;

        // Finding the node with maximum degree
        for (int i = 2; i <= n; i++)
            if (deg[i] > deg[max])
                max = i;

        // Union of all edges incident
        // on vertex with maximum degree
        for (int v : g[max]) {
            System.out.println(max + " " + v);
            union(max, v);
        }

        // Carrying out normal Kruskal Algorithm
        for (int u = 1; u <= n; u++) {
            for (int v : g[u]) {
                int x = find(u);
                int y = find(v);
                if (x == y)
                    continue;
                union(x, y);
                System.out.println(u + " " + v);
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        // Number of nodes
        int n = 5;

        // Number of edges
        int m = 5;

        // ArrayList to store the graph
        ArrayList<Integer> g[] = new ArrayList[n + 1];
        for (int i = 1; i <= n; i++)
            g[i] = new ArrayList<>();

        // Array to store the degree
        // of each node in the graph
        int deg[] = new int[n + 1];

        // Add edges and update degrees
        g[1].add(2);
        g[2].add(1);
        deg[1]++;
        deg[2]++;
        g[1].add(5);
        g[5].add(1);
        deg[1]++;
        deg[5]++;
        g[2].add(3);
        g[3].add(2);
        deg[2]++;
        deg[3]++;
        g[5].add(3);
        g[3].add(5);
        deg[3]++;
        deg[5]++;
        g[3].add(4);
        g[4].add(3);
        deg[3]++;
        deg[4]++;

        findSpanningTree(deg, n, m, g);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from typing import List

# par and rank will store the parent
# and rank of particular node
# in the Union Find Algorithm
par = []
rnk = []

# Find function of Union Find Algorithm
def find(x: int) -> int:

    global par

    if (par[x] != x):
        par[x] = find(par[x])

    return par[x]

# Union function of Union Find Algorithm
def Union(u: int, v: int) -> None:

    global par, rnk

    x = find(u)
    y = find(v)

    if (x == y):
        return
    if (rnk[x] > rnk[y]):
        par[y] = x
    elif (rnk[x] < rnk[y]):
        par[x] = y
    else:
        par[x] = y
        rnk[y] += 1

# Function to find the required spanning tree
def findSpanningTree(deg: List[int], n: int, m: int,
                     g: List[List[int]]) -> None:

    global rnk, par

    # Initialising parent of a node
    # by itself
    par = [i for i in range(n + 1)]
    rnk = [0] * (n + 1)

    # Variable to store the node
    # with maximum degree
    max = 1

    # Finding the node with maximum degree
    for i in range(2, n + 1):
        if (deg[i] > deg[max]):
            max = i

    # Union of all edges incident
    # on vertex with maximum degree
    for v in g[max]:
        print("{} {}".format(max, v))
        Union(max, v)

    # Carrying out normal Kruskal Algorithm
    for u in range(1, n + 1):
        for v in g[u]:
            x = find(u)
            y = find(v)

            if (x == y):
                continue

            Union(x, y)
            print("{} {}".format(u, v))

# Driver code
if __name__ == "__main__":

    # Number of nodes
    n = 5

    # Number of edges
    m = 5

    # ArrayList to store the graph
    g = [[] for _ in range(n + 1)]

    # Array to store the degree
    # of each node in the graph
    deg = [0] * (n + 1)

    # Add edges and update degrees
    g[1].append(2)
    g[2].append(1)
    deg[1] += 1
    deg[2] += 1
    g[1].append(5)
    g[5].append(1)
    deg[1] += 1
    deg[5] += 1
    g[2].append(3)
    g[3].append(2)
    deg[2] += 1
    deg[3] += 1
    g[5].append(3)
    g[3].append(5)
    deg[3] += 1
    deg[5] += 1
    g[3].append(4)
    g[4].append(3)
    deg[3] += 1
    deg[4] += 1

    findSpanningTree(deg, n, m, g)

# This code is contributed by sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // par and rank will store the parent
    // and rank of particular node
    // in the Union Find Algorithm
    static int []par;
    static int []rank;

    // Find function of Union Find Algorithm
    static int find(int x)
    {
        if (par[x] != x)
            par[x] = find(par[x]);
        return par[x];
    }

    // Union function of Union Find Algorithm
    static void union(int u, int v)
    {
        int x = find(u);
        int y = find(v);
        if (x == y)
            return;
        if (rank[x] > rank[y])
            par[y] = x;
        else if (rank[x] < rank[y])
            par[x] = y;
        else {
            par[x] = y;
            rank[y]++;
        }
    }

    // Function to find the required spanning tree
    static void findSpanningTree(int []deg, int n,
                                int m, List<int> []g)
    {
        par = new int[n + 1];
        rank = new int[n + 1];

        // Initialising parent of a node
        // by itself
        for (int i = 1; i <= n; i++)
            par[i] = i;

        // Variable to store the node
        // with maximum degree
        int max = 1;

        // Finding the node with maximum degree
        for (int i = 2; i <= n; i++)
            if (deg[i] > deg[max])
                max = i;

        // Union of all edges incident
        // on vertex with maximum degree
        foreach (int v in g[max])
        {
            Console.WriteLine(max + " " + v);
            union(max, v);
        }

        // Carrying out normal Kruskal Algorithm
        for (int u = 1; u <= n; u++)
        {
            foreach (int v in g[u])
            {
                int x = find(u);
                int y = find(v);
                if (x == y)
                    continue;
                union(x, y);
                Console.WriteLine(u + " " + v);
            }
        }
    }

    // Driver code
    public static void Main(String []args)
    {

        // Number of nodes
        int n = 5;

        // Number of edges
        int m = 5;

        // ArrayList to store the graph
        List<int> []g = new List<int>[n + 1];
        for (int i = 1; i <= n; i++)
            g[i] = new List<int>();

        // Array to store the degree
        // of each node in the graph
        int []deg = new int[n + 1];

        // Add edges and update degrees
        g[1].Add(2);
        g[2].Add(1);
        deg[1]++;
        deg[2]++;
        g[1].Add(5);
        g[5].Add(1);
        deg[1]++;
        deg[5]++;
        g[2].Add(3);
        g[3].Add(2);
        deg[2]++;
        deg[3]++;
        g[5].Add(3);
        g[3].Add(5);
        deg[3]++;
        deg[5]++;
        g[3].Add(4);
        g[4].Add(3);
        deg[3]++;
        deg[4]++;

        findSpanningTree(deg, n, m, g);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // par and rank will store the parent
    // and rank of particular node
    // in the Union Find Algorithm
    let par, rank;

    // Find function of Union Find Algorithm
    function find(x)
    {
        if (par[x] != x)
            par[x] = find(par[x]);
        return par[x];
    }

    // Union function of Union Find Algorithm
    function union(u, v)
    {
        let x = find(u);
        let y = find(v);
        if (x == y)
            return;
        if (rank[x] > rank[y])
            par[y] = x;
        else if (rank[x] < rank[y])
            par[x] = y;
        else {
            par[x] = y;
            rank[y]++;
        }
    }

    // Function to find the required spanning tree
    function findSpanningTree(deg, n, m, g)
    {
        par = new Array(n + 1);
        rank = new Array(n + 1);

        // Initialising parent of a node
        // by itself
        for (let i = 1; i <= n; i++)
            par[i] = i;

        // Variable to store the node
        // with maximum degree
        let max = 1;

        // Finding the node with maximum degree
        for (let i = 2; i <= n; i++)
            if (deg[i] > deg[max])
                max = i;

        // Union of all edges incident
        // on vertex with maximum degree
        for (let v = 0; v < g[max].length; v++) {
            document.write(max + " " + g[max][v] + "</br>");
            union(max, g[max][v]);
        }

        // Carrying out normal Kruskal Algorithm
        for (let u = 1; u <= n; u++) {
            for (let v = 0; v < g[u].length; v++) {
                let x = find(u);
                let y = find(g[u][v]);
                if (x == y)
                    continue;
                union(x, y);
                document.write(u + " " + g[u][v] + "</br>");
            }
        }
    }

    // Number of nodes
    let n = 5;

    // Number of edges
    let m = 5;

    // ArrayList to store the graph
    let g = new Array(n + 1);
    for (let i = 1; i <= n; i++)
      g[i] = [];

    // Array to store the degree
    // of each node in the graph
    let deg = new Array(n + 1);
    deg.fill(0);

    // Add edges and update degrees
    g[1].push(2);
    g[2].push(1);
    deg[1]++;
    deg[2]++;
    g[1].push(5);
    g[5].push(1);
    deg[1]++;
    deg[5]++;
    g[2].push(3);
    g[3].push(2);
    deg[2]++;
    deg[3]++;
    g[5].push(3);
    g[3].push(5);
    deg[3]++;
    deg[5]++;
    g[3].push(4);
    g[4].push(3);
    deg[3]++;
    deg[4]++;

    findSpanningTree(deg, n, m, g);

</script>
```

**Output:** 

```
3 2
3 5
3 4
1 2
```

**时间复杂度:** O(N * logN)，其中 N 为图中节点总数。
**辅助空间:** O(N)