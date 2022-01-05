# 将邻接表转换为图的邻接矩阵表示

> 原文:[https://www . geesforgeks . org/convert-邻接表-邻接表-矩阵-图的表示/](https://www.geeksforgeeks.org/convert-adjacency-list-to-adjacency-matrix-representation-of-a-graph/)

给定一个**图** 的[邻接表表示，任务是将给定的**邻接表**转换为**邻接矩阵**表示。](https://www.geeksforgeeks.org/graph-and-its-representations/)

**示例:**

> **输入:**adjList[]= { { 0–>1–>3 }、{ 1–>2 }、{ 2–>3 } }
> T3】输出:T5】0 1 0 1
> 0 1 0
> 0 0 1
> 0 0 0 0
> 
> **输入:**adjList[]= { { 0–>1–>4 }、{ 1–>0–>2–>3–>4 }、{ 2–>1–>3 }、{ 3–>1–>2–>4 }、{ 4–>0–>1–>3 } }
> **输出:【T4**

**邻接表:**使用列表数组。数组的大小等于顶点的数量。让数组成为数组[]。条目数组[i]表示与第 i <sup>个</sup>顶点相邻的顶点列表。

**邻接矩阵:**邻接矩阵是一个大小为 V×V 的 2D 数组，其中 V 是图中的顶点数。假设 2D 数组是 adj[][]，槽 adj[i][j] = 1 表示从顶点 I 到顶点 j 有一条边。

按照以下步骤将邻接表转换为邻接矩阵:

*   用 **0** s 初始化矩阵
*   迭代邻接表中的顶点
*   对于邻接表中的每一个**j**顶点，遍历其边。
*   对于第**顶点有边的每个顶点 **i** ，设置 mat[i][j] = 1。**

**下面是上述方法的实现:**

## **C++**

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to insert vertices to adjacency list
void insert(vector<int> adj[], int u, int v)
{
    // Insert a vertex v to vertex u
    adj[u].push_back(v);
    return;
}

// Function to display adjacency list
void printList(vector<int> adj[], int V)
{
    for (int i = 0; i < V; i++) {
        cout << i;
        for (auto j : adj[i])
            cout << " --> " << j;
        cout << endl;
    }
    cout << endl;
}

// Function to convert adjacency
// list to adjacency matrix
vector<vector<int> > convert(vector<int> adj[],
                             int V)
{
    // Initialize a matrix
    vector<vector<int> > matrix(V,
                                vector<int>(V, 0));

    for (int i = 0; i < V; i++) {
        for (auto j : adj[i])
            matrix[i][j] = 1;
    }
    return matrix;
}

// Function to display adjacency matrix
void printMatrix(vector<vector<int> > adj, int V)
{
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            cout << adj[i][j] << "   ";
        }
        cout << endl;
    }
    cout << endl;
}

