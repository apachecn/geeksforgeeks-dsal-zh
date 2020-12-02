# 无向图

中奇数和偶数度节点的度数之和之间的差

> 原文： [https://www.geeksforgeeks.org/difference-between-sum-of-degrees-of-odd-and-even-degree-nodes-in-an-undirected-graph/](https://www.geeksforgeeks.org/difference-between-sum-of-degrees-of-odd-and-even-degree-nodes-in-an-undirected-graph/)

给定[无向图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，其中 **N 个**顶点且 **M 个**边，任务是找到奇数度节点和偶度度节点的度和之间的绝对差 在无向图中。
**范例**：

> **输入**：N = 4，边缘[] [] = {{1，2}，{1，3}，{1，4}，{2，3}，{2，4}，{ 3，4}}
> **输出**：12
> **说明**：
> 下图是上述信息的图形：
> 
> ![](img/86b8bf5ee84a0057344218ba88219df0.png)
> 
> 节点->度
> 1-> 3
> 2-> 3
> 3-> 3
> 4-> 3
> 奇数度节点的总和= 3 + 3 + 3 + 3 = 12
> 偶数度节点的总和= 0
> 差= 12
> **输入**：N = 5，edges [] [] = {{1，2 }，{1，3}，{2，4}，{2，5}}}
> **输出**：4

**方法**：

1.  对于每个顶点，度可以通过给定图形在相应顶点处的 [](https://www.geeksforgeeks.org/convert-adjacency-matrix-to-adjacency-list-representation-of-graph/) ，[邻接表](https://www.geeksforgeeks.org/convert-adjacency-matrix-to-adjacency-list-representation-of-graph/)的长度来计算。
2.  计算奇数度节点和偶数度节点的度数之和，然后打印出差异。

下面是上述方法的实现：

## C ++

```

// C++ implementation to print the
// Difference Between sum of degrees
// of odd degree nodes and even 
// degree nodes.
#include <bits/stdc++.h>
using namespace std;

// Function to print the difference
// Between sum of degrees of odd
// degree nodes and even degree nodes.
int OddEvenDegree(int N, int M,
                    int edges[][2])
{
    // To store Adjacency List of
    // a Graph
    vector<int> Adj[N + 1];

    int EvenSum = 0;
    int OddSum = 0;

    // Make Adjacency List
    for (int i = 0 ; i < M ; i++) {
        int x = edges[i][0];
        int y = edges[i][1];

        Adj[x].push_back(y);
        Adj[y].push_back(x);
    }

    // Traverse each vertex
    for (int i = 1; i <= N; i++) {

        // Find size of Adjacency List
        int x = Adj[i].size();

        // If length of Adj[i] is
        // an odd number, add
        // length in OddSum
        if (x % 2 != 0)
        {
            OddSum += x;
        }
        else
        {
            // If length of Adj[i] is
            // an even number, add 
            // length in EvenSum
            EvenSum += x;
        }

    }

    return abs(OddSum - EvenSum);
}

// Driver code
int main()
{
    // Vertices and Edges
    int N = 4, M = 6;

    // Edges
    int edges[M][2] = { { 1, 2 }, { 1, 3 }, { 1, 4 },
                       { 2, 3 }, { 2, 4 }, { 3, 4 } };

    // Function Call
    cout<< OddEvenDegree(N, M, edges);

    return 0;
}

```

## 爪哇

```

// Java implementation to print the
// difference between sum of degrees
// of odd degree nodes and even 
// degree nodes.
import java.util.*;

class GFG{

// Function to print the difference
// between sum of degrees of odd
// degree nodes and even degree nodes.
static int OddEvenDegree(int N, int M,
                         int edges[][])
{

    // To store adjacency list 
    // of a graph
    @SuppressWarnings("unchecked")
    Vector<Integer> []Adj = new Vector[N + 1];

    for(int i = 0; i < N + 1; i++)
    {
       Adj[i] = new Vector<Integer>();
    }

    int EvenSum = 0;
    int OddSum = 0;

    // Make adjacency list
    for(int i = 0; i < M; i++)
    {
       int x = edges[i][0];
       int y = edges[i][1];

       Adj[x].add(y);
       Adj[y].add(x);
    }

    // Traverse each vertex
    for(int i = 1; i <= N; i++)
    {

       // Find size of adjacency list
       int x = Adj[i].size();

       // If length of Adj[i] is
       // an odd number, add
       // length in OddSum
       if (x % 2 != 0)
       {
           OddSum += x;
       }
       else
       {

           // If length of Adj[i] is
           // an even number, add 
           // length in EvenSum
           EvenSum += x;
       }
    }
    return Math.abs(OddSum - EvenSum);
}

// Driver code
public static void main(String[] args)
{

    // Vertices and edges
    int N = 4, M = 6;

    // Edges
    int edges[][] = { { 1, 2 }, { 1, 3 }, { 1, 4 },
                      { 2, 3 }, { 2, 4 }, { 3, 4 } };

    // Function call
    System.out.print(OddEvenDegree(N, M, edges));
}
}

// This code is contributed by PrinciRaj1992

```

## Python3

```

# Python3 implementation to print the
# Difference Between sum of degrees
# of odd degree nodes and even 
# degree nodes.

# Function to print the difference
# Between sum of degrees of odd
# degree nodes and even degree nodes.
def OddEvenDegree(N, M, edges):

    # To store Adjacency 
    # List of a Graph
    Adj = [[] for i in range(N + 1)]

    EvenSum = 0;
    OddSum = 0;

    # Make Adjacency List
    for i in range(M):
        x = edges[i][0];
        y = edges[i][1];

        Adj[x].append(y);
        Adj[y].append(x);

    # Traverse each vertex
    for i in range(1, N + 1):

        # Find size of 
        # Adjacency List
        x = len(Adj[i])

        # If length of Adj[i] is
        # an odd number, add
        # length in OddSum
        if (x % 2 != 0):
            OddSum += x;        
        else:

            # If length of Adj[i] is
            # an even number, add 
            # length in EvenSum
            EvenSum += x;        

    return abs(OddSum - EvenSum);

# Driver code
if __name__ == "__main__":

    # Vertices and Edges
    N = 4
    M = 6

    # Edges
    edges = [[1, 2], [1, 3], 
             [1, 4], [2, 3], 
             [2, 4], [3, 4]]

    # Function Call
    print(OddEvenDegree(N, M, 
                        edges));

# This code is contributed by rutvik_56

```

## C＃

```

// C# implementation to print the
// difference between sum of degrees
// of odd degree nodes and even 
// degree nodes.
using System;
using System.Collections.Generic;
class GFG{

// Function to print the difference
// between sum of degrees of odd
// degree nodes and even degree nodes.
static int OddEvenDegree(int N, int M,
                         int [,]edges)
{
  // To store adjacency list 
  // of a graph
  List<int> []Adj = new List<int>[N + 1];

  for(int i = 0; i < N + 1; i++)
  {
    Adj[i] = new List<int>();
  }

  int EvenSum = 0;
  int OddSum = 0;

  // Make adjacency list
  for(int i = 0; i < M; i++)
  {
    int x = edges[i, 0];
    int y = edges[i, 1];

    Adj[x].Add(y);
    Adj[y].Add(x);
  }

  // Traverse each vertex
  for(int i = 1; i <= N; i++)
  {
    // Find size of adjacency list
    int x = Adj[i].Count;

    // If length of Adj[i] is
    // an odd number, add
    // length in OddSum
    if (x % 2 != 0)
    {
      OddSum += x;
    }
    else
    {
      // If length of Adj[i] is
      // an even number, add 
      // length in EvenSum
      EvenSum += x;
    }
  }
  return Math.Abs(OddSum - EvenSum);
}

// Driver code
public static void Main(String[] args)
{
  // Vertices and edges
  int N = 4, M = 6;

  // Edges
  int [,]edges = {{1, 2}, {1, 3}, {1, 4},
                  {2, 3}, {2, 4}, {3, 4}};

  // Function call
  Console.Write(OddEvenDegree(N, M, edges));
}
}

// This code is contributed by Princi Singh

```

**Output:** 

```
12

```

[![competitive-programming-img](img/5211864e7e7a28eeeb039fa5d6073a24.png)](https://practice.geeksforgeeks.org/courses/competitive-programming-live?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_cp)

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。