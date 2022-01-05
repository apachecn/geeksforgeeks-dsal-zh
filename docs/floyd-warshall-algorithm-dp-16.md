# 弗洛伊德·沃肖尔算法| DP-16

> 原文:[https://www . geesforgeks . org/Floyd-war shall-algorithm-DP-16/](https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/)

[弗洛伊德·沃肖尔算法](http://en.wikipedia.org/wiki/Floyd%E2%80%93Warshall_algorithm)用于求解所有对最短路径问题。问题是寻找给定边加权有向图中每对顶点之间的最短距离。
T3】例:

```
Input:
       graph[][] = { {0,   5,  INF, 10},
                    {INF,  0,  3,  INF},
                    {INF, INF, 0,   1},
                    {INF, INF, INF, 0} }
which represents the following graph
             10
       (0)------->(3)
        |         /|\
      5 |          |
        |          | 1
       \|/         |
       (1)------->(2)
            3       
Note that the value of graph[i][j] is 0 if i is equal to j 
And graph[i][j] is INF (infinite) if there is no edge from vertex i to j.

Output:
Shortest distance matrix
      0      5      8      9
    INF      0      3      4
    INF    INF      0      1
    INF    INF    INF      0
```

**弗洛伊德·沃肖尔算法**
我们初始化解矩阵的第一步与输入图矩阵相同。然后，我们通过将所有顶点视为中间顶点来更新解矩阵。其思想是一个接一个地拾取所有顶点，并更新所有最短路径，其中包括拾取的顶点作为最短路径中的中间顶点。当我们选取顶点数 k 作为中间顶点时，我们已经考虑了顶点{0，1，2，..k-1}作为中间顶点。对于源顶点和目标顶点的每一对(I，j)，都有两种可能的情况。
**1)** k 在从 I 到 j 的最短路径中不是中间顶点，我们保持 dist[i][j]的值不变。
**2)** k 是从 I 到 j 的最短路径中的中间顶点，我们将 dist[i][j]的值更新为 dist[I][k]+dist[k][j]if dist[I][j]>dist[I][k]+dist[k][j]
下图显示了以上全对最短路径问题中的最优子结构性质。

![Floyd Warshall Algorithm](img/957485506abad8275ceb037ee2a55849.png)

以下是弗洛伊德·沃肖尔算法的实现。

## C++

```
// C++ Program for Floyd Warshall Algorithm
#include <bits/stdc++.h>
using namespace std;

// Number of vertices in the graph
#define V 4

/* Define Infinite as a large enough
value.This value will be used for
vertices not connected to each other */
#define INF 99999

// A function to print the solution matrix
void printSolution(int dist[][V]);

// Solves the all-pairs shortest path
// problem using Floyd Warshall algorithm
void floydWarshall(int graph[][V])
{
    /* dist[][] will be the output matrix
    that will finally have the shortest
    distances between every pair of vertices */
    int dist[V][V], i, j, k;

    /* Initialize the solution matrix same
    as input graph matrix. Or we can say
    the initial values of shortest distances
    are based on shortest paths considering
    no intermediate vertex. */
    for (i = 0; i < V; i++)
        for (j = 0; j < V; j++)
            dist[i][j] = graph[i][j];

    /* Add all vertices one by one to
    the set of intermediate vertices.
    ---> Before start of an iteration,
    we have shortest distances between all
    pairs of vertices such that the
    shortest distances consider only the
    vertices in set {0, 1, 2, .. k-1} as
    intermediate vertices.
    ----> After the end of an iteration,
    vertex no. k is added to the set of
    intermediate vertices and the set becomes {0, 1, 2, ..
    k} */
    for (k = 0; k < V; k++) {
        // Pick all vertices as source one by one
        for (i = 0; i < V; i++) {
            // Pick all vertices as destination for the
            // above picked source
            for (j = 0; j < V; j++) {
                // If vertex k is on the shortest path from
                // i to j, then update the value of
                // dist[i][j]
                if (dist[i][j] > (dist[i][k] + dist[k][j])
                    && (dist[k][j] != INF
                        && dist[i][k] != INF))
                    dist[i][j] = dist[i][k] + dist[k][j];
            }
        }
    }

    // Print the shortest distance matrix
    printSolution(dist);
}

/* A utility function to print solution */
void printSolution(int dist[][V])
{
    cout << "The following matrix shows the shortest "
            "distances"
            " between every pair of vertices \n";
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            if (dist[i][j] == INF)
                cout << "INF"
                     << "     ";
            else
                cout << dist[i][j] << "     ";
        }
        cout << endl;
    }
}

// Driver code
int main()
{
    /* Let us create the following weighted graph
            10
    (0)------->(3)
        |     /|\
    5 |     |
        |     | 1
    \|/     |
    (1)------->(2)
            3     */
    int graph[V][V] = { { 0, 5, INF, 10 },
                        { INF, 0, 3, INF },
                        { INF, INF, 0, 1 },
                        { INF, INF, INF, 0 } };

    // Print the solution
    floydWarshall(graph);
    return 0;
}

// This code is contributed by Mythri J L
```

