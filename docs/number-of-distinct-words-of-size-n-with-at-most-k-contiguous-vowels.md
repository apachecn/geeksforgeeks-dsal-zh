# 大小为 N、最多有 K 个连续元音的不同单词的数量

> 原文:[https://www . geeksforgeeks . org/最多 k 个连续元音的大小不同单词数/](https://www.geeksforgeeks.org/number-of-distinct-words-of-size-n-with-at-most-k-contiguous-vowels/)

给定两个整数 **N** 和 **K** ，任务是找出由长度为 **N** 的小写字母组成的不同[字符串](https://www.geeksforgeeks.org/string-data-structure/)的数量，这些字符串最多可以由 **K** 个连续的元音组成。由于答案可能太大，打印**答案%1000000007** 。

> **输入:** N = 1，K = 0
> **输出:** 21
> **说明:**所有的 21 个辅音都在那里，有 0 个连续的元音，长度为 1。
> 
> **输入:** N = 1，K = 1
> T3】输出: 26

**方法:**解决这个问题的思路是基于[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。按照以下步骤解决问题:

*   让 **dp[i][j]** 成为区分长度为 **i** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)的方法数，其中[字符串](https://www.geeksforgeeks.org/string-data-structure/)的最后一个 **j** 字符是元音。
*   所以[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)的状态是:
    *   如果 **j = 0** ，那么**DP[I][j]=(DP[I-1][0]+DP[I-1][1]+……+DP[I-1][K])* 21**(由整数变量**和** ) 表示，因为最后添加的字符应该是一个辅音，而不仅仅是 **j** 的值将变成 **0** ，而不管它在先前状态下的值如何。
    *   如果 **i < j** 那么 **dp[i][j] = 0** 。因为不可能创建包含 **j** 元音并且长度小于 **j** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)。
    *   如果 **i == j** ，那么 **dp[i][j] = 5 <sup>i</sup>** 因为[串](https://www.geeksforgeeks.org/string-data-structure/)中的字符数等于元音数，所以所有的字符都应该是元音。
    *   如果 **j < i** 那么 **dp[i][j] = dp[i-1][j-1]*5** 因为一个长度为 **i** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)带有最后一个 **j** 字符只有当最后一个字符是元音并且长度为 **i-1** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/)具有最后一个**j–1**字符作为元音时，才能发出元音。
*   打印**DP[n][0]+DP[n][1]+……+DP[n][K]**之和作为答案。

以下是上述方法的实施情况

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Power function to calculate
// long powers with mod
long long int power(long long int x,
                    long long int y,
                    long long int p)
{
    long long int res = 1ll;

    x = x % p;

    if (x == 0)
        return 0;

    while (y > 0) {

        if (y & 1)
            res = (res * x) % p;
        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Function for finding number of ways to
// create string with length N and atmost
// K contiguous vowels
int kvowelwords(int N, int K)
{

    long long int i, j;
    long long int MOD = 1000000007;

    // Array dp to store number of ways
    long long int dp[N + 1][K + 1] = { 0 };

    long long int sum = 1;
    for (i = 1; i <= N; i++) {

        // dp[i][0] = (dp[i-1][0]+dp[i-1][1]..dp[i-1][k])*21
        dp[i][0] = sum * 21;
        dp[i][0] %= MOD;

        // Now setting sum to be dp[i][0]
        sum = dp[i][0];

        for (j = 1; j <= K; j++) {
            // If j>i, no ways are possible to create
            // a string with length i and vowel j
            if (j > i)
                dp[i][j] = 0;
            else if (j == i) {
                // If j = i all the character should
                // be vowel
                dp[i][j] = power(5ll, i, MOD);
            }
            else {
                // dp[i][j] relation with dp[i-1][j-1]
                dp[i][j] = dp[i - 1][j - 1] * 5;
            }

            dp[i][j] %= MOD;

            // Adding dp[i][j] in the sum
            sum += dp[i][j];
            sum %= MOD;
        }
    }

    return sum;
}
// Driver Program
int main()
{
    // Input
    int N = 3;
    int K = 3;

    // Function Call
    cout << kvowelwords(N, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Power function to calculate
// long powers with mod
static int power(int x, int y, int p)
{
    int res = 1;
    x = x % p;

    if (x == 0)
        return 0;

    while (y > 0)
    {
        if ((y & 1) != 0)
            res = (res * x) % p;

        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Function for finding number of ways to
// create string with length N and atmost
// K contiguous vowels
static int kvowelwords(int N, int K)
{
    int i, j;
    int MOD = 1000000007;

    // Array dp to store number of ways
    int[][] dp = new int[N + 1][K + 1] ;

    int sum = 1;
    for(i = 1; i <= N; i++)
    {

        // dp[i][0] = (dp[i-1][0]+dp[i-1][1]..dp[i-1][k])*21
        dp[i][0] = sum * 21;
        dp[i][0] %= MOD;

        // Now setting sum to be dp[i][0]
        sum = dp[i][0];

        for(j = 1; j <= K; j++)
        {

            // If j>i, no ways are possible to create
            // a string with length i and vowel j
            if (j > i)
                dp[i][j] = 0;

            else if (j == i)
            {

                // If j = i all the character should
                // be vowel
                dp[i][j] = power(5, i, MOD);
            }
            else
            {

                // dp[i][j] relation with dp[i-1][j-1]
                dp[i][j] = dp[i - 1][j - 1] * 5;
            }

            dp[i][j] %= MOD;

            // Adding dp[i][j] in the sum
            sum += dp[i][j];
            sum %= MOD;
        }
    }
    return sum;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int N = 3;
    int K = 3;

    // Function Call
    System.out.println( kvowelwords(N, K));
}
}

// This code is contributed by target_2
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Power function to calculate
# long powers with mod
def power(x, y, p):

    res = 1
    x = x % p

    if (x == 0):
        return 0

    while (y > 0):
        if (y & 1):
            res = (res * x) % p

        y = y >> 1
        x = (x * x) % p

    return res

# Function for finding number of ways to
# create string with length N and atmost
# K contiguous vowels
def kvowelwords(N, K):

    i, j = 0, 0
    MOD = 1000000007

    # Array dp to store number of ways
    dp = [[0 for i in range(K + 1)]
             for i in range(N + 1)]

    sum = 1
    for i in range(1, N + 1):

        #dp[i][0] = (dp[i-1][0]+dp[i-1][1]..dp[i-1][k])*21
        dp[i][0] = sum * 21
        dp[i][0] %= MOD

        # Now setting sum to be dp[i][0]
        sum = dp[i][0]

        for j in range(1, K + 1):

            # If j>i, no ways are possible to create
            # a string with length i and vowel j
            if (j > i):
                dp[i][j] = 0
            elif (j == i):

                # If j = i all the character should
                # be vowel
                dp[i][j] = power(5, i, MOD)
            else:

                # dp[i][j] relation with dp[i-1][j-1]
                dp[i][j] = dp[i - 1][j - 1] * 5

            dp[i][j] %= MOD

            # Adding dp[i][j] in the sum
            sum += dp[i][j]
            sum %= MOD

    return sum

# Driver Code
if __name__ == '__main__':

    # Input
    N = 3
    K = 3

    # Function Call
    print (kvowelwords(N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Power function to calculate
// long powers with mod
static int power(int x, int y, int p)
{
    int res = 1;
    x = x % p;

    if (x == 0)
        return 0;

    while (y > 0)
    {
        if ((y & 1) != 0)
            res = (res * x) % p;

        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Function for finding number of ways to
// create string with length N and atmost
// K contiguous vowels
static int kvowelwords(int N, int K)
{
    int i, j;
    int MOD = 1000000007;

    // Array dp to store number of ways
    int[,] dp = new int[N + 1, K + 1];

    int sum = 1;
    for(i = 1; i <= N; i++)
    {

        // dp[i][0] = (dp[i-1, 0]+dp[i-1, 1]..dp[i-1][k])*21
        dp[i, 0] = sum * 21;
        dp[i, 0] %= MOD;

        // Now setting sum to be dp[i][0]
        sum = dp[i, 0];

        for(j = 1; j <= K; j++)
        {

            // If j>i, no ways are possible to create
            // a string with length i and vowel j
            if (j > i)
                dp[i, j] = 0;

            else if (j == i)
            {

                // If j = i all the character should
                // be vowel
                dp[i, j] = power(5, i, MOD);
            }
            else
            {

                // dp[i][j] relation with dp[i-1][j-1]
                dp[i, j] = dp[i - 1, j - 1] * 5;
            }

            dp[i, j] %= MOD;

            // Adding dp[i][j] in the sum
            sum += dp[i, j];
            sum %= MOD;
        }
    }
    return sum;
}

// Driver Code
public static void Main()
{

    // Input
    int N = 3;
    int K = 3;

    // Function Call
    Console.Write(kvowelwords(N, K));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript code for above approach

// Power function to calculate
// long powers with mod
function power(x, y, p)
{
    let res = 1;
    x = x % p;

    if (x == 0)
        return 0;

    while (y > 0)
    {
        if ((y & 1) != 0)
            res = (res * x) % p;

        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Function for finding number of ways to
// create string with length N and atmost
// K contiguous vowels
function kvowelwords(N, K)
{
    let i, j;
    let MOD = 1000000007;

    // Array dp to store number of ways
    let dp = new Array(N + 1)
    // Loop to create 2D array using 1D array
    for (i = 0; i < dp.length; i++) {
        dp[i] = new Array(K + 1);
    }

    let sum = 1;
    for(i = 1; i <= N; i++)
    {

        // dp[i][0] = (dp[i-1][0]+dp[i-1][1]..dp[i-1][k])*21
        dp[i][0] = sum * 21;
        dp[i][0] %= MOD;

        // Now setting sum to be dp[i][0]
        sum = dp[i][0];

        for(j = 1; j <= K; j++)
        {

            // If j>i, no ways are possible to create
            // a string with length i and vowel j
            if (j > i)
                dp[i][j] = 0;

            else if (j == i)
            {

                // If j = i all the character should
                // be vowel
                dp[i][j] = power(5, i, MOD);
            }
            else
            {

                // dp[i][j] relation with dp[i-1][j-1]
                dp[i][j] = dp[i - 1][j - 1] * 5;
            }

            dp[i][j] %= MOD;

            // Adding dp[i][j] in the sum
            sum += dp[i][j];
            sum %= MOD;
        }
    }
    return sum;
}

// Driver Code

    // Input
    let N = 3;
    let K = 3;

    // Function Call
    document.write( kvowelwords(N, K));

    // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
17576
```

**时间复杂度:**O(n×K)
T3】辅助空间: O(N×K)