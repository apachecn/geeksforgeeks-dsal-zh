# 二进制字符串中的最小分割，每个子字符串都是 4 或 6 的幂。

> 原文:[https://www . geesforgeks . org/minimum-splits in-a-binary-string-so-每个子串都是 4 或 6 的幂/](https://www.geeksforgeeks.org/minimum-splits-in-a-binary-string-such-that-every-substring-is-a-power-of-4-or-6/)

给定一个由 0 和 1 组成的字符串 S。找到最小分割，使得子串是 4 或 6 的二进制表示，没有前导零。如果无法进行分区，打印-1。
**例:**

```
Input: 100110110
Output: 3
The string can be split into a minimum of 
three substrings 100(power of 4), 110
(power of 6) and 110(power of 6).

Input : 00000
Output : -1
0 is not a power of  4 or 6.
```

[Recommended: Please solve it on *“PRACTICE”* first, before moving on to the solution.](https://practice.geeksforgeeks.org/problems/cutting-binary-string/0/)

一个简单的**解决方案是在不同的索引处递归地拆分字符串，并检查每个拆分是 4 的幂还是 6 的幂。从索引 0 开始，从其他字符串中拆分字符串[0]。如果它是 4 或 6 的幂，则递归调用索引 1 并执行相同的操作。当整个字符串被拆分时，检查分区的总数是否最少。然后拆分字符串[0..1]，检查它是 4 的幂还是 6 的幂，然后递归调用 rest string。在字符串遍历结束时将分区与最小分区进行比较。这种方法在时间上将呈指数增长。
一个**高效的**解决方案是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。创建一维 dp 表，其中 dp[i]存储拆分字符串[i]所需的最小分区数..n-1]转换成 4 或 6 的幂的子串。假设我们在索引 I 和 str[i..j]是 4 或 6 的幂，则最小分区数将是分割 str[j+1]的最小分区数..n-1]加上一个分区来拆分字符串[i..j]从字符串，即 dp[j+1] + 1。因此(j！=(n-1))和(dp[j + 1]！=-1)将是:** 

> **dp[i] = min（dp[i]， dp[j + 1] + 1）**

****执行:**** 

## **C++**

