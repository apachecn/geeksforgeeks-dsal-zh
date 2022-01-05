# 为多个查询找到树中每个节点的父节点

> 原文:[https://www . geesforgeks . org/find-多查询树中每个节点的父节点/](https://www.geeksforgeeks.org/find-parent-of-each-node-in-a-tree-for-multiple-queries/)

给定一棵具有从 0 到 N–1 编号的 **N** 顶点的树和包含树中节点的 **Q** 查询，任务是为多个查询找到给定节点的父节点。将第 0 个节点视为根节点，并将根节点的父节点视为根本身。
**例:**

```
Tree:
      0
     /  \
    1    2
    |   / \
    3  4   5

Input: N = 2
Output: 0
Explanation:
Parent of node 2 is node 0 i.e root node

Input: N = 3
Output: 1
Explanation:
Parent of node 3 is node 1
```

**逼近** :
默认情况下，我们将根节点的父节点指定为根本身。然后，我们使用广度优先遍历(BFS)遍历树。当我们将节点 s 的子节点标记为已访问时，我们还会将这些子节点的父节点分配为节点 s。最后，对于不同的查询，会打印该节点的父[]的值。
以下是上述办法的实施:

## C++

```
// C++ implementation for
// the above approach

#include <bits/stdc++.h>
using namespace std;

const int sz = 1e5;

// Adjacency list representation
// of the tree
vector<int> tree[sz + 1];

// Boolean array to mark all the
// vertices which are visited
bool vis[sz + 1];

// Array of vector where ith index
// stores the path from the root
// node to the ith node
int ans[sz + 1];

// Function to create an
// edge between two vertices
void addEdge(int a, int b)
{

    // Add a to b's list
    tree[a].push_back(b);

    // Add b to a's list
    tree[b].push_back(a);
}

// Modified Breadth-First Function
void bfs(int node)
{

    // Create a queue of {child, parent}
    queue<pair<int, int> > qu;

    // Push root node in the front of
    qu.push({ node, 0 });

    while (!qu.empty()) {
        pair<int, int> p = qu.front();

        // Dequeue a vertex from queue
        qu.pop();
        ans[p.first] = p.second;
        vis[p.first] = true;

        // Get all adjacent vertices of the dequeued
        // vertex s. If any adjacent has not
        // been visited then enqueue it
        for (int child : tree[p.first]) {
            if (!vis[child]) {
                qu.push({ child, p.first });
            }
        }
    }
}

// Driver code
int main()
{

    // Number of vertices
    int n = 6;

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(2, 4);
    addEdge(2, 5);

    // Calling modified bfs function
    bfs(0);

    int q[] = { 2, 3 };

    for (int i = 0; i < 2; i++) {
        cout << ans[q[i]] << '\n';
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for
// the above approach
import java.util.*;

class GFG
{
static int sz = (int) 1e5;

// Adjacency list representation
// of the tree
static Vector<Integer> []tree = new Vector[sz + 1];

// Boolean array to mark all the
// vertices which are visited
static boolean []vis = new boolean[sz + 1];

// Array of vector where ith index
// stores the path from the root
// node to the ith node
static int []ans = new int[sz + 1];
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to create an
// edge between two vertices
static void addEdge(int a, int b)
{

    // Add a to b's list
    tree[a].add(b);

    // Add b to a's list
    tree[b].add(a);
}

// Modified Breadth-First Function
static void bfs(int node)
{

    // Create a queue of {child, parent}
    Queue<pair> qu = new LinkedList<>();

    // Push root node in the front of
    qu.add(new pair(node, 0 ));

    while (!qu.isEmpty())
    {
        pair p = qu.peek();

        // Dequeue a vertex from queue
        qu.remove();
        ans[p.first] = p.second;
        vis[p.first] = true;

        // Get all adjacent vertices of the dequeued
        // vertex s. If any adjacent has not
        // been visited then enqueue it
        for (int child : tree[p.first])
        {
            if (!vis[child])
            {
                qu.add(new pair(child, p.first ));
            }
        }
    }
}

// Driver code
public static void main(String[] args)
{

    // Number of vertices
    int n = 6;
    for (int i = 0; i < sz + 1; i++)
        tree[i] = new Vector<Integer>();

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(2, 4);
    addEdge(2, 5);

    // Calling modified bfs function
    bfs(0);

    int q[] = { 2, 3 };

    for (int i = 0; i < 2; i++)
    {
        System.out.println(ans[q[i]]);
    }
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation for
# the above approach

sz = 10**5

# Adjacency list representation
# of the tree
tree = [[] for _ in range(sz + 1)]

# Boolean array to mark all the
# vertices which are visited
vis = [0] * (sz + 1)

# Array of vector where ith index
# stores the path from the root
# node to the ith node
ans = [0] * (sz + 1)

# Function to create an
# edge between two vertices
def addEdge(a, b):

    # Add a to b's list
    tree[a].append(b)

    # Add b to a's list
    tree[b].append(a)

# Modified Breadth-First Function
def bfs(node):

    # Create a queue of child, parent
    qu = []

    # Push root node in the front of
    qu.append([node, 0])

    while (len(qu)):
        p = qu[0]

        # Dequeue a vertex from queue
        qu.pop(0)
        ans[p[0]] = p[1]
        vis[p[0]] = True

        # Get all adjacent vertices of the dequeued
        # vertex s. If any adjacent has not
        # been visited then enqueue it
        for child in tree[p[0]]:
            if (not vis[child]):
                qu.append([child, p[0]])

# Driver code

# Number of vertices
n = 6

addEdge(0, 1)
addEdge(0, 2)
addEdge(1, 3)
addEdge(2, 4)
addEdge(2, 5)

# Calling modified bfs function
bfs(0)

q = [2, 3]

for i in range(2):
    print(ans[q[i]])

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
static int sz = (int) 1e5;

// Adjacency list representation
// of the tree
static List<int> []tree = new List<int>[sz + 1];

// Boolean array to mark all the
// vertices which are visited
static Boolean []vis = new Boolean[sz + 1];

// Array of vector where ith index
// stores the path from the root
// node to the ith node
static int []ans = new int[sz + 1];
public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to create an
// edge between two vertices
static void addEdge(int a, int b)
{

    // Add a to b's list
    tree[a].Add(b);

    // Add b to a's list
    tree[b].Add(a);
}

// Modified Breadth-First Function
static void bfs(int node)
{

    // Create a queue of {child, parent}
    Queue<pair> qu = new Queue<pair>();

    // Push root node in the front of
    qu.Enqueue(new pair(node, 0 ));

    while (qu.Count != 0)
    {
        pair p = qu.Peek();

        // Dequeue a vertex from queue
        qu.Dequeue();
        ans[p.first] = p.second;
        vis[p.first] = true;

        // Get all adjacent vertices of the dequeued
        // vertex s. If any adjacent has not
        // been visited then enqueue it
        foreach (int child in tree[p.first])
        {
            if (!vis[child])
            {
                qu.Enqueue(new pair(child, p.first ));
            }
        }
    }
}

// Driver code
public static void Main(String[] args)
{

    // Number of vertices
    for (int i = 0; i < sz + 1; i++)
        tree[i] = new List<int>();

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(2, 4);
    addEdge(2, 5);

    // Calling modified bfs function
    bfs(0);

    int []q = { 2, 3 };

    for (int i = 0; i < 2; i++)
    {
        Console.WriteLine(ans[q[i]]);
    }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript implementation for the above approach

    let sz = 1e5;

    // Adjacency list representation
    // of the tree
    let tree = new Array(sz + 1);

    // Boolean array to mark all the
    // vertices which are visited
    let vis = new Array(sz + 1);
    vis.fill(false);

    // Array of vector where ith index
    // stores the path from the root
    // node to the ith node
    let ans = new Array(sz + 1);
    ans.fill(0);

    // Function to create an
    // edge between two vertices
    function addEdge(a, b)
    {

        // Add a to b's list
        tree[a].push(b);

        // Add b to a's list
        tree[b].push(a);
    }

    // Modified Breadth-First Function
    function bfs(node)
    {

        // Create a queue of {child, parent}
        let qu = [];

        // Push root node in the front of
        qu.push([node, 0 ]);

        while (qu.length > 0)
        {
            let p = qu[0];

            // Dequeue a vertex from queue
            qu.shift();
            ans[p[0]] = p[1];
            vis[p[0]] = true;

            // Get all adjacent vertices of the dequeued
            // vertex s. If any adjacent has not
            // been visited then enqueue it
            for (let child = 0; child < tree[p[0]].length; child++)
            {
                if (!vis[tree[p[0]][child]])
                {
                    qu.push([tree[p[0]][child], p[0]]);
                }
            }
        }
    }

    // Number of vertices
    let n = 6;
    for (let i = 0; i < sz + 1; i++)
        tree[i] = [];

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(2, 4);
    addEdge(2, 5);

    // Calling modified bfs function
    bfs(0);

    let q = [ 2, 3 ];

    for (let i = 0; i < 2; i++)
    {
        document.write(ans[q[i]] + "</br>");
    }

</script>
```

**Output:** 

```
0
1
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)