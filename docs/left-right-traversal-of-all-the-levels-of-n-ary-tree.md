# 二叉树所有层次的左右遍历

> 原文:[https://www . geeksforgeeks . org/n 元树的左右遍历/](https://www.geeksforgeeks.org/left-right-traversal-of-all-the-levels-of-n-ary-tree/)

给定以节点 1 为根的二叉树，任务是按照以下定义的顺序打印元素。

1.  首先，以另一种方式打印最后一级的所有元素，例如首先打印最左边的元素，然后打印最右边的元素&继续这样，直到最后一级遍历完所有元素。
2.  现在对其余的级别做同样的操作。

**示例:**

```
Input:
            1
          /   \
        2      3
      /   \   /
     4     5 6
Output: 4 6 5 2 3 1
Explanation:
First print all elements of the last 
level which will be printed as follows: 4 6 5
Now tree becomes
       1
     /   \
    2     3

Now print elements as 2 3
Now the tree becomes: 1

Input:
        1
      /   \
     2     3
Output: 2 3 1
```

**接近**:

*   进行 bfs 调用，并将 I 级的所有节点存储在一个向量数组中。
*   还要记录 bfs 呼叫中达到的最高级别。
*   现在从最大级别到 0 打印所需的图案

下面是上述方法的实现:

## C++

```
// C++ implementation
// for the above approach
#include <bits/stdc++.h>
using namespace std;

const int sz = 1e5;
int maxLevel = 0;

// Adjacency list
// representation of the tree
vector<int> tree[sz + 1];

// Boolean array to mark all the
// vertices which are visited
bool vis[sz + 1];

// Integer array to store
// the level of each node
int level[sz + 1];

// Array of vector where ith index
// stores all the nodes at level i
vector<int> nodes[sz + 1];

// Utility function to create an
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
  // the queue and mark as visited
  qu.push({ node, 0 });
  nodes[0].push_back(node);
  vis[node] = true;
  level[1] = 0;

  while (!qu.empty()) {

    pair<int, int> p = qu.front();
    // Dequeue a vertex from queue
    qu.pop();
    vis[p.first] = true;

    // Get all adjacent vertices of the dequeued
    // vertex s. If any adjacent has not
    // been visited then enqueue it
    for (int child : tree[p.first]) {
        if (!vis[child]) {
            qu.push({ child, p.first });
            level[child] = level[p.first] + 1;
            maxLevel = max(maxLevel, level[child]);
            nodes[level[child]].push_back(child);
        }
    }
  }
}

// Function to display
// the pattern
void display()
{
  for (int i = maxLevel; i >= 0; i--) {
    int len = nodes[i].size();
    // Printing all nodes
    // at given level
    for (int j = 0; j < len / 2; j++) {
        cout << nodes[i][j] << " " << nodes[i][len - 1 - j] << " ";
    }
    // If count of nodes
    // at level i is odd
    // print remaining node
    if (len % 2 == 1) {
        cout << nodes[i][len / 2] << " ";
    }
  }
}

// Driver code
int main()
{
  // Number of vertices
  int n = 6;

  addEdge(1, 2);
  addEdge(1, 3);
  addEdge(2, 4);
  addEdge(2, 5);
  addEdge(3, 6);

  // Calling modified bfs function
  bfs(1);

  display();

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// for the above approach
import java.util.*;

@SuppressWarnings("unchecked")

class GFG{

static int sz = 100000;
static int maxLevel = 0;

// Adjacency list
// representation of the tree
static ArrayList []tree = new ArrayList[sz + 1];

// boolean array to mark all the
// vertices which are visited
static boolean []vis = new boolean[sz + 1];

// Integer array to store
// the level of each node
static int []level = new int[sz + 1];

// Array of vector where ith index
// stores all the nodes at level i
static ArrayList []nodes = new ArrayList[sz + 1];

// Utility function to create an
// edge between two vertices
static void addEdge(int a, int b)
{

    // Add a to b's list
    tree[a].add(b);

    // Add b to a's list
    tree[b].add(a);
}

static class Pair
{
    int Key, Value;
    Pair(int Key, int Value)
    {
        this.Key = Key;
        this.Value = Value;
    }
}

// Modified Breadth-Key Function
static void bfs(int node)
{

    // Create a queue of {child, parent}
    Queue<Pair> qu = new LinkedList<>();

    // Push root node in the front of
    // the queue and mark as visited
    qu.add(new Pair(node, 0));
    nodes[0].add(node);
    vis[node] = true;
    level[1] = 0;

    while (qu.size() != 0)
    {
        Pair p = qu.poll();

        // Dequeue a vertex from queue
        vis[p.Key] = true;

        // Get all adjacent vertices of the dequeued
        // vertex s. If any adjacent has not
        // been visited then put it
        for(int child : (ArrayList<Integer>)tree[p.Key])
        {
            if (!vis[child])
            {
                qu.add(new Pair(child, p.Key));
                level[child] = level[p.Key] + 1;
                maxLevel = Math.max(maxLevel,
                                    level[child]);
                nodes[level[child]].add(child);
            }
        }
    }
}

// Function to display
// the pattern
static void display()
{
    for(int i = maxLevel; i >= 0; i--)
    {
        int len = nodes[i].size();

        // Printing all nodes
        // at given level
        for(int j = 0; j < len / 2; j++)
        {
            System.out.print((int)nodes[i].get(j) + " " +
                             (int)nodes[i].get(len - 1 - j) +
                             " ");
        }

        // If count of nodes
        // at level i is odd
        // print remaining node
        if (len % 2 == 1)
        {
            System.out.print(
                (int)nodes[i].get(len / 2) + " ");
        }
    }
}

// Driver code
public static void main(String[] args)
{
    for(int i = 0; i < sz + 1; i++)
    {
        tree[i] = new ArrayList();
        nodes[i] = new ArrayList();
        vis[i] = false;
        level[i] = 0;
    }

    addEdge(1, 2);
    addEdge(1, 3);
    addEdge(2, 4);
    addEdge(2, 5);
    addEdge(3, 6);

    // Calling modified bfs function
    bfs(1);

    display();
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python3 implementation
# for the above approach
from collections import deque

sz = 10 ** 5
maxLevel = 0

# Adjacency list
# representation of the tree
tree = [[] for i in range(sz + 1)]

# Boolean array to mark all the
# vertices which are visited
vis = [False] * (sz + 1)

# Integer array to store
# the level of each node
level = [0] * (sz + 1)

# Array of vector where ith index
# stores all the nodes at level i
nodes = [[] for i in range(sz + 1)]

# Utility function to create an
# edge between two vertices
def addEdge(a, b):

    global tree

    # Add a to b's list
    tree[a].append(b)

    # Add b to a's list
    tree[b].append(a)

# Modified Breadth-First Function
def bfs(node):

    global maxLevel

    # Create a queue of {child, parent}
    qu =  deque()

    # Push root node in the front of
    # the queue and mark as visited
    qu.append([node, 0 ])

    nodes[0].append(node)
    vis[node] = True
    level[1] = 0

    while (len(qu) > 0):

        p = qu.popleft()

        # Dequeue a vertex from queue
        # qu.pop()
        vis[p[0]] = True

        # Get all adjacent vertices of the dequeued
        # vertex s. If any adjacent has not
        # been visited then enqueue it
        for child in tree[p[0]]:
            if (not vis[child]):
                qu.append([child, p[0]])
                level[child] = level[p[0]] + 1
                maxLevel = max(maxLevel, level[child])
                nodes[level[child]].append(child)

# Function to display
# the pattern
def display():

    for i in range(maxLevel, -1, -1):
        lenn = len(nodes[i])

        # Printing all nodes
        # at given level
        for j in range(lenn // 2):
            print(nodes[i][j],
                  nodes[i][lenn - 1 - j], end = " ")

        # If count of nodes
        # at level i is odd
        # prremaining node
        if (lenn % 2 == 1):
            print(nodes[i][lenn // 2], end = " ")

# Driver code
if __name__ == '__main__':

    # Number of vertices
    n = 6

    addEdge(1, 2)
    addEdge(1, 3)
    addEdge(2, 4)
    addEdge(2, 5)
    addEdge(3, 6)

    # Calling modified bfs function
    bfs(1)

    display()

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation
// for the above approach
using System;
using System.Collections.Generic;
using System.Collections;

class GFG{

static int sz = 100000;
static int maxLevel = 0;

// Adjacency list
// representation of the tree
static ArrayList []tree = new ArrayList[sz + 1];

// Boolean array to mark all the
// vertices which are visited
static bool []vis = new bool[sz + 1];

// Integer array to store
// the level of each node
static int []level = new int[sz + 1];

// Array of vector where ith index
// stores all the nodes at level i
static ArrayList []nodes = new ArrayList[sz + 1];

// Utility function to create an
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
    Queue qu = new Queue();

    // Push root node in the front of
    // the queue and mark as visited
    qu.Enqueue(new KeyValuePair<int, int>(node, 0));
    nodes[0].Add(node);
    vis[node] = true;
    level[1] = 0;

    while(qu.Count != 0)
    {

        KeyValuePair<int,
                     int> p = (KeyValuePair<int,
                                            int>)qu.Peek();

        // Dequeue a vertex from queue
        qu.Dequeue();
        vis[p.Key] = true;

        // Get all adjacent vertices of the dequeued
        // vertex s. If any adjacent has not
        // been visited then enqueue it
        foreach(int child in tree[p.Key])
        {
            if (!vis[child])
            {
                qu.Enqueue(new KeyValuePair<int, int>(
                           child, p.Key));
                level[child] = level[p.Key] + 1;
                maxLevel = Math.Max(maxLevel, level[child]);
                nodes[level[child]].Add(child);
            }
        }
    }
}

// Function to display
// the pattern
static void display()
{

    for(int i = maxLevel; i >= 0; i--)
    {
        int len = nodes[i].Count;

        // Printing all nodes
        // at given level
        for(int j = 0; j < len / 2; j++)
        {
            Console.Write((int)nodes[i][j] + " " +
                          (int)nodes[i][len - 1 - j] +
                           " ");
        }

        // If count of nodes
        // at level i is odd
        // print remaining node
        if (len % 2 == 1)
        {
            Console.Write((int)nodes[i][len / 2] + " ");
        }
    }
}

// Driver code
public static void Main(string[] args)
{
    for(int i = 0; i < sz + 1; i++)
    {
        tree[i] = new ArrayList();
        nodes[i] = new ArrayList();
        vis[i] = false;
        level[i] = 0;
    }

    addEdge(1, 2);
    addEdge(1, 3);
    addEdge(2, 4);
    addEdge(2, 5);
    addEdge(3, 6);

    // Calling modified bfs function
    bfs(1);

    display();
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// JavaScript implementation
// for the above approach

let sz = 100000;
let maxLevel = 0;

// Adjacency list
// representation of the tree
let tree = new Array(sz + 1);

// boolean array to mark all the
// vertices which are visited
let vis = new Array(sz + 1);

// Integer array to store
// the level of each node
let level = new Array(sz + 1);

// Array of vector where ith index
// stores all the nodes at level i
let nodes = new Array(sz + 1);

// Utility function to create an
// edge between two vertices
function addEdge(a,b)
{
    // Add a to b's list
    tree[a].push(b);

    // Add b to a's list
    tree[b].push(a);
}

// Modified Breadth-Key Function
function bfs(node)
{
    let qu=[];
    // Push root node in the front of
    // the queue and mark as visited
    qu.push([node, 0]);
    nodes[0].push(node);
    vis[node] = true;
    level[1] = 0;

    while (qu.length != 0)
    {
        let p = qu.shift();

        // Dequeue a vertex from queue
        vis[p[0]] = true;

        // Get all adjacent vertices of the dequeued
        // vertex s. If any adjacent has not
        // been visited then put it
        for(let child=0;child<tree[p[0]].length;child++)
        {
            if (!vis[tree[p[0]][child]])
            {

                qu.push([tree[p[0]][child], p[0]]);
                level[tree[p[0]][child]] = level[p[0]] + 1;
                maxLevel = Math.max(maxLevel,
                                    level[tree[p[0]][child]]);

                nodes[level[tree[p[0]][child]]].
                push(tree[p[0]][child]);

            }
        }
    }
}

// Function to display
// the pattern
function display()
{

    for(let i = maxLevel; i >= 0; i--)
    {
        let len = nodes[i].length;  
        // Printing all nodes
        // at given level
        for(let j = 0; j < Math.floor(len / 2); j++)
        {
            document.write(nodes[i][j] + " " +
                             nodes[i][len - 1 - j] +
                             " ");
        }

        // If count of nodes
        // at level i is odd
        // print remaining node
        if (len % 2 == 1)
        {
            document.write(
                nodes[i][Math.floor(len / 2)] + " ");
        }
    }
}

// Driver code
for(let i = 0; i < sz + 1; i++)
    {
        tree[i] = [];
        nodes[i] = [];
        vis[i] = false;
        level[i] = 0;
    }

    addEdge(1, 2);
    addEdge(1, 3);
    addEdge(2, 4);
    addEdge(2, 5);
    addEdge(3, 6);

    // Calling modified bfs function
    bfs(1);

    display();

// This code is contributed by patel2127

</script>
```

**Output:** 

```
4 6 5 2 3 1
```

**时间复杂度** : O(V + E)，其中 V 为顶点总数，E 为边总数。
**辅助空间** : O(V)。