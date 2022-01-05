# N 元树中深度最大的最小值节点

> 原文:[https://www . geeksforgeeks . org/最小值节点具有最大深度树/](https://www.geeksforgeeks.org/minimum-valued-node-having-maximum-depth-in-an-n-ary-tree/)

给定一个由 **N** 个节点组成的**树**，任务是从根节点开始寻找深度最大的节点，取深度为零的根节点。如果有 1 个以上的最大深度节点，则找到具有最小值的节点。

**例:**

```
Input:     
             1
           /   \
          2     3
         /  \
        4    5

Output: 4
Explanation:
For this tree: 
Height of Node 1 - 0, 
Height of Node 2 - 1, 
Height of Node 3 - 1, 
Height of Node 4 - 2, 
Height of Node 5 - 2\. 
Hence, the nodes whose height is 
maximum are 4 and 5, out of which 
4 is minimum valued.

Input:     
             1
           /   
          2   
         /
        3  

Output: 3
Explanation:
For this tree: 
Height of Node 1 - 0, 
Height of Node 2 - 1, 
Height of Node 3 - 2
Hence, the node whose height 
is maximum is 3.
```

**方法:**

*   The idea is to use [Depth First Search (DFS)](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/) on the tree. For each node, check the height of each node when we move down the tree.
*   Check whether it is the largest so far, and if its height is equal to the maximum, then whether it is the minimum node.
*   If so, update the maximum height and node values up to now accordingly.

下面是上述方法的实现:

## c++

```
// C++ implementation of for
// the above problem

#include <bits/stdc++.h>
using namespace std;

#define MAX 100000

vector<int> graph[MAX + 1];

// To store the height of each node
int maxHeight, minNode;

// Function to perform dfs
void dfs(int node, int parent,
         int h)
{
    // Store the height of node
    int height = h;

    if (height > maxHeight) {
        maxHeight = height;
        minNode = node;
    }
    else if (height == maxHeight
             && minNode > node)
        minNode = node;

    for (int to : graph[node]) {
        if (to == parent)
            continue;
        dfs(to, node, h + 1);
    }
}

// Driver code
int main()
{
    // Number of nodes
    int N = 5;

    // Edges of the tree
    graph[1].push_back(2);
    graph[1].push_back(3);
    graph[2].push_back(4);
    graph[2].push_back(5);

    maxHeight = 0;
    minNode = 1;

    dfs(1, 1, 0);

    cout << minNode << "\n";

    return 0;
}
```

## Java

```
// Java implementation of for
// the above problem
import java.util.*;

class GFG{

static final int MAX = 100000;
@SuppressWarnings("unchecked")
static Vector<Integer>[] graph = new Vector[MAX + 1];

// To store the height of each node
static int maxHeight, minNode;

// Function to perform dfs
static void dfs(int node, int parent, int h)
{

    // Store the height of node
    int height = h;
    if (height > maxHeight)
    {
        maxHeight = height;
        minNode = node;
    }
    else if (height == maxHeight &&
             minNode > node)
        minNode = node;

    for(int to : graph[node])
    {
        if (to == parent)
            continue;
        dfs(to, node, h + 1);
    }
}

// Driver code
public static void main(String[] args)
{
    // Number of nodes
    int N = 5;
    for(int i = 0; i < graph.length; i++)
        graph[i] = new Vector<Integer>();

    // Edges of the tree
    graph[1].add(2);
    graph[1].add(3);
    graph[2].add(4);
    graph[2].add(5);
    maxHeight = 0;
    minNode = 1;
    dfs(1, 1, 0);
    System.out.print(minNode + "\n");
}
}

// This code is contributed by sapnasingh4991
```

## python 3

```
# Python3 implementation of for
# the above problem
MAX = 100000

graph = [[] for i in range(MAX + 1)]

# To store the height of each node
maxHeight = 0
minNode = 0

# Function to perform dfs
def dfs(node, parent, h):

    global minNode, maxHeight

    # Store the height of node
    height = h

    if (height > maxHeight):
        maxHeight = height
        minNode = node

    elif (height == maxHeight and
          minNode > node):
        minNode = node

    for to in graph[node]:
        if to == parent:
            continue

        dfs(to, node, h + 1)

# Driver code
if __name__=="__main__":

    # Number of nodes
    N = 5

    # Edges of the tree
    graph[1].append(2)
    graph[1].append(3)
    graph[2].append(4)
    graph[2].append(5)

    maxHeight = 0
    minNode = 1

    dfs(1, 1, 0)

    print(minNode)

# This code is contributed by rutvik_56
```

## c#

```
// C# implementation of for
// the above problem
using System;
using System.Collections.Generic;

public class GFG{

static readonly int MAX = 100000;
static List<int>[] graph = new List<int>[MAX + 1];

// To store the height of each node
static int maxHeight, minNode;

// Function to perform dfs
static void dfs(int node, int parent, int h)
{

    // Store the height of node
    int height = h;
    if (height > maxHeight)
    {
        maxHeight = height;
        minNode = node;
    }
    else if (height == maxHeight &&
             minNode > node)
        minNode = node;

    foreach(int to in graph[node])
    {
        if (to == parent)
            continue;
        dfs(to, node, h + 1);
    }
}

// Driver code
public static void Main(String[] args)
{
    for(int i = 0; i < graph.Length; i++)
        graph[i] = new List<int>();

    // Edges of the tree
    graph[1].Add(2);
    graph[1].Add(3);
    graph[2].Add(4);
    graph[2].Add(5);
    maxHeight = 0;
    minNode = 1;
    dfs(1, 1, 0);
    Console.Write(minNode + "\n");
}
}

// This code is contributed by shikhasingrajput
```

## Javascript

```
<script>
    // Javascript implementation of for the above problem

    let MAX = 100000;
    let graph = new Array(MAX + 1);

    // To store the height of each node
    let maxHeight, minNode;

    // Function to perform dfs
    function dfs(node, parent, h)
    {

        // Store the height of node
        let height = h;
        if (height > maxHeight)
        {
            maxHeight = height;
            minNode = node;
        }
        else if (height == maxHeight &&
                 minNode > node)
            minNode = node;

        for(let to = 0; to < graph[node].length; to++)
        {
            if (graph[node][to] == parent)
                continue;
            dfs(graph[node][to], node, h + 1);
        }
    }

    for(let i = 0; i < graph.length; i++)
        graph[i] = [];

    // Edges of the tree
    graph[1].push(2);
    graph[1].push(3);
    graph[2].push(4);
    graph[2].push(5);
    maxHeight = 0;
    minNode = 1;
    dfs(1, 1, 0);
    document.write(minNode + "</br>");

// This code is contributed by decode2207.
</script>
```

**输出:**

```
4
```