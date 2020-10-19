# 正好有`k`个硬币的路径数

> 原文： [https://www.geeksforgeeks.org/number-of-paths-with-exactly-k-coins/](https://www.geeksforgeeks.org/number-of-paths-with-exactly-k-coins/)

给定一个矩阵，其中每个单元格都有一定数量的硬币。 用正确的`k`个硬币计算从右上角到右下角的方式数。 我们可以从单元格`(i, j)`移至`(i + 1, j)`和`(i, j + 1)`。

**示例**：

```
Input:  k = 12
        mat[][] = { {1, 2, 3},
                    {4, 6, 5},
                    {3, 2, 1}
                  };
Output:  2
There are two paths with 12 coins
1 -> 2 -> 6 -> 2 -> 1
1 -> 2 -> 3 -> 5 -> 1

```

[](https://practice.geeksforgeeks.org/problem-page.php?pid=383)

## 强烈建议您在继续解决方案之前，单击这里进行练习。

可以递归定义上述问题，如下所示：

```
pathCount(m, n, k):   Number of paths to reach mat[m][n] from mat[0][0] 
                      with exactly k coins

If (m == 0 and n == 0)
   return 1 if mat[0][0] == k else return 0
Else:
    pathCount(m, n, k) = pathCount(m-1, n, k - mat[m][n]) + 
                         pathCount(m, n-1, k - mat[m][n]) 
```

下面是上述递归算法的实现。

## C++ 

```cpp

// A Naive Recursive C++ program  
// to count paths with exactly 
// 'k' coins 
#include <bits/stdc++.h> 
#define R 3 
#define C 3 
using namespace std; 

// Recursive function to count paths with sum k from 
// (0, 0) to (m, n) 
int pathCountRec(int mat[][C], int m, int n, int k) 
{ 
    // Base cases 
    if (m < 0 || n < 0) return 0; 
    if (m==0 && n==0) return (k == mat[m][n]); 

    // (m, n) can be reached either through (m-1, n) or 
    // through (m, n-1) 
    return pathCountRec(mat, m-1, n, k-mat[m][n]) + 
           pathCountRec(mat, m, n-1, k-mat[m][n]); 
} 

// A wrapper over pathCountRec() 
int pathCount(int mat[][C], int k) 
{ 
    return pathCountRec(mat, R-1, C-1, k); 
} 

// Driver program 
int main() 
{ 
    int k = 12; 
    int mat[R][C] = { {1, 2, 3}, 
                      {4, 6, 5}, 
                      {3, 2, 1} 
                  }; 
    cout << pathCount(mat, k); 
    return 0; 
}

```

## Java

```
// A Naive Recursive Java program to  
// count paths with exactly 'k' coins   
  
class GFG { 
  
    static final int R = 3; 
    static final int C = 3; 
  
// Recursive function to count paths with sum k from  
// (0, 0) to (m, n)  
    static int pathCountRec(int mat[][], int m, int n, int k) { 
        // Base cases  
        if (m < 0 || n < 0) { 
            return 0; 
        } 
        if (m == 0 && n == 0 && (k == mat[m][n])) { 
            return 1; 
        } 
  
        // (m, n) can be reached either through (m-1, n) or  
        // through (m, n-1)  
        return pathCountRec(mat, m - 1, n, k - mat[m][n]) 
                + pathCountRec(mat, m, n - 1, k - mat[m][n]); 
    } 
  
// A wrapper over pathCountRec()  
    static int pathCount(int mat[][], int k) { 
        return pathCountRec(mat, R - 1, C - 1, k); 
    } 
  
    // Driver code  
    public static void main(String[] args) { 
        int k = 12; 
        int mat[][] = {{1, 2, 3}, 
        {4, 6, 5}, 
        {3, 2, 1} 
        }; 
        System.out.println(pathCount(mat, k)); 
    } 
} 
  
/* This Java code is contributed by Rajput-Ji*/
```

## Python3

```
# A Naive Recursive Python program to 
# count paths with exactly 'k' coins 
  
R = 3
C = 3
  
# Recursive function to count paths 
# with sum k from (0, 0) to (m, n) 
def pathCountRec(mat, m, n, k): 
  
    # Base cases 
    if m < 0 or n < 0: 
        return 0
    elif m == 0 and n == 0: 
        return k == mat[m][n] 
  
    # #(m, n) can be reached either 
    # through (m-1, n) or through 
    # (m, n-1) 
    return (pathCountRec(mat, m-1, n, k-mat[m][n])  
         + pathCountRec(mat, m, n-1, k-mat[m][n])) 
  
# A wrapper over pathCountRec() 
def pathCount(mat, k): 
    return pathCountRec(mat, R-1, C-1, k) 
  
# Driver Program 
k = 12
mat = [[1, 2, 3], 
       [4, 6, 5], 
       [3, 2, 1]] 
  
print(pathCount(mat, k)) 
  
# This code is contributed by Shrikant13.
```

## C#

```
using System; 
  
// A Naive Recursive c# program to  
// count paths with exactly 'k' coins  
  
public class GFG 
{ 
  
    public const int R = 3; 
    public const int C = 3; 
  
// Recursive function to count paths with sum k from  
// (0, 0) to (m, n)  
    public static int pathCountRec(int[][] mat, int m, int n, int k) 
    { 
        // Base cases  
        if (m < 0 || n < 0) 
        { 
            return 0; 
        } 
        if (m == 0 && n == 0 && (k == mat[m][n])) 
        { 
            return 1; 
        } 
  
        // (m, n) can be reached either through (m-1, n) or  
        // through (m, n-1)  
        return pathCountRec(mat, m - 1, n, k - mat[m][n])  
                + pathCountRec(mat, m, n - 1, k - mat[m][n]); 
    } 
  
// A wrapper over pathCountRec()  
    public static int pathCount(int[][] mat, int k) 
    { 
        return pathCountRec(mat, R - 1, C - 1, k); 
    } 
  
    // Driver code  
    public static void Main(string[] args) 
    { 
        int k = 12; 
        int[][] mat = new int[][] 
        { 
            new int[] {1, 2, 3}, 
            new int[] {4, 6, 5}, 
            new int[] {3, 2, 1} 
        }; 
        Console.WriteLine(pathCount(mat, k)); 
    } 
} 
  
// This code is contributed by Shrikant13
```

## PHP

```
<?php 
// A Naive Recursive PHP program to 
// count paths with exactly 'k' coins 
  
$R = 3; 
$C = 3; 
  
// Recursive function to count paths 
// with sum k from (0, 0) to (m, n) 
function pathCountRec( $mat, $m, $n, $k) 
{ 
      
    // Base cases 
    if ($m < 0 or $n < 0)  
        return 0; 
    if ($m == 0 and $n == 0)  
        return ($k == $mat[$m][$n]); 
  
    // (m, n) can be reached either  
    // through (m-1, n) or through  
    // (m, n-1) 
    return pathCountRec($mat, $m - 1, 
                $n, $k - $mat[$m][$n]) 
              + pathCountRec($mat, $m, 
           $n - 1, $k - $mat[$m][$n]); 
} 
  
// A wrapper over pathCountRec() 
function pathCount($mat, $k) 
{ 
    global $R, $C; 
    return pathCountRec($mat, $R-1,  
                            $C-1, $k); 
} 
  
// Driver program 
  
    $k = 12; 
    $mat = array(array(1, 2, 3), 
                 array(4, 6, 5), 
                 array(3, 2, 1) ); 
                   
    echo pathCount($mat, $k); 
  
// This code is contributed by anuj_67. 
?>
```

输出：

```
2
```

上述解决方案递归的时间复杂度是指数的。 我们可以使用动态编程在伪多项式时间（时间复杂度取决于输入的数值）中解决此问题。 这个想法是使用 3 维表`dp[m][n][k]`，其中`m`是行号，`n`是列号，`k`是硬币数。 下面是基于动态编程的实现。

## C++

```
// A Dynamic Programming based C++ program to count paths with 
// exactly 'k' coins 
#include <bits/stdc++.h> 
#define R 3 
#define C 3 
#define MAX_K 1000 
using namespace std; 
  
int dp[R][C][MAX_K]; 
  
int pathCountDPRecDP(int mat[][C], int m, int n, int k) 
{ 
    // Base cases 
    if (m < 0 || n < 0) return 0; 
    if (m==0 && n==0) return (k == mat[m][n]); 
  
    // If this subproblem is already solved 
    if (dp[m][n][k] != -1) return dp[m][n][k]; 
  
    // (m, n) can be reached either through (m-1, n) or 
    // through (m, n-1) 
    dp[m][n][k] = pathCountDPRecDP(mat, m-1, n, k-mat[m][n]) + 
                  pathCountDPRecDP(mat, m, n-1, k-mat[m][n]); 
  
    return dp[m][n][k]; 
} 
  
// This function mainly initializes dp[][][] and calls 
// pathCountDPRecDP() 
int pathCountDP(int mat[][C], int k) 
{ 
    memset(dp, -1, sizeof dp); 
    return pathCountDPRecDP(mat, R-1, C-1, k); 
} 
  
// Driver Program to test above functions 
int main() 
{ 
    int k = 12; 
    int mat[R][C] = { {1, 2, 3}, 
                      {4, 6, 5}, 
                      {3, 2, 1} 
                  }; 
    cout << pathCountDP(mat, k); 
    return 0; 
}
```

## Java

```
// A Dynamic Programming based JAVA program to count paths with 
// exactly 'k' coins 
  
  
class GFG 
{ 
      
    static final int R = 3; 
    static final int C = 3; 
    static final int MAX_K = 100; 
      
    static int [][][]dp=new int[R][C][MAX_K]; 
      
    static int pathCountDPRecDP(int [][]mat, int m, int n, int k) 
    { 
        // Base cases 
        if (m < 0 || n < 0) return 0; 
        if (m==0 && n==0) return (k == mat[m][n] ? 1 : 0); 
      
        // If this subproblem is already solved 
        if (dp[m][n][k] != -1) return dp[m][n][k]; 
      
        // (m, n) can be reached either through (m-1, n) or 
        // through (m, n-1) 
        dp[m][n][k] = pathCountDPRecDP(mat, m-1, n, k-mat[m][n]) + 
                    pathCountDPRecDP(mat, m, n-1, k-mat[m][n]); 
      
        return dp[m][n][k]; 
    } 
      
    // This function mainly initializes dp[][][] and calls 
    // pathCountDPRecDP() 
    static int pathCountDP(int [][]mat, int k) 
    { 
        for(int i=0;i<R;i++) 
            for(int j=0;j<C;j++) 
                for(int l=0;l<MAX_K;l++) 
                  dp[i][j][l]=-1; 
                    
        return pathCountDPRecDP(mat, R-1, C-1, k); 
    } 
      
    // Driver Program to test above functions 
    public static void main(String []args) 
    { 
        int k = 12; 
        int[][] mat = new int[][] 
        { 
            new int[] {1, 2, 3}, 
            new int[] {4, 6, 5}, 
            new int[] {3, 2, 1} 
        }; 
                      
        System.out.println(pathCountDP(mat, k)); 
          
    } 
  
} 
  
// This code is contributed by ihritik
```

## Python3

```
# A Dynamic Programming based Python3 program to 
# count paths with exactly 'k' coins 
R = 3
C = 3
MAX_K = 1000
  
def pathCountDPRecDP(mat, m, n, k): 
  
    # Base cases 
    if m < 0 or n < 0: 
        return 0
    elif m == 0 and n == 0: 
        return k == mat[m][n] 
      
    # If this subproblem is already solved 
    if (dp[m][n][k] != -1): 
        return dp[m][n][k] 
  
    # #(m, n) can be reached either 
    # through (m-1, n) or through 
    # (m, n-1) 
    dp[m][n][k] = (pathCountDPRecDP(mat, m - 1, n, k - mat[m][n]) + 
                   pathCountDPRecDP(mat, m, n - 1, k - mat[m][n])) 
      
    return dp[m][n][k] 
  
# A wrapper over pathCountDPRecDP() 
def pathCountDP(mat, k): 
    return pathCountDPRecDP(mat, R - 1, C - 1, k) 
  
# Driver Code 
k = 12
  
# Initialising dp[][][] 
dp = [[ [-1 for col in range(MAX_K)]  
            for col in range(C)]  
            for row in range(R)] 
  
mat = [[1, 2, 3], 
       [4, 6, 5], 
       [3, 2, 1]] 
  
print(pathCountDP(mat, k)) 
  
# This code is contributed by ashutosh450
```

## C#

```
// A Dynamic Programming based C# program  
// to count paths with exactly 'k' coins 
using System; 
  
class GFG 
{ 
    static readonly int R = 3; 
    static readonly int C = 3; 
    static readonly int MAX_K = 100; 
      
    static int [,,]dp = new int[R, C, MAX_K]; 
      
    static int pathCountDPRecDP(int [,]mat, int m,  
                                int n, int k) 
    { 
        // Base cases 
        if (m < 0 || n < 0) return 0; 
        if (m == 0 && n == 0)  
            return (k == mat[m, n] ? 1 : 0); 
      
        // If this subproblem is already solved 
        if (dp[m, n, k] != -1) return dp[m, n, k]; 
      
        // (m, n) can be reached either through (m-1, n) or 
        // through (m, n-1) 
        dp[m, n, k] = pathCountDPRecDP(mat, m - 1, n, k - mat[m, n]) + 
                      pathCountDPRecDP(mat, m, n - 1, k - mat[m, n]); 
      
        return dp[m, n, k]; 
    } 
      
    // This function mainly initializes [,]dp[] and  
    // calls pathCountDPRecDP() 
    static int pathCountDP(int [,]mat, int k) 
    { 
        for(int i = 0; i < R; i++) 
            for(int j = 0; j < C; j++) 
                for(int l = 0; l < MAX_K; l++) 
                dp[i, j, l] = -1; 
                      
        return pathCountDPRecDP(mat, R - 1, C - 1, k); 
    } 
      
    // Driver Code 
    public static void Main(String []args) 
    { 
        int k = 12; 
        int[,] mat = { {1, 2, 3}, 
                       {4, 6, 5}, 
                       {3, 2, 1}}; 
                      
        Console.WriteLine(pathCountDP(mat, k)); 
    } 
} 
  
// This code is contributed by PrinciRaj1992
```

输出：

```
2
```

该解决方案的时间复杂度为`O(m * n * k)`。