## C

```
// C Program for Floyd Warshall Algorithm
#include<stdio.h>

// Number of vertices in the graph
#define V 4

/* Define Infinite as a large enough 
  value. This value will be used
  for vertices not connected to each other */
#define INF 99999

// A function to print the solution matrix
void printSolution(int dist[][V]);

// Solves the all-pairs shortest path 
// problem using Floyd Warshall algorithm
void floydWarshall (int graph[][V])
{
    /* dist[][] will be the output matrix 
      that will finally have the shortest 
      distances between every pair of vertices */
    int dist[V][V], i, j, k;

    /* Initialize the solution matrix 
      same as input graph matrix. Or 
       we can say the initial values of 
       shortest distances are based
       on shortest paths considering no 
       intermediate vertex. */
    for (i = 0; i < V; i++)
        for (j = 0; j < V; j++)
            dist[i][j] = graph[i][j];

    /* Add all vertices one by one to 
      the set of intermediate vertices.
      ---> Before start of an iteration, we 
      have shortest distances between all
      pairs of vertices such that the shortest 
      distances consider only the
      vertices in set {0, 1, 2, .. k-1} as 
      intermediate vertices.
      ----> After the end of an iteration, 
      vertex no. k is added to the set of
      intermediate vertices and the set 
      becomes {0, 1, 2, .. k} */
    for (k = 0; k < V; k++)
    {
        // Pick all vertices as source one by one
        for (i = 0; i < V; i++)
        {
            // Pick all vertices as destination for the
            // above picked source
            for (j = 0; j < V; j++)
            {
                // If vertex k is on the shortest path from
                // i to j, then update the value of dist[i][j]
                if (dist[i][k] + dist[k][j] < dist[i][j])
                    dist[i][j] = dist[i][k] + dist[k][j];
            }
        }
    }

    // Print the shortest distance matrix
    printSolution(dist);
}

/* A utility function to print solution */
void printSolution(int dist[][V])
{
    printf ("The following matrix shows the shortest distances"
            " between every pair of vertices \n");
    for (int i = 0; i < V; i++)
    {
        for (int j = 0; j < V; j++)
        {
            if (dist[i][j] == INF)
                printf("%7s", "INF");
            else
                printf ("%7d", dist[i][j]);
        }
        printf("\n");
    }
}

// driver program to test above function
int main()
{
    /* Let us create the following weighted graph
            10
       (0)------->(3)
        |         /|\
      5 |          |
        |          | 1
       \|/         |
       (1)------->(2)
            3           */
    int graph[V][V] = { {0,   5,  INF, 10},
                        {INF, 0,   3, INF},
                        {INF, INF, 0,   1},
                        {INF, INF, INF, 0}
                      };

    // Print the solution
    floydWarshall(graph);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program for Floyd Warshall All Pairs Shortest
// Path algorithm.
import java.util.*;
import java.lang.*;
import java.io.*;

class AllPairShortestPath
{
    final static int INF = 99999, V = 4;

    void floydWarshall(int graph[][])
    {
        int dist[][] = new int[V][V];
        int i, j, k;

        /* Initialize the solution matrix 
           same as input graph matrix.
           Or we can say the initial values 
           of shortest distances
           are based on shortest paths 
           considering no intermediate
           vertex. */
        for (i = 0; i < V; i++)
            for (j = 0; j < V; j++)
                dist[i][j] = graph[i][j];

        /* Add all vertices one by one 
           to the set of intermediate
           vertices.
          ---> Before start of an iteration, 
               we have shortest
               distances between all pairs 
               of vertices such that
               the shortest distances consider 
               only the vertices in
               set {0, 1, 2, .. k-1} as 
               intermediate vertices.
          ----> After the end of an iteration, 
                vertex no. k is added
                to the set of intermediate 
                vertices and the set
                becomes {0, 1, 2, .. k} */
        for (k = 0; k < V; k++)
        {
            // Pick all vertices as source one by one
            for (i = 0; i < V; i++)
            {
                // Pick all vertices as destination for the
                // above picked source
                for (j = 0; j < V; j++)
                {
                    // If vertex k is on the shortest path from
                    // i to j, then update the value of dist[i][j]
                    if (dist[i][k] + dist[k][j] < dist[i][j])
                        dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }

        // Print the shortest distance matrix
        printSolution(dist);
    }

    void printSolution(int dist[][])
    {
        System.out.println("The following matrix shows the shortest "+
                         "distances between every pair of vertices");
        for (int i=0; i<V; ++i)
        {
            for (int j=0; j<V; ++j)
            {
                if (dist[i][j]==INF)
                    System.out.print("INF ");
                else
                    System.out.print(dist[i][j]+"   ");
            }
            System.out.println();
        }
    }

    // Driver program to test above function
    public static void main (String[] args)
    {
        /* Let us create the following weighted graph
           10
        (0)------->(3)
        |         /|\
        5 |          |
        |          | 1
        \|/         |
        (1)------->(2)
           3           */
        int graph[][] = { {0,   5,  INF, 10},
                          {INF, 0,   3, INF},
                          {INF, INF, 0,   1},
                          {INF, INF, INF, 0}
                        };
        AllPairShortestPath a = new AllPairShortestPath();

        // Print the solution
        a.floydWarshall(graph);
    }
}

// Contributed by Aakash Hasija
```

