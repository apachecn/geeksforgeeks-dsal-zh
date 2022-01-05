# 求图的最大值排列

> 原文:[https://www . geesforgeks . org/find-最大值-图形置换/](https://www.geeksforgeeks.org/find-the-maximum-value-permutation-of-a-graph/)

给定一个包含 **N 个**节点的图。对于节点的任何排列 **P <sub>1</sub> ，P <sub>2</sub> ，P <sub>3</sub> ，…，P <sub>N</sub>** 排列的值被定义为在其左侧至少有一个节点与其有边的索引的数量。找出所有排列的最大值。
**示例:**

> **输入:** N = 3，边[] = {{1，2}，{2，3}}
> **输出:** 2
> 考虑排列 2 1 3
> 节点 1 左边有节点 2，图中有一条边连接它们。
> 节点 3 的左边有节点 2，图中有一条边连接它们。
> **输入:** N = 4，边[] = {{1，3}，{2，4}}
> **输出:** 2
> 考虑排列 1 2 3 4
> 节点 3 左边有节点 1，图中有边连接它们。
> 节点 4 的左边有节点 2，图中有一条边连接它们。

**逼近:**让我们从开头的任意一个节点开始，我们可以用与之相邻的任意一个节点跟上去，重复这个过程。这类似于 dfs 遍历，其中除了第一个节点之外，每个节点之前都有一个与其共享一条边的节点。因此，对于每个连接的组件，我们可以得到该组件节点排列的最大值是组件的**大小–1**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of nodes
// in the current connected component
int dfs(int x, vector<int> adj[], int vis[])
{
    // Initialise size to 1
    int sz = 1;

    // Mark the node as visited
    vis[x] = 1;

    // Start a dfs for every unvisited
    // adjacent node
    for (auto ch : adj[x])
        if (!vis[ch])
            sz += dfs(ch, adj, vis);

    // Return the number of nodes in
    // the current connected component
    return sz;
}

// Function to return the maximum value
// of the required permutation
int maxValue(int n, vector<int> adj[])
{
    int val = 0;
    int vis[n + 1] = { 0 };

    // For each connected component
    // add the corresponding value
    for (int i = 1; i <= n; i++)
        if (!vis[i])
            val += dfs(i, adj, vis) - 1;
    return val;
}

// Driver code
int main()
{
    int n = 3;
    vector<int> adj[n + 1] = { { 1, 2 }, { 2, 3 } };
    cout << maxValue(n, adj);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int vis[];

// Function to return the number of nodes
// in the current connected component
static int dfs(int x, Vector<Vector<Integer>> adj)
{
    // Initialise size to 1
    int sz = 1;

    // Mark the node as visited
    vis[x] = 1;

    // Start a dfs for every unvisited
    // adjacent node
    for (int i = 0; i < adj.get(x).size(); i++)
        if (vis[adj.get(x).get(i)] == 0)
            sz += dfs(adj.get(x).get(i), adj);

    // Return the number of nodes in
    // the current connected component
    return sz;
}

// Function to return the maximum value
// of the required permutation
static int maxValue(int n, Vector<Vector<Integer>> adj)
{
    int val = 0;
    vis = new int[n + 1];

    for (int i = 0; i < n; i++)
    vis[i] = 0;

    // For each connected component
    // add the corresponding value
    for (int i = 0; i < n; i++)
        if (vis[i] == 0)
            val += dfs(i, adj) - 1;
    return val;
}

// Driver code
public static void main(String args[])
{
    int n = 3;
    Vector<Vector<Integer>> adj = new Vector<Vector<Integer>>() ;

    // create the graph
    Vector<Integer> v = new Vector<Integer>();
    v.add(0);
    v.add(1);
    Vector<Integer> v1 = new Vector<Integer>();
    v1.add(1);
    v1.add(2);

    adj.add(v);
    adj.add(v1);
    adj.add(new Vector<Integer>());

    System.out.println( maxValue(n, adj));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number of nodes
# in the current connected component
def dfs(x, adj, vis):

    # Initialise size to 1
    sz = 1

    # Mark the node as visited
    vis[x] = 1

    # Start a dfs for every unvisited
    # adjacent node
    for ch in adj:
        if (not vis[ch]):
            sz += dfs(ch, adj, vis)

    # Return the number of nodes in
    # the current connected component
    return sz

# Function to return the maximum value
# of the required permutation
def maxValue(n, adj):

    val = 0
    vis = [0] * (n + 1)

    # For each connected component
    # add the corresponding value
    for i in range(1, n + 1):
        if (not vis[i]):
            val += dfs(i, adj, vis) - 1
    return val

# Driver Code
if __name__ == '__main__':
    n = 3
    adj = [1, 2 , 2, 3]
    print(maxValue(n, adj))

# This code is contributed by
# SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static int []vis ;

// Function to return the number of nodes
// in the current connected component
static int dfs(int x, List<List<int>> adj)
{
    // Initialise size to 1
    int sz = 1;

    // Mark the node as visited
    vis[x] = 1;

    // Start a dfs for every unvisited
    // adjacent node
    for (int i = 0; i < adj[x].Count; i++)
        if (vis[adj[x][i]] == 0)
            sz += dfs(adj[x][i], adj);

    // Return the number of nodes in
    // the current connected component
    return sz;
}

// Function to return the maximum value
// of the required permutation
static int maxValue(int n, List<List<int>> adj)
{
    int val = 0;
    vis = new int[n + 1];

    for (int i = 0; i < n; i++)
        vis[i] = 0;

    // For each connected component
    // add the corresponding value
    for (int i = 0; i < n; i++)
        if (vis[i] == 0)
            val += dfs(i, adj) - 1;
    return val;
}

// Driver code
public static void Main(String []args)
{
    int n = 3;
    List<List<int>> adj = new List<List<int>>() ;

    // create the graph
    List<int> v = new List<int>();
    v.Add(0);
    v.Add(1);
    List<int> v1 = new List<int>();
    v1.Add(1);
    v1.Add(2);

    adj.Add(v);
    adj.Add(v1);
    adj.Add(new List<int>());

    Console.WriteLine( maxValue(n, adj));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the number of nodes
// in the current connected component
function dfs(x, adj, vis)
{
    if(x>1)
        return 1;

    // Initialise size to 1
    var sz = 1;

    // Mark the node as visited
    vis[x] = 1;
    // Start a dfs for every unvisited
    // adjacent node
    adj[x].forEach(ch => {

        if (!vis[ch])
            sz += dfs(ch, adj, vis);
    });

    // Return the number of nodes in
    // the current connected component
    return sz;
}

// Function to return the maximum value
// of the required permutation
function maxValue(n, adj)
{
    var val = 0;
    var vis = Array(n+1).fill(0);

    // For each connected component
    // add the corresponding value
    for (var i = 0; i < n; i++)
        if (!vis[i])
            val += dfs(i, adj, vis) - 1;
    return val;
}

// Driver code
var n = 2;
var adj =  [ [ 0, 1 ], [ 1, 2] ];
document.write( maxValue(n, adj));

// This code is contributed by famously.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)