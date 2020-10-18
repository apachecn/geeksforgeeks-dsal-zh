# 程序检查矩阵是否为下三角

> 原文： [https://www.geeksforgeeks.org/program-check-matrix-lower-triangular/](https://www.geeksforgeeks.org/program-check-matrix-lower-triangular/)

给定一个正方形矩阵，任务是检查矩阵是否为下三角形式。 如果主对角线上的所有条目均为零，则将方阵称为下三角。

![](img/b3f690fdbca6e40250267197f2d13abe.png)

示例：

```
Input : mat[4][4] = {{1, 0, 0, 0},
                     {1, 4, 0, 0},
                     {4, 6, 2, 0},
                     {0, 4, 7, 6}};
Output : Matrix is in lower triangular form.

Input : mat[4][4] = {{1, 0, 0, 0},
                     {4, 3, 0, 1},
                     {7, 9, 2, 0},
                     {8, 5, 3, 6}};
Output : Matrix is not in lower triangular form.

```



## C++ 

```cpp

// Program to check lower 
// triangular matrix. 
#include <bits/stdc++.h> 
#define N 4 
using namespace std; 

// Function to check matrix is in  
// lower triangular form or not. 
bool isLowerTriangularMatrix(int mat[N][N]) 
{ 
    for (int i = 0; i < N; i++) 
        for (int j = i + 1; j < N; j++) 
            if (mat[i][j] != 0) 
                return false; 
    return true; 
} 

// Driver function. 
int main() 
{ 
    int mat[N][N] = { { 1, 0, 0, 0 }, 
                      { 1, 4, 0, 0 }, 
                      { 4, 6, 2, 0 }, 
                      { 0, 4, 7, 6 } }; 

    // Function call 
    if (isLowerTriangularMatrix(mat)) 
        cout << "Yes"; 
    else
        cout << "No"; 
    return 0; 
} 

```

## Java

```java

// Java Program to check for  
// a lower triangular matrix. 
import java.io.*; 

class Lower_triangular 
{ 
    int N = 4; 

    // Function to check matrix is  
    // in lower triangular form or not. 
    boolean isLowerTriangularMatrix(int mat[][]) 
    { 
        for (int i = 0; i < N; i++) 
            for (int j = i + 1; j < N; j++) 
                if (mat[i][j] != 0) 
                    return false; 

        return true; 
    } 

    // Driver function. 
    public static void main(String args[]) 
    { 
        Lower_triangular ob = new Lower_triangular(); 
        int mat[][] = { { 1, 0, 0, 0 }, 
                        { 1, 4, 0, 0 }, 
                        { 4, 6, 2, 0 }, 
                        { 0, 4, 7, 6 } }; 

        // Function call 
        if (ob.isLowerTriangularMatrix(mat)) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 
} 

// This code is contributed by Anshika Goyal. 

```

## Python3

```py

# Python3 Program to check  
# lower triangular matrix. 

# Function to check matrix  
# is in lower triangular 
def islowertriangular(M): 
    for i in range(0, len(M)): 
        for j in range(i + 1, len(M)): 
            if(M[i][j] != 0):  
                    return False
    return True

# Driver function. 
M = [[1,0,0,0], 
     [1,4,0,0], 
     [4,6,2,0], 
     [0,4,7,6]] 

if islowertriangular(M): 
    print ("Yes") 
else: 
    print ("No") 

# This code is contributed by Anurag Rawat 

```

## C# 

```cs

// C# program to check for 
// a lower triangular matrix. 
using System; 

class Lower_triangular  
{ 
    int N = 4; 

    // Function to check matrix is 
    // in lower triangular form or not. 
    bool isLowerTriangularMatrix(int[, ] mat) 
    { 
        for (int i = 0; i < N; i++) 
            for (int j = i + 1; j < N; j++) 
                if (mat[i, j] != 0) 
                    return false; 

        return true; 
    } 

    // Driver function. 
    public static void Main() 
    { 
        Lower_triangular ob = new Lower_triangular(); 
        int[, ] mat = { { 1, 0, 0, 0 }, 
                        { 1, 4, 0, 0 }, 
                        { 4, 6, 2, 0 }, 
                        { 0, 4, 7, 6 } }; 

        // Function call 
        if (ob.isLowerTriangularMatrix(mat)) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP Program to check lower 
// triangular matrix. 
$N = 4; 

// Function to check matrix is in  
// lower triangular form or not. 
function isLowerTriangularMatrix($mat) 
{ 
    global $N; 
    for ($i = 0; $i < $N; $i++) 
        for ($j = $i + 1; $j < $N; $j++) 
            if ($mat[$i][$j] != 0) 
                return false; 
    return true; 
} 

// Driver Code 
$mat = array(array( 1, 0, 0, 0 ), 
             array( 1, 4, 0, 0 ), 
             array( 4, 6, 2, 0 ), 
             array( 0, 4, 7, 6 ));  

// Function call 
if (isLowerTriangularMatrix($mat)) 
    echo("Yes"); 
else
    echo("No"); 

// This code is contributed by Ajit. 
?> 

```

Output:

```
Yes

```



* * *

* * *



