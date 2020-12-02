# 查询顶点 X 和 Y 是否在无向图

的相同连接组件中

> 原文： [https://www.geeksforgeeks.org/queries-to-check-if-vertices-x-and-y-are-in-the-same-connected-component-of-an-undirected-graph/](https://www.geeksforgeeks.org/queries-to-check-if-vertices-x-and-y-are-in-the-same-connected-component-of-an-undirected-graph/)

给定**无向图**，该图由`N`个顶点和`M`个边组成，并查询类型为 **{X ，Y}** ，任务是检查顶点`X`和`Y`是否在图形的相同连接组件中。

**示例**：

> **输入**：Q [] [] = {{1，5}，{3，2}，{5，2}}
> 图：
> 
> ```
> 1-3-4   2
>   |
>   5   
> 
> ```
> 
> **输出**：是否否
> **说明**：
> 从给定的图中可以看出，顶点{1，5}在相同的连接组件中。
> 但是{3，2}和{5，2}来自不同的组件。
> **输入**：Q [] [] = {{1，9}，{2，8}，{3，5}，{7，9}}。
> 图：
> 
> ```
> 1-3-4  2-5-6  7-9
>        |
>        8   
> 
> ```
> 
> **输出**：否是否是
> **说明**：
> 从给定的图中可以看出，顶点{2，8}和{7，9}是 来自相同的连接组件。
> 但是{1，9}和{3，5}来自不同的组件。

**方法**：的想法是使用[不交集联合](https://www.geeksforgeeks.org/union-find/)解决该问题。 使用的不相交集并集数据结构的基本接口如下：

*   **make_set（v）**：创建一个由新元素 v 组成的新集合。
*   **find_set（v）**：返回包含元素 v 的集合的代表。使用[路径压缩对其进行优化。](https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/)
*   **union_set（a，b）**：合并两个指定的集合（元素所在的集合和元素 b 所在的集合）。 将两个连接的顶点合并以形成单个集合（连接的组件）。
*   最初，所有顶点都是不同的集合（即其自身的父对象），并使用 **make_set** 函数形成。
*   如果使用 **union_set** 功能连接了两个顶点，则这些顶点将合并。
*   现在，对于每个查询，使用 **find_set** 函数检查给定的两个顶点是否来自同一集合。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Maximum number of nodes or
// vertices that can be present
// in the graph
#define MAX_NODES 100005

// Store the parent of each vertex
int parent[MAX_NODES];

// Stores the size of each set
int size_set[MAX_NODES];

// Function to initialize the
// parent of each vertices
void make_set(int v)
{
    parent[v] = v;
    size_set[v] = 1;
}

// Function to find the representative
// of the set which contain element v
int find_set(int v)
{
    if (v == parent[v])
        return v;

    // Path compression technique to
    // optimize the time complexity
    return parent[v]
           = find_set(parent[v]);
}

// Function to merge two different set
// into a single set by finding the
// representative of each set and merge
// the smallest set with the larger one
void union_set(int a, int b)
{

    // Finding the set representative
    // of each element
    a = find_set(a);
    b = find_set(b);

    // Check if they have different set
    // repersentative
    if (a != b) {

        // Compare the set sizes
        if (size_set[a] < size_set[b])
            swap(a, b);

        // Assign parent of smaller set
        // to the larger one
        parent[b] = a;

        // Add the size of smaller set
        // to the larger one
        size_set[a] += size_set[b];
    }
}

// Function to check the vertices
// are on the same set or not
string check(int a, int b)
{
    a = find_set(a);
    b = find_set(b);

    // Check if they have same
    // set representative or not
    return (a == b) ? "Yes" : "No";
}

// Driver Code
int main()
{
    int n = 5, m = 3;

    make_set(1);
    make_set(2);
    make_set(3);
    make_set(4);
    make_set(5);

    // Connected vertices and taking
    // them into single set
    union_set(1, 3);
    union_set(3, 4);
    union_set(3, 5);

    // Number of queries
    int q = 3;

    // Function call
    cout << check(1, 5) << endl;
    cout << check(3, 2) << endl;
    cout << check(5, 2) << endl;

    return 0;
}

```

## Java

```java

// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Maximum number of nodes or
// vertices that can be present
// in the graph
static final int MAX_NODES = 100005;

// Store the parent of each vertex
static int []parent = new int[MAX_NODES];

// Stores the size of each set
static int []size_set = new int[MAX_NODES];

// Function to initialize the
// parent of each vertices
static void make_set(int v)
{
    parent[v] = v;
    size_set[v] = 1;
}

// Function to find the representative
// of the set which contain element v
static int find_set(int v)
{
    if (v == parent[v])
        return v;

    // Path compression technique to
    // optimize the time complexity
    return parent[v] = find_set(parent[v]);
}

// Function to merge two different set
// into a single set by finding the
// representative of each set and merge
// the smallest set with the larger one
static void union_set(int a, int b)
{

    // Finding the set representative
    // of each element
    a = find_set(a);
    b = find_set(b);

    // Check if they have different set
    // repersentative
    if (a != b) {

        // Compare the set sizes
        if (size_set[a] < size_set[b]) 
        {
            a = a+b;
            b = a-b;
            a = a-b;
        }

        // Assign parent of smaller set
        // to the larger one
        parent[b] = a;

        // Add the size of smaller set
        // to the larger one
        size_set[a] += size_set[b];
    }
}

// Function to check the vertices
// are on the same set or not
static String check(int a, int b)
{
    a = find_set(a);
    b = find_set(b);

    // Check if they have same
    // set representative or not
    return (a == b) ? "Yes" : "No";
}

// Driver Code
public static void main(String[] args)
{
    int n = 5, m = 3;

    make_set(1);
    make_set(2);
    make_set(3);
    make_set(4);
    make_set(5);

    // Connected vertices and taking
    // them into single set
    union_set(1, 3);
    union_set(3, 4);
    union_set(3, 5);

    // Number of queries
    int q = 3;

    // Function call
    System.out.print(check(1, 5) + "\n");
    System.out.print(check(3, 2) + "\n");
    System.out.print(check(5, 2) + "\n");
}
}

// This code is contributed by Rohit_ranjan

```

## Python3

```

# Python3 Program to implement
# the above approach

# Maximum number of nodes or
# vertices that can be present
# in the graph
MAX_NODES = 100005

# Store the parent of each vertex
parent = [0 for i in range(MAX_NODES)];

# Stores the size of each set
size_set = [0 for i in range(MAX_NODES)];

# Function to initialize the
# parent of each vertices
def make_set(v):

    parent[v] = v;
    size_set[v] = 1;

# Function to find the 
# representative of the 
# set which contain element v
def find_set(v):

    if (v == parent[v]):
        return v;

    # Path compression technique to
    # optimize the time complexity
    parent[v] = find_set(parent[v]);

    return parent[v]

# Function to merge two 
# different set into a 
# single set by finding the
# representative of each set 
# and merge the smallest set 
# with the larger one
def union_set(a, b):

    # Finding the set 
    # representative 
    # of each element
    a = find_set(a);
    b = find_set(b);

    # Check if they have 
    # different set 
    # repersentative
    if (a != b):

        # Compare the set sizes
        if (size_set[a] < 
            size_set[b]):
            swap(a, b);

        # Assign parent of 
        # smaller set to 
        # the larger one
        parent[b] = a;

        # Add the size of smaller set
        # to the larger one
        size_set[a] += size_set[b];

# Function to check the vertices
# are on the same set or not
def check(a, b):

    a = find_set(a);
    b = find_set(b);

    # Check if they have same
    # set representative or not
    if a == b:
        return ("Yes")
    else:
        return ("No")

# Driver code      
if __name__=="__main__":

    n = 5
    m = 3;

    make_set(1);
    make_set(2);
    make_set(3);
    make_set(4);
    make_set(5);

    # Connected vertices 
    # and taking them 
    # into single set
    union_set(1, 3);
    union_set(3, 4);
    union_set(3, 5);

    # Number of queries
    q = 3;

    # Function call
    print(check(1, 5))
    print(check(3, 2))
    print(check(5, 2))

# This code is contributed by rutvik_56

```

## C#

```cs

// C# program to implement
// the above approach
using System;

class GFG{

// Maximum number of nodes or
// vertices that can be present
// in the graph
static readonly int MAX_NODES = 100005;

// Store the parent of each vertex
static int []parent = new int[MAX_NODES];

// Stores the size of each set
static int []size_set = new int[MAX_NODES];

// Function to initialize the
// parent of each vertices
static void make_set(int v)
{
    parent[v] = v;
    size_set[v] = 1;
}

// Function to find the representative
// of the set which contain element v
static int find_set(int v)
{
    if (v == parent[v])
        return v;

    // Path compression technique to
    // optimize the time complexity
    return parent[v] = find_set(parent[v]);
}

// Function to merge two different set
// into a single set by finding the
// representative of each set and merge
// the smallest set with the larger one
static void union_set(int a, int b)
{

    // Finding the set representative
    // of each element
    a = find_set(a);
    b = find_set(b);

    // Check if they have different set
    // repersentative
    if (a != b)
    {

        // Compare the set sizes
        if (size_set[a] < size_set[b]) 
        {
            a = a + b;
            b = a - b;
            a = a - b;
        }

        // Assign parent of smaller set
        // to the larger one
        parent[b] = a;

        // Add the size of smaller set
        // to the larger one
        size_set[a] += size_set[b];
    }
}

// Function to check the vertices
// are on the same set or not
static String check(int a, int b)
{
    a = find_set(a);
    b = find_set(b);

    // Check if they have same
    // set representative or not
    return (a == b) ? "Yes" : "No";
}

// Driver Code
public static void Main(String[] args)
{
    //int n = 5, m = 3;

    make_set(1);
    make_set(2);
    make_set(3);
    make_set(4);
    make_set(5);

    // Connected vertices and taking
    // them into single set
    union_set(1, 3);
    union_set(3, 4);
    union_set(3, 5);

    // Number of queries
    //int q = 3;

    // Function call
    Console.Write(check(1, 5) + "\n");
    Console.Write(check(3, 2) + "\n");
    Console.Write(check(5, 2) + "\n");
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
Yes
No
No

```

***时间复杂度**：O（N + M + sizeof（Q））*
***辅助空间**：O（N）*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。