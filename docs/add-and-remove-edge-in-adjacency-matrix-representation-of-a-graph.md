# 在图的邻接矩阵表示中添加和移除边

> 原文:[https://www . geesforgeks . org/添加和移除邻接矩阵中的边-图的表示/](https://www.geeksforgeeks.org/add-and-remove-edge-in-adjacency-matrix-representation-of-a-graph/)

**先决条件:** [图及其表示](https://www.geeksforgeeks.org/graph-and-its-representations/)
给定由 N 个顶点组成的图的邻接矩阵**g【】【】**，任务是在插入所有**边【】**并移除顶点之间的边 **(X，Y)** 后修改矩阵。在邻接矩阵中，如果图的顶点 **i** 和 **j** 之间存在边，则 **g[i][j] = 1** 和 **g[j][i] = 1** 。如果这两个顶点之间不存在边，则 **g[i][j] = 0** 和 **g[j][i] = 0** 。

**示例:**

> **输入:** N = 6，边[] = {{0，1}，{0，2}，{0，3}，{0，4}，{1，3}，{2，3}，{2，4}，{2，5}，{3，5}}，X = 2， Y = 3
> **输出:**
> 边插入后的邻接矩阵:
> 0 1 1 1 1 0 1 0 0
> 1 0 1 0 1 1 1 1
> 1 1 1 0 0 1
> 1 0 1 0 0 0
> 0 1 0 0
> 边移除后的邻接矩阵:
> 0 1 1 1 1 1 0
> 1 0 1 0 0 0
> 1 0 0 1 1
> 1 1 0 0 1
> 1 0 1 0 0 0 0
> 0 0 1 0 0
> **说明:**
> 插入边后的图及对应的邻接矩阵:
> 
> [![](img/580ed075f2239e7f65e9cd0bb80ce7d0.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200604170814/add-and-remove-edge-in-adjacency-matrix-representation-initial1.jpg)
> 
> 顶点 **X** 和 **Y** 之间的去除后图和去除边缘后的邻接矩阵:
> 
> [![](img/4a5227e1561475c95d93608fc1ed2a11.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200604170842/add-and-remove-edge-in-adjacency-matrix-representation-final2.jpg)
> 
> **输入:** N = 6，边[] = {{0，1}，{0，2}，{0，3}，{0，4}，{1，3}，{2，3}，{2，4}，{2，5}，{3，5}}，X = 3， Y = 5
> **输出:**
> 边插入后的邻接矩阵:
> 0 1 1 1 1 0 1 0 0
> 1 0 1 0 1 1 1 1
> 1 1 1 0 0 1
> 1 0 1 0 0 0
> 0 1 0 1 0
> 边移除后的邻接矩阵:
> 0 1 1 1 1 1 0
> 1 0 1 0 0 0
> 1 0 1 1 1 1
> 1 1 0 0 0
> 1 0 1 0 0 0
> 0 1 0 0 0 0

**方法:**
初始化维度矩阵 **N x N** 并按照以下步骤操作:

*   **插入边:**要在两个顶点之间插入边，假设 **i** 和 **j** ，如果两个顶点 **i** 和 **j** 都存在，则将邻接矩阵中的对应值设置为 1，即*T7】g【I】j = 1T9】和*T11】g【j】I = 1*。*
*   **移除边:**要移除两个顶点之间的边，假设 **i** 和 **j** ，将邻接矩阵中的相应值设置为 0。即如果顶点 **i** 和 **j** 都存在，则设置 ***g[i][j]=0*** 和 ***g[j][i]=0*** 。

下面是上述方法的实现:

## C++

```
// C++ program to add and remove edge
// in the adjacency matrix of a graph

#include <iostream>
using namespace std;

class Graph {
private:
    // Number of vertices
    int n;

    // Adjacency matrix
    int g[10][10];

public:
    // Constructor
    Graph(int x)
    {
        n = x;

        // Initializing each element of the
        // adjacency matrix to zero
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                g[i][j] = 0;
            }
        }
    }

    // Function to display adjacency matrix
    void displayAdjacencyMatrix()
    {
        // Displaying the 2D matrix
        for (int i = 0; i < n; i++) {
            cout << "\n";
            for (int j = 0; j < n; j++) {
                cout << " " << g[i][j];
            }
        }
    }

    // Function to update adjacency
    // matrix for edge insertion
    void addEdge(int x, int y)
    {
        // Checks if the vertices
        // exist in the graph
        if ((x < 0) || (x >= n)) {
            cout << "Vertex" << x
                 << " does not exist!";
        }
        if ((y < 0) || (y >= n)) {
            cout << "Vertex" << y
                 << " does not exist!";
        }

        // Checks if it is a self edge
        if (x == y) {
            cout << "Same Vertex!";
        }

        else {
            // Insert edge
            g[y][x] = 1;
            g[x][y] = 1;
        }
    }

    // Function to update adjacency
    // matrix for edge removal
    void removeEdge(int x, int y)
    {
        // Checks if the vertices
        // exist in the graph
        if ((x < 0) || (x >= n)) {
            cout << "Vertex" << x
                 << " does not exist!";
        }
        if ((y < 0) || (y >= n)) {
            cout << "Vertex" << y
                 << " does not exist!";
        }

        // Checks if it is a self edge
        if (x == y) {
            cout << "Same Vertex!";
        }

        else {
            // Remove edge
            g[y][x] = 0;
            g[x][y] = 0;
        }
    }
};

// Driver Code
int main()
{
    int N = 6, X = 2, Y = 3;

    Graph obj(N);

    // Adding edges to the graph
    obj.addEdge(0, 1);
    obj.addEdge(0, 2);
    obj.addEdge(0, 3);
    obj.addEdge(0, 4);
    obj.addEdge(1, 3);
    obj.addEdge(2, 3);
    obj.addEdge(2, 4);
    obj.addEdge(2, 5);
    obj.addEdge(3, 5);

    cout << "Adjacency matrix after"
         << " edge insertions:\n";
    obj.displayAdjacencyMatrix();

    obj.removeEdge(X, Y);

    cout << "\nAdjacency matrix after"
         << " edge removal:\n";
    obj.displayAdjacencyMatrix();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to add and remove edge
// in the adjacency matrix of a graph

class Graph {

    // Number of vertices
    private int n;

    // Adjacency matrix
    private int[][] g = new int[10][10];

    // Constructor
    Graph(int x)
    {
        this.n = x;

        // Initializing each element of the
        // adjacency matrix to zero
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n; ++j) {
                g[i][j] = 0;
            }
        }
    }

    // Function to display adjacency matrix
    public void displayAdjacencyMatrix()
    {
        // Displaying the 2D matrix
        for (int i = 0; i < n; ++i) {
            System.out.println();
            for (int j = 0; j < n; ++j) {
                System.out.print(" " + g[i][j]);
            }
        }

        System.out.println();
    }

    // Function to update adjacency
    // matrix for edge insertion
    public void addEdge(int x, int y)
    {
        // Checks if the vertices exists
        if ((x < 0) || (x >= n)) {
            System.out.printf("Vertex " + x
                              + " does not exist!");
        }
        if ((y < 0) || (y >= n)) {
            System.out.printf("Vertex " + y
                              + " does not exist!");
        }

        // Checks if it is a self edge
        if (x == y) {
            System.out.println("Same Vertex!");
        }

        else {
            // Insert edge
            g[y][x] = 1;
            g[x][y] = 1;
        }
    }

    // Function to update adjacency
    // matrix for edge removal
    public void removeEdge(int x, int y)
    {
        // Checks if the vertices exists
        if ((x < 0) || (x >= n)) {
            System.out.printf("Vertex " + x
                              + " does not exist!");
        }
        if ((y < 0) || (y >= n)) {
            System.out.printf("Vertex " + y
                              + " does not exist!");
        }

        // Checks if it is a self edge
        if (x == y) {
            System.out.println("Same Vertex!");
        }

        else {
            // Remove edge
            g[y][x] = 0;
            g[x][y] = 0;
        }
    }
}

// Driver Code
class Main {
    public static void main(String[] args)
    {

        int N = 6, X = 2, Y = 3;
        Graph obj = new Graph(N);

        // Inserting edges
        obj.addEdge(0, 1);
        obj.addEdge(0, 2);
        obj.addEdge(0, 3);
        obj.addEdge(0, 4);
        obj.addEdge(1, 3);
        obj.addEdge(2, 3);
        obj.addEdge(2, 4);
        obj.addEdge(2, 5);
        obj.addEdge(3, 5);

        System.out.println("Adjacency matrix after"
                           + " edge insertions:");
        obj.displayAdjacencyMatrix();

        obj.removeEdge(2, 3);

        System.out.println("\nAdjacency matrix after"
                           + " edge removal:");
        obj.displayAdjacencyMatrix();
    }
}
```

## 蟒蛇 3

```
# Python3 program to add and remove edge
# in adjacency matrix representation of a graph

class Graph:

    # Number of vertices
    __n = 0

    # Adjacency matrix
    __g = [[0 for x in range(10)]
              for y in range(10)]

    # Constructor
    def __init__(self, x):
        self.__n = x

        # Initializing each element of
        # the adjacency matrix to zero
        for i in range(0, self.__n):
            for j in range(0, self.__n):
                self.__g[i][j] = 0

    # Function to display adjacency matrix            
    def displayAdjacencyMatrix(self):

        # Displaying the 2D matrix
        for i in range(0, self.__n):
            print()
            for j in range(0, self.__n):
                print("", self.__g[i][j], end = "")

    # Function to update adjacency
    # matrix for edge insertion            
    def addEdge(self, x, y):

        # Checks if the vertices
        # exist in the graph
        if (x < 0) or (x >= self.__n):
            print("Vertex {} does not exist!".format(x))
        if (y < 0) or (y >= self.__n):
            print("Vertex {} does not exist!".format(y))

        # Checks if it is a self edge
        if(x == y):
            print("Same Vertex!")

        else:

            # Adding edge between the vertices
            self.__g[y][x] = 1
            self.__g[x][y] = 1

    # Function to update adjacency
    # matrix for edge removal        
    def removeEdge(self, x, y):

        # Checks if the vertices
        # exist in the graph
        if (x < 0) or (x >= self.__n):
            print("Vertex {} does not exist!".format(x))
        if (y < 0) or (y >= self.__n):
            print("Vertex {} does not exist!".format(y))

        # Checks if it is a self edge
        if(x == y):
            print("Same Vertex!")

        else:

            # Remove edge from between
            # the vertices
            self.__g[y][x] = 0
            self.__g[x][y] = 0

# Driver code   

# Creating an object of class Graph
obj = Graph(6);

# Adding edges to the graph
obj.addEdge(0, 1)
obj.addEdge(0, 2)
obj.addEdge(0, 3)
obj.addEdge(0, 4)
obj.addEdge(1, 3)
obj.addEdge(2, 3)
obj.addEdge(2, 4)
obj.addEdge(2, 5)
obj.addEdge(3, 5)

# Edges added to the adjacency matrix
print("Adjacency matrix after "
      "edge insertions:\n")
obj.displayAdjacencyMatrix();

# Removing the edge between vertices
# "2" and "3" from the graph
obj.removeEdge(2, 3);

# The adjacency matrix after
# removing the edge
print("\nAdjacency matrix after "
      "edge removal:\n")
obj.displayAdjacencyMatrix();

# This code is contributed by amarjeet_singh
```

## C#

```
// C# program to add and remove edge
// in adjacency matrix representation
// of a graph
using System;

class Graph{

// Number of vertices
private int n;

// Adjacency matrix
private int[,] g = new int[10, 10];

// Constructor
public Graph(int x)
{
    this.n = x;

    // Initializing each element of
    // the adjacency matrix to zero
    for(int i = 0; i < n; ++i)
    {
        for(int j = 0; j < n; ++j)
        {
            g[i, j] = 0;
        }
    }
}

// Function to display adjacency matrix
public void displayAdjacencyMatrix()
{

    // Displaying the 2D matrix
    for(int i = 0; i < n; ++i)
    {
        Console.WriteLine();
        for(int j = 0; j < n; ++j)
        {
            Console.Write(" " + g[i, j]);
        }
    }
}

// Function to update adjacency
// matrix for edge insertion
public void addEdge(int x, int y)
{

    // Checks if the vertices exist
    // in the graph
    if ((x < 0) || (x >= n))
    {
        Console.WriteLine("Vertex {0} does " +
                          "not exist!", x);
    }
    if ((y < 0) || (y >= n))
    {
        Console.WriteLine("Vertex {0} does " +
                          "not exist!", y);
    }

    // Checks if it is a self edge
    if (x == y)
    {
        Console.WriteLine("Same Vertex!");
    }

    else
    {

        // Adding edge between the vertices
        g[y, x] = 1;
        g[x, y] = 1;
    }
}

// Function to update adjacency
// matrix for edge removal
public void removeEdge(int x, int y)
{

    // Checks if the vertices exist
    // in the graph
    if ((x < 0) || (x >= n))
    {
        Console.WriteLine("Vertex {0} does" +
                          "not exist!", x);
    }
    if ((y < 0) || (y >= n))
    {
        Console.WriteLine("Vertex {0} does" +
                          "not exist!", y);
    }

    // Checks if it is a self edge
    if (x == y)
    {
        Console.WriteLine("Same Vertex!");
    }

    else
    {

        // Remove edge from between
        // the vertices
        g[y, x] = 0;
        g[x, y] = 0;
    }
}
}

class GFG{

// Driver code
public static void Main(String[] args)
{

    // Creating an object of class Graph
    Graph obj = new Graph(6);

    // Adding edges to the graph
    obj.addEdge(0, 1);
    obj.addEdge(0, 2);
    obj.addEdge(0, 3);
    obj.addEdge(0, 4);
    obj.addEdge(1, 3);
    obj.addEdge(2, 3);
    obj.addEdge(2, 4);
    obj.addEdge(2, 5);
    obj.addEdge(3, 5);

    // Edges added to the adjacency matrix
    Console.WriteLine("Adjacency matrix after " +
                      "edge insertions:\n");
    obj.displayAdjacencyMatrix();

    // Removing the edge between vertices
    // "2" and "3" from the graph
    obj.removeEdge(2, 3);

    // The adjacency matrix after
    // removing the edge
    Console.WriteLine("\nAdjacency matrix after " +
                      "edge removal:");
    obj.displayAdjacencyMatrix();
}
}

// This code is contributed by amarjeet_singh
```

## java 描述语言

```
<script>

// Javascript program to add and remove edge
// in adjacency matrix representation
// of a graph

// Number of vertices
var n = 0;

// Adjacency matrix
var g = Array.from(Array(10), ()=>Array(10).fill(0));

// Constructor
function initialize(x)
{
    n = x;

    // Initializing each element of
    // the adjacency matrix to zero
    for(var i = 0; i < n; ++i)
    {
        for(var j = 0; j < n; ++j)
        {
            g[i][j] = 0;
        }
    }
}

// Function to display adjacency matrix
function displayAdjacencyMatrix()
{

    // Displaying the 2D matrix
    for(var i = 0; i < n; ++i)
    {
        document.write("<br>");
        for(var j = 0; j < n; ++j)
        {
            document.write(" " + g[i][j]);
        }
    }
}

// Function to update adjacency
// matrix for edge insertion
function addEdge(x, y)
{

    // Checks if the vertices exist
    // in the graph
    if ((x < 0) || (x >= n))
    {
        document.write(`Vertex ${x} does not exist!`);
    }
    if ((y < 0) || (y >= n))
    {
        document.write(`Vertex ${y} does not exist!`);
    }

    // Checks if it is a self edge
    if (x == y)
    {
        document.write("Same Vertex!<br>");
    }

    else
    {

        // Adding edge between the vertices
        g[y][x] = 1;
        g[x][y] = 1;
    }
}

// Function to update adjacency
// matrix for edge removal
function removeEdge(x, y)
{

    // Checks if the vertices exist
    // in the graph
    if ((x < 0) || (x >= n))
    {
        document.write(`Vertex ${x} does not exist!`);
    }
    if ((y < 0) || (y >= n))
    {
        document.write(`Vertex ${y} does not exist!`);
    }

    // Checks if it is a self edge
    if (x == y)
    {
        document.write("Same Vertex!<br>");
    }

    else
    {

        // Remove edge from between
        // the vertices
        g[y][x] = 0;
        g[x][y] = 0;
    }
}

// Driver code
// Creating an object of class Graph
initialize(6);
// Adding edges to the graph
addEdge(0, 1);
addEdge(0, 2);
addEdge(0, 3);
addEdge(0, 4);
addEdge(1, 3);
addEdge(2, 3);
addEdge(2, 4);
addEdge(2, 5);
addEdge(3, 5);
// Edges added to the adjacency matrix
document.write("Adjacency matrix after " +
                  "edge insertions:<br>");
displayAdjacencyMatrix();
// Removing the edge between vertices
// "2" and "3" from the graph
removeEdge(2, 3);

// The adjacency matrix after
// removing the edge
document.write("<br>Adjacency matrix after " +
                  "edge removal:<br>");
displayAdjacencyMatrix();

</script>
```

**Output:** 

```
Adjacency matrix after edge insertions:

 0 1 1 1 1 0
 1 0 0 1 0 0
 1 0 0 1 1 1
 1 1 1 0 0 1
 1 0 1 0 0 0
 0 0 1 1 0 0
Adjacency matrix after edge removal:

 0 1 1 1 1 0
 1 0 0 1 0 0
 1 0 0 0 1 1
 1 1 0 0 0 1
 1 0 1 0 0 0
 0 0 1 1 0 0
```

***时间复杂度:**边的插入和删除需要 O(1)个复杂度，而显示邻接矩阵需要 O(N <sup>2</sup> )。*
***辅助空间:** O(N <sup>2</sup> )*