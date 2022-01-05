# 求给定和的子矩阵

> 原文:[https://www . geesforgeks . org/find-sub-matrix-with-the-given-sum/](https://www.geeksforgeeks.org/find-sub-matrix-with-the-given-sum/)

给定一个**N×N**矩阵和两个整数 **S** 和 **K** ，任务是找出是否存在和等于 **S** 的**K×K**子矩阵。

**示例:**

> **输入:** K = 2，S = 14，mat[][] = {
> { 1，2，3，4 }，
> { 5，6，7，8 }，
> { 9，10，11，12 }，
> { 13，14，15，16 }}
> **输出:**是
> 1 2
> 5 6
> 是所需的 2×2 子矩阵，元素和= 14
> 
> **输入:** K = 1，S = 5，mat[][] = {{1，2}，{7，8 } }
> T3】输出:否

**方法:**动态规划可以解决这个问题，

*   创建一个数组 **dp[N + 1][N + 1]** ，其中 **dp[i][j]** 存储所有元素的和，行在 **1** 到 **i** 之间，列在 **1** 到 **j** 之间。
*   一旦二维矩阵生成，现在假设我们希望找到从 **(i，j)** 到 **(i + x，j + x)** 的平方和。所需金额将为**DP[I+x][j+x]–DP[I][j+x]–DP[I+x][j]+DP[I][j]**，其中:
    1.  第一项表示存在于 **1** 到 **i + x** 之间的行和 **1** 到 **j + x** 之间的列中的所有元素的总和。这个地区有我们需要的广场。
    2.  第二个两项是去掉我们需要的区域之外但在第一步计算的区域之内的区域。
    3.  第二步减去 **1** 到 **i** 之间的行和 **1** 到 **j** 之间的列的元素之和两次，所以加一次。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define N 4

// Function to return the sum of the sub-matrix
int getSum(int r1, int r2, int c1, int c2,
           int dp[N + 1][N + 1])
{
    return dp[r2][c2] - dp[r2][c1] - dp[r1][c2]
           + dp[r1][c1];
}

// Function that returns true if it is possible
// to find the sub-matrix with required sum
bool sumFound(int K, int S, int grid[N][N])
{

    // 2-D array to store the sum of
    // all the sub-matrices
    int dp[N + 1][N + 1];

    // Filling of dp[][] array
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            dp[i + 1][j + 1] = dp[i + 1][j] + dp[i][j + 1]
                               - dp[i][j] + grid[i][j];

    // Checking for each possible sub-matrix of size k X k
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++) {
            int sum = getSum(i, i + K, j, j + K, dp);

            if (sum == S)
                return true;
        }

    // Sub-matrix with the given sum not found
    return false;
}

// Driver code
int main()
{
    int grid[N][N] = { { 1, 2, 3, 4 },
                       { 5, 6, 7, 8 },
                       { 9, 10, 11, 12 },
                       { 13, 14, 15, 16 } };
    int K = 2;
    int S = 14;

    // Function call
    if (sumFound(K, S, grid))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}
// Modified by Kartik Verma
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG {
    static int N = 4;

    // Function to return the sum of the sub-matrix
    static int getSum(int r1, int r2, int c1, int c2,
                      int dp[][])
    {
        return dp[r2][c2] - dp[r2][c1] - dp[r1][c2]
            + dp[r1][c1];
    }

    // Function that returns true if it is possible
    // to find the sub-matrix with required sum
    static boolean sumFound(int K, int S, int grid[][])
    {

        // 2-D array to store the sum of
        // all the sub-matrices
        int dp[][] = new int[N + 1][N + 1];

        // Filling of dp[][] array
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                dp[i + 1][j + 1] = dp[i + 1][j]
                                   + dp[i][j + 1] - dp[i][j]
                                   + grid[i][j];
            }
        }

        // Checking for each possible sub-matrix of size k X
        // k
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                int sum = getSum(i, i + K, j, j + K, dp);

                if (sum == S) {
                    return true;
                }
            }
        }

        // Sub-matrix with the given sum not found
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        int grid[][] = { { 1, 2, 3, 4 },
                         { 5, 6, 7, 8 },
                         { 9, 10, 11, 12 },
                         { 13, 14, 15, 16 } };
        int K = 2;
        int S = 14;

        // Function call
        if (sumFound(K, S, grid)) {
            System.out.println("Yes");
        }
        else {
            System.out.println("No");
        }
    }
}

// This code contributed by Rajput-Ji
// Modified by Kartik Verma
```

## 蟒蛇 3

```
# Python implementation of the approach
N = 4

# Function to return the sum of the sub-matrix

def getSum(r1, r2, c1, c2, dp):
    return dp[r2][c2] - dp[r2][c1] - dp[r1][c2] + dp[r1][c1]

# Function that returns true if it is possible
# to find the sub-matrix with required sum
def sumFound(K, S, grid):

    # 2-D array to store the sum of
    # all the sub-matrices
    dp = [[0 for i in range(N+1)] for j in range(N+1)]

    # Filling of dp[][] array
    for i in range(N):
        for j in range(N):
            dp[i + 1][j + 1] = dp[i + 1][j] + \
                dp[i][j + 1] - dp[i][j] + grid[i][j]

    # Checking for each possible sub-matrix of size k X k
    for i in range(0, N):
        for j in range(0, N):
            sum = getSum(i, i + K, j, j + K, dp)
            if (sum == S):
                return True

    # Sub-matrix with the given sum not found
    return False

