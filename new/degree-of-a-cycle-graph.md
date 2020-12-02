# 循环图的程度

> 原文： [https://www.geeksforgeeks.org/degree-of-a-cycle-graph/](https://www.geeksforgeeks.org/degree-of-a-cycle-graph/)

给定循环图中的顶点数。 任务是找到循环图的度数和边数。

**程度：**任何顶点的程度定义为其上的边缘入射数。

**循环图：**在图论中，由单个循环组成的图称为**循环图或圆形图**。 具有 n 个顶点的循环图称为 **Cn** 。

**循环图的属性：-**

*   它是一个连通图。
*   循环图或循环图是由单个循环组成的图。
*   在循环图中，顶点数等于边数。
*   当且仅当其具有偶数个顶点时，循环图才是 2 边可着色或 2 顶点可着色的。
*   当且仅当循环图的顶点数为奇数时，它才是 3 边可着色的或 3 边可着色的。
*   在循环图中，图中每个顶点的度为 2。
*   循环图的度为顶点数的 2 倍。 由于每个边缘被计数两次。

**示例：**

```
Input: Number of vertices = 4
Output: Degree is 8
        Edges are 4
Explanation: 
The total edges are 4 
and the Degree of the Graph is 8
as 2 edge incident on each of 
the vertices i.e on a, b, c, and d. 

Input: number of vertices = 5
Output: Degree is 10
        Edges are 5

```

下面是上述问题的实现：

**程序 1：**对于 4 个顶点的循环图

## C ++

```

// C++ implementation of above program. 

#include <bits/stdc++.h> 
using namespace std; 

// function that calculates the 
// number of Edge in a cycle graph. 
int getnumberOfEdges(int numberOfVertices) 
{ 
    int numberOfEdges = 0; 

    // The numberOfEdges of the cycle graph 
    // will be same as the numberOfVertices 
    numberOfEdges = numberOfVertices; 

    // return the numberOfEdges 
    return numberOfEdges; 
} 

// function that calculates the degree 
int getDegree(int numberOfVertices) 
{ 
    int degree; 

    // The degree of the cycle graph 
    // will be twice the numberOfVertices 
    degree = 2 * numberOfVertices; 

    // return the degree 
    return degree; 
} 

// Driver code 
int main() 
{ 

    // Get the number of vertices 
    int numberOfVertices = 4; 

    // Find the numberOfEdges and degree 
    // from the numberOfVertices 
    // and print the result 
    cout << "For numberOfVertices = "
         << numberOfVertices 
         << "\nDegree = "
         << getDegree(numberOfVertices) 
         << "\nNumber of Edges = "
         << getnumberOfEdges(numberOfVertices); 

    return 0; 
} 

```