```
// CPP program for Minimum splits in a
//string such that substring is a power of 4 or 6.

#include <bits/stdc++.h>
using namespace std;

// Function to find if given number
// is power of another number or not.
bool isPowerOf(long val, int base)
{

    // Divide given number repeatedly
    // by base value.
    while (val > 1) {
        if (val % base != 0)
            return false; // not a power
        val /= base;
    }

    return true;
}

// Function to find minimum number of
// partitions of given binary string
// so that each partition is power of 4 or 6.
int numberOfPartitions(string binaryNo)
{
    int i, j, n = binaryNo.length();

    // Variable to store integer value of
    // given binary string partition.
    long val;

    // DP table to store results of
    // partitioning done at differentindices.
    int dp[n];

    // If the last digit is 1, hence 4^0=1 and 6^0=1
    dp[n - 1] = ((binaryNo[n - 1] - '0') == 0) ? -1 : 1;

    // Fix starting position for partition
    for (i = n - 2; i >= 0; i--) {
        val = 0;

        // Binary representation
        // with leading zeroes is not allowed.
        if ((binaryNo[i] - '0') == 0) {
            dp[i] = -1;
            continue;
        }

        dp[i] = INT_MAX;

        // Iterate for all different partitions starting from i
        for (j = i; j < n; j++) {

            // Find integer value of current
            // binary partition.
            val = (val * 2) + (long)(binaryNo[j] - '0');

            // Check if the value is a power of 4 or 6 or not
            // apply recurrence relation
            if (isPowerOf(val, 4) || isPowerOf(val, 6)) {
                if (j == n - 1) {
                    dp[i] = 1;
                }
                else {
                    if (dp[j + 1] != -1)
                        dp[i] = min(dp[i], dp[j + 1] + 1);
                }
            }
        }

        // If no partitions are possible, then
        // make dp[i] = -1 to represent this.
        if (dp[i] == INT_MAX)
            dp[i] = -1;
    }

    return dp[0];
}

// Driver code
int main()
{
    string binaryNo = "100110110";
    cout << numberOfPartitions(binaryNo);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for Minimum splits
// in a string such that substring
// is a power of 4 or 6.
import java.io.*;

class GFG
{
    static boolean isPowerOf(long val,
                             int base)
{

    // Divide given number
    // repeatedly by base value.
    while (val > 1)
    {
        if (val % base != 0)
            return false; // not a power
        val /= base;
    }

    return true;
}

// Function to find minimum
// number of partitions of
// given binary string so that
// each partition is power
// of 4 or 6.
static int numberOfPartitions(String binaryNo)
{
    int i, j, n = binaryNo.length();

    // Variable to store integer
    // value of given binary
    // string partition.
    long val;

    // DP table to store results
    // of partitioning done at
    // differentindices.
    int dp[] = new int[n];

    // If the last digit is 1,
    // hence 4^0=1 and 6^0=1
    dp[n - 1] = (((binaryNo.charAt(n - 1) -
                               '0') == 0) ?
                                   -1 : 1);

    // Fix starting position
    // for partition
    for (i = n - 2; i >= 0; i--)
    {
        val = 0;

        // Binary representation
        // with leading zeroes
        // is not allowed.
        if ((binaryNo.charAt(i) - '0') == 0)
        {
            dp[i] = -1;
            continue;
        }

        dp[i] = Integer.MAX_VALUE;

        // Iterate for all different
        // partitions starting from i
        for (j = i; j < n; j++)
        {

            // Find integer value of
            // current binary partition.
            val = (val * 2) +
                  (long)(binaryNo.charAt(j) - '0');

            // Check if the value is a
            // power of 4 or 6 or not
            // apply recurrence relation
            if (isPowerOf(val, 4) ||
                isPowerOf(val, 6))
            {
                if (j == n - 1)
                {
                    dp[i] = 1;
                }
                else
                {
                    if (dp[j + 1] != -1)
                        dp[i] = Math.min(dp[i],
                                         dp[j + 1] + 1);
                }
            }
        }

        // If no partitions are possible,
        // then make dp[i] = -1 to
        // represent this.
        if (dp[i] == Integer.MAX_VALUE)
            dp[i] = -1;
    }

    return dp[0];
}

// Driver code
public static void main (String[] args)
{
    String binaryNo = "100110110";
    System.out.println(numberOfPartitions(binaryNo));
}
}

// This code is contributed
// by shiv_bhakt.
```

## **蟒蛇 3**

```
# Python 3 program for Minimum
# splits in a string such that
# substring is a power of 4 or 6.

import sys

# Function to find if given number
# is power of another number or not.
def isPowerOf(val, base):

    # Divide given number repeatedly
    # by base value.
    while (val > 1):
        if (val % base != 0):
            return False # not a power
        val //= base

    return True

# Function to find minimum number of
# partitions of given binary string
# so that each partition is power of 4 or 6.
def numberOfPartitions(binaryNo):

    n = len(binaryNo)

    # DP table to store results of
    # partitioning done at differentindices.
    dp = [0] * n

    # If the last digit is 1, hence 4^0=1 and 6^0=1
    if ((ord(binaryNo[n - 1]) - ord('0')) == 0) :
        dp[n - 1] = -1
    else:
        dp[n - 1] = 1

    # Fix starting position for partition
    for i in range( n - 2, -1, -1):
        val = 0

        # Binary representation
        # with leading zeroes is not allowed.
        if ((ord(binaryNo[i]) - ord('0')) == 0):
            dp[i] = -1
            continue

        dp[i] = sys.maxsize

        # Iterate for all different partitions starting from i
        for j in range(i, n):

            # Find integer value of current
            # binary partition.
            val = (val * 2) + (ord(binaryNo[j]) - ord('0'))

            # Check if the value is a power of 4 or 6 or not
            # apply recurrence relation
            if (isPowerOf(val, 4) or isPowerOf(val, 6)):
                if (j == n - 1):
                    dp[i] = 1

                else :
                    if (dp[j + 1] != -1):
                        dp[i] = min(dp[i], dp[j + 1] + 1)

        # If no partitions are possible, then
        # make dp[i] = -1 to represent this.
        if (dp[i] == sys.maxsize):
            dp[i] = -1

    return dp[0]

# Driver code
if __name__ == "__main__":

    binaryNo = "100110110"
    print(numberOfPartitions(binaryNo))

# This code is contributed by Ita_c.   
```

## **C#**

