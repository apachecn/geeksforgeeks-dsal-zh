# 计算相邻数字相等的 N 位数

> 原文:[https://www . geesforgeks . org/count-n-digits-numbers-其相邻数字具有相等的-gcd/](https://www.geeksforgeeks.org/count-n-digit-numbers-whose-adjacent-digits-have-equal-gcd/)

给定一个正整数 **N** ，任务是找出所有相邻数字相等的 **N** 位数[最大公约数(GCD)](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。

**示例:**

> **输入:** N = 2
> **输出:** 90
> **说明:**
> 所有 2 位数都满足条件，因为只有一对数字，有 90 个 2 位数。
> 
> **输入:**N = 3
> T3】输出: 457

**天真方法:**解决给定问题最简单的方法是[生成所有可能的 **N** 位数字](https://www.geeksforgeeks.org/find-possible-words-phone-digits/)并计算相邻数字相等的那些数字 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。检查所有数字后，打印**计数的值**作为数字的总计数。

***时间复杂度:**O(N * 10<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化，因为上述问题有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和一个[最优子结构](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。子问题可以存储在 **dp[][][]表** [记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)中，其中 **dp[index][prev][gcd]** 存储从 **index <sup>th</sup>** 位置到结束的答案，其中 **prev** 用于存储数字的前一位数字， **gcd** 是数字中现有相邻数字之间的 gcd。按照以下步骤解决问题:

*   初始化一个全局多维数组 **dp[100][10][10]** ，所有值为 **-1** ，存储每次递归调用的结果。
*   定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)，比如**数(索引，prev，gcd，N)** ，并执行以下步骤:
    *   如果**索引**的值为 **(N + 1)** ，则返回 **1** 作为已经形成的有效 **N** 位数。
    *   如果状态**DP[索引][prev][gcd]** 的结果已经计算出来，则返回该值**DP[索引][prev][gcd]** 。
    *   如果当前**索引**为 **1** ，则可以放置**【1-9】**中的任意数字。
    *   如果当前**索引**大于 **1** ，则可以放置**【0-9】**中的任意数字。
    *   如果索引大于 **2** ，如果当前数字和前一个数字的 gcd 等于已经存在的相邻数字的 GCD，则可以放置一个数字。
    *   对数字进行有效放置后，**递归调用**(索引+ 1)** 的**计数**函数。**
    *   返回所有可能的有效数字位置的总和作为答案。
*   打印函数**返回的数值作为结果。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int dp[100][10][10];

// Recursive function to find the count
// of all the N-digit numbers whose
// adjacent digits having equal GCD
int countOfNumbers(int index, int prev,
                   int gcd, int N)
{
    // If index is N+1
    if (index == N + 1)
        return 1;

    int& val = dp[index][prev][gcd];

    // If the state has already
    // been computed
    if (val != -1)
        return val;

    // Stores the total count of all
    // N-digit numbers
    val = 0;

    // If index = 1, any digit from
    // [1-9] can be placed.

    // If N = 0, 0 can be placed as well
    if (index == 1) {

        for (int digit = (N == 1 ? 0 : 1);
             digit <= 9;
             ++digit) {

            // Update the value val
            val += countOfNumbers(
                index + 1,
                digit, gcd, N);
        }
    }

    // If index is 2, then any digit
    // from [0-9] can be placed
    else if (index == 2) {

        for (int digit = 0;
             digit <= 9; ++digit) {
            val += countOfNumbers(
                index + 1, digit,
                __gcd(prev, digit), N);
        }
    }

    // Otherwise any digit from [0-9] can
    // be placed if the GCD of current
    // and previous digit is gcd
    else {

        for (int digit = 0;
             digit <= 9; ++digit) {

            // Check if GCD of current
            // and previous digit is gcd
            if (__gcd(digit, prev) == gcd) {
                val += countOfNumbers(
                    index + 1, digit, gcd, N);
            }
        }
    }

    // Return the total count
    return val;
}

// Function to find the count of all
// the N-digit numbers whose adjacent
// digits having equal GCD
int countNumbers(int N)
{
    // Initialize dp array with -1
    memset(dp, -1, sizeof dp);

    // Function Call to find the
    // resultant count
    return countOfNumbers(1, 0, 0, N);
}

// Driver Code
int main()
{
    int N = 2;
    cout << countNumbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{
static int[][][] dp = new int[100][10][10];

static int _gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0)
          return b;
        if (b == 0)
          return a;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return _gcd(a-b, b);
        return _gcd(a, b-a);
    }

// Recursive function to find the count
// of all the N-digit numbers whose
// adjacent digits having equal GCD
static int countOfNumbers(int index, int prev,
                   int gcd, int N)
{
    // If index is N+1
    if (index == N + 1)
        return 1;

    int val = dp[index][prev][gcd];

    // If the state has already
    // been computed
    if (val != -1)
        return val;

    // Stores the total count of all
    // N-digit numbers
    val = 0;

    // If index = 1, any digit from
    // [1-9] can be placed.

    // If N = 0, 0 can be placed as well
    if (index == 1) {

        for (int digit = (N == 1 ? 0 : 1);
             digit <= 9;
             ++digit) {

            // Update the value val
            val += countOfNumbers(
                index + 1,
                digit, gcd, N);
        }
    }

    // If index is 2, then any digit
    // from [0-9] can be placed
    else if (index == 2) {

        for (int digit = 0;
             digit <= 9; ++digit) {
            val += countOfNumbers(
                index + 1, digit,
                _gcd(prev, digit), N);
        }
    }

    // Otherwise any digit from [0-9] can
    // be placed if the GCD of current
    // and previous digit is gcd
    else {

        for (int digit = 0;
             digit <= 9; ++digit) {

            // Check if GCD of current
            // and previous digit is gcd
            if (_gcd(digit, prev) == gcd) {
                val += countOfNumbers(
                    index + 1, digit, gcd, N);
            }
        }
    }

    // Return the total count
    return val;
}

// Function to find the count of all
// the N-digit numbers whose adjacent
// digits having equal GCD
static int countNumbers(int N)
{
    int i, j, k;

    // Initialize dp array with -1
    for(i = 0; i < 100; i++)
    {
        for(j = 0; j < 10; j++)
        {
            for(k = 0; k < 10; k++)
            {
                dp[i][j][k] = -1;
            }
        }
    }

    // Function Call to find the
    // resultant count
    return countOfNumbers(1, 0, 0, N);
}

    public static void main(String[] args)
    {
        int N = 2;
    System.out.println(countNumbers(N));
    }
}

// This code is contributed by target_2
```

## 蟒蛇 3

```
# Python3 program for the above approach
dp = [[[-1 for i in range(10)]
           for j in range(10)]
           for k in range(100)]

from math import gcd

# Recursive function to find the count
# of all the N-digit numbers whose
# adjacent digits having equal GCD
def countOfNumbers(index, prev, gcd1, N):

    # If index is N+1
    if (index == N + 1):
        return 1

    val = dp[index][prev][gcd1]

    # If the state has already
    # been computed
    if (val != -1):
        return val

    # Stores the total count of all
    # N-digit numbers
    val = 0

    # If index = 1, any digit from
    # [1-9] can be placed.

    # If N = 0, 0 can be placed as well
    if (index == 1):
        digit = 0 if N == 1 else 1

        while(digit <= 9):

            # Update the value val
            val += countOfNumbers(index + 1,
                                  digit, gcd1, N)
            digit += 1

    # If index is 2, then any digit
    # from [0-9] can be placed
    elif (index == 2):
        for digit in range(10):
            val += countOfNumbers(index + 1, digit,
                                  gcd(prev, digit), N)

    # Otherwise any digit from [0-9] can
    # be placed if the GCD of current
    # and previous digit is gcd
    else:
        for digit in range(10):

            # Check if GCD of current
            # and previous digit is gcd
            if (gcd(digit, prev) == gcd):
                val += countOfNumbers(index + 1, digit,
                                      gcd1, N)

    # Return the total count
    return val

# Function to find the count of all
# the N-digit numbers whose adjacent
# digits having equal GCD
def countNumbers(N):

    # Function Call to find the
    # resultant count
    return countOfNumbers(1, 0, 0, N)

# Driver Code
if __name__ == '__main__':

    N = 2
    print(countNumbers(N))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{
  static int[,,] dp = new int[100, 10, 10];

  static int _gcd(int a, int b)
  {
    // Everything divides 0
    if (a == 0)
      return b;
    if (b == 0)
      return a;

    // base case
    if (a == b)
      return a;

    // a is greater
    if (a > b)
      return _gcd(a-b, b);
    return _gcd(a, b-a);
  }

  // Recursive function to find the count
  // of all the N-digit numbers whose
  // adjacent digits having equal GCD
  static int countOfNumbers(int index, int prev,
                            int gcd, int N)
  {
    // If index is N+1
    if (index == N + 1)
      return 1;

    int val = dp[index,prev,gcd];

    // If the state has already
    // been computed
    if (val != -1)
      return val;

    // Stores the total count of all
    // N-digit numbers
    val = 0;

    // If index = 1, any digit from
    // [1-9] can be placed.

    // If N = 0, 0 can be placed as well
    if (index == 1) {

      for (int digit = (N == 1 ? 0 : 1);
           digit <= 9;
           ++digit) {

        // Update the value val
        val += countOfNumbers(
          index + 1,
          digit, gcd, N);
      }
    }

    // If index is 2, then any digit
    // from [0-9] can be placed
    else if (index == 2) {

      for (int digit = 0;
           digit <= 9; ++digit) {
        val += countOfNumbers(
          index + 1, digit,
          _gcd(prev, digit), N);
      }
    }

    // Otherwise any digit from [0-9] can
    // be placed if the GCD of current
    // and previous digit is gcd
    else {

      for (int digit = 0;
           digit <= 9; ++digit) {

        // Check if GCD of current
        // and previous digit is gcd
        if (_gcd(digit, prev) == gcd) {
          val += countOfNumbers(
            index + 1, digit, gcd, N);
        }
      }
    }

    // Return the total count
    return val;
  }

  // Function to find the count of all
  // the N-digit numbers whose adjacent
  // digits having equal GCD
  static int countNumbers(int N)
  {
    int i, j, k;

    // Initialize dp array with -1
    for(i = 0; i < 100; i++)
    {
      for(j = 0; j < 10; j++)
      {
        for(k = 0; k < 10; k++)
        {
          dp[i,j,k] = -1;
        }
      }
    }

    // Function Call to find the
    // resultant count
    return countOfNumbers(1, 0, 0, N);
  }

  // Driver code
  static public void Main ()
  {
    int N = 2;
    Console.Write(countNumbers(N));
  }
}

// This code is contributed by shubham singh
```

## java 描述语言

```
<script>
// Javascript program for the above approach

let dp = new Array(100).fill(0).map(() => new Array(10).fill(0).map(() => new Array(10).fill(-1)));

// Recursive function to find the count
// of all the N-digit numbers whose
// adjacent digits having equal GCD
function countOfNumbers(index, prev, gcd, N)
{

    // If index is N+1
    if (index == N + 1)
        return 1;

    let val = dp[index][prev][gcd];

    // If the state has already
    // been computed
    if (val != -1)
        return val;

    // Stores the total count of all
    // N-digit numbers
    val = 0;

    // If index = 1, any digit from
    // [1-9] can be placed.

    // If N = 0, 0 can be placed as well
    if (index == 1) {

        for (let digit = (N == 1 ? 0 : 1);
             digit <= 9;
             ++digit) {

            // Update the value val
            val += countOfNumbers(
                index + 1,
                digit, gcd, N);
        }
    }

    // If index is 2, then any digit
    // from [0-9] can be placed
    else if (index == 2) {

        for (let digit = 0; digit <= 9; ++digit) {
            val += countOfNumbers(
                index + 1, digit,
                __gcd(prev, digit), N);
        }
    }

    // Otherwise any digit from [0-9] can
    // be placed if the GCD of current
    // and previous digit is gcd
    else {

        for (let digit = 0; digit <= 9; ++digit) {

            // Check if GCD of current
            // and previous digit is gcd
            if (__gcd(digit, prev) == gcd) {
                val += countOfNumbers(
                    index + 1, digit, gcd, N);
            }
        }
    }

    // Return the total count
    return val;
}

// Function to find the count of all
// the N-digit numbers whose adjacent
// digits having equal GCD
function countNumbers(N)
{
    // Function Call to find the
    // resultant count
    return countOfNumbers(1, 0, 0, N);
}

function __gcd(a, b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b); 

}

let N = 2;
document.write(countNumbers(N));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
90
```

***时间复杂度:**O(N * 1000)*
T5**辅助空间:** O(N * 10 * 10)