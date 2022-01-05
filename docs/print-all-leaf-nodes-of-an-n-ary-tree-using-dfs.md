# 使用 DFS 打印 n 元树的所有叶节点

> 原文:[https://www . geesforgeks . org/print-n 元树的所有叶节点-使用-dfs/](https://www.geeksforgeeks.org/print-all-leaf-nodes-of-an-n-ary-tree-using-dfs/)

给定一个数组**边[][2]** ，其中**(边[i][0]，边[i][1])** 定义了 n 元树中的一条边，任务是使用打印给定树的所有叶节点。

**示例:**

```
Input: edge[][] = {{1, 2}, {1, 3}, {2, 4}, {2, 5}, {3, 6}}
Output: 4 5 6
    1
   / \
  2   3
 / \   \
4   5   6

Input: edge[][] = {{1, 5}, {1, 7}, {5, 6}}
Output: 6 7
```

**方法:** [DFS](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/) 可以用来遍历完整的树。我们将在遍历时跟踪父节点，以避免访问节点数组。最初，我们可以为每个节点设置一个标志，如果该节点至少有一个子节点(即非叶节点)，那么我们将重置该标志。没有子节点的节点是叶节点。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform DFS on the tree
void dfs(list<int> t[], int node, int parent)
{
    int flag = 1;

    // Iterating the children of current node
    for (auto ir : t[node]) {

        // There is at least a child
        // of the current node
        if (ir != parent) {
            flag = 0;
            dfs(t, ir, node);
        }
    }

    // Current node is connected to only
    // its parent i.e. it is a leaf node
    if (flag == 1)
        cout << node << " ";
}

// Driver code
int main()
{
    // Adjacency list
    list<int> t[1005];

    // List of all edges
    pair<int, int> edges[] = { { 1, 2 },
                               { 1, 3 },
                               { 2, 4 },
                               { 3, 5 },
                               { 3, 6 },
                               { 3, 7 },
                               { 6, 8 } };

    // Count of edges
    int cnt = sizeof(edges) / sizeof(edges[0]);

    // Number of nodes
    int node = cnt + 1;

    // Create the tree
    for (int i = 0; i < cnt; i++) {
        t[edges[i].first].push_back(edges[i].second);
        t[edges[i].second].push_back(edges[i].first);
    }

    // Function call
    dfs(t, 1, 0);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Pair class
static class pair
{
    int first,second;
    pair(int a, int b)
    {
        first = a;
        second = b;
    }
}

// Function to perform DFS on the tree
static void dfs(Vector t, int node, int parent)
{
    int flag = 1;

    // Iterating the children of current node
    for (int i = 0; i < ((Vector)t.get(node)).size(); i++)
    {
        int ir = (int)((Vector)t.get(node)).get(i);

        // There is at least a child
        // of the current node
        if (ir != parent)
        {
            flag = 0;
            dfs(t, ir, node);
        }
    }

    // Current node is connected to only
    // its parent i.e. it is a leaf node
    if (flag == 1)
        System.out.print( node + " ");
}

// Driver code
public static void main(String args[])
{
    // Adjacency list
    Vector t = new Vector();

    // List of all edges
    pair edges[] = { new pair( 1, 2 ),
                    new pair( 1, 3 ),
                    new pair( 2, 4 ),
                    new pair( 3, 5 ),
                    new pair( 3, 6 ),
                    new pair( 3, 7 ),
                    new pair( 6, 8 ) };

    // Count of edges
    int cnt = edges.length;

    // Number of nodes
    int node = cnt + 1;

    for(int i = 0; i < 1005; i++)
    {
        t.add(new Vector());
    }

    // Create the tree
    for (int i = 0; i < cnt; i++)
    {
        ((Vector)t.get(edges[i].first)).add(edges[i].second);
        ((Vector)t.get(edges[i].second)).add(edges[i].first);
    }

    // Function call
    dfs(t, 1, 0);
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
t = [[] for i in range(1005)]

# Function to perform DFS on the tree
def dfs(node, parent):
    flag = 1

    # Iterating the children of current node
    for ir in t[node]:

        # There is at least a child
        # of the current node
        if (ir != parent):
            flag = 0
            dfs(ir, node)

    # Current node is connected to only
    # its parent i.e. it is a leaf node
    if (flag == 1):
        print(node, end = " ")

# Driver code

# List of all edges
edges = [[ 1, 2 ],
         [ 1, 3 ],
         [ 2, 4 ],
         [ 3, 5 ],
         [ 3, 6 ],
         [ 3, 7 ],
         [ 6, 8 ]]

# Count of edges
cnt = len(edges)

# Number of nodes
node = cnt + 1

# Create the tree
for i in range(cnt):
    t[edges[i][0]].append(edges[i][1])
    t[edges[i][1]].append(edges[i][0])

# Function call
dfs(1, 0)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System.Collections;
using System.Collections.Generic;
using System;

class GFG{

// Pair class
class pair
{
    public int first, second;
    public pair(int a, int b)
    {
        first = a;
        second = b;
    }
}

// Function to perform DFS on the tree
static void dfs(ArrayList t, int node,
                             int parent)
{
    int flag = 1;

    // Iterating the children of current node
    for(int i = 0;
            i < ((ArrayList)t[node]).Count;
            i++)
    {
        int ir = (int)((ArrayList)t[node])[i];

        // There is at least a child
        // of the current node
        if (ir != parent)
        {
            flag = 0;
            dfs(t, ir, node);
        }
    }

    // Current node is connected to only
    // its parent i.e. it is a leaf node
    if (flag == 1)
        Console.Write( node + " ");
}

// Driver code
public static void Main(string []args)
{

    // Adjacency list
    ArrayList t = new ArrayList();

    // List of all edges
    pair []edges = { new pair(1, 2),
                     new pair(1, 3),
                     new pair(2, 4),
                     new pair(3, 5),
                     new pair(3, 6),
                     new pair(3, 7),
                     new pair(6, 8) };

    // Count of edges
    int cnt = edges.Length;

    for(int i = 0; i < 1005; i++)
    {
        t.Add(new ArrayList());
    }

    // Create the tree
    for(int i = 0; i < cnt; i++)
    {
        ((ArrayList)t[edges[i].first]).Add(
            edges[i].second);
        ((ArrayList)t[edges[i].second]).Add(
            edges[i].first);
    }

    // Function call
    dfs(t, 1, 0);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to perform DFS on the tree
function dfs(t, node, parent)
{
    let flag = 1;

    // Iterating the children of current node
    for(let i = 0; i < t[node].length; i++)
    {
        let ir = t[node][i];

        // There is at least a child
        // of the current node
        if (ir != parent)
        {
            flag = 0;
            dfs(t, ir, node);
        }
    }

    // Current node is connected to only
    // its parent i.e. it is a leaf node
    if (flag == 1)
        document.write( node + " ");
}

// Driver code

// Adjacency list
let t = []

// List of all edges
let edges = [ [ 1, 2 ], [ 1, 3 ],
              [ 2, 4 ], [ 3, 5 ],
              [ 3, 6 ], [ 3, 7 ],
              [ 6, 8 ] ];

// Count of edges
let cnt = edges.length;

// Number of nodes
let node = cnt + 1;

for(let i = 0; i < 1005; i++)
{
    t.push([]);
}

// Create the tree
for(let i = 0; i < cnt; i++)
{
    t[edges[i][0]].push(edges[i][1])
    t[edges[i][1]].push(edges[i][0])
}

// Function call
dfs(t, 1, 0);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
4 5 8 7
```

**时间复杂度:** O(N)，其中 N 为图中节点数。
**辅助空间:** O(N)