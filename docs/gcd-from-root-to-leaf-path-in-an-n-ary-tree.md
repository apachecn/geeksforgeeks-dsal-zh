# N 元树中从根到叶路径的 GCD

> 原文:[https://www . geesforgeks . org/gcd-从根到叶的 n 叉树路径/](https://www.geeksforgeeks.org/gcd-from-root-to-leaf-path-in-an-n-ary-tree/)

给定一个 **N 元树**和一个存储所有节点相关值的数组 **val[]** 。还给出了叶节点 **X** 和 **N** 整数，表示节点的值。任务是在叶到根的路径中找到节点中所有数字的 **gcd** 。
**举例:**

```
Input: 
            1
          /   \ 
        2      3
      /      /   \ 
     4      5     6 
                /   \
              7      8 

val[] = { -1, 6, 2, 6, 3, 4, 12, 10, 18 } 
leaf = 8 
Output: 6 

GCD(val[1], val[3], val[6], val[8]) = GCD(6, 6, 12, 18) = 6 

Input:
            1
          /   \ 
        2      3
      /      /   \ 
     4      5     6 
                /   \
              7      8 

val[] = { 6, 2, 6, 3, 4, 12, 10, 18 }
leaf = 5  
Output: 2
```

**方法:**使用[树](https://www.geeksforgeeks.org/dfs-traversal-of-a-tree-using-recursion/)中的 DFS 可以解决问题。在 DFS 函数中，我们包含一个额外的参数 G，初始值作为根。每次递归调用 DFS 函数访问一个新节点时，都会将 **G** 的值更新为 [**gcd**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) **(G，val【node】)**。一旦我们到达给定的叶节点，我们打印 gcd(G，val[叶节点])的值，并脱离 DFS 函数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 9

// Function to add edges in the tree
void addEgde(list<int>* adj, int u, int v)
{
    adj[u].push_back(v);
    adj[v].push_back(u);
}

// Function to find the GCD from root to leaf path
void DFS(int node, int parent, int G, int leaf,
         int val[], list<int>* adj)
{
    // If we reach the desired leaf
    if (node == leaf) {
        G = __gcd(G, val[node]);
        cout << G;
        return;
    }

    // Call DFS for children
    for (auto it : adj[node]) {

        if (it != parent)
            DFS(it, node, __gcd(G, val[it]), leaf, val, adj);
    }
}

// Driver code
int main()
{

    int n = 8;
    list<int>* adj = new list<int>[n + 1];

    addEgde(adj, 1, 2);
    addEgde(adj, 2, 4);
    addEgde(adj, 1, 3);
    addEgde(adj, 3, 5);
    addEgde(adj, 3, 6);
    addEgde(adj, 6, 7);
    addEgde(adj, 6, 8);

    int leaf = 5;

    // -1 to indicate no value in node 0
    int val[] = { -1, 6, 2, 6, 3, 4, 12, 10, 18 };

    // Initially GCD is the value of the root
    int G = val[1];

    DFS(1, -1, G, leaf, val, adj);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static final int N = 9;

// Function to add edges in the tree
static void addEgde(List<Integer> []adj, int u, int v)
{
    adj[u].add(v);
    adj[v].add(u);
}

// Function to find the GCD from root to leaf path
static void DFS(int node, int parent, int G, int leaf,
        int val[], List<Integer> []adj)
{
    // If we reach the desired leaf
    if (node == leaf)
    {
        G = __gcd(G, val[node]);
        System.out.print(G);
        return;
    }

    // Call DFS for children
    for (int it : adj[node])
    {

        if (it != parent)
            DFS(it, node, __gcd(G, val[it]), leaf, val, adj);
    }
}
static int __gcd(int a, int b)
{
    return b == 0? a:__gcd(b, a % b);    
}

// Driver code
public static void main(String[] args)
{

    int n = 8;
    List<Integer> []adj = new LinkedList[n + 1];
        for (int i = 0; i < n + 1; i++)
            adj[i] = new LinkedList<Integer>();
    addEgde(adj, 1, 2);
    addEgde(adj, 2, 4);
    addEgde(adj, 1, 3);
    addEgde(adj, 3, 5);
    addEgde(adj, 3, 6);
    addEgde(adj, 6, 7);
    addEgde(adj, 6, 8);

    int leaf = 5;

    // -1 to indicate no value in node 0
    int val[] = { -1, 6, 2, 6, 3, 4, 12, 10, 18 };

    // Initially GCD is the value of the root
    int G = val[1];

    DFS(1, -1, G, leaf, val, adj);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import gcd
N = 9

# Function to add edges in the tree
def addEgde(adj, u, v):
    adj[u].append(v)
    adj[v].append(u)

# Function to find the GCD
# from root to leaf path
def DFS(node, parent, G, leaf, val, adj):

    # If we reach the desired leaf
    if (node == leaf):
        G = gcd(G, val[node])
        print(G, end = "")
        return

    # Call DFS for children
    for it in adj[node]:
        if (it != parent):
            DFS(it, node, gcd(G, val[it]),
                          leaf, val, adj)

# Driver code
if __name__ == '__main__':
    n = 8
    adj = [[0 for i in range(n + 1)]
              for j in range(n + 1)]

    addEgde(adj, 1, 2)
    addEgde(adj, 2, 4)
    addEgde(adj, 1, 3)
    addEgde(adj, 3, 5)
    addEgde(adj, 3, 6)
    addEgde(adj, 6, 7)
    addEgde(adj, 6, 8)

    leaf = 5

    # -1 to indicate no value in node 0
    val = [-1, 6, 2, 6, 3, 4, 12, 10, 18]

    # Initially GCD is the value of the root
    G = val[1]

    DFS(1, -1, G, leaf, val, adj)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
static readonly int N = 9;

// Function to add edges in the tree
static void addEgde(List<int> []adj, int u, int v)
{
    adj[u].Add(v);
    adj[v].Add(u);
}

// Function to find the GCD from root to leaf path
static void DFS(int node, int parent, int G, int leaf,
        int []val, List<int> []adj)
{
    // If we reach the desired leaf
    if (node == leaf)
    {
        G = __gcd(G, val[node]);
        Console.Write(G);
        return;
    }

    // Call DFS for children
    foreach (int it in adj[node])
    {

        if (it != parent)
            DFS(it, node, __gcd(G, val[it]), leaf, val, adj);
    }
}
static int __gcd(int a, int b)
{
    return b == 0? a:__gcd(b, a % b);    
}

// Driver code
public static void Main(String[] args)
{

    int n = 8;
    List<int> []adj = new List<int>[n + 1];
        for (int i = 0; i < n + 1; i++)
            adj[i] = new List<int>();
    addEgde(adj, 1, 2);
    addEgde(adj, 2, 4);
    addEgde(adj, 1, 3);
    addEgde(adj, 3, 5);
    addEgde(adj, 3, 6);
    addEgde(adj, 6, 7);
    addEgde(adj, 6, 8);

    int leaf = 5;

    // -1 to indicate no value in node 0
    int []val = { -1, 6, 2, 6, 3, 4, 12, 10, 18 };

    // Initially GCD is the value of the root
    int G = val[1];

    DFS(1, -1, G, leaf, val, adj);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

let N = 9;

// Function to add edges in the tree
function addEgde(adj,u,v)
{
    adj[u].push(v);
    adj[v].push(u);
}

// Function to find the GCD from root to leaf path
function DFS(node,parent,G,leaf,val,adj)
{
    // If we reach the desired leaf
    if (node == leaf)
    {
        G = __gcd(G, val[node]);
        document.write(G);
        return;
    }

    // Call DFS for children
    for (let it of adj[node])
    {

        if (it != parent)
            DFS(it, node, __gcd(G, val[it]), leaf, val, adj);
    }
}

// Driver code
function __gcd(a,b)
{
    return b == 0? a:__gcd(b, a % b);   
}

let n = 8;
let adj = new Array(n + 1);
for (let i = 0; i < n + 1; i++)
    adj[i] = [];
addEgde(adj, 1, 2);
addEgde(adj, 2, 4);
addEgde(adj, 1, 3);
addEgde(adj, 3, 5);
addEgde(adj, 3, 6);
addEgde(adj, 6, 7);
addEgde(adj, 6, 8);

let leaf = 5;

// -1 to indicate no value in node 0
let val = [ -1, 6, 2, 6, 3, 4, 12, 10, 18 ];

// Initially GCD is the value of the root
let G = val[1];

DFS(1, -1, G, leaf, val, adj);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
2
```