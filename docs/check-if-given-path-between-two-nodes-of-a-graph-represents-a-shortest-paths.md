# 检查图的两个节点之间的给定路径是否代表最短路径

> 原文:[https://www . geesforgeks . org/check-如果给定路径在图的两个节点之间，则表示最短路径/](https://www.geeksforgeeks.org/check-if-given-path-between-two-nodes-of-a-graph-represents-a-shortest-paths/)

给定一个未加权的有向图和由图的两个节点之间的遍历序列组成的 **Q** 查询，任务是找出这些序列是否代表两个节点之间的最短路径之一。
**例:**

```
Input: 1 2 3 4
Output: NO
```

![](img/84fe33c97f761ade6f4718bc9959199f.png)

```
Explanation:
The first and last node of the input sequence 
is 1 and 4 respectively. The shortest path 
between 1 and 4 is 1 -> 3 -> 4 hence, 
the output is NO for the 1st example.

Input: 1 3 4
Output: YES
```

**方法:**
想法是使用**弗洛伊德·沃肖尔算法**来存储所有顶点对的长度。如果序列的开始和结束节点之间的最短路径的长度比序列的长度少一个，那么给定的序列代表节点之间的最短路径之一。
以下是上述方法的实施:

## C++

```
// C++ program for
// the above approach
#include <bits/stdc++.h>
using namespace std;
#define INFINITE 10000

// Function to store the
// length of shortest path
// between all pairs of nodes
void shortestPathLength(int n, int graph[4][4], int dis[4][4])
{
  // Initializing dis matrix
  // with current distance value 
  for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
          dis[i][j] = graph[i][j];
      }
  }

  // Floyd-Warshall Algorithm
  for (int k = 0; k < n; k++) {
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < n; j++) {
          dis[i][j] = min(dis[i][j], dis[i][k] + dis[k][j]);
      }
    }
  }
}

// A function that prints YES if the
// given path is the shortest path
// and prints NO if the given path
// is not shortest
void checkShortestPath(int length, int path[], int dis[4][4])
{
  // Check if the given path
  // is shortest or not
  // as discussed in above approach
  if (dis[path[0] - 1][path[length - 1] - 1] == length - 1) {
      cout << "YES" << endl;
  }
  else {
      cout << "NO" << endl;
  }
}

// Driver code
int main()
{
    // Adjacency matrix representing the graph
    const int n = 4;
    int graph[n][n] = { { 0, 1, 1, INFINITE },
                        { INFINITE, 0, 1, INFINITE },
                        { INFINITE, INFINITE, 0, 1 },
                        { 1, INFINITE, INFINITE, 0 } };
    // A matrix to store the length of shortest
    int dis[n][n];

    // path between all pairs of vertices
    shortestPathLength(n, graph, dis);

    int path1[] = { 1, 2, 3, 4 };
    checkShortestPath(n, path1, dis);

    int path2[] = { 1, 3, 4 };
    checkShortestPath(3, path2, dis);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{
static int INFINITE = 10000;

// Function to store the
// length of shortest path
// between all pairs of nodes
static void shortestPathLength(int n, int graph[][],
                                      int dis[][])
{
    // Initializing dis matrix
    // with current distance value
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            dis[i][j] = graph[i][j];
        }
    }

    // Floyd-Warshall Algorithm
    for (int k = 0; k < n; k++)
    {
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                dis[i][j] = Math.min(dis[i][j],
                                     dis[i][k] +
                                     dis[k][j]);
            }
        }
    }
}

// A function that prints YES if the
// given path is the shortest path
// and prints NO if the given path
// is not shortest
static void checkShortestPath(int length,
                              int path[],
                              int dis[][])
{
    // Check if the given path
    // is shortest or not
    // as discussed in above approach
    if (dis[path[0] - 1][path[length - 1] - 1] == length - 1)
    {
        System.out.println("YES");
    }
    else
    {
        System.out.println("NO");
    }
}

// Driver code
public static void main(String[] args)
{
    // Adjacency matrix representing the graph
    int n = 4;
    int graph[][] = { { 0, 1, 1, INFINITE },
                      { INFINITE, 0, 1, INFINITE },
                      { INFINITE, INFINITE, 0, 1 },
                      { 1, INFINITE, INFINITE, 0 } };

    // A matrix to store the length of shortest
    int [][]dis = new int[n][n];

    // path between all pairs of vertices
    shortestPathLength(n, graph, dis);

    int path1[] = { 1, 2, 3, 4 };
    checkShortestPath(n, path1, dis);

    int path2[] = { 1, 3, 4 };
    checkShortestPath(3, path2, dis);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
INFINITE = 10000

# Function to store the
# length of shortest path
# between all pairs of nodes
def shortestPathLength(n, graph, dis):

    # Initializing dis matrix
    # with current distance value
    for i in range(n):
        for j in range(n):
            dis[i][j] = graph[i][j]

    # Floyd-Warshall Algorithm
    for k in range(n):
        for i in range(n):
            for j in range(n):
                dis[i][j] = min(dis[i][j],
                    dis[i][k] + dis[k][j])

# A function that prints YES if the
# given path is the shortest path
# and prints NO if the given path
# is not shortest
def checkShortestPath(length, path, dis):

    # Check if the given path
    # is shortest or not
    # as discussed in above approach
    if (dis[path[0] - 1][path[length - 1] - 1] == length - 1):
        print("YES")
    else:
        print("NO")

# Driver code

# Adjacency matrix representing the graph
n = 4
graph = [[ 0, 1, 1, INFINITE],
         [INFINITE, 0, 1, INFINITE],
         [INFINITE, INFINITE, 0, 1],
         [1, INFINITE, INFINITE, 0]]

# A matrix to store the length of shortest
dis = [[0 for i in range(n)]
          for i in range(n)]

# path between all pairs of vertices
shortestPathLength(n, graph, dis)

path1 = [1, 2, 3, 4]
checkShortestPath(n, path1, dis)

path2 = [1, 3, 4]
checkShortestPath(3, path2, dis)

# This code is contributed Mohit Kumar
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

static int INFINITE = 10000;

// Function to store the
//.Length of shortest path
// between all pairs of nodes
static void shortestPathLength(int n, int [,]graph,
                                    int [,]dis)
{
    // Initializing dis matrix
    // with current distance value
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            dis[i, j] = graph[i, j];
        }
    }

    // Floyd-Warshall Algorithm
    for (int k = 0; k < n; k++)
    {
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                dis[i, j] = Math.Min(dis[i, j],
                                    dis[i, k] +
                                    dis[k, j]);
            }
        }
    }
}

// A function that prints YES if the
// given path is the shortest path
// and prints NO if the given path
// is not shortest
static void checkShortestPath(int length,
                            int []path,
                            int [,]dis)
{
    // Check if the given path
    // is shortest or not
    // as discussed in above approach
    if (dis[path[0] - 1, path[length - 1] - 1] == length - 1)
    {
        Console.WriteLine("YES");
    }
    else
    {
        Console.WriteLine("NO");
    }
}

// Driver code
public static void Main(String[] args)
{
    // Adjacency matrix representing the graph
    int n = 4;
    int [,]graph = { { 0, 1, 1, INFINITE },
                    { INFINITE, 0, 1, INFINITE },
                    { INFINITE, INFINITE, 0, 1 },
                    { 1, INFINITE, INFINITE, 0 } };

    // A matrix to store the.Length of shortest
    int [,]dis = new int[n, n];

    // path between all pairs of vertices
    shortestPathLength(n, graph, dis);

    int []path1 = { 1, 2, 3, 4 };
    checkShortestPath(n, path1, dis);

    int []path2 = { 1, 3, 4 };
    checkShortestPath(3, path2, dis);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

let INFINITE = 10000;

// Function to store the
// length of shortest path
// between all pairs of nodes
function shortestPathLength(n,graph,dis)
{
    // Initializing dis matrix
    // with current distance value
    for (let i = 0; i < n; i++)
    {
        for (let j = 0; j < n; j++)
        {
            dis[i][j] = graph[i][j];
        }
    }

    // Floyd-Warshall Algorithm
    for (let k = 0; k < n; k++)
    {
        for (let i = 0; i < n; i++)
        {
            for (let j = 0; j < n; j++)
            {
                dis[i][j] = Math.min(dis[i][j],
                                     dis[i][k] +
                                     dis[k][j]);
            }
        }
    }
}

function checkShortestPath( length,path,dis)
{
    // Check if the given path
    // is shortest or not
    // as discussed in above approach
    if (dis[path[0] - 1][path[length - 1] - 1] == length - 1)
    {
        document.write("YES<br>");
    }
    else
    {
        document.write("NO<br>");
    }
}

let  n = 4;
let graph= [[ 0, 1, 1, INFINITE ],
                      [ INFINITE, 0, 1, INFINITE ],
                      [ INFINITE, INFINITE, 0, 1 ],
                      [ 1, INFINITE, INFINITE, 0 ] ];

let dis = new Array(n);
for(let i=0;i<n;i++)
{
    dis[i]=new Array(n);
    for(let j=0;j<n;j++)
    {
        dis[i][j]=0;
    }
}
// path between all pairs of vertices
shortestPathLength(n, graph, dis);

let path1 = [ 1, 2, 3, 4 ];
checkShortestPath(n, path1, dis);

let path2 = [ 1, 3, 4 ];
checkShortestPath(3, path2, dis);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
NO
YES
```

**时间复杂度:** O(V^3)