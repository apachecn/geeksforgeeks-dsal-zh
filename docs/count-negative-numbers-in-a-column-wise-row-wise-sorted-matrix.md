# 在按列和行排序矩阵中统计负数

> 原文： [https://www.geeksforgeeks.org/count-negative-numbers-in-a-column-wise-row-wise-sorted-matrix/](https://www.geeksforgeeks.org/count-negative-numbers-in-a-column-wise-row-wise-sorted-matrix/)

在按列/按行排序的矩阵`M[][]`中找到负数的数量。 假设`M`具有`n`行和`m`列。

例：

```
Input:  M =  [-3, -2, -1,  1]
             [-2,  2,  3,  4]
             [4,   5,  7,  8]
Output : 4
We have 4 negative numbers in this matrix

```

**我们强烈建议您最小化浏览器，然后自己尝试。**

**朴素的解决方案**：

这是一个朴素的非最优解决方案。

我们从左上角开始，从左到右，从上到下逐一计数负数。

对于给定的示例：

```
[-3, -2, -1,  1]
[-2,  2,  3,  4]
[4,   5,  7,  8]

Evaluation process

[?,  ?,  ?,  1]
[?,  2,  3,  4]
[4,  5,  7,  8]
```

以下是上述想法的实现。

## C++ 

```cpp

// CPP implementation of Naive method 
// to count of negative numbers in 
// M[n][m] 
#include <bits/stdc++.h> 
using namespace std; 

int countNegative(int M[][4], int n, int m) 
{ 
    int count = 0; 

    // Follow the path shown using 
    // arrows above 
    for (int i = 0; i < n; i++) { 
        for (int j = 0; j < m; j++) { 
            if (M[i][j] < 0) 
                count += 1; 

            // no more negative numbers 
            // in this row 
            else
                break; 
        } 
    } 
    return count; 
} 

// Driver program to test above functions 
int main() 
{ 
    int M[3][4] = { { -3, -2, -1, 1 }, 
                    { -2, 2, 3, 4 }, 
                    { 4, 5, 7, 8 } }; 

    cout << countNegative(M, 3, 4); 
    return 0; 
} 
// This code is contributed by Niteesh Kumar 

```

## Java

```java
// Java implementation of Naive method 
// to count of negative numbers in 
// M[n][m] 
import java.util.*; 
import java.lang.*; 
import java.io.*; 
  
class GFG { 
    static int countNegative(int M[][], int n, 
                             int m) 
    { 
        int count = 0; 
  
        // Follow the path shown using 
        // arrows above 
        for (int i = 0; i < n; i++) { 
            for (int j = 0; j < m; j++) { 
                if (M[i][j] < 0) 
                    count += 1; 
  
                // no more negative numbers 
                // in this row 
                else
                    break; 
            } 
        } 
        return count; 
    } 
  
    // Driver program to test above functions 
    public static void main(String[] args) 
    { 
        int M[][] = { { -3, -2, -1, 1 }, 
                      { -2, 2, 3, 4 }, 
                      { 4, 5, 7, 8 } }; 
  
        System.out.println(countNegative(M, 3, 4)); 
    } 
} 
// This code is contributed by Chhavi
```

## Python

```py
# Python implementation of Naive method to count of  
# negative numbers in M[n][m] 
  
def countNegative(M, n, m): 
    count = 0
  
    # Follow the path shown using arrows above 
    for i in range(n): 
        for j in range(m):  
  
            if M[i][j] < 0: 
                count += 1
  
            else: 
                # no more negative numbers in this row 
                break
    return count 
  
  
# Driver code 
M = [  
      [-3, -2, -1,  1], 
      [-2,  2,  3,  4], 
      [ 4,  5,  7,  8] 
    ] 
print(countNegative(M, 3, 4))
```

## C#

```cs
// C# implementation of Naive method 
// to count of negative numbers in 
// M[n][m] 
using System; 
  
class GFG { 
  
    // Function to count 
    // negative number 
    static int countNegative(int[, ] M, int n, 
                             int m) 
    { 
        int count = 0; 
  
        // Follow the path shown 
        // using arrows above 
        for (int i = 0; i < n; i++) { 
            for (int j = 0; j < m; j++) { 
                if (M[i, j] < 0) 
                    count += 1; 
  
                // no more negative numbers 
                // in this row 
                else
                    break; 
            } 
        } 
        return count; 
    } 
  
    // Driver Code 
    public static void Main() 
    { 
        int[, ] M = { { -3, -2, -1, 1 }, 
                      { -2, 2, 3, 4 }, 
                      { 4, 5, 7, 8 } }; 
  
        Console.WriteLine(countNegative(M, 3, 4)); 
    } 
} 
  
// This code is contributed by Sam007
```

## PHP

```php
<?php 
// PHP implementation of Naive method 
// to count of negative numbers in  
// M[n][m] 
  
function countNegative($M, $n, $m) 
{ 
    $count = 0; 
  
    // Follow the path shown using  
    // arrows above 
    for( $i = 0; $i < $n; $i++) 
    { 
        for( $j = 0; $j < $m; $j++) 
        { 
            if( $M[$i][$j] < 0 ) 
                $count += 1; 
          
            // no more negative numbers 
            // in this row 
            else
                break; 
        } 
    } 
    return $count; 
} 
  
    // Driver Code 
    $M = array(array(-3, -2, -1, 1), 
               array(-2, 2, 3, 4), 
               array(4, 5, 7, 8)); 
      
    echo countNegative($M, 3, 4); 
      
// This code is contributed by anuj_67. 
?>
```

输出：

```
4
```

在这种方法中，我们遍历所有元素，因此，在最坏的情况下（当矩阵中所有数字均为负数时），这需要`O(n * m)`的时间。