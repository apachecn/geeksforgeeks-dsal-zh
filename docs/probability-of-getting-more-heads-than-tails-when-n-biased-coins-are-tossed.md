# 投掷 N 枚偏向硬币时正面多于反面的概率

> 原文:[https://www . geeksforgeeks . org/n-biased-coins-through-to-head-多于-tail-当 n-biased-coins-through-through-through-through-through-through-through-through-through-through-through-](https://www.geeksforgeeks.org/probability-of-getting-more-heads-than-tails-when-n-biased-coins-are-tossed/)

给定奇数长度的数组**p[]****N**，其中 **p[i]** 表示获得第**I**枚硬币正面的概率。由于硬币有偏差，获得人头的概率并不总是等于 **0.5** 。任务是找到头部比尾部获得更多次数的概率。

**示例:**

> **输入:** p[] = {0.3，0.4，0.7 }
> T3】输出: 0.442
> 一个尾巴的概率=(1–一个头部的概率)
> 对于头部大于尾部，有 4 种可能:
> T8】P({头部，头部，尾部})= 0.3 x 0.4 x(1–0.7)= 0.036
> **P({尾部，头部，头部 head })**= 0.3 x(1–0.4)x 0.7 = 0.126
> **P({ head，head，head })**= 0.3 x 0.4 x 0.7 = 0.084
> 将上述概率
> **相加为 0.036+0.196+0.126+0.084 = 0.442**
> 
> **输入:** p[] = {0.3，0.5，0.2，0.6，0.9 }
> T3】输出: 0.495

**天真的方法:**天真的方法是创造所有正面和反面的**2<sup>n</sup>T5】可能性。然后计算不同排列的概率，当头部的数量大于尾部的数量时相加，就像例子解释的那样。当 **n** 较大时，这将给出 TLE。**

**高效途径:**思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。让我们假设 **dp[i][j]** 是用第一枚 **i** 硬币获得 **j** 人头的概率。要将 **j** 头放在 **i <sup>th</sup>** 位置，有两种可能:

1.  如果直到**(I–1)**硬币的头数等于 **j** ，那么在 **i <sup>th</sup>** 处会出现一条尾巴。
2.  如果直到**(I–1)**硬币的头数等于**(j–1)**，则一个头出现在 **i <sup>第</sup>** 位置

因此，它可以分成如下子问题:

> dp[i][j] = dp[i – 1][j] * （1 – p[i]） + dp[i – 1][j – 1] * p[i]

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the probability when
// number of heads is greater than the number of tails
double Probability(double p[], int n)
{

    // Declaring the DP table
    double dp[n + 1][n + 1];
    memset(dp, 0.0, sizeof(dp));

    // Base case
    dp[0][0] = 1.0;

    // Iterating for every coin
    for (int i = 1; i <= n; i += 1) {

        // j represents the numbers of heads
        for (int j = 0; j <= i; j += 1) {

            // If number of heads is equal to zero
            // there there is only one possibility
            if (j == 0)
                dp[i][j] = dp[i - 1][j]
                           * (1.0 - p[i]);
            else
                dp[i][j] = dp[i - 1][j]
                               * (1.0 - p[i])
                           + dp[i - 1][j - 1] * p[i];
        }
    }

    double ans = 0.0;

    // When the number of heads is greater than (n+1)/2
    // it means that heads are greater than tails as
    // no of tails + no of heads is equal to n for
    // any permutation of heads and tails
    for (int i = (n + 1) / 2; i <= n; i += 1)
        ans += dp[n][i];

    return ans;
}

// Driver Code
int main()
{
    // 1 based indexing
    double p[] = { 0.0, 0.3, 0.4, 0.7 };

    // Number of coins
    int n = sizeof(p) / sizeof(p[0]) - 1;

    // Function call
    cout << Probability(p, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function to return the probability when
// number of heads is greater than the number of tails
static double Probability(double p[], int n)
{

    // Declaring the DP table
    double [][]dp = new double[n + 1][n + 1];

    // Base case
    dp[0][0] = 1.0;

    // Iterating for every coin
    for (int i = 1; i <= n; i += 1)
    {

        // j represents the numbers of heads
        for (int j = 0; j <= i; j += 1)
        {

            // If number of heads is equal to zero
            // there there is only one possibility
            if (j == 0)
                dp[i][j] = dp[i - 1][j]
                        * (1.0 - p[i]);
            else
                dp[i][j] = dp[i - 1][j]
                            * (1.0 - p[i])
                        + dp[i - 1][j - 1] * p[i];
        }
    }

    double ans = 0.0;

    // When the number of heads is greater than (n+1)/2
    // it means that heads are greater than tails as
    // no of tails + no of heads is equal to n for
    // any permutation of heads and tails
    for (int i = (n + 1) / 2; i <= n; i += 1)
        ans += dp[n][i];

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    // 1 based indexing
    double p[] = { 0.0, 0.3, 0.4, 0.7 };

    // Number of coins
    int n = p.length - 1;

    // Function call
    System.out.println(Probability(p, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import numpy as np

# Function to return the probability when
# number of heads is greater than
# the number of tails
def Probability(p, n) :

    # Declaring the DP table
    dp = np.zeros((n + 1, n + 1));
    for i in range(n + 1) :
        for j in range(n + 1) :
            dp[i][j] = 0.0

    # Base case
    dp[0][0] = 1.0;

    # Iterating for every coin
    for i in range(1, n + 1) :

        # j represents the numbers of heads
        for j in range(i + 1) :

            # If number of heads is equal to zero
            # there there is only one possibility
            if (j == 0) :
                dp[i][j] = dp[i - 1][j] * (1.0 - p[i]);
            else :
                dp[i][j] = (dp[i - 1][j] * (1.0 - p[i]) +
                            dp[i - 1][j - 1] * p[i]);

    ans = 0.0;

    # When the number of heads is greater than (n+1)/2
    # it means that heads are greater than tails as
    # no of tails + no of heads is equal to n for
    # any permutation of heads and tails
    for i in range((n + 1)// 2, n + 1) :
        ans += dp[n][i];

    return ans;

# Driver Code
if __name__ == "__main__" :

    # 1 based indexing
    p = [ 0.0, 0.3, 0.4, 0.7 ];

    # Number of coins
    n = len(p) - 1;

    # Function call
    print(Probability(p, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to return the probability when
// number of heads is greater than the number of tails
static double Probability(double []p, int n)
{

    // Declaring the DP table
    double [,]dp = new double[n + 1, n + 1];

    // Base case
    dp[0, 0] = 1.0;

    // Iterating for every coin
    for (int i = 1; i <= n; i += 1)
    {

        // j represents the numbers of heads
        for (int j = 0; j <= i; j += 1)
        {

            // If number of heads is equal to zero
            // there there is only one possibility
            if (j == 0)
                dp[i,j] = dp[i - 1,j]
                        * (1.0 - p[i]);
            else
                dp[i,j] = dp[i - 1,j]
                            * (1.0 - p[i])
                        + dp[i - 1,j - 1] * p[i];
        }
    }

    double ans = 0.0;

    // When the number of heads is greater than (n+1)/2
    // it means that heads are greater than tails as
    // no of tails + no of heads is equal to n for
    // any permutation of heads and tails
    for (int i = (n + 1) / 2; i <= n; i += 1)
        ans += dp[n,i];

    return ans;
}

// Driver Code
static public void Main ()
{

    // 1 based indexing
    double []p = { 0.0, 0.3, 0.4, 0.7 };

    // Number of coins
    int n = p.Length - 1;

    // Function call
    Console.Write(Probability(p, n));
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the probability when
// number of heads is greater than the number of tails
function Probability(p , n)
{

    // Declaring the DP table
    var dp = Array(n + 1).fill(0).map(
        x => Array(n + 1).fill(0));

    // Base case
    dp[0][0] = 1.0;

    // Iterating for every coin
    for(var i = 1; i <= n; i += 1)
    {

        // j represents the numbers of heads
        for(var j = 0; j <= i; j += 1)
        {

            // If number of heads is equal to zero
            // there there is only one possibility
            if (j == 0)
                dp[i][j] = dp[i - 1][j] *
                           (1.0 - p[i]);
            else
                dp[i][j] = dp[i - 1][j] * (1.0 - p[i]) +
                           dp[i - 1][j - 1] * p[i];
        }
    }

    var ans = 0.0;

    // When the number of heads is greater than (n+1)/2
    // it means that heads are greater than tails as
    // no of tails + no of heads is equal to n for
    // any permutation of heads and tails
    for(var i = parseInt((n + 1) / 2); i <= n; i += 1)
        ans += dp[n][i];

    return ans;
}

// Driver Code

// 1 based indexing
var p = [ 0.0, 0.3, 0.4, 0.7 ];

// Number of coins
var n = p.length - 1;

// Function call
document.write(Probability(p, n));

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
0.442
```