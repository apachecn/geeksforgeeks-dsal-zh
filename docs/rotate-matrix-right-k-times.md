# 向右旋转矩阵`K`次

> 原文： [https://www.geeksforgeeks.org/rotate-matrix-right-k-times/](https://www.geeksforgeeks.org/rotate-matrix-right-k-times/)

给定一个大小为`N * M`且值为`K`的矩阵。我们必须将矩阵向右旋转`K`次。

**示例**：

```
Input :  N = 3, M = 3, K = 2
         12 23 34
         45 56 67
         78 89 91 

Output : 23 34 12
         56 67 45
         89 91 78 

Input :  N = 2, M = 2, K = 2
         1 2
         3 4

Output : 1 2
         3 4

```



一种简单而有效的方法是将矩阵的每一行视为一个数组并执行数组旋转。 可以通过使用临时数组将元素从`K`复制到数组的末尾到数组的开头来完成。 然后剩下的元素从开始到`K-1`到结束。

让我们举个例子：

![](img/d7f73cd5cca5983cb8d9a6644c1f3759.png)

## C++ 

```cpp

// CPP program to rotate a matrix right by k times 
#include <iostream> 

// size of matrix 
#define M 3 
#define N 3 

using namespace std; 

// function to rotate matrix by k times 
void rotateMatrix(int matrix[][M], int k) { 
  // temporary array of size M 
  int temp[M]; 

  // within the size of matrix 
  k = k % M; 

  for (int i = 0; i < N; i++) { 

    // copy first M-k elements to temporary array 
    for (int t = 0; t < M - k; t++) 
      temp[t] = matrix[i][t]; 

    // copy the elements from k to end to starting 
    for (int j = M - k; j < M; j++) 
      matrix[i][j - M + k] = matrix[i][j]; 

    // copy elements from temporary array to end 
    for (int j = k; j < M; j++) 
      matrix[i][j] = temp[j - k]; 
  } 
} 

// function to display the matrix 
void displayMatrix(int matrix[][M]) { 
  for (int i = 0; i < N; i++) { 
    for (int j = 0; j < M; j++) 
      cout << matrix[i][j] << " "; 
    cout << endl; 
  } 
} 

// Driver's code 
int main() { 
  int matrix[N][M] = {{12, 23, 34}, 
                     {45, 56, 67},  
                     {78, 89, 91}}; 
  int k = 2; 

  // rotate matrix by k 
  rotateMatrix(matrix, k); 

  // display rotated matrix 
  displayMatrix(matrix); 

  return 0; 
} 

```

## Java

```java
// Java program to rotate a matrix  
// right by k times 
  
class GFG 
{ 
    // size of matrix 
    static final int M=3; 
    static final int N=3; 
      
    // function to rotate matrix by k times 
    static void rotateMatrix(int matrix[][], int k) 
    { 
        // temporary array of size M 
        int temp[]=new int[M]; 
          
        // within the size of matrix 
        k = k % M; 
          
        for (int i = 0; i < N; i++) 
        { 
          
            // copy first M-k elements  
            // to temporary array 
            for (int t = 0; t < M - k; t++) 
            temp[t] = matrix[i][t]; 
          
            // copy the elements from k  
            // to end to starting 
            for (int j = M - k; j < M; j++) 
            matrix[i][j - M + k] = matrix[i][j]; 
          
            // copy elements from  
            // temporary array to end 
            for (int j = k; j < M; j++) 
            matrix[i][j] = temp[j - k]; 
        } 
    } 
      
    // function to display the matrix 
    static void displayMatrix(int matrix[][]) 
    { 
        for (int i = 0; i < N; i++) 
        { 
            for (int j = 0; j < M; j++) 
            System.out.print(matrix[i][j] + " "); 
            System.out.println(); 
        } 
    }  
      
    // Driver code 
    public static void main (String[] args) 
    { 
        int matrix[][] = {{12, 23, 34}, 
                        {45, 56, 67},  
                        {78, 89, 91}}; 
    int k = 2; 
      
    // rotate matrix by k 
    rotateMatrix(matrix, k); 
      
    // display rotated matrix 
    displayMatrix(matrix); 
    } 
} 
  
// This code is contributed by Anant Agarwal.
```

## Python3

```py
# Python program to rotate  
# a matrix right by k times 
  
# size of matrix 
M = 3
N = 3
matrix = [[12, 23, 34], 
          [45, 56, 67],  
          [78, 89, 91]] 
  
# function to rotate 
# matrix by k times 
def rotateMatrix(k) : 
  
    global M, N, matrix 
      
    # temporary array  
    # of size M 
    temp = [0] * M 
      
    # within the size 
    # of matrix 
    k = k % M 
      
    for i in range(0, N) :  
      
        # copy first M-k elements 
        # to temporary array 
        for t in range(0, M - k) : 
            temp[t] = matrix[i][t] 
      
        # copy the elements from  
        # k to end to starting 
        for j in range(M - k, M) : 
            matrix[i][j - M + k] = matrix[i][j] 
      
        # copy elements from  
        # temporary array to end 
        for j in range(k, M) : 
            matrix[i][j] = temp[j - k] 
      
# function to display 
# the matrix 
def displayMatrix() : 
  
    global M, N, matrix 
    for i in range(0, N) : 
      
        for j in range(0, M) : 
            print ("{} " .  
                   format(matrix[i][j]), end = "") 
        print () 
  
# Driver code 
k = 2
  
# rotate matrix by k 
rotateMatrix(k) 
  
# display rotated matrix 
displayMatrix() 
  
# This code is contributed by  
# Manish Shaw(manishshaw1)
```

## C#

```cs
// C# program to rotate a   
// matrix right by k times 
using System; 
  
class GFG { 
      
    // size of matrix 
    static int M=3; 
    static int N=3; 
      
    // function to rotate matrix by k times 
    static void rotateMatrix(int [,] matrix,  
                             int k) 
    { 
          
        // temporary array of size M 
        int [] temp=new int[M]; 
          
        // within the size of matrix 
        k = k % M; 
          
        for (int i = 0; i < N; i++) 
        { 
          
            // copy first M-k elements  
            // to temporary array 
            for (int t = 0; t < M - k; t++) 
            temp[t] = matrix[i, t]; 
          
            // copy the elements from k  
            // to end to starting 
            for (int j = M - k; j < M; j++) 
            matrix[i, j - M + k] = matrix[i, j]; 
          
            // copy elements from  
            // temporary array to end 
            for (int j = k; j < M; j++) 
            matrix[i, j] = temp[j - k]; 
        } 
    } 
      
    // function to display the matrix 
    static void displayMatrix(int [,] matrix) 
    { 
        for (int i = 0; i < N; i++) 
        { 
            for (int j = 0; j < M; j++) 
            Console.Write(matrix[i, j] + " "); 
            Console.WriteLine(); 
        } 
    }  
      
    // Driver code 
    public static void Main () 
    { 
        int [,] matrix = {{12, 23, 34}, 
                          {45, 56, 67},  
                          {78, 89, 91}}; 
        int k = 2; 
          
        // rotate matrix by k 
        rotateMatrix(matrix, k); 
          
        // display rotated matrix 
        displayMatrix(matrix); 
    } 
} 
  
// This code is contributed by KRV.
```

## PHP

```php
<?php 
// PHP program to rotate  
// a matrix right by k times 
  
// size of matrix 
$M = 3; 
$N = 3; 
  
// function to rotate 
// matrix by k times 
function rotateMatrix(&$matrix, $k)  
{ 
    global $M, $N; 
      
    // temporary array  
    // of size M 
    $temp = array(); 
      
    // within the size 
    // of matrix 
    $k = $k % $M; 
      
    for ($i = 0; $i < $N; $i++) 
    { 
      
        // copy first M-k elements 
        // to temporary array 
        for ($t = 0;  
             $t < $M - $k; $t++) 
        $temp[$t] = $matrix[$i][$t]; 
      
        // copy the elements from  
        // k to end to starting 
        for ($j = $M - $k;  
             $j < $M; $j++) 
        $matrix[$i][$j - $M + $k] = 
                    $matrix[$i][$j]; 
      
        // copy elements from  
        // temporary array to end 
        for ($j = $k; $j < $M; $j++) 
        $matrix[$i][$j] = $temp[$j - $k]; 
    } 
} 
  
// function to display 
// the matrix 
function displayMatrix(&$matrix)  
{ 
    global $M, $N; 
    for ($i = 0; $i < $N; $i++)  
    { 
        for ($j = 0; $j < $M; $j++) 
        echo ($matrix[$i][$j]." "); 
        echo ("\n"); 
    } 
} 
  
// Driver code 
$matrix = array(array(12, 23, 34), 
                array(45, 56, 67),  
                array(78, 89, 91)); 
$k = 2; 
  
// rotate matrix by k 
rotateMatrix($matrix, $k); 
  
// display rotated matrix 
displayMatrix($matrix); 
  
// This code is contributed by  
// Manish Shaw(manishshaw1) 
?>
```

输出：

```
23 34 12 
56 67 45 
89 91 78
```

