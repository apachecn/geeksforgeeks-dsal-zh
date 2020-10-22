# 计算矩阵中所有排序的行

> 原文： [https://www.geeksforgeeks.org/count-sorted-rows-matrix/](https://www.geeksforgeeks.org/count-sorted-rows-matrix/)

给定一个`m * n`大小的矩阵，任务是对矩阵中按严格递增顺序或严格递减顺序排序的所有行进行计数吗？

**示例**：

```
Input : m = 4,  n = 5
        mat[m][n] = 1 2 3 4 5
                    4 3 1 2 6
                    8 7 6 5 4
                    5 7 8 9 10
Output: 3 

```



这个想法很简单，涉及矩阵的两个遍历。

1.  从矩阵左侧严格按**递增顺序**遍历所有行

2.  从矩阵右侧严格降序遍历

以下是上述想法的实现。

## C++ 

```cpp

// C++ program to find number of sorted rows 
#include <bits/stdc++.h> 
#define MAX 100 
using namespace std; 

// Function to count all sorted rows in a matrix 
int sortedCount(int mat[][MAX], int r, int c) 
{ 
    int result = 0; // Initialize result 

    // Start from left side of matrix to 
    // count increasing order rows 
    for (int i=0; i<r; i++) 
    { 
        // Check if there is any pair ofs element 
        // that are  not in increasing order. 
        int j; 
        for (j=0; j<c-1; j++) 
            if (mat[i][j+1] <= mat[i][j]) 
                break; 

        // If the loop didn't break (All elements 
        // of current row were in increasing order) 
        if (j == c-1) 
            result++; 
    } 

    // Start from right side of matrix to 
    // count increasing order rows ( reference 
    // to left these are in decreasing order ) 
    for (int i=0; i<r; i++) 
    { 
        // Check if there is any pair ofs element 
        // that are  not in decreasing order. 
        int j; 
        for (j=c-1; j>0; j--) 
            if (mat[i][j-1] <= mat[i][j]) 
                break; 

        // Note c > 1 condition is required to make 
        // sure that a single column row is not counted 
        // twice (Note that a single column row is sorted 
        // both in increasing and decreasing order)  
        if (c > 1 && j == 0) 
            result++; 
    } 
    return result; 
} 

// Driver program to run the case 
int main() 
{ 
    int m = 4, n = 5; 
    int mat[][MAX] = {{1, 2, 3, 4, 5}, 
                      {4, 3, 1, 2, 6}, 
                      {8, 7, 6, 5, 4}, 
                      {5, 7, 8, 9, 10}}; 
    cout << sortedCount(mat, m, n); 
    return 0; 
} 

```

## Java

```java
// Java program to find number of sorted rows 
  
class GFG { 
      
    static int MAX = 100; 
  
    // Function to count all sorted rows in a matrix 
    static int sortedCount(int mat[][], int r, int c) 
    { 
        int result = 0; // Initialize result 
  
        // Start from left side of matrix to 
        // count increasing order rows 
        for (int i = 0; i < r; i++) { 
              
            // Check if there is any pair ofs element 
            // that are not in increasing order. 
            int j; 
            for (j = 0; j < c - 1; j++) 
                if (mat[i][j + 1] <= mat[i][j]) 
                    break; 
  
            // If the loop didn't break (All elements 
            // of current row were in increasing order) 
            if (j == c - 1) 
                result++; 
        } 
  
        // Start from right side of matrix to 
        // count increasing order rows ( reference 
        // to left these are in decreasing order ) 
        for (int i = 0; i < r; i++) { 
              
            // Check if there is any pair ofs element 
            // that are not in decreasing order. 
            int j; 
            for (j = c - 1; j > 0; j--) 
                if (mat[i][j - 1] <= mat[i][j]) 
                    break; 
  
            // Note c > 1 condition is required to make 
            // sure that a single column row is not counted 
            // twice (Note that a single column row is sorted 
            // both in increasing and decreasing order) 
            if (c > 1 && j == 0) 
                result++; 
        } 
        return result; 
    } 
      
    // Driver code 
    public static void main(String arg[]) 
    { 
        int m = 4, n = 5; 
        int mat[][] = { { 1, 2, 3, 4, 5 }, 
                        { 4, 3, 1, 2, 6 }, 
                        { 8, 7, 6, 5, 4 }, 
                        { 5, 7, 8, 9, 10 } }; 
        System.out.print(sortedCount(mat, m, n)); 
    } 
} 
  
// This code is contributed by Anant Agarwal.
```

## Python

```py
# Python3 program to find number  
# of sorted rows 
def sortedCount(mat, r, c): 
      
    result = 0
      
    # Start from left side of matrix to  
    # count increasing order rows  
    for i in range(r): 
          
        # Check if there is any pair ofs element  
        # that are not in increasing order. 
        j = 0
        for j in range(c - 1): 
            if mat[i][j + 1] <= mat[i][j]: 
                break
      
        # If the loop didn't break (All elements  
        # of current row were in increasing order) 
        if j == c - 2: 
            result += 1
  
    # Start from right side of matrix to  
    # count increasing order rows ( reference  
    # to left these are in decreasing order ) 
    for i in range(0, r): 
  
        # Check if there is any pair ofs element  
        # that are not in decreasing order. 
        j = 0
        for j in range(c - 1, 0, -1): 
            if mat[i][j - 1] <= mat[i][j]: 
                break
          
        # Note c > 1 condition is required to  
        # make sure that a single column row  
        # is not counted twice (Note that a  
        # single column row is sorted both  
        # in increasing and decreasing order) 
        if c > 1 and j == 1: 
            result += 1
      
    return result      
  
# Driver code 
m, n = 4, 5
  
mat = [[1, 2, 3, 4, 5], 
       [4, 3, 1, 2, 6], 
       [8, 7, 6, 5, 4], 
       [5, 7, 8, 9, 10]] 
  
print(sortedCount(mat, m, n)) 
  
# This code is contributed by 
# Mohit kumar 29 (IIIT gwalior)
```

## C#

```cs
// C# program to find number of sorted rows 
using System; 
  
class GFG { 
      
// static int MAX = 100; 
  
    // Function to count all sorted rows in  
    // a matrix 
    static int sortedCount(int [,]mat, int r, 
                                       int c) 
    { 
        int result = 0; // Initialize result 
  
        // Start from left side of matrix to 
        // count increasing order rows 
        for (int i = 0; i < r; i++) { 
              
            // Check if there is any pair of 
            // element that are not in 
            // increasing order. 
            int j; 
            for (j = 0; j < c - 1; j++) 
                if (mat[i,j + 1] <= mat[i,j]) 
                    break; 
  
            // If the loop didn't break (All 
            // elements of current row were  
            // in increasing order) 
            if (j == c - 1) 
                result++; 
        } 
  
        // Start from right side of matrix  
        // to count increasing order rows  
        // ( reference to left these are in  
        // decreasing order ) 
        for (int i = 0; i < r; i++) { 
              
            // Check if there is any pair  
            // ofs element that are not in 
            // decreasing order. 
            int j; 
            for (j = c - 1; j > 0; j--) 
                if (mat[i,j - 1] <= mat[i,j]) 
                    break; 
  
            // Note c > 1 condition is  
            // required to make sure that a  
            // single column row is not  
            // counted twice (Note that a  
            // single column row is sorted 
            // both in increasing and 
            // decreasing order) 
            if (c > 1 && j == 0) 
                result++; 
        } 
        return result; 
    } 
      
    // Driver code 
    public static void Main() 
    { 
        int m = 4, n = 5; 
        int [,]mat = { { 1, 2, 3, 4, 5 }, 
                       { 4, 3, 1, 2, 6 }, 
                       { 8, 7, 6, 5, 4 }, 
                       { 5, 7, 8, 9, 10 } }; 
                         
        Console.WriteLine( 
                   sortedCount(mat, m, n)); 
    } 
} 
  
// This code is contributed by anuj_67.
```

## PHP

```php
<?php 
// PHP program to find  
// number of sorted rows 
  
$MAX = 100; 
  
// Function to count all  
// sorted rows in a matrix 
function sortedCount($mat,  
                     $r, $c) 
{ 
    // Initialize result 
    $result = 0;  
  
    // Start from left side of 
    // matrix to count increasing  
    // order rows 
    for ( $i = 0; $i < $r; $i++) 
    { 
        // Check if there is any  
        // pair ofs element that  
        // are not in increasing order. 
        $j; 
        for ($j = 0; $j < $c - 1; $j++) 
            if ($mat[$i][$j + 1] <= $mat[$i][$j]) 
                break; 
  
        // If the loop didn't break  
        // (All elements of current  
        // row were in increasing order) 
        if ($j == $c - 1) 
            $result++; 
    } 
  
    // Start from right side of  
    // matrix to count increasing  
    // order rows ( reference to left 
    // these are in decreasing order ) 
    for ($i = 0; $i < $r; $i++) 
    { 
        // Check if there is any pair  
        // ofs element that are not 
        // in decreasing order. 
        $j; 
        for ($j = $c - 1; $j > 0; $j--) 
            if ($mat[$i][$j - 1] <= $mat[$i][$j]) 
                break; 
  
        // Note c > 1 condition is  
        // required to make sure that  
        // a single column row is not  
        // counted twice (Note that a  
        // single column row is sorted 
        // both in increasing and  
        // decreasing order)  
        if ($c > 1 && $j == 0) 
            $result++; 
    } 
    return $result; 
} 
  
// Driver Code 
$m = 4; $n = 5; 
$mat = array(array(1, 2, 3, 4, 5), 
             array(4, 3, 1, 2, 6), 
             array(8, 7, 6, 5, 4), 
             array(5, 7, 8, 9, 10)); 
echo sortedCount($mat, $m, $n); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
3
```

时间复杂度：`O(m * n)`。

辅助空间：`O(1)`。

如果您有另一种优化的方法来解决此问题，请分享评论。