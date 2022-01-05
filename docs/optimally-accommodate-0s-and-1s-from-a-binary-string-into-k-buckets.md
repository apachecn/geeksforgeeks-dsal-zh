# 最佳地将二进制串中的 0 和 1 容纳到 K 个桶中

> 原文:[https://www . geeksforgeeks . org/optimal-accept-0s 和-1s-from-a-binary-string-to-k-bucket/](https://www.geeksforgeeks.org/optimally-accommodate-0s-and-1s-from-a-binary-string-into-k-buckets/)

给定一个二进制字符串 **S** ，由 0 和 1 组成。您必须将 0 和 1 放入 **K** 桶中，以满足以下条件:

1.  您可以将 0 和 1 填充到桶**中，保持 0 和 1 的相对顺序**，例如，您不能将 S[1]放入桶 2，将 S[0]放入桶 1。您必须保留二进制字符串的原始顺序。
2.  任何存储桶都不应留空，字符串中的任何元素都不应不被指定。
3.  每个桶的所有乘积之和(0 的个数* 1 的个数)应该是所有可能的容纳安排中的最小值。

如果无法解决，则打印 **-1。**

**示例:**

```
Input: S = "0001", K = 2
Output: 0
We have 3 choices {"0", "001"}, {"00", "01"}, {"000", 1}
First choice, we will get 1*0 + 2*1 = 2
Second choice, we will get 2*0 + 1*1 = 1
Third choice, we will get 3*0 + 0*1 = 0
Out of all the 3 choices, the third choice 
is giving the minimum answer.

Input: S = "0101", K = 1
Output: 1 
```

**递归实现:**您必须在不干扰上述条件的情况下，将二进制字符串容纳到 K 个桶中。然后通过将元素从**开始放入到 N** (N =二进制字符串的长度)中，填充第 I 个**桶(从 0 开始)，并不断添加计数 0 和 1，直到开始索引，可以得到简单的递归解。对于每次迭代，如果有 **x 个 0 和 y 个 1**直到开始，则再次出现 **f(start，K) = x * y + f(start + 1，K–1)**，因为下一个调节将从第(start + 1)个索引开始，剩余桶将为 K–1。**

因此，递归公式将是–

```
F(start, current_bucket) =  |           |
                            |       min |  F(i + 1, next_bucket) + (ones * zeroes in current_bucket)  
                            |           |   
                            | i = start to N
```

**自上而下的动态方法:**
通过将 start 和 bucket 变量不同组合的结果保存到二维 DP 数组中，可以将递归关系改为**动态解**。我们可以利用字符串的顺序应该被保留的事实。您可以有一个二维数组保存大小状态**【字符串*桶的大小】**，其中 dp[i][j]将告诉我们在使用 j + 1 个桶索引字符串之前的最小容纳值。我们的最终答案将在**DP【N-1】【K-1】**中。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// 2-D dp array saving different states
// dp[i][j] = minimum value of accommodation
// till i'th index of the string
// using j+1 number of buckets.
vector<vector<int> > dp;

// Function to find the minimum required
// sum using dynamic programming
int solveUtil(int start, int bucket, string str, int K)
{
    int N = str.size();

    // If both start and bucket reached end then
    // return 0 else that arrangement is not possible
    // so return INT_MAX
    if (start == N) {
        if (bucket == K)
            return 0;
        return INT_MAX;
    }

    // Corner case
    if (bucket == K)
        return INT_MAX;

    // If state if already calculated
    // then return its answer
    if (dp[start][bucket] != -1)
        return dp[start][bucket];

    int zeroes = 0;
    int ones = 0;
    int ans = INT_MAX;

    // Start filling zeroes and ones which to be accommodated
    // in jth bucket then ans for current arrangement will be
    // ones*zeroes + recur(i+1, bucket+1)
    for (int i = start; i < N; ++i) {
        if (str[i] == '1')
            ones++;
        else
            zeroes++;

        if (ones * zeroes > ans)
            break;

        int temp = solveUtil(i + 1, bucket + 1, str, K);

        // If this arrangement is not possible then
        // don't calculate further
        if (temp != INT_MAX) {
            ans = min(ans, temp + (ones * zeroes));
        }
    }

    return dp[start][bucket] = ans;
}

// Function to initialize the dp and call
// solveUtil() method to get the answer
int solve(string str, int K)
{
    int N = str.size();
    dp.clear();
    dp.resize(N, vector<int>(K, -1));

    // Start with 0-th index and 1 bucket
    int ans = solveUtil(0, 0, str, K);

    return ans == INT_MAX ? -1 : ans;
}

// Driver code
int main()
{
    string S = "0101";

    // K buckets
    int K = 2;

    cout << solve(S, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;
import java.util.*;

class GFG{

// 2-D dp array saving different states
// dp[i][j] = minimum value of accommodation
// till i'th index of the string
// using j+1 number of buckets.
static int[][] dp;

// Function to find the minimum required
// sum using dynamic programming
static int solveUtil(int start, int bucket,
                     String str, int K)
{
    int N = str.length();

    // If both start and bucket reached end
    // then return 0 else that arrangement
    // is not possible so return INT_MAX
    if (start == N)
    {
        if (bucket == K)
        {
            return 0;
        }
        return Integer.MAX_VALUE;
    }

    // Corner case
    if (bucket == K)
    {
        return Integer.MAX_VALUE;
    }

    // If state if already calculated
    // then return its answer
    if (dp[start][bucket] != -1)
    {
        return dp[start][bucket];
    }
    int zeroes = 0;
    int ones = 0;
    int ans = Integer.MAX_VALUE;

    // Start filling zeroes and ones which to be
    // accommodated in jth bucket then ans for
    // current arrangement will be
    // ones*zeroes + recur(i+1, bucket+1)
    for(int i = start; i < N; ++i)
    {
        if (str.charAt(i) == '1')
        {
            ones++;
        }
        else
        {
            zeroes++;
        }
        if (ones * zeroes > ans)
        {
            break;
        }
        int temp = solveUtil(i + 1, bucket + 1, str, K);

        // If this arrangement is not possible then
        // don't calculate further
        if (temp != Integer.MAX_VALUE)
        {
            ans = Math.min(ans, temp + (ones * zeroes));
        }
    }
    return dp[start][bucket] = ans;
}

// Function to initialize the dp and call
// solveUtil() method to get the answer
static int solve(String str, int K)
{
    int N = str.length();
    dp = new int[N][K];

    for(int[] row : dp)
    {
        Arrays.fill(row, -1);
    }

    // Start with 0-th index and 1 bucket
    int ans = solveUtil(0, 0, str, K);
    return ans == Integer.MAX_VALUE ? -1 : ans;
}

// Driver code
public static void main(String[] args)
{
    String S = "0101";

    // K buckets
    int K = 2;

    System.out.println(solve(S, K));
}
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# 2-D dp array saving different states
# dp[i][j] = minimum value of accommodation
# till i'th index of the str1ing
# using j+1 number of buckets.

# Function to find the minimum required
# sum using dynamic programming
def solveUtil(start, bucket, str1, K,dp):

    N = len(str1)

    # If both start and bucket reached end then
    # return 0 else that arrangement is not possible
    # so return INT_MAX
    if (start == N) :
        if (bucket == K):
            return 0
        return 10**9

    # Corner case
    if (bucket == K):
        return 10**9

    # If state if already calculated
    # then return its answer
    if (dp[start][bucket] != -1):
        return dp[start][bucket]

    zeroes = 0
    ones = 0
    ans = 10**9

    # Start filling zeroes and ones which to be accommodated
    # in jth bucket then ans for current arrangement will be
    # ones*zeroes + recur(i+1, bucket+1)
    for i in range(start,N):
        if (str1[i] == '1'):
            ones += 1
        else:
            zeroes += 1

        if (ones * zeroes > ans):
            break

        temp = solveUtil(i + 1, bucket + 1, str1, K,dp)

        # If this arrangement is not possible then
        # don't calculate further
        if (temp != 10**9):
            ans = min(ans, temp + (ones * zeroes))

    dp[start][bucket] = ans

    return ans

# Function to initialize the dp and call
# solveUtil() method to get the answer
def solve(str1, K):

    N = len(str1)

    dp = [[-1 for i in range(K)] for i in range(N)]

    # Start with 0-th index and 1 bucket
    ans = solveUtil(0, 0, str1, K,dp)

    if ans == 10**9:
        return -1
    else:
        return ans

# Driver code

s = "0101"
S=[i for i in s]

# K buckets
K = 2

print(solve(S, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

    // 2-D dp array saving different states
    // dp[i][j] = minimum value of accommodation
    // till i'th index of the string
    // using j+1 number of buckets.
    static int[,] dp;

    // Function to find the minimum required
    // sum using dynamic programming
    static int solveUtil(int start, int bucket,
                         string str, int K)
    {
        int N = str.Length;

        // If both start and bucket reached end
        // then return 0 else that arrangement
        // is not possible so return INT_MAX
        if (start == N)
        {
            if (bucket == K)
            {
                return 0;
            }
            return Int32.MaxValue;
        }

        // Corner case
        if (bucket == K)
        {
            return Int32.MaxValue;
        }

        // If state if already calculated
        // then return its answer
        if (dp[start,bucket] != -1)
        {
            return dp[start, bucket];
        }
        int zeroes = 0;
        int ones = 0;
        int ans = Int32.MaxValue;

        // Start filling zeroes and ones which to be
        // accommodated in jth bucket then ans for
        // current arrangement will be
        // ones*zeroes + recur(i+1, bucket+1)
        for(int i = start; i < N; ++i)
        {
            if (str[i] == '1')
            {
                ones++;
            }
            else
            {
                zeroes++;
            }
            if (ones * zeroes > ans)
            {
                break;
            }
            int temp = solveUtil(i + 1, bucket + 1, str, K);

            // If this arrangement is not possible then
            // don't calculate further
            if (temp != Int32.MaxValue)
            {
                ans = Math.Min(ans, temp + (ones * zeroes));
            }
        }
        return dp[start, bucket] = ans;
    }

    // Function to initialize the dp and call
    // solveUtil() method to get the answer
    static int solve(string str, int K)
    {
        int N = str.Length;
        dp = new int[N, K];       
        for(int i = 0; i < N; i++)
        {
            for(int j = 0; j < K; j++)
            {
                dp[i, j] = -1;
            }
        }

        // Start with 0-th index and 1 bucket
        int ans = solveUtil(0, 0, str, K);
        return ans == Int32.MaxValue ? -1 : ans;
    }

  // Driver code
  static void Main()
  {
    string S = "0101";

    // K buckets
    int K = 2;

    Console.WriteLine(solve(S, K));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// 2-D dp array saving different states
// dp[i][j] = minimum value of accommodation
// till i'th index of the string
// using j+1 number of buckets.
let dp;

// Function to find the minimum required
// sum using dynamic programming
function solveUtil(start, bucket, str, K)
{
    let N = str.length;

    // If both start and bucket reached end
    // then return 0 else that arrangement
    // is not possible so return INT_MAX
    if (start == N)
    {
        if (bucket == K)
        {
            return 0;
        }
        return Number.MAX_VALUE;
    }

    // Corner case
    if (bucket == K)
    {
        return Number.MAX_VALUE;
    }

    // If state if already calculated
    // then return its answer
    if (dp[start][bucket] != -1)
    {
        return dp[start][bucket];
    }
    let zeroes = 0;
    let ones = 0;
    let ans = Number.MAX_VALUE;

    // Start filling zeroes and ones which to be
    // accommodated in jth bucket then ans for
    // current arrangement will be
    // ones*zeroes + recur(i+1, bucket+1)
    for(let i = start; i < N; ++i)
    {
        if (str[i] == '1')
        {
            ones++;
        }
        else
        {
            zeroes++;
        }
        if (ones * zeroes > ans)
        {
            break;
        }
        let temp = solveUtil(i + 1, bucket + 1, str, K);

        // If this arrangement is not possible then
        // don't calculate further
        if (temp != Number.MAX_VALUE)
        {
            ans = Math.min(ans, temp + (ones * zeroes));
        }
    }
    return dp[start][bucket] = ans;
}

// Function to initialize the dp and call
// solveUtil() method to get the answer
function solve(str, K)
{
    let N = str.length;
    dp = new Array(N);
    for(let i = 0; i < N; i++)
    {
        dp[i] = new Array(K);
        for(let j = 0; j < K; j++)
        {
            dp[i][j] = -1;
        }
    }

    // Start with 0-th index and 1 bucket
    let ans = solveUtil(0, 0, str, K);
    return ans == Number.MAX_VALUE ? -1 : ans;
}

// Driver code
let  S = "0101";

// K buckets
let K = 2;

document.write(solve(S, K));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N<sup>3</sup>)
T5】空间复杂度: O(N <sup>2</sup>

这个解决方案仍然没有优化，因为它多次调用同一个状态。因此，现在来看看优化的自下而上动力定位方法。

**自下而上的动态法:**我们先试着思考一下最终状态。这里的变量是桶的数量和字符串的索引。假设 **dp[i][j]是字符串元素 0 到 j-1 和 I 桶的乘积的最小和。**现在要定义我们的转换函数，我们必须从后面开始，考虑每个可能位置 k 的分区。因此，我们的转换函数看起来像:

```
dp [i][j] = for all k = 0 to j min(dp[i][k-1] + numberOfZeroes * numberOfOnes)

for i = 0 (single partition) simple count number of 0's and 1's and do the multiplication. 
And if number of buckets is more than string length till now ans is -1 as we cant fill all 
the available buckets.
```

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum required
// sum using dynamic programming
int solve(string str, int K)
{
    int n = str.length();

    // dp[i][j] = minimum val of accommodation
    // till j'th index of the string
    // using i+1 number of buckets.
    // Final ans will be in dp[n-1][K-1]
    long long dp[K][n];

    // Initialise dp with all states as 0
    memset(dp, 0, sizeof dp);

    // Corner cases
    if (n < K)
        return -1;
    else if (n == K)
        return 0;

    // Filling first row, if only 1 bucket then simple count
    // number of zeros and ones and do the multiplication
    long long zeroes = 0, ones = 0;

    for (int i = 0; i < n; i++) {
        if (str[i] == '0')
            zeroes++;
        else
            ones++;

        dp[0][i] = ones * zeroes;
    }

    for (int s = 1; s < K; s++) {
        for (int i = 0; i < n; i++) {

            dp[s][i] = INT_MAX;

            ones = 0;
            zeroes = 0;
            for (int k = i; k >= 0; k--) {
                if (str[k] == '0')
                    zeroes++;
                else
                    ones++;

                // If k = 0 then this arrangement is not possible
                dp[s][i] = min(dp[s][i],
                               +((k - 1 >= 0)
                                     ? ones * zeroes + dp[s - 1][k - 1]
                                     : INT_MAX));
            }
        }
    }

    // If no arrangement is possible then
    // our answer will remain INT_MAX so return -1
    return (dp[K - 1][n - 1] == INT_MAX) ? -1 : dp[K - 1][n - 1];
}

// Driver code
int main()
{
    string S = "0101";

    // K buckets
    int K = 2;

    cout << solve(S, K) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{
    // Function to find the minimum required
    // sum using dynamic programming
    static long solve(String str, int K)
    {
        int n = str.length();

        // dp[i][j] = minimum val of accommodation
        // till j'th index of the string
        // using i+1 number of buckets.
        // Final ans will be in dp[n-1][K-1]
        long dp[][] = new long[K][n];

        // Corner cases
        if (n < K)
            return -1;
        else if (n == K)
            return 0;

        // Filling first row, if only 1 bucket then simple count
        // number of zeros and ones and do the multiplication
        long zeroes = 0, ones = 0;

        for (int i = 0; i < n; i++)
        {
            if (str.charAt(i) == '0')
                zeroes++;
            else
                ones++;

            dp[0][i] = ones * zeroes;
        }

        for (int s = 1; s < K; s++)
        {
            for (int i = 0; i < n; i++)
            {

                dp[s][i] = Integer.MAX_VALUE;

                ones = 0;
                zeroes = 0;
                for (int k = i; k >= 0; k--)
                {
                    if (str.charAt(k) == '0')
                        zeroes++;
                    else
                        ones++;

                    // If k = 0 then this arrangement is not possible
                    dp[s][i] = Math.min(dp[s][i],
                                +((k - 1 >= 0)
                                        ? ones * zeroes + dp[s - 1][k - 1]
                                        : Integer.MAX_VALUE));
                }
            }
        }

        // If no arrangement is possible then
        // our answer will remain INT_MAX so return -1
        return (dp[K - 1][n - 1] == Integer.MAX_VALUE) ? -1 : dp[K - 1][n - 1];
    }

    // Driver code
    public static void main (String[] args)
    {

        String S = "0101";

        // K buckets
        int K = 2;

        System.out.println(solve(S, K));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function to find the minimum required
# sum using dynamic programming
def solve(Str, K):
    n = len(Str)

    # dp[i][j] = minimum val of accommodation
    # till j'th index of the string
    # using i+1 number of buckets.
    # Final ans will be in dp[n-1][K-1]
    # Initialise dp with all states as 0
    dp = [[0 for i in range(n)] for j in range(K)]

    # Corner cases
    if(n < K):
        return -1
    elif(n == K):
        return 0

    # Filling first row, if only 1 bucket then simple count
    # number of zeros and ones and do the multiplication
    zeroes = 0
    ones = 0

    for i in range(n):
        if(Str[i] == '0'):
            zeroes += 1
        else:
            ones += 1
        dp[0][i] = ones * zeroes

    for s in range(1, K):
        for i in range(n):
            dp[s][i] = sys.maxsize
            ones = 0
            zeroes = 0

            for k in range(i, -1, -1):
                if(Str[k] == '0'):
                    zeroes += 1
                else:
                    ones += 1

                # If k = 0 then this arrangement
                # is not possible
                temp = 0
                if(k - 1 >= 0):
                    temp = ones * zeroes + dp[s - 1][k - 1]
                else:
                    temp = sys.maxsize
                dp[s][i] = min(dp[s][i], temp)

    # If no arrangement is possible then
    # our answer will remain INT_MAX so return -1
    if(dp[K - 1][n - 1] == sys.maxsize):
        return -1
    else:
        return dp[K - 1][n - 1]

# Driver code
S = "0101"

# K buckets
K = 2
print(solve(S, K))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to find the minimum required
    // sum using dynamic programming
    static long solve(string str, int K)
    {
        int n = str.Length;

        // dp[i, j] = minimum val of accommodation
        // till j'th index of the string
        // using i+1 number of buckets.
        // Final ans will be in dp[n-1, K-1]
        long [, ] dp = new long[K, n];

        // Corner cases
        if (n < K)
            return -1;
        else if (n == K)
            return 0;

        // Filling first row, if only 1 bucket then simple count
        // number of zeros and ones and do the multiplication
        long zeroes = 0, ones = 0;

        for (int i = 0; i < n; i++)
        {
            if (str[i] == '0')
                zeroes++;
            else
                ones++;

            dp[0, i] = ones * zeroes;
        }

        for (int s = 1; s < K; s++)
        {
            for (int i = 0; i < n; i++)
            {

                dp[s, i] = Int32.MaxValue;

                ones = 0;
                zeroes = 0;
                for (int k = i; k >= 0; k--)
                {
                    if (str[k] == '0')
                        zeroes++;
                    else
                        ones++;

                    // If k = 0 then this arrangement is not possible
                    dp[s, i] = Math.Min(dp[s, i],
                                +((k - 1 >= 0)
                                        ? ones * zeroes + dp[s - 1, k - 1]
                                        : Int32.MaxValue));
                }
            }
        }

        // If no arrangement is possible then
        // our answer will remain INT_MAX so return -1
        return (dp[K - 1, n - 1] == Int32.MaxValue) ? -1 : dp[K - 1, n - 1];
    }

    // Driver code
    public static void Main (string[] args)
    {

        string S = "0101";

        // K buckets
        int K = 2;

        Console.WriteLine(solve(S, K));

    }

}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function to find the minimum required
    // sum using dynamic programming
    function solve(str,K)
    {
        let n = str.length;

        // dp[i][j] = minimum val of accommodation
        // till j'th index of the string
        // using i+1 number of buckets.
        // Final ans will be in dp[n-1][K-1]
        let dp = new Array(K);
        for(let i=0;i<K;i++)
        {
            dp[i]=new Array(n);
            for(let j=0;j<n;j++)
            {
                dp[i][j]=0;
            }
        }

        // Corner cases
        if (n < K)
            return -1;
        else if (n == K)
            return 0;

        // Filling first row, if only 1 bucket then simple count
        // number of zeros and ones and do the multiplication
        let zeroes = 0, ones = 0;

        for (let i = 0; i < n; i++)
        {
            if (str[i] == '0')
                zeroes++;
            else
                ones++;

            dp[0][i] = ones * zeroes;
        }

        for (let s = 1; s < K; s++)
        {
            for (let i = 0; i < n; i++)
            {

                dp[s][i] = Number.MAX_VALUE;

                ones = 0;
                zeroes = 0;
                for (let k = i; k >= 0; k--)
                {
                    if (str[k] == '0')
                        zeroes++;
                    else
                        ones++;

                    // If k = 0 then this
                    // arrangement is not possible
                    dp[s][i] = Math.min(dp[s][i],
                                +((k - 1 >= 0)
                          ? ones * zeroes + dp[s - 1][k - 1]
                                        : Number.MAX_VALUE));
                }
            }
        }

        // If no arrangement is possible then
        // our answer will remain INT_MAX so return -1
        return (dp[K - 1][n - 1] == Number.MAX_VALUE) ?
        -1 : dp[K - 1][n - 1];
    }

    // Driver code
    let S = "0101";
    // K buckets
    let K = 2;

    document.write(solve(S, K));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N<sup>3</sup>)
T5】空间复杂度: O(N <sup>2</sup> )