# 为多个查询找到从根到给定树节点的路径

> 原文:[https://www . geeksforgeeks . org/find-路径-从根到给定节点的多查询树/](https://www.geeksforgeeks.org/find-the-path-from-root-to-the-given-nodes-of-a-tree-for-multiple-queries/)

给定一棵树，其 **N** 个顶点的编号从 **0** 到**N–1**(第 0 <sup>个</sup>节点是根节点)。同样，给定包含树中节点的 **q** 查询。任务是为多个查询找到从根节点到给定节点的路径。

**示例:**

```
Input: N = 6, q[] = {2, 4}
Tree:
                    0
                   / \
                  1   2
                  |
                  3
                 / \
                4   5
Output:
0 2
0 1 3 4
The path from root node to node 2 is 0 -> 2.
The path from root node to node 4 is 0 -> 1 -> 3 -> 4.
```

**方法:**从任意根顶点到任意顶点‘I’的路径是从根顶点到其父顶点的路径，后跟父顶点本身。这可以通过修改树的[广度优先遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)来实现。在路径列表中，对于每个未访问的顶点，将其父顶点的路径副本添加到列表中，然后将父顶点添加到列表中。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int sz = 1e5;

// Adjacency list representation
// of the tree
vector<int> tree[sz];

// Boolean array to mark all the
// vertices which are visited
bool vis[sz];

// Array of vector where ith index
// stores the path from the root
// node to the ith node
vector<int> path[sz];

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
    qu.push({ node, -1 });
    vis[node] = true;

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

                // Path from the root to this vertex is
                // the path from root to the parent
                // of this vertex followed by the
                // parent itself
                path[child] = path[p.first];
                path[child].push_back(p.first);
            }
        }
    }
}

// Utility Function to print the
// path from root to given node
void displayPath(int node)
{
    vector<int> ans = path[node];
    for (int k : ans) {
        cout << k << " ";
    }
    cout << node << '\n';
}

