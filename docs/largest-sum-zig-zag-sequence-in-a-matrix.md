# 矩阵中最大和之字形序列

> 原文:[https://www . geesforgeks . org/maximum-sum-zig-zag-sequence-in-a-matrix/](https://www.geeksforgeeks.org/largest-sum-zig-zag-sequence-in-a-matrix/)

给定一个 n×n 的矩阵，求和最大的锯齿形序列的和。之字形序列从顶部开始，到底部结束。序列的两个连续元素不能属于同一列。

**示例:**

```
Input : mat[][] = 3  1  2
                  4  8  5
                  6  9  7
Output : 18
Zigzag sequence is: 3->8->7
Another such sequence is 2->4->7

Input : mat[][] =  4  2  1
                   3  9  6
                  11  3 15
Output : 28
```

这个问题有一个 [**最优子结构**](https://www.geeksforgeeks.org/dynamic-programming-set-2-optimal-substructure-property/) 。

```
Maximum Zigzag sum starting from arr[i][j] to a 
bottom cell can be written as :
zzs(i, j) = arr[i][j] + max(zzs(i+1, k)), 
               where k = 0, 1, 2 and k != j
zzs(i, j) = arr[i][j], if i = n-1 

We have to find the largest among all as
Result = zzs(0, j) where 0 <= j < n
```

## C++

```
// C++ program to find the largest sum zigzag sequence
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

// Returns largest sum of a Zigzag sequence starting
// from (i, j) and ending at a bottom cell.
int largestZigZagSumRec(int mat[][MAX], int i,
                                int j, int n)
{
   // If we have reached bottom
   if (i == n-1)
     return mat[i][j];

   // Find the largest sum by considering all
   // possible next elements in sequence.
   int zzs = 0;
   for (int k=0; k<n; k++)
     if (k != j)
       zzs = max(zzs, largestZigZagSumRec(mat, i+1, k, n));

   return zzs + mat[i][j];
}

// Returns largest possible sum of a Zigzag sequence
// starting from top and ending at bottom.
int largestZigZag(int mat[][MAX], int n)
{
   // Consider all cells of top row as starting point
   int res = 0;
   for (int j=0; j<n; j++)
     res = max(res, largestZigZagSumRec(mat, 0, j, n));

   return res;
}

// Driver program to test above
int main()
{
    int n = 3;
    int  mat[][MAX] = { {4, 2, 1},
                        {3, 9, 6},
                        {11, 3, 15}};
    cout << "Largest zigzag sum: " << largestZigZag(mat, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the largest sum
// zigzag sequence
import java.io.*;

class GFG {

    static int MAX = 100;

    // Returns largest sum of a Zigzag
    // sequence starting from (i, j)
    // and ending at a bottom cell.
    static int largestZigZagSumRec(int mat[][],
                            int i, int j, int n)
    {

        // If we have reached bottom
        if (i == n-1)
            return mat[i][j];

        // Find the largest sum by considering all
        // possible next elements in sequence.
        int zzs = 0;

        for (int k=0; k<n; k++)
            if (k != j)
            zzs = Math.max(zzs,
               largestZigZagSumRec(mat, i+1, k, n));

        return zzs + mat[i][j];
    }

    // Returns largest possible sum of a Zigzag
    // sequence starting from top and ending
    // at bottom.
    static int largestZigZag(int mat[][], int n)
    {
        // Consider all cells of top row as starting
        // point
        int res = 0;
        for (int j=0; j<n; j++)
            res = Math.max(res,
                   largestZigZagSumRec(mat, 0, j, n));

        return res;
    }

    // Driver program to test above
    public static void main (String[] args)
    {
        int n = 3;

        int mat[][] = { {4, 2, 1},
                        {3, 9, 6},
                        {11, 3, 15} };
        System.out.println( "Largest zigzag sum: "
                       + largestZigZag(mat, n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to find the largest
# sum zigzag sequence
MAX = 100

# Returns largest sum of a Zigzag
# sequence starting from (i, j) and
# ending at a bottom cell.
def largestZigZagSumRec( mat, i, j, n):

    # If we have reached bottom
    if (i == n-1):
        return mat[i][j]

    # Find the largest sum by considering all
    # possible next elements in sequence.
    zzs = 0
    for k in range(n):
        if (k != j):
            zzs = max(zzs, largestZigZagSumRec(mat, i + 1, k, n))

    return zzs + mat[i][j]

# Returns largest possible sum of a
# Zigzag sequence starting from top
# and ending at bottom.
def largestZigZag(mat, n):

    # Consider all cells of top row as
    # starting point
    res = 0
    for j in range(n):
        res = max(res, largestZigZagSumRec(mat, 0, j, n))

    return res

# Driver Code
if __name__ == "__main__":
    n = 3
    mat = [ [4, 2, 1],
            [3, 9, 6],
            [11, 3, 15]]
    print("Largest zigzag sum: " ,
           largestZigZag(mat, n))

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to find the largest sum
// zigzag sequence
using System;
class GFG {

    // static int MAX = 100;

    // Returns largest sum of a Zigzag
    // sequence starting from (i, j)
    // and ending at a bottom cell.
    static int largestZigZagSumRec(int [,]mat,
                          int i, int j, int n)
    {

        // If we have reached bottom
        if (i == n-1)
            return mat[i,j];

        // Find the largest sum by considering all
        // possible next elements in sequence.
        int zzs = 0;

        for (int k = 0; k < n; k++)
            if (k != j)
            zzs = Math.Max(zzs, largestZigZagSumRec(mat,
                                           i + 1, k, n));

        return zzs + mat[i,j];
    }

    // Returns largest possible
    // sum of a Zigzag sequence
    // starting from top and ending
    // at bottom.
    static int largestZigZag(int [,]mat, int n)
    {

        // Consider all cells of
        // top row as starting
        // point
        int res = 0;
        for (int j = 0; j < n; j++)
            res = Math.Max(res,
                largestZigZagSumRec(mat, 0, j, n));

        return res;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 3;
        int [,]mat = {{4, 2, 1},
                      {3, 9, 6},
                      {11, 3, 15}};
        Console.WriteLine("Largest zigzag sum: "
                           + largestZigZag(mat, n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// largest sum zigzag sequence

$MAX = 100;

// Returns largest sum of a
// Zigzag sequence starting
// from (i, j) and ending at
// a bottom cell.
function largestZigZagSumRec($mat, $i,
                              $j, $n)
{
    // If we have reached bottom
    if ($i == $n - 1)
        return $mat[$i][$j];

    // Find the largest sum
    // by considering all
    // possible next elements
    // in sequence.
    $zzs = 0;
    for ($k = 0; $k < $n; $k++)
        if ($k != $j)
        $zzs = max($zzs, largestZigZagSumRec($mat,
                                $i + 1, $k, $n));

    return $zzs + $mat[$i][$j];
}

// Returns largest possible
// sum of a Zigzag sequence
// starting from top and
// ending at bottom.
function largestZigZag( $mat, $n)
{

    // Consider all cells of top
    // row as starting point
    $res = 0;
    for ($j = 0; $j < $n; $j++)
        $res = max($res, largestZigZagSumRec(
                            $mat, 0, $j, $n));

    return $res;
}

    // Driver Code
    $n = 3;
    $mat = array(array(4, 2, 1),
                 array(3, 9, 6),
                 array(11, 3, 15));
    echo "Largest zigzag sum: " , largestZigZag($mat, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find the largest sum
// zigzag sequence

    let  MAX = 100;

    // Returns largest sum of a Zigzag
    // sequence starting from (i, j)
    // and ending at a bottom cell.
    function largestZigZagSumRec(mat,i,j,n)
    {
        // If we have reached bottom
        if (i == n-1)
            return mat[i][j];

        // Find the largest sum by considering all
        // possible next elements in sequence.
        let zzs = 0;

        for (let k=0; k<n; k++)
            if (k != j)
            zzs = Math.max(zzs,
               largestZigZagSumRec(mat, i+1, k, n));

        return zzs + mat[i][j];
    }

    // Returns largest possible sum of a Zigzag
    // sequence starting from top and ending
    // at bottom.
    function largestZigZag(mat,n)
    {
        // Consider all cells of top row as starting
        // point
        let res = 0;
        for (let j=0; j<n; j++)
            res = Math.max(res,
                   largestZigZagSumRec(mat, 0, j, n));

        return res;
    }

    // Driver program to test above
    let n = 3;

    let mat = [ [4, 2, 1],
            [3, 9, 6],
            [11, 3, 15]];
       document.write("Largest zigzag sum: " +
           largestZigZag(mat, n))

    // This code is contributed by rag2127

</script>
```

**输出:**

```
Largest zigzag sum: 28
```

[**【重叠子问题】**](https://www.geeksforgeeks.org/dynamic-programming-set-1/)
考虑到上述实现，对于大小为 3×3 的矩阵 mat【】【】，为了找到元素 mat(i，j)的之字形和(zzs)，形成以下递归树。

```
Recursion tree for cell (0, 0)
             zzs(0,0)                                
           /         \                               
    zzs(1,1)           zzs(1,2)                      
    /     \            /      \                      
zzs(2,0)  zzs(2,2)  zzs(2,0)  zzs(2,1)               

Recursion tree for cell (0, 1)
            zzs(0,1)
           /         \              
    zzs(1,0)          zzs(1,2)
    /     \            /      \    
zzs(2,1)  zzs(2,2)  zzs(2,0)  zzs(2,1)

Recursion tree for cell (0, 2)
             zzs(0,2)
           /         \                                             
    zzs(1,0)           zzs(1,1)                             
    /     \            /      \                             
 zzs(2,1)  zzs(2,2)  zzs(2,0)  zzs(2,2)
```

我们可以看到有很多子问题被一次又一次地解决。因此，该问题具有重叠子结构性质，用记忆法或制表法都可以避免同一子问题的重新计算。下面是 LIS 问题的列表实现。

## C++

```
// Memoization based C++ program to find the largest
// sum zigzag sequence
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;
int dp[MAX][MAX];

// Returns largest sum of a Zigzag sequence starting
// from (i, j) and ending at a bottom cell.
int largestZigZagSumRec(int mat[][MAX], int i,
                                int j, int n)
{
   if (dp[i][j] != -1)
      return dp[i][j];

   // If we have reached bottom
   if (i == n-1)
     return (dp[i][j] = mat[i][j]);

   // Find the largest sum by considering all
   // possible next elements in sequence.
   int zzs = 0;
   for (int k=0; k<n; k++)
     if (k != j)
       zzs = max(zzs, largestZigZagSumRec(mat, i+1, k, n));

   return (dp[i][j] = (zzs + mat[i][j]));
}

// Returns largest possible sum of a Zigzag sequence
// starting from top and ending at bottom.
int largestZigZag(int mat[][MAX], int n)
{
   memset(dp, -1, sizeof(dp));

   // Consider all cells of top row as starting point
   int res = 0;
   for (int j=0; j<n; j++)
     res = max(res, largestZigZagSumRec(mat, 0, j, n));

   return res;
}

// Driver program to test above
int main()
{
    int n = 3;
    int  mat[][MAX] = { {4, 2, 1},
                        {3, 9, 6},
                        {11, 3, 15}};
    cout << "Largest zigzag sum: " << largestZigZag(mat, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Memoization based Java program to find the largest
// sum zigzag sequence
class GFG
{

static int MAX = 100;
static int [][]dp = new int[MAX][MAX];

// Returns largest sum of a Zigzag sequence starting
// from (i, j) and ending at a bottom cell.
static int largestZigZagSumRec(int mat[][], int i,
                                int j, int n)
{
    if (dp[i][j] != -1)
        return dp[i][j];

    // If we have reached bottom
    if (i == n - 1)
        return (dp[i][j] = mat[i][j]);

    // Find the largest sum by considering all
    // possible next elements in sequence.
    int zzs = 0;
    for (int k = 0; k < n; k++)
        if (k != j)
            zzs = Math.max(zzs, largestZigZagSumRec(mat,
                                    i + 1, k, n));

    return (dp[i][j] = (zzs + mat[i][j]));
}

// Returns largest possible sum of a Zigzag sequence
// starting from top and ending at bottom.
static int largestZigZag(int mat[][], int n)
{
    for (int i = 0; i < MAX; i++)
        for (int k = 0; k < MAX; k++)
                dp[i][k] = -1;

    // Consider all cells of top row as starting point
    int res = 0;
    for (int j = 0; j < n; j++)
        res = Math.max(res, largestZigZagSumRec(mat,
                                           0, j, n));

    return res;
}

// Driver code
public static void main(String[] args)
{
    int n = 3;
    int mat[][] = { {4, 2, 1},
                    {3, 9, 6},
                    {11, 3, 15}};
    System.out.print("Largest zigzag sum: " +
                        largestZigZag(mat, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Memoization based Python3 program to find the largest
# sum zigzag sequence
MAX = 100;

dp = [[0 for i in range(MAX)] for j in range(MAX)]

# Returns largest sum of a Zigzag sequence starting
# from (i, j) and ending at a bottom cell.
def largestZigZagSumRec(mat, i, j, n):
    if (dp[i][j] != -1):
        return dp[i][j];

    # If we have reached bottom
    if (i == n - 1):
        dp[i][j] = mat[i][j];
        return (dp[i][j]);

    # Find the largest sum by considering all
    # possible next elements in sequence.
    zzs = 0;
    for k in range(n):
        if (k != j):
            zzs = max(zzs, largestZigZagSumRec(mat,
                     i + 1, k, n));
    dp[i][j] = (zzs + mat[i][j]);
    return (dp[i][j]);

# Returns largest possible sum of a Zigzag sequence
# starting from top and ending at bottom.
def largestZigZag(mat, n):
    for i in range(MAX):
        for k in range(MAX):
            dp[i][k] = -1;

    # Consider all cells of top row as starting point
    res = 0;
    for j in range(n):
        res = max(res, largestZigZagSumRec(mat, 0, j, n));

    return res;

# Driver code
if __name__ == '__main__':
    n = 3;
    mat = [[4, 2, 1], [3, 9, 6], [11, 3, 15]];
    print("Largest zigzag sum: ", largestZigZag(mat, n));

# This code is contributed by Rajput-Ji
```

## C#

```
// Memoization based C# program to find the largest
// sum zigzag sequence
using System;

class GFG
{

static int MAX = 100;
static int [,]dp = new int[MAX, MAX];

// Returns largest sum of a Zigzag sequence starting
// from (i, j) and ending at a bottom cell.
static int largestZigZagSumRec(int [,]mat, int i,
                                int j, int n)
{
    if (dp[i, j] != -1)
        return dp[i, j];

    // If we have reached bottom
    if (i == n - 1)
        return (dp[i, j] = mat[i, j]);

    // Find the largest sum by considering all
    // possible next elements in sequence.
    int zzs = 0;
    for (int k = 0; k < n; k++)
        if (k != j)
            zzs = Math.Max(zzs, largestZigZagSumRec(mat,
                                    i + 1, k, n));

    return (dp[i, j] = (zzs + mat[i, j]));
}

// Returns largest possible sum of a Zigzag sequence
// starting from top and ending at bottom.
static int largestZigZag(int [,]mat, int n)
{
    for (int i = 0; i < MAX; i++)
        for (int k = 0; k < MAX; k++)
                dp[i, k] = -1;

    // Consider all cells of top row as starting point
    int res = 0;
    for (int j = 0; j < n; j++)
        res = Math.Max(res, largestZigZagSumRec(mat,
                                        0, j, n));
    return res;
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;
    int [,]mat = { {4, 2, 1},
                    {3, 9, 6},
                    {11, 3, 15}};
    Console.Write("Largest zigzag sum: " +
                        largestZigZag(mat, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Memoization based Javascript program to find the largest
// sum zigzag sequence

    let MAX = 100;
    let dp=new Array(MAX);

    // Returns largest sum of a Zigzag sequence starting
// from (i, j) and ending at a bottom cell.
    function largestZigZagSumRec(mat,i,j,n)
    {
        if (dp[i][j] != -1)
        return dp[i][j];

    // If we have reached bottom
    if (i == n - 1)
        return (dp[i][j] = mat[i][j]);

    // Find the largest sum by considering all
    // possible next elements in sequence.
    let zzs = 0;
    for (let k = 0; k < n; k++)
        if (k != j)
            zzs = Math.max(zzs, largestZigZagSumRec(mat,
                                    i + 1, k, n));

    return (dp[i][j] = (zzs + mat[i][j]));
    }

    // Returns largest possible sum of a Zigzag sequence
// starting from top and ending at bottom.
    function largestZigZag(mat,n)
    {
        for (let i = 0; i < MAX; i++)
        {
            dp[i]=new Array(MAX);
            for (let k = 0; k < MAX; k++)
                dp[i][k] = -1;
         }
    // Consider all cells of top row as starting point
    let res = 0;
    for (let j = 0; j < n; j++)
        res = Math.max(res, largestZigZagSumRec(mat,
                                           0, j, n));

    return res;
    }

    // Driver code
    let n = 3;
    let mat=[[4, 2, 1],[3, 9, 6],[11, 3, 15]];
    document.write("Largest zigzag sum: " +
                        largestZigZag(mat, n));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Largest zigzag sum: 28
```