# 所有分区的元素之和，所有元素都不小于 K

> 原文:[https://www . geeksforgeeks . org/所有分区的元素总和-数量-无元素小于-k/](https://www.geeksforgeeks.org/sum-of-elements-of-all-partitions-of-number-such-that-no-element-is-less-than-k/)

给定一个整数 N，任务是找到这个数的所有整数分区的总和，使得每个分区不包含任何小于 k 的整数
**示例:**

> **输入:** N = 6，K = 2
> **输出:** 24
> 在这种情况下，有 4 个有效分区。
> 1) {6}
> 2) {4，2}
> 3) {3，3}
> 4) {2，2，2}
> 因此，总和应为
> 6+4+2+3+3+2+2+2 = 24
> **输入:** N = 10 和 K = 3
> **输出:** 50
> 这里，5 个有效分区为:
> 1 4}
> 在这种情况下，总和为
> 10+7+3+6+4+5+5+3+3+4 = 50

**逼近:**这个问题有一个简单的**递归**解。首先，我们需要计算 N 个数的有效分区的总数，使得每个分区包含大于或等于 K 的整数。因此，我们将迭代地应用我们的递归解决方案来寻找具有最小整数 K，K+1，K+2，…，N 的有效分区。
我们的最终答案将是 **N *有效分区数**，因为每个有效分区的和等于 N。
以下是设计递归函数来寻找有效分区总数的一些关键思想。

*   如果 **N < K** 那么分区是不可能的。
*   如果 **N < 2*K** 那么只有一个分区是可能的，那就是数字 N 本身。
*   我们可以用递归的方式找到包含至少等于‘I’的整数的分区数(‘I’可以是从 K 到 N)，然后将它们全部相加得到最终答案。

**递归函数寻找有效分区数的伪代码:**

```
f(N,K):
       if N < K
           return 0
       if N < 2K
           return 1
       Initialize answer = 1
       FOR i from K to N
           answer = answer + f(N-i,i)
return answer 
```

下面是**动态规划解:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns total number of valid
// partitions of integer N
long long int countPartitions(int n, int k)
{

    // Global declaration of 2D dp array
    // which will be later used for memoization
    long long int dp[201][201];

    // initializing 2D dp array with -1
    // we will use this 2D array for memoization
    for (int i = 0; i < n + 1; i++) {
        for (int j = 0; j < n + 1; j++) {
            dp[i][j] = -1;
        }
    }

    // if this subproblem is already previously
    // calculated, then directly return that answer
    if (dp[n][k] >= 0)
        return dp[n][k];

    // if N < K, then no valid
    // partition is possible
    if (n < k)
        return 0;

    // if N is between K to 2*K then
    // there is only one
    // partition and that is the number N itself
    if (n < 2 * k)
        return 1;

    // Initialize answer with 1 as
    // the number N itself
    // is always a valid partition
    long long int answer = 1;

    // for loop to iterate over K to N
    // and find number of
    // possible valid partitions recursively.
    for (int i = k; i < n; i++)
        answer = answer + countPartitions(n - i, i);

    // memoization is done by storing
    // this calculated answer
    dp[n][k] = answer;

    // returning number of valid partitions
    return answer;
}