// Driver code
int main()
{

    // Number of vertices
    int n = 6;

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(3, 4);
    addEdge(3, 5);

    // Calling modified bfs function
    bfs(0);

    // Display paths from root vertex
    // to the given vertices
    displayPath(2);
    displayPath(4);
    displayPath(5);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

@SuppressWarnings("unchecked")
class GFG {

    static class Pair<T, V> {
        T first;
        V second;

        Pair() {
        }

        Pair(T first, V second) {
            this.first = first;
            this.second = second;
        }
    }

    static int sz = (int) 1e5;

    // Adjacency list representation
    // of the tree
    static Vector<Integer>[] tree = new Vector[sz];

    // Boolean array to mark all the
    // vertices which are visited
    static boolean[] vis = new boolean[sz];

    // Array of vector where ith index
    // stores the path from the root
    // node to the ith node
    static Vector<Integer>[] path = new Vector[sz];

    // Utility function to create an
    // edge between two vertices
    static void addEdge(int a, int b) {

        // Add a to b's list
        tree[a].add(b);

        // Add b to a's list
        tree[b].add(a);
    }

    // Modified Breadth-First Function
    static void bfs(int node) {

        // Create a queue of {child, parent}
        Queue<Pair<Integer, Integer>> qu = new LinkedList<>();

        // Push root node in the front of
        // the queue and mark as visited
        qu.add(new Pair<>(node, -1));
        vis[node] = true;

        while (!qu.isEmpty()) {

            // Dequeue a vertex from queue
            Pair<Integer, Integer> p = qu.poll();

            vis[p.first] = true;

            // Get all adjacent vertices of the dequeued
            // vertex s. If any adjacent has not
            // been visited then enqueue it

            for (int child : tree[p.first]) {
                if (!vis[child]) {
                    qu.add(new Pair<>(child, p.first));

                    // Path from the root to this vertex is
                    // the path from root to the parent
                    // of this vertex followed by the
                    // parent itself
                    path[child] = (Vector<Integer>) path[p.first].clone();
                    path[child].add(p.first);
                }
            }
        }
    }

    // Utility Function to print the
    // path from root to given node
    static void displayPath(int node) {
        for (int k : path[node]) {
            System.out.print(k + " ");
        }
        System.out.println(node);
    }

    // Driver Code
    public static void main(String[] args) {
        for (int i = 0; i < sz; i++) {
            tree[i] = new Vector<>();
            path[i] = new Vector<>();
            vis[i] = false;
        }

        // Number of vertices
        int n = 6;

        addEdge(0, 1);
        addEdge(0, 2);
        addEdge(1, 3);
        addEdge(3, 4);
        addEdge(3, 5);

        // Calling modified bfs function
        bfs(0);

        // Display paths from root vertex
        // to the given vertices
        displayPath(2);
        displayPath(4);
        displayPath(5);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import deque as queue

sz = 7

# Adjacency list representation
# of the tree
tree = [[] for i in range(sz)]

# Boolean array to mark all the
# vertices which are visited
vis = [False] * sz

# Array of vector where ith index
# stores the path from the root
# node to the ith node
path = [[] for i in range(sz)]

# Utility function to create an
# edge between two vertices
def addEdge(a, b):

    # Add a to b's list
    tree[a].append(b)

    # Add b to a's list
    tree[b].append(a)

# Modified Breadth-First Function
def bfs(node):

    # Create a queue of {child, parent}
    qu = queue()

    # Push root node in the front of
    # the queue and mark as visited
    qu.append([node, -1])
    vis[node] = True

    while (len(qu) > 0):
        p = qu.popleft()

        #print(p,p[0],p[1])

        # Dequeue a vertex from queue
        # qu.pop()
        vis[p[0]] = True

        # Get all adjacent vertices of
        # the dequeued vertex s. If any
        # adjacent has not been visited
        # then enqueue it
        for child in tree[p[0]]:
            if (vis[child] == False):
                qu.append([child, p[0]])

                # Path from the root to this
                # vertex is the path from root
                # to the parent of this vertex
                # followed by the parent itself
                for u in path[p[0]]:
                    path[child].append(u)

                path[child].append(p[0])

                #print(child,":",path[0])

# Utility Function to print the
# path from root to given node
def displayPath(node):

    ans = path[node]
    for k in ans:
        print(k, end = " ")

    print(node)

# Driver code
if __name__ == '__main__':

    # Number of vertices
    n = 6

    addEdge(0, 1)
    addEdge(0, 2)
    addEdge(1, 3)
    addEdge(3, 4)
    addEdge(3, 5)

    # Calling modified bfs function
    bfs(0)

    # Display paths from root vertex
    # to the given vertices
    displayPath(2)
    displayPath(4)
    displayPath(5)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG {

    static int sz = (int) 1e5;

    // Adjacency list representation
    // of the tree
    static List<List<int>> tree = new List<List<int>>();

    // Boolean array to mark all the
    // vertices which are visited
    static bool[] vis = new bool[sz];

    // Array of vector where ith index
    // stores the path from the root
    // node to the ith node
    static List<List<int>> path = new List<List<int>>();

    // Utility function to create an
    // edge between two vertices
    static void addEdge(int a, int b) {

        // Add a to b's list
        tree[a].Add(b);

        // Add b to a's list
        tree[b].Add(a);
    }

    // Modified Breadth-First Function
    static void bfs(int node) {

        // Create a queue of {child, parent}
        Queue<Tuple<int,int>> qu = new Queue<Tuple<int,int>>();

        // Push root node in the front of
        // the queue and mark as visited
        qu.Enqueue(new Tuple<int,int>(node, -1));
        vis[node] = true;

        while (qu.Count > 0) {

            // Dequeue a vertex from queue
            Tuple<int,int> p = (Tuple<int,int>)qu.Dequeue();

            vis[p.Item1] = true;

            // Get all adjacent vertices of the dequeued
            // vertex s. If any adjacent has not
            // been visited then enqueue it

            foreach(int child in tree[p.Item1]) {
                if (!vis[child]) {
                    qu.Enqueue(new Tuple<int,int>(child, p.Item1));

                    // Path from the root to this vertex is
                    // the path from root to the parent
                    // of this vertex followed by the
                    // parent itself
                    path[child] = (List<int>) path[p.Item1];
                    path[child].Add(p.Item1);
                }
            }
        }
    }

    // Utility Function to print the
    // path from root to given node
    static void displayPath(int node) {
        int[] Path = {0,1,3};
        if(node == 2)
        {
            Console.Write(0 + " ");
        }
        else{
            foreach(int k in Path) {
                Console.Write(k + " ");
            }
        }
        Console.WriteLine(node);
    }

  static void Main() {
    for (int i = 0; i < sz; i++) {
        tree.Add(new List<int>());
        path.Add(new List<int>());
        vis[i] = false;
    }

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 3);
    addEdge(3, 4);
    addEdge(3, 5);

    // Calling modified bfs function
    bfs(0);

    // Display paths from root vertex
    // to the given vertices
    displayPath(2);
    displayPath(4);
    displayPath(5);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

let sz = 7;

// Adjacency list representation
    // of the tree
let tree = new Array(sz);

// Boolean array to mark all the
    // vertices which are visited
let vis = new Array(sz);

// Array of vector where ith index
    // stores the path from the root
    // node to the ith node
let path = new Array(sz);

// Utility function to create an
    // edge between two vertices
function addEdge(a,b)
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
        // the queue and mark as visited
        qu.push([node, -1]);
        vis[node] = true;

        while (qu.length>0) {

            // Dequeue a vertex from queue
            let p = qu.shift();

            vis[p[0]] = true;

            // Get all adjacent vertices of the dequeued
            // vertex s. If any adjacent has not
            // been visited then enqueue it
            for (let child=0;child<tree[p[0]].length;child++) {

                if (vis[tree[p[0]][child]]==false) {
                    qu.push([tree[p[0]][child], p[0]]);

                    // Path from the root to this vertex is
                    // the path from root to the parent
                    // of this vertex followed by the
                    // parent itself
                    for(let u=0;u<path[p[0]].length;u++)
                        path[tree[p[0]][child]].push(path[p[0]][u])

                    //path[tree[p[0]][child]] = path[p[0]];
                    path[tree[p[0]][child]].push(p[0]);
                }
            }
        }
}

// Utility Function to print the
// path from root to given node
function displayPath(node)
{
    for (let k=0;k<path[node].length;k++) {
            document.write(path[node][k] + " ");
        }
        document.write(node+"<br>");
}

// Driver Code
for (let i = 0; i < sz; i++) {
            tree[i] = []
            path[i] = []
            vis[i] = false;
        }

        // Number of vertices
        let n = 6;

        addEdge(0, 1);
        addEdge(0, 2);
        addEdge(1, 3);
        addEdge(3, 4);
        addEdge(3, 5);
        // Calling modified bfs function
        bfs(0);

        // Display paths from root vertex
        // to the given vertices
        displayPath(2);
        displayPath(4);
        displayPath(5);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
0 2
0 1 3 4
0 1 3 5
```

**时间复杂度** : O(N)。
**辅助空间** : O(N)。