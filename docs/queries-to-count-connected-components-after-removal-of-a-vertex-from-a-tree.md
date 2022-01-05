# 从树中移除顶点后对连接的组件进行计数的查询

> 原文:[https://www . geeksforgeeks . org/从树中移除顶点后查询计数连接组件/](https://www.geeksforgeeks.org/queries-to-count-connected-components-after-removal-of-a-vertex-from-a-tree/)

给定由范围**【0，N)** 中的值组成的 **N** 节点组成的[树和由范围**【0，N)** 中的值组成的 **Q** 整数的数组**查询[]** 。每个查询的任务是移除顶点值 **Q[i]** ，并计算结果图中的连通分量。](https://www.geeksforgeeks.org/generic-treesn-array-trees/)

**示例:**

> **输入:** N = 7，边[][2] = {{0，1}，{0，2}，{0，3}，{1，4}，{1，5}，{3，6}}，查询[] = {0，1，6}
> 
> ![](img/e52ab83d38307572f6627b99c71e0980.png)
> 
> **输出:**
> 3 3 1
> **解释:**
> **查询 1:** 移除值为 0 的节点会导致移除边(0，1)、(0，2)和(0，3)。因此，剩下的图有 3 个连通分量:[1，4，5]，[2]，[3，6]
> **查询 2:** 移除值为 1 的节点会导致移除边(1，4)、(1，5)和(1，0)。因此，剩余图有 3 个连通分量:[4]，[5]，[2，0，3，6]
> **查询 3:** 移除值为 6 的节点会导致移除边(3，6)。因此，剩下的图有 1 个连通分量:[0，1，2，3，4，5]。
> 
> **输入:** N = 7，边[][2] = {{0，1}，{0，2}，{0，3}，{1，4}，{1，5}，{3，6}}，查询[] = {5，3，2}
> 
> ![](img/e52ab83d38307572f6627b99c71e0980.png)
> 
> **输出:** 1 2 1
> **解释:**
> **查询 1:** 值为 5 的节点的移除导致边缘(1，5)的移除。因此，剩下的图有 1 个连通分量:[0，1，2，3，4，6]
> **查询 2:** 移除值为 3 的节点会导致移除边(0，3)，(3，6)。因此，剩下的图有 2 个连通分量:[0，1，2，4，5]，[6]
> **查询 3:** 移除值为 2 的节点会导致移除边(0，2)。因此，剩下的图有 1 个连通分支:[0，1，3，4，5，6]

**方法:**想法是观察在**树**中，每当删除一个节点时，连接到该节点的节点就会分离。因此，连接组件的[计数等于删除节点](https://www.geeksforgeeks.org/program-to-count-number-of-connected-components-in-an-undirected-graph/)的[度。
因此，方法是预先计算并存储数组中每个节点](https://www.geeksforgeeks.org/find-degree-particular-vertex-graph/)的[度。对于每个查询，连接组件的计数只是查询中对应节点的度。](https://www.geeksforgeeks.org/print-the-degree-of-every-node-from-the-given-prufer-sequence/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define MAX 100005

// Stores degree of the nodes
int degree[MAX];

// Function that finds the degree of
// each node in the given graph
void DegreeOfNodes(int Edges[][2],
                   int N)
{
    // Precompute degrees of each node
    for (int i = 0; i < N - 1; i++) {
        degree[Edges[i][0]]++;
        degree[Edges[i][1]]++;
    }
}

// Function to print the number of
// connected components
void findConnectedComponents(int x)
{
    // Print the degree of node x
    cout << degree[x] << ' ';
}

// Function that counts the connected
// components after removing a vertex
// for each query
void countCC(int N, int Q, int Queries[],
             int Edges[][2])
{

    // Count degree of each node
    DegreeOfNodes(Edges, N);

    // Iterate over each query
    for (int i = 0; i < Q; i++) {

        // Find connected components
        // after removing given vertex
        findConnectedComponents(Queries[i]);
    }
}

// Driver Code
int main()
{
    // Given N nodes and Q queries
    int N = 7, Q = 3;

    // Given array of queries
    int Queries[] = { 0, 1, 6 };

    // Given Edges
    int Edges[][2] = { { 0, 1 }, { 0, 2 },
                       { 0, 3 }, { 1, 4 },
                       { 1, 5 }, { 3, 6 } };

    // Function Call
    countCC(N, Q, Queries, Edges);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG{

static final int MAX  = 100005;

// Stores degree of the nodes
static int []degree = new int[MAX];

// Function that finds the degree of
// each node in the given graph
static void DegreeOfNodes(int [][]Edges,
                          int N)
{
  // Precompute degrees of each node
  for (int i = 0; i < N - 1; i++)
  {
    degree[Edges[i][0]]++;
    degree[Edges[i][1]]++;
  }
}

// Function to print the number of
// connected components
static void findConnectedComponents(int x)
{
  // Print the degree of node x
  System.out.print(degree[x] + " ");
}

// Function that counts the connected
// components after removing a vertex
// for each query
static void countCC(int N, int Q,
                    int Queries[],
                    int [][]Edges)
{
  // Count degree of each node
  DegreeOfNodes(Edges, N);

  // Iterate over each query
  for (int i = 0; i < Q; i++)
  {
    // Find connected components
    // after removing given vertex
    findConnectedComponents(Queries[i]);
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given N nodes and Q queries
  int N = 7, Q = 3;

  // Given array of queries
  int Queries[] = {0, 1, 6};

  // Given Edges
  int [][]Edges = {{0, 1}, {0, 2},
                   {0, 3}, {1, 4},
                   {1, 5}, {3, 6}};

  // Function Call
  countCC(N, Q, Queries, Edges);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
MAX = 100005

# Stores degree of the nodes
degree = [0] * MAX

# Function that finds the degree of
# each node in the given graph
def DegreeOfNodes(Edges, N):

    # Precompute degrees of each node
    for i in range(N - 1):
        degree[Edges[i][0]] += 1
        degree[Edges[i][1]] += 1

# Function to print the number of
# connected components
def findConnectedComponents(x):

    # Print the degree of node x
    print(degree[x], end = " ")

# Function that counts the connected
# components after removing a vertex
# for each query
def countCC(N, Q, Queries, Edges):

    # Count degree of each node
    DegreeOfNodes(Edges, N)

    # Iterate over each query
    for i in range(Q):

        # Find connected components
        # after removing given vertex
        findConnectedComponents(Queries[i])

# Driver Code
if __name__ == '__main__':

    # Given N nodes and Q queries
    N = 7
    Q = 3

    # Given array of queries
    Queries = [ 0, 1, 6 ]

    # Given Edges
    Edges = [ [ 0, 1 ], [ 0, 2 ],
              [ 0, 3 ], [ 1, 4 ],
              [ 1, 5 ], [ 3, 6 ] ]

    # Function call
    countCC(N, Q, Queries, Edges)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

static readonly int MAX  = 100005;

// Stores degree of the nodes
static int []degree = new int[MAX];

// Function that finds the degree of
// each node in the given graph
static void DegreeOfNodes(int [,]Edges,
                          int N)
{
  // Precompute degrees of each node
  for (int i = 0; i < N - 1; i++)
  {
    degree[Edges[i, 0]]++;
    degree[Edges[i, 1]]++;
  }
}

// Function to print the number of
// connected components
static void findConnectedComponents(int x)
{
  // Print the degree of node x
  Console.Write(degree[x] + " ");
}

// Function that counts the connected
// components after removing a vertex
// for each query
static void countCC(int N, int Q,
                    int []Queries,
                    int [,]Edges)
{
  // Count degree of each node
  DegreeOfNodes(Edges, N);

  // Iterate over each query
  for (int i = 0; i < Q; i++)
  {
    // Find connected components
    // after removing given vertex
    findConnectedComponents(Queries[i]);
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given N nodes and Q queries
  int N = 7, Q = 3;

  // Given array of queries
  int []Queries = {0, 1, 6};

  // Given Edges
  int [,]Edges = {{0, 1}, {0, 2},
                  {0, 3}, {1, 4},
                  {1, 5}, {3, 6}};

  // Function Call
  countCC(N, Q, Queries, Edges);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach
var MAX = 100005

// Stores degree of the nodes
var degree = Array(MAX).fill(0)

// Function that finds the degree of
// each node in the given graph
function DegreeOfNodes(Edges, N)
{
    // Precompute degrees of each node
    for (var i = 0; i < N - 1; i++) {
        degree[Edges[i][0]]++;
        degree[Edges[i][1]]++;
    }
}

// Function to print the number of
// connected components
function findConnectedComponents(x)
{
    // Print the degree of node x
    document.write( degree[x] + ' ');
}

// Function that counts the connected
// components after removing a vertex
// for each query
function countCC(N, Q, Queries, Edges)
{

    // Count degree of each node
    DegreeOfNodes(Edges, N);

    // Iterate over each query
    for (var i = 0; i < Q; i++) {

        // Find connected components
        // after removing given vertex
        findConnectedComponents(Queries[i]);
    }
}

// Driver Code
// Given N nodes and Q queries
var N = 7, Q = 3;
// Given array of queries
var Queries = [ 0, 1, 6 ];
// Given Edges
var Edges = [ [ 0, 1 ], [ 0, 2 ],
                   [ 0, 3 ], [ 1, 4 ],
                   [ 1, 5 ], [ 3, 6 ] ];
// Function Call
countCC(N, Q, Queries, Edges);

</script>
```

**Output:** 

```
3 3 1
```

***时间复杂度:** O(E + Q)，其中 E 为边数(E = N–1)，Q 为查询数。*
***辅助空间:** O(V)，其中 V 为顶点数。*