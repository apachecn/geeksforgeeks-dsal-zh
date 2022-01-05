# 给定树中所有可能路径的长度总和

> 原文:[https://www . geesforgeks . org/给定树中所有可能路径的长度总和/](https://www.geeksforgeeks.org/sum-of-lengths-of-all-paths-possible-in-a-given-tree/)

给定一棵具有 **N** 个节点的树，任务是找出所有路径的长度之和。树中两个节点的路径长度是路径上的边数，对于树中两个相邻的节点，路径的长度是 1。

**示例:**

```
Input:
       0
     /   \
   1      2
 /  \
3    4 
Output: 18
Paths of length 1 = (0, 1), (0, 2), (1, 3), (1, 4) = 4
Paths of length 2 = (0, 3), (0, 4), (1, 2), (3, 4) = 4
Paths of length 3 = (3, 2), (4, 2) = 2
The sum of lengths of all paths = 
    (4 * 1) + (4 * 2) + (2 * 3) = 18

Input:
       0
     /
   1
 /
2
Output: 4
```

**天真的方法:**检查所有可能的路径，然后添加它们来计算最终结果。这种方法的复杂性将是 0(T2 2)。

**高效进场:**可以注意到，一棵树的每一条边都是一座[桥](https://www.geeksforgeeks.org/bridge-in-a-graph/)。因此，该边将出现在该边所连接的两个子树之间的每条可能路径中。
例如，边(1–0)存在于{1，3，4}和{0，2}之间的每条可能路径中，(1–0)用于 6 倍于子树{1，3，4}的大小乘以子树{0，2}的大小。因此，对于每条边，计算这条边将被考虑多少次，以得到通过它的路径。 [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 可以用来存储子树的大小，所有边的贡献可以用另一个 DFS 来计算。这种方法的复杂性将是 **O(n)** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int sz = 1e5;

// Number of vertices
int n;

// Adjacency list representation
// of the tree
vector<int> tree[sz];

// Array that stores the subtree size
int subtree_size[sz];

// Array to mark all the
// vertices which are visited
int vis[sz];

// Utility function to create an
// edge between two vertices
void addEdge(int a, int b)
{

    // Add a to b's list
    tree[a].push_back(b);

    // Add b to a's list
    tree[b].push_back(a);
}

// Function to calculate the subtree size
int dfs(int node)
{

    // Mark visited
    vis[node] = 1;
    subtree_size[node] = 1;

    // For every adjacent node
    for (auto child : tree[node]) {

        // If not already visited
        if (!vis[child]) {

            // Recursive call for the child
            subtree_size[node] += dfs(child);
        }
    }
    return subtree_size[node];
}

// Function to calculate the
// contribution of each edge
void contribution(int node, int& ans)
{

    // Mark current node as visited
    vis[node] = true;

    // For every adjacent node
    for (int child : tree[node]) {

        // If it is not already visisted
        if (!vis[child]) {
            ans += (subtree_size[child]
                    * (n - subtree_size[child]));
            contribution(child, ans);
        }
    }
}

// Function to return the required sum
int getSum()
{

    // First pass of the dfs
    memset(vis, 0, sizeof(vis));
    dfs(0);

    // Second pass
    int ans = 0;
    memset(vis, 0, sizeof(vis));
    contribution(0, ans);

    return ans;
}

// Driver code
int main()
{
    n = 5;

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(1, 4);

    cout << getSum();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

@SuppressWarnings("unchecked")
class GFG{

static int sz = 100005;

// Number of vertices
static int n;

// Adjacency list representation
// of the tree
static ArrayList []tree = new ArrayList[sz];

// Array that stores the subtree size
static int []subtree_size = new int[sz];

// Array to mark all the
// vertices which are visited
static int []vis = new int[sz];

// Utility function to create an
// edge between two vertices
static void AddEdge(int a, int b)
{

    // Add a to b's list
    tree[a].add(b);

    // Add b to a's list
    tree[b].add(a);
}

// Function to calculate the subtree size
static int dfs(int node)
{

    // Mark visited
    vis[node] = 1;
    subtree_size[node] = 1;

    // For every adjacent node
    for(int child : (ArrayList<Integer>)tree[node])
    {

        // If not already visited
        if (vis[child] == 0)
        {

            // Recursive call for the child
            subtree_size[node] += dfs(child);
        }
    }
    return subtree_size[node];
}

// Function to calculate the
// contribution of each edge
static int contribution(int node, int ans)
{

    // Mark current node as visited
    vis[node] = 1;

    // For every adjacent node
    for(int child : (ArrayList<Integer>)tree[node])
    {

        // If it is not already visisted
        if (vis[child] == 0)
        {
            ans += (subtree_size[child] *
               (n - subtree_size[child]));
            ans = contribution(child, ans);
        }
    }
    return ans;
}

// Function to return the required sum
static int getSum()
{

    // First pass of the dfs
    Arrays.fill(vis, 0);
    dfs(0);

    // Second pass
    int ans = 0;
    Arrays.fill(vis, 0);
    ans = contribution(0, ans);

    return ans;
}

// Driver code
public static void main(String []args)
{
    n = 5;

    for(int i = 0; i < sz; i++)
    {
        tree[i] = new ArrayList();
    }

    AddEdge(0, 1);
    AddEdge(0, 2);
    AddEdge(1, 3);
    AddEdge(1, 4);

    System.out.println(getSum());
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python3 implementation of the approach
sz = 10**5

# Number of vertices
n = 5
an = 0

# Adjacency list representation
# of the tree
tree = [[] for i in range(sz)]

# Array that stores the subtree size
subtree_size = [0] * sz

# Array to mark all the
# vertices which are visited
vis = [0] * sz

# Utility function to create an
# edge between two vertices
def addEdge(a, b):

    # Add a to b's list
    tree[a].append(b)

    # Add b to a's list
    tree[b].append(a)

# Function to calculate the subtree size
def dfs(node):
    leaf = True

    # Mark visited
    vis[node] = 1

    # For every adjacent node
    for child in tree[node]:

        # If not already visited
        if (vis[child] == 0):
            leaf = False
            dfs(child)

            # Recursive call for the child
            subtree_size[node] += subtree_size[child]

    if leaf:
        subtree_size[node] = 1

# Function to calculate the
# contribution of each edge
def contribution(node,ans):
    global an

    # Mark current node as visited
    vis[node] = 1

    # For every adjacent node
    for child in tree[node]:

        # If it is not already visisted
        if (vis[child] == 0):
            an += (subtree_size[child] *
              (n - subtree_size[child]))
            contribution(child, ans)

# Function to return the required sum
def getSum():

    # First pass of the dfs
    for i in range(sz):
        vis[i] = 0
    dfs(0)

    # Second pass
    ans = 0
    for i in range(sz):
        vis[i] = 0

    contribution(0, ans)

    return an

# Driver code
n = 5

addEdge(0, 1)
addEdge(0, 2)
addEdge(1, 3)
addEdge(1, 4)

print(getSum())

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

static int sz = 100005;

// Number of vertices
static int n;

// Adjacency list representation
// of the tree
static ArrayList []tree = new ArrayList[sz];

// Array that stores the subtree size
static int []subtree_size = new int[sz];

// Array to mark all the
// vertices which are visited
static int []vis = new int[sz];

// Utility function to create an
// edge between two vertices
static void addEdge(int a, int b)
{

    // Add a to b's list
    tree[a].Add(b);

    // Add b to a's list
    tree[b].Add(a);
}

// Function to calculate the subtree size
static int dfs(int node)
{

    // Mark visited
    vis[node] = 1;
    subtree_size[node] = 1;

    // For every adjacent node
    foreach(int child in tree[node])
    {

        // If not already visited
        if (vis[child] == 0)
        {

            // Recursive call for the child
            subtree_size[node] += dfs(child);
        }
    }
    return subtree_size[node];
}

// Function to calculate the
// contribution of each edge
static void contribution(int node, ref int ans)
{

    // Mark current node as visited
    vis[node] = 1;

    // For every adjacent node
    foreach(int child in tree[node])
    {

        // If it is not already visisted
        if (vis[child] == 0)
        {
            ans += (subtree_size[child] *
               (n - subtree_size[child]));
            contribution(child, ref ans);
        }
    }
}

// Function to return the required sum
static int getSum()
{

    // First pass of the dfs
    Array.Fill(vis, 0);
    dfs(0);

    // Second pass
    int ans = 0;
    Array.Fill(vis, 0);
    contribution(0, ref ans);

    return ans;
}

// Driver code
public static void Main()
{
    n = 5;

    for(int i = 0; i < sz; i++)
    {
        tree[i] = new ArrayList();
    }

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(1, 4);

    Console.Write(getSum());
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let sz = 100005;

// Number of vertices
let  n;
// Adjacency list representation
// of the tree
let tree = new Array(sz);
// Array that stores the subtree size
let subtree_size = new Array(sz);
// Array to mark all the
// vertices which are visited
let vis = new Array(sz);

// Utility function to create an
// edge between two vertices
function AddEdge(a,b)
{
    // Add a to b's list
    tree[a].push(b);

    // Add b to a's list
    tree[b].push(a);
}

// Function to calculate the subtree size
function dfs(node)
{
    // Mark visited
    vis[node] = 1;
    subtree_size[node] = 1;

    // For every adjacent node
    for(let child=0;child<tree[node].length;child++)
    {

        // If not already visited
        if (vis[tree[node][child]] == 0)
        {

            // Recursive call for the child
            subtree_size[node] += dfs(tree[node][child]);
        }
    }
    return subtree_size[node];
}

// Function to calculate the
// contribution of each edge
function contribution(node,ans)
{
    // Mark current node as visited
    vis[node] = 1;

    // For every adjacent node
    for(let child=0;child<tree[node].length;child++)
    {

        // If it is not already visisted
        if (vis[tree[node][child]] == 0)
        {
            ans += (subtree_size[tree[node][child]] *
               (n - subtree_size[tree[node][child]]));
            ans = contribution(tree[node][child], ans);
        }
    }
    return ans;
}

// Function to return the required sum
function getSum()
{
    // First pass of the dfs
    for(let i=0;i<vis.length;i++)
    {
        vis[i]=0;
    }
    dfs(0);

    // Second pass
    let ans = 0;
    for(let i=0;i<vis.length;i++)
    {
        vis[i]=0;
    }
    ans = contribution(0, ans);

    return ans;
}

// Driver code
n = 5;

for(let i = 0; i < sz; i++)
{
    tree[i] = [];
}

AddEdge(0, 1);
AddEdge(0, 2);
AddEdge(1, 3);
AddEdge(1, 4);

document.write(getSum());

// This code is contributed by patel2127
</script>
```

**Output:**

```
18
```