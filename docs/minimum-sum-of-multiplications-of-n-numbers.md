# n 个数相乘的最小和

> 原文:[https://www . geesforgeks . org/n-numbers 的最小乘法和/](https://www.geeksforgeeks.org/minimum-sum-of-multiplications-of-n-numbers/)

给定 n 个整数。任务是通过一次取两个相邻的数，并把它们的总和 100%放回，直到剩下一个数，来最小化所有数的乘积之和。

**示例:**

```
Input : 40 60 20 
Output : 2400  
Explanation: There are two possible cases:
1st possibility: Take 40 and 60, so multiplication=2400
and put back (60+40) % 100 = 0, making it 0, 20.
Multiplying 0 and 20 we get 0 so 
multiplication = 2400+0 = 2400\. Put back (0+20)%100 = 20\. 
2nd possibility: take 60 and 20, so 60*20 = 1200,
put back (60+20)%100 = 80, making it [40, 80] 
multiply 40*80 to get 3200, so multiplication
sum = 1200+3200 = 4400\. Put back (40+80)%100 = 20 

Input : 5 6 
Output : 30 
Explanation: Only possibility is 5*6=30 
```

**方法:**问题是[矩阵链乘法动态规划](https://www.geeksforgeeks.org/dynamic-programming-set-8-matrix-chain-multiplication/)
的变种，思路是把 N 个数分割成 k 的每一个可能值，对较小的部分进行递归求解，将乘法相加，存储其中的最小值。因为我们将它分成 k 个部分，所以对于每个 DP <sub>i，j</sub> 我们将有 k 个分区 i < =k < j，存储它们的最小值。于是我们得到了类似[矩阵链乘法动态规划](https://www.geeksforgeeks.org/dynamic-programming-set-8-matrix-chain-multiplication/)的公式。

> DP <sub>i，j</sub> = min(DP <sub>i，j</sub> ，(DP <sub>i，k</sub> +DP <sub>k+1，j</sub> +(累计 _sum <sub>i，k</sub>*累计 _sum <sub>k+1，j</sub>))
> 每 i < =k < j。

由于许多子问题会重复出现，因此我们使用记忆化将这些值存储在 nXn 矩阵中。

下面给出了上述方法的说明:

## C++

```
// CPP program to find the
// minimum sum of multiplication
// of n numbers
#include <bits/stdc++.h>
using namespace std;

// Used in recursive
// memoized solution
long long dp[1000][1000];

// function to calculate the cumulative
// sum from a[i] to a[j]
long long sum(int a[], int i, int j)
{    
    long long ans = 0;
    for (int m = i; m <= j; m++)    
        ans = (ans + a[m]) % 100;
    return ans;
}

long long solve(int a[], int i, int j)
{
    // base case
    if (i == j)
        return 0;

    // memoization, if the partition
    // has been called before then
    // return the stored value
    if (dp[i][j] != -1)
        return dp[i][j];

    // store a max value
    dp[i][j] = INT_MAX;

    // we break them into k partitions
    for (int k = i; k < j; k++)
    {
        // store the min of the
        // formula thus obtained
        dp[i][j] = min(dp[i][j], (solve(a, i, k) +
                              solve(a, k + 1, j) +
              (sum(a, i, k) * sum(a, k + 1, j))));
    }

    // return the minimum
    return dp[i][j];
}

void initialize(int n)
{
    for (int i = 0; i <= n; i++)
        for (int j = 0; j <= n; j++)
            dp[i][j] = -1;    
}

// Driver code
int main() {
    int a[] = {40, 60, 20};
    int n = sizeof(a) / sizeof(a[0]);
    initialize(n);
    cout << solve(a, 0, n - 1) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the 
// minimum sum of multiplication
// of n numbers
import java.io.*;
import java.math.*;

class GFG
{

    // Used in recursive
    // memoized solution
    static long dp[][] = new long[1000][1000];

    // function to calculate the
    // cumulative  sum from a[i] to a[j]
    static long sum(int a[], int i, int j)
    {    
        long ans = 0;
        for (int m = i; m <= j; m++)    
            ans = (ans + a[m]) % 100;
        return ans;
    }

    static long solve(int a[], int i, int j)
    {
        // base case
        if (i == j)
            return 0;

        // memoization, if the partition
        // has been called before then
        // return the stored value
        if (dp[i][j] != -1)
            return dp[i][j];

        // store a max value
        dp[i][j] = 100000000;

        // we break them into k partitions
        for (int k = i; k < j; k++)
        {
            // store the min of the
            // formula thus obtained
            dp[i][j] = Math.min(dp[i][j], (solve(a, i, k) +
                                       solve(a, k + 1, j) +
                        (sum(a, i, k) * sum(a, k + 1,j))));
        }

        // return the minimum
        return dp[i][j];
    }

    static void initialize(int n)
    {
        for (int i = 0; i <= n; i++)
            for (int j = 0; j <= n; j++)
                dp[i][j] = -1;    
    }

    // Driver code
    public static void main(String args[])
    {
        int a[] = {40, 60, 20};
        int n = a.length;
        initialize(n);
        System.out.println(solve(a, 0, n - 1));

    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 program to find the
# minimum sum of multiplication
# of n numbers

import numpy as np
import sys

# Used in recursive
# memoized solution
dp = np.zeros((1000,1000))

# function to calculate the cumulative
# sum from a[i] to a[j]
def sum(a, i, j) :

    ans = 0
    for m in range(i, j + 1) :
        ans = (ans + a[m]) % 100

    return ans

def solve(a, i, j) :

    # base case
    if (i == j) :
        return 0

    # memoization, if the partition
    # has been called before then
    # return the stored value
    if (dp[i][j] != -1) :

        return dp[i][j]

    # store a max value
    dp[i][j] = sys.maxsize

    # we break them into k partitions
    for k in range(i, j) :

        # store the min of the
        # formula thus obtained
        dp[i][j] = min(dp[i][j], (solve(a, i, k) + solve(a, k + 1, j)
                                + (sum(a, i, k) * sum(a, k + 1, j))))

    # return the minimum
    return dp[i][j]

def initialize(n) :

    for i in range(n + 1) :
        for j in range(n + 1) :
            dp[i][j] = -1   

#Driver code
if __name__ == "__main__" :

    a = [40, 60, 20]
    n = len(a)
    initialize(n)
    print(int(solve(a, 0, n - 1)))

# This code is contributed by Ryuga
```

## C#

```
// C# program to find the
// minimum sum of multiplication
// of n numbers
using System;

class GFG
{

    // Used in recursive
    // memoized solution
    static long [,]dp = new long[1000, 1000];

    // Function to calculate the cumulative
    // sum from a[i] to a[j]
    static long sum(int []a, int i, int j)
    {
        long ans = 0;
        for (int m = i; m <= j; m++)
            ans = (ans + a[m]) % 100;
        return ans;
    }

    static long solve(int []a, int i, int j)
    {
        // base case
        if (i == j)
            return 0;

        // memoization, if the partition
        // has been called before then
        // return the stored value
        if (dp[i, j] != -1)
            return dp[i, j];

        // store a max value
        dp[i, j] = 100000000;

        // we break them into k partitions
        for (int k = i; k < j; k++)
        {
            // store the min of the
            // formula thus obtained
            dp[i, j] = Math.Min(dp[i, j], (solve(a, i, k) +
                                       solve(a, k + 1, j) +
                       (sum(a, i, k) * sum(a, k + 1, j))));
        }

        // return the minimum
        return dp[i, j];
    }

    static void initialize(int n)
    {
        for (int i = 0; i <= n; i++)
            for (int j = 0; j <= n; j++)
                dp[i, j] = -1;
    }

    // Driver code
    public static void Main()
    {
        int []a = {40, 60, 20};
        int n = a.Length;
        initialize(n);
        Console.WriteLine(solve(a, 0, n - 1));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// minimum sum of multiplication
// of n numbers

// Used in recursive
// memoized solution
$dp = array(array());

// function to calculate the
// cumulative sum from a[i] to a[j]
function sum( $a, $i, $j)
{
    $ans = 0;
    for ( $m = $i; $m <= $j; $m++)
        $ans = ($ans + $a[$m]) % 100;
    return $ans;
}

function solve( $a, $i, $j)
{
    global $dp;
    // base case
    if ($i == $j)
        return 0;

    // memoization, if the partition
    // has been  called before then
    // return the stored value
    if ($dp[$i][$j] != -1)
        return $dp[$i][$j];

    // store a max value
    $dp[$i][$j] = PHP_INT_MAX;

    // we break them into
    // k partitions
    for ( $k = $i; $k < $j; $k++)
    {
        // store the min of the
        // formula thus obtained
        $dp[$i][$j] = min($dp[$i][$j],
                      (solve($a, $i, $k) +
                       solve($a, $k + 1, $j) +
                      (sum($a, $i, $k) *
                       sum($a, $k + 1, $j))));
    }

    // return the minimum
    return $dp[$i][$j];
}

function initialize( $n)
{
    global $dp;
    for ( $i = 0; $i <= $n; $i++)
        for ( $j = 0; $j <= $n; $j++)
            $dp[$i][$j] = -1;
}

// Driver code
$a = array(40, 60, 20);
$n = count($a);
initialize($n);
echo solve($a, 0, $n - 1) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the
// minimum sum of multiplication
// of n numbers

// Used in recursive
// memoized solution
var dp = Array.from(Array(1000), ()=>Array(1000));

// function to calculate the cumulative
// sum from a[i] to a[j]
function sum( a,  i,  j)
{    
    var ans = 0;
    for (var m = i; m <= j; m++)    
        ans = (ans + a[m]) % 100;
    return ans;
}

function solve( a,  i,  j)
{
    // base case
    if (i == j)
        return 0;

    // memoization, if the partition
    // has been called before then
    // return the stored value
    if (dp[i][j] != -1)
        return dp[i][j];

    // store a max value
    dp[i][j] = 1000000000;

    // we break them into k partitions
    for (var k = i; k < j; k++)
    {
        // store the min of the
        // formula thus obtained
        dp[i][j] = Math.min(dp[i][j], (solve(a, i, k) +
                              solve(a, k + 1, j) +
              (sum(a, i, k) * sum(a, k + 1, j))));
    }

    // return the minimum
    return dp[i][j];
}

function initialize(n)
{
    for (var i = 0; i <= n; i++)
        for (var j = 0; j <= n; j++)
            dp[i][j] = -1;    
}

// Driver code
var a = [40, 60, 20];
var n = a.length;
initialize(n);
document.write( solve(a, 0, n - 1));

</script>
```

**输出:**

```
2400
```

**时间复杂度:**o(n^3)
T3】辅助空间: O(n^2)