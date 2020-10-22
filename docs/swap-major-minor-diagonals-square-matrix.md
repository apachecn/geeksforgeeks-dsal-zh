# 交换方阵的主要和次要对角线

> 原文： [https://www.geeksforgeeks.org/swap-major-minor-diagonals-square-matrix/](https://www.geeksforgeeks.org/swap-major-minor-diagonals-square-matrix/)

给定方阵，交换主要和次要对角线元素。

**矩阵的主要对角元素**：

主要对角元素是从矩阵的左上角到右下角的元素。 主对角线也称为主对角线或主对角线。

**矩阵的次要对角元素**：

次要对角元素是从矩阵的右上角到左下角的元素。 也称为次要对角线。

**示例**：

```
Input : 0 1 2
        3 4 5
        6 7 8

Output : 2 1 0
         3 4 5
         8 7 6

```



**方法**：

一个简单的事情应该是，主对角线的索引相同，即假设`A`为矩阵，则`A[1][1]`将为对角线元素。次对角线的索引的总和等于矩阵的大小。 假设`A`是大小为 3 的矩阵，那么`A[1][2]`将是次对角元素。

下面是上述方法的实现：

## C++ 

```cpp

// CPP Program to swap diagonal of a matrix 
#include <bits/stdc++.h> 
using namespace std; 

// size of square matrix 
#define N 3 

// Function to swap diagonal of matrix 
void swapDiagonal(int matrix[][N]) { 
  for (int i = 0; i < N; i++) 
    swap(matrix[i][i], matrix[i][N - i - 1]); 
} 

// Driver Code 
int main() { 
  int matrix[N][N] = {{0, 1, 2},  
                      {3, 4, 5},  
                      {6, 7, 8}}; 

  swapDiagonal(matrix); 

  // Displaying modified matrix 
  for (int i = 0; i < N; i++) { 
    for (int j = 0; j < N; j++) 
      cout << matrix[i][j] << " "; 
    cout << endl; 
  } 

  return 0; 
} 

```

## Java

```java
// Java implementation to swap 
// diagonal of a matrix 
import java.io.*; 
  
class Gfg { 
static int N = 3; 
  
// Function to swap diagonal of matrix 
static void swapDiagonal(int matrix[][]) { 
    for (int i = 0; i < N; i++) { 
    int temp = matrix[i][i]; 
    matrix[i][i] = matrix[i][N - i - 1]; 
    matrix[i][N - i - 1] = temp; 
    } 
} 
  
// Driver function 
public static void main(String arg[]) { 
    int matrix[][] = {{0, 1, 2},  
                      {3, 4, 5},  
                      {6, 7, 8}}; 
  
    swapDiagonal(matrix); 
  
    // Displaying modified matrix 
    for (int i = 0; i < N; i++) { 
    for (int j = 0; j < N; j++) 
        System.out.print(matrix[i][j] + " "); 
    System.out.println(); 
    } 
} 
} 
  
// This code is contributed by Anant Agarwal.
```

## Python3

```py
# Python3 Program to swap diagonal of a matrix 
  
# size of square matrix 
N = 3
  
# Function to swap diagonal of matrix 
def swapDiagonal(matrix): 
      
    for i in range(N): 
          
        matrix[i][i], matrix[i][N-i-1] = \ 
            matrix[i][N-i-1], matrix[i][i] 
  
  
# Driver Code 
matrix = [[0, 1, 2], 
          [3, 4, 5], 
          [6, 7, 8]] 
  
# swap diagonals of matrix 
swapDiagonal(matrix); 
  
# Displaying modified matrix 
for i in range(N):     
    for j in range(N):         
        print(matrix[i][j], end = ' ')         
    print()
```

## C#

```cs
// C# implementation to swap 
// diagonal of a matrix 
using System; 
  
class Gfg { 
      
    static int N = 3; 
      
    // Function to swap diagonal of matrix 
    static void swapDiagonal(int [,]matrix) { 
        for (int i = 0; i < N; i++) { 
        int temp = matrix[i,i]; 
        matrix[i,i] = matrix[i,N - i - 1]; 
        matrix[i,N - i - 1] = temp; 
        } 
    } 
      
    // Driver function 
    public static void Main() { 
        int [,]matrix = {{0, 1, 2},  
                         {3, 4, 5},  
                         {6, 7, 8}}; 
      
        swapDiagonal(matrix); 
      
        // Displaying modified matrix 
        for (int i = 0; i < N; i++) { 
            for (int j = 0; j < N; j++) 
                Console.Write(matrix[i,j] + " "); 
            Console.WriteLine(); 
        } 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// PHP Program to swap  
// diagonal of a matrix 
  
// size of square matrix 
$N = 3; 
  
// Function to swap  
// diagonal of matrix 
function swapDiagonal($matrix)  
{ 
    global $N; 
    for ($i = 0; $i < $N; $i++) 
    { 
        $tmp=$matrix[$i][$i]; 
        $matrix[$i][$i] = $matrix[$i][$N - $i - 1]; 
        $matrix[$i][$N - $i - 1] = $tmp; 
    } 
      
// Displaying modified matrix 
for ($i = 0; $i < $N; $i++)  
{ 
    for ($j = 0; $j < $N; $j++) 
        echo $matrix[$i][$j] . " "; 
    echo "\n"; 
} 
} 
  
// Driver Code 
$matrix = array(array(0, 1, 2),  
                array(3, 4, 5),  
                array(6, 7, 8)); 
  
swapDiagonal($matrix); 
  
// This code is contributed by mits 
?>
```

输出：

```
2 1 0
3 4 5
8 7 6
```
