# 图的传递闭包

> 原文:[https://www . geeksforgeeks . org/transitive-闭包-of-a-graph/](https://www.geeksforgeeks.org/transitive-closure-of-a-graph/)

给定一个有向图，对于给定图中的所有顶点对(I，j)，找出一个顶点 j 是否可以从另一个顶点 I 到达。这里的可达是指从顶点 I 到 j 有一条路径，可达矩阵称为图的传递闭包。

```
For example, consider below graph
```

![transitiveclosure](img/3d1c5c8a806e148053c9af79a3d2ec4a.png)

```
Transitive closure of above graphs is 
     1 1 1 1 
     1 1 1 1 
     1 1 1 1 
     0 0 0 1
```

图是以邻接矩阵的形式给出的，比如‘图[V][V]’，其中图[i][j]是 1，如果从顶点 I 到顶点 j 有一条边或者 I 等于 j，否则图[i][j]是 0。
[可以使用 Floyd Warshall 算法](https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/)，我们可以使用 [Floyd Warshall](https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/) 计算距离矩阵 dist[V][V]，如果 dist[i][j]是无限的，那么 j 是从 I 不可达的，否则 j 是可达的，dist[i][j]的值会小于 V.
我们可以针对这个特定的问题，不直接使用 Floyd Warshall，而是在空间和时间方面进行优化。以下是优化:

1.  我们可以创建一个布尔可达能力矩阵 reach[V][V](节省空间)，而不是 floyd warshall 中的整数结果矩阵( [dist[V][V])。如果 j 可从 I 到达，则达到[i][j]的值将为 1，否则为 0。](https://www.geeksforgeeks.org/floyd-warshall-algorithm-dp-16/)
2.  我们可以用逻辑运算代替算术运算。对于算术运算“+”，使用逻辑 and“& &”，对于 min，使用逻辑 or“| |”。(我们通过一个常数因子节省时间。时间复杂度是相同的)

下面是上述方法的实现:

## C++

```
// Program for transitive closure
// using Floyd Warshall Algorithm
#include<stdio.h>

// Number of vertices in the graph
#define V 4

// A function to print the solution matrix
void printSolution(int reach[][V]);

// Prints transitive closure of graph[][]
// using Floyd Warshall algorithm
void transitiveClosure(int graph[][V])
{
    /* reach[][] will be the output matrix
    // that will finally have the
       shortest distances between
       every pair of vertices */
    int reach[V][V], i, j, k;

    /* Initialize the solution matrix same
    as input graph matrix. Or
       we can say the initial values of
       shortest distances are based
       on shortest paths considering
       no intermediate vertex. */
    for (i = 0; i < V; i++)
        for (j = 0; j < V; j++)
            reach[i][j] = graph[i][j];

    /* Add all vertices one by one to the
    set of intermediate vertices.
      ---> Before start of a iteration,
           we have reachability values for
           all pairs of vertices such that
           the reachability values
           consider only the vertices in
           set {0, 1, 2, .. k-1} as
           intermediate vertices.
     ----> After the end of a iteration,
           vertex no. k is added to the
            set of intermediate vertices
            and the set becomes {0, 1, .. k} */
    for (k = 0; k < V; k++)
    {
        // Pick all vertices as
        // source one by one
        for (i = 0; i < V; i++)
        {
            // Pick all vertices as
            // destination for the
            // above picked source
            for (j = 0; j < V; j++)
            {
                // If vertex k is on a path
                // from i to j,
                // then make sure that the value
                // of reach[i][j] is 1
                reach[i][j] = reach[i][j] ||
                  (reach[i][k] && reach[k][j]);
            }
        }
    }

    // Print the shortest distance matrix
    printSolution(reach);
}

/* A utility function to print solution */
void printSolution(int reach[][V])
{
    printf ("Following matrix is transitive");
    printf("closure of the given graph\n");
    for (int i = 0; i < V; i++)
    {
        for (int j = 0; j < V; j++)
        {
              /* because "i==j means same vertex"
               and we can reach same vertex
               from same vertex. So, we print 1....
               and we have not considered this in
               Floyd Warshall Algo. so we need to
               make this true by ourself
               while printing transitive closure.*/
              if(i == j)
                printf("1 ");
              else
                printf ("%d ", reach[i][j]);
        }
        printf("\n");
    }
}

// Driver Code
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
    int graph[V][V] = { {1, 1, 0, 1},
                        {0, 1, 1, 0},
                        {0, 0, 1, 1},
                        {0, 0, 0, 1}
                      };

    // Print the solution
    transitiveClosure(graph);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program for transitive closure
// using Floyd Warshall Algorithm
import java.util.*;
import java.lang.*;
import java.io.*;

class GraphClosure
{
    final static int V = 4; //Number of vertices in a graph

    // Prints transitive closure of graph[][] using Floyd
    // Warshall algorithm
    void transitiveClosure(int graph[][])
    {
        /* reach[][] will be the output matrix that will finally
           have the shortest  distances between every pair of
           vertices */
        int reach[][] = new int[V][V];
        int  i, j, k;

        /* Initialize the solution matrix same as input graph
           matrix. Or  we can say the initial values of shortest
           distances are based  on shortest paths considering
           no intermediate vertex. */
        for (i = 0; i < V; i++)
            for (j = 0; j < V; j++)
                reach[i][j] = graph[i][j];

        /* Add all vertices one by one to the set of intermediate
           vertices.
          ---> Before start of a iteration, we have reachability
               values for all  pairs of vertices such that the
               reachability values consider only the vertices in
               set {0, 1, 2, .. k-1} as intermediate vertices.
          ----> After the end of a iteration, vertex no. k is
                added to the set of intermediate vertices and the
                set becomes {0, 1, 2, .. k} */
        for (k = 0; k < V; k++)
        {
            // Pick all vertices as source one by one
            for (i = 0; i < V; i++)
            {
                // Pick all vertices as destination for the
                // above picked source
                for (j = 0; j < V; j++)
                {
                    // If vertex k is on a path from i to j,
                    // then make sure that the value of reach[i][j] is 1
                    reach[i][j] = (reach[i][j]!=0) ||
                             ((reach[i][k]!=0) && (reach[k][j]!=0))?1:0;
                }
            }
        }

        // Print the shortest distance matrix
        printSolution(reach);
    }

    /* A utility function to print solution */
    void printSolution(int reach[][])
    {
        System.out.println("Following matrix is transitive closure"+
                           " of the given graph");
        for (int i = 0; i < V; i++)
        {
            for (int j = 0; j < V; j++) {
                if ( i == j)
                  System.out.print("1 ");
                else
                  System.out.print(reach[i][j]+" ");
            }
            System.out.println();
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
        /* Let us create the following weighted graph
           10
        (0)------->(3)
        |         /|\
      5 |          |
        |          | 1
        \|/        |
        (1)------->(2)
           3           */

        /* Let us create the following weighted graph

              10
         (0)------->(3)
          |         /|\
        5 |          |
          |          | 1
         \|/         |
         (1)------->(2)
            3           */
         int graph[][] = new int[][]{ {1, 1, 0, 1},
                                      {0, 1, 1, 0},
                                      {0, 0, 1, 1},
                                      {0, 0, 0, 1}
                                    };

         // Print the solution
         GraphClosure g = new GraphClosure();
         g.transitiveClosure(graph);
    }
}
// This code is contributed by Aakash Hasija
```

## 计算机编程语言

```
# Python program for transitive closure using Floyd Warshall Algorithm
#Complexity : O(V^3)

from collections import defaultdict

#Class to represent a graph
class Graph:

    def __init__(self, vertices):
        self.V = vertices

    # A utility function to print the solution
    def printSolution(self, reach):
        print ("Following matrix transitive closure of the given graph ")   
        for i in range(self.V):
            for j in range(self.V):
                if (i == j):
                  print "%7d\t" % (1),
                else:
                  print "%7d\t" %(reach[i][j]),
            print ""

    # Prints transitive closure of graph[][] using Floyd Warshall algorithm
    def transitiveClosure(self,graph):
        '''reach[][] will be the output matrix that will finally
        have reachability values.
        Initialize the solution matrix same as input graph matrix'''
        reach =[i[:] for i in graph]
        '''Add all vertices one by one to the set of intermediate
        vertices.
         ---> Before start of a iteration, we have reachability value
         for all pairs of vertices such that the reachability values
          consider only the vertices in set
        {0, 1, 2, .. k-1} as intermediate vertices.
          ----> After the end of an iteration, vertex no. k is
         added to the set of intermediate vertices and the
        set becomes {0, 1, 2, .. k}'''
        for k in range(self.V):

            # Pick all vertices as source one by one
            for i in range(self.V):

                # Pick all vertices as destination for the
                # above picked source
                for j in range(self.V):

                    # If vertex k is on a path from i to j,
                       # then make sure that the value of reach[i][j] is 1
                    reach[i][j] = reach[i][j] or (reach[i][k] and reach[k][j])

        self.printSolution(reach)

g= Graph(4)

graph = [[1, 1, 0, 1],
         [0, 1, 1, 0],
         [0, 0, 1, 1],
         [0, 0, 0, 1]]

#Print the solution
g.transitiveClosure(graph)

#This code is contributed by Neelam Yadav
```

## C#

```
// C# Program for transitive closure
// using Floyd Warshall Algorithm
using System;

class GFG
{
    static int V = 4; // Number of vertices in a graph

    // Prints transitive closure of graph[,]
    // using Floyd Warshall algorithm
    void transitiveClosure(int [,]graph)
    {
        /* reach[,] will be the output matrix that
        will finally have the shortest distances
        between every pair of vertices */
        int [,]reach = new int[V, V];
        int i, j, k;

        /* Initialize the solution matrix same as
        input graph matrix. Or we can say the
        initial values of shortest distances are
        based on shortest paths considering no
        intermediate vertex. */
        for (i = 0; i < V; i++)
            for (j = 0; j < V; j++)
                reach[i, j] = graph[i, j];

        /* Add all vertices one by one to the 
        set of intermediate vertices.
        ---> Before start of a iteration, we have
            reachability values for all pairs of
            vertices such that the reachability
            values consider only the vertices in
            set {0, 1, 2, .. k-1} as intermediate vertices.
        ---> After the end of a iteration, vertex no. 
             k is added to the set of intermediate
             vertices and the set becomes {0, 1, 2, .. k} */
        for (k = 0; k < V; k++)
        {
            // Pick all vertices as source one by one
            for (i = 0; i < V; i++)
            {
                // Pick all vertices as destination
                // for the above picked source
                for (j = 0; j < V; j++)
                {
                    // If vertex k is on a path from i to j,
                    // then make sure that the value of
                    // reach[i,j] is 1
                    reach[i, j] = (reach[i, j] != 0) ||
                                 ((reach[i, k] != 0) &&
                                  (reach[k, j] != 0)) ? 1 : 0;
                }
            }
        }

        // Print the shortest distance matrix
        printSolution(reach);
    }

    /* A utility function to print solution */
    void printSolution(int [,]reach)
    {
        Console.WriteLine("Following matrix is transitive" +
                          " closure of the given graph");
        for (int i = 0; i < V; i++)
        {
            for (int j = 0; j < V; j++){
                if (i == j)
                  Console.Write("1 ");
                else
                  Console.Write(reach[i, j] + " ");
            }
            Console.WriteLine();
        }
    }

    // Driver Code
    public static void Main (String[] args)
    {
        /* Let us create the following weighted graph
        10
        (0)------->(3)
        |     /|\
    5 |     |
        |     | 1
        \|/ |
        (1)------->(2)
        3     */

        /* Let us create the following weighted graph

            10
        (0)------->(3)
        |     /|\
        5 |     |
        |     | 1
        \|/     |
        (1)------->(2)
            3     */
        int [,]graph = new int[,]{{1, 1, 0, 1},
                                  {0, 1, 1, 0},
                                  {0, 0, 1, 1},
                                  {0, 0, 0, 1}};

        // Print the solution
        GFG g = new GFG();
        g.transitiveClosure(graph);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript Program for transitive closure
      // using Floyd Warshall Algorithm
      var V = 4; // Number of vertices in a graph

      // Prints transitive closure of graph[,]
      // using Floyd Warshall algorithm
      function transitiveClosure(graph) {
        /* reach[,] will be the output matrix that
        will finally have the shortest distances
        between every pair of vertices */
        var reach = Array.from(Array(V), () => new Array(V));
        var i, j, k;

        /* Initialize the solution matrix same as
        input graph matrix. Or we can say the
        initial values of shortest distances are
        based on shortest paths considering no
        intermediate vertex. */
        for (i = 0; i < V; i++)
          for (j = 0; j < V; j++) reach[i][j] = graph[i][j];

        /* Add all vertices one by one to the
        set of intermediate vertices.
        ---> Before start of a iteration, we have
            reachability values for all pairs of
            vertices such that the reachability
            values consider only the vertices in
            set {0, 1, 2, .. k-1} as intermediate vertices.
        ---> After the end of a iteration, vertex no.
            k is added to the set of intermediate
            vertices and the set becomes {0, 1, 2, .. k} */
        for (k = 0; k < V; k++) {
          // Pick all vertices as source one by one
          for (i = 0; i < V; i++) {
            // Pick all vertices as destination
            // for the above picked source
            for (j = 0; j < V; j++) {
              // If vertex k is on a path from i to j,
              // then make sure that the value of
              // reach[i,j] is 1
              reach[i][j] =
                reach[i][j] != 0 || (reach[i][k] != 0 && reach[k][j] != 0)
                  ? 1
                  : 0;
            }
          }
        }

        // Print the shortest distance matrix
        printSolution(reach);
      }

      /* A utility function to print solution */
      function printSolution(reach) {
        document.write(
          "Following matrix is transitive" + " closure of the given graph <br>"
        );
        for (var i = 0; i < V; i++) {
          for (var j = 0; j < V; j++) {
            if (i == j) document.write("1 ");
            else document.write(reach[i][j] + " ");
          }
          document.write("<br>");
        }
      }

      // Driver Code
      /* Let us create the following weighted graph
        10
        (0)------->(3)
        |     /|\
    5 |     |
        |     | 1
        \|/ |
        (1)------->(2)
        3     */

      /* Let us create the following weighted graph

            10
        (0)------->(3)
        |     /|\
        5 |     |
        |     | 1
        \|/     |
        (1)------->(2)
            3     */
      var graph = [
        [1, 1, 0, 1],
        [0, 1, 1, 0],
        [0, 0, 1, 1],
        [0, 0, 0, 1],
      ];

      // Print the solution

      transitiveClosure(graph);

      // This code is contributed by rdtank.
    </script>
```

**Output**

```
Following matrix is transitiveclosure of the given graph
1 1 1 1 
0 1 1 1 
0 0 1 1 
0 0 0 1 
```

**时间复杂度:** O(V <sup>3</sup> )，其中 V 是给定图中的顶点数。
见下图，了解 O(V <sup>2</sup> )解决方案。
[使用 DFS 的图的传递闭包](https://www.geeksforgeeks.org/transitive-closure-of-a-graph-using-dfs/)
**参考文献:**
[Clifford Stein、Thomas H. Cormen、Charles E. Leiserson、Ronald L.](http://www.flipkart.com/introduction-algorithms-8120340078/p/itmczynzhyhxv2gs?pid=9788120340077&affid=sandeepgfg)
算法导论如果您发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请写评论。