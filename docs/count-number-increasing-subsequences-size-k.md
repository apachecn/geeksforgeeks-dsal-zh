# 计算大小为 k 的递增子序列的数量

> 原文:[https://www . geesforgeks . org/count-number-递增-subseries-size-k/](https://www.geeksforgeeks.org/count-number-increasing-subsequences-size-k/)

给定一个包含 **n** 个整数的数组 **arr[]** 。问题是计算大小为 **k** 的数组中递增子序列的数量。

**示例:**

```
Input : arr[] = {2, 6, 4, 5, 7}, 
            k = 3
Output : 5
The subsequences of size '3' are:
{2, 6, 7}, {2, 4, 5}, {2, 4, 7},
{2, 5, 7} and {4, 5, 7}.

Input : arr[] = {12, 8, 11, 13, 10, 15, 14, 16, 20}, 
            k = 4
Output : 39
```

**方法:**想法是通过定义 2D 矩阵来使用动态规划，比如 dp[][]。 **dp[i][j]** 存储以元素 **arr[j]** 结束的大小为 **i** 的递增子序列的计数。因此 dp[i][j]可以定义为:

> dp[i][j] = 1，其中 i = 1 和 1 <= j <= n 
> dp[i][j] =和(dp[i-1][j])，其中 1 < i < = k，i < = j < = n 和 arr[m] < arr[j]为(i-1) < = m < j。

下面是上述方法的实现:

## C++

```
// C++ implementation to count number of
// increasing subsequences of size k
#include <bits/stdc++.h>

using namespace std;

// function to count number of increasing
// subsequences of size k
int numOfIncSubseqOfSizeK(int arr[], int n, int k)
{
    int dp[k][n], sum = 0;
    memset(dp, 0, sizeof(dp));

    // count of increasing subsequences of size 1
    // ending at each arr[i]
    for (int i = 0; i < n; i++)
        dp[0][i] = 1;

    // building up the matrix dp[][]
    // Here 'l' signifies the size of
    // increasing subsequence of size (l+1).
    for (int l = 1; l < k; l++) {

        // for each increasing subsequence of size 'l'
        // ending with element arr[i]
        for (int i = l; i < n; i++) {

            // count of increasing subsequences of size 'l'
            // ending with element arr[i]
            dp[l][i] = 0;
            for (int j = l - 1; j < i; j++) {
                if (arr[j] < arr[i])
                    dp[l][i] += dp[l - 1][j];
            }
        }
    }

    // sum up the count of increasing subsequences of
    // size 'k' ending at each element arr[i]
    for (int i = k - 1; i < n; i++)
        sum += dp[k - 1][i];

    // required number of increasing
    // subsequences of size k
    return sum;
}

// Driver program to test above
int main()
{
    int arr[] = { 12, 8, 11, 13, 10, 15, 14, 16, 20 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 4;

    cout << "Number of Increasing Subsequences of size "
         << k << " = " << numOfIncSubseqOfSizeK(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation to count number of
// increasing subsequences of size k

class GFG {

// function to count number of increasing
// subsequences of size k
    static int numOfIncSubseqOfSizeK(int arr[], int n, int k) {
        int dp[][] = new int[k][n], sum = 0;

        // count of increasing subsequences of size 1
        // ending at each arr[i]
        for (int i = 0; i < n; i++) {
            dp[0][i] = 1;
        }

        // building up the matrix dp[][]
        // Here 'l' signifies the size of
        // increasing subsequence of size (l+1).
        for (int l = 1; l < k; l++) {

            // for each increasing subsequence of size 'l'
            // ending with element arr[i]
            for (int i = l; i < n; i++) {

                // count of increasing subsequences of size 'l'
                // ending with element arr[i]
                dp[l][i] = 0;
                for (int j = l - 1; j < i; j++) {
                    if (arr[j] < arr[i]) {
                        dp[l][i] += dp[l - 1][j];
                    }
                }
            }
        }

        // sum up the count of increasing subsequences of
        // size 'k' ending at each element arr[i]
        for (int i = k - 1; i < n; i++) {
            sum += dp[k - 1][i];
        }

        // required number of increasing
        // subsequences of size k
        return sum;
    }

// Driver program to test above
    public static void main(String[] args) {
        int arr[] = {12, 8, 11, 13, 10, 15, 14, 16, 20};
        int n = arr.length;
        int k = 4;

        System.out.print("Number of Increasing Subsequences of size "
                + k + " = " + numOfIncSubseqOfSizeK(arr, n, k));

    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to count number
# of increasing subsequences of size k
import math as mt

# function to count number of increasing
# subsequences of size k
def numOfIncSubseqOfSizeK(arr, n, k):

    dp = [[0 for i in range(n)]
             for i in range(k)]

    # count of increasing subsequences
    # of size 1 ending at each arr[i]
    for i in range(n):
        dp[0][i] = 1

    # building up the matrix dp[][]
    # Here 'l' signifies the size of
    # increasing subsequence of size (l+1).
    for l in range(1, k):

        # for each increasing subsequence of
        # size 'l' ending with element arr[i]
        for i in range(l, n):

            # count of increasing subsequences of
            # size 'l' ending with element arr[i]
            dp[l][i] = 0
            for j in range(l - 1, i):
                if (arr[j] < arr[i]):
                    dp[l][i] += dp[l - 1][j]

    # Sum up the count of increasing subsequences
    # of size 'k' ending at each element arr[i]
    Sum = 0
    for i in range(k - 1, n):
        Sum += dp[k - 1][i]

    # required number of increasing
    # subsequences of size k
    return Sum

# Driver Code
arr = [12, 8, 11, 13, 10,
          15, 14, 16, 20 ]
n = len(arr)
k = 4

print("Number of Increasing Subsequences of size",
         k, "=", numOfIncSubseqOfSizeK(arr, n, k))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation to count number of
// increasing subsequences of size k

using System;

public class GFG {

// function to count number of increasing
// subsequences of size k
    static int numOfIncSubseqOfSizeK(int []arr, int n, int k) {
        int [,]dp = new int[k,n]; int sum = 0;

        // count of increasing subsequences of size 1
        // ending at each arr[i]
        for (int i = 0; i < n; i++) {
            dp[0,i] = 1;
        }

        // building up the matrix dp[,]
        // Here 'l' signifies the size of
        // increasing subsequence of size (l+1).
        for (int l = 1; l < k; l++) {

            // for each increasing subsequence of size 'l'
            // ending with element arr[i]
            for (int i = l; i < n; i++) {

                // count of increasing subsequences of size 'l'
                // ending with element arr[i]
                dp[l,i] = 0;
                for (int j = l - 1; j < i; j++) {
                    if (arr[j] < arr[i]) {
                        dp[l,i] += dp[l - 1,j];
                    }
                }
            }
        }

        // sum up the count of increasing subsequences of
        // size 'k' ending at each element arr[i]
        for (int i = k - 1; i < n; i++) {
            sum += dp[k - 1,i];
        }

        // required number of increasing
        // subsequences of size k
        return sum;
    }

// Driver program to test above
    public static void Main() {
        int []arr = {12, 8, 11, 13, 10, 15, 14, 16, 20};
        int n = arr.Length;
        int k = 4;

        Console.Write("Number of Increasing Subsequences of size "
                + k + " = " + numOfIncSubseqOfSizeK(arr, n, k));

    }
}
// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to count
// number of increasing
// subsequences of size k

// function to count number
// of increasing subsequences
// of size k
function numOfIncSubseqOfSizeK($arr,
                               $n, $k)
{
    $dp = array(array());
    $sum = 0;
    $dp = array_fill(0, $n + 1, false);

    // count of increasing
    // subsequences of size 1
    // ending at each arr[i]
    for ($i = 0; $i < $n; $i++)
        $dp[0][$i] = 1;

    // building up the matrix
    // dp[][]. Here 'l' signifies
    // the size of increasing
    // subsequence of size (l+1).
    for ($l = 1; $l < $k; $l++)
    {

        // for each increasing
        // subsequence of size 'l'
        // ending with element arr[i]
        for ($i = $l; $i < $n; $i++)
        {

            // count of increasing
            // subsequences of size 'l'
            // ending with element arr[i]
            $dp[$l][$i] = 0;
            for ($j = $l - 1; $j < $i; $j++)
            {
                if ($arr[$j] < $arr[$i])
                    $dp[$l][$i] += $dp[$l - 1][$j];
            }
        }
    }

    // sum up the count of increasing
    // subsequences of size 'k' ending
    // at each element arr[i]
    for ($i = $k - 1; $i < $n; $i++)
        $sum += $dp[$k - 1][$i];

    // required number of increasing
    // subsequences of size k
    return $sum;
}

// Driver Code
$arr = array(12, 8, 11, 13,
             10, 15, 14, 16, 20);
$n = sizeof($arr);
$k = 4;

echo "Number of Increasing ".
     "Subsequences of size ",
                 $k , " = " ,
     numOfIncSubseqOfSizeK($arr,
                           $n, $k);

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>

// JavaScript implementation to count number of
// increasing subsequences of size k

// function to count number of increasing
// subsequences of size k
    function numOfIncSubseqOfSizeK(arr, n, k)
    {
        let dp = new Array(k), sum = 0;

        // Loop to create 2D array using 1D array
        for (let i = 0; i < dp.length; i++) {
            dp[i] = new Array(2);
        }

        // count of increasing subsequences of size 1
        // ending at each arr[i]
        for (let i = 0; i < n; i++) {
            dp[0][i] = 1;
        }

        // building up the matrix dp[][]
        // Here 'l' signifies the size of
        // increasing subsequence of size (l+1).
        for (let l = 1; l < k; l++) {

            // for each increasing subsequence of size 'l'
            // ending with element arr[i]
            for (let i = l; i < n; i++) {

                // count of increasing subsequences of size 'l'
                // ending with element arr[i]
                dp[l][i] = 0;
                for (let j = l - 1; j < i; j++) {
                    if (arr[j] < arr[i]) {
                        dp[l][i] += dp[l - 1][j];
                    }
                }
            }
        }

        // sum up the count of increasing subsequences of
        // size 'k' ending at each element arr[i]
        for (let i = k - 1; i < n; i++) {
            sum += dp[k - 1][i];
        }

        // required number of increasing
        // subsequences of size k
        return sum;
    }

// Driver code   

        let arr = [12, 8, 11, 13, 10, 15, 14, 16, 20];
        let n = arr.length;
        let k = 4;

        document.write("Number of Increasing Subsequences of size "
                + k + " = " + numOfIncSubseqOfSizeK(arr, n, k));

</script>
```

**输出:**

```
Number of Increasing Subsequences of size 4 = 39
```

**时间复杂度:** O(kn <sup>2</sup> )。
**辅助空间:** O(kn)。