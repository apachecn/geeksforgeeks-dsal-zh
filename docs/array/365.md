# 将矩阵元素逐行移动`k`

> 原文： [https://www.geeksforgeeks.org/shift-matrix-elements-k/](https://www.geeksforgeeks.org/shift-matrix-elements-k/)

给定方阵`mat[][]`和数字`k`。 任务是在矩阵的右侧移动每行的前`k`个元素。

**示例**：

```
Input : mat[N][N] = {{1, 2, 3},
                     {4, 5, 6},
                     {7, 8, 9}}
        k = 2
Output :mat[N][N] = {{3, 1, 2}
                     {6, 4, 5}
                     {9, 7, 8}}

Input : mat[N][N] = {{1, 2, 3, 4}
                     {5, 6, 7, 8}
                     {9, 10, 11, 12}
                     {13, 14, 15, 16}}
        k = 2
Output :mat[N][N] = {{3, 4, 1, 2}
                     {7, 8, 5, 6}
                     {11, 12, 9, 10}
                     {15, 16, 13, 14}}

Note: Matrix should be a square matrix

```



## C++ 

```cpp

// C++ program to shift k elements in a matrix. 
#include <bits/stdc++.h> 
using namespace std; 
#define N 4 

// Function to shift first k elements of  
// each row of matrix. 
void shiftMatrixByK(int mat[N][N], int k) 
{ 
    if (k > N) { 
        cout << "shifting is not possible" << endl; 
        return; 
    } 

    int j = 0; 
    while (j < N) { 

        // Print elements from index k 
        for (int i = k; i < N; i++) 
            cout << mat[j][i] << " "; 

        // Print elements before index k 
        for (int i = 0; i < k; i++) 
            cout << mat[j][i] << " "; 

        cout << endl; 
        j++; 
    } 
} 

// Driver code 
int main() 
{ 
    int mat[N][N] = {{1, 2, 3, 4}, 
                     {5, 6, 7, 8}, 
                     {9, 10, 11, 12}, 
                     {13, 14, 15, 16}}; 
    int k = 2; 

    // Function call 
    shiftMatrixByK(mat, k); 

    return 0; 
} 

```

## Java

```java

// Java program to shift k elements in a  
// matrix. 
import java.io.*; 
import java.util.*; 

public class GFG { 

    static int N = 4; 

    // Function to shift first k elements  
    // of each row of matrix. 
    static void shiftMatrixByK(int [][]mat, 
                                    int k) 
    { 
        if (k > N) { 
            System.out.print("Shifting is"
                        + " not possible"); 
            return; 
        } 

        int j = 0; 
        while (j < N) { 

            // Print elements from index k 
            for (int i = k; i < N; i++) 
                System.out.print(mat[j][i] + " "); 

            // Print elements before index k 
            for (int i = 0; i < k; i++) 
                System.out.print(mat[j][i] + " "); 

            System.out.println(); 
            j++; 
        } 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int [][]mat = new int [][] 
                    { {1, 2, 3, 4}, 
                      {5, 6, 7, 8}, 
                      {9, 10, 11, 12}, 
                      {13, 14, 15, 16} }; 
        int k = 2; 

        // Function call 
        shiftMatrixByK(mat, k); 
    } 
} 

// This code is contributed by Manish Shaw  
// (manishshaw1) 

```

## Python3

```py

# Python3 program to shift k  
# elements in a matrix. 

N = 4
# Function to shift first k  
# elements of each row of  
# matrix. 
def shiftMatrixByK(mat, k): 
    if (k > N) : 
        print ("shifting is"
            " not possible") 
        return

    j = 0
    while (j < N) : 

        # Print elements from 
        # index k 
        for i in range(k, N): 
            print ("{} " .  
            format(mat[j][i]), end="") 

        # Print elements before 
        # index k 
        for i in range(0, k): 
            print ("{} " .  
            format(mat[j][i]), end="") 

        print ("") 
        j = j + 1

# Driver code 
mat = [[1, 2, 3, 4], 
       [5, 6, 7, 8], 
       [9, 10, 11, 12], 
       [13, 14, 15, 16]] 
k = 2

# Function call 
shiftMatrixByK(mat, k) 

# This code is contributed by  
# Manish Shaw (manishshaw1) 

```

## C# 

```cs

// C# program to shift k elements in a  
// matrix. 
using System; 

class GFG { 

    static int N = 4; 

    // Function to shift first k elements  
    // of each row of matrix. 
    static void shiftMatrixByK(int [,]mat, 
                                    int k) 
    { 
        if (k > N) { 
            Console.WriteLine("shifting is"
                        + " not possible"); 
            return; 
        } 

        int j = 0; 
        while (j < N) { 

            // Print elements from index k 
            for (int i = k; i < N; i++) 
                Console.Write(mat[j,i] + " "); 

            // Print elements before index k 
            for (int i = 0; i < k; i++) 
                Console.Write(mat[j,i] + " "); 

            Console.WriteLine(); 
            j++; 
        } 
    } 

    // Driver code 
    public static void Main() 
    { 
        int [,]mat = new int [,] 
                    { {1, 2, 3, 4}, 
                      {5, 6, 7, 8}, 
                      {9, 10, 11, 12}, 
                      {13, 14, 15, 16} }; 
        int k = 2; 

        // Function call 
        shiftMatrixByK(mat, k); 
    } 
} 

// This code is contributed by Manish Shaw  
// (manishshaw1) 

```

## PHP

```php

<?php 
// PHP program to shift k  
// elements in a matrix. 

// Function to shift first k  
// elements of each row of matrix. 
function shiftMatrixByK($mat, $k) 
{ 
    $N = 4; 
    if ($k > $N)  
    { 
        echo ("shifting is not possible\n"); 
        return; 
    } 

    $j = 0; 
    while ($j < $N)  
    { 

        // Print elements from index k 
        for ($i = $k; $i < $N; $i++) 
            echo ($mat[$j][$i]." "); 

        // Print elements before index k 
        for ($i = 0; $i < $k; $i++) 
            echo ($mat[$j][$i]." "); 

        echo ("\n"); 
        $j++; 
    } 
} 

// Driver code 
$mat = array(array(1, 2, 3, 4), 
             array(5, 6, 7, 8), 
             array(9, 10, 11, 12), 
             array(13, 14, 15, 16)); 
$k = 2; 

// Function call 
shiftMatrixByK($mat, $k); 

// This code is contributed by  
// Manish Shaw(manishshaw1) 
?> 

```

**输出**：

```
3 4 1 2 
7 8 5 6 
11 12 9 10 
15 16 13 14

```



* * *

* * *



