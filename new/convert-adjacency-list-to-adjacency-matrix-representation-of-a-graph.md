# 将邻接列表转换为图的邻接矩阵表示

> 原文： [https://www.geeksforgeeks.org/convert-adjacency-list-to-adjacency-matrix-representation-of-a-graph/](https://www.geeksforgeeks.org/convert-adjacency-list-to-adjacency-matrix-representation-of-a-graph/)

给定**图** 的[邻接表表示形式，任务是将给定的**邻接表**转换​​为**邻接矩阵**表示形式。](https://www.geeksforgeeks.org/graph-and-its-representations/)

**示例**：

> **输入**：adjList [] = {{0-> 1-> 3}，{1-> 2}，{2-> 3}}
> **输出**：
> 0 1 0 1
> 0 0 1 0
> 0 0 0 1
> 0 0 0 0
> 
> **输入**：adjList [] = {{0-> 1-> 4}，{1-> 0-> 2-> 3-> 4} ，{2 – > 1 – > 3}，{3 – > 1 – > 2 – > 4}，{4 – > 0 – > 1 – > 3}}
> **输出**：
> 0 1 0 0 1
> 1 0 1 1 1
> 0 1 0 1 0
> 0 1 1 0 1
> 1 1 0 1 0

**邻接列表**：使用列表数组。 数组的大小等于顶点数。 令数组为 array []。 入口数组[i]表示与第 i <sup>个</sup>顶点相邻的顶点的列表。

**邻接矩阵**：邻接矩阵是大小为 V x V 的 2D 数组，其中 V 是图形中的顶点数。 假设 2D 数组为 adj [] []，则槽 adj [i] [j] = 1 表示从顶点 i 到顶点 j 有一条边。

请按照以下步骤将邻接列表转换为邻接矩阵：

*   用`0`s 初始化矩阵。
*   遍历邻接表中的顶点
*   对于邻接表中的每个 **j <sup>个</sup>** 顶点，遍历其边缘。
*   对于每个 **j <sup>第</sup>** 顶点具有边的顶点`i`，设置 mat [i] [j] = 1。

下面是上述方法的实现：

## C++

```cpp

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

## Java

```java

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

## Python

```py

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

## C#

```cs

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

**Output:** 

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
```

***时间复杂度**：O（N * M）*
***辅助空间**：O（N <sup>2</sup> ）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。