## 计算机编程语言

```
# Python Program for Floyd Warshall Algorithm

# Number of vertices in the graph
V = 4

# Define infinity as the large 
# enough value. This value will be
# used for vertices not connected to each other
INF = 99999

# Solves all pair shortest path 
# via Floyd Warshall Algorithm

def floydWarshall(graph):

    """ dist[][] will be the output 
       matrix that will finally
        have the shortest distances 
        between every pair of vertices """
    """ initializing the solution matrix 
    same as input graph matrix
    OR we can say that the initial 
    values of shortest distances
    are based on shortest paths considering no 
    intermediate vertices """

    dist = list(map(lambda i: list(map(lambda j: j, i)), graph))

    """ Add all vertices one by one 
    to the set of intermediate
     vertices.
     ---> Before start of an iteration, 
     we have shortest distances
     between all pairs of vertices 
     such that the shortest
     distances consider only the 
     vertices in the set 
    {0, 1, 2, .. k-1} as intermediate vertices.
      ----> After the end of a 
      iteration, vertex no. k is
     added to the set of intermediate 
     vertices and the 
    set becomes {0, 1, 2, .. k}
    """
    for k in range(V):

        # pick all vertices as source one by one
        for i in range(V):

            # Pick all vertices as destination for the
            # above picked source
            for j in range(V):

                # If vertex k is on the shortest path from
                # i to j, then update the value of dist[i][j]
                dist[i][j] = min(dist[i][j],
                                 dist[i][k] + dist[k][j]
                                 )
    printSolution(dist)

# A utility function to print the solution
def printSolution(dist):
    print "Following matrix shows the shortest distances\
 between every pair of vertices"
    for i in range(V):
        for j in range(V):
            if(dist[i][j] == INF):
                print "%7s" % ("INF"),
            else:
                print "%7d\t" % (dist[i][j]),
            if j == V-1:
                print ""

# Driver program to test the above program
# Let us create the following weighted graph
"""
            10
       (0)------->(3)
        |         /|\
      5 |          |
        |          | 1
       \|/         |
       (1)------->(2)
            3           """
graph = [[0, 5, INF, 10],
         [INF, 0, 3, INF],
         [INF, INF, 0,   1],
         [INF, INF, INF, 0]
         ]
# Print the solution
floydWarshall(graph)
# This code is contributed by Mythri J L
```

## C#

