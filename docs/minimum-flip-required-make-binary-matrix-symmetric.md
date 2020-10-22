# 使二进制矩阵对称所需的最小翻转

> 原文： [https://www.geeksforgeeks.org/minimum-flip-required-make-binary-matrix-symmetric/](https://www.geeksforgeeks.org/minimum-flip-required-make-binary-matrix-symmetric/)

给定大小为`N X N`的二进制矩阵，由 1 和 0 组成。 任务是找到使矩阵沿[主对角线](https://en.wikipedia.org/wiki/Main_diagonal)对称所需的最小翻转。

**示例**：

```
Input : mat[][] = { { 0, 0, 1 },
                    { 1, 1, 1 },
                    { 1, 0, 0 } };
Output : 2
Value of mat[1][0] is not equal to mat[0][1].
Value of mat[2][1] is not equal to mat[1][2].
So, two flip are required.

Input : mat[][] = { { 1, 1, 1, 1, 0 },
                    { 0, 1, 0, 1, 1 },
                    { 1, 0, 0, 0, 1 },
                    { 0, 1, 0, 1, 0 },
                    { 0, 1, 0, 0, 1 } };                  
Output : 3

```



**方法 1（简单）**：

这个想法是找到矩阵的转置并找到使转置和原始矩阵相等所需的最小翻转次数。 要找到最小翻转，请找到原始矩阵和转置矩阵不相同的位置数，例如`x`。 因此，我们的答案将是`x / 2`。

以下是此方法的实现：

## C++ 

```cpp

// CPP Program to find minimum flip required to make 
// Binary Matrix symmetric along main diagonal 
#include <bits/stdc++.h> 
#define N 3 
using namespace std; 

// Return the minimum flip required to make 
// Binary Matrix symmetric along main diagonal. 
int minimumflip(int mat[][N], int n) 
{ 
    int transpose[n][n]; 

    // finding the transpose of the matrix 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < n; j++) 
            transpose[i][j] = mat[j][i]; 

    // Finding the number of position where 
    // element are not same. 
    int flip = 0; 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < n; j++) 
            if (transpose[i][j] != mat[i][j]) 
                flip++; 

    return flip / 2; 
} 

// Driver Program 
int main() 
{ 
    int n = 3; 
    int mat[N][N] = { 
        { 0, 0, 1 }, 
        { 1, 1, 1 }, 
        { 1, 0, 0 } 
    }; 
    cout << minimumflip(mat, n) << endl; 
    return 0; 
} 

```

## Java

```java
// Java Program to find minimum flip 
// required to make Binary Matrix 
// symmetric along main diagonal 
import java.util.*; 
  
class GFG { 
      
    // Return the minimum flip required 
    // to make Binary Matrix symmetric 
    // along main diagonal. 
    static int minimumflip(int mat[][], int n) 
    { 
        int transpose[][] = new int[n][n]; 
       
        // finding the transpose of the matrix 
        for (int i = 0; i < n; i++) 
            for (int j = 0; j < n; j++) 
                transpose[i][j] = mat[j][i]; 
       
        // Finding the number of position  
        // where element are not same. 
        int flip = 0; 
        for (int i = 0; i < n; i++) 
            for (int j = 0; j < n; j++) 
                if (transpose[i][j] != mat[i][j]) 
                    flip++; 
       
        return flip / 2; 
    } 
      
    /* Driver program to test above function */
    public static void main(String[] args)  
    { 
        int n = 3; 
        int mat[][] = {{ 0, 0, 1 }, 
                       { 1, 1, 1 }, 
                       { 1, 0, 0 }}; 
          
        System.out.println(minimumflip(mat, n)); 
    } 
} 
      
// This code is contributed by Arnav Kr. Mandal.
```

## Python3

```py
# Python3 code to find minimum flip 
# required to make Binary Matrix  
# symmetric along main diagonal 
N = 3
  
# Return the minimum flip required  
# to make Binary Matrix symmetric 
# along main diagonal. 
def minimumflip(mat, n): 
      
    transpose =[[0] * n] * n 
      
    # finding the transpose of the matrix 
    for i in range(n): 
        for j in range(n): 
            transpose[i][j] = mat[j][i] 
      
    # Finding the number of position  
    # where element are not same. 
    flip = 0
    for i in range(n): 
        for j in range(n): 
            if transpose[i][j] != mat[i][j]: 
                flip += 1
      
    return int(flip / 2) 
      
# Driver Program 
n = 3
mat =[[ 0, 0, 1], 
      [ 1, 1, 1], 
      [ 1, 0, 0]] 
print( minimumflip(mat, n)) 
  
# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```cs
// C# Program to find minimum flip 
// required to make Binary Matrix 
// symmetric along main diagonal 
using System; 
  
class GFG { 
      
    // Return the minimum flip required 
    // to make Binary Matrix symmetric 
    // along main diagonal. 
    static int minimumflip(int [,]mat, int n) 
    { 
        int [,]transpose = new int[n,n]; 
      
        // finding the transpose of the matrix 
        for (int i = 0; i < n; i++) 
            for (int j = 0; j < n; j++) 
                transpose[i,j] = mat[j,i]; 
      
        // Finding the number of position  
        // where element are not same. 
        int flip = 0; 
        for (int i = 0; i < n; i++) 
            for (int j = 0; j < n; j++) 
                if (transpose[i,j] != mat[i,j]) 
                    flip++; 
      
        return flip / 2; 
    } 
      
    /* Driver program to test above function */
    public static void Main()  
    { 
        int n = 3; 
        int [,]mat = {{ 0, 0, 1 }, 
                      { 1, 1, 1 }, 
                      { 1, 0, 0 }}; 
          
        Console.WriteLine(minimumflip(mat, n)); 
    } 
} 
      
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// PHP Program to find minimum 
// flip required to make 
$N = 3; 
  
// Return the minimum flip  
// required to make Binary  
// Matrix symmetric along  
// main diagonal. 
function minimumflip($mat, $n) 
{ 
    global $N; 
    $transpose; 
  
    // finding the transpose 
    // of the matrix 
    for ( $i = 0; $i < $n; $i++) 
        for ($j = 0; $j < $n; $j++) 
            $transpose[$i][$j] = $mat[$j][$i]; 
  
    // Finding the number of  
    // position where element 
    // are not same. 
    $flip = 0; 
    for ( $i = 0; $i < $n; $i++) 
        for ( $j = 0; $j < $n; $j++) 
            if ($transpose[$i][$j] != $mat[$i][$j]) 
                $flip++; 
  
    return $flip / 2; 
} 
  
// Driver Code 
$n = 3; 
$mat = array(array(0, 0, 1), 
             array(1, 1, 1), 
             array(1, 0, 0)); 
  
echo minimumflip($mat, $n),"\n"; 
  
// This code is contributed by aj_36 
?>
```

输出：

```
2
```

方法 2（有效方法）：

这个想法是找到使矩阵的上三角等于矩阵的下三角所需的最小翻转。 为此，我们运行两个嵌套循环，即从`i = 0`到`n`的外循环，即矩阵的每一行，以及从`j = 0`到`i`的内循环，并检查`mat[i][j]`是否等于`mat[j][i]`。 其中不等于的实例数将是使矩阵沿主对角线对称的最小翻转次数。

以下是此方法的实现：

## C++

```cpp
// CPP Program to find minimum flip required to make 
// Binary Matrix symmetric along main diagonal 
#include <bits/stdc++.h> 
#define N 3 
using namespace std; 
  
// Return the minimum flip required to make 
// Binary Matrix symmetric along main diagonal. 
int minimumflip(int mat[][N], int n) 
{ 
    // Comparing elements across diagonal 
    int flip = 0; 
    for (int i = 0; i < n; i++) 
        for (int j = 0; j < i; j++) 
            if (mat[i][j] != mat[j][i]) 
                flip++; 
    return flip; 
} 
  
// Driver Program 
int main() 
{ 
    int n = 3; 
    int mat[N][N] = { 
        { 0, 0, 1 }, 
        { 1, 1, 1 }, 
        { 1, 0, 0 } 
    }; 
    cout << minimumflip(mat, n) << endl; 
    return 0; 
}
```

## Java

```java
// Java Program to find minimum flip 
// required to make Binary Matrix 
// symmetric along main diagonal 
import java.util.*; 
  
class GFG { 
      
    // Return the minimum flip required  
    // to make Binary Matrix symmetric 
    // along main diagonal. 
    static int minimumflip(int mat[][], int n) 
    { 
        // Comparing elements across diagonal 
        int flip = 0; 
        for (int i = 0; i < n; i++) 
            for (int j = 0; j < i; j++) 
                if (mat[i][j] != mat[j][i]) 
                    flip++; 
        return flip; 
    } 
      
    /* Driver program to test above function */
    public static void main(String[] args)  
    { 
        int n = 3; 
        int mat[][] = {{ 0, 0, 1 }, 
                       { 1, 1, 1 }, 
                       { 1, 0, 0 }}; 
          
       System.out.println(minimumflip(mat, n)); 
    } 
} 
      
// This code is contributed by Arnav Kr. Mandal.
```

## Python3

```py
# Python3 code to find minimum flip 
# required to make Binary Matrix 
# symmetric along main diagonal 
N = 3
  
# Return the minimum flip required 
# to make Binary Matrix symmetric  
# along main diagonal. 
def minimumflip( mat , n ): 
  
    # Comparing elements across diagonal 
    flip = 0
    for i in range(n): 
        for j in range(i): 
            if mat[i][j] != mat[j][i] : 
                flip += 1
      
    return flip 
  
# Driver Program 
n = 3
mat =[[ 0, 0, 1], 
      [ 1, 1, 1], 
      [ 1, 0, 0]] 
print( minimumflip(mat, n)) 
  
# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```cs
// C# Program to find minimum flip 
// required to make Binary Matrix 
// symmetric along main diagonal 
using System; 
  
class GFG { 
      
    // Return the minimum flip required  
    // to make Binary Matrix symmetric 
    // along main diagonal. 
    static int minimumflip(int [,]mat, int n) 
    { 
          
        // Comparing elements across diagonal 
        int flip = 0; 
        for (int i = 0; i < n; i++) 
            for (int j = 0; j < i; j++) 
                if (mat[i,j] != mat[j,i]) 
                    flip++; 
        return flip; 
    } 
      
    /* Driver program to test above function */
    public static void Main()  
    { 
        int n = 3; 
        int [,]mat = {{ 0, 0, 1 }, 
                      { 1, 1, 1 }, 
                      { 1, 0, 0 }}; 
          
    Console.WriteLine(minimumflip(mat, n)); 
    } 
} 
      
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// PHP Program to find minimum 
// flip required to make Binary 
// Matrix symmetric along main diagonal 
$N = 3; 
  
// Return the minimum flip  
// required to make Binary  
// Matrix symmetric along main diagonal. 
  
function minimumflip($mat, $n) 
{ 
    // Comparing elements 
    // across diagonal 
    $flip = 0; 
    for ($i = 0; $i < $n; $i++) 
        for ($j = 0; $j < $i; $j++) 
            if ($mat[$i][$j] != $mat[$j][$i]) 
                $flip++; 
    return $flip; 
} 
  
// Driver Code 
$n = 3; 
$mat = array(array(0, 0, 1), 
             array(1, 1, 1), 
             array(1, 0, 0)); 
echo minimumflip($mat, $n), "\n"; 
      
// This code is contributed by ajit 
?>
```

输出：

```
2
```

