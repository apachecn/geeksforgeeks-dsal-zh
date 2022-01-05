# 检查路径是否存在于存在 K 个顶点的树中，或者最多在距离 D 处

> 原文:[https://www . geeksforgeeks . org/check-a-path-exists-in-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-](https://www.geeksforgeeks.org/check-if-a-path-exists-in-a-tree-with-k-vertices-present-or-are-at-most-at-a-distance-d/)

给定一棵树，其 **N** 个顶点编号为**【0，N–1】**、 **K** 个顶点，距离为 **D** ，任务是找出是否存在从根到某个顶点的路径，使得每个 **K** 个顶点都属于该路径，或者最多与该路径有一段距离 **D** 。

**示例:**

```
Input: 
             0
           /   \
         /       \
       1           2
     /   \        /  \
   /       \     /     \
  3         4   5        8
               /  \        
              /     \
             6       7
                    /
                   /
                  9
K = {6, 7, 8, 5}, D = 1
Output: YES
Explanation: 
The path *( 0 - 2 - 5 - 7 )*
satisfies the condition. Vertices *5* 
and *7* are a part of the path. 
Vertex *6* is the child of vertex 
*5* and *8* is the child of *2*. 

Input:
             0
           /   \
         /       \
       1           2
     /   \        /  \
   /       \     /     \
  3         4   5        8
   \           /  \        
    \         /     \
     10      6       7
                    /
                   /
                  9
K = {10, 9, 8, 5}, D = 2
Output: NO
Explanation: 
No such path exists that satisfies the condition.
```

**进场:**

*   对于每个顶点，存储它们各自的父顶点和深度。
*   从给定的 **K** 顶点中选择最深的顶点
*   继续用其父级 **D** 替换除根和最深顶点之外的 **K** 顶点
*   如果当前的一组 **K** 顶点可以形成一条*连续路径*，那么答案是**是**还是**否**否则。

下面的代码是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Class to represent the Tree
class Tree {

    int T;

    // Stores the timing of traversals
    vector<int> parent;

    // Stores the parent of each vertex
    vector<int> depth;

    // Stores the depth of each vertex
    vector<int> tin;

    // Stores the time to reach
    // every vertex
    vector<int> tout;

    // Stores the time of leaving
    // every vertex after DFS calls
    // from its children
    vector<vector<int> > edges;

    // Store the edges

public:
    // Constructor
    Tree(int n)
    {
        T = 0;
        parent = depth = vector<int>(n);
        tin = tout = vector<int>(n);
        edges = vector<vector<int> >(n);
    }

    // Adding edges
    void addEdge(int u, int v)
    {
        edges[u].push_back(v);
        edges[v].push_back(u);
    }

    void dfs(int v, int p = -1, int d = 0)
    {
        // Store the time to reach vertex v
        tin[v] = T++;

        // Store the parent of vertex v
        parent[v] = p;

        // Store the depth of vertex v
        depth[v] = d;

        // Run DFS for all its children of v
        for (auto i : edges[v]) {
            if (i == p)
                continue;

            dfs(i, v, d + 1);
        }

        // Store the leaving time
        // of vertex v
        tout[v] = T++;
    }

    // Checks and returns whether vertex
    // v is parent of vertex u or not
    bool checkTiming(int v, int u)
    {
        if (tin[v] <= tin[u]
            && tout[u] <= tout[v])
            return true;

        return false;
    }

    // Checks and returns if the path exists
    void pathExistence(vector<int> k, int d)
    {
        int deepest_vertex = k[0];

        // Find the deepest vertex among the
        // given K vertices
        for (int i = 0; i < k.size(); i++) {
            if (depth[k[i]] > depth[deepest_vertex])
                deepest_vertex = k[i];
        }

        // Replace each of the K vertices
        // except for the root and the
        // deepest vertex
        for (int i = 0; i < k.size(); i++) {
            if (k[i] == deepest_vertex)
                continue;

            int count = d;

            while (count > 0) {

                // Stop when root
                // has been reached
                if (parent[k[i]] == -1)
                    break;

                k[i] = parent[k[i]];
                count--;
            }
        }

        bool ans = true;

        // Check if each of the K-1 vertices
        // are a parent of the deepest vertex
        for (auto i : k)
            ans &= checkTiming(i, deepest_vertex);

        if (ans)
            cout << "Yes" << endl;
        else
            cout << "No" << endl;
    }
};

// Driver Code
int main()
{
    Tree t(11);

    t.addEdge(0, 1);
    t.addEdge(0, 2);
    t.addEdge(1, 3);
    t.addEdge(1, 4);
    t.addEdge(2, 5);
    t.addEdge(2, 8);
    t.addEdge(5, 6);
    t.addEdge(4, 10);
    t.addEdge(3, 7);
    t.addEdge(3, 9);

    t.dfs(0);

    vector<int> k = { 2, 6, 8, 5 };

    int d = 2;

    t.pathExistence(k, d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
import java.lang.*;

class GFG{

static int T;

// Stores the timing of traversals
static int[] parent;

// Stores the parent of each vertex
static int[] depth;

// Stores the depth of each vertex
static int[] tin;

// Stores the time to reach
// every vertex
static int[] tout;

// Stores the time of leaving
// every vertex after DFS calls
// from its children
static ArrayList<ArrayList<Integer>> edges;

// Adding edges
static void addEdge(int u, int v)
{
    edges.get(u).add(v);
    edges.get(v).add(u);
}

static void dfs(int v, int p, int d)
{

    // Store the time to reach vertex v
    tin[v] = T++;

    // Store the parent of vertex v
    parent[v] = p;

    // Store the depth of vertex v
    depth[v] = d;

    // Run DFS for all its children of v
    for(Integer i : edges.get(v))
    {
        if (i == p)
            continue;

        dfs(i, v, d + 1);
    }

    // Store the leaving time
    // of vertex v
    tout[v] = T++;
}

// Checks and returns whether vertex
// v is parent of vertex u or not
static boolean checkTiming(int v, int u)
{
    if (tin[v] <= tin[u] &&
       tout[u] <= tout[v])
        return true;

    return false;
}

// Checks and returns if the path exists
static void pathExistence(int[] k, int d)
{
    int deepest_vertex = k[0];

    // Find the deepest vertex among the
    // given K vertices
    for(int i = 0; i < k.length; i++)
    {
        if (depth[k[i]] > depth[deepest_vertex])
            deepest_vertex = k[i];
    }

    // Replace each of the K vertices
    // except for the root and the
    // deepest vertex
    for(int i = 0; i < k.length; i++)
    {
        if (k[i] == deepest_vertex)
            continue;

        int count = d;

        while (count > 0)
        {

            // Stop when root
            // has been reached
            if (parent[k[i]] == -1)
                break;

            k[i] = parent[k[i]];
            count--;
        }
    }

    boolean ans = true;

    // Check if each of the K-1 vertices
    // are a parent of the deepest vertex
    for(int i : k)
        ans &= checkTiming(i, deepest_vertex);

    if (ans)
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver code
public static void main(String[] args)
{
    int n = 11;
    T = 0;

    parent = new int[n];
    depth = new int[n];
    tin = new int[n];
    tout = new int[n];
    edges = new ArrayList<>();

    for(int i = 0; i < n; i++)
        edges.add(new ArrayList<>());

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(1, 4);
    addEdge(2, 5);
    addEdge(2, 8);
    addEdge(5, 6);
    addEdge(4, 10);
    addEdge(3, 7);
    addEdge(3, 9);

    dfs(0, -1, 0);

    int[] k = { 2, 6, 8, 5 };

    int d = 2;

    pathExistence(k, d);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation of above approach

T = 0
n = 11

# Stores the timing of traversals
parent = n * [0]

# Stores the parent of each vertex
depth = n * [0]

# Stores the depth of each vertex
tin = n * [0]

# Stores the time to reach every vertex
tout = n * [0]

# Stores the time of leaving
# every vertex after DFS calls
# from its children
edges = []
for i in range(n):
    edges.append([])

# Adding edges
def addEdge(u, v):

    edges[u].append(v)
    edges[v].append(u)

def dfs(v, p, d):
    global T 
    # Store the time to reach vertex v
    T += 1
    tin[v] = T

    # Store the parent of vertex v
    parent[v] = p

    # Store the depth of vertex v
    depth[v] = d

    # Run DFS for all its children of v
    for i in edges[v]:

        if (i == p):
            continue

        dfs(i, v, d + 1)

    # Store the leaving time
    # of vertex v
    T += 1
    tout[v] = T

# Checks and returns whether vertex
# v is parent of vertex u or not
def checkTiming(v, u):

    if (tin[v] <= tin[u] and tout[u] <= tout[v]):
        return True

    return False

# Checks and returns if the path exists
def pathExistence(k, d):

    deepest_vertex = k[0]

    # Find the deepest vertex among the
    # given K vertices
    for i in range(len(k)):

        if (depth[k[i]] > depth[deepest_vertex]):
            deepest_vertex = k[i]

    # Replace each of the K vertices
    # except for the root and the
    # deepest vertex
    for i in range(len(k)):

        if (k[i] == deepest_vertex):
            continue

        count = d

        while (count > 0):

            # Stop when root
            # has been reached
            if (parent[k[i]] == -1):
                break

            k[i] = parent[k[i]]
            count-=1

    ans = True

    # Check if each of the K-1 vertices
    # are a parent of the deepest vertex
    for i in k:
        ans &= checkTiming(i, deepest_vertex)

    if ans:
        print("Yes")
    else:
        print("No")

addEdge(0, 1)
addEdge(0, 2)
addEdge(1, 3)
addEdge(1, 4)
addEdge(2, 5)
addEdge(2, 8)
addEdge(5, 6)
addEdge(4, 10)
addEdge(3, 7)
addEdge(3, 9)

dfs(0, -1, 0)

k = [ 2, 6, 8, 5 ]
d = 2

pathExistence(k, d)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;
class GFG {

    static int T;

    // Stores the timing of traversals
    static int[] parent;

    // Stores the parent of each vertex
    static int[] depth;

    // Stores the depth of each vertex
    static int[] tin;

    // Stores the time to reach
    // every vertex
    static int[] tout;

    // Stores the time of leaving
    // every vertex after DFS calls
    // from its children
    static List<List<int>> edges;

    // Adding edges
    static void addEdge(int u, int v)
    {
        edges[u].Add(v);
        edges[v].Add(u);
    }

    static void dfs(int v, int p, int d)
    {

        // Store the time to reach vertex v
        tin[v] = T++;

        // Store the parent of vertex v
        parent[v] = p;

        // Store the depth of vertex v
        depth[v] = d;

        // Run DFS for all its children of v
        foreach(int i in edges[v])
        {
            if (i == p)
                continue;

            dfs(i, v, d + 1);
        }

        // Store the leaving time
        // of vertex v
        tout[v] = T++;
    }

    // Checks and returns whether vertex
    // v is parent of vertex u or not
    static bool checkTiming(int v, int u)
    {
        if (tin[v] <= tin[u] && tout[u] <= tout[v])
            return true;

        return false;
    }

    // Checks and returns if the path exists
    static void pathExistence(int[] k, int d)
    {
        int deepest_vertex = k[0];

        // Find the deepest vertex among the
        // given K vertices
        for(int i = 0; i < k.Length; i++)
        {
            if (depth[k[i]] > depth[deepest_vertex])
                deepest_vertex = k[i];
        }

        // Replace each of the K vertices
        // except for the root and the
        // deepest vertex
        for(int i = 0; i < k.Length; i++)
        {
            if (k[i] == deepest_vertex)
                continue;

            int count = d;

            while (count > 0)
            {

                // Stop when root
                // has been reached
                if (parent[k[i]] == -1)
                    break;

                k[i] = parent[k[i]];
                count--;
            }
        }

        bool ans = true;

        // Check if each of the K-1 vertices
        // are a parent of the deepest vertex
        foreach(int i in k)
            ans &= checkTiming(i, deepest_vertex);

        if (ans)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }

  static void Main() {
    int n = 11;
    T = 0;

    parent = new int[n];
    depth = new int[n];
    tin = new int[n];
    tout = new int[n];
    edges = new List<List<int>>();

    for(int i = 0; i < n; i++)
        edges.Add(new List<int>());

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(1, 4);
    addEdge(2, 5);
    addEdge(2, 8);
    addEdge(5, 6);
    addEdge(4, 10);
    addEdge(3, 7);
    addEdge(3, 9);

    dfs(0, -1, 0);

    int[] k = { 2, 6, 8, 5 };

    int d = 2;

    pathExistence(k, d);
  }
}

// This code is contributed by decode2207.
```

## java 描述语言

```
<script>

// Javascript implementation of above approach
let T;

// Stores the timing of traversals
let parent;

// Stores the parent of each vertex
let depth;

// Stores the depth of each vertex
let tin;

// Stores the time to reach
// every vertex
let tout;

// Stores the time of leaving
// every vertex after DFS calls
// from its children
let edges;

// Adding edges
function addEdge(u, v)
{
    edges[u].push(v);
    edges[v].push(u);
}

function dfs(v, p, d)
{

    // Store the time to reach vertex v
    tin[v] = T++;

    // Store the parent of vertex v
    parent[v] = p;

    // Store the depth of vertex v
    depth[v] = d;

    // Run DFS for all its children of v
    for(let i = 0; i < edges[v].length; i++)
    {
        if (edges[v][i] == p)
            continue;

        dfs(edges[v][i], v, d + 1);
    }

    // Store the leaving time
    // of vertex v
    tout[v] = T++;
}

// Checks and returns whether vertex
// v is parent of vertex u or not
function checkTiming(v, u)
{
    if (tin[v] <= tin[u] &&
       tout[u] <= tout[v])
        return true;

    return false;
}

// Checks and returns if the path exists
function pathExistence(k, d)
{
    let deepest_vertex = k[0];

    // Find the deepest vertex among the
    // given K vertices
    for(let i = 0; i < k.length; i++)
    {
        if (depth[k[i]] > depth[deepest_vertex])
            deepest_vertex = k[i];
    }

    // Replace each of the K vertices
    // except for the root and the
    // deepest vertex
    for(let i = 0; i < k.length; i++)
    {
        if (k[i] == deepest_vertex)
            continue;

        let count = d;

        while (count > 0)
        {

            // Stop when root
            // has been reached
            if (parent[k[i]] == -1)
                break;

            k[i] = parent[k[i]];
            count--;
        }
    }

    let ans = true;

    // Check if each of the K-1 vertices
    // are a parent of the deepest vertex
    for(let i = 0; i < k.length; i++)
        ans &= checkTiming(k[i], deepest_vertex);

    if (ans)
        document.write("Yes");
    else
        document.write("No");
}

// Driver code
let n = 11;
T = 0;

parent = new Array(n);
depth = new Array(n);
tin = new Array(n);
tout = new Array(n);
edges = [];

for(let i = 0; i < n; i++)
    edges.push([]);

addEdge(0, 1);
addEdge(0, 2);
addEdge(1, 3);
addEdge(1, 4);
addEdge(2, 5);
addEdge(2, 8);
addEdge(5, 6);
addEdge(4, 10);
addEdge(3, 7);
addEdge(3, 9);

dfs(0, -1, 0);

let k = [ 2, 6, 8, 5 ];
let d = 2;

pathExistence(k, d);

// This code is contributed by mukesh07

</script>
```

**Output:** 

```
Yes
```