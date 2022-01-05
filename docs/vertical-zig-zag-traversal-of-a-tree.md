# 树的垂直之字形遍历

> 原文:[https://www . geesforgeks . org/vertical-zig-zag-遍历树/](https://www.geeksforgeeks.org/vertical-zig-zag-traversal-of-a-tree/)

给定一棵二叉树，任务是以垂直之字形遍历顺序打印元素。
**树的垂直之字形遍历**定义为:

1.  按照从右到左的顺序打印第一层的元素，如果没有剩余的元素，则跳到下一层。
2.  按照从左到右的顺序打印最后一级的元素，如果没有剩余的元素，则跳到上一级。
3.  当还有节点需要遍历时，重复上述步骤。

**示例:**

```
Input: 
     1
  /     \
 2       3
  \     /  \
  4    5    6
  /          \
 7            8
Output: 1, 7, 3, 8, 2, 4, 6, 5
Explanation: 
1\. First print elements of 1st level
   which will be printed as follows: 1

2\. Now remaining part of the tree is 
    *
  /    \
 2       3
  \     /  \
  4    5     6
  /           \
7              8

3\. Now move to 4th level print 
   from leftmost one element, 
   which will be: 7

4\. Now tree becomes:
     *
  /     \
 2       3
  \     /  \
  4    5    6
  /          \
  *           8

5\. Now move to since we move 
   from 2nd level since we move 
   from the lower level to higher-level 
   so start from rightmost, 
   so the element will be: 3

6\. Now tree becomes:
     *
  /     \
 2       *
  \     /  \
  4    5    6
  /          \
 *            8

7\. Now again move to 4th level 
   print from the leftmost remaining element, 
   which will be 8

8\. Now tree becomes:
     *  
  /     \
 2       *
  \     /  \
  4    5    6
  /          \
 *            *

9\. Now again move to 2nd level 
   print from the rightmost remaining element, 
   which will be 2 continue this way 
   until all elements are not traversed
```

**方法:**创建一个向量**树[]** ，其中**树【I】**将存储该树在第 **i** 级的所有节点。取两个指针 **p1** 指向第一级， **p2** 指向最后一级。现在，使用这两个指针以交替的方式开始打印节点(即从右向左为 **p1** ，从左向右为 **p2** )。如果在 **p1** 所指的层级中没有剩余节点，则移动到下一层级，如果在 **p2** 所指的层级中没有剩余节点，则移动到上一层级。

下面是上述方法的实现:

## C++

```
// C++ program to print Vertical
// Zig-Zag traversal of tree
#include <bits/stdc++.h>
using namespace std;

const int sz = 1e5;
int maxLevel = 0;

// Adjacency list representation
// of the tree
vector<int> tree[sz + 1];

// Boolean array to mark all the
// vertices which are visited
bool vis[sz + 1];

// Integer array to store the level
// of each node
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

// Utility Function to display the pattern
void display()
{
    bool flag = true;

    // Pointers for the first and the last levels
    int p1 = 0, p2 = maxLevel;

    // i points to the last node of level
    // p1 and j points to the first
    // node of the level p2
    int i = nodes[p1].size() - 1, j = 0;

    // While there are nodes left to traverse
    while (p1 <= p2) {

        // Print the nodes in an alternate fashion
        if (flag) {

            // Print the last unvisited node
            // of the level p1
            cout << nodes[p1][i] << " ";

            // Move to the previous node
            i--;

            // If there are no nodes left then
            // move to the next level
            if (i < 0) {
                p1++;
                i = nodes[p1].size() - 1;
            }
        }
        else {

            // Print the first unvisited node
            // of the level p2
            cout << nodes[p2][j] << " ";

            // Move to the next node
            j++;

            // If there are no nodes left then
            // move to the previous level
            if (j >= nodes[p2].size()) {
                p2--;
                j = 0;
            }
        }

        // Change the flag
        flag = !flag;

        // If all the nodes have been traversed
        if (p1 >= p2 && i < j) {
            break;
        }
    }
}

// Driver code
int main()
{

    // Number of vertices
    int n = 8;

    addEdge(1, 2);
    addEdge(1, 3);
    addEdge(2, 4);
    addEdge(3, 5);
    addEdge(3, 6);
    addEdge(4, 7);
    addEdge(6, 8);

    // Calling modified bfs function
    bfs(1);

    display();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print vertical
// Zig-Zag traversal of tree
import java.util.*;

@SuppressWarnings("unchecked")
class GFG{

static int sz = 100000;
static int maxLevel = 0;

// Adjacency list
// representation of the tree
static ArrayList []tree = new ArrayList[sz + 1];

// Boolean array to mark all the
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

// Modified Breadth-First Function
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

        vis[p.Key] = true;

        // Get all adjacent vertices of the
        // dequeued vertex s. If any adjacent
        // has not been visited then enqueue it
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
    boolean flag = true;

    // Pointers for the first and
    // the last levels
    int p1 = 0, p2 = maxLevel;

    // i points to the last node of level
    // p1 and j points to the first
    // node of the level p2
    int i = nodes[p1].size() - 1, j = 0;

    // While there are nodes left
    // to traverse
    while (p1 <= p2)
    {

        // Print the nodes in an
        // alternate fashion
        if (flag)
        {

            // Print the last unvisited node
            // of the level p1
            System.out.print((int)nodes[p1].get(i) + " ");

            // Move to the previous node
            i--;

            // If there are no nodes left then
            // move to the next level
            if (i < 0)
            {
                p1++;
                i = nodes[p1].size() - 1;
            }
        }
        else
        {

            // Print the first unvisited node
            // of the level p2
            System.out.print((nodes[p2]).get(j) + " ");

            // Move to the next node
            j++;

            // If there are no nodes left then
            // move to the previous level
            if (j >= nodes[p2].size())
            {
                p2--;
                j = 0;
            }
        }

        // Change the flag
        flag = !flag;

        // If all the nodes have been traversed
        if (p1 >= p2 && i < j)
        {
            break;
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
    addEdge(3, 5);
    addEdge(3, 6);
    addEdge(4, 7);
    addEdge(6, 8);

    // Calling modified bfs function
    bfs(1);

    display();
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python3 program to print Vertical
# Zig-Zag traversal of tree
from collections import deque

sz = int(1e5)
maxLevel = 0

# Adjacency list representation
# of the tree
tree = [[] for _ in range(sz + 1)]

# Boolean array to mark all the
# vertices which are visited
vis = [False for _ in range(sz + 1)]

# Integer array to store the level
# of each node
level = [0 for _ in range(sz + 1)]

# Array of vector where ith index
# stores all the nodes at level i
nodes = [[] for _ in range(sz + 1)]

# Utility function to create an
# edge between two vertices
def addEdge(a, b):

    # Add a to b's list
    tree[a].append(b)

    # Add b to a's list
    tree[b].append(a)

# Modified Breadth-First Function
def bfs(node):

    global maxLevel

    # Create a queue of child, parent
    qu = deque()

    # Push root node in the front of
    # the queue and mark as visited
    qu.append([node, 0])
    nodes[0].append(node)
    vis[node] = True
    level[1] = 0

    while qu:
        p = qu[0]

        # Dequeue a vertex from queue
        qu.popleft()
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

# Utility Function to display the pattern
def display():

    global maxLevel

    flag = True

    # Pointers for the first
    # and the last levels
    p1 = 0
    p2 = maxLevel

    # i points to the last node of level
    # p1 and j points to the first
    # node of the level p2
    i = len(nodes[p1]) - 1
    j = 0

    # While there are nodes left to traverse
    while (p1 <= p2):

        # Print the nodes in an alternate fashion
        if (flag):

            # Print the last unvisited node
            # of the level p1
            print(nodes[p1][i], end = " ")

            # Move to the previous node
            i -= 1

            # If there are no nodes left then
            # move to the next level
            if (i < 0):
                p1 += 1
                i = len(nodes[p1]) - 1
        else:

            # Print the first unvisited node
            # of the level p2
            print(nodes[p2][j], end = " ")

            # Move to the next node
            j += 1

            # If there are no nodes left then
            # move to the previous level
            if (j >= len(nodes[p2])):
                p2 -= 1
                j = 0

        # Change the flag
        flag = not flag

        # If all the nodes have been traversed
        if (p1 >= p2 and i < j):
            break

# Driver code
if __name__ == "__main__":

    # Number of vertices
    n = 8

    addEdge(1, 2)
    addEdge(1, 3)
    addEdge(2, 4)
    addEdge(3, 5)
    addEdge(3, 6)
    addEdge(4, 7)
    addEdge(6, 8)

    # Calling modified bfs function
    bfs(1)

    display()

# This code is contributed by sanjeev2552
```

## C#

```
// C# program to print vertical
// Zig-Zag traversal of tree
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
                maxLevel = Math.Max(maxLevel,
                                    level[child]);
                nodes[level[child]].Add(child);
            }
        }
    }
}

// Function to display
// the pattern
static void display()
{
   bool flag = true;

    // Pointers for the first and
    // the last levels
    int p1 = 0, p2 = maxLevel;

    // i points to the last node of level
    // p1 and j points to the first
    // node of the level p2
    int i = nodes[p1].Count - 1, j = 0;

    // While there are nodes left
    // to traverse
    while (p1 <= p2)
    {

        // Print the nodes in an
        // alternate fashion
        if (flag)
        {

            // Print the last unvisited node
            // of the level p1
            Console.Write((int)nodes[p1][i] + " ");

            // Move to the previous node
            i--;

            // If there are no nodes left then
            // move to the next level
            if (i < 0)
            {
                p1++;
                i = nodes[p1].Count - 1;
            }
        }
        else
        {

            // Print the first unvisited node
            // of the level p2
            Console.Write((int)nodes[p2][j] + " ");

            // Move to the next node
            j++;

            // If there are no nodes left then
            // move to the previous level
            if (j >= nodes[p2].Count)
            {
                p2--;
                j = 0;
            }
        }

        // Change the flag
        flag = !flag;

        // If all the nodes have been traversed
        if (p1 >= p2 && i < j)
        {
            break;
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
    addEdge(3, 5);
    addEdge(3, 6);
    addEdge(4, 7);
    addEdge(6, 8);

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

// JavaScript program to print vertical
// Zig-Zag traversal of tree

var sz = 100000;
var maxLevel = 0;

// Adjacency list
// representation of the tree
var tree = Array.from(Array(sz + 1), ()=>Array());

// Boolean array to mark all the
// vertices which are visited
var vis = Array(sz + 1).fill(false);

// Integer array to store
// the level of each node
var level = Array(sz + 1).fill(0);

// Array of vector where ith index
// stores all the nodes at level i
var nodes = Array.from(Array(sz + 1), ()=>Array());

// Utility function to create an
// edge between two vertices
function addEdge(a, b)
{

    // push a to b's list
    tree[a].push(b);

    // push b to a's list
    tree[b].push(a);
}

// Modified Breadth-First Function
function bfs(node)
{

    // Create a queue of {child, parent}
    var qu = [];

    // Push root node in the front of
    // the queue and mark as visited
    qu.push([node, 0]);
    nodes[0].push(node);
    vis[node] = true;
    level[1] = 0;

    while(qu.length != 0)
    {
        var p = qu[0];

        // shift a vertex from queue
        qu.shift();
        vis[p[0]] = true;

        // Get all adjacent vertices of the dequeued
        // vertex s. If any adjacent has not
        // been visited then enqueue it
        for(var child of tree[p[0]])
        {
            if (!vis[child])
            {
                qu.push([child, p[0]]);
                level[child] = level[p[0]] + 1;
                maxLevel = Math.max(maxLevel,
                                    level[child]);
                nodes[level[child]].push(child);
            }
        }
    }
}

// Function to display
// the pattern
function display()
{
   var flag = true;

    // Pointers for the first and
    // the last levels
    var p1 = 0, p2 = maxLevel;

    // i points to the last node of level
    // p1 and j points to the first
    // node of the level p2
    var i = nodes[p1].length - 1, j = 0;

    // While there are nodes left
    // to traverse
    while (p1 <= p2)
    {

        // Print the nodes in an
        // alternate fashion
        if (flag)
        {

            // Print the last unvisited node
            // of the level p1
            document.write(nodes[p1][i] + " ");

            // Move to the previous node
            i--;

            // If there are no nodes left then
            // move to the next level
            if (i < 0)
            {
                p1++;
                i = nodes[p1].length - 1;
            }
        }
        else
        {

            // Print the first unvisited node
            // of the level p2
            document.write(nodes[p2][j] + " ");

            // Move to the next node
            j++;

            // If there are no nodes left then
            // move to the previous level
            if (j >= nodes[p2].length)
            {
                p2--;
                j = 0;
            }
        }

        // Change the flag
        flag = !flag;

        // If all the nodes have been traversed
        if (p1 >= p2 && i < j)
        {
            break;
        }
    }
}

// Driver code
for(var i = 0; i < sz + 1; i++)
{
    tree[i] = Array();
    nodes[i] = Array();
    vis[i] = false;
    level[i] = 0;
}
addEdge(1, 2);
addEdge(1, 3);
addEdge(2, 4);
addEdge(3, 5);
addEdge(3, 6);
addEdge(4, 7);
addEdge(6, 8);

// Calling modified bfs function
bfs(1);

display();

</script>
```

**Output:** 

```
1 7 3 8 2 4 6 5
```

**时间复杂度:** O(n)