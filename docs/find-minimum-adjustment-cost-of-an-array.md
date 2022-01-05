# 求一个数组的最小调整成本

> 原文:[https://www . geesforgeks . org/find-最小调整-阵列成本/](https://www.geeksforgeeks.org/find-minimum-adjustment-cost-of-an-array/)

给定一个正整数数组，替换数组中的每个元素，使数组中相邻元素之间的差小于或等于给定的目标。我们需要最小化调整成本，也就是新旧价值差异的总和。我们基本上需要最小化∑| A[I]–A<sub>new</sub>[I]|其中 0 ≤ i ≤ n-1，n 为 A[]的大小，A <sub>new</sub> []为相邻差小于或等于目标的数组。
假设数组的所有元素都小于常数 M = 100。
**例:**

```
Input: arr = [1, 3, 0, 3], target = 1
Output: Minimum adjustment cost is 3
Explanation: One of the possible solutions 
is [2, 3, 2, 3]

Input: arr = [2, 3, 2, 3], target = 1
Output: Minimum adjustment cost is 0
Explanation:  All adjacent elements in the input 
array are already less than equal to given target

Input: arr = [55, 77, 52, 61, 39, 6, 
             25, 60, 49, 47], target = 10
Output: Minimum adjustment cost is 75
Explanation: One of the possible solutions is 
[55, 62, 52, 49, 39, 29, 30, 40, 49, 47]
```

为了最小化调整成本∑| A[I]–A<sub>新的</sub> [i]|对于数组中的所有索引 I，| A[I]–A<sub>新的</sub> [i]|应该尽可能接近于零。另外，| A[I]–A<sub>新增</sub>【I+1】]|≤目标。
这个问题可以通过**动态编程**解决。
让 dp[i][j]定义将 A[i]更改为 j 时的最小调整成本，然后 dp 关系由–
定义

```
dp[i][j] = min{dp[i - 1][k]} + |j - A[i]|
           for all k's such that |k - j| ≤ target
```

这里，0 ≤ i ≤ n 和 0 ≤ j ≤ M，其中 n 是数组中的元素个数，M = 100。我们必须考虑所有 k，使得 max(j–target，0) ≤ k ≤ min(M，j + target)
最后，对于所有 0 ≤ j ≤ M，
阵列的最小调整成本将是 min { DP[n–1][j]}。以下是上述想法的实现–

## C++

