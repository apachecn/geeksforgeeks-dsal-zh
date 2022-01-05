# 为二叉树的每个节点计算具有较小值的祖先

> 原文:[https://www . geeksforgeeks . org/count-祖先-二叉树的每个节点具有较小的值/](https://www.geeksforgeeks.org/count-ancestors-with-smaller-value-for-each-node-of-a-binary-tree/)

给定一个由 **N** 节点组成的[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，值从 **1** 到 **N** ，根在节点 **1** ，每个节点的任务是计算值小于当前节点的[祖先](https://www.geeksforgeeks.org/print-ancestors-of-a-given-node-in-binary-tree/)的数量。

**示例:**

> **输入:**下面是给定的树:
> **1
> /\
> 4 5
> /\
> 6 3 2
> **输出:** 0 1 1 1 1 2
> **说明:**
> 由于节点 1 是根节点，所以没有祖先。
> 节点 2 的祖先:{1，5}。值小于 2 的祖先数为 1。
> 节点 3 的祖先:{1，5}。值小于 3 的祖先数为 1。
> 节点 4 的祖先:{1}。值小于 4 的祖先数为 1。
> 节点 5 的祖先:{1}。值小于 5 的祖先数为 1。
> 节点 6 的祖先:{1，4}。值小于 6 的祖先数为 2。**
> 
> ****输入:**下面是给定的树:
> **1
> /\
> 3 2
> \
> 4
> **输出:** 0 1 1 2
> **说明:**
> 节点 1 没有祖先。
> 节点 2 的祖先:{1}。值小于 2 的祖先数为 1。
> 节点 3 的祖先:{1}。值小于 3 的祖先数为 1。
> 节点 4 的祖先:{1，2}。值小于 4 的祖先数为 2。****

******方法:**想法是从树的根节点执行 [DFS 遍历，并将每个节点的直接父节点存储在一个数组中。然后迭代每个节点，并使用父数组，将其值与其所有祖先进行比较。最后，打印结果。
按照以下步骤解决问题:](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)****

*   ****初始化一个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如说 **par[]** 大小 **N** ，用 **-1** 来存储每个节点的直接父节点。****
*   ****从根节点开始执行 [DFS 遍历，并执行以下步骤:](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)

    *   更新当前节点的父节点。
    *   递归调用当前节点的子节点。**** 
*   ****现在，[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，并执行以下步骤:

    *   将当前节点存储在一个变量中，比如**节点**。
    *   [迭代而](https://www.geeksforgeeks.org/loops-in-c-and-cpp/) **par【节点】**不等于 **-1** :
        *   如果 **par【节点】**小于 **i** ，那么将 **cnt** 增加 **1** 。
        *   将**节点**更新为 **par【节点】**。
    *   完成上述步骤后，打印 **cnt** 的值作为当前节点的值。**** 

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to add an edge
// between nodes u and v
void add_edge(vector<int> adj[],
              int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Function to perform the DFS Traversal
// and store parent of each node
void dfs(vector<int>& parent,
         vector<int> adj[],
         int u,
         int par = -1)
{
    // Store the immediate parent
    parent[u] = par;

    // Traverse the children of
    // the current node
    for (auto child : adj[u]) {

        // Recursively call for
        // function dfs for the
        // child node
        if (child != par)
            dfs(parent, adj, child, u);
    }
}

// Function to count the number of
// ancestors with values smaller
// than that of the current node
void countSmallerAncestors(
    vector<int> adj[], int n)
{
    // Stores the parent of each node
    vector<int> parent(int(1e5), 0);

    // Perform the DFS Traversal
    dfs(parent, adj, 1);

    // Traverse all the nodes
    for (int i = 1; i <= n; i++) {

        int node = i;

        // Store the number of ancestors
        // smaller than node
        int cnt = 0;

        // Loop until parent[node] != -1
        while (parent[node] != -1) {

            // If the condition satisfies,
            // increment cnt by 1
            if (parent[node] < i)
                cnt += 1;

            node = parent[node];
        }

        // Print the required result
        // for the current node
        cout << cnt << " ";
    }
}

// Driver Code
int main()
{
    int N = 6;
    vector<int> adj[int(1e5)];

    // Tree Formation
    add_edge(adj, 1, 5);
    add_edge(adj, 1, 4);
    add_edge(adj, 4, 6);
    add_edge(adj, 5, 3);
    add_edge(adj, 5, 2);

    countSmallerAncestors(adj, N);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to add an edge
// between nodes u and v
static void add_edge(ArrayList<ArrayList<Integer>> adj,
                     int u, int v)
{
    adj.get(u).add(v);
    adj.get(v).add(u);
}

// Function to perform the DFS Traversal
// and store parent of each node
static void dfs(ArrayList<Integer> parent,
                ArrayList<ArrayList<Integer>> adj,
                int u, int par)
{

    // Store the immediate parent
    parent.set(u,par);

    // Traverse the children of
    // the current node
    for(int child : adj.get(u))
    {

        // Recursively call for
        // function dfs for the
        // child node
        if (child != par)
            dfs(parent, adj, child, u);
    }
}

// Function to count the number of
// ancestors with values smaller
// than that of the current node
static void countSmallerAncestors(
    ArrayList<ArrayList<Integer>> adj, int n)
{

    // Stores the parent of each node
    ArrayList<Integer> parent = new ArrayList<Integer>();
    for(int i = 0; i < (int)(1e5); i++)
    {
        parent.add(0);
    }

    // Perform the DFS Traversal
    dfs(parent, adj, 1, -1);

    // Traverse all the nodes
    for(int i = 1; i <= n; i++)
    {
        int node = i;

        // Store the number of ancestors
        // smaller than node
        int cnt = 0;

        // Loop until parent[node] != -1
        while (parent.get(node) != -1)
        {

            // If the condition satisfies,
            // increment cnt by 1
            if (parent.get(node) < i)
                cnt += 1;

            node = parent.get(node);
        }

        // Print the required result
        // for the current node
        System.out.print(cnt + " ");
    }
}

// Driver code
public static void main (String[] args)
{
    int N = 6;
    ArrayList<ArrayList<Integer>> adj = new ArrayList<ArrayList<Integer>>();
    for(int i = 0; i < (int)(1e5); i++)
    {
        adj.add(new ArrayList<Integer>());
    }

    // Tree Formation
    add_edge(adj, 1, 5);
    add_edge(adj, 1, 4);
    add_edge(adj, 4, 6);
    add_edge(adj, 5, 3);
    add_edge(adj, 5, 2);

    countSmallerAncestors(adj, N);
}
}

// This code is contributed by avanitrachhadiya2155**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# Function to add an edge
# between nodes u and v
def add_edge(u, v):

    global adj
    adj[u].append(v)
    adj[v].append(u)

# Function to perform the DFS Traversal
# and store parent of each node
def dfs(u, par = -1):

    global adj, parent

    # Store the immediate parent
    parent[u] = par

    # Traverse the children of
    # the current node
    for child in adj[u]:

        # Recursively call for
        # function dfs for the
        # child node
        if (child != par):
            dfs(child, u)

# Function to count the number of
# ancestors with values smaller
# than that of the current node
def countSmallerAncestors(n):

    global parent, adj

    # Stores the parent of each node

    # Perform the DFS Traversal
    dfs(1)

    # Traverse all the nodes
    for i in range(1, n + 1):
        node = i

        # Store the number of ancestors
        # smaller than node
        cnt = 0

        # Loop until parent[node] != -1
        while (parent[node] != -1):

            # If the condition satisfies,
            # increment cnt by 1
            if (parent[node] < i):
                cnt += 1

            node = parent[node]

        # Print the required result
        # for the current node
        print(cnt, end = " ")

# Driver Code
if __name__ == '__main__':

    N = 6
    adj = [[] for i in range(10**5)]
    parent = [0] * (10**5)

    # Tree Formation
    add_edge(1, 5)
    add_edge(1, 4)
    add_edge(4, 6)
    add_edge(5, 3)
    add_edge(5, 2)

    countSmallerAncestors(N)

# This code is contributed by mohit kumar 29**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to add an edge
    // between nodes u and v
    static void add_edge(List<List<int>> adj, int u, int v)
    {
        adj[u].Add(v);
        adj[v].Add(u);
    }

    // Function to perform the DFS Traversal
    // and store parent of each node
    static void dfs(List<int> parent,
             List<List<int>> adj,
             int u,
             int par = -1)
    {
        // Store the immediate parent
        parent[u] = par;

        // Traverse the children of
        // the current node
        foreach(int child in adj[u]) {

            // Recursively call for
            // function dfs for the
            // child node
            if (child != par)
                dfs(parent, adj, child, u);
        }
    }

    // Function to count the number of
    // ancestors with values smaller
    // than that of the current node
    static void countSmallerAncestors(
        List<List<int>> adj, int n)
    {
        // Stores the parent of each node
        List<int> parent = new List<int>();
        for(int i = 0; i < (int)(1e5); i++)
        {
            parent.Add(0);
        }

        // Perform the DFS Traversal
        dfs(parent, adj, 1);

        // Traverse all the nodes
        for (int i = 1; i <= n; i++) {

            int node = i;

            // Store the number of ancestors
            // smaller than node
            int cnt = 0;

            // Loop until parent[node] != -1
            while (parent[node] != -1) {

                // If the condition satisfies,
                // increment cnt by 1
                if (parent[node] < i)
                    cnt += 1;

                node = parent[node];
            }

            // Print the required result
            // for the current node
            Console.Write(cnt + " ");
        }
    }

  static void Main() {
    int N = 6;
    List<List<int>> adj = new List<List<int>>();
    for(int i = 0; i < (int)(1e5); i++)
    {
        adj.Add(new List<int>());
    }

    // Tree Formation
    add_edge(adj, 1, 5);
    add_edge(adj, 1, 4);
    add_edge(adj, 4, 6);
    add_edge(adj, 5, 3);
    add_edge(adj, 5, 2);

    countSmallerAncestors(adj, N);
  }
}**
```

## ****java 描述语言****

```
**<script>

// JavaScript program for the above approach

// Function to add an edge
// between nodes u and v
function add_edge(adj, u, v)
{
    adj[u].push(v);
    adj[v].push(u);
}

// Function to perform the DFS Traversal
// and store parent of each node
function dfs(parent, adj, u, par = -1)
{
    // Store the immediate parent
    parent[u] = par;

    // Traverse the children of
    // the current node
    adj[u].forEach(child => {

        // Recursively call for
        // function dfs for the
        // child node
        if (child != par)
            dfs(parent, adj, child, u);
    });
}

// Function to count the number of
// ancestors with values smaller
// than that of the current node
function countSmallerAncestors(adj, n)
{
    // Stores the parent of each node
    var parent = Array(100000).fill(0);

    // Perform the DFS Traversal
    dfs(parent, adj, 1);

    // Traverse all the nodes
    for (var i = 1; i <= n; i++) {

        var node = i;

        // Store the number of ancestors
        // smaller than node
        var cnt = 0;

        // Loop until parent[node] != -1
        while (parent[node] != -1) {

            // If the condition satisfies,
            // increment cnt by 1
            if (parent[node] < i)
                cnt += 1;

            node = parent[node];
        }

        // Print the required result
        // for the current node
        document.write( cnt + " ");
    }
}

// Driver Code

var N = 6;
var adj = Array.from(Array(100000), ()=>Array());

// Tree Formation
add_edge(adj, 1, 5);
add_edge(adj, 1, 4);
add_edge(adj, 4, 6);
add_edge(adj, 5, 3);
add_edge(adj, 5, 2);
countSmallerAncestors(adj, N);

</script>**
```

******Output:** 

```
0 1 1 1 1 2
```**** 

*******时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*****