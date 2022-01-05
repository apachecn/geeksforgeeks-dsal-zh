# 形成具有给定范围内整数的数组的方法，以便总和可被 2 整除

> 原文:[https://www . geesforgeks . org/形成给定范围内具有整数的数组的方法，以便总和可被 2 整除/](https://www.geeksforgeeks.org/ways-to-form-an-array-having-integers-in-given-range-such-that-total-sum-is-divisible-by-2/)

给定三个正整数 **N** 、 **L** 和 **R** 。任务是找到形成大小为 **N** 的数组的方法的数量，其中每个元素位于范围**【L，R】**中，使得数组中所有元素的总和可被 **2** 整除。
**示例:**

> **输入:** N = 2，L = 1，R = 3
> **输出:** 5
> 所有元素之和可被 2 整除的可能数组有
> 【1，1】【2，2】【1，3】【3，1】和【3，3】
> **输入:** N = 3，L = 2，R = 2
> **输出:** 1

**方法:**想法是找出余数为 0 和 1 模 2 分别位于 L 和 r 之间的数字的计数。这个计数可以如下计算:

> 我们需要计算余数为 1 的范围之间的数模 2
> **F** =所需类型范围内的第一个数
> **L** =所需类型范围内的最后一个数
> **Count =(L–F)/2**
> CNT 0，cnt1 表示每种类型范围之间的数的计数。

然后，使用动态规划我们可以解决这个问题。设 **dp[i][j]** 表示取模 2 的前 I 个数之和等于 j 的路数，假设我们需要计算 dp[i][0]，那么它会有如下递推关系:**DP[I][0]=(CNT 0 * DP[I–1][0]+CNT 1 * DP[I–1][1])**。第一项表示直到(I–1)的和余数为 0 的路数，因此我们可以将 cnt0 数放在 i <sup>第</sup>个位置，这样和余数仍然保持为 0。第二项表示直到(I–1)的路的数量，其和余数为 1，因此我们可以将 cnt1 的数字放在 i <sup>第</sup>个位置，使得和余数变为 0。同样，我们可以计算 dp[i][1]。
最终答案用 **dp[N][0]** 表示。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of ways to
// form an array of size n such that sum of
// all elements is divisible by 2
int countWays(int n, int l, int r)
{
    int tL = l, tR = r;

    // Represents first and last numbers
    // of each type (modulo 0 and 1)
    int L[2] = { 0 }, R[2] = { 0 };
    L[l % 2] = l, R[r % 2] = r;

    l++, r--;

    if (l <= tR && r >= tL)
        L[l % 2] = l, R[r % 2] = r;

    // Count of numbers of each type between range
    int cnt0 = 0, cnt1 = 0;
    if (R[0] && L[0])
        cnt0 = (R[0] - L[0]) / 2 + 1;
    if (R[1] && L[1])
        cnt1 = (R[1] - L[1]) / 2 + 1;

    int dp[n][2];

    // Base Cases
    dp[1][0] = cnt0;
    dp[1][1] = cnt1;
    for (int i = 2; i <= n; i++) {

        // Ways to form array whose sum upto
        // i numbers modulo 2 is 0
        dp[i][0] = (cnt0 * dp[i - 1][0]
                    + cnt1 * dp[i - 1][1]);

        // Ways to form array whose sum upto
        // i numbers modulo 2 is 1
        dp[i][1] = (cnt0 * dp[i - 1][1]
                    + cnt1 * dp[i - 1][0]);
    }

    // Return the required count of ways
    return dp[n][0];
}

// Driver Code
int main()
{
    int n = 2, l = 1, r = 3;
    cout << countWays(n, l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the number of ways to
// form an array of size n such that sum of
// all elements is divisible by 2
static int countWays(int n, int l, int r)
{
    int tL = l, tR = r;

    // Represents first and last numbers
    // of each type (modulo 0 and 1)
    int[] L = new int[3];
    int[] R = new int[3];
    L[l % 2] = l;
    R[r % 2] = r;

    l++;
    r--;

    if (l <= tR && r >= tL)
    {
        L[l % 2] = l;
        R[r % 2] = r;
    }

    // Count of numbers of each type between range
    int cnt0 = 0, cnt1 = 0;
    if (R[0] > 0 && L[0] > 0)
        cnt0 = (R[0] - L[0]) / 2 + 1;
    if (R[1] > 0 && L[1] > 0)
        cnt1 = (R[1] - L[1]) / 2 + 1;

    int[][] dp = new int[n + 1][3];

    // Base Cases
    dp[1][0] = cnt0;
    dp[1][1] = cnt1;
    for (int i = 2; i <= n; i++)
    {

        // Ways to form array whose sum upto
        // i numbers modulo 2 is 0
        dp[i][0] = (cnt0 * dp[i - 1] [0]
                    + cnt1 * dp[i - 1][1]);

        // Ways to form array whose sum upto
        // i numbers modulo 2 is 1
        dp[i][1] = (cnt0 * dp[i - 1][1]
                    + cnt1 * dp[i - 1][0]);
    }

    // Return the required count of ways
    return dp[n][0];
}

// Driver Code
public static void main(String[] args)
{
    int n = 2, l = 1, r = 3;
    System.out.println(countWays(n, l, r));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number of ways to
# form an array of size n such that sum of
# all elements is divisible by 2
def countWays(n, l, r):

    tL, tR = l, r

    # Represents first and last numbers
    # of each type (modulo 0 and 1)
    L = [0 for i in range(2)]
    R = [0 for i in range(2)]

    L[l % 2] = l
    R[r % 2] = r

    l += 1
    r -= 1

    if (l <= tR and r >= tL):
        L[l % 2], R[r % 2] = l, r

    # Count of numbers of each type
    # between range
    cnt0, cnt1 = 0, 0
    if (R[0] and L[0]):
        cnt0 = (R[0] - L[0]) // 2 + 1
    if (R[1] and L[1]):
        cnt1 = (R[1] - L[1]) // 2 + 1

    dp = [[0 for i in range(2)]
             for i in range(n + 1)]

    # Base Cases
    dp[1][0] = cnt0
    dp[1][1] = cnt1
    for i in range(2, n + 1):

        # Ways to form array whose sum
        # upto i numbers modulo 2 is 0
        dp[i][0] = (cnt0 * dp[i - 1][0] +
                    cnt1 * dp[i - 1][1])

        # Ways to form array whose sum upto
        # i numbers modulo 2 is 1
        dp[i][1] = (cnt0 * dp[i - 1][1] +
                    cnt1 * dp[i - 1][0])

    # Return the required count of ways
    return dp[n][0]

# Driver Code
n, l, r = 2, 1, 3
print(countWays(n, l, r))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach

using System;

class GFG
{

// Function to return the number of ways to
// form an array of size n such that sum of
// all elements is divisible by 2
static int countWays(int n, int l, int r)
{
    int tL = l, tR = r;

    // Represents first and last numbers
    // of each type (modulo 0 and 1)
    int[] L = new int[3];
    int[] R = new int[3];
    L[l % 2] = l;
    R[r % 2] = r;

    l++;
    r--;

    if (l <= tR && r >= tL)
    {
        L[l % 2] = l;
        R[r % 2] = r;
    }

    // Count of numbers of each type between range
    int cnt0 = 0, cnt1 = 0;
    if (R[0] > 0 && L[0] > 0)
        cnt0 = (R[0] - L[0]) / 2 + 1;
    if (R[1] > 0 && L[1] > 0)
        cnt1 = (R[1] - L[1]) / 2 + 1;

    int[,] dp=new int[n + 1, 3];

    // Base Cases
    dp[1, 0] = cnt0;
    dp[1, 1] = cnt1;
    for (int i = 2; i <= n; i++)
    {

        // Ways to form array whose sum upto
        // i numbers modulo 2 is 0
        dp[i, 0] = (cnt0 * dp[i - 1, 0]
                    + cnt1 * dp[i - 1, 1]);

        // Ways to form array whose sum upto
        // i numbers modulo 2 is 1
        dp[i, 1] = (cnt0 * dp[i - 1, 1]
                    + cnt1 * dp[i - 1, 0]);
    }

    // Return the required count of ways
    return dp[n, 0];
}

// Driver Code
static void Main()
{
    int n = 2, l = 1, r = 3;
    Console.WriteLine(countWays(n, l, r));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number of ways to
// form an array of size n such that sum of
// all elements is divisible by 2
function countWays($n, $l, $r)
{
    $tL = $l;
    $tR = $r;

    $L = array_fill(0, 2, 0);
    $R = array_fill(0, 2, 0);

    // Represents first and last numbers
    // of each type (modulo 0 and 1)
    $L[$l % 2] = $l;
    $R[$r % 2] = $r;

    $l++;
    $r--;

    if ($l <= $tR && $r >= $tL)
    {
        $L[$l % 2] = $l;
        $R[$r % 2] = $r;
    }

    // Count of numbers of each type
    // between range
    $cnt0 = 0;
    $cnt1 = 0;
    if ($R[0] && $L[0])
        $cnt0 = ($R[0] - $L[0]) / 2 + 1;

    if ($R[1] && $L[1])
        $cnt1 = ($R[1] - $L[1]) / 2 + 1;

    $dp = array();

    // Base Cases
    $dp[1][0] = $cnt0;
    $dp[1][1] = $cnt1;
    for ($i = 2; $i <= $n; $i++)
    {

        // Ways to form array whose sum upto
        // i numbers modulo 2 is 0
        $dp[$i][0] = ($cnt0 * $dp[$i - 1][0] +
                      $cnt1 * $dp[$i - 1][1]);

        // Ways to form array whose sum upto
        // i numbers modulo 2 is 1
        $dp[$i][1] = ($cnt0 * $dp[$i - 1][1] +
                      $cnt1 * $dp[$i - 1][0]);
    }

    // Return the required count of ways
    return $dp[$n][0];
}

// Driver Code
$n = 2;
$l = 1;
$r = 3;

echo countWays($n, $l, $r);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to return the number of ways to
    // form an array of size n such that sum of
    // all elements is divisible by 2
    function countWays(n, l, r)
    {
        let tL = l, tR = r;

        // Represents first and last numbers
        // of each type (modulo 0 and 1)
        let L = new Array(3);
        let R = new Array(3);
        L[l % 2] = l;
        R[r % 2] = r;

        l++;
        r--;

        if (l <= tR && r >= tL)
        {
            L[l % 2] = l;
            R[r % 2] = r;
        }

        // Count of numbers of each type between range
        let cnt0 = 0, cnt1 = 0;
        if (R[0] > 0 && L[0] > 0)
            cnt0 = (R[0] - L[0]) / 2 + 1;
        if (R[1] > 0 && L[1] > 0)
            cnt1 = (R[1] - L[1]) / 2 + 1;

        let dp = new Array(n + 1);
        for (let i = 0; i <= n; i++)
        {   
            dp[i] = new Array(3);
            for (let j = 0; j < 3; j++)
            {
                dp[i][j] = 0;
            }
        }

        // Base Cases
        dp[1][0] = cnt0;
        dp[1][1] = cnt1;
        for (let i = 2; i <= n; i++)
        {

            // Ways to form array whose sum upto
            // i numbers modulo 2 is 0
            dp[i][0] = (cnt0 * dp[i - 1] [0]
                        + cnt1 * dp[i - 1][1]);

            // Ways to form array whose sum upto
            // i numbers modulo 2 is 1
            dp[i][1] = (cnt0 * dp[i - 1][1]
                        + cnt1 * dp[i - 1][0]);
        }

        // Return the required count of ways
        return dp[n][0];
    }

    let n = 2, l = 1, r = 3;
    document.write(countWays(n, l, r));

</script>
```

**Output:** 

```
5
```