```
// A C# program for Floyd Warshall All 
// Pairs Shortest Path algorithm.

using System;

public class AllPairShortestPath
{
    readonly static int INF = 99999, V = 4;

    void floydWarshall(int[,] graph)
    {
        int[,] dist = new int[V, V];
        int i, j, k;

        // Initialize the solution matrix 
        // same as input graph matrix
        // Or we can say the initial 
        // values of shortest distances
        // are based on shortest paths 
        // considering no intermediate
        // vertex
        for (i = 0; i < V; i++) {
            for (j = 0; j < V; j++) {
                dist[i, j] = graph[i, j];
            }
        }

        /* Add all vertices one by one to 
        the set of intermediate vertices.
        ---> Before start of a iteration,
             we have shortest distances
             between all pairs of vertices
             such that the shortest distances
             consider only the vertices in
             set {0, 1, 2, .. k-1} as 
             intermediate vertices.
        ---> After the end of a iteration, 
             vertex no. k is added
             to the set of intermediate
             vertices and the set
             becomes {0, 1, 2, .. k} */
        for (k = 0; k < V; k++)
        {
            // Pick all vertices as source
            // one by one
            for (i = 0; i < V; i++)
            {
                // Pick all vertices as destination
                // for the above picked source
                for (j = 0; j < V; j++)
                {
                    // If vertex k is on the shortest
                    // path from i to j, then update
                    // the value of dist[i][j]
                    if (dist[i, k] + dist[k, j] < dist[i, j]) 
                    {
                        dist[i, j] = dist[i, k] + dist[k, j];
                    }
                }
            }
        }

        // Print the shortest distance matrix
        printSolution(dist);
    }

    void printSolution(int[,] dist)
    {
        Console.WriteLine("Following matrix shows the shortest "+
                        "distances between every pair of vertices");
        for (int i = 0; i < V; ++i)
        {
            for (int j = 0; j < V; ++j)
            {
                if (dist[i, j] == INF) {
                    Console.Write("INF ");
                } else {
                    Console.Write(dist[i, j] + " ");
                }
            }

            Console.WriteLine();
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        /* Let us create the following
           weighted graph
              10
        (0)------->(3)
        |         /|\
        5 |         |
        |         | 1
        \|/         |
        (1)------->(2)
             3             */
        int[,] graph = { {0, 5, INF, 10},
                        {INF, 0, 3, INF},
                        {INF, INF, 0, 1},
                        {INF, INF, INF, 0}
                        };

        AllPairShortestPath a = new AllPairShortestPath();

        // Print the solution
        a.floydWarshall(graph);
    }
}

// This article is contributed by 
// Abdul Mateen Mohammed
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program for Floyd Warshall Algorithm 

// Solves the all-pairs shortest path problem
// using Floyd Warshall algorithm 
function floydWarshall ($graph, $V, $INF) 
{ 
    /* dist[][] will be the output matrix 
    that will finally have the shortest 
    distances between every pair of vertices */
    $dist = array(array(0,0,0,0),
                  array(0,0,0,0),
                  array(0,0,0,0),
                  array(0,0,0,0));

    /* Initialize the solution matrix same 
    as input graph matrix. Or we can say the 
    initial values of shortest distances are 
    based on shortest paths considering no 
    intermediate vertex. */
    for ($i = 0; $i < $V; $i++) 
        for ($j = 0; $j < $V; $j++) 
            $dist[$i][$j] = $graph[$i][$j]; 

    /* Add all vertices one by one to the set 
    of intermediate vertices. 
    ---> Before start of an iteration, we have 
    shortest distances between all pairs of 
    vertices such that the shortest distances 
    consider only the vertices in set 
    {0, 1, 2, .. k-1} as intermediate vertices. 
    ----> After the end of an iteration, vertex 
    no. k is added to the set of intermediate
    vertices and the set becomes {0, 1, 2, .. k} */
    for ($k = 0; $k < $V; $k++) 
    { 
        // Pick all vertices as source one by one 
        for ($i = 0; $i < $V; $i++) 
        { 
            // Pick all vertices as destination 
            // for the above picked source 
            for ($j = 0; $j < $V; $j++) 
            { 
                // If vertex k is on the shortest path from 
                // i to j, then update the value of dist[i][j] 
                if ($dist[$i][$k] + $dist[$k][$j] < 
                                    $dist[$i][$j]) 
                    $dist[$i][$j] = $dist[$i][$k] +
                                    $dist[$k][$j]; 
            } 
        } 
    } 

    // Print the shortest distance matrix 
    printSolution($dist, $V, $INF); 
} 

/* A utility function to print solution */
function printSolution($dist, $V, $INF) 
{ 
    echo "The following matrix shows the " .
             "shortest distances between " . 
                "every pair of vertices \n"; 
    for ($i = 0; $i < $V; $i++) 
    { 
        for ($j = 0; $j < $V; $j++) 
        { 
            if ($dist[$i][$j] == $INF) 
                echo "INF " ; 
            else
                echo $dist[$i][$j], " ";
        } 
        echo "\n"; 
    } 
} 

// Driver Code

// Number of vertices in the graph 
$V = 4 ;

/* Define Infinite as a large enough 
value. This value will be used for
vertices not connected to each other */
$INF = 99999 ;

/* Let us create the following weighted graph 
        10 
(0)------->(3) 
    |     /|\ 
5 |     | 
    |     | 1 
\|/     | 
(1)------->(2) 
        3     */
$graph = array(array(0, 5, $INF, 10), 
               array($INF, 0, 3, $INF), 
               array($INF, $INF, 0, 1), 
               array($INF, $INF, $INF, 0)); 

// Print the solution 
floydWarshall($graph, $V, $INF); 

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
      // A JavaScript program for Floyd Warshall All
      // Pairs Shortest Path algorithm.

      var INF = 99999;
      class AllPairShortestPath {
        constructor() {
          this.V = 4;
        }

        floydWarshall(graph) {
          var dist = Array.from(Array(this.V), () => new Array(this.V).fill(0));
          var i, j, k;

          // Initialize the solution matrix
          // same as input graph matrix
          // Or we can say the initial
          // values of shortest distances
          // are based on shortest paths
          // considering no intermediate
          // vertex
          for (i = 0; i < this.V; i++) {
            for (j = 0; j < this.V; j++) {
              dist[i][j] = graph[i][j];
            }
          }

          /* Add all vertices one by one to
        the set of intermediate vertices.
        ---> Before start of a iteration,
            we have shortest distances
            between all pairs of vertices
            such that the shortest distances
            consider only the vertices in
            set {0, 1, 2, .. k-1} as
            intermediate vertices.
        ---> After the end of a iteration,
            vertex no. k is added
            to the set of intermediate
            vertices and the set
            becomes {0, 1, 2, .. k} */
          for (k = 0; k < this.V; k++) {
            // Pick all vertices as source
            // one by one
            for (i = 0; i < this.V; i++) {
              // Pick all vertices as destination
              // for the above picked source
              for (j = 0; j < this.V; j++) {
                // If vertex k is on the shortest
                // path from i to j, then update
                // the value of dist[i][j]
                if (dist[i][k] + dist[k][j] < dist[i][j]) {
                  dist[i][j] = dist[i][k] + dist[k][j];
                }
              }
            }
          }

          // Print the shortest distance matrix
          this.printSolution(dist);
        }

        printSolution(dist) {
          document.write(
            "Following matrix shows the shortest " +
              "distances between every pair of vertices<br>"
          );
          for (var i = 0; i < this.V; ++i) {
            for (var j = 0; j < this.V; ++j) {
              if (dist[i][j] == INF) {
                document.write(" INF ");
              } else {
                document.write("  " + dist[i][j] + " ");
              }
            }

            document.write("<br>");
          }
        }
      }
      // Driver Code
      /* Let us create the following
        weighted graph
            10
        (0)------->(3)
        |         /|\
        5 |         |
        |         | 1
        \|/         |
        (1)------->(2)
            3             */
      var graph = [
        [0, 5, INF, 10],
        [INF, 0, 3, INF],
        [INF, INF, 0, 1],
        [INF, INF, INF, 0],
      ];

      var a = new AllPairShortestPath();

      // Print the solution
      a.floydWarshall(graph);

      // This code is contributed by rdtaank.
    </script>
```

**输出:**

```
Following matrix shows the shortest distances between every pair of vertices
      0      5      8      9
    INF      0      3      4
    INF    INF      0      1
    INF    INF    INF      0
```

**时间复杂度:** O(V^3)
上面的程序只打印最短的距离。我们还可以通过将前置信息存储在单独的 2D 矩阵中来修改解决方案以打印最短路径。
同样，INF 的值可以从 limits.h 取为 INT_MAX，以确保我们处理最大可能值。当我们取 INF 为 INT_MAX 时，需要改变上述程序中的 if 条件，以避免算术溢出。

```
#include 

#define INF INT_MAX
..........................
if ( dist[i][k] != INF && 
     dist[k][j] != INF && 
     dist[i][k] + dist[k][j] < dist[i][j]
    )
 dist[i][j] = dist[i][k] + dist[k][j];
...........................
```

如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论