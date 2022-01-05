# 没有长度≥ 3 的子串的二进制串数

> 原文:[https://www . geesforgeks . org/二进制字符串数-这样就没有长度为 3 的子字符串/](https://www.geeksforgeeks.org/number-of-binary-strings-such-that-there-is-no-substring-of-length-3/)

给定一个整数 **N** ，任务是计算可能的二进制字符串的数量，使得所有 1 的长度中没有长度≥ 3 的子字符串。这个计数可能会变得非常大，因此以 **10 <sup>9</sup> + 7** 为模打印答案。
**举例:**

> **输入:** N = 4
> **输出:** 13
> 所有可能的有效字符串为 0000、0001、0010、0100、
> 1000、0101、0011、1010、1001、0110、1100、1101 和 1011。
> **输入:** N = 2
> **输出:** 4

**方法:**对于从 **1** 到 **N** 的每个值，唯一需要的字符串是其中“1”连续出现两次的子字符串数，一次或零次。这可以从 **2** 到 **N** 递归计算。[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)可用于记忆，其中 **dp[i][j]** 将存储可能字符串的数量，使得 **1** 刚刚连续出现 **j** 次直到**I<sup>th</sup>T21】索引，并且 **j** 将为 **0，1，2，…，i** (可能从 **1** 到
**DP[I][0]= DP[I–1][0]+DP[I–1][1]+DP[I–1][2]**如在 **i** 位置，将会放入 **0** 。
**DP[I][1]= DP[I–1][0]**由于在**(I–1)**位置没有 **1** 所以我们取这个值。
**DP[I][2]= DP[I–1][1]**作为第一个 **1** 出现在**(I–1)<sup>第</sup>** 位置(连续)，所以我们直接取那个值。
底壳长度为 1 串，即 **dp[1][0] = 1** ， **dp[1][1] = 1** ， **dp[1][2] = 0** 。因此，在**N**位置找到所有值**DP[N][0]+DP[N][1]+DP[N][2]**和所有可能情况的总和。
以下是上述方法的实施:** 

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const long MOD = 1000000007;

// Function to return the count of
// all possible binary strings
long countStr(long N)
{

    long dp[N + 1][3];

    // Fill 0's in the dp array
    memset(dp, 0, sizeof(dp));

    // Base cases
    dp[1][0] = 1;
    dp[1][1] = 1;
    dp[1][2] = 0;

    for (int i = 2; i <= N; i++) {

        // dp[i][j] is the number of possible
        // strings such that '1' just appeared
        // consecutively j times upto ith index
        dp[i][0] = (dp[i - 1][0] + dp[i - 1][1]
                    + dp[i - 1][2])
                   % MOD;

        // Taking previously calculated value
        dp[i][1] = dp[i - 1][0] % MOD;
        dp[i][2] = dp[i - 1][1] % MOD;
    }

    // Taking all the possible cases that
    // can appear at the Nth position
    long ans = (dp[N][0] + dp[N][1] + dp[N][2]) % MOD;

    return ans;
}

// Driver code
int main()
{
    long N = 8;

    cout << countStr(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    final static long MOD = 1000000007;

    // Function to return the count of
    // all possible binary strings
    static long countStr(int N)
    {
        long dp[][] = new long[N + 1][3];

        // Fill 0's in the dp array
        //memset(dp, 0, sizeof(dp));

        // Base cases
        dp[1][0] = 1;
        dp[1][1] = 1;
        dp[1][2] = 0;

        for (int i = 2; i <= N; i++)
        {

            // dp[i][j] is the number of possible
            // strings such that '1' just appeared
            // consecutively j times upto ith index
            dp[i][0] = (dp[i - 1][0] + dp[i - 1][1]
                        + dp[i - 1][2]) % MOD;

            // Taking previously calculated value
            dp[i][1] = dp[i - 1][0] % MOD;
            dp[i][2] = dp[i - 1][1] % MOD;
        }

        // Taking all the possible cases that
        // can appear at the Nth position
        long ans = (dp[N][0] + dp[N][1] + dp[N][2]) % MOD;

        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 8;

        System.out.println(countStr(N));
    }
}

// This code is contributed by AnkitRai01
```

## 计算机编程语言

```
# Python3 implementation of the approach
MOD = 1000000007

# Function to return the count of
# all possible binary strings
def countStr(N):

    dp = [[0 for i in range(3)] for i in range(N + 1)]

    # Base cases
    dp[1][0] = 1
    dp[1][1] = 1
    dp[1][2] = 0

    for i in range(2, N + 1):

        # dp[i][j] is the number of possible
        # strings such that '1' just appeared
        # consecutively j times upto ith index
        dp[i][0] = (dp[i - 1][0] + dp[i - 1][1] +
                    dp[i - 1][2]) % MOD

        # Taking previously calculated value
        dp[i][1] = dp[i - 1][0] % MOD
        dp[i][2] = dp[i - 1][1] % MOD

    # Taking all the possible cases that
    # can appear at the Nth position
    ans = (dp[N][0] + dp[N][1] + dp[N][2]) % MOD

    return ans

# Driver code
if __name__ == '__main__':
    N = 8

    print(countStr(N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static long MOD = 1000000007;

    // Function to return the count of
    // all possible binary strings
    static long countStr(int N)
    {
        long [,]dp = new long[N + 1, 3];

        // Base cases
        dp[1, 0] = 1;
        dp[1, 1] = 1;
        dp[1, 2] = 0;

        for (int i = 2; i <= N; i++)
        {

            // dp[i,j] is the number of possible
            // strings such that '1' just appeared
            // consecutively j times upto ith index
            dp[i, 0] = (dp[i - 1, 0] + dp[i - 1, 1]
                        + dp[i - 1, 2]) % MOD;

            // Taking previously calculated value
            dp[i, 1] = dp[i - 1, 0] % MOD;
            dp[i, 2] = dp[i - 1, 1] % MOD;
        }

        // Taking all the possible cases that
        // can appear at the Nth position
        long ans = (dp[N, 0] + dp[N, 1] + dp[N, 2]) % MOD;

        return ans;
    }

    // Driver code
    public static void Main ()
    {
        int N = 8;

        Console.WriteLine(countStr(N));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var MOD = 1000000007;

// Function to return the count of
// all possible binary strings
function countStr(N)
{

    var dp = Array.from(Array(N+1), ()=> Array(3).fill(0));

    // Base cases
    dp[1][0] = 1;
    dp[1][1] = 1;
    dp[1][2] = 0;

    for (var i = 2; i <= N; i++) {

        // dp[i][j] is the number of possible
        // strings such that '1' just appeared
        // consecutively j times upto ith index
        dp[i][0] = (dp[i - 1][0] + dp[i - 1][1]
                    + dp[i - 1][2])
                   % MOD;

        // Taking previously calculated value
        dp[i][1] = dp[i - 1][0] % MOD;
        dp[i][2] = dp[i - 1][1] % MOD;
    }

    // Taking all the possible cases that
    // can appear at the Nth position
    var ans = (dp[N][0] + dp[N][1] + dp[N][2]) % MOD;

    return ans;
}

// Driver code
var N = 8;
document.write( countStr(N));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
149
```

**时间复杂度:** O(N)