// Driver code
int main()
{
    int V = 5;

    vector<int> adjList[V];

    // Inserting edges
    insert(adjList, 0, 1);
    insert(adjList, 0, 4);
    insert(adjList, 1, 0);
    insert(adjList, 1, 2);
    insert(adjList, 1, 3);
    insert(adjList, 1, 4);
    insert(adjList, 2, 1);
    insert(adjList, 2, 3);
    insert(adjList, 3, 1);
    insert(adjList, 3, 2);
    insert(adjList, 3, 4);
    insert(adjList, 4, 0);
    insert(adjList, 4, 1);
    insert(adjList, 4, 3);

    // Display adjacency list
    cout << "Adjacency List: \n";
    printList(adjList, V);

    // Function call which returns
    // adjacency matrix after conversion
    vector<vector<int> > adjMatrix
        = convert(adjList, V);

    // Display adjacency matrix
    cout << "Adjacency Matrix: \n";
    printMatrix(adjMatrix, V);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to insert vertices to adjacency list
static void insert(Vector<Integer> adj[],
                   int u, int v)
{

    // Insert a vertex v to vertex u
    adj[u].add(v);
    return;
}

// Function to display adjacency list
static void printList(Vector<Integer> adj[],
                      int V)
{
    for(int i = 0; i < V; i++)
    {
        System.out.print(i);

        for(int j : adj[i])
            System.out.print(" --> " + j);

        System.out.println();
    }
    System.out.println();
}

// Function to convert adjacency
// list to adjacency matrix
static int[][] convert(Vector<Integer> adj[],
                       int V)
{

    // Initialize a matrix
    int [][]matrix = new int[V][V];

    for(int i = 0; i < V; i++)
    {
        for(int j : adj[i])
            matrix[i][j] = 1;
    }
    return matrix;
}

// Function to display adjacency matrix
static void printMatrix(int[][] adj, int V)
{
    for(int i = 0; i < V; i++)
    {
        for(int j = 0; j < V; j++)
        {
            System.out.print(adj[i][j] + " ");
        }
        System.out.println();
    }
    System.out.println();
}

// Driver code
public static void main(String[] args)
{
    int V = 5;

    @SuppressWarnings("unchecked")
    Vector<Integer> []adjList = new Vector[V];
    for(int i = 0; i < adjList.length; i++)
        adjList[i] = new Vector<Integer>();

    // Inserting edges
    insert(adjList, 0, 1);
    insert(adjList, 0, 4);
    insert(adjList, 1, 0);
    insert(adjList, 1, 2);
    insert(adjList, 1, 3);
    insert(adjList, 1, 4);
    insert(adjList, 2, 1);
    insert(adjList, 2, 3);
    insert(adjList, 3, 1);
    insert(adjList, 3, 2);
    insert(adjList, 3, 4);
    insert(adjList, 4, 0);
    insert(adjList, 4, 1);
    insert(adjList, 4, 3);

    // Display adjacency list
    System.out.print("Adjacency List: \n");
    printList(adjList, V);

    // Function call which returns
    // adjacency matrix after conversion
    int[][] adjMatrix = convert(adjList, V);

    // Display adjacency matrix
    System.out.print("Adjacency Matrix: \n");
    printMatrix(adjMatrix, V);
}
}

// This code is contributed by amal kumar choubey
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach

# Function to insert vertices
# to adjacency list
def insert(adj, u, v):

    # Insert a vertex v to vertex u
    adj[u].append(v)
    return

# Function to display adjacency list
def printList(adj, V):

    for i in range(V):
        print(i, end = '')

        for j in adj[i]:
            print(' --> ' + str(j), end = '')

        print()

    print()

# Function to convert adjacency
# list to adjacency matrix
def convert(adj, V):

    # Initialize a matrix
    matrix = [[0 for j in range(V)]
                 for i in range(V)]

    for i in range(V):
        for j in adj[i]:
            matrix[i][j] = 1

    return matrix

# Function to display adjacency matrix
def printMatrix(adj, V):

    for i in range(V):
        for j in range(V):
            print(adj[i][j], end = ' ')

        print()

    print()

# Driver code
if __name__=='__main__':

    V = 5

    adjList = [[] for i in range(V)]

    # Inserting edges
    insert(adjList, 0, 1)
    insert(adjList, 0, 4)
    insert(adjList, 1, 0)
    insert(adjList, 1, 2)
    insert(adjList, 1, 3)
    insert(adjList, 1, 4)
    insert(adjList, 2, 1)
    insert(adjList, 2, 3)
    insert(adjList, 3, 1)
    insert(adjList, 3, 2)
    insert(adjList, 3, 4)
    insert(adjList, 4, 0)
    insert(adjList, 4, 1)
    insert(adjList, 4, 3)

    # Display adjacency list
    print("Adjacency List: ")
    printList(adjList, V)

    # Function call which returns
    # adjacency matrix after conversion
    adjMatrix = convert(adjList, V)

    # Display adjacency matrix
    print("Adjacency Matrix: ")
    printMatrix(adjMatrix, V)

