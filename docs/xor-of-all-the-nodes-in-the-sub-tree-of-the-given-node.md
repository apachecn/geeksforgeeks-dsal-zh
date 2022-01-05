# 给定节点的子树中所有节点的异或

> 原文:[https://www . geesforgeks . org/给定节点的子树中所有节点的异或/](https://www.geeksforgeeks.org/xor-of-all-the-nodes-in-the-sub-tree-of-the-given-node/)

给定一个 n 元树和 **Q** 查询，其中每个查询由一个整数 **u** 组成，表示一个节点。任务是打印给定节点的子树中所有节点值的异或。
**例:**

> **输入:**
> 
> ![](img/36c37d09437a34cd08f144c16e2ec63d.png)
> 
> q[] = {0，1，4，5}
> **输出:**
> 0
> 3
> 5
> 6
> 查询 1: (1 ^ 2 ^ 3 ^ 4 ^ 5 ^ 6 ^ 7) = 0
> 查询 2: (2 ^ 4 ^ 5) = 3
> 查询 3: (5) = 5
> 查询 4: (6) = 6

**天真的方法:**对于每个节点，我们必须为每个查询遍历树，找到子树所有节点的 xor。所以代码的复杂度会是 **O(N * Q)** 。
**高效的方法:**如果我们通过遍历总树一次来预先计算子树的所有节点的 xor，并且首先计算子节点的子树的所有节点的 xor，然后使用子节点的值来计算父节点的子树的所有节点的 xor。这样我们就可以计算出 **O(N)** 时间内的异或，并存储起来以备查询。当询问时，我们将在 **O(1)** 时间打印预先计算的值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Adjacency list of the graph
vector<vector<int> > graph;

// Value of the node
vector<int> values, xor_values;

// Function to pre-compute the xor values
int pre_compute_xor(int i, int prev)
{
    // xor of the sub-tree
    int x = values[i];

    for (int j = 0; j < graph[i].size(); j++)
        if (graph[i][j] != prev) {

            // xor x with xor of the sub-tree
            // of it child nodes
            x ^= pre_compute_xor(graph[i][j], i);
        }

    xor_values[i] = x;

    // Return the xor
    return x;
}

// Function to return the xor of
// the nodes of the sub-tree
// rooted at node u
int query(int u)
{
    return xor_values[u];
}

// Driver code
int main()
{
    int n = 7;

    graph.resize(n);
    xor_values.resize(n);

    // Create the graph
    graph[0].push_back(1);
    graph[0].push_back(2);
    graph[1].push_back(3);
    graph[1].push_back(4);
    graph[2].push_back(5);
    graph[2].push_back(6);

    // Set the values of the nodes
    values.push_back(1);
    values.push_back(2);
    values.push_back(3);
    values.push_back(4);
    values.push_back(5);
    values.push_back(6);
    values.push_back(7);

    // Pre-computation
    pre_compute_xor(0, -1);

    // Perform queries
    int queries[] = { 0, 1, 4, 5 };
    int q = sizeof(queries) / sizeof(queries[0]);
    for (int i = 0; i < q; i++)
        cout << query(queries[i]) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int n = 7;

// Adjacency list of the graph
static Vector<Integer> []graph = new Vector[n];

// Value of the node
static Vector<Integer> values = new Vector<Integer>(),
xor_values = new Vector<Integer>(n);

// Function to pre-compute the xor values
static int pre_compute_xor(int i, int prev)
{
    // xor of the sub-tree
    int x = values.get(i);

    for (int j = 0; j < graph[i].size(); j++)
        if (graph[i].get(j)!= prev)
        {

            // xor x with xor of the sub-tree
            // of it child nodes
            x ^= pre_compute_xor(graph[i].get(j), i);
        }
    xor_values.remove(i);
    xor_values.add(i, x);

    // Return the xor
    return x;
}

// Function to return the xor of
// the nodes of the sub-tree
// rooted at node u
static int query(int u)
{
    return xor_values.get(u);
}

// Driver code
public static void main(String[] args)
{

    for(int i = 0; i < n; i++)
    {
        graph[i] = new Vector<Integer>();
        xor_values.add(0);
    }

    // Create the graph
    graph[0].add(1);
    graph[0].add(2);
    graph[1].add(3);
    graph[1].add(4);
    graph[2].add(5);
    graph[2].add(6);

    // Set the values of the nodes
    values.add(1);
    values.add(2);
    values.add(3);
    values.add(4);
    values.add(5);
    values.add(6);
    values.add(7);

    // Pre-computation
    pre_compute_xor(0, -1);

    // Perform queries
    int queries[] = { 0, 1, 4, 5 };
    int q = queries.length;
    for (int i = 0; i < q; i++)
        System.out.print(query(queries[i]) +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Adjacency list of the graph
graph = []

# Value of the node
values = []
xor_values = []

# Function to pre-compute the xor values
def pre_compute_xor(i, prev):

    # xor of the sub-tree
    x = values[i]

    for j in range(len(graph[i])):
        if graph[i][j] != prev:

            # xor x with xor of the sub-tree
            # of it child nodes
            x ^= pre_compute_xor(graph[i][j], i)

    xor_values[i] = x

    # Return the xor
    return x

# Function to return the xor of
# the nodes of the sub-tree
# rooted at node u
def query(u):

    return xor_values[u]

# Driver code
n = 7
for i in range(n):
    graph.append([])
    xor_values.append(0)

# Create the graph
graph[0].append(1)
graph[0].append(2)
graph[1].append(3)
graph[1].append(4)
graph[2].append(5)
graph[2].append(6)

# Set the values of the nodes
values.append(1)
values.append(2)
values.append(3)
values.append(4)
values.append(5)
values.append(6)
values.append(7)

# Pre-computation
pre_compute_xor(0, -1)

# Perform queries
queries = [ 0, 1, 4, 5 ]
q = len(queries)
for i in range(q):
    print(query(queries[i]))

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static int n = 7;

// Adjacency list of the graph
static List<int> []graph = new List<int>[n];

// Value of the node
static List<int> values = new List<int>(),
xor_values = new List<int>(n);

// Function to pre-compute the xor values
static int pre_compute_xor(int i, int prev)
{
    // xor of the sub-tree
    int x = values[i];

    for (int j = 0; j < graph[i].Count; j++)
        if (graph[i][j] != prev)
        {

            // xor x with xor of the sub-tree
            // of it child nodes
            x ^= pre_compute_xor(graph[i][j], i);
        }
    xor_values.RemoveAt(i);
    xor_values.Insert(i, x);

    // Return the xor
    return x;
}

// Function to return the xor of
// the nodes of the sub-tree
// rooted at node u
static int query(int u)
{
    return xor_values[u];
}

// Driver code
public static void Main(String[] args)
{

    for(int i = 0; i < n; i++)
    {
        graph[i] = new List<int>();
        xor_values.Add(0);
    }

    // Create the graph
    graph[0].Add(1);
    graph[0].Add(2);
    graph[1].Add(3);
    graph[1].Add(4);
    graph[2].Add(5);
    graph[2].Add(6);

    // Set the values of the nodes
    values.Add(1);
    values.Add(2);
    values.Add(3);
    values.Add(4);
    values.Add(5);
    values.Add(6);
    values.Add(7);

    // Pre-computation
    pre_compute_xor(0, -1);

    // Perform queries
    int []queries = { 0, 1, 4, 5 };
    int q = queries.Length;
    for (int i = 0; i < q; i++)
        Console.Write(query(queries[i]) +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let n = 7;

// Adjacency list of the graph
let graph = new Array(n);

// Value of the node
let values = new Array();
let xor_values = new Array(n);

// Function to pre-compute the xor values
function pre_compute_xor(i, prev) {
    // xor of the sub-tree
    let x = values[i];

    for (let j = 0; j < graph[i].length; j++)
        if (graph[i][j] != prev) {

            // xor x with xor of the sub-tree
            // of it child nodes
            x ^= pre_compute_xor(graph[i][j], i);
        }
    xor_values.splice(i, 1);
    xor_values.splice(i, 0, x);

    // Return the xor
    return x;
}

// Function to return the xor of
// the nodes of the sub-tree
// rooted at node u
function query(u) {
    return xor_values[u];
}

// Driver code

for (let i = 0; i < n; i++) {
    graph[i] = new Array();
    xor_values.push(0);
}

// Create the graph
graph[0].push(1);
graph[0].push(2);
graph[1].push(3);
graph[1].push(4);
graph[2].push(5);
graph[2].push(6);

// Set the values of the nodes
values.push(1);
values.push(2);
values.push(3);
values.push(4);
values.push(5);
values.push(6);
values.push(7);

// Pre-computation
pre_compute_xor(0, -1);

// Perform queries
let queries = [0, 1, 4, 5];
let q = queries.length;
for (let i = 0; i < q; i++)
    document.write(query(queries[i]) + "<br>");

// This code is contributed by gfgking

</script>
```

**Output:** 

```
0
3
5
6
```