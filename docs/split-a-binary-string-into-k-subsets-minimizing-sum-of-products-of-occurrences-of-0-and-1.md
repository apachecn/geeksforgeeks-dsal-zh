# 将二进制串分割成 K 个子集，最小化 0 和 1 的乘积之和

> 原文:[https://www . geeksforgeeks . org/split-a-binary-string-in-k-subset-最小化-0 和-1 的乘积和/](https://www.geeksforgeeks.org/split-a-binary-string-into-k-subsets-minimizing-sum-of-products-of-occurrences-of-0-and-1/)

给定一个二进制字符串 **S** ，任务是将序列划分为 **K** 个非空子集，使得所有子集的 **0** 和 **1** 的乘积之和最小。如果不可能打印-1。
**举例:**

> **输入:** S = "0001 "，K = 2
> **输出:** 0
> **解释**
> 我们有 3 个选择{0，001}、{00，01}、{000，1}
> 各自的乘积之和为{1*0 + 2*1 = 2}、{2*0 + 1*1 = 1}、{3*0 + 0*1 = 0}。
> **输入:**S =“1011000110110100”，K = 5
> **输出:** 8
> **说明:**子集{10，11，000，11011，0100}将乘积{ 1*1 + 0*2 + 3*0 + 1*4 + 3*1 = 8 }的和最小化。

**方法:**为了解决这个问题，我们采用了自下而上的[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)。

*   我们计算所有子集的乘积的最小和，然后，对于每个子集，我们使用这个值来计算该子集所有大小的乘积的最小和。
*   对于从索引 **i** 开始到索引 **j** 结束的子集，该值将是最小的**DP[I-1]+(count _ zero * count _ one)**，其中 **count_zero** 和 **count_one** 分别是 **0** 和 **1** 在 **i** 和 **j** 之间的出现。
*   对于每个指数 **j** ，我们在所有可能的值中找到最小值 **i** 。
*   返回**DP[N–1]**获得最终答案。

下面的代码是上述方法的实现:

## C++

```
// C++ Program to split a given string
// into K segments such that the sum
// of product of occurence of
// characters in them is minimized

#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// sum of products of occurences
// of 0 and 1 in each segments
int minSumProd(string S, int K)
{
    // Store the length of
    // the string
    int len = S.length();

    // Not possible to
    // generate subsets
    // greater than the
    // length of string
    if (K > len)
        return -1;

    // If the number of subsets
    // equals the length
    if (K == len)
        return 0;

    vector<int> dp(len);
    int count_zero = 0, count_one = 0;

    // Precompute the sum of
    // products for all index
    for (int j = 0; j < len; j++) {

        (S[j] == '0')
            ? count_zero++
            : count_one++;
        dp[j] = count_zero * count_one;
    }

    // Calculate the minimum sum of
    // products for K subsets
    for (int i = 1; i < K; i++) {

        for (int j = len; j >= i; j--) {

            count_zero = 0, count_one = 0;
            dp[j] = INT_MAX;

            for (int k = j; k >= i; k--) {

                (S[k] == '0') ? count_zero++
                              : count_one++;
                dp[j]
                    = min(
                        dp[j],
                        count_zero * count_one
                            + dp[k - 1]);
            }
        }
    }

    return dp[len - 1];
}

// Driver code
int main()
{
    string S = "1011000110110100";
    int K = 5;
    cout << minSumProd(S, K) << '\n';
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to split a given String
// into K segments such that the sum
// of product of occurence of
// characters in them is minimized
import java.util.*;

class GFG{

// Function to return the minimum
// sum of products of occurences
// of 0 and 1 in each segments
static int minSumProd(String S, int K)
{
    // Store the length of
    // the String
    int len = S.length();

    // Not possible to
    // generate subsets
    // greater than the
    // length of String
    if (K > len)
        return -1;

    // If the number of subsets
    // equals the length
    if (K == len)
        return 0;

    int []dp = new int[len];
    int count_zero = 0, count_one = 0;

    // Precompute the sum of
    // products for all index
    for (int j = 0; j < len; j++)
    {
        if(S.charAt(j) == '0')
            count_zero++;
        else
            count_one++;
        dp[j] = count_zero * count_one;
    }

    // Calculate the minimum sum of
    // products for K subsets
    for (int i = 1; i < K; i++)
    {
        for (int j = len-1; j >= i; j--)
        {
            count_zero = 0;
            count_one = 0;
            dp[j] = Integer.MAX_VALUE;

            for (int k = j; k >= i; k--)
            {
                if(S.charAt(k) == '0')
                    count_zero++;
                else
                    count_one++;
                dp[j] = Math.min(dp[j], count_zero *
                                        count_one +
                                        dp[k - 1]);
            }
        }
    }

    return dp[len - 1];
}

// Driver code
public static void main(String[] args)
{
    String S = "1011000110110100";
    int K = 5;
    System.out.print(minSumProd(S, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to split a given String
# into K segments such that the sum
# of product of occurence of
# characters in them is minimized
import sys

# Function to return the minimum
# sum of products of occurences
# of 0 and 1 in each segments
def minSumProd(S, K):

    # Store the length of
    # the String
    Len = len(S);

    # Not possible to
    # generate subsets
    # greater than the
    # length of String
    if (K > Len):
        return -1;

    # If the number of subsets
    # equals the length
    if (K == Len):
        return 0;

    dp = [0] * Len;
    count_zero = 0;
    count_one = 0;

    # Precompute the sum of
    # products for all index
    for j in range(0, Len, 1):
        if (S[j] == '0'):
            count_zero += 1;
        else:
            count_one += 1;
        dp[j] = count_zero * count_one;

    # Calculate the minimum sum of
    # products for K subsets
    for i in range(1, K):
        for j in range(Len - 1, i - 1, -1):
            count_zero = 0;
            count_one = 0;
            dp[j] = sys.maxsize;

            for k in range(j, i - 1, -1):
                if (S[k] == '0'):
                    count_zero += 1;
                else:
                    count_one += 1;

                dp[j] = min(dp[j], count_zero *
                                   count_one +
                                   dp[k - 1]);
    return dp[Len - 1];

# Driver code
if __name__ == '__main__':

    S = "1011000110110100";
    K = 5;

    print(minSumProd(S, K));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to split a given String
// into K segments such that the sum
// of product of occurence of
// characters in them is minimized
using System;

class GFG{

// Function to return the minimum
// sum of products of occurences
// of 0 and 1 in each segments
static int minSumProd(string S, int K)
{

    // Store the length of
    // the String
    int len = S.Length;

    // Not possible to
    // generate subsets
    // greater than the
    // length of String
    if (K > len)
        return -1;

    // If the number of subsets
    // equals the length
    if (K == len)
        return 0;

    int []dp = new int[len];
    int count_zero = 0, count_one = 0;

    // Precompute the sum of
    // products for all index
    for(int j = 0; j < len; j++)
    {
       if(S[j] == '0')
       {
           count_zero++;
       }
       else
       {
           count_one++;
       }
       dp[j] = count_zero * count_one;
    }

    // Calculate the minimum sum
    // of products for K subsets
    for(int i = 1; i < K; i++)
    {
       for(int j = len - 1; j >= i; j--)
       {
          count_zero = 0;
          count_one = 0;
          dp[j] = Int32.MaxValue;

          for(int k = j; k >= i; k--)
          {
             if(S[k] == '0')
             {
                 count_zero++;
             }
             else
             {
                 count_one++;
             }
             dp[j] = Math.Min(dp[j], count_zero *
                                      count_one +
                                      dp[k - 1]);
          }
       }
    }
    return dp[len - 1];
}

// Driver code
public static void Main(string[] args)
{
    string S = "1011000110110100";
    int K = 5;

    Console.Write(minSumProd(S, K));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript Program to split a given string
// into K segments such that the sum
// of product of occurence of
// characters in them is minimized

// Function to return the minimum
// sum of products of occurences
// of 0 and 1 in each segments
function minSumProd(S, K) {
    // Store the length of
    // the string
    let len = S.length;

    // Not possible to
    // generate subsets
    // greater than the
    // length of string
    if (K > len)
        return -1;

    // If the number of subsets
    // equals the length
    if (K == len)
        return 0;

    let dp = new Array(len);
    let count_zero = 0, count_one = 0;

    // Precompute the sum of
    // products for all index
    for (let j = 0; j < len; j++) {

        (S[j] == '0')
            ? count_zero++
            : count_one++;
        dp[j] = count_zero * count_one;
    }

    // Calculate the minimum sum of
    // products for K subsets
    for (let i = 1; i < K; i++) {

        for (let j = len; j >= i; j--) {

            count_zero = 0, count_one = 0;
            dp[j] = Number.MAX_SAFE_INTEGER;

            for (let k = j; k >= i; k--) {

                (S[k] == '0') ? count_zero++
                    : count_one++;
                dp[j]
                    = Math.min(
                        dp[j],
                        count_zero * count_one
                        + dp[k - 1]);
            }
        }
    }

    return dp[len - 1];
}

// Driver code
let S = "1011000110110100";
let K = 5;
document.write(minSumProd(S, K));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
8
```

**时间复杂度:***O(K * N * N)*
T5】辅助空间复杂度: *O(N)*