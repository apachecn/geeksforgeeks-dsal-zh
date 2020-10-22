# 在矩阵中查找特定偶对

> 原文： [https://www.geeksforgeeks.org/find-a-specific-pair-in-matrix/](https://www.geeksforgeeks.org/find-a-specific-pair-in-matrix/)

给定一个整数的`nxn`矩阵`mat[n][n]`，求出所有索引选择的`mat(c, d) – mat(a, b)`的最大值，以使`c > a`和`d > b`。

**示例**：

```
Input:
mat[N][N] = {{ 1, 2, -1, -4, -20 },
             { -8, -3, 4, 2, 1 }, 
             { 3, 8, 6, 1, 3 },
             { -4, -1, 1, 7, -6 },
             { 0, -4, 10, -5, 1 }};
Output: 18
The maximum value is 18 as mat[4][2] 
- mat[1][0] = 18 has maximum difference. 
```

该程序应只对矩阵进行一次遍历。 即预期时间复杂度为`O(n^2)`。

一种简单的**解决方案**是应用暴力。 对于矩阵中的所有值`mat(a, b)`，我们找到具有最大值的`mat(c, d)`，使得`c > a`和`d > b`并继续更新到目前为止找到的最大值。 我们最终返回最大值。

以下是其实现。

## C++ 

```cpp

// A Naive method to find maximum value of mat[d][e] 
// - ma[a][b] such that d > a and e > b 
#include <bits/stdc++.h> 
using namespace std; 
#define N 5 

// The function returns maximum value A(d,e) - A(a,b) 
// over all choices of indexes such that both d > a 
// and e > b. 
int findMaxValue(int mat[][N]) 
{ 
    // stores maximum value 
    int maxValue = INT_MIN; 

    // Consider all possible pairs mat[a][b] and 
    // mat[d][e] 
    for (int a = 0; a < N - 1; a++) 
    for (int b = 0; b < N - 1; b++) 
        for (int d = a + 1; d < N; d++) 
        for (int e = b + 1; e < N; e++) 
            if (maxValue < (mat[d][e] - mat[a][b])) 
                maxValue = mat[d][e] - mat[a][b]; 

    return maxValue; 
} 

// Driver program to test above function 
int main() 
{ 
int mat[N][N] = { 
                { 1, 2, -1, -4, -20 }, 
                { -8, -3, 4, 2, 1 }, 
                { 3, 8, 6, 1, 3 }, 
                { -4, -1, 1, 7, -6 }, 
                { 0, -4, 10, -5, 1 } 
            }; 
    cout << "Maximum Value is "
        << findMaxValue(mat); 

    return 0; 
} 

```

## Java

```java
// A Naive method to find maximum value of mat1[d][e] 
// - ma[a][b] such that d > a and e > b 
import java.io.*; 
import java.util.*; 
   
class GFG  
{ 
    // The function returns maximum value A(d,e) - A(a,b) 
    // over all choices of indexes such that both d > a 
    // and e > b. 
    static int findMaxValue(int N,int mat[][]) 
    { 
        // stores maximum value 
        int maxValue = Integer.MIN_VALUE; 
       
        // Consider all possible pairs mat[a][b] and 
        // mat1[d][e] 
        for (int a = 0; a < N - 1; a++) 
          for (int b = 0; b < N - 1; b++) 
             for (int d = a + 1; d < N; d++) 
               for (int e = b + 1; e < N; e++) 
                  if (maxValue < (mat[d][e] - mat[a][b])) 
                      maxValue = mat[d][e] - mat[a][b]; 
       
        return maxValue; 
    } 
       
    // Driver code 
    public static void main (String[] args)  
    { 
        int N = 5; 
  
        int mat[][] = { 
                      { 1, 2, -1, -4, -20 }, 
                      { -8, -3, 4, 2, 1 }, 
                      { 3, 8, 6, 1, 3 }, 
                      { -4, -1, 1, 7, -6 }, 
                      { 0, -4, 10, -5, 1 } 
                   }; 
  
        System.out.print("Maximum Value is " +  
                         findMaxValue(N,mat)); 
    } 
} 
   
// This code is contributed 
// by Prakriti Gupta
```

## Python 3

```
# A Naive method to find maximum  
# value of mat[d][e] - mat[a][b] 
# such that d > a and e > b 
N = 5
  
# The function returns maximum  
# value A(d,e) - A(a,b) over  
# all choices of indexes such  
# that both d > a and e > b. 
def findMaxValue(mat): 
      
    # stores maximum value 
    maxValue = 0
  
    # Consider all possible pairs  
    # mat[a][b] and mat[d][e] 
    for a in range(N - 1): 
        for b in range(N - 1): 
            for d in range(a + 1, N): 
                for e in range(b + 1, N): 
                    if maxValue < int (mat[d][e] - 
                                       mat[a][b]): 
                        maxValue = int(mat[d][e] - 
                                       mat[a][b]); 
  
    return maxValue; 
  
# Driver Code 
mat = [[ 1, 2, -1, -4, -20 ], 
       [ -8, -3, 4, 2, 1 ], 
       [ 3, 8, 6, 1, 3 ], 
       [ -4, -1, 1, 7, -6 ], 
       [ 0, -4, 10, -5, 1 ]]; 
         
print("Maximum Value is " + 
       str(findMaxValue(mat))) 
        
# This code is contributed  
# by ChitraNayal
```

## C#

```cs
// A Naive method to find maximum  
// value of mat[d][e] - mat[a][b] 
// such that d > a and e > b 
using System; 
class GFG 
{ 
      
    // The function returns 
    // maximum value A(d,e) - A(a,b) 
    // over all choices of indexes  
    // such that both d > a 
    // and e > b. 
    static int findMaxValue(int N,  
                            int [,]mat) 
    { 
          
        //stores maximum value 
        int maxValue = int.MinValue; 
      
        // Consider all possible pairs  
        // mat[a][b] and mat[d][e] 
        for (int a = 0; a< N - 1; a++) 
        for (int b = 0; b < N - 1; b++) 
            for (int d = a + 1; d < N; d++) 
            for (int e = b + 1; e < N; e++) 
                if (maxValue < (mat[d, e] -  
                                mat[a, b])) 
                    maxValue = mat[d, e] -  
                               mat[a, b]; 
  
        return maxValue; 
    } 
      
    // Driver code 
    public static void Main ()  
    { 
        int N = 5; 
  
        int [,]mat = {{1, 2, -1, -4, -20}, 
                      {-8, -3, 4, 2, 1}, 
                      {3, 8, 6, 1, 3}, 
                      {-4, -1, 1, 7, -6}, 
                      {0, -4, 10, -5, 1}}; 
        Console.Write("Maximum Value is " +  
                      findMaxValue(N,mat)); 
    } 
} 
  
// This code is contributed  
// by ChitraNayal
```

## PHP

```php
<?php 
// A Naive method to find maximum  
// value of $mat[d][e] - ma[a][b] 
// such that $d > $a and $e > $b 
$N = 5; 
  
// The function returns maximum  
// value A(d,e) - A(a,b) over  
// all choices of indexes such  
// that both $d > $a and $e > $b. 
function findMaxValue(&$mat) 
{ 
    global $N; 
      
    // stores maximum value 
    $maxValue = PHP_INT_MIN; 
  
    // Consider all possible  
    // pairs $mat[$a][$b] and 
    // $mat[$d][$e] 
    for ($a = 0; $a < $N - 1; $a++) 
    for ($b = 0; $b < $N - 1; $b++) 
        for ($d = $a + 1; $d < $N; $d++) 
        for ($e = $b + 1; $e < $N; $e++) 
            if ($maxValue < ($mat[$d][$e] -  
                             $mat[$a][$b])) 
                $maxValue = $mat[$d][$e] -  
                            $mat[$a][$b]; 
  
    return $maxValue; 
} 
  
// Driver Code 
$mat = array(array(1, 2, -1, -4, -20), 
             array(-8, -3, 4, 2, 1), 
             array(3, 8, 6, 1, 3), 
             array(-4, -1, 1, 7, -6), 
             array(0, -4, 10, -5, 1)); 
              
echo "Maximum Value is " .  
       findMaxValue($mat); 
  
// This code is contributed  
// by ChitraNayal 
?>
```

输出：

```
Maximum Value is 18
```

上面的程序以`O(n ^ 4)`的时间运行，这远不及`O(n ^ 2)`的预期时间复杂度

一个有效的解决方案会占用更多空间。 我们对矩阵进行预处理，以使`index(i, j)`将矩阵中从`(i, j)`到`(N-1, N-1)`的元素的最大值存储，并且在此过程中将继续更新到目前为止找到的最大值。 我们最终返回最大值。

## C++

```cpp
// An efficient method to find maximum value of mat[d] 
// - ma[a][b] such that c > a and d > b 
#include <bits/stdc++.h> 
using namespace std; 
#define N 5 
  
// The function returns maximum value A(c,d) - A(a,b) 
// over all choices of indexes such that both c > a 
// and d > b. 
int findMaxValue(int mat[][N]) 
{ 
    //stores maximum value 
    int maxValue = INT_MIN; 
  
    // maxArr[i][j] stores max of elements in matrix 
    // from (i, j) to (N-1, N-1) 
    int maxArr[N][N]; 
  
    // last element of maxArr will be same's as of 
    // the input matrix 
    maxArr[N-1][N-1] = mat[N-1][N-1]; 
  
    // preprocess last row 
    int maxv = mat[N-1][N-1];  // Initialize max 
    for (int j = N - 2; j >= 0; j--) 
    { 
        if (mat[N-1][j] > maxv) 
            maxv = mat[N - 1][j]; 
        maxArr[N-1][j] = maxv; 
    } 
  
    // preprocess last column 
    maxv = mat[N - 1][N - 1];  // Initialize max 
    for (int i = N - 2; i >= 0; i--) 
    { 
        if (mat[i][N - 1] > maxv) 
            maxv = mat[i][N - 1]; 
        maxArr[i][N - 1] = maxv; 
    } 
  
    // preprocess rest of the matrix from bottom 
    for (int i = N-2; i >= 0; i--) 
    { 
        for (int j = N-2; j >= 0; j--) 
        { 
            // Update maxValue 
            if (maxArr[i+1][j+1] - mat[i][j] > 
                                            maxValue) 
                maxValue = maxArr[i + 1][j + 1] - mat[i][j]; 
  
            // set maxArr (i, j) 
            maxArr[i][j] = max(mat[i][j], 
                               max(maxArr[i][j + 1], 
                                   maxArr[i + 1][j]) ); 
        } 
    } 
  
    return maxValue; 
} 
  
// Driver program to test above function 
int main() 
{ 
    int mat[N][N] = { 
                      { 1, 2, -1, -4, -20 }, 
                      { -8, -3, 4, 2, 1 }, 
                      { 3, 8, 6, 1, 3 }, 
                      { -4, -1, 1, 7, -6 }, 
                      { 0, -4, 10, -5, 1 } 
                    }; 
    cout << "Maximum Value is " 
         << findMaxValue(mat); 
  
    return 0; 
}
```

## Java

```java
// An efficient method to find maximum value of mat1[d] 
// - ma[a][b] such that c > a and d > b 
import java.io.*; 
import java.util.*; 
   
class GFG  
{ 
    // The function returns maximum value A(c,d) - A(a,b) 
    // over all choices of indexes such that both c > a 
    // and d > b. 
    static int findMaxValue(int N,int mat[][]) 
    { 
        //stores maximum value 
        int maxValue = Integer.MIN_VALUE; 
       
        // maxArr[i][j] stores max of elements in matrix 
        // from (i, j) to (N-1, N-1) 
        int maxArr[][] = new int[N][N]; 
       
        // last element of maxArr will be same's as of 
        // the input matrix 
        maxArr[N-1][N-1] = mat[N-1][N-1]; 
       
        // preprocess last row 
        int maxv = mat[N-1][N-1];  // Initialize max 
        for (int j = N - 2; j >= 0; j--) 
        { 
            if (mat[N-1][j] > maxv) 
                maxv = mat[N - 1][j]; 
            maxArr[N-1][j] = maxv; 
        } 
       
        // preprocess last column 
        maxv = mat[N - 1][N - 1];  // Initialize max 
        for (int i = N - 2; i >= 0; i--) 
        { 
            if (mat[i][N - 1] > maxv) 
                maxv = mat[i][N - 1]; 
            maxArr[i][N - 1] = maxv; 
        } 
       
        // preprocess rest of the matrix from bottom 
        for (int i = N-2; i >= 0; i--) 
        { 
            for (int j = N-2; j >= 0; j--) 
            { 
                // Update maxValue 
                if (maxArr[i+1][j+1] - mat[i][j] > maxValue) 
                    maxValue = maxArr[i + 1][j + 1] - mat[i][j]; 
       
                // set maxArr (i, j) 
                maxArr[i][j] = Math.max(mat[i][j], 
                                   Math.max(maxArr[i][j + 1], 
                                       maxArr[i + 1][j]) ); 
            } 
        } 
       
        return maxValue; 
    } 
      
    // Driver code 
    public static void main (String[] args)  
    { 
        int N = 5; 
  
        int mat[][] = { 
                      { 1, 2, -1, -4, -20 }, 
                      { -8, -3, 4, 2, 1 }, 
                      { 3, 8, 6, 1, 3 }, 
                      { -4, -1, 1, 7, -6 }, 
                      { 0, -4, 10, -5, 1 } 
                   }; 
  
        System.out.print("Maximum Value is " +  
                           findMaxValue(N,mat)); 
    } 
} 
   
// Contributed by Prakriti Gupta
```

## Python3

```py
# An efficient method to find maximum value  
# of mat[d] - ma[a][b] such that c > a and d > b 
  
import sys 
N = 5
  
# The function returns maximum value  
# A(c,d) - A(a,b) over all choices of  
# indexes such that both c > a and d > b. 
def findMaxValue(mat): 
  
    # stores maximum value 
    maxValue = -sys.maxsize -1
  
    # maxArr[i][j] stores max of elements  
    # in matrix from (i, j) to (N-1, N-1) 
    maxArr = [[0 for x in range(N)] 
                 for y in range(N)] 
  
    # last element of maxArr will be  
    # same's as of the input matrix 
    maxArr[N - 1][N - 1] = mat[N - 1][N - 1] 
  
    # preprocess last row 
    maxv = mat[N - 1][N - 1]; # Initialize max 
    for j in range (N - 2, -1, -1): 
      
        if (mat[N - 1][j] > maxv): 
            maxv = mat[N - 1][j] 
        maxArr[N - 1][j] = maxv 
      
    # preprocess last column 
    maxv = mat[N - 1][N - 1] # Initialize max 
    for i in range (N - 2, -1, -1): 
      
        if (mat[i][N - 1] > maxv): 
            maxv = mat[i][N - 1] 
        maxArr[i][N - 1] = maxv 
  
    # preprocess rest of the matrix 
    # from bottom 
    for i in range (N - 2, -1, -1): 
      
        for j in range (N - 2, -1, -1): 
          
            # Update maxValue 
            if (maxArr[i + 1][j + 1] -
                mat[i][j] > maxValue): 
                maxValue = (maxArr[i + 1][j + 1] - 
                                       mat[i][j]) 
  
            # set maxArr (i, j) 
            maxArr[i][j] = max(mat[i][j],  
                           max(maxArr[i][j + 1],  
                               maxArr[i + 1][j])) 
          
    return maxValue 
  
# Driver Code 
mat = [[ 1, 2, -1, -4, -20 ], 
       [-8, -3, 4, 2, 1 ], 
       [ 3, 8, 6, 1, 3 ], 
       [ -4, -1, 1, 7, -6] , 
       [0, -4, 10, -5, 1 ]] 
                      
print ("Maximum Value is", 
        findMaxValue(mat)) 
  
# This code is contributed by iAyushRaj
```

## C#

```cs
// An efficient method to find  
// maximum value of mat1[d] 
// - ma[a][b] such that c > a  
// and d > b 
using System; 
class GFG  { 
      
    // The function returns 
    // maximum value A(c,d) - A(a,b) 
    // over all choices of indexes  
    // such that both c > a 
    // and d > b. 
    static int findMaxValue(int N, int [,]mat) 
    { 
          
        //stores maximum value 
        int maxValue = int.MinValue; 
      
        // maxArr[i][j] stores max  
        // of elements in matrix 
        // from (i, j) to (N-1, N-1) 
        int [,]maxArr = new int[N, N]; 
      
        // last element of maxArr  
        // will be same's as of 
        // the input matrix 
        maxArr[N - 1, N - 1] = mat[N - 1,N - 1]; 
      
        // preprocess last row 
         // Initialize max 
        int maxv = mat[N - 1, N - 1]; 
        for (int j = N - 2; j >= 0; j--) 
        { 
            if (mat[N - 1, j] > maxv) 
                maxv = mat[N - 1, j]; 
            maxArr[N - 1, j] = maxv; 
        } 
      
        // preprocess last column 
        // Initialize max 
        maxv = mat[N - 1,N - 1];  
        for (int i = N - 2; i >= 0; i--) 
        { 
            if (mat[i, N - 1] > maxv) 
                maxv = mat[i,N - 1]; 
            maxArr[i,N - 1] = maxv; 
        } 
      
        // preprocess rest of the 
        // matrix from bottom 
        for (int i = N - 2; i >= 0; i--) 
        { 
            for (int j = N - 2; j >= 0; j--) 
            { 
                  
                // Update maxValue 
                if (maxArr[i + 1,j + 1] -  
                     mat[i, j] > maxValue) 
                    maxValue = maxArr[i + 1,j + 1] -  
                                         mat[i, j]; 
      
                // set maxArr (i, j) 
                maxArr[i,j] = Math.Max(mat[i, j], 
                              Math.Max(maxArr[i, j + 1], 
                              maxArr[i + 1, j]) ); 
            } 
        } 
      
        return maxValue; 
    } 
      
    // Driver code 
    public static void Main ()  
    { 
        int N = 5; 
  
        int [,]mat = {{ 1, 2, -1, -4, -20 }, 
                      { -8, -3, 4, 2, 1 }, 
                      { 3, 8, 6, 1, 3 }, 
                      { -4, -1, 1, 7, -6 }, 
                      { 0, -4, 10, -5, 1 }}; 
        Console.Write("Maximum Value is " +  
                        findMaxValue(N,mat)); 
    } 
} 
  
// This code is contributed by nitin mittal.
```

## PHP

```php
<?php  
// An efficient method to find  
// maximum value of mat[d] - ma[a][b]  
// such that c > a and d > b 
$N = 5; 
  
// The function returns maximum  
// value A(c,d) - A(a,b) over 
// all choices of indexes such  
// that both c > a and d > b. 
function findMaxValue($mat) 
{ 
    global $N; 
      
    // stores maximum value 
    $maxValue = PHP_INT_MIN; 
  
    // maxArr[i][j] stores max  
    // of elements in matrix 
    // from (i, j) to (N-1, N-1) 
    $maxArr[$N][$N] = array(); 
  
    // last element of maxArr  
    // will be same's as of 
    // the input matrix 
    $maxArr[$N - 1][$N - 1] = $mat[$N - 1][$N - 1]; 
  
    // preprocess last row 
    $maxv = $mat[$N - 1][$N - 1]; // Initialize max 
    for ($j = $N - 2; $j >= 0; $j--) 
    { 
        if ($mat[$N - 1][$j] > $maxv) 
            $maxv = $mat[$N - 1][$j]; 
        $maxArr[$N - 1][$j] = $maxv; 
    } 
  
    // preprocess last column 
    $maxv = $mat[$N - 1][$N - 1]; // Initialize max 
    for ($i = $N - 2; $i >= 0; $i--) 
    { 
        if ($mat[$i][$N - 1] > $maxv) 
            $maxv = $mat[$i][$N - 1]; 
        $maxArr[$i][$N - 1] = $maxv; 
    } 
  
    // preprocess rest of the 
    // matrix from bottom 
    for ($i = $N - 2; $i >= 0; $i--) 
    { 
        for ($j = $N - 2; $j >= 0; $j--) 
        { 
            // Update maxValue 
            if ($maxArr[$i + 1][$j + 1] -  
                $mat[$i][$j] > $maxValue) 
                $maxValue = $maxArr[$i + 1][$j + 1] -  
                            $mat[$i][$j]; 
  
            // set maxArr (i, j) 
            $maxArr[$i][$j] = max($mat[$i][$j], 
                              max($maxArr[$i][$j + 1], 
                                  $maxArr[$i + 1][$j])); 
        } 
    } 
  
    return $maxValue; 
} 
  
// Driver Code 
$mat = array(array(1, 2, -1, -4, -20), 
             array(-8, -3, 4, 2, 1), 
             array(3, 8, 6, 1, 3), 
             array(-4, -1, 1, 7, -6), 
             array(0, -4, 10, -5, 1) 
                    ); 
echo "Maximum Value is ".  
      findMaxValue($mat); 
  
// This code is contributed  
// by ChitraNayal 
?>
```

输出：

```
Maximum Value is 18
```

如果允许我们修改矩阵，则可以避免使用多余的空间，而应使用输入矩阵。

练习：同时打印索引`(a, b)`和`(c, d)`。