# 方阵的两个对角线中的行公共元素

> 原文： [https://www.geeksforgeeks.org/row-wise-common-elements-two-diagonals-square-matrix/](https://www.geeksforgeeks.org/row-wise-common-elements-two-diagonals-square-matrix/)

给定一个方阵，找出在同一行中以及在主和次对角线上都相同的数字计数。

**示例**：

```
Input : 1 2 1
        4 5 2
        0 5 1
Output : 2
Primary diagonal is 1 5 1
Secondary diagonal is 1 5 0
Two elements (1 and 5) match 
in two diagonals and same.

Input : 1 0 0
        0 1 0
        0 0 1
Output : 1
Primary diagonal is 1 1 1
Secondary diagonal is 0 1 0
Only one element is same.

```



我们可以在`O(n)`时间，`O(1)`空间和仅一个遍历中实现这一目标。 我们可以在主对角线的第`i`行找到当前元素作为`mat[i][i]`，在次对角线的第`i`个元素找到作为`mat[i][n-i-1]`。

## C++ 

```cpp

// CPP program to find common elements in 
// two diagonals. 
#include <iostream> 
#define MAX 100 
using namespace std; 

// Returns count of row wise same 
// elements in two diagonals of 
// mat[n][n] 
int countCommon(int mat[][MAX], int n) 
{ 
    int res = 0; 
    for (int i=0;i<n;i++) 
        if (mat[i][i] == mat[i][n-i-1]) 
             res++; 
    return res; 
} 

// Driver Code 
int main() 
{ 
    int mat[][MAX] = {{1, 2, 3},  
                      {4, 5, 6}, 
                      {7, 8, 9}}; 
    cout << countCommon(mat, 3); 
    return 0; 
} 

```

## Java

```java
// Java program to find common  
// elements in two diagonals. 
import java.io.*; 
  
class GFG 
{ 
    int MAX = 100; 
      
    // Returns count of row wise same elements  
    // in two diagonals of mat[n][n] 
    static int countCommon(int mat[][], int n) 
    { 
        int res = 0; 
        for (int i = 0; i < n; i++) 
            if (mat[i][i] == mat[i][n - i - 1]) 
                res++; 
        return res; 
    } 
  
    // Driver Code 
    public static void main(String args[])throws IOException 
    { 
        int mat[][] = {{1, 2, 3},  
                       {4, 5, 6}, 
                       {7, 8, 9}}; 
        System.out.println(countCommon(mat, 3)); 
    } 
} 
  
// This code is contributed by Anshika Goyal.
```

## Python3

```py
# Python3 program to find common  
# elements in two diagonals. 
  
Max = 100
  
# Returns count of row wise same 
# elements in two diagonals of 
# mat[n][n] 
def countCommon(mat, n): 
    res = 0
      
    for i in range(n): 
          
        if mat[i][i] == mat[i][n-i-1] : 
            res = res + 1
    return res      
  
# Driver Code 
mat = [[1, 2, 3], 
       [4, 5, 6], 
       [7, 8, 9]] 
  
print(countCommon(mat, 3)) 
  
# This code is contributed by Anant Agarwal.
```

## C#

```cs
// C# program to find common  
// elements in two diagonals. 
using System; 
  
class GFG { 
      
    // Returns count of row wise same 
    // elements in two diagonals of 
    // mat[n][n] 
    static int countCommon(int [,]mat, int n) 
    { 
        int res = 0; 
          
        for (int i = 0; i < n; i++) 
            if (mat[i,i] == mat[i,n - i - 1]) 
                res++; 
                  
        return res; 
    } 
  
    // Driver Code 
    public static void Main() 
    { 
        int [,]mat = {{1, 2, 3},  
                      {4, 5, 6}, 
                      {7, 8, 9}}; 
        Console.WriteLine(countCommon(mat, 3)); 
    } 
} 
  
// This code is contributed by vt_m.
```

## PHP

```php
<?php 
// PHP program to find common  
// elements in two diagonals. 
$MAX = 100; 
  
// Returns count of row wise 
// same elements in two  
// diagonals of mat[n][n] 
function countCommon($mat, $n) 
{ 
    global $MAX; 
    $res = 0; 
    for ($i = 0; $i < $n; $i++) 
        if ($mat[$i][$i] == $mat[$i][$n - $i - 1]) 
            $res++; 
    return $res; 
} 
  
// Driver Code 
$mat = array(array(1, 2, 3),  
             array(4, 5, 6), 
             array(7, 8, 9)); 
echo countCommon($mat, 3); 
  
// This code is contributed by aj_36 
?>
```

输出：

```
  1  
```