// Driver code
int main()
{
    int n = 10, k = 3;

    // Printing total number of valid partitions
    cout << "Total Aggregate sum of all Valid Partitions: "
         << countPartitions(n, k) * n;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// above approach
class GFG
{
// Function that returns
// total number of valid
// partitions of integer N
static long countPartitions(int n, int k)
{

    // Global declaration of 2D
    // dp array which will be
    // later used for memoization
    long[][] dp = new long[201][201];

    // initializing 2D dp array
    // with -1 we will use this
    // 2D array for memoization
    for (int i = 0; i < n + 1; i++)
    {
        for (int j = 0; j < n + 1; j++)
        {
            dp[i][j] = -1;
        }
    }

    // if this subproblem is already
    // previously calculated, then
    // directly return that answer
    if (dp[n][k] >= 0)
        return dp[n][k];

    // if N < K, then no valid
    // partition is possible
    if (n < k)
        return 0;

    // if N is between K to 2*K
    // then there is only one
    // partition and that is
    // the number N itself
    if (n < 2 * k)
        return 1;

    // Initialize answer with 1
    // as the number N itself
    // is always a valid partition
    long answer = 1;

    // for loop to iterate over
    // K to N and find number of
    // possible valid partitions
    // recursively.
    for (int i = k; i < n; i++)
        answer = answer +
                 countPartitions(n - i, i);

    // memoization is done by storing
    // this calculated answer
    dp[n][k] = answer;

    // returning number of
    // valid partitions
    return answer;
}

// Driver code
public static void main(String[] args)
{
    int n = 10, k = 3;

    // Printing total number
    // of valid partitions
    System.out.println("Total Aggregate sum of " +
                       "all Valid Partitions: " +
                       countPartitions(n, k) * n);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function that returns total number of valid
# partitions of integer N
def countPartitions(n, k):

    # Global declaration of 2D dp array
    # which will be later used for memoization
    dp = [[0] * 201] * 201

    # Initializing 2D dp array with -1
    # we will use this 2D array for memoization
    for i in range(n + 1):
        for j in range(n + 1):
            dp[i][j] = -1

    # If this subproblem is already previously
    # calculated, then directly return that answer
    if (dp[n][k] >= 0):
        return dp[n][k]

    # If N < K, then no valid
    # partition is possible
    if (n < k) :
        return 0

    # If N is between K to 2*K then
    # there is only one partition
    # and that is the number N itself
    if (n < 2 * k):
        return 1

    # Initialize answer with 1 as
    # the number N itself
    # is always a valid partition
    answer = 1

    # For loop to iterate over K to N
    # and find number of possible valid
    # partitions recursively.
    for i in range(k, n):
        answer = (answer +
                  countPartitions(n - i, i))

    # Memoization is done by storing
    # this calculated answer
    dp[n][k] = answer

    # Returning number of valid partitions
    return answer

# Driver code
n = 10
k = 3

# Printing total number of valid partitions
print("Total Aggregate sum of all "
      "Valid Partitions: ",
      countPartitions(n, k) * n)

# This code is contributed by sanjoy_62
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
    // Function that returns total number of valid
    // partitions of integer N
    public static long countPartitions(int n, int k)
    {

        // Global declaration of 2D dp array
        // which will be later used for memoization
        long[,] dp = new long[201,201];

        // initializing 2D dp array with -1
        // we will use this 2D array for memoization
        for (int i = 0; i < n + 1; i++) {
            for (int j = 0; j < n + 1; j++) {
                dp[i,j] = -1;
            }
        }

        // if this subproblem is already previously
        // calculated, then directly return that answer
        if (dp[n,k] >= 0)
            return dp[n,k];

        // if N < K, then no valid 
        // partition is possible
        if (n < k)
            return 0;

        // if N is between K to 2*K then
        // there is only one
        // partition and that is the number N itself
        if (n < 2 * k)
            return 1;

        // Initialize answer with 1 as 
        // the number N itself
        // is always a valid partition
        long answer = 1;

        // for loop to iterate over K to N
        // and find number of
        // possible valid partitions recursively.
        for (int i = k; i < n; i++)
            answer = answer + countPartitions(n - i, i);

        // memoization is done by storing
        // this calculated answer
        dp[n,k] = answer;

        // returning number of valid partitions
        return answer;
    }

    // Driver code 
    static void Main()
    {
        int n = 10, k = 3;

        // Printing total number of valid partitions
        Console.Write("Total Aggregate sum of all Valid Partitions: " + countPartitions(n, k) * n);
    }
    //This code is contributed by DrRoot_
}
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    // Function that returns
    // total number of valid
    // partitions of integer N
    function countPartitions(n, k)
    {

        // Global declaration of 2D
        // dp array which will be
        // later used for memoization
        let dp = new Array(201);

        // initializing 2D dp array
        // with -1 we will use this
        // 2D array for memoization
        for (let i = 0; i < n + 1; i++)
        {
            dp[i] = new Array(201);
            for (let j = 0; j < n + 1; j++)
            {
                dp[i][j] = -1;
            }
        }

        // if this subproblem is already
        // previously calculated, then
        // directly return that answer
        if (dp[n][k] >= 0)
            return dp[n][k];

        // if N < K, then no valid
        // partition is possible
        if (n < k)
            return 0;

        // if N is between K to 2*K
        // then there is only one
        // partition and that is
        // the number N itself
        if (n < 2 * k)
            return 1;

        // Initialize answer with 1
        // as the number N itself
        // is always a valid partition
        let answer = 1;

        // for loop to iterate over
        // K to N and find number of
        // possible valid partitions
        // recursively.
        for (let i = k; i < n; i++)
            answer = answer + countPartitions(n - i, i);

        // memoization is done by storing
        // this calculated answer
        dp[n][k] = answer;

        // returning number of
        // valid partitions
        return answer;
    }

    let n = 10, k = 3;

    // Printing total number
    // of valid partitions
    document.write("Total Aggregate sum of " +
                       "all Valid Partitions: " +
                       countPartitions(n, k) * n);

// This code is contributed by rameshtravel07.
</script>
```

**Output:** 

```
Total Aggregate sum of all Valid Partitions: 50
```

**时间复杂度:** O(N <sup>2</sup> )