# Driver code
grid = [[1, 2, 3, 4],
        [5, 6, 7, 8],
        [9, 10, 11, 12],
        [13, 14, 15, 16]]
K = 2
S = 14

# Function call
if (sumFound(K, S, grid)):
    print("Yes")
else:
    print("No")

# This code is contributed by ankush_953
# Modified by Kartik Verma
```

## C#

```
// C# implementation of the approach
using System;

class GfG {
    static int N = 4;

    // Function to return the sum of the sub-matrix
    static int getSum(int r1, int r2, int c1, int c2,
                      int[, ] dp)
    {
        return dp[r2, c2] - dp[r2, c1] - dp[r1, c2]
            + dp[r1, c1];
    }

    // Function that returns true if it is possible
    // to find the sub-matrix with required sum
    static bool sumFound(int K, int S, int[, ] grid)
    {

        // 2-D array to store the sum of
        // all the sub-matrices
        int[, ] dp = new int[N + 1, N + 1];

        // Filling of dp[,] array
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                dp[i + 1, j + 1] = dp[i + 1, j]
                                   + dp[i, j + 1] - dp[i, j]
                                   + grid[i, j];
            }
        }

        // Checking for each possible sub-matrix of size k X
        // k
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                int sum = getSum(i, i + K, j, j + K, dp);

                if (sum == S) {
                    return true;
                }
            }
        }

        // Sub-matrix with the given sum not found
        return false;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[, ] grid = { { 1, 2, 3, 4 },
                         { 5, 6, 7, 8 },
                         { 9, 10, 11, 12 },
                         { 13, 14, 15, 16 } };
        int K = 2;
        int S = 14;

        // Function call
        if (sumFound(K, S, grid)) {
            Console.WriteLine("Yes");
        }
        else {
            Console.WriteLine("No");
        }
    }
}

// This code has been contributed by 29AjayKumar
// Modified by Kartik Verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

$GLOBALS['N'] = 4;

// Function to return the sum of
// the sub-matrix
function getSum($r1, $r2, $c1, $c2, $dp)
{
    return $dp[$r2][$c2] - $dp[$r2][$c1] -
           $dp[$r1][$c2] + $dp[$r1][$c1];
}

// Function that returns true if it is
// possible to find the sub-matrix with
// required sum
function sumFound($K, $S, $grid)
{

    // 2-D array to store the sum of
    // all the sub-matrices
    $dp = array(array());

    for ($i = 0; $i < $GLOBALS['N']; $i++)
        for ($j = 0; $j < $GLOBALS['N']; $j++)
            $dp[$i][$j] = 0 ;

    // Filling of dp[][] array
    for ($i = 0; $i < $GLOBALS['N']; $i++)
        for ($j = 0; $j < $GLOBALS['N']; $j++)
            $dp[$i + 1][$j + 1] = $dp[$i + 1][$j] +
                                  $dp[$i][$j + 1] -
                                  $dp[$i][$j] +
                                  $grid[$i][$j];

    // Checking for each possible sub-matrix
    // of size k X k
    for ($i = 0;
         $i < $GLOBALS['N']; $i++)
        for ($j = 0;
             $j < $GLOBALS['N']; $j++)
        {
            $sum = getSum($i, $i + $K, $j,
                          $j + $K, $dp);

            if ($sum == $S)
                return true;
        }

    // Sub-matrix with the given
    // sum not found
    return false;
}

// Driver code
$grid = array(array(1, 2, 3, 4),
              array(5, 6, 7, 8),
              array(9, 10, 11, 12),
              array(13, 14, 15, 16));
$K = 2;
$S = 14;

// Function call
if (sumFound($K, $S, $grid))
    echo "Yes";
else
    echo "No";

// This code is contributed by Ryuga
//Modified by Kartik Verma
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var N = 4

// Function to return the sum of the sub-matrix
function getSum(r1, r2, c1, c2, dp)
{
    return dp[r2][c2] - dp[r2][c1] - dp[r1][c2]
           + dp[r1][c1];
}

// Function that returns true if it is possible
// to find the sub-matrix with required sum
function sumFound(K, S, grid)
{

    // 2-D array to store the sum of
    // all the sub-matrices
    var dp = Array.from(Array(N+1), ()=> Array(N+1).fill(0));

    // Filling of dp[][] array
    for (var i = 0; i < N; i++)
        for (var j = 0; j < N; j++)
            dp[i + 1][j + 1] = dp[i + 1][j] + dp[i][j + 1]
                               - dp[i][j] + grid[i][j];

    // Checking for each possible sub-matrix of size k X k
    for (var i = 0; i < N; i++)
        for (var j = 0; j < N; j++) {
            var sum = getSum(i, i + K, j, j + K, dp);

            if (sum == S)
                return true;
        }

    // Sub-matrix with the given sum not found
    return false;
}

// Driver code
var grid = [ [ 1, 2, 3, 4 ],
                   [ 5, 6, 7, 8 ],
                   [ 9, 10, 11, 12 ],
                   [ 13, 14, 15, 16 ] ];
var K = 2;
var S = 14;
// Function call
if (sumFound(K, S, grid))
    document.write( "Yes");
else
    document.write( "No" );

</script>
```

**Output:** 

```
Yes
```