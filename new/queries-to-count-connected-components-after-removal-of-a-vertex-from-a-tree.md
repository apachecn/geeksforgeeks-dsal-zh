# 查询从树中删除顶点后对连接的组件进行计数的方法

> 原文： [https://www.geeksforgeeks.org/queries-to-count-connected-components-after-removal-of-a-vertex-from-a-tree/](https://www.geeksforgeeks.org/queries-to-count-connected-components-after-removal-of-a-vertex-from-a-tree/)

给定一个[树](https://www.geeksforgeeks.org/generic-treesn-array-trees/)，该树由**个**查询[]** 的**查询[]** 组成，它们的值分别在 **[0，N]** 范围内 Q** 个整数，由 **[0，N）**范围内的值组成。 每个查询的任务是删除值 **Q [i]** 的顶点，并计算结果图中的连接分量。

**示例**：

> **输入**：N = 7，Edges [] [2] = {{0，1}，{0，2}，{0，3}，{1，4}，{1，5}， {3，6}}，查询[] = {0，1，6}
> 
> ![](img/e52ab83d38307572f6627b99c71e0980.png)
> 
> **输出**：
> 3 3 1
> **说明**：
> **查询 1**：删除值为 0 的节点会导致边缘（ 0，1），（0，2）和（0，3）。 因此，其余图具有 3 个相连的组件：[1、4、5]，[2]，[3、6]
> **查询 2**：删除值为 1 的节点导致删除了 边（1、4），（1、5）和（1、0）。 因此，剩余图具有 3 个相连的组件：[4]，[5]，[2、0、3、6]
> **查询 3**：删除值 6 的节点将导致边的删除 （3，6）。 因此，其余图形具有 1 个相连的分量：[0、1、2、3、4、5]。
> 
> **输入**：N = 7，Edges [] [2] = {{0，1}，{0，2}，{0，3}，{1，4}，{1，5}， {3，6}}，查询[] = {5，3，2}
> 
> ![](img/e52ab83d38307572f6627b99c71e0980.png)
> 
> **输出**：1 2 1
> **说明**：
> **查询 1**：删除值 5 的节点将导致边缘（1、5 ）。 因此，其余图具有 1 个相连的分量：[0、1、2、3、4、6]
> **查询 2**：删除值 3 的节点将导致边的删除（0， 3），（3、6）。 因此，其余图具有 2 个相连的组件：[0，1，2，4，5]，[6]
> **查询 3**：删除值为 2 的节点会导致边缘（ 0，2）。 因此，其余图具有 1 个连接的分量：[0、1、3、4、5、6]

**方法**：的想法是观察在**树**中，每当删除一个节点时，连接到该节点的节点就会分离。 因此，连接组件的[计数等于已删除节点](https://www.geeksforgeeks.org/program-to-count-number-of-connected-components-in-an-undirected-graph/)的[度。
因此，方法是预先计算并在阵列中存储每个节点](https://www.geeksforgeeks.org/find-degree-particular-vertex-graph/)的[度。 对于每个查询，连接的组件数只是查询中相应节点的程度。](https://www.geeksforgeeks.org/print-the-degree-of-every-node-from-the-given-prufer-sequence/)

下面是上述方法的实现：

## C++

```cpp

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

    // Interate over each query
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

## Java

```java

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

  // Interate over each query
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

## Python

```py

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

# Function to prthe number of
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

    # Interate over each query
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

```cs

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

  // Interate over each query
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

**Output:** 

```
3 3 1

```

***时间复杂度**：O（E + Q），其中 E 是边数（E = N – 1），Q 是查询数。*
***辅助空间**：O（V），其中 V 是顶点的个数。*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。