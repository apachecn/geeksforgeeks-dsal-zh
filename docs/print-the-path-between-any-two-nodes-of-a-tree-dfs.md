# 打印树的任意两个节点之间的路径| DFS

> 原文:[https://www . geesforgeks . org/print-任意两个树节点之间的路径-dfs/](https://www.geeksforgeeks.org/print-the-path-between-any-two-nodes-of-a-tree-dfs/)

给定一个具有 **N-1** 边的不同节点 **N** 的树和一对节点 **P** 。任务是使用 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 找到并打印树的两个给定节点之间的路径。

```
Input: N = 10
          1
       /    \
      2      3
    / | \  / | \
   4  5 6  7 8  9
Pair = {4, 8}
Output: 4 -> 2 -> 1 -> 3 -> 8

Input: N = 3
      1
     /  \
    2    3
Pair = {2, 3}
Output:  2 -> 1 -> 3
```

![](img/048973da0da003a46af40352b564a17a.png)

**例如，上图中**节点 **5** 和 **3** 之间的路径为 **5 - > 2 - > 1 - > 3** 。
节点 **4** 和 **8** 之间的路径为**4->2->1->3->8**。

**进场:**

*   其思想是从源节点运行 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) ，并将遍历的节点推入[栈](https://www.geeksforgeeks.org/stack-data-structure/)，直到遍历完目的节点。
*   每当[回溯](http://wstackww.geeksforgeeks.org/backtracking-algorithms/)发生时，从堆栈中弹出该节点。

**注意:**给定的一对节点之间应该有一条路径。

下面是上述方法的实现:

## C++

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

// An utility function to add an edge in an
// undirected graph.
void addEdge(vector<int> v[],
             int x,
             int y)
{
    v[x].push_back(y);
    v[y].push_back(x);
}

// A function to print the path between
// the given pair of nodes.
void printPath(vector<int> stack)
{
    int i;
    for (i = 0; i < (int)stack.size() - 1;
         i++) {
        cout << stack[i] << " -> ";
    }
    cout << stack[i];
}

// An utility function to do
// DFS of graph recursively
// from a given vertex x.
void DFS(vector<int> v[],
         bool vis[],
         int x,
         int y,
         vector<int> stack)
{
    stack.push_back(x);
    if (x == y) {

        // print the path and return on
        // reaching the destination node
        printPath(stack);
        return;
    }
    vis[x] = true;

    // if backtracking is taking place
    if (!v[x].empty()) {
        for (int j = 0; j < v[x].size(); j++) {
            // if the node is not visited
            if (vis[v[x][j]] == false)
                DFS(v, vis, v[x][j], y, stack);
        }
    }

    stack.pop_back();
}

// A utility function to initialise
// visited for the node and call
// DFS function for a given vertex x.
void DFSCall(int x,
             int y,
             vector<int> v[],
             int n,
             vector<int> stack)
{
    // visited array
    bool vis[n + 1];

    memset(vis, false, sizeof(vis));

    // DFS function call
    DFS(v, vis, x, y, stack);
}

// Driver Code
int main()
{
    int n = 10;
    vector<int> v[n], stack;

    // Vertex numbers should be from 1 to 9.
    addEdge(v, 1, 2);
    addEdge(v, 1, 3);
    addEdge(v, 2, 4);
    addEdge(v, 2, 5);
    addEdge(v, 2, 6);
    addEdge(v, 3, 7);
    addEdge(v, 3, 8);
    addEdge(v, 3, 9);

    // Function Call
    DFSCall(4, 8, v, n, stack);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GFG
{
    static Vector<Vector<Integer>> v = new Vector<Vector<Integer>>();

    // An utility function to add an edge in an
    // undirected graph.
    static void addEdge(int x, int y){
        v.get(x).add(y);
        v.get(y).add(x);
    }

    // A function to print the path between
    // the given pair of nodes.
    static void printPath(Vector<Integer> stack)
    {
        for(int i = 0; i < stack.size() - 1; i++)
        {
            System.out.print(stack.get(i) + " -> ");
        }
        System.out.println(stack.get(stack.size() - 1));
    }

    // An utility function to do
    // DFS of graph recursively
    // from a given vertex x.
    static void DFS(boolean vis[], int x, int y, Vector<Integer> stack)
    {
        stack.add(x);
        if (x == y)
        {

            // print the path and return on
            // reaching the destination node
            printPath(stack);
            return;
        }
        vis[x] = true;

        // if backtracking is taking place     
        if (v.get(x).size() > 0)
        {
            for(int j = 0; j < v.get(x).size(); j++)
            {

                // if the node is not visited
                if (vis[v.get(x).get(j)] == false)
                {
                    DFS(vis, v.get(x).get(j), y, stack);
                }
            }
        }

        stack.remove(stack.size() - 1);
    }

    // A utility function to initialise
    // visited for the node and call
    // DFS function for a given vertex x.
    static void DFSCall(int x, int y, int n,
                        Vector<Integer> stack)
    {

        // visited array
        boolean vis[] = new boolean[n + 1];
        Arrays.fill(vis, false);

        // memset(vis, false, sizeof(vis))

        // DFS function call
        DFS(vis, x, y, stack);
    }

  // Driver code
    public static void main(String[] args)
    {
        for(int i = 0; i < 100; i++)
        {
            v.add(new Vector<Integer>());
        }

        int n = 10;
        Vector<Integer> stack = new Vector<Integer>();

        // Vertex numbers should be from 1 to 9.
        addEdge(1, 2);
        addEdge(1, 3);
        addEdge(2, 4);
        addEdge(2, 5);
        addEdge(2, 6);
        addEdge(3, 7);
        addEdge(3, 8);
        addEdge(3, 9);

        // Function Call
        DFSCall(4, 8, n, stack);
    }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
v = [[] for i in range(100)]

# An utility function to add an edge in an
# undirected graph.
def addEdge(x, y):
    v[x].append(y)
    v[y].append(x)

# A function to print the path between
# the given pair of nodes.
def printPath(stack):
    for i in range(len(stack) - 1):
        print(stack[i], end = " -> ")
    print(stack[-1])

# An utility function to do
# DFS of graph recursively
# from a given vertex x.
def DFS(vis, x, y, stack):
    stack.append(x)
    if (x == y):

        # print the path and return on
        # reaching the destination node
        printPath(stack)
        return
    vis[x] = True

    # if backtracking is taking place

    if (len(v[x]) > 0):
        for j in v[x]:

            # if the node is not visited
            if (vis[j] == False):
                DFS(vis, j, y, stack)

    del stack[-1]

# A utility function to initialise
# visited for the node and call
# DFS function for a given vertex x.
def DFSCall(x, y, n, stack):

    # visited array
    vis = [0 for i in range(n + 1)]

    #memset(vis, false, sizeof(vis))

    # DFS function call
    DFS(vis, x, y, stack)

# Driver Code
n = 10
stack = []

# Vertex numbers should be from 1 to 9.
addEdge(1, 2)
addEdge(1, 3)
addEdge(2, 4)
addEdge(2, 5)
addEdge(2, 6)
addEdge(3, 7)
addEdge(3, 8)
addEdge(3, 9)

# Function Call
DFSCall(4, 8, n, stack)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{
    static List<List<int>> v = new List<List<int>>();

    // An utility function to Add an edge in an
    // undirected graph.
    static void addEdge(int x, int y)
    {
        v[x].Add(y);
        v[y].Add(x);
    }

    // A function to print the path between
    // the given pair of nodes.
    static void printPath(List<int> stack)
    {
        for(int i = 0; i < stack.Count - 1; i++)
        {
            Console.Write(stack[i] + " -> ");
        }
        Console.WriteLine(stack[stack.Count - 1]);
    }

    // An utility function to do
    // DFS of graph recursively
    // from a given vertex x.
    static void DFS(bool []vis, int x, int y, List<int> stack)
    {
        stack.Add(x);
        if (x == y)
        {

            // print the path and return on
            // reaching the destination node
            printPath(stack);
            return;
        }
        vis[x] = true;

        // if backtracking is taking place     
        if (v[x].Count > 0)
        {
            for(int j = 0; j < v[x].Count; j++)
            {

                // if the node is not visited
                if (vis[v[x][j]] == false)
                {
                    DFS(vis, v[x][j], y, stack);
                }
            }
        }        
        stack.RemoveAt(stack.Count - 1);
    }

    // A utility function to initialise
    // visited for the node and call
    // DFS function for a given vertex x.
    static void DFSCall(int x, int y, int n,
                        List<int> stack)
    {

        // visited array
        bool []vis = new bool[n + 1];
        Array.Fill(vis, false);

        // memset(vis, false, sizeof(vis))

        // DFS function call
        DFS(vis, x, y, stack);
    }

  // Driver code
    public static void Main(string[] args)
    {
        for(int i = 0; i < 100; i++)
        {
            v.Add(new List<int>());
        }

        int n = 10;
        List<int> stack = new List<int>();

        // Vertex numbers should be from 1 to 9.
        addEdge(1, 2);
        addEdge(1, 3);
        addEdge(2, 4);
        addEdge(2, 5);
        addEdge(2, 6);
        addEdge(3, 7);
        addEdge(3, 8);
        addEdge(3, 9);

        // Function Call
        DFSCall(4, 8, n, stack);
    }
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach
let v = [];

// An utility function to add an edge in an
// undirected graph.
function addEdge(x, y)
{
    v[x].push(y);
    v[y].push(x);
}

// A function to print the path between
// the given pair of nodes.
function printPath(stack)
{
    for(let i = 0; i < stack.length - 1; i++)
    {
        document.write(stack[i] + " -> ");
    }
    document.write(stack[stack.length - 1] + "<br>");
}

// An utility function to do
// DFS of graph recursively
// from a given vertex x.
function DFS(vis, x, y, stack)
{
    stack.push(x);
    if (x == y)
    {

        // Print the path and return on
        // reaching the destination node
        printPath(stack);
        return;
    }
    vis[x] = true;

    // If backtracking is taking place    
    if (v[x].length > 0)
    {
        for(let j = 0; j < v[x].length; j++)
        {

            // If the node is not visited
            if (vis[v[x][j]] == false)
            {
                DFS(vis, v[x][j], y, stack);
            }
        }
    }
    stack.pop();
}

// A utility function to initialise
// visited for the node and call
// DFS function for a given vertex x.
function DFSCall(x, y, n, stack)
{

    // Visited array
    let vis = new Array(n + 1);
    for(let i = 0; i < (n + 1); i++)
    {
        vis[i] = false;
    }

    // memset(vis, false, sizeof(vis))

    // DFS function call
    DFS(vis, x, y, stack);
}

// Driver code
for(let i = 0; i < 100; i++)
{
    v.push([]);
}

let n = 10;
let stack = [];

// Vertex numbers should be from 1 to 9.
addEdge(1, 2);
addEdge(1, 3);
addEdge(2, 4);
addEdge(2, 5);
addEdge(2, 6);
addEdge(3, 7);
addEdge(3, 8);
addEdge(3, 9);

// Function Call
DFSCall(4, 8, n, stack);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
4 -> 2 -> 1 -> 3 -> 8
```

**有效方法:**

在这种方法中，我们将利用 [<u>【最低共同祖先】</u>](https://www.geeksforgeeks.org/lca-for-general-or-n-ary-trees-sparse-matrix-dp-approach-onlogn-ologn/) (LCA)的概念。

1.我们将使用 DFS 找到每个节点的级别和父节点。

2.我们将找到两个给定节点的最低共同祖先。

3.从第一个节点开始，我们将前往生命周期评价，并继续推进

路径向量中的中间节点。

4.然后，从第二个节点，我们将再次前往 LCA，但这一次

我们将反转遇到的中间节点，然后将它们推入

我们的路径向量。

5.最后，打印路径向量以获得两个节点之间的路径。

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// An utility function to add an edge in the tree
void addEdge(vector<int> adj[], int x,
             int y)
{
    adj[x].push_back(y);
    adj[y].push_back(x);
}

// running dfs to find level and parent of every node
void dfs(vector<int> adj[], int node, int l,
            int p, int lvl[], int par[])
{
   lvl[node] = l;
   par[node] = p;

   for(int child : adj[node])
   {
      if(child != p)
        dfs(adj, child, l+1, node, lvl, par);
   }
}

int LCA(int a, int b, int par[], int lvl[])
{ 
   // if node a is at deeper level than
   // node b
   if(lvl[a] > lvl[b])
    swap(a, b);

   // finding the difference in levels
   // of node a and b
   int diff = lvl[b] - lvl[a];

   // moving b to the level of a
   while(diff != 0)
   {
      b = par[b];
      diff--;
   }

   // means we have found the LCA
   if(a == b)
    return a;

   // finding the LCA
   while(a != b)
    a=par[a], b=par[b];

   return a;
}

void printPath(vector<int> adj[], int a, int b, int n)
{
    // stores level of every node
    int lvl[n+1];

    // stores parent of every node
    int par[n+1];

    // running dfs to find parent and level
    // of every node in the tree
    dfs(adj, 1, 0, -1, lvl, par);

    // finding the lowest common ancestor
    // of the nodes a and b
    int lca = LCA(a, b, par, lvl);

    // stores path between nodes a and b
    vector<int> path;

    // traversing the path from a to lca
    while(a != lca)
      path.push_back(a), a = par[a];

    path.push_back(a);

    vector<int> temp;

    // traversing the path from b to lca
    while(b != lca)
      temp.push_back(b), b=par[b];

    // reversing the path to get actual path
    reverse(temp.begin(), temp.end());

    for(int x : temp)
      path.push_back(x);

    // printing the path
    for(int i = 0; i < path.size() - 1; i++)
      cout << path[i] << " -> ";

    cout << path[path.size() - 1] << endl;
}

// Driver Code
int main()
{  
  /*                          1

                        /            \

                     2                7

               /             \

             3                6

    /        |        \

  4          8          5

 */
    // number of nodes in the tree
    int n = 8;

    // adjacency list representation of the tree
    vector<int> adj[n+1];

    addEdge(adj, 1, 2);
    addEdge(adj, 1, 7);
    addEdge(adj, 2, 3);
    addEdge(adj, 2, 6);
    addEdge(adj, 3, 4);
    addEdge(adj, 3, 8);
    addEdge(adj, 3, 5);

    // taking two input nodes
    // between which path is
    // to be printed
    int a = 4, b = 7;

    printPath(adj, a, b, n);

    return 0;
}
```

**Output**

```
4 -> 3 -> 2 -> 1 -> 7
```

**时间复杂度:** O(N)

**空间复杂度:** O(N)