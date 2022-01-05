# 统计位数不超过前两位绝对差值的 N 位数

> 原文:[https://www . geesforgeks . org/count-n 位数-其位数不超过前两位数的绝对差值/](https://www.geeksforgeeks.org/count-n-digit-numbers-whose-digits-does-not-exceed-absolute-difference-of-the-two-previous-digits/)

给定一个整数 **N** ，任务是计算 **N 位数字**的个数，使得除了第一个和第二个数字外，每个数字都小于或等于前两个数字的绝对差值。

**示例:**

> **输入:** N = 1
> **输出:** 10
> **说明:**从[0–9]开始的所有数字都有效，因为位数是 1。
> 
> **输入:**N = 3
> T3】输出: 375

**天真方法:**最简单的方法是迭代所有可能的 **N** 位数字，对于每个这样的数字，检查其所有数字是否满足上述条件。

***时间复杂度:**O(10<sup>N</sup>* N)*
***辅助空间:** O(1)*

**有效方法:**在有效方法中，构造所有可能的数字，而不是在一系列数字上验证条件。这可以在[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的帮助下实现，因为它有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。子问题可以使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)存储在 **dp[][][]表**中，其中**DP[数字][prev1][prev2]** 存储从**数字-第**位置直到结束的答案，当选择前一个数字时，是 **prev1** ，选择的第二个最前面的数字是 **prev2。**

按照以下步骤解决问题:

*   通过执行以下步骤，定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **数字(数字，prev1，prev2)** 。
    *   检查[基本情况](https://www.geeksforgeeks.org/recursion/)。如果**数字**的值等于 **N+1** ，则**返回 1** 作为有效的 **N 位数**。
    *   如果状态**DP[数字][prev1][prev2]** 的结果已经计算出来，则返回该状态**DP[数字][prev1][prev2** 】。
    *   如果当前**位**为 **1** ，则可以放置**【1-9】**中的任意一位。如果 **N=1** ，那么 **0** 也可以放置。
    *   如果当前**位**为 **2** ，则可以放置**【0-9】**中的任意一位。
    *   否则**【0-(ABS(prev 1-prev 2))】**中的任意数字都可以放在当前位置。
    *   进行有效放置后，**递归调用**计数**函数，获取索引**数字+1** 。**
    *   返回所有可能的有效数字位置的总和作为答案。

以下是上述方法的代码:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

long long dp[50][10][10];

// Function to count N digit numbers whose
// digits are less than or equal to the
// absolute difference of previous two digits
long long countOfNumbers(int digit, int prev1,
                         int prev2, int N)
{
    // If all digits are traversed
    if (digit == N + 1)
        return 1;

    // If the state has already been computed
    if (dp[digit][prev1][prev2] != -1)
        return dp[digit][prev1][prev2];

    dp[digit][prev1][prev2] = 0;

    // If the current digit is 1,
    // any digit from [1-9] can be placed.
    // If N==1, 0 can also be placed.
    if (digit == 1) {
        for (int j = (N == 1 ? 0 : 1);
             j <= 9; ++j) {

            dp[digit][prev1][prev2]
                += countOfNumbers(digit + 1,
                                  j, prev1, N);
        }
    }

    // If the current digit is 2, any
    // digit from [0-9] can be placed
    else if (digit == 2) {
        for (int j = 0; j <= 9; ++j) {

            dp[digit][prev1][prev2]
                += countOfNumbers(
                    digit + 1, j, prev1, N);
        }
    }

    // For other digits, any digit
    // from 0 to abs(prev1 - prev2) can be placed
    else {
        for (int j = 0; j <= abs(prev1 - prev2); ++j) {

            dp[digit][prev1][prev2]
                += countOfNumbers(digit + 1, j, prev1, N);
        }
    }

    // Return the answer
    return dp[digit][prev1][prev2];
}

// Driver code
int main()
{
    // Initializing dp array with -1.
    memset(dp, -1, sizeof dp);

    // Input
    int N = 3;

    // Function call
    cout << countOfNumbers(1, 0, 0, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int dp[][][] = new int[50][10][10];

static void initialize()
{
    for(int i = 0; i < 50; i++)
    {
        for(int j = 0; j < 10; j++)
        {
            for(int k = 0; k < 10; k++)
            {
                dp[i][j][k] = -1;
            }
        }
    }
}

// Function to count N digit numbers whose
// digits are less than or equal to the
// absolute difference of previous two digits
static int countOfNumbers(int digit, int prev1,
                          int prev2, int N)
{

    // If all digits are traversed
    if (digit == N + 1)
        return 1;

    // If the state has already been computed
    if (dp[digit][prev1][prev2] != -1)
        return dp[digit][prev1][prev2];

    dp[digit][prev1][prev2] = 0;

    // If the current digit is 1,
    // any digit from [1-9] can be placed.
    // If N==1, 0 can also be placed.
    if (digit == 1)
    {
        for(int j = (N == 1 ? 0 : 1);
                j <= 9; ++j)
        {
            dp[digit][prev1][prev2] += countOfNumbers(
                digit + 1, j, prev1, N);
        }
    }

    // If the current digit is 2, any
    // digit from [0-9] can be placed
    else if (digit == 2)
    {
        for(int j = 0; j <= 9; ++j)
        {
            dp[digit][prev1][prev2] += countOfNumbers(
                    digit + 1, j, prev1, N);
        }
    }

    // For other digits, any digit
    // from 0 to abs(prev1 - prev2) can be placed
    else
    {
        for(int j = 0; j <= Math.abs(prev1 - prev2); ++j)
        {
            dp[digit][prev1][prev2] += countOfNumbers(
                digit + 1, j, prev1, N);
        }
    }

    // Return the answer
    return dp[digit][prev1][prev2];
}

// Driver Code
public static void main(String[] args)
{
    initialize();

    // Input
    int N = 3;

    // Function call
    System.out.print(countOfNumbers(1, 0, 0, N));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach
dp = [[[-1 for i in range(10)]
           for j in range(10)]
           for k in range(50)]

# Function to count N digit numbers whose
# digits are less than or equal to the
# absolute difference of previous two digits
def countOfNumbers(digit, prev1, prev2, N):

    # If all digits are traversed
    if (digit == N + 1):
        return 1

    # If the state has already been computed
    if (dp[digit][prev1][prev2] != -1):
        return dp[digit][prev1][prev2]

    dp[digit][prev1][prev2] = 0

    # If the current digit is 1,
    # any digit from [1-9] can be placed.
    # If N==1, 0 can also be placed.
    if (digit == 1):
        term = 0 if N == 1 else 1

        for j in range(term, 10, 1):
            dp[digit][prev1][prev2] += countOfNumbers(
                digit + 1, j, prev1, N)

    # If the current digit is 2, any
    # digit from [0-9] can be placed
    elif (digit == 2):
        for j in range(10):
            dp[digit][prev1][prev2] += countOfNumbers(
                digit + 1, j, prev1, N)

    # For other digits, any digit
    # from 0 to abs(prev1 - prev2) can be placed
    else:
        for j in range(abs(prev1 - prev2) + 1):
            dp[digit][prev1][prev2] += countOfNumbers(
                digit + 1, j, prev1, N)

    # Return the answer
    return dp[digit][prev1][prev2]

# Driver code
if __name__ == '__main__':

    # Input
    N = 3

    # Function call
    print(countOfNumbers(1, 0, 0, N))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int [,,]dp = new int[50, 10, 10];

static void initialize()
{
    for(int i = 0; i < 50; i++)
    {
        for(int j = 0; j < 10; j++)
        {
            for(int k = 0; k < 10; k++)
            {
                dp[i, j, k] = -1;
            }
        }
    }
}

// Function to count N digit numbers whose
// digits are less than or equal to the
// absolute difference of previous two digits
static int countOfNumbers(int digit, int prev1,
                          int prev2, int N)
{

    // If all digits are traversed
    if (digit == N + 1)
        return 1;

    // If the state has already been computed
    if (dp[digit, prev1, prev2] != -1)
        return dp[digit, prev1, prev2];

    dp[digit, prev1, prev2] = 0;

    // If the current digit is 1,
    // any digit from [1-9] can be placed.
    // If N==1, 0 can also be placed.
    if (digit == 1)
    {
        for(int j = (N == 1 ? 0 : 1);
                j <= 9; ++j)
        {
            dp[digit, prev1, prev2] += countOfNumbers(
                              digit + 1, j, prev1, N);
        }
    }

    // If the current digit is 2, any
    // digit from [0-9] can be placed
    else if (digit == 2)
    {
        for(int j = 0; j <= 9; ++j)
        {
            dp[digit, prev1, prev2] += countOfNumbers(
                              digit + 1, j, prev1, N);
        }
    }

    // For other digits, any digit
    // from 0 to abs(prev1 - prev2)
    // can be placed
    else
    {
        for(int j = 0; j <= Math.Abs(prev1 - prev2); ++j)
        {
            dp[digit, prev1, prev2] += countOfNumbers(
                              digit + 1, j, prev1, N);
        }
    }

    // Return the answer
    return dp[digit, prev1, prev2];
}

// Driver code
public static void Main()
{
    initialize();

    // Input
    int N = 3;

    // Function call
    Console.Write(countOfNumbers(1, 0, 0, N));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

var dp = Array.from(Array(50), ()=>Array(10));
for(var i =0; i<10; i++)
        for(var j =0; j<10; j++)
            dp[i][j] = new Array(10).fill(-1);

// Function to count N digit numbers whose
// digits are less than or equal to the
// absolute difference of previous two digits
function countOfNumbers(digit, prev1, prev2, N)
{
    // If all digits are traversed
    if (digit == N + 1)
        return 1;

    // If the state has already been computed
    if (dp[digit][prev1][prev2] != -1)
        return dp[digit][prev1][prev2];

    dp[digit][prev1][prev2] = 0;

    // If the current digit is 1,
    // any digit from [1-9] can be placed.
    // If N==1, 0 can also be placed.
    if (digit == 1) {
        for (var j = (N == 1 ? 0 : 1);
             j <= 9; ++j) {

            dp[digit][prev1][prev2]
                += countOfNumbers(digit + 1,
                                  j, prev1, N);
        }
    }

    // If the current digit is 2, any
    // digit from [0-9] can be placed
    else if (digit == 2) {
        for (var j = 0; j <= 9; ++j) {

            dp[digit][prev1][prev2]
                += countOfNumbers(
                    digit + 1, j, prev1, N);
        }
    }

    // For other digits, any digit
    // from 0 to abs(prev1 - prev2) can be placed
    else {
        for (var j = 0; j <= Math.abs(prev1 - prev2); ++j) {

            dp[digit][prev1][prev2]
                += countOfNumbers(digit + 1, j, prev1, N);
        }
    }

    // Return the answer
    return dp[digit][prev1][prev2];
}

// Driver code

// Input
var N = 3;

// Function call
document.write( countOfNumbers(1, 0, 0, N));

</script>
```

**Output:** 

```
375
```

***时间复杂度:**O(N * 10<sup>3</sup>)*
***辅助空间:**O(N * 10<sup>2</sup>)*