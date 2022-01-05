# 哈密顿圈|回溯-6

> 原文:[https://www . geesforgeks . org/Hamiltonian-cycle-backtracking-6/](https://www.geeksforgeeks.org/hamiltonian-cycle-backtracking-6/)

[无向图中的哈密顿路径](http://en.wikipedia.org/wiki/Hamiltonian_path)是一条恰好访问每个顶点一次的路径。哈密尔顿循环(或哈密尔顿电路)是哈密尔顿路径，使得从哈密尔顿路径的最后一个顶点到第一个顶点有一条边(在图中)。确定给定的图是否包含哈密顿圈。如果包含，则打印路径。以下是所需功能的输入和输出。
*输入:*
一个 2D 数组图[V][V]其中 V 是图中的顶点数，图[V][V]是图的邻接矩阵表示。如果有从 I 到 j 的直接边，则值图[i][j]为 1，否则图[i][j]为 0。
*输出:*
应该包含哈密顿路径的数组路径[V]。路径[i]应该代表哈密顿路径中的第 I 个顶点。如果图中没有哈密顿圈，代码也应该返回 false。
例如，下图中的哈密顿圈是{0，1，2，4，3，0}。

```
(0)--(1)--(2)
 |   / \   |
 |  /   \  | 
 | /     \ |
(3)-------(4)
```

下图不包含任何哈密顿圈。

```
(0)--(1)--(2)
 |   / \   |
 |  /   \  | 
 | /     \ |
(3)      (4) 
```

**朴素算法**
生成所有可能的顶点配置，并打印满足给定约束的配置。会有 n 个！(n 阶乘)构型。

```
while there are untried conflagrations
{
   generate the next configuration
   if ( there are edges between two consecutive vertices of this
      configuration and there is an edge from the last vertex to 
      the first ).
   {
      print this configuration;
      break;
   }
}
```

**回溯算法**
创建一个空路径数组，并在其中添加顶点 0。添加其他顶点，从顶点 1 开始。在添加顶点之前，检查它是否与先前添加的顶点相邻，并且尚未添加。如果我们找到这样一个顶点，我们就把这个顶点作为解的一部分。如果我们没有找到顶点，那么我们返回假。

**回溯解决方案的实现**
以下是回溯解决方案的实现。

## C++

```
/* C++ program for solution of Hamiltonian
Cycle problem using backtracking */
#include <bits/stdc++.h>
using namespace std;

// Number of vertices in the graph
#define V 5

void printSolution(int path[]);

/* A utility function to check if
the vertex v can be added at index 'pos'
in the Hamiltonian Cycle constructed
so far (stored in 'path[]') */
bool isSafe(int v, bool graph[V][V],
            int path[], int pos)
{
    /* Check if this vertex is an adjacent
    vertex of the previously added vertex. */
    if (graph [path[pos - 1]][ v ] == 0)
        return false;

    /* Check if the vertex has already been included.
    This step can be optimized by creating
    an array of size V */
    for (int i = 0; i < pos; i++)
        if (path[i] == v)
            return false;

    return true;
}

/* A recursive utility function
to solve hamiltonian cycle problem */
bool hamCycleUtil(bool graph[V][V],
                  int path[], int pos)
{
    /* base case: If all vertices are
    included in Hamiltonian Cycle */
    if (pos == V)
    {
        // And if there is an edge from the
        // last included vertex to the first vertex
        if (graph[path[pos - 1]][path[0]] == 1)
            return true;
        else
            return false;
    }

    // Try different vertices as a next candidate
    // in Hamiltonian Cycle. We don't try for 0 as
    // we included 0 as starting point in hamCycle()
    for (int v = 1; v < V; v++)
    {
        /* Check if this vertex can be added
        // to Hamiltonian Cycle */
        if (isSafe(v, graph, path, pos))
        {
            path[pos] = v;

            /* recur to construct rest of the path */
            if (hamCycleUtil (graph, path, pos + 1) == true)
                return true;

            /* If adding vertex v doesn't lead to a solution,
            then remove it */
            path[pos] = -1;
        }
    }

    /* If no vertex can be added to
    Hamiltonian Cycle constructed so far,
    then return false */
    return false;
}

/* This function solves the Hamiltonian Cycle problem
using Backtracking. It mainly uses hamCycleUtil() to
solve the problem. It returns false if there is no
Hamiltonian Cycle possible, otherwise return true
and prints the path. Please note that there may be
more than one solutions, this function prints one
of the feasible solutions. */
bool hamCycle(bool graph[V][V])
{
    int *path = new int[V];
    for (int i = 0; i < V; i++)
        path[i] = -1;

    /* Let us put vertex 0 as the first vertex in the path.
    If there is a Hamiltonian Cycle, then the path can be
    started from any point of the cycle as the graph is undirected */
    path[0] = 0;
    if (hamCycleUtil(graph, path, 1) == false )
    {
        cout << "\nSolution does not exist";
        return false;
    }

    printSolution(path);
    return true;
}

/* A utility function to print solution */
void printSolution(int path[])
{
    cout << "Solution Exists:"
            " Following is one Hamiltonian Cycle \n";
    for (int i = 0; i < V; i++)
        cout << path[i] << " ";

    // Let us print the first vertex again
    // to show the complete cycle
    cout << path[0] << " ";
    cout << endl;
}

// Driver Code
int main()
{
    /* Let us create the following graph
        (0)--(1)--(2)
        | / \ |
        | / \ |
        | / \ |
        (3)-------(4) */
    bool graph1[V][V] = {{0, 1, 0, 1, 0},
                        {1, 0, 1, 1, 1},
                        {0, 1, 0, 0, 1},
                        {1, 1, 0, 0, 1},
                        {0, 1, 1, 1, 0}};

    // Print the solution
    hamCycle(graph1);

    /* Let us create the following graph
    (0)--(1)--(2)
    | / \ |
    | / \ |
    | / \ |
    (3) (4) */
    bool graph2[V][V] = {{0, 1, 0, 1, 0},
                         {1, 0, 1, 1, 1},
                         {0, 1, 0, 0, 1},
                         {1, 1, 0, 0, 0},
                         {0, 1, 1, 0, 0}};

    // Print the solution
    hamCycle(graph2);

    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
/* C program for solution of Hamiltonian Cycle problem
   using backtracking */
#include<stdio.h>

// Number of vertices in the graph
#define V 5

void printSolution(int path[]);

/* A utility function to check if the vertex v can be added at
   index 'pos' in the Hamiltonian Cycle constructed so far (stored
   in 'path[]') */
bool isSafe(int v, bool graph[V][V], int path[], int pos)
{
    /* Check if this vertex is an adjacent vertex of the previously
       added vertex. */
    if (graph [ path[pos-1] ][ v ] == 0)
        return false;

    /* Check if the vertex has already been included.
      This step can be optimized by creating an array of size V */
    for (int i = 0; i < pos; i++)
        if (path[i] == v)
            return false;

    return true;
}

/* A recursive utility function to solve hamiltonian cycle problem */
bool hamCycleUtil(bool graph[V][V], int path[], int pos)
{
    /* base case: If all vertices are included in Hamiltonian Cycle */
    if (pos == V)
    {
        // And if there is an edge from the last included vertex to the
        // first vertex
        if ( graph[ path[pos-1] ][ path[0] ] == 1 )
           return true;
        else
          return false;
    }

    // Try different vertices as a next candidate in Hamiltonian Cycle.
    // We don't try for 0 as we included 0 as starting point in hamCycle()
    for (int v = 1; v < V; v++)
    {
        /* Check if this vertex can be added to Hamiltonian Cycle */
        if (isSafe(v, graph, path, pos))
        {
            path[pos] = v;

            /* recur to construct rest of the path */
            if (hamCycleUtil (graph, path, pos+1) == true)
                return true;

            /* If adding vertex v doesn't lead to a solution,
               then remove it */
            path[pos] = -1;
        }
    }

    /* If no vertex can be added to Hamiltonian Cycle constructed so far,
       then return false */
    return false;
}

/* This function solves the Hamiltonian Cycle problem using Backtracking.
  It mainly uses hamCycleUtil() to solve the problem. It returns false
  if there is no Hamiltonian Cycle possible, otherwise return true and
  prints the path. Please note that there may be more than one solutions,
  this function prints one of the feasible solutions. */
bool hamCycle(bool graph[V][V])
{
    int *path = new int[V];
    for (int i = 0; i < V; i++)
        path[i] = -1;

    /* Let us put vertex 0 as the first vertex in the path. If there is
       a Hamiltonian Cycle, then the path can be started from any point
       of the cycle as the graph is undirected */
    path[0] = 0;
    if ( hamCycleUtil(graph, path, 1) == false )
    {
        printf("\nSolution does not exist");
        return false;
    }

    printSolution(path);
    return true;
}

/* A utility function to print solution */
void printSolution(int path[])
{
    printf ("Solution Exists:"
            " Following is one Hamiltonian Cycle \n");
    for (int i = 0; i < V; i++)
        printf(" %d ", path[i]);

    // Let us print the first vertex again to show the complete cycle
    printf(" %d ", path[0]);
    printf("\n");
}

// driver program to test above function
int main()
{
   /* Let us create the following graph
      (0)--(1)--(2)
       |   / \   |
       |  /   \  |
       | /     \ |
      (3)-------(4)    */
   bool graph1[V][V] = {{0, 1, 0, 1, 0},
                      {1, 0, 1, 1, 1},
                      {0, 1, 0, 0, 1},
                      {1, 1, 0, 0, 1},
                      {0, 1, 1, 1, 0},
                     };

    // Print the solution
    hamCycle(graph1);

   /* Let us create the following graph
      (0)--(1)--(2)
       |   / \   |
       |  /   \  |
       | /     \ |
      (3)       (4)    */
    bool graph2[V][V] = {{0, 1, 0, 1, 0},
                      {1, 0, 1, 1, 1},
                      {0, 1, 0, 0, 1},
                      {1, 1, 0, 0, 0},
                      {0, 1, 1, 0, 0},
                     };

    // Print the solution
    hamCycle(graph2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java program for solution of Hamiltonian Cycle problem
   using backtracking */
class HamiltonianCycle
{
    final int V = 5;
    int path[];

    /* A utility function to check if the vertex v can be
       added at index 'pos'in the Hamiltonian Cycle
       constructed so far (stored in 'path[]') */
    boolean isSafe(int v, int graph[][], int path[], int pos)
    {
        /* Check if this vertex is an adjacent vertex of
           the previously added vertex. */
        if (graph[path[pos - 1]][v] == 0)
            return false;

        /* Check if the vertex has already been included.
           This step can be optimized by creating an array
           of size V */
        for (int i = 0; i < pos; i++)
            if (path[i] == v)
                return false;

        return true;
    }

    /* A recursive utility function to solve hamiltonian
       cycle problem */
    boolean hamCycleUtil(int graph[][], int path[], int pos)
    {
        /* base case: If all vertices are included in
           Hamiltonian Cycle */
        if (pos == V)
        {
            // And if there is an edge from the last included
            // vertex to the first vertex
            if (graph[path[pos - 1]][path[0]] == 1)
                return true;
            else
                return false;
        }

        // Try different vertices as a next candidate in
        // Hamiltonian Cycle. We don't try for 0 as we
        // included 0 as starting point in hamCycle()
        for (int v = 1; v < V; v++)
        {
            /* Check if this vertex can be added to Hamiltonian
               Cycle */
            if (isSafe(v, graph, path, pos))
            {
                path[pos] = v;

                /* recur to construct rest of the path */
                if (hamCycleUtil(graph, path, pos + 1) == true)
                    return true;

                /* If adding vertex v doesn't lead to a solution,
                   then remove it */
                path[pos] = -1;
            }
        }

        /* If no vertex can be added to Hamiltonian Cycle
           constructed so far, then return false */
        return false;
    }

    /* This function solves the Hamiltonian Cycle problem using
       Backtracking. It mainly uses hamCycleUtil() to solve the
       problem. It returns false if there is no Hamiltonian Cycle
       possible, otherwise return true and prints the path.
       Please note that there may be more than one solutions,
       this function prints one of the feasible solutions. */
    int hamCycle(int graph[][])
    {
        path = new int[V];
        for (int i = 0; i < V; i++)
            path[i] = -1;

        /* Let us put vertex 0 as the first vertex in the path.
           If there is a Hamiltonian Cycle, then the path can be
           started from any point of the cycle as the graph is
           undirected */
        path[0] = 0;
        if (hamCycleUtil(graph, path, 1) == false)
        {
            System.out.println("\nSolution does not exist");
            return 0;
        }

        printSolution(path);
        return 1;
    }

    /* A utility function to print solution */
    void printSolution(int path[])
    {
        System.out.println("Solution Exists: Following" +
                           " is one Hamiltonian Cycle");
        for (int i = 0; i < V; i++)
            System.out.print(" " + path[i] + " ");

        // Let us print the first vertex again to show the
        // complete cycle
        System.out.println(" " + path[0] + " ");
    }

    // driver program to test above function
    public static void main(String args[])
    {
        HamiltonianCycle hamiltonian =
                                new HamiltonianCycle();
        /* Let us create the following graph
           (0)--(1)--(2)
            |   / \   |
            |  /   \  |
            | /     \ |
           (3)-------(4)    */
        int graph1[][] = {{0, 1, 0, 1, 0},
            {1, 0, 1, 1, 1},
            {0, 1, 0, 0, 1},
            {1, 1, 0, 0, 1},
            {0, 1, 1, 1, 0},
        };

        // Print the solution
        hamiltonian.hamCycle(graph1);

        /* Let us create the following graph
           (0)--(1)--(2)
            |   / \   |
            |  /   \  |
            | /     \ |
           (3)       (4)    */
        int graph2[][] = {{0, 1, 0, 1, 0},
            {1, 0, 1, 1, 1},
            {0, 1, 0, 0, 1},
            {1, 1, 0, 0, 0},
            {0, 1, 1, 0, 0},
        };

        // Print the solution
        hamiltonian.hamCycle(graph2);
    }
}
// This code is contributed by Abhishek Shankhadhar
```

## 蟒蛇 3

```
# Python program for solution of
# hamiltonian cycle problem

class Graph():
    def __init__(self, vertices):
        self.graph = [[0 for column in range(vertices)]
                            for row in range(vertices)]
        self.V = vertices

    ''' Check if this vertex is an adjacent vertex
        of the previously added vertex and is not
        included in the path earlier '''
    def isSafe(self, v, pos, path):
        # Check if current vertex and last vertex
        # in path are adjacent
        if self.graph[ path[pos-1] ][v] == 0:
            return False

        # Check if current vertex not already in path
        for vertex in path:
            if vertex == v:
                return False

        return True

    # A recursive utility function to solve
    # hamiltonian cycle problem
    def hamCycleUtil(self, path, pos):

        # base case: if all vertices are
        # included in the path
        if pos == self.V:
            # Last vertex must be adjacent to the
            # first vertex in path to make a cyle
            if self.graph[ path[pos-1] ][ path[0] ] == 1:
                return True
            else:
                return False

        # Try different vertices as a next candidate
        # in Hamiltonian Cycle. We don't try for 0 as
        # we included 0 as starting point in hamCycle()
        for v in range(1,self.V):

            if self.isSafe(v, pos, path) == True:

                path[pos] = v

                if self.hamCycleUtil(path, pos+1) == True:
                    return True

                # Remove current vertex if it doesn't
                # lead to a solution
                path[pos] = -1

        return False

    def hamCycle(self):
        path = [-1] * self.V

        ''' Let us put vertex 0 as the first vertex
            in the path. If there is a Hamiltonian Cycle,
            then the path can be started from any point
            of the cycle as the graph is undirected '''
        path[0] = 0

        if self.hamCycleUtil(path,1) == False:
            print ("Solution does not exist\n")
            return False

        self.printSolution(path)
        return True

    def printSolution(self, path):
        print ("Solution Exists: Following",
                 "is one Hamiltonian Cycle")
        for vertex in path:
            print (vertex, end = " ")
        print (path[0], "\n")

# Driver Code

''' Let us create the following graph
    (0)--(1)--(2)
    | / \ |
    | / \ |
    | /     \ |
    (3)-------(4) '''
g1 = Graph(5)
g1.graph = [ [0, 1, 0, 1, 0], [1, 0, 1, 1, 1],
            [0, 1, 0, 0, 1,],[1, 1, 0, 0, 1],
            [0, 1, 1, 1, 0], ]

# Print the solution
g1.hamCycle();

''' Let us create the following graph
    (0)--(1)--(2)
    | / \ |
    | / \ |
    | /     \ |
    (3)     (4) '''
g2 = Graph(5)
g2.graph = [ [0, 1, 0, 1, 0], [1, 0, 1, 1, 1],
        [0, 1, 0, 0, 1,], [1, 1, 0, 0, 0],
        [0, 1, 1, 0, 0], ]

# Print the solution
g2.hamCycle();

# This code is contributed by Divyanshu Mehta
```

## C#

```
// C# program for solution of Hamiltonian
// Cycle problem using backtracking
using System;

public class HamiltonianCycle
{
    readonly int V = 5;
    int []path;

    /* A utility function to check
    if the vertex v can be added at
    index 'pos'in the Hamiltonian Cycle
    constructed so far (stored in 'path[]') */
    bool isSafe(int v, int [,]graph,
                int []path, int pos)
    {
        /* Check if this vertex is
        an adjacent vertex of the
        previously added vertex. */
        if (graph[path[pos - 1], v] == 0)
            return false;

        /* Check if the vertex has already
        been included. This step can be
        optimized by creating an array
        of size V */
        for (int i = 0; i < pos; i++)
            if (path[i] == v)
                return false;

        return true;
    }

    /* A recursive utility function
    to solve hamiltonian cycle problem */
    bool hamCycleUtil(int [,]graph, int []path, int pos)
    {
        /* base case: If all vertices
        are included in Hamiltonian Cycle */
        if (pos == V)
        {
            // And if there is an edge from the last included
            // vertex to the first vertex
            if (graph[path[pos - 1],path[0]] == 1)
                return true;
            else
                return false;
        }

        // Try different vertices as a next candidate in
        // Hamiltonian Cycle. We don't try for 0 as we
        // included 0 as starting point in hamCycle()
        for (int v = 1; v < V; v++)
        {
            /* Check if this vertex can be
            added to Hamiltonian Cycle */
            if (isSafe(v, graph, path, pos))
            {
                path[pos] = v;

                /* recur to construct rest of the path */
                if (hamCycleUtil(graph, path, pos + 1) == true)
                    return true;

                /* If adding vertex v doesn't
                lead to a solution, then remove it */
                path[pos] = -1;
            }
        }

        /* If no vertex can be added to Hamiltonian Cycle
        constructed so far, then return false */
        return false;
    }

    /* This function solves the Hamiltonian
    Cycle problem using Backtracking. It
    mainly uses hamCycleUtil() to solve the
    problem. It returns false if there
    is no Hamiltonian Cycle possible,
    otherwise return true and prints the path.
    Please note that there may be more than
    one solutions, this function prints one
    of the feasible solutions. */
    int hamCycle(int [,]graph)
    {
        path = new int[V];
        for (int i = 0; i < V; i++)
            path[i] = -1;

        /* Let us put vertex 0 as the first
        vertex in the path. If there is a
        Hamiltonian Cycle, then the path can be
        started from any point of the cycle
        as the graph is undirected */
        path[0] = 0;
        if (hamCycleUtil(graph, path, 1) == false)
        {
            Console.WriteLine("\nSolution does not exist");
            return 0;
        }

        printSolution(path);
        return 1;
    }

    /* A utility function to print solution */
    void printSolution(int []path)
    {
        Console.WriteLine("Solution Exists: Following" +
                        " is one Hamiltonian Cycle");
        for (int i = 0; i < V; i++)
            Console.Write(" " + path[i] + " ");

        // Let us print the first vertex again
        //  to show the complete cycle
        Console.WriteLine(" " + path[0] + " ");
    }

    // Driver code
    public static void Main(String []args)
    {
        HamiltonianCycle hamiltonian =
                                new HamiltonianCycle();
        /* Let us create the following graph
        (0)--(1)--(2)
            | / \ |
            | / \ |
            | /     \ |
        (3)-------(4) */
        int [,]graph1= {{0, 1, 0, 1, 0},
            {1, 0, 1, 1, 1},
            {0, 1, 0, 0, 1},
            {1, 1, 0, 0, 1},
            {0, 1, 1, 1, 0},
        };

        // Print the solution
        hamiltonian.hamCycle(graph1);

        /* Let us create the following graph
        (0)--(1)--(2)
            | / \ |
            | / \ |
            | /     \ |
        (3)     (4) */
        int [,]graph2 = {{0, 1, 0, 1, 0},
            {1, 0, 1, 1, 1},
            {0, 1, 0, 0, 1},
            {1, 1, 0, 0, 0},
            {0, 1, 1, 0, 0},
        };

        // Print the solution
        hamiltonian.hamCycle(graph2);
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for solution of
// Hamiltonian Cycle problem
// using backtracking
$V = 5;

/* A utility function to check if
the vertex v can be added at index 'pos'
in the Hamiltonian Cycle constructed so far
(stored in 'path[]') */
function isSafe($v, $graph, &$path, $pos)
{
    /* Check if this vertex is
    an adjacent vertex of the
    previously added vertex. */
    if ($graph[$path[$pos - 1]][$v] == 0)
        return false;

    /* Check if the vertex has already been included.
    This step can be optimized by creating an array
    of size V */
    for ($i = 0; $i < $pos; $i++)
        if ($path[$i] == $v)
            return false;

    return true;
}

/* A recursive utility function
to solve hamiltonian cycle problem */
function hamCycleUtil($graph, &$path, $pos)
{
    global $V;

    /* base case: If all vertices are included in
    Hamiltonian Cycle */
    if ($pos == $V)
    {
        // And if there is an edge from the
        // last included vertex to the first vertex
        if ($graph[$path[$pos - 1]][$path[0]] == 1)
            return true;
        else
            return false;
    }

    // Try different vertices as a next candidate in
    // Hamiltonian Cycle. We don't try for 0 as we
    // included 0 as starting point hamCycle()
    for ($v = 1; $v < $V; $v++)
    {
        /* Check if this vertex can be added
        to Hamiltonian Cycle */
        if (isSafe($v, $graph, $path, $pos))
        {
            $path[$pos] = $v;

            /* recur to construct rest of the path */
            if (hamCycleUtil($graph, $path,
                                     $pos + 1) == true)
                return true;

            /* If adding vertex v doesn't lead to a solution,
            then remove it */
            $path[$pos] = -1;
        }
    }

    /* If no vertex can be added to Hamiltonian Cycle
    constructed so far, then return false */
    return false;
}

/* This function solves the Hamiltonian Cycle problem using
Backtracking. It mainly uses hamCycleUtil() to solve the
problem. It returns false if there is no Hamiltonian Cycle
possible, otherwise return true and prints the path.
Please note that there may be more than one solutions,
this function prints one of the feasible solutions. */
function hamCycle($graph)
{
    global $V;
    $path = array_fill(0, $V, 0);
    for ($i = 0; $i < $V; $i++)
        $path[$i] = -1;

    /* Let us put vertex 0 as the first vertex in the path.
    If there is a Hamiltonian Cycle, then the path can be
    started from any point of the cycle as the graph is
    undirected */
    $path[0] = 0;
    if (hamCycleUtil($graph, $path, 1) == false)
    {
        echo("\nSolution does not exist");
        return 0;
    }

    printSolution($path);
    return 1;
}

/* A utility function to print solution */
function printSolution($path)
{
    global $V;
    echo("Solution Exists: Following is ".
         "one Hamiltonian Cycle\n");
    for ($i = 0; $i < $V; $i++)
        echo(" ".$path[$i]." ");

    // Let us print the first vertex again to show the
    // complete cycle
    echo(" ".$path[0]." \n");
}

// Driver Code

/* Let us create the following graph
(0)--(1)--(2)
    | / \ |
    | / \ |
    | / \ |
(3)-------(4) */
$graph1 = array(array(0, 1, 0, 1, 0),
    array(1, 0, 1, 1, 1),
    array(0, 1, 0, 0, 1),
    array(1, 1, 0, 0, 1),
    array(0, 1, 1, 1, 0),
);

// Print the solution
hamCycle($graph1);

/* Let us create the following graph
(0)--(1)--(2)
    | / \ |
    | / \ |
    | / \ |
(3) (4) */
$graph2 = array(array(0, 1, 0, 1, 0),
                array(1, 0, 1, 1, 1),
                array(0, 1, 0, 0, 1),
                array(1, 1, 0, 0, 0),
                array(0, 1, 1, 0, 0));

// Print the solution
hamCycle($graph2);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
      // JavaScript program for solution of Hamiltonian
      // Cycle problem using backtracking

      class HamiltonianCycle {
        constructor() {
          this.V = 5;
          this.path = [];
        }

        /* A utility function to check
    if the vertex v can be added at
    index 'pos'in the Hamiltonian Cycle
    constructed so far (stored in 'path[]') */
        isSafe(v, graph, path, pos) {
          /* Check if this vertex is
        an adjacent vertex of the
        previously added vertex. */
          if (graph[path[pos - 1]][v] == 0) return false;

          /* Check if the vertex has already
        been included. This step can be
        optimized by creating an array
        of size V */
          for (var i = 0; i < pos; i++) if (path[i] == v) return false;

          return true;
        }

        /* A recursive utility function
    to solve hamiltonian cycle problem */
        hamCycleUtil(graph, path, pos) {
          /* base case: If all vertices
        are included in Hamiltonian Cycle */
          if (pos == this.V) {
            // And if there is an edge from the last included
            // vertex to the first vertex
            if (graph[path[pos - 1]][path[0]] == 1) return true;
            else return false;
          }

          // Try different vertices as a next candidate in
          // Hamiltonian Cycle. We don't try for 0 as we
          // included 0 as starting point in hamCycle()
          for (var v = 1; v < this.V; v++) {
            /* Check if this vertex can be
            added to Hamiltonian Cycle */
            if (this.isSafe(v, graph, path, pos)) {
              path[pos] = v;

              /* recur to construct rest of the path */
              if (this.hamCycleUtil(graph, path, pos + 1) == true) return true;

              /* If adding vertex v doesn't
                lead to a solution, then remove it */
              path[pos] = -1;
            }
          }

          /* If no vertex can be added to Hamiltonian Cycle
        constructed so far, then return false */
          return false;
        }

        /* This function solves the Hamiltonian
    Cycle problem using Backtracking. It
    mainly uses hamCycleUtil() to solve the
    problem. It returns false if there
    is no Hamiltonian Cycle possible,
    otherwise return true and prints the path.
    Please note that there may be more than
    one solutions, this function prints one
    of the feasible solutions. */
        hamCycle(graph) {
          this.path = new Array(this.V).fill(0);
          for (var i = 0; i < this.V; i++) this.path[i] = -1;

          /* Let us put vertex 0 as the first
        vertex in the path. If there is a
        Hamiltonian Cycle, then the path can be
        started from any point of the cycle
        as the graph is undirected */
          this.path[0] = 0;
          if (this.hamCycleUtil(graph, this.path, 1) == false) {
            document.write("<br>Solution does not exist");
            return 0;
          }

          this.printSolution(this.path);
          return 1;
        }

        /* A utility function to print solution */
        printSolution(path) {
          document.write(
            "Solution Exists: Following" + " is one Hamiltonian Cycle <br>"
          );
          for (var i = 0; i < this.V; i++) document.write(" " + path[i] + " ");

          // Let us print the first vertex again
          // to show the complete cycle
          document.write(" " + path[0] + " <br>");
        }
      }
      // Driver code
      var hamiltonian = new HamiltonianCycle();
      /* Let us create the following graph
        (0)--(1)--(2)
            | / \ |
            | / \ |
            | /     \ |
        (3)-------(4) */
      var graph1 = [
        [0, 1, 0, 1, 0],
        [1, 0, 1, 1, 1],
        [0, 1, 0, 0, 1],
        [1, 1, 0, 0, 1],
        [0, 1, 1, 1, 0],
      ];

      // Print the solution
      hamiltonian.hamCycle(graph1);

      /* Let us create the following graph
        (0)--(1)--(2)
            | / \ |
            | / \ |
            | /     \ |
        (3)     (4) */
      var graph2 = [
        [0, 1, 0, 1, 0],
        [1, 0, 1, 1, 1],
        [0, 1, 0, 0, 1],
        [1, 1, 0, 0, 0],
        [0, 1, 1, 0, 0],
      ];

      // Print the solution
      hamiltonian.hamCycle(graph2);

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
Solution Exists: Following is one Hamiltonian Cycle
 0  1  2  4  3  0

Solution does not exist
```

注意，上面的代码总是打印一个从 0 开始的循环。起点应该无关紧要，因为周期可以从任何一点开始。如果要更改起点，应该对上述代码进行两处更改。
更改“路径[0]= 0；”到“路径[0]= s；”哪里是你的新起点。也将循环”改为(int v = 1；V<V；v++)“in hamCycleUtil()to”为(int v = 0；伏<伏；v++)”。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。