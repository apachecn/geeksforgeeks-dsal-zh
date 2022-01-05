# 给定 N 元树的每个顶点的最大子树和

> 原文:[https://www . geesforgeks . org/给定 n 元树的每个顶点的最大子树和/](https://www.geeksforgeeks.org/largest-subtree-sum-for-each-vertex-of-given-n-ary-tree/)

给定一个由 **N** 个节点组成的 [N 数组](https://www.geeksforgeeks.org/generic-treesn-array-trees/)树，根在 **1** ，边为 **{u，v}** 形式，以及一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **值[]** 。每个顶点 **i** 都有一个由**值【I】**表示的整数值。任务是通过将每个顶点的值添加到其子顶点的非空子集，为每个顶点找到最大的子树和。

**示例:**

> **输入:**边[][] = {{1，2}，{1，3}，{3，4}}，值[] = {1，-1，0，1}
> **输出:** 2 -1 1 1
> **解释:**
> 下面是给定的树:
> 
> 1
> / \
> 2 3
> \
> 4
> 可以为每个顶点选择以下子集:
> 顶点 1:可以用值{1，0，1}选择顶点{1，3，4}的子集。因此，sum = 1 + 0 + 1 = 2。
> 顶点 2:顶点{2}的子集可以用值{-1}选择。因此，sum = -1。
> 顶点 3:顶点{3，4}的子集可以用值{0，1}选择。因此，sum = 0 + 1 = 1。
> 顶点 4:可以用值{1}选择顶点{4}的子集。因此，总和= 1。
> 
> **输入:**边[][] = {{1，2}，{1，3}，{2，4}，{2，5}}，值[] = {1，-1，-2，1，3}
> **输出:** 5 4 -2 1 3
> **解释:**
> 下面是给定的树:
> 
> 1
> / \
> 2 3
> / \
> 4 5
> 可以为每个顶点选择以下子集:
> 顶点 1:可以选择值为{1，1，3}的顶点子集{1，4，5}。因此，sum = 1 + 1 + 3 = 5。
> 顶点 2:顶点{4，5}的子集可以用值{1，3}选择。因此，sum = 1 + 3 = 4。
> 顶点 3:可以用值{-2}选择顶点{3}的子集。因此，sum = -2。
> 顶点 4:可以用值{1}选择顶点{4}的子集。因此，总和= 1。
> 顶点 5:可以用值{3}选择顶点{5}的子集。因此，总和= 3。

**天真方法:**最简单的方法是遍历每个顶点的子树 **i** 从 **1** 到 **N** 并对其执行 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)。对于每个顶点 **i** ，选择其子顶点中具有非负值的子集。如果所选顶点的子集为空，则搜索并打印具有最小值的节点，使其成为顶点 **i** 的子节点。否则，打印子集中存在的节点的节点值总和。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**思路是使用 [DFS 遍历](https://www.geeksforgeeks.org/depth-first-traversal-for-a-graph/)和[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)方法。按照以下步骤解决问题:

*   初始化一个大小为 **N** 的数组**ans【】**来存储每个顶点的最大[子树和](https://www.geeksforgeeks.org/find-largest-subtree-sum-tree/)。
*   对每个顶点执行 DFS 遍历，并对每个顶点使用一些大负值初始化 **v** 、**ans【v】**。
*   如果顶点 **v** 是一个叶子顶点，那么这个顶点的答案就是**值【v】**。因此，分配 **ans[v] = values[v]** 。
*   否则，遍历与顶点 **v** 相邻的顶点，对于每个相邻的顶点 **u** ，将 **ans[v]** 更新为 **ans[v] = max(ans[u] +值[v]，值[v]，ans[u])** 。
*   完成上述步骤后，打印存储在**ans【】**数组中的值，作为每个顶点的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define V 3
#define M 2

// Function to perform the DFS
// Traversal on the given Tree
void dfs(int v, int p,
         vector<int> adj[],
     int ans[], int vals[])
{

    // To check if v is leaf vertex
    bool isLeaf = 1;

    // Initialize answer for vertex v
    ans[v] = INT_MIN;

    // Traverse adjacency list of v
    for(int u : adj[v])
    {
        if (u == p)
            continue;

        isLeaf = 0;
        dfs(u, v, adj, ans, vals);

        // Update maximum subtree sum
        ans[v] = max(ans[u] + vals[v],
                 max(ans[u], vals[u]));
    }

    // If v is leaf
    if (isLeaf)
    {
        ans[v] = vals[v];
    }
}

// Function to calculate maximum
// subtree sum for each vertex
void printAnswer(int n,
                 int edges[V][M],
                 int values[])
{

    // Stores the adjacency list
    vector<int> adj[n];

    // Add Edegs to the list
    for(int i = 0; i < n - 1; i++)
    {
        int u = edges[i][0] - 1;
        int v = edges[i][1] - 1;

        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    // Stores largest subtree
    // sum for each vertex
    int ans[n] ;

    // Calculate answer
    dfs(0, -1, adj, ans, values);

    // Print the result
    for(auto x : ans)
    {
        cout << x << " ";
    }
}

// Driver Code
int main()
{

    // Given nodes
    int N = 4;

    // Give N edges
    int edges[V][M] = { { 1, 2 },
                        { 1, 3 },
                        { 3, 4 } };

    // Given values
    int values[] = { 1, -1, 0, 1 };

    // Function Call
    printAnswer(N, edges, values);
}

// This code is contributed by Princi Singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.ArrayList;

@SuppressWarnings("unchecked")
class GFG {

    // Function to perform the DFS
    // Traversal on the given Tree
    static void dfs(int v, int p,
                    ArrayList<Integer> adj[],
                    int ans[], int vals[])
    {

        // To check if v is leaf vertex
        boolean isLeaf = true;

        // Initialize answer for vertex v
        ans[v] = Integer.MIN_VALUE;

        // Traverse adjacency list of v
        for (int u : adj[v]) {
            if (u == p)
                continue;
            isLeaf = false;
            dfs(u, v, adj, ans, vals);

            // Update maximum subtree sum
            ans[v] = Math.max(
                ans[u] + vals[v],
                Math.max(ans[u],
                         vals[u]));
        }

        // If v is leaf
        if (isLeaf) {
            ans[v] = vals[v];
        }
    }

    // Function to calculate maximum
    // subtree sum for each vertex
    static void printAnswer(
        int n, int edges[][], int values[])
    {

        // Stores the adjacency list
        ArrayList<Integer> adj[]
            = new ArrayList[n];

        for (int i = 0; i < n; i++)
            adj[i] = new ArrayList<>();

        // Add Edegs to the list
        for (int i = 0; i < n - 1; i++) {

            int u = edges[i][0] - 1;
            int v = edges[i][1] - 1;
            adj[u].add(v);
            adj[v].add(u);
        }

        // Stores largest subtree
        // sum for each vertex
        int ans[] = new int[n];

        // Calculate answer
        dfs(0, -1, adj, ans, values);

        // Print the result
        for (int x : ans) {
            System.out.print(x + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given nodes
        int N = 4;

        // Give N edges
        int edges[][]
            = new int[][] { { 1, 2 },
                            { 1, 3 },
                            { 3, 4 } };

        // Given values
        int values[] = { 1, -1, 0, 1 };

        // Function Call
        printAnswer(N, edges, values);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

V = 3
M = 2

# Function to perform the DFS
# Traversal on the given Tree
def dfs(v, p):

    # To check if v is leaf vertex
    isLeaf = 1

    # Initialize answer for vertex v
    ans[v] = -10**9

    # Traverse adjacency list of v
    for u in adj[v]:
        if (u == p):
            continue

        isLeaf = 0
        dfs(u, v)

        # Update maximum subtree sum
        ans[v] = max(ans[u] + vals[v],max(ans[u], vals[u]))

    # If v is leaf
    if (isLeaf):
        ans[v] = vals[v]

# Function to calculate maximum
# subtree sum for each vertex
def printAnswer(n, edges, vals):

    # Stores the adjacency list
    # vector<int> adj[n];

    # Add Edegs to the list
    for i in range(n - 1):
        u = edges[i][0] - 1
        v = edges[i][1] - 1

        adj[u].append(v)
        adj[v].append(u)

    # Calculate answer
    dfs(0, -1)

    # Prthe result
    for x in ans:
        print(x, end=" ")

# Driver Code
if __name__ == '__main__':

    # Given nodes
    N = 4

    # Give N edges
    edges=[ [ 1, 2],
            [ 1, 3],
            [ 3, 4] ]

    adj=[[] for i in range(N)]
    ans=[0 for i in range(N)]

    # Given values
    vals=[1, -1, 0, 1]

    # Function Call
    printAnswer(N, edges, vals)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to perform the DFS
// Traversal on the given Tree
static void dfs(int v, int p,
                List<int> []adj,
                int []ans, int []vals)
{
  // To check if v is leaf
  // vertex
  bool isLeaf = true;

  // Initialize answer for
  // vertex v
  ans[v] = int.MinValue;

  // Traverse adjacency list
  // of v
  foreach (int u in adj[v])
  {
    if (u == p)
      continue;
    isLeaf = false;
    dfs(u, v, adj, ans, vals);

    // Update maximum subtree
    // sum
    ans[v] = Math.Max(ans[u] +
                      vals[v],
             Math.Max(ans[u],
                      vals[u]));
  }

  // If v is leaf
  if (isLeaf)
  {
    ans[v] = vals[v];
  }
}

// Function to calculate maximum
// subtree sum for each vertex
static void printAnswer(int n,
                        int [,]edges,
                        int []values)
{
  // Stores the adjacency list
  List<int> []adj =
       new List<int>[n];

  for (int i = 0; i < n; i++)
    adj[i] = new List<int>();

  // Add Edegs to the list
  for (int i = 0;
           i < n - 1; i++)
  {
    int u = edges[i, 0] - 1;
    int v = edges[i, 1] - 1;
    adj[u].Add(v);
    adj[v].Add(u);
  }

  // Stores largest subtree
  // sum for each vertex
  int []ans = new int[n];

  // Calculate answer
  dfs(0, -1, adj,
      ans, values);

  // Print the result
  foreach (int x in ans)
  {
    Console.Write(x + " ");
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given nodes
  int N = 4;

  // Give N edges
  int [,]edges = new int[,] {{1, 2},
                             {1, 3},
                             {3, 4}};
  // Given values
  int []values = {1, -1, 0, 1};

  // Function Call
  printAnswer(N, edges, values);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to perform the DFS
    // Traversal on the given Tree
    function dfs(v, p, adj, ans, vals)
    {
      // To check if v is leaf
      // vertex
      let isLeaf = true;

      // Initialize answer for
      // vertex v
      ans[v] = Number.MIN_VALUE;

      // Traverse adjacency list
      // of v
      for(let u = 0; u < adj[v].length; u++)
      {
        if (adj[v][u] == p)
          continue;
        isLeaf = false;
        dfs(adj[v][u], v, adj, ans, vals);

        // Update maximum subtree
        // sum
        ans[v] = Math.max(ans[adj[v][u]] +
                          vals[v],
                 Math.max(ans[adj[v][u]],
                          vals[adj[v][u]]));
      }

      // If v is leaf
      if (isLeaf)
      {
        ans[v] = vals[v];
      }
    }

    // Function to calculate maximum
    // subtree sum for each vertex
    function printAnswer(n, edges, values)
    {
      // Stores the adjacency list
      let adj = new Array(n);

      for (let i = 0; i < n; i++)
        adj[i] = [];

      // Add Edegs to the list
      for (let i = 0; i < n - 1; i++)
      {
        let u = edges[i][0] - 1;
        let v = edges[i][1] - 1;
        adj[u].push(v);
        adj[v].push(u);
      }

      // Stores largest subtree
      // sum for each vertex
      let ans = new Array(n);

      // Calculate answer
      dfs(0, -1, adj, ans, values);

      // Print the result
      for(let x = 0; x < ans.length; x++)
      {
        document.write(ans[x] + " ");
      }
    }

    // Given nodes
    let N = 4;

    // Give N edges
    let edges = [[1, 2], [1, 3], [3, 4]];
    // Given values
    let values = [1, -1, 0, 1];

    // Function Call
    printAnswer(N, edges, values);

</script>
```

**Output:** 

```
2 -1 1 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)