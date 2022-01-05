# 好字符串的位数总和

> 原文:[https://www . geesforgeks . org/好字符串的位数总和/](https://www.geeksforgeeks.org/sum-of-digits-of-the-good-strings/)

如果字符串仅由数字 **0** 到 **9** 组成，并且相邻元素不同，则称为好字符串。任务是找到以给定数字 **Y** 结束的所有可能的长度良好字符串的数字总和 **X** 。答案可能很大，所以以 **10 <sup>9</sup> + 7** 为模打印答案。

**示例:**

> **输入:** X = 2，Y = 2
> **输出:** 61
> 以 2 结尾的长度为 2 的所有可能字符串为:
> 02，12，32，42，52，62，72，82，92。
> 现在，((0+2)+(1+2)+(3+2)+(4+2)+(5+2)
> +(6+2)+(7+2)+(8+2)+(9+2))= 61
> 
> **输入:** X = 6，Y = 4
> T3】输出: 1567751

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。让我们定义以下状态:

1.  **dp[i][j]:** 以 **j** 结尾的所有可能的长度为 **i** 的好字符串的位数总和。
2.  **cnt[i][j]:** 数一数以 **j** 结尾的长度为 **i** 的好弦。

前一个状态的值必须用来计算当前状态的值，因为相邻的数字必须进行比较，看它们是否相等。现在，循环关系将是:

> DP[I][j]= DP[I][j]+DP[I-1][k]+CNT[I-1][k]* j

这里，**DP[I–1][k]**是以 **k** 和 **k 结束的长度为**(I–1)**的好串的位数之和！= j** 。
**cnt[i -1][k]** 是以 **k** 和 **k 结束的长度为**(I–1)**的好串数！= j** 。
因此对于位置 **i** ，**(CNT(I–1)【k】* j)**必须添加，因为 **j** 被放在索引 **i** 处，并且具有长度**(I–1)**的可能串的计数是**CNT【I–1】【k】**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define DIGITS 10
#define MAX 10000
#define MOD 1000000007

// To store the states of the dp
long dp[MAX][DIGITS], cnt[MAX][DIGITS];

// Function to fill the dp table
void precompute()
{

    // dp[i][j] : Sum of the digits of all
    // possible good strings of length
    // i that end with j
    // cnt[i][j] : Count of the good strings
    // of length i that end with j

    // Sum of digits of the string of length
    // 1 is i as i is only number in that string
    // and count of good strings of length 1
    // that end with i is also 1
    for (int i = 0; i < DIGITS; i++)
        dp[1][i] = i, cnt[1][i] = 1;

    for (int i = 2; i < MAX; i++) {
        for (int j = 0; j < DIGITS; j++) {
            for (int k = 0; k < DIGITS; k++) {

                // Adjacent digits are different
                if (j != k) {
                    dp[i][j] = dp[i][j]
                               + (dp[i - 1][k] + (cnt[i - 1][k] * j) % MOD)
                                     % MOD;
                    dp[i][j] %= MOD;

                    // Increment the count as digit at
                    // (i - 1)'th index is k and count
                    // of good strings is equal to this
                    // because at the end of the strings of
                    // length (i - 1) we are just
                    // putting digit j as the last digit
                    cnt[i][j] += cnt[i - 1][k];
                    cnt[i][j] %= MOD;
                }
            }
        }
    }
}

// Driver code
int main()
{
    long long int x = 6, y = 4;

    precompute();

    cout << dp[x][y];

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    final static int DIGITS = 10;
    final static int MAX = 10000;
    final static int MOD = 1000000007;

    // To store the states of the dp
    static int dp[][] = new int[MAX][DIGITS];
    static int cnt[][] = new int[MAX][DIGITS];

    // Function to fill the dp table
    static void precompute()
    {

        // dp[i][j] : Sum of the digits of all
        // possible good strings of length
        // i that end with j
        // cnt[i][j] : Count of the good strings
        // of length i that end with j

        // Sum of digits of the string of length
        // 1 is i as i is only number in that string
        // and count of good strings of length 1
        // that end with i is also 1
        for (int i = 0; i < DIGITS; i++)
        {
            dp[1][i] = i;
            cnt[1][i] = 1;
        }

        for (int i = 2; i < MAX; i++)
        {
            for (int j = 0; j < DIGITS; j++)
            {
                for (int k = 0; k < DIGITS; k++)
                {

                    // Adjacent digits are different
                    if (j != k)
                    {
                        dp[i][j] = dp[i][j] + (dp[i - 1][k] +
                                             (cnt[i - 1][k] * j) % MOD)
                                                                 % MOD;
                        dp[i][j] %= MOD;

                        // Increment the count as digit at
                        // (i - 1)'th index is k and count
                        // of good strings is equal to this
                        // because at the end of the strings of
                        // length (i - 1) we are just
                        // putting digit j as the last digit
                        cnt[i][j] += cnt[i - 1][k];
                        cnt[i][j] %= MOD;
                    }
                }
            }
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int x = 6, y = 4;

        precompute();

        System.out.println(dp[x][y]);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
DIGITS = 10;
MAX = 10000;
MOD = 1000000007;

# To store the states of the dp
dp = [[0 for i in range(DIGITS)]
         for i in range(MAX)];
cnt = [[0 for i in range(DIGITS)]
          for i in range(MAX)];

# Function to fill the dp table
def precompute():

    # dp[i][j] : Sum of the digits of all
    # possible good strings of length
    # i that end with j
    # cnt[i][j] : Count of the good strings
    # of length i that end with j

    # Sum of digits of the string of length
    # 1 is i as i is only number in that string
    # and count of good strings of length 1
    # that end with i is also 1
    for i in range(DIGITS):

        dp[1][i] = i;
        cnt[1][i] = 1;

    for i in range(2, MAX):
        for j in range(DIGITS):
            for k in range(DIGITS):

                # Adjacent digits are different
                if (j != k):

                    dp[i][j] = dp[i][j] + (dp[i - 1][k] +\
                                         (cnt[i - 1][k] * j) % MOD) % MOD;
                    dp[i][j] %= MOD;

                    # Increment the count as digit at
                    # (i - 1)'th index is k and count
                    # of good strings is equal to this
                    # because at the end of the strings of
                    # length (i - 1) we are just
                    # putting digit j as the last digit
                    cnt[i][j] += cnt[i - 1][k];
                    cnt[i][j] %= MOD;

# Driver code
x = 6; y = 4;

precompute();

print(dp[x][y]);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    readonly static int DIGITS = 10;
    readonly static int MAX = 10000;
    readonly static int MOD = 1000000007;

    // To store the states of the dp
    static int [,]dp = new int[MAX, DIGITS];
    static int [,]cnt = new int[MAX, DIGITS];

    // Function to fill the dp table
    static void precompute()
    {

        // dp[i][j] : Sum of the digits of all
        // possible good strings of length
        // i that end with j
        // cnt[i][j] : Count of the good strings
        // of length i that end with j

        // Sum of digits of the string of length
        // 1 is i as i is only number in that string
        // and count of good strings of length 1
        // that end with i is also 1
        for (int i = 0; i < DIGITS; i++)
        {
            dp[1, i] = i;
            cnt[1, i] = 1;
        }

        for (int i = 2; i < MAX; i++)
        {
            for (int j = 0; j < DIGITS; j++)
            {
                for (int k = 0; k < DIGITS; k++)
                {

                    // Adjacent digits are different
                    if (j != k)
                    {
                        dp[i, j] = dp[i, j] + (dp[i - 1, k] +
                                             (cnt[i - 1, k] * j) % MOD)
                                                                 % MOD;
                        dp[i, j] %= MOD;

                        // Increment the count as digit at
                        // (i - 1)'th index is k and count
                        // of good strings is equal to this
                        // because at the end of the strings of
                        // length (i - 1) we are just
                        // putting digit j as the last digit
                        cnt[i, j] += cnt[i - 1, k];
                        cnt[i, j] %= MOD;
                    }
                }
            }
        }
    }

    // Driver code
    public static void Main (String[] args)
    {
        int x = 6, y = 4;

        precompute();

        Console.WriteLine(dp[x,y]);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var DIGITS = 10
var MAX = 10000
var MOD = 1000000007

// To store the states of the dp
var dp = Array.from(Array(MAX), ()=> Array(DIGITS).fill(0));
var cnt = Array.from(Array(MAX), ()=> Array(DIGITS).fill(0));

// Function to fill the dp table
function precompute()
{

    // dp[i][j] : Sum of the digits of all
    // possible good strings of length
    // i that end with j
    // cnt[i][j] : Count of the good strings
    // of length i that end with j

    // Sum of digits of the string of length
    // 1 is i as i is only number in that string
    // and count of good strings of length 1
    // that end with i is also 1
    for (var i = 0; i < DIGITS; i++)
        dp[1][i] = i, cnt[1][i] = 1;

    for (var i = 2; i < MAX; i++) {
        for (var j = 0; j < DIGITS; j++) {
            for (var k = 0; k < DIGITS; k++) {

                // Adjacent digits are different
                if (j != k) {
                    dp[i][j] = dp[i][j]
                               + (dp[i - 1][k] +
                                  (cnt[i - 1][k] * j) % MOD)% MOD;
                    dp[i][j] %= MOD;

                    // Increment the count as digit at
                    // (i - 1)'th index is k and count
                    // of good strings is equal to this
                    // because at the end of the strings of
                    // length (i - 1) we are just
                    // putting digit j as the last digit
                    cnt[i][j] += cnt[i - 1][k];
                    cnt[i][j] %= MOD;
                }
            }
        }
    }
}

// Driver code
var x = 6, y = 4;
precompute();
document.write( dp[x][y]);

</script>
```

**Output:** 

```
1567751
```

**时间复杂度:** O(N)