```
// C# program for Minimum splits
// in a string such that substring
// is a power of 4 or 6.

using System;

class GFG
{
    static bool isPowerOf(long val, int b)
{

    // Divide given number
    // repeatedly by base value.
    while (val > 1)
    {
        if (val % b != 0)
            return false; // not a power
        val /= b;
    }

    return true;
}

// Function to find minimum
// number of partitions of
// given binary string so that
// each partition is power
// of 4 or 6.
static int numberOfPartitions(string binaryNo)
{
    int i, j, n = binaryNo.Length;

    // Variable to store integer
    // value of given binary
    // string partition.
    long val;

    // DP table to store results
    // of partitioning done at
    // differentindices.
    int[] dp = new int[n];

    // If the last digit is 1,
    // hence 4^0=1 and 6^0=1
    dp[n - 1] = (((binaryNo[n - 1] -
                               '0') == 0) ?
                                   -1 : 1);

    // Fix starting position
    // for partition
    for (i = n - 2; i >= 0; i--)
    {
        val = 0;

        // Binary representation
        // with leading zeroes
        // is not allowed.
        if ((binaryNo[i] - '0') == 0)
        {
            dp[i] = -1;
            continue;
        }

        dp[i] = int.MaxValue;

        // Iterate for all different
        // partitions starting from i
        for (j = i; j < n; j++)
        {

            // Find integer value of
            // current binary partition.
            val = (val * 2) +
                  (long)(binaryNo[j] - '0');

            // Check if the value is a
            // power of 4 or 6 or not
            // apply recurrence relation
            if (isPowerOf(val, 4) ||
                isPowerOf(val, 6))
            {
                if (j == n - 1)
                {
                    dp[i] = 1;
                }
                else
                {
                    if (dp[j + 1] != -1)
                        dp[i] = Math.Min(dp[i],
                                         dp[j + 1] + 1);
                }
            }
        }

        // If no partitions are possible,
        // then make dp[i] = -1 to
        // represent this.
        if (dp[i] == int.MaxValue)
            dp[i] = -1;
    }

    return dp[0];
}

// Driver code
public static void Main ()
{
    string binaryNo = "100110110";
    Console.Write(numberOfPartitions(binaryNo));
}
}
```

## **java 描述语言**

```
<script>

// Javascript program for Minimum splits in a
//string such that substring is a power of 4 or 6.

// Function to find if given number
// is power of another number or not.
function isPowerOf(val, base)
{

    // Divide given number repeatedly
    // by base value.
    while (val > 1) {
        if (val % base != 0)
            return false; // not a power
        val /= base;
    }

    return true;
}

// Function to find minimum number of
// partitions of given binary string
// so that each partition is power of 4 or 6.
function numberOfPartitions(binaryNo)
{
    var i, j, n = binaryNo.length;

    // Variable to store integer value of
    // given binary string partition.
    var val;

    // DP table to store results of
    // partitioning done at differentindices.
    var dp = Array(n);

    // If the last digit is 1, hence 4^0=1 and 6^0=1
    dp[n - 1] = ((binaryNo[n - 1] - '0') == 0) ? -1 : 1;

    // Fix starting position for partition
    for (i = n - 2; i >= 0; i--) {
        val = 0;

        // Binary representation
        // with leading zeroes is not allowed.
        if ((binaryNo[i] - '0') == 0) {
            dp[i] = -1;
            continue;
        }

        dp[i] = 1000000000;

        // Iterate for all different partitions starting from i
        for (j = i; j < n; j++) {

            // Find integer value of current
            // binary partition.
            val = (val * 2) + (binaryNo[j] - '0');

            // Check if the value is a power of 4 or 6 or not
            // apply recurrence relation
            if (isPowerOf(val, 4) || isPowerOf(val, 6)) {
                if (j == n - 1) {
                    dp[i] = 1;
                }
                else {
                    if (dp[j + 1] != -1)
                        dp[i] = Math.min(dp[i], dp[j + 1] + 1);
                }
            }
        }

        // If no partitions are possible, then
        // make dp[i] = -1 to represent this.
        if (dp[i] == 1000000000)
            dp[i] = -1;
    }

    return dp[0];
}

// Driver code
var binaryNo = "100110110";
document.write( numberOfPartitions(binaryNo));

// This code is contributed by itsok.
</script>
```

****输出:****

```
 3
```

****时间复杂度:** O(n^2*log(x)，x =可从输入字符串获得的 4 或 6 的最大幂。
**辅助空间:** O(n)**