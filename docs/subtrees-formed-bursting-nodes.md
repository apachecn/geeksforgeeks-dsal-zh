# 爆发节点后形成的子树

> 原文:[https://www . geesforgeks . org/subtrees-formed-burst-nodes/](https://www.geeksforgeeks.org/subtrees-formed-bursting-nodes/)

您将获得一个具有特殊**属性**的 **n 元树**:如果我们拆分树的一个随机节点，该节点及其直接父节点直到根都将消失。该树有 N 个节点，节点编号从 1 到 N。根始终为 1。给定一系列表示我们开始拆分的节点数的**查询**，问题是为每个独立的查询找到根据上述属性最终将形成的子树的数量。

**示例:**

```
Input:
Consider the following tree:
             1
           / | \ 
          2  3  4
            / \   \
           5   6   7
                  / \
                 8   9

q = 2
n = 1  
n = 7   
Output:
3
4
Explanation:
In the first query after bursting node 1, there 
will be 3 subtrees formed rooted at 2, 3 and 4.
In the second query after bursting node 7, nodes 
4 and 1 also get burst, thus there will 
be 4 subtrees formed rooted at 8, 9, 2 and 3.
```

由于我们正在处理 n 元树，我们可以使用类似于**图**的表示，并在列表数组中添加双向边。现在，如果我们拆分一个节点，我们可以肯定地说，它的所有子树都将成为独立的子树。此外，它的父母和其他祖先的所有孩子，直到根爆裂，也将成为单独的子树。所以在我们的最终答案中，我们希望**排除**当前节点及其路径中的所有祖先，直到根。因此，我们可以形成**方程**求解为:

答案[node] =度[node]+all child[parent[node]]–count path[node]
其中 allChild[]:节点的子节点数+其
父节点的子节点数+..+根的子节点数
父节点[]:树中节点的父节点
度[]:节点的子节点数
计数路径[]:从根到节点父节点的节点数

我们可以使用邻接表上的**深度优先搜索**来填充上面所有的数组。我们可以从根 1 开始，假设它的父级为 0，并首先重复深度，将其值传播给其子级。因此，我们可以对上述数组进行预处理和填充，并相应地为每个查询返回等式的值。

以下是上述方法的实施情况:

## C++

```
// C++ program to find number of subtrees after bursting nodes
#include <bits/stdc++.h>
using namespace std;

// do depth first search of node nod; par is its parent
void dfs(int nod, int par, list<int> adj[], int allChild[],
         int parent[], int degree[], int countPath[])
{
    // go through the adjacent nodes
    for (auto it = adj[nod].begin(); it != adj[nod].end(); it++) {
        int curr = *it;

        // avoid cycling
        if (curr == par)
            continue;

        degree[nod]++;
        countPath[curr] = countPath[nod] + 1;
        parent[curr] = nod;
    }

    // propagated from parent
    allChild[nod] = allChild[parent[nod]] + degree[nod];

    // go through the adjacent nodes
    for (auto it = adj[nod].begin(); it != adj[nod].end(); it++) {
        int curr = *it;

        // avoid cycling
        if (curr == par)
            continue;

        // recur and go depth first
        dfs(curr, nod, adj, allChild, parent, degree, countPath);
    }
}

// Driver code
int main()
{
    int n = 9;

    // adjacency list for each node
    list<int> adj[n + 1];

    // allChild[]: number of node's children + number of its
    // parent's children + ..+ number of root's children
    // parent[]: parent of a node in the tree
    // degree[]: number of children for a node
    // countPath[]: number of nodes from root to parent of node
    int allChild[n + 1] = { 0 }, parent[n + 1] = { 0 },
       degree[n + 1] = { 0 }, countPath[n + 1] = { 0 };

    // construct tree
    adj[1].push_back(2);
    adj[2].push_back(1);
    adj[1].push_back(3);
    adj[3].push_back(1);
    adj[1].push_back(4);
    adj[4].push_back(1);
    adj[3].push_back(5);
    adj[5].push_back(3);
    adj[3].push_back(6);
    adj[6].push_back(3);
    adj[4].push_back(7);
    adj[7].push_back(4);
    adj[7].push_back(8);
    adj[8].push_back(7);
    adj[7].push_back(9);
    adj[9].push_back(7);

    // assume 1 is root and 0 is its parent
    dfs(1, 0, adj, allChild, parent, degree, countPath);

    // 2 queries
    int curr = 1;
    cout << degree[curr] + allChild[parent[curr]] - countPath[curr] << endl;

    curr = 7;
    cout << degree[curr] + allChild[parent[curr]] - countPath[curr] << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of subtrees
// after bursting nodes
import java.util.*;

class GFG{

// Do depth first search of node nod;
// par is its parent
static void dfs(int nod, int par,
                List<Integer> adj[],
                int allChild[],
                int parent[],
                int degree[],
                int countPath[])
{

    // Go through the adjacent nodes
    for(int it : adj[nod])
    {
        int curr = it;

        // astatic void cycling
        if (curr == par)
            continue;

        degree[nod]++;
        countPath[curr] = countPath[nod] + 1;
        parent[curr] = nod;
    }

    // Propagated from parent
    allChild[nod] = allChild[parent[nod]] +
                             degree[nod];

    // Go through the adjacent nodes
    for(int it : adj[nod])
    {
        int curr = it;

        // astatic void cycling
        if (curr == par)
            continue;

        // recur and go depth first
        dfs(curr, nod, adj, allChild,
            parent, degree, countPath);
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 9;

    // Adjacency list for each node
    @SuppressWarnings("unchecked")
    List<Integer> []adj = new List[n + 1];
    for(int i = 0; i < adj.length; i++)
        adj[i] = new Vector<Integer>();

    // allChild[]: number of node's children +
    // number of its parent's children + ..+
    // number of root's children
    // parent[]: parent of a node in the tree
    // degree[]: number of children for a node
    // countPath[]: number of nodes from root
    // to parent of node
    int []allChild = new int[n + 1];
    int []parent = new int[n + 1];
    int []degree = new int[n + 1];
    int []countPath = new int[n + 1];

    // Contree
    adj[1].add(2);
    adj[2].add(1);
    adj[1].add(3);
    adj[3].add(1);
    adj[1].add(4);
    adj[4].add(1);
    adj[3].add(5);
    adj[5].add(3);
    adj[3].add(6);
    adj[6].add(3);
    adj[4].add(7);
    adj[7].add(4);
    adj[7].add(8);
    adj[8].add(7);
    adj[7].add(9);
    adj[9].add(7);

    // Assume 1 is root and 0 is its parent
    dfs(1, 0, adj, allChild, parent,
        degree, countPath);

    // 2 queries
    int curr = 1;
    System.out.print(degree[curr] +
            allChild[parent[curr]] -
                  countPath[curr] + "\n");

    curr = 7;
    System.out.print(degree[curr] +
            allChild[parent[curr]] -
                  countPath[curr] + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to find number of
# subtrees after bursting nodes

# Do depth first search of node
# nod par is its parent
def dfs(nod, par, adj, allChild,
        parent, degree, countPath):

    # Go through the adjacent nodes
    for it in adj[nod]:
        curr = it

        # Avoid cycling
        if (curr == par):
            continue

        degree[nod] += 1
        countPath[curr] = countPath[nod] + 1
        parent[curr] = nod

    # Propagated from parent
    allChild[nod] = (allChild[parent[nod]] +
                     degree[nod])

    # Go through the adjacent nodes
    for it in adj[nod]:
        curr = it

        # Avoid cycling
        if (curr == par):
            continue

        # recur and go depth first
        dfs(curr, nod, adj, allChild,
            parent, degree, countPath)

# Driver code
if __name__ == '__main__':

    n = 9

    # Adjacency list for each node
    adj = [[] for i in range(n + 1)]

    # allChild: number of node's children + number of its
    # parent's children + ..+ number of root's children
    # parent: parent of a node in the tree
    # degree: number of children for a node
    # countPath: number of nodes from root to parent of node
    allChild, parent = [0] * (n + 1), [0] * (n + 1)
    degree, countPath = [0] * (n + 1), [0] * (n + 1)

    # Construct tree
    adj[1].append(2)
    adj[2].append(1)
    adj[1].append(3)
    adj[3].append(1)
    adj[1].append(4)
    adj[4].append(1)
    adj[3].append(5)
    adj[5].append(3)
    adj[3].append(6)
    adj[6].append(3)
    adj[4].append(7)
    adj[7].append(4)
    adj[7].append(8)
    adj[8].append(7)
    adj[7].append(9)
    adj[9].append(7)

    # Assume 1 is root and 0 is its parent
    dfs(1, 0, adj, allChild, parent,
        degree, countPath)

    # 2 queries
    curr = 1
    print(degree[curr] + allChild[parent[curr]] -
          countPath[curr])

    curr = 7
    print(degree[curr] + allChild[parent[curr]] -
          countPath[curr])

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find number of subtrees
// after bursting nodes
using System;
using System.Collections.Generic;

class GFG{

// Do depth first search of node nod;
// par is its parent
static void dfs(int nod, int par,
                List<int> []adj,
                int []allChild,
                int []parent,
                int []degree,
                int []countPath)
{

    // Go through the adjacent nodes
    foreach(int it in adj[nod])
    {
        int curr = it;

        // astatic void cycling
        if (curr == par)
            continue;

        degree[nod]++;
        countPath[curr] = countPath[nod] + 1;
        parent[curr] = nod;
    }

    // Propagated from parent
    allChild[nod] = allChild[parent[nod]] +
                             degree[nod];

    // Go through the adjacent nodes
    foreach(int it in adj[nod])
    {
        int curr = it;

        // astatic void cycling
        if (curr == par)
            continue;

        // recur and go depth first
        dfs(curr, nod, adj, allChild,
            parent, degree, countPath);
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 9;

    // Adjacency list for each node
    List<int> []adj = new List<int>[n + 1];
    for(int i = 0; i < adj.Length; i++)
        adj[i] = new List<int>();

    // allChild[]: number of node's children +
    // number of its parent's children + ..+
    // number of root's children
    // parent[]: parent of a node in the tree
    // degree[]: number of children for a node
    // countPath[]: number of nodes from root
    // to parent of node
    int []allChild = new int[n + 1];
    int []parent = new int[n + 1];
    int []degree = new int[n + 1];
    int []countPath = new int[n + 1];

    // Contree
    adj[1].Add(2);
    adj[2].Add(1);
    adj[1].Add(3);
    adj[3].Add(1);
    adj[1].Add(4);
    adj[4].Add(1);
    adj[3].Add(5);
    adj[5].Add(3);
    adj[3].Add(6);
    adj[6].Add(3);
    adj[4].Add(7);
    adj[7].Add(4);
    adj[7].Add(8);
    adj[8].Add(7);
    adj[7].Add(9);
    adj[9].Add(7);

    // Assume 1 is root and 0 is its parent
    dfs(1, 0, adj, allChild, parent,
        degree, countPath);

    // 2 queries
    int curr = 1;
    Console.Write(degree[curr] +
        allChild[parent[curr]] -
               countPath[curr] + "\n");

    curr = 7;
    Console.Write(degree[curr] +
        allChild[parent[curr]] -
               countPath[curr] + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program to find number of subtrees
// after bursting nodes

    // Do depth first search of node nod;
// par is its parent
    function dfs(nod,par,adj,allChild,parent,degree,countPath)
    {
        // Go through the adjacent nodes
    for(let it=0;it<adj[nod].length;it++)
    {
        let curr = adj[nod][it];

        // astatic void cycling
        if (curr == par)
            continue;

        degree[nod]++;
        countPath[curr] = countPath[nod] + 1;
        parent[curr] = nod;
    }

    // Propagated from parent
    allChild[nod] = allChild[parent[nod]] +
                             degree[nod];

    // Go through the adjacent nodes
    for(let it=0;it<adj[nod].length;it++)
    {
        let curr = adj[nod][it];

        // astatic void cycling
        if (curr == par)
            continue;

        // recur and go depth first
        dfs(curr, nod, adj, allChild,
            parent, degree, countPath);
    }
    }

    // Driver code
    let n = 9;

    // Adjacency list for each node
    let adj = new Array(n + 1);
    for(let i = 0; i < adj.length; i++)
        adj[i] = [];

    // allChild[]: number of node's children +
    // number of its parent's children + ..+
    // number of root's children
    // parent[]: parent of a node in the tree
    // degree[]: number of children for a node
    // countPath[]: number of nodes from root
    // to parent of node
    let allChild = new Array(n + 1);
    let parent = new Array(n + 1);
    let degree = new Array(n + 1);
    let countPath = new Array(n + 1);
     for(let i=0;i<n+1;i++)
    {
        allChild[i]=0;
        parent[i]=0;
        degree[i]=0;
        countPath[i]=0;
    }

    // Contree
    adj[1].push(2);
    adj[2].push(1);
    adj[1].push(3);
    adj[3].push(1);
    adj[1].push(4);
    adj[4].push(1);
    adj[3].push(5);
    adj[5].push(3);
    adj[3].push(6);
    adj[6].push(3);
    adj[4].push(7);
    adj[7].push(4);
    adj[7].push(8);
    adj[8].push(7);
    adj[7].push(9);
    adj[9].push(7);

    // Assume 1 is root and 0 is its parent
    dfs(1, 0, adj, allChild, parent,
        degree, countPath);

    // 2 queries
    let curr = 1;
    document.write(degree[curr] +
            allChild[parent[curr]] -
                  countPath[curr] + "<br>");

    curr = 7;
    document.write(degree[curr] +
            allChild[parent[curr]] -
                  countPath[curr] + "<br>");

// This code is contributed by unknown2108
</script>
```

**输出:**

```
3 
4
```

上述算法的**时间复杂度**为 O(E * lg(V))，其中 E 为边数，V 为顶点数。