# 计算二进制字符串的数量，使得所有 1 都不存在长度大于或等于 3 的子字符串

> 原文:[https://www . geesforgeks . org/count-number-of-binary-strings-this-没有长度大于或等于 3 的子串，且全部为 1/](https://www.geeksforgeeks.org/count-number-of-binary-strings-such-that-there-is-no-substring-of-length-greater-than-or-equal-to-3-with-all-1s/)

给定一个整数 **N** ，任务是计算可能长度为 **N** 的二进制字符串的数量，使得它们不包含**“111”**作为子字符串。答案可能很大，所以打印答案模 **10 <sup>9</sup> + 7** 。
**举例:**

> **输入:** N = 3
> **输出:** 7
> 所有可能的子串为“000”、“001”、
> “010”、“011”、“100”、“101”和“110”。
> “111”不是有效字符串。
> **输入** N = 16
> **输出:** 19513

**方法:** [动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以用来解决这个问题。创建一个 dp[][]数组，其中 dp[i][j]将存储可能的子字符串的计数，使得 1 在第 I 个索引之前连续出现 j 次。现在，循环关系将是:

> dp[i][0] = dp[i – 1][0] + dp[i – 1][1] + dp[i – 1][2]
> dp[i ][1] = dp[i – 1][0]
> dp[i][2] = dp[i – 1][1]

基本情况为 **dp[1][0] = 1** 、 **dp[1][1] = 1** 和 **dp[1][2] = 0** 。现在，所需的字符串数将是**DP[N][0]+DP[N][1]+DP[N][2]**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const long MOD = 1000000007;

// Function to return the count
// of all possible valid strings
long countStrings(long N)
{

    long dp[N + 1][3];

    // Fill 0's in the dp array
    memset(dp, 0, sizeof(dp));

    // Base cases
    dp[1][0] = 1;
    dp[1][1] = 1;
    dp[1][2] = 0;

    for (int i = 2; i <= N; i++) {

        // dp[i][j] = number of possible strings
        // such that '1' just appeared consecutively
        // j times upto the ith index
        dp[i][0] = (dp[i - 1][0] + dp[i - 1][1]
                    + dp[i - 1][2])
                   % MOD;

        // Taking previously calculated value
        dp[i][1] = dp[i - 1][0] % MOD;
        dp[i][2] = dp[i - 1][1] % MOD;
    }

    // Taking all possible cases that
    // can appear at the Nth position
    long ans = (dp[N][0] + dp[N][1]
                + dp[N][2])
               % MOD;

    return ans;
}

// Driver code
int main()
{
    long N = 3;

    cout << countStrings(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    final static int MOD = 1000000007;

    // Function to return the count
    // of all possible valid strings
    static long countStrings(int N)
    {
        int i, j;

        int dp[][] = new int[N + 1][3];

        // Fill 0's in the dp array
        for(i = 0; i < N + 1; i++)
        {
            for(j = 9; j < 3 ; j ++)
            {
                dp[i][j] = 0;
            }
        }

        // Base cases
        dp[1][0] = 1;
        dp[1][1] = 1;
        dp[1][2] = 0;

        for (i = 2; i <= N; i++)
        {

            // dp[i][j] = number of possible strings
            // such that '1' just appeared consecutively
            // j times upto the ith index
            dp[i][0] = (dp[i - 1][0] + dp[i - 1][1] +
                        dp[i - 1][2]) % MOD;

            // Taking previously calculated value
            dp[i][1] = dp[i - 1][0] % MOD;
            dp[i][2] = dp[i - 1][1] % MOD;
        }

        // Taking all possible cases that
        // can appear at the Nth position
        int ans = (dp[N][0] + dp[N][1] +
                              dp[N][2]) % MOD;

        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 3;

        System.out.println(countStrings(N));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MOD = 1000000007

# Function to return the count
# of all possible valid strings
def countStrings(N):

    # Initialise and fill 0's in the dp array
    dp = [[0] * 3 for i in range(N + 1)]

    # Base cases
    dp[1][0] = 1;
    dp[1][1] = 1;
    dp[1][2] = 0;

    for i in range(2, N + 1):

        # dp[i][j] = number of possible strings
        # such that '1' just appeared consecutively
        # j times upto the ith index
        dp[i][0] = (dp[i - 1][0] +
                    dp[i - 1][1] +
                    dp[i - 1][2]) % MOD

        # Taking previously calculated value
        dp[i][1] = dp[i - 1][0] % MOD
        dp[i][2] = dp[i - 1][1] % MOD

    # Taking all possible cases that
    # can appear at the Nth position
    ans = (dp[N][0] + dp[N][1] + dp[N][2]) % MOD

    return ans

# Driver code
if __name__ == '__main__':

    N = 3

    print(countStrings(N))

# This code is contributed by ashutosh450
```

## C#

```
// C# implementation of the above approach
using System;        

class GFG
{
    static readonly int MOD = 1000000007;

    // Function to return the count
    // of all possible valid strings
    static long countStrings(int N)
    {
        int i, j;

        int [,]dp = new int[N + 1, 3];

        // Fill 0's in the dp array
        for(i = 0; i < N + 1; i++)
        {
            for(j = 9; j < 3; j ++)
            {
                dp[i, j] = 0;
            }
        }

        // Base cases
        dp[1, 0] = 1;
        dp[1, 1] = 1;
        dp[1, 2] = 0;

        for (i = 2; i <= N; i++)
        {

            // dp[i,j] = number of possible strings
            // such that '1' just appeared consecutively
            // j times upto the ith index
            dp[i, 0] = (dp[i - 1, 0] + dp[i - 1, 1] +
                        dp[i - 1, 2]) % MOD;

            // Taking previously calculated value
            dp[i, 1] = dp[i - 1, 0] % MOD;
            dp[i, 2] = dp[i - 1, 1] % MOD;
        }

        // Taking all possible cases that
        // can appear at the Nth position
        int ans = (dp[N, 0] + dp[N, 1] +
                              dp[N, 2]) % MOD;

        return ans;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int N = 3;

        Console.WriteLine(countStrings(N));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// javascript implementation of the approach

    var MOD = 1000000007;

    // Function to return the count
    // of all possible valid strings
    function countStrings(N)
    {
        var i, j;

        var dp = Array(N+1).fill(0).map(x => Array(3).fill(0));

        // Fill 0's in the dp array
        for(i = 0; i < N + 1; i++)
        {
            for(j = 9; j < 3 ; j ++)
            {
                dp[i][j] = 0;
            }
        }

        // Base cases
        dp[1][0] = 1;
        dp[1][1] = 1;
        dp[1][2] = 0;

        for (i = 2; i <= N; i++)
        {

            // dp[i][j] = number of possible strings
            // such that '1' just appeared consecutively
            // j times upto the ith index
            dp[i][0] = (dp[i - 1][0] + dp[i - 1][1] +
                        dp[i - 1][2]) % MOD;

            // Taking previously calculated value
            dp[i][1] = dp[i - 1][0] % MOD;
            dp[i][2] = dp[i - 1][1] % MOD;
        }

        // Taking all possible cases that
        // can appear at the Nth position
        var ans = (dp[N][0] + dp[N][1] +
                              dp[N][2]) % MOD;

        return ans;
    }

// Driver code
var N = 3;
document.write(countStrings(N));

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
7
```