# n 元树每个节点的子树中的叶节点数

> 原文:[https://www . geesforgeks . org/n 元树的每个节点的子树中的叶节点数/](https://www.geeksforgeeks.org/number-of-leaf-nodes-in-the-subtree-of-every-node-of-an-n-ary-tree/)

给定一个 [**N 元树**](https://www.geeksforgeeks.org/tag/n-ary-tree/) ，打印每个节点的子树中的叶节点数。
**例** :

```
Input:      
            1 
          /    \
         2      3
             /  |   \
            4   5    6
Output:
The node 1 has 4 leaf nodes
The node 2 has 1 leaf nodes
The node 3 has 3 leaf nodes
The node 4 has 1 leaf nodes
The node 5 has 1 leaf nodes
The node 6 has 1 leaf nodes
```

**逼近**:思路是对给定的树进行 DFS 遍历，对于每个节点保留一个数组 leaf【】，以存储其下子树的叶节点数。
现在，当沿树向下循环时，如果发现一个叶节点，将其叶[i]值设置为 1，并向上返回。现在，每次从向上的函数调用返回时，添加它下面的节点的叶节点。
一旦完成 DFS 遍历，我们将获得数组叶[]中叶节点的计数。
以下是上述方法的实施:

## C++

```
// C++ program to print the number of
// leaf nodes of every node
#include <bits/stdc++.h>
using namespace std;

// Function to insert edges of tree
void insert(int x, int y, vector<int> adjacency[])
{
    adjacency[x].push_back(y);
}

// Function to run DFS on a tree
void dfs(int node, int leaf[], int vis[],
         vector<int> adjacency[])
{
    leaf[node] = 0;
    vis[node] = 1;

    // iterate on all the nodes
    // connected to node
    for (auto it : adjacency[node]) {

        // If not visited
        if (!vis[it]) {
            dfs(it, leaf, vis, adjacency);
            leaf[node] += leaf[it];
        }
    }

    if (!adjacency[node].size())
        leaf[node] = 1;
}

// Function to print number of
// leaf nodes of a node
void printLeaf(int n, int leaf[])
{
    // Function to print leaf nodes
    for (int i = 1; i <= n; i++) {
        cout << "The node " << i << " has "
             << leaf[i] << " leaf nodes\n";
    }
}

// Driver Code
int main()
{
    // Given N-ary Tree

    /*     1
         /   \
        2     3
            / | \
            4 5 6 */

    int N = 6; // no of nodes
    vector<int> adjacency[N + 1]; // adjacency list for tree

    insert(1, 2, adjacency);
    insert(1, 3, adjacency);
    insert(3, 4, adjacency);
    insert(3, 5, adjacency);
    insert(3, 6, adjacency);

    int leaf[N + 1]; // Store count of leaf in subtree of i
    int vis[N + 1] = { 0 }; // mark nodes visited

    dfs(1, leaf, vis, adjacency);

    printLeaf(N, leaf);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the number of
// leaf nodes of every node
import java.util.*;

class GFG
{
static Vector<Vector<Integer>> adjacency = new
       Vector<Vector<Integer>>();

// Function to insert edges of tree
static void insert(int x, int y)
{
    adjacency.get(x).add(y);
}

// Function to run DFS on a tree
static void dfs(int node, int leaf[], int vis[])
{
    leaf[node] = 0;
    vis[node] = 1;

    // iterate on all the nodes
    // connected to node
    for (int i = 0; i < adjacency.get(node).size(); i++)
    {
        int it = adjacency.get(node).get(i);

        // If not visited
        if (vis[it] == 0)
        {
            dfs(it, leaf, vis);
            leaf[node] += leaf[it];
        }
    }

    if (adjacency.get(node).size() == 0)
        leaf[node] = 1;
}

// Function to print number of
// leaf nodes of a node
static void printLeaf(int n, int leaf[])
{
    // Function to print leaf nodes
    for (int i = 1; i <= n; i++)
    {
        System.out.print( "The node " + i + " has " +
                          leaf[i] + " leaf nodes\n");
    }
}

// Driver Code
public static void main(String args[])
{
    // Given N-ary Tree

    /*     1
        / \
        2     3
            / | \
            4 5 6 */

    int N = 6; // no of nodes

    for(int i = 0; i <= N; i++)
    adjacency.add(new Vector<Integer>());

    insert(1, 2);
    insert(1, 3);
    insert(3, 4);
    insert(3, 5);
    insert(3, 6);

    // Store count of leaf in subtree of i
    int leaf[] = new int[N + 1];

    // mark nodes visited
    int vis[] = new int[N + 1] ;

    dfs(1, leaf, vis);

    printLeaf(N, leaf);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to print the number of
# leaf nodes of every node
adjacency = [[] for i in range(100)]

# Function to insert edges of tree
def insert(x, y):
    adjacency[x].append(y)

# Function to run DFS on a tree
def dfs(node, leaf, vis):

    leaf[node] = 0
    vis[node] = 1

    # iterate on all the nodes
    # connected to node
    for it in adjacency[node]:

        # If not visited
        if (vis[it] == False):
            dfs(it, leaf, vis)
            leaf[node] += leaf[it]

    if (len(adjacency[node]) == 0):
        leaf[node] = 1

# Function to prnumber of
# leaf nodes of a node
def printLeaf(n, leaf):

    # Function to prleaf nodes
    for i in range(1, n + 1):
        print("The node", i, "has", 
               leaf[i], "leaf nodes")

# Driver Code

# Given N-ary Tree
'''
/*     1
    / \
    2     3
        / | \
        4 5 6 '''

N = 6 # no of nodes
# adjacency list for tree

insert(1, 2)
insert(1, 3)
insert(3, 4)
insert(3, 5)
insert(3, 6)

# Store count of leaf in subtree of i
leaf = [0 for i in range(N + 1)]

# mark nodes visited
vis = [0 for i in range(N + 1)]

dfs(1, leaf, vis)

printLeaf(N, leaf)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to print the number of
// leaf nodes of every node
using System;
using System.Collections.Generic;

class GFG
{
static List<List<int>> adjacency = new
       List<List<int>>();

// Function to insert edges of tree
static void insert(int x, int y)
{
    adjacency[x].Add(y);
}

// Function to run DFS on a tree
static void dfs(int node, int []leaf, int []vis)
{
    leaf[node] = 0;
    vis[node] = 1;

    // iterate on all the nodes
    // connected to node
    for (int i = 0; i < adjacency[node].Count; i++)
    {
        int it = adjacency[node][i];

        // If not visited
        if (vis[it] == 0)
        {
            dfs(it, leaf, vis);
            leaf[node] += leaf[it];
        }
    }

    if (adjacency[node].Count == 0)
        leaf[node] = 1;
}

// Function to print number of
// leaf nodes of a node
static void printLeaf(int n, int []leaf)
{
    // Function to print leaf nodes
    for (int i = 1; i <= n; i++)
    {
        Console.Write( "The node " + i + " has " +
                          leaf[i] + " leaf nodes\n");
    }
}

// Driver Code
public static void Main(String []args)
{
    // Given N-ary Tree

    /*     1
        / \
        2     3
            / | \
            4 5 6 */

    int N = 6; // no of nodes

    for(int i = 0; i <= N; i++)
    adjacency.Add(new List<int>());

    insert(1, 2);
    insert(1, 3);
    insert(3, 4);
    insert(3, 5);
    insert(3, 6);

    // Store count of leaf in subtree of i
    int []leaf = new int[N + 1];

    // mark nodes visited
    int []vis = new int[N + 1] ;

    dfs(1, leaf, vis);

    printLeaf(N, leaf);
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to print the number of
// leaf nodes of every node

let adjacency = [];

// Function to insert edges of tree
function insert(x,y)
{
    adjacency[x].push(y);
}

// Function to run DFS on a tree
function dfs(node,leaf,vis)
{
    leaf[node] = 0;
    vis[node] = 1;

    // iterate on all the nodes
    // connected to node
    for (let i = 0; i < adjacency[node].length; i++)
    {
        let it = adjacency[node][i];

        // If not visited
        if (vis[it] == 0)
        {
            dfs(it, leaf, vis);
            leaf[node] += leaf[it];
        }
    }

    if (adjacency[node].length == 0)
        leaf[node] = 1;
}

// Function to print number of
// leaf nodes of a node
function printLeaf(n,leaf)
{
    // Function to print leaf nodes
    for (let i = 1; i <= n; i++)
    {
        document.write( "The node " + i + " has " +
                          leaf[i] + " leaf nodes<br>");
    }
}

// Driver Code

// Given N-ary Tree

/*     1
        / \
        2     3
            / | \
            4 5 6 */

let N = 6; // no of nodes

for(let i = 0; i <= N; i++)
    adjacency.push([]);

insert(1, 2);
insert(1, 3);
insert(3, 4);
insert(3, 5);
insert(3, 6);

// Store count of leaf in subtree of i
let leaf = new Array(N + 1);
for(let i=0;i<leaf.length;i++)
{
    leaf[i]=0;
}
// mark nodes visited
let vis = new Array(N + 1) ;
for(let i=0;i<vis.length;i++)
{
    vis[i]=0;
}

dfs(1, leaf, vis);

printLeaf(N, leaf);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
The node 1 has 4 leaf nodes
The node 2 has 1 leaf nodes
The node 3 has 3 leaf nodes
The node 4 has 1 leaf nodes
The node 5 has 1 leaf nodes
The node 6 has 1 leaf nodes
```