# This code is contributed by rutvik_56
```

## **C#**

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to insert vertices to adjacency list
static void insert(List<int> []adj,
                        int u, int v)
{

    // Insert a vertex v to vertex u
    adj[u].Add(v);
    return;
}

// Function to display adjacency list
static void printList(List<int> []adj,
                           int V)
{
    for(int i = 0; i < V; i++)
    {
        Console.Write(i);

        foreach(int j in adj[i])
            Console.Write(" --> " + j);

        Console.WriteLine();
    }
    Console.WriteLine();
}

// Function to convert adjacency
// list to adjacency matrix
static int[,] convert(List<int> []adj,
                           int V)
{

    // Initialize a matrix
    int [,]matrix = new int[V, V];

    for(int i = 0; i < V; i++)
    {
        foreach(int j in adj[i])
            matrix[i, j] = 1;
    }
    return matrix;
}

// Function to display adjacency matrix
static void printMatrix(int[,] adj, int V)
{
    for(int i = 0; i < V; i++)
    {
        for(int j = 0; j < V; j++)
        {
            Console.Write(adj[i, j] + " ");
        }
        Console.WriteLine();
    }
    Console.WriteLine();
}

// Driver code
public static void Main(String[] args)
{
    int V = 5;

    List<int> []adjList = new List<int>[V];
    for(int i = 0; i < adjList.Length; i++)
        adjList[i] = new List<int>();

    // Inserting edges
    insert(adjList, 0, 1);
    insert(adjList, 0, 4);
    insert(adjList, 1, 0);
    insert(adjList, 1, 2);
    insert(adjList, 1, 3);
    insert(adjList, 1, 4);
    insert(adjList, 2, 1);
    insert(adjList, 2, 3);
    insert(adjList, 3, 1);
    insert(adjList, 3, 2);
    insert(adjList, 3, 4);
    insert(adjList, 4, 0);
    insert(adjList, 4, 1);
    insert(adjList, 4, 3);

    // Display adjacency list
    Console.Write("Adjacency List: \n");
    printList(adjList, V);

    // Function call which returns
    // adjacency matrix after conversion
    int[,] adjMatrix = convert(adjList, V);

    // Display adjacency matrix
    Console.Write("Adjacency Matrix: \n");
    printMatrix(adjMatrix, V);
}
}

// This code is contributed by amal kumar choubey
```

## **java 描述语言**

```
<script>

// Javascript program to implement
// the above approach

// Function to insert vertices to adjacency list
function insert(adj, u, v)
{

    // Insert a vertex v to vertex u
    adj[u].push(v);
    return;
}

// Function to display adjacency list
function printList(adj, V)
{
    for(var i = 0; i < V; i++)
    {
        document.write(i);

        for(var j of adj[i])
            document.write(" --> " + j);

        document.write("<br>");
    }
    document.write("<br>");
}

// Function to convert adjacency
// list to adjacency matrix
function convert(adj, V)
{

    // Initialize a matrix
    var matrix = Array.from(Array(V), ()=>Array(V).fill(0));
    for (var i = 0; i < V; i++) {
        for (var j of adj[i])
            matrix[i][j] = 1;
    }
    return matrix;
}

// Function to display adjacency matrix
function printMatrix(adj, V)
{
    for(var i = 0; i < V; i++)
    {
        for(var j = 0; j < V; j++)
        {
            document.write(adj[i][j] + " ");
        }
        document.write("<br>");
    }
    document.write("<br>");
}

// Driver code
var V = 5;
var adjList = Array.from(Array(V), ()=>Array().fill(0));

// Inserting edges
insert(adjList, 0, 1);
insert(adjList, 0, 4);
insert(adjList, 1, 0);
insert(adjList, 1, 2);
insert(adjList, 1, 3);
insert(adjList, 1, 4);
insert(adjList, 2, 1);
insert(adjList, 2, 3);
insert(adjList, 3, 1);
insert(adjList, 3, 2);
insert(adjList, 3, 4);
insert(adjList, 4, 0);
insert(adjList, 4, 1);
insert(adjList, 4, 3);
// Display adjacency list
document.write("Adjacency List: <br>");
printList(adjList, V);
// Function call which returns
// adjacency matrix after conversion
var adjMatrix = convert(adjList, V);
// Display adjacency matrix
document.write("Adjacency Matrix: <br>");
printMatrix(adjMatrix, V);

</script>
```

****Output:** 

```
Adjacency List: 
0 --> 1 --> 4
1 --> 0 --> 2 --> 3 --> 4
2 --> 1 --> 3
3 --> 1 --> 2 --> 4
4 --> 0 --> 1 --> 3

Adjacency Matrix: 
0   1   0   0   1   
1   0   1   1   1   
0   1   0   1   0   
0   1   1   0   1   
1   1   0   1   0
```** 

*****时间复杂度:** O(N*M)*
***辅助空间:** O(N <sup>2</sup> )***