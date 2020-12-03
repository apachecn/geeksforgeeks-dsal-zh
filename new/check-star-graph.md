# 检查星形图

> 原文： [https://www.geeksforgeeks.org/check-star-graph/](https://www.geeksforgeeks.org/check-star-graph/)

为您提供了一个 n * n 矩阵，该矩阵表示具有 n 个顶点的图，请检查输入矩阵是否表示星形图。

**示例**：

```
Input : Mat[][] = {{0, 1, 0},
                   {1, 0, 1},
                   {0, 1, 0}}
Output : Star graph

Input : Mat[][] = {{0, 1, 0},
                   {1, 1, 1},
                   {0, 1, 0}}
Output : Not a Star graph

```

**星图**：星图是一种特殊类型的图，其中 n-1 个顶点的度为 1，单个顶点的度为 n –1。这看起来像 n – 1 个顶点连接到单个中心 顶点。 总顶点数为 n 的星图称为 Sn。

这是星形图的说明：

![](img/66afe4002bf1240be604e5474800ea05.png)

**方法**：仅遍历整个矩阵并记录度为 1 和度为 n-1 的顶点数。 如果度为 1 的顶点数为 n-1，度为 n-1 的顶点数为 1，则我们的图应为星形图，否则应为星形图。

**注意**：

*   对于 S1，必须只有一个没有边的顶点。

*   对于 S2，必须有两个顶点，每个顶点的度数为 1，或者可以说，这两个顶点通过一条边连接。

*   对于 Sn（n> 2），只需检查上述标准即可。

## C++

```cpp

// CPP to find whether given graph is star or not 
#include<bits/stdc++.h> 
using namespace std; 

// define the size of incidence matrix 
#define size 4 

// function to find star graph 
bool checkStar(int mat[][size]) 
{ 
    // initialize number of vertex 
    // with deg 1 and n-1 
    int vertexD1 = 0, vertexDn_1 = 0; 

    // check for S1 
    if (size == 1) 
        return (mat[0][0] == 0); 

    // check for S2 
    if (size == 2)     
       return (mat[0][0] == 0 && mat[0][1] == 1 &&  
               mat[1][0] == 1 && mat[1][1] == 0 ); 

    // check for Sn (n>2) 
    for (int i = 0; i < size; i++) 
    { 
        int degreeI = 0; 
        for (int j = 0; j < size; j++) 
            if (mat[i][j]) 
                degreeI++; 

        if (degreeI == 1) 
            vertexD1++; 
        else if (degreeI == size-1) 
            vertexDn_1++; 
    } 

    return (vertexD1 == (size-1) &&  
            vertexDn_1 == 1); 
} 

// driver code 
int main() 
{ 
    int mat[size][size] = { {0, 1, 1, 1}, 
                            {1, 0, 0, 0}, 
                            {1, 0, 0, 0}, 
                            {1, 0, 0, 0}}; 

    checkStar(mat) ? cout << "Star Graph" :  
                     cout << "Not a Star Graph"; 
    return 0; 
} 

```

## Java

```java

// Java program to find whether  
// given graph is star or not 
import java.io.*; 

class GFG 
{ 
    // define the size of 
    // incidence matrix 
    static int size = 4; 

    // function to find 
    // star graph 
    static boolean checkStar(int mat[][]) 
    { 
        // initialize number of  
        // vertex with deg 1 and n-1 
        int vertexD1 = 0,  
            vertexDn_1 = 0; 

        // check for S1 
        if (size == 1) 
            return (mat[0][0] == 0); 

        // check for S2 
        if (size == 2)  
        return (mat[0][0] == 0 &&  
                mat[0][1] == 1 &&  
                mat[1][0] == 1 && 
                mat[1][1] == 0); 

        // check for Sn (n>2) 
        for (int i = 0; i < size; i++) 
        { 
            int degreeI = 0; 
            for (int j = 0; j < size; j++) 
                if (mat[i][j] == 1) 
                    degreeI++; 

            if (degreeI == 1) 
                vertexD1++; 
            else if (degreeI == size - 1) 
                vertexDn_1++; 
        } 

        return (vertexD1 == (size - 1) &&  
                vertexDn_1 == 1); 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int mat[][] = {{0, 1, 1, 1}, 
                       {1, 0, 0, 0}, 
                       {1, 0, 0, 0}, 
                       {1, 0, 0, 0}}; 

        if (checkStar(mat)) 
            System.out.print("Star Graph");  
        else
            System.out.print("Not a Star Graph"); 
    } 
} 

// This code is contributed by  
// Manish Shaw(manishshaw1) 

```

## Python

```py

# Python to find whether  
# given graph is star 
# or not 

# define the size  
# of incidence matrix 
size = 4

# def to  
# find star graph 
def checkStar(mat) : 

    global size 

    # initialize number of  
    # vertex with deg 1 and n-1 
    vertexD1 = 0
    vertexDn_1 = 0

    # check for S1 
    if (size == 1) : 
        return (mat[0][0] == 0) 

    # check for S2 
    if (size == 2) : 
        return (mat[0][0] == 0 and 
                mat[0][1] == 1 and 
                mat[1][0] == 1 and 
                mat[1][1] == 0) 

    # check for Sn (n>2) 
    for i in range(0, size) : 

        degreeI = 0
        for j in range(0, size) : 
            if (mat[i][j]) : 
                degreeI = degreeI + 1

        if (degreeI == 1) : 
            vertexD1 = vertexD1 + 1

        elif (degreeI == size - 1): 
            vertexDn_1 = vertexDn_1 + 1

    return (vertexD1 == (size - 1) and 
            vertexDn_1 == 1) 

# Driver code 
mat = [[0, 1, 1, 1], 
       [1, 0, 0, 0], 
       [1, 0, 0, 0], 
       [1, 0, 0, 0]] 

if(checkStar(mat)) : 
    print ("Star Graph") 
else : 
    print ("Not a Star Graph") 

# This code is contributed by  
# Manish Shaw(manishshaw1) 

```

## C#

```cs

// C# to find whether given 
// graph is star or not 
using System; 

class GFG 
{ 
    // define the size of 
    // incidence matrix 
    static int size = 4; 

    // function to find 
    // star graph 
    static bool checkStar(int [,]mat) 
    { 
        // initialize number of  
        // vertex with deg 1 and n-1 
        int vertexD1 = 0, vertexDn_1 = 0; 

        // check for S1 
        if (size == 1) 
            return (mat[0, 0] == 0); 

        // check for S2 
        if (size == 2)  
        return (mat[0, 0] == 0 &&  
                mat[0, 1] == 1 &&  
                mat[1, 0] == 1 && 
                mat[1, 1] == 0); 

        // check for Sn (n>2) 
        for (int i = 0; i < size; i++) 
        { 
            int degreeI = 0; 
            for (int j = 0; j < size; j++) 
                if (mat[i, j] == 1) 
                    degreeI++; 

            if (degreeI == 1) 
                vertexD1++; 
            else if (degreeI == size - 1) 
                vertexDn_1++; 
        } 

        return (vertexD1 == (size - 1) &&  
                vertexDn_1 == 1); 
    } 

    // Driver code 
    static void Main() 
    { 
        int [,]mat = new int[4, 4]{{0, 1, 1, 1}, 
                                   {1, 0, 0, 0}, 
                                   {1, 0, 0, 0}, 
                                   {1, 0, 0, 0}}; 

        if (checkStar(mat)) 
            Console.Write("Star Graph");  
        else
            Console.Write("Not a Star Graph"); 
    } 
} 
// This code is contributed by  
// Manish Shaw(manishshaw1) 

```

## 的 PHP

```

<?php 
// PHP to find whether  
// given graph is star 
// or not 

// define the size  
// of incidence matrix 
$size = 4; 

// function to  
// find star graph 
function checkStar($mat) 
{ 
    global $size; 

    // initialize number of  
    // vertex with deg 1 and n-1 
    $vertexD1 = 0; 
    $vertexDn_1 = 0; 

    // check for S1 
    if ($size == 1) 
        return ($mat[0][0] == 0); 

    // check for S2 
    if ($size == 2)  
    return ($mat[0][0] == 0 &&  
            $mat[0][1] == 1 &&  
            $mat[1][0] == 1 &&  
            $mat[1][1] == 0 ); 

    // check for Sn (n>2) 
    for ($i = 0; $i < $size; $i++) 
    { 
        $degreeI = 0; 
        for ($j = 0; $j < $size; $j++) 
            if ($mat[$i][$j]) 
                $degreeI++; 

        if ($degreeI == 1) 
            $vertexD1++; 
        else if ($degreeI == $size - 1) 
            $vertexDn_1++; 
    } 

    return ($vertexD1 == ($size - 1) &&  
            $vertexDn_1 == 1); 
} 

// Driver code 
$mat = array(array(0, 1, 1, 1), 
             array(1, 0, 0, 0), 
             array(1, 0, 0, 0), 
             array(1, 0, 0, 0)); 

if(checkStar($mat)) 
    echo ("Star Graph"); 
else
    echo ("Not a Star Graph"); 

// This code is contributed by  
// Manish Shaw(manishshaw1) 
?> 

```

**Output:**

```
Star Graph
```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。