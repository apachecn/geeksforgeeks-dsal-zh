# 用 M 种颜色填充 N 个位置的方法，这样就正好有 K 对相邻的不同颜色

> 原文:[https://www . geeksforgeeks . org/填充 n 个位置的方法-使用-m-colors-这样-有-正好-k 对相邻的不同颜色/](https://www.geeksforgeeks.org/ways-to-fill-n-positions-using-m-colors-such-that-there-are-exactly-k-pairs-of-adjacent-different-colors/)

给定三个整数 **N** 、 **M** 和 **K** 。任务是找到使用 **M** 颜色填充 **N** 位置的方法数量，这样就正好有 **K** 对不同的相邻颜色。

**示例:**

> **输入:** N = 3，M = 2，K = 1
> **输出:** 4
> 让颜色为 1 和 2，那么方式为:
> 1，1，2
> 1，2，2
> 2，2，1
> 2，1，1
> 以上 4 种方式正好有一对相邻元素颜色不同。
> 
> **输入:** N = 3，M = 3，K = 2
> T3】输出: 12

**方法:**我们可以用[带记忆的动态规划](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)来解决上述问题。有 **N** 个位置要填充，因此递归函数将由两个调用组成，一个是如果下一个位置填充了相同的颜色，另一个是如果填充了不同的颜色。因此，递归调用将是:

*   **count way(index+1，cnt)** ，如果下一个索引填充了相同的颜色。
*   **(m–1)* count way(index+1，cnt + 1)** ，如果下一个索引填充了不同的颜色。路数乘以**(m–1)**。

基本情况是:

*   如果**索引= n** ，则检查 **cnt** 的值。如果 **cnt = K** 则是一种可能的方式，因此返回 **1** ，否则返回 **0** 。
*   为了避免重复调用，请记住二维数组中的返回值，并在再次使用相同参数进行递归调用时返回该值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define max 4

// Recursive function to find the required number of ways
int countWays(int index, int cnt, int dp[][max], int n, int m, int k)
{

    // When all positions are filled
    if (index == n) {

        // If adjacent pairs are exactly K
        if (cnt == k)
            return 1;
        else
            return 0;
    }

    // If already calculated
    if (dp[index][cnt] != -1)
        return dp[index][cnt];

    int ans = 0;

    // Next position filled with same color
    ans += countWays(index + 1, cnt, dp, n, m, k);

    // Next position filled with different color
    // So there can be m-1 different colors
    ans += (m - 1) * countWays(index + 1, cnt + 1, dp, n, m, k);

    return dp[index][cnt] = ans;
}

// Driver Code
int main()
{
    int n = 3, m = 3, k = 2;
    int dp[n + 1][max];
    memset(dp, -1, sizeof dp);

    cout << m * countWays(1, 0, dp, n, m, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach
class solution
{
static final int  max=4;

// Recursive function to find the required number of ways
static int countWays(int index, int cnt, int dp[][], int n, int m, int k)
{

    // When all positions are filled
    if (index == n) {

        // If adjacent pairs are exactly K
        if (cnt == k)
            return 1;
        else
            return 0;
    }

    // If already calculated
    if (dp[index][cnt] != -1)
        return dp[index][cnt];

    int ans = 0;

    // Next position filled with same color
    ans += countWays(index + 1, cnt, dp, n, m, k);

    // Next position filled with different color
    // So there can be m-1 different colors
    ans += (m - 1) * countWays(index + 1, cnt + 1, dp, n, m, k);

    return dp[index][cnt] = ans;
}

// Driver Code
public static void main(String args[])
{
    int n = 3, m = 3, k = 2;
    int dp[][]= new int [n + 1][max];
    for(int i=0;i<n+1;i++)
    for(int j=0;j<max;j++)
    dp[i][j]=-1;

    System.out.println(m * countWays(1, 0, dp, n, m, k));
}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

max = 4

# Recursive function to find the
# required number of ways
def countWays(index, cnt, dp, n, m, k):

    # When all positions are filled
    if (index == n) :

        # If adjacent pairs are exactly K
        if (cnt == k):
            return 1
        else:
            return 0

    # If already calculated
    if (dp[index][cnt] != -1):
        return dp[index][cnt]

    ans = 0

    # Next position filled with same color
    ans += countWays(index + 1, cnt, dp, n, m, k)

    # Next position filled with different color
    # So there can be m-1 different colors
    ans += (m - 1) * countWays(index + 1,
                               cnt + 1, dp, n, m, k)

    dp[index][cnt] = ans
    return dp[index][cnt]

# Driver Code
if __name__ == "__main__":

    n = 3
    m = 3
    k = 2
    dp = [[-1 for x in range(n + 1)]
              for y in range(max)]

    print(m * countWays(1, 0, dp, n, m, k))

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach

using System;

class solution
{
static int max=4;

// Recursive function to find the required number of ways
static int countWays(int index, int cnt, int [,]dp, int n, int m, int k)
{

    // When all positions are filled
    if (index == n) {

        // If adjacent pairs are exactly K
        if (cnt == k)
            return 1;
        else
            return 0;
    }

    // If already calculated
    if (dp[index,cnt] != -1)
        return dp[index,cnt];

    int ans = 0;

    // Next position filled with same color
    ans += countWays(index + 1, cnt, dp, n, m, k);

    // Next position filled with different color
    // So there can be m-1 different colors
    ans += (m - 1) * countWays(index + 1, cnt + 1, dp, n, m, k);

    return dp[index,cnt] = ans;
}

// Driver Code
public static void Main()
{
    int n = 3, m = 3, k = 2;
    int [,]dp= new int [n + 1,max];
    for(int i=0;i<n+1;i++)
        for(int j=0;j<max;j++)
            dp[i,j]=-1;

    Console.WriteLine(m * countWays(1, 0, dp, n, m, k));
}
// This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

$GLOBALS['max'] = 4;

// Recursive function to find the
// required number of ways
function countWays($index, $cnt, $dp,
                         $n, $m, $k)
{

    // When all positions are filled
    if ($index == $n)
    {

        // If adjacent pairs are exactly K
        if ($cnt == $k)
            return 1;
        else
            return 0;
    }

    // If already calculated
    if ($dp[$index][$cnt] != -1)
        return $dp[$index][$cnt];

    $ans = 0;

    // Next position filled with same color
    $ans += countWays($index + 1, $cnt,
                      $dp, $n, $m, $k);

    // Next position filled with different color
    // So there can be m-1 different colors
    $ans += ($m - 1) * countWays($index + 1, $cnt + 1,
                                 $dp, $n, $m, $k);

    $dp[$index][$cnt] = $ans;

    return $dp[$index][$cnt];
}

// Driver Code
$n = 3;
$m = 3;
$k = 2;
$dp = array(array());

for($i = 0; $i < $n + 1; $i++)
    for($j = 0; $j < $GLOBALS['max']; $j++)
        $dp[$i][$j] = -1;

echo $m * countWays(1, 0, $dp, $n, $m, $k);

// This code is contributed by aishwarya.27
?>
```

## java 描述语言

```
<script>
//Javascript implementation of the approach

let max=4;

// Recursive function to find the required number of ways
function countWays(index,cnt,dp,n,m,k)
{
    // When all positions are filled
    if (index == n) {

        // If adjacent pairs are exactly K
        if (cnt == k)
            return 1;
        else
            return 0;
    }

    // If already calculated
    if (dp[index][cnt] != -1)
        return dp[index][cnt];

    let ans = 0;

    // Next position filled with same color
    ans += countWays(index + 1, cnt, dp, n, m, k);

    // Next position filled with different color
    // So there can be m-1 different colors
    ans += (m - 1) * countWays(index + 1, cnt + 1, dp, n, m, k);

    return dp[index][cnt] = ans;
}

// Driver Code
let n = 3, m = 3, k = 2;
let dp=new Array(n+1);
for(let i=0;i<n+1;i++)
{   
    dp[i]=new Array(max);
    for(let j=0;j<max;j++)
        dp[i][j]=-1;
}   
document.write(m * countWays(1, 0, dp, n, m, k));   

// This code is contributed by rag2127
</script>
```

**Output:** 

```
12
```