```
// C++ program to find minimum adjustment cost of an array
#include <bits/stdc++.h>
using namespace std;

#define M 100

// Function to find minimum adjustment cost of an array
int minAdjustmentCost(int A[], int n, int target)
{
    // dp[i][j] stores minimal adjustment cost on changing
    // A[i] to j
    int dp[n][M + 1];

    // handle first element of array separately
    for (int j = 0; j <= M; j++)
        dp[0][j] = abs(j - A[0]);

    // do for rest elements of the array
    for (int i = 1; i < n; i++)
    {
        // replace A[i] to j and calculate minimal adjustment
        // cost dp[i][j]
        for (int j = 0; j <= M; j++)
        {
          // initialize minimal adjustment cost to INT_MAX
          dp[i][j] = INT_MAX;

          // consider all k such that k >= max(j - target, 0) and
          // k <= min(M, j + target) and take minimum
          for (int k = max(j-target,0); k <= min(M,j+target); k++)
             dp[i][j] = min(dp[i][j], dp[i - 1][k] + abs(A[i] - j));
        }
    }   

    // return minimum value from last row of dp table
    int res = INT_MAX;
    for (int j = 0; j <= M; j++)
        res = min(res, dp[n - 1][j]);

    return res;
}

// Driver Program to test above functions
int main()
{
    int arr[] = {55, 77, 52, 61, 39, 6, 25, 60, 49, 47};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target = 10;

    cout << "Minimum adjustment cost is "
         << minAdjustmentCost(arr, n, target) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum adjustment cost of an array
import java.io.*;
import java.util.*;

class GFG
{
    public static int M = 100;

    // Function to find minimum adjustment cost of an array
    static int minAdjustmentCost(int A[], int n, int target)
    {
        // dp[i][j] stores minimal adjustment cost on changing
        // A[i] to j
        int[][] dp = new int[n][M + 1];

        // handle first element of array separately
        for (int j = 0; j <= M; j++)
            dp[0][j] = Math.abs(j - A[0]);

        // do for rest elements of the array
        for (int i = 1; i < n; i++)
        {
            // replace A[i] to j and calculate minimal adjustment
            // cost dp[i][j]
            for (int j = 0; j <= M; j++)
            {
                // initialize minimal adjustment cost to INT_MAX
                dp[i][j] = Integer.MAX_VALUE;

                // consider all k such that k >= max(j - target, 0) and
                // k <= min(M, j + target) and take minimum
                int k = Math.max(j-target,0);
                for ( ; k <= Math.min(M,j+target); k++)
                    dp[i][j] = Math.min(dp[i][j], dp[i - 1][k] + 
                                                Math.abs(A[i] - j));
            }
        }   

        // return minimum value from last row of dp table
        int res = Integer.MAX_VALUE;
        for (int j = 0; j <= M; j++)
            res = Math.min(res, dp[n - 1][j]);

        return res;
    }

    // Driver program
    public static void main (String[] args)
    {
        int arr[] = {55, 77, 52, 61, 39, 6, 25, 60, 49, 47};
        int n = arr.length;
        int target = 10;

        System.out.println("Minimum adjustment cost is "
                    +minAdjustmentCost(arr, n, target));
    }
}

// This code is contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to find minimum
# adjustment cost of an array
M = 100

# Function to find minimum
# adjustment cost of an array
def minAdjustmentCost(A, n, target):

    # dp[i][j] stores minimal adjustment
    # cost on changing A[i] to j
    dp = [[0 for i in range(M + 1)]
             for i in range(n)]

    # handle first element
    # of array separately
    for j in range(M + 1):
        dp[0][j] = abs(j - A[0])

    # do for rest elements
    # of the array
    for i in range(1, n):

        # replace A[i] to j and
        # calculate minimal adjustment
        # cost dp[i][j]
        for j in range(M + 1):

            # initialize minimal adjustment
            # cost to INT_MAX
            dp[i][j] = 100000000

            # consider all k such that
            # k >= max(j - target, 0) and
            # k <= min(M, j + target) and
            # take minimum
            for k in range(max(j - target, 0),
                           min(M, j + target) + 1):
                dp[i][j] = min(dp[i][j], dp[i - 1][k] +
                                        abs(A[i] - j))

    # return minimum value from
    # last row of dp table
    res = 10000000
    for j in range(M + 1):
        res = min(res, dp[n - 1][j])
    return res

# Driver Code
arr= [55, 77, 52, 61, 39,
       6, 25, 60, 49, 47]
n = len(arr)
target = 10
print("Minimum adjustment cost is",
       minAdjustmentCost(arr, n, target),
                              sep = ' ')

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# program to find minimum adjustment
// cost of an array
using System;

class GFG {

    public static int M = 100;

    // Function to find minimum adjustment
    // cost of an array
    static int minAdjustmentCost(int []A, int n,
                                     int target)
    {

        // dp[i][j] stores minimal adjustment
        // cost on changing A[i] to j
        int[,] dp = new int[n,M + 1];

        // handle first element of array
        // separately
        for (int j = 0; j <= M; j++)
            dp[0,j] = Math.Abs(j - A[0]);

        // do for rest elements of the array
        for (int i = 1; i < n; i++)
        {
            // replace A[i] to j and calculate
            // minimal adjustment cost dp[i][j]
            for (int j = 0; j <= M; j++)
            {
                // initialize minimal adjustment
                // cost to INT_MAX
                dp[i,j] = int.MaxValue;

                // consider all k such that
                // k >= max(j - target, 0) and
                // k <= min(M, j + target) and
                // take minimum
                int k = Math.Max(j - target, 0);

                for ( ; k <= Math.Min(M, j +
                                   target); k++)
                    dp[i,j] = Math.Min(dp[i,j],
                                   dp[i - 1,k]
                         + Math.Abs(A[i] - j));
            }
        }

        // return minimum value from last
        // row of dp table
        int res = int.MaxValue;
        for (int j = 0; j <= M; j++)
            res = Math.Min(res, dp[n - 1,j]);

        return res;
    }

    // Driver program
    public static void Main ()
    {
        int []arr = {55, 77, 52, 61, 39,
                        6, 25, 60, 49, 47};
        int n = arr.Length;
        int target = 10;

        Console.WriteLine("Minimum adjustment"
                                 + " cost is "
         + minAdjustmentCost(arr, n, target));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// adjustment cost of an array

$M = 100;

// Function to find minimum
// adjustment cost of an array
function minAdjustmentCost( $A, $n, $target)
{

    // dp[i][j] stores minimal
    // adjustment cost on changing
    // A[i] to j
    global $M;
    $dp = array(array());

    // handle first element
    // of array separately
    for($j = 0; $j <= $M; $j++)
        $dp[0][$j] = abs($j - $A[0]);

    // do for rest
    // elements of the array
    for($i = 1; $i < $n; $i++)
    {

        // replace A[i] to j and
        // calculate minimal adjustment
        // cost dp[i][j]
        for($j = 0; $j <= $M; $j++)
        {

            // initialize minimal adjustment
            // cost to INT_MAX
            $dp[$i][$j] = PHP_INT_MAX;

            // consider all k such that
            // k >= max(j - target, 0) and
            // k <= min(M, j + target) and
            // take minimum
            for($k = max($j - $target, 0);
                $k <= min($M, $j + $target);
                                       $k++)
                $dp[$i][$j] = min($dp[$i][$j],
                              $dp[$i - 1][$k] +
                              abs($A[$i] - $j));
        }
    }

    // return minimum value
    // from last row of dp table
    $res = PHP_INT_MAX;
    for($j = 0; $j <= $M; $j++)
        $res = min($res, $dp[$n - 1][$j]);

    return $res;
}

    // Driver Code
    $arr = array(55, 77, 52, 61, 39,
                 6, 25, 60, 49, 47);
    $n = count($arr);
    $target = 10;

    echo "Minimum adjustment cost is "
        , minAdjustmentCost($arr, $n, $target);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find minimum adjustment cost of an array
    let M = 100;

    // Function to find minimum adjustment cost of an array
    function minAdjustmentCost(A, n, target)
    {

        // dp[i][j] stores minimal adjustment cost on changing
        // A[i] to j
        let dp = new Array(n);
        for (let i = 0; i < n; i++)
        {
            dp[i] = new Array(n);
            for (let j = 0; j <= M; j++)
            {
                dp[i][j] = 0;
            }
        }

        // handle first element of array separately
        for (let j = 0; j <= M; j++)
            dp[0][j] = Math.abs(j - A[0]);

        // do for rest elements of the array
        for (let i = 1; i < n; i++)
        {
            // replace A[i] to j and calculate minimal adjustment
            // cost dp[i][j]
            for (let j = 0; j <= M; j++)
            {
                // initialize minimal adjustment cost to INT_MAX
                dp[i][j] = Number.MAX_VALUE;

                // consider all k such that k >= max(j - target, 0) and
                // k <= min(M, j + target) and take minimum
                let k = Math.max(j-target,0);
                for ( ; k <= Math.min(M,j+target); k++)
                    dp[i][j] = Math.min(dp[i][j], dp[i - 1][k] + 
                                                Math.abs(A[i] - j));
            }
        }   

        // return minimum value from last row of dp table
        let res = Number.MAX_VALUE;
        for (let j = 0; j <= M; j++)
            res = Math.min(res, dp[n - 1][j]);

        return res;
    }

    let arr = [55, 77, 52, 61, 39, 6, 25, 60, 49, 47];
    let n = arr.length;
    let target = 10;

    document.write("Minimum adjustment cost is "
                       +minAdjustmentCost(arr, n, target));

  // This code is contributed by decode2207.
</script>
```

输出:

```
Minimum adjustment cost is 75
```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。