# 重新排列给定的二进制字符串以最大化它们的按位异或值

> 原文:[https://www . geeksforgeeks . org/重排给定二进制字符串以最大化它们的按位异或值/](https://www.geeksforgeeks.org/rearrange-given-binary-strings-to-maximize-their-bitwise-xor-value/)

给定三个长度分别为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)**S1****S2**和 **S3** ，任务是通过重新排列给定字符串的字符来找到最大可能的[位异或](https://www.geeksforgeeks.org/tag/xor/)。

**示例:**

> **输入:**S1 =“1001”，S2 =“0010”，S3 =“1110”
> **输出:** 15
> **解释:**
> 将 S1 的数字重新排列为“1010”，S2 为“1000”，S3 为“1101”。
> 这些字符串的异或是“1111”，十进制形式为 15。
> 
> **输入:**S1 =“11111”，S2 =“11111”，S3 =“11111”
> **输出:** 31
> **说明:**
> 没有其他方式排列位数。因此，异或是“11111”，十进制形式为 31。

**天真方法:**最简单的方法是生成所有可能的方式来重新排列 **S1** 、 **S2** 和 **S3** 。假设字符串中分别有 **O1** 、 **O2** 和 **O3** 设定位 **S1** 、 **S2** 和 **S3** 。要检查以获得最大[位异或](https://www.geeksforgeeks.org/calculate-xor-1-n/)值的重新排列总数如下:

> 重新排列 S1 =**<sup>N</sup>C<sub>O1</sub>T5
> 重新排列 S2 =**T8】NC<sub>O2</sub>**T13】重新排列 S3 =**T15】NC<sub>O3</sub>T19】的总方式****
> 
> 因此，要检查的所有可能的重新排列=**T1】NC<sub>O1</sub>*<sup>N</sup>C<sub>O2</sub>*<sup>N</sup>C<sub>O3</sub>T13】**

***时间复杂度:** O((N！) <sup>3</sup> ，其中 N 是给定字符串的长度。*
***辅助空间:** O(N)*

**有效方法:**想法是找到一个合适的重排 **S1** 、 **S2** 和 **S3** 这样他们的**位异或**值最大化使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。子问题可以存储在 **dp[][][][]** 表中，其中 **dp[i][o1][o2][o3]** 存储从索引 **i** 开始直到位置 **N-1** 的**最大异或**值，其中 **o1** 为， **o2** 和 **o3** 为**1**的编号****

从 **0** 到**(N–1)**的任何位置 **i** 都可能有四种情况:

1.  将 **1** s 分配给所有的**三根**弦
2.  将 **1** s 分配给任意两个**弦**
3.  将 **1** s 分配给任意一个**弦**。
4.  将 **0** s 分配给**所有**琴弦。

根据以上每个位置的可能情况，计算可从四种可能性中获得的最大[位异或](https://www.geeksforgeeks.org/tag/xor/):

按照以下步骤解决问题:

*   初始化一个表 **dp[][][][]** 来存储从 **0 到 N-1** 的位置 **i** 在 **S1** 、 **S2** 和 **S3** 的数量。
*   过渡状态如下:

> **dp[i][o1][o2][o3] = max(dp(将 1 分配给所有三个字符串)、dp(将 1 分配给两个字符串中的任何一个)、dp(将 1 分配给任何一个字符串)、dp(不将 1 分配给任何字符串))**其中，
> 
> **i** =当前位置
> **o1** =要放入琴弦 S1
> **o2** =要放入琴弦 S2
> **o3** 的剩余位置=要放入琴弦 S3 的剩余位置

*   使用上述转换解决所有情况的子问题，并打印其中的最大[异或](https://www.geeksforgeeks.org/calculate-xor-1-n/)值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Dp table to store the sub-problems
int dp[20][20][20][20];

// Function to find the maximum XOR
// value after rearranging the digits
int maxXorValue(int i, string& s1,
                string& s2, string& s3,
                int ones1, int ones2,
                int ones3, int n)
{
    // Base Case
    if (i >= n)
        return 0;

    // Return if already calculated
    if (dp[i][ones1][ones2][ones3] != -1)
        return dp[i][ones1][ones2][ones3];

    int option1 = 0, option2 = 0,
        option3 = 0, option4 = 0,
        option5 = 0, option6 = 0,
        option7 = 0, option8 = 0;

    // Assigning 1's to all string at
    // position 'i'.
    if (ones1 > 0 && ones2 > 0
        && ones3 > 0)

        // 2^(n-1-i) is the value
        // added to the total
        option1
            = (1 << ((n - 1) - i))
              + maxXorValue(i + 1, s1,
                            s2, s3, ones1 - 1,
                            ones2 - 1,
                            ones3 - 1, n);

    // Assigning 1's to strings 1 & 2
    if (ones1 > 0 && ones2 > 0
        && (n - i > ones3))
        option2
            = 0
              + maxXorValue(i + 1, s1,
                            s2, s3, ones1 - 1,
                            ones2 - 1,
                            ones3, n);

    // Assigning 1's to strings 2 & 3
    if (ones2 > 0 && ones3 > 0
        && (n - i > ones1))
        option3 = 0
                  + maxXorValue(i + 1, s1,
                                s2, s3,
                                ones1,
                                ones2 - 1,
                                ones3 - 1, n);

    // Assigning 1's to strings 3 & 1
    if (ones3 > 0 && ones1 > 0
        && (n - i > ones2))
        option4
            = 0
              + maxXorValue(i + 1, s1,
                            s2, s3,
                            ones1 - 1,
                            ones2,
                            ones3 - 1, n);

    // Assigning 1 to string 1
    if (ones1 > 0 && (n - i > ones2)
        && (n - i > ones3))
        option5 = (1 << ((n - 1) - i))
                  + maxXorValue(i + 1, s1,
                                s2, s3,
                                ones1 - 1,
                                ones2,
                                ones3, n);

    // Assigning 1 to string 2
    if (ones2 > 0 && (n - i > ones3)
        && (n - i > ones1))
        option6 = (1 << ((n - 1) - i))
                  + maxXorValue(i + 1, s1,
                                s2, s3, ones1,
                                ones2 - 1,
                                ones3, n);

    // Assigning 1 to string 3.
    if (ones3 > 0 && (n - i > ones2)
        && (n - i > ones1))
        option7 = (1 << ((n - 1) - i))
                  + maxXorValue(i + 1, s1,
                                s2, s3, ones1,
                                ones2,
                                ones3 - 1, n);

    // Assigning 0 to all the strings
    if ((n - i > ones2) && (n - i > ones3)
        && (n - i > ones1))
        option8 = 0
                  + maxXorValue(i + 1, s1,
                                s2, s3,
                                ones1,
                                ones2,
                                ones3, n);

    // Take the maximum amongst all of
    // the above solutions
    return dp[i][ones1][ones2][ones3]
           = max(option1,
                 max(option2,
                     max(option3,
                         max(option4,
                             max(option5,
                                 max(option6,
                                     max(option7,
                                         option8)))))));
}

// Function to get the count of ones
// in the string s
int onesCount(string& s)
{
    int count = 0;

    // Traverse the string
    for (auto x : s) {
        if (x == '1')
            ++count;
    }

    // Return the count
    return count;
}

// Utility Function to find the maximum
// XOR value after rearranging the digits
void maxXORUtil(string s1, string s2,
                string s3, int n)
{

    // Find the count of ones in
    // each of the strings
    int ones1 = onesCount(s1);
    int ones2 = onesCount(s2);
    int ones3 = onesCount(s3);

    // Initialize dp table with -1
    memset(dp, -1, sizeof dp);

    // Function Call
    cout << maxXorValue(0, s1, s2, s3,
                        ones1, ones2,
                        ones3, n);
}

// Driver code
int main()
{
    string s1 = "11110";
    string s2 = "10101";
    string s3 = "00111";

    int n = s1.size();

    // Function Call
    maxXORUtil(s1, s2, s3, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;
class GFG{

// Dp table to store the sub-problems
static int[][][][]  dp = new int[20][20][20][20];

// Function to find the maximum XOR
// value after rearranging the digits
static int maxXorValue(int i, String s1,
                       String s2, String s3,
                       int ones1, int ones2,
                       int ones3, int n)
{

    // Base Case
    if (i >= n)
        return 0;

    // Return if already calculated
    if (dp[i][ones1][ones2][ones3] != -1)
        return dp[i][ones1][ones2][ones3];

    int option1 = 0, option2 = 0,
        option3 = 0, option4 = 0,
        option5 = 0, option6 = 0,
        option7 = 0, option8 = 0;

    // Assigning 1's to all string at
    // position 'i'.
    if (ones1 > 0 && ones2 > 0 &&
        ones3 > 0)

        // 2^(n-1-i) is the value
        // added to the total
        option1 = (1 << ((n - 1) - i)) +
              maxXorValue(i + 1, s1, s2,
                          s3, ones1 - 1,
                              ones2 - 1,
                              ones3 - 1, n);

    // Assigning 1's to strings 1 & 2
    if (ones1 > 0 && ones2 > 0 &&
       (n - i > ones3))
        option2 = 0 + maxXorValue(i + 1, s1, s2,
                                  s3, ones1 - 1,
                                      ones2 - 1,
                                      ones3, n);

    // Assigning 1's to strings 2 & 3
    if (ones2 > 0 && ones3 > 0 &&
       (n - i > ones1))
        option3 = 0 + maxXorValue(i + 1, s1, s2,
                                  s3, ones1,
                                  ones2 - 1,
                                  ones3 - 1, n);

    // Assigning 1's to strings 3 & 1
    if (ones3 > 0 && ones1 > 0 &&
       (n - i > ones2))
        option4 = 0 + maxXorValue(i + 1, s1, s2,
                                  s3, ones1 - 1,
                                  ones2,
                                  ones3 - 1, n);

    // Assigning 1 to string 1
    if (ones1 > 0 && (n - i > ones2) &&
       (n - i > ones3))
        option5 = (1 << ((n - 1) - i)) +
                  maxXorValue(i + 1, s1, s2,
                              s3, ones1 - 1,
                              ones2, ones3, n);

    // Assigning 1 to string 2
    if (ones2 > 0 && (n - i > ones3) &&
       (n - i > ones1))
        option6 = (1 << ((n - 1) - i)) +
                  maxXorValue(i + 1, s1,
                              s2, s3, ones1,
                              ones2 - 1,
                              ones3, n);

    // Assigning 1 to string 3.
    if (ones3 > 0 && (n - i > ones2) &&
       (n - i > ones1))
        option7 = (1 << ((n - 1) - i)) +
                  maxXorValue(i + 1, s1,
                              s2, s3, ones1,
                              ones2,
                              ones3 - 1, n);

    // Assigning 0 to all the strings
    if ((n - i > ones2) && (n - i > ones3) &&
        (n - i > ones1))
        option8 = 0 + maxXorValue(i + 1, s1,
                                  s2, s3, ones1,
                                  ones2, ones3, n);

    // Take the maximum amongst all of
    // the above solutions
    return dp[i][ones1][ones2][ones3] =
        Math.max(option1,
                 Math.max(option2,
                     Math.max(option3,
                        Math.max(option4,
                             Math.max(option5,
                                 Math.max(option6,
                                     Math.max(option7,
                                              option8)))))));
}

// Function to get the count of ones
// in the string s
static int onesCount(String s)
{
    int count = 0;

    // Traverse the string
    for(char x : s.toCharArray())
    {
        if (x == '1')
            ++count;
    }

    // Return the count
    return count;
}

// Utility Function to find the maximum
// XOR value after rearranging the digits
static void maxXORUtil(String s1, String s2,
                       String s3, int n)
{

    // Find the count of ones in
    // each of the strings
    int ones1 = onesCount(s1);
    int ones2 = onesCount(s2);
    int ones3 = onesCount(s3);

    // Initialize dp table with -1
    for(int[][][] i : dp)
        for(int[][] j : i)
            for(int[] k : j)
                Arrays.fill(k, -1);

    // Function Call
    System.out.println(maxXorValue(0, s1, s2, s3,
                                   ones1, ones2,
                                   ones3, n));
}

// Driver code
public static void main (String[] args)
{
    String s1 = "11110";
    String s2 = "10101";
    String s3 = "00111";

    int n = s1.length();

    // Function call
    maxXORUtil(s1, s2, s3, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Dp table to store the
# sub-problems
dp = [[[[-1 for x in range(20)]
            for y in range(20)]
            for z in range(20)]
            for p in range(20)]

# Function to find the maximum
# XOR value after rearranging
# the digits
def maxXorValue(i, s1, s2, s3,
                ones1, ones2,
                ones3, n):

    # Base Case
    if (i >= n):
        return 0

    # Return if already
     #calculated
    if (dp[i][ones1][ones2][ones3] != -1):
        return dp[i][ones1][ones2][ones3]

    option1 = 0
    option2 = 0
    option3 = 0
    option4 = 0
    option5 = 0
    option6 = 0
    option7 = 0
    option8 = 0

    # Assigning 1's to all
    # string at position 'i'.
    if (ones1 > 0 and ones2 > 0 and
        ones3 > 0):

        # 2^(n-1-i) is the value
        # added to the total
        option1 = ((1 << ((n - 1) - i)) +
                    maxXorValue(i + 1, s1,
                                s2, s3,
                                ones1 - 1,
                                ones2 - 1,
                                ones3 - 1, n))

    # Assigning 1's to strings
    # 1 & 2
    if (ones1 > 0 and ones2 > 0 and
       (n - i > ones3)):
        option2 = (0 + maxXorValue(i + 1, s1,
                                   s2, s3,
                                   ones1 - 1,
                                   ones2 - 1,
                                   ones3, n))

    # Assigning 1's to strings
    # 2 & 3
    if (ones2 > 0 and ones3 > 0 and
       (n - i > ones1)):
        option3 = (0 + maxXorValue(i + 1, s1,
                                   s2, s3,
                                   ones1,
                                   ones2 - 1,
                                   ones3 - 1, n))

    # Assigning 1's to strings
    # 3 & 1
    if (ones3 > 0 and ones1 > 0 and
       (n - i > ones2)):
        option4 = (0 + maxXorValue(i + 1, s1,
                                   s2, s3,
                                   ones1 - 1,
                                   ones2,
                                   ones3 - 1, n))

    # Assigning 1 to string 1
    if (ones1 > 0 and (n - i > ones2)
            and (n - i > ones3)):
        option5 = ((1 << ((n - 1) - i))
                   + maxXorValue(i + 1, s1,
                                 s2, s3,
                                 ones1 - 1,
                                 ones2,
                                 ones3, n))

    # Assigning 1 to string 2
    if (ones2 > 0 and (n - i > ones3) and
       (n - i > ones1)):
        option6 = ((1 << ((n - 1) - i)) +
                    maxXorValue(i + 1, s1,
                                s2, s3,
                                ones1,
                                ones2 - 1,
                                ones3, n))

    # Assigning 1 to string 3.
    if (ones3 > 0 and (n - i > ones2) and
        (n - i > ones1)):
        option7 = ((1 << ((n - 1) - i)) +
                    maxXorValue(i + 1, s1,
                                s2, s3,
                                ones1, ones2,
                                ones3 - 1, n))

    # Assigning 0 to all the strings
    if ((n - i > ones2) and (n - i > ones3) and
        (n - i > ones1)):
        option8 = (0 + maxXorValue(i + 1, s1,
                                   s2, s3,
                                   ones1,
                                   ones2,
                                   ones3, n))

    # Take the maximum amongst all of
    # the above solutions
    dp[i][ones1][ones2][ones3] = max(option1,
                                 max(option2,
                                 max(option3,
                                 max(option4,
                                 max(option5,
                                 max(option6,
                                 max(option7,
                                 option8)))))))
    return dp[i][ones1][ones2][ones3]

# Function to get the count
# of ones in the string s
def onesCount(s):

    count = 0

    # Traverse the string
    for x in s:
        if (x == '1'):
            count += 1

    # Return the count
    return count

# Utility Function to find
# the maximum XOR value after
# rearranging the digits
def maxXORUtil(s1, s2,
               s3, n):

    # Find the count of ones in
    # each of the strings
    ones1 = onesCount(s1)
    ones2 = onesCount(s2)
    ones3 = onesCount(s3)

    global dp

    # Function Call
    print(maxXorValue(0, s1, s2, s3,
                      ones1, ones2,
                      ones3, n))

# Driver code
if __name__ == "__main__":

    s1 = "11110"
    s2 = "10101"
    s3 = "00111"
    n = len(s1)

    # Function Call
    maxXORUtil(s1, s2, s3, n)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Dp table to store
// the sub-problems
static int[,,,] dp =
       new int[20, 20,
               20, 20];

// Function to find the
// maximum XOR value after
// rearranging the digits
static int maxXorValue(int i, String s1,
                       String s2, String s3,
                       int ones1, int ones2,
                       int ones3, int n)
{    
  // Base Case
  if (i >= n)
    return 0;

  // Return if already calculated
  if (dp[i, ones1,
         ones2, ones3] != -1)
    return dp[i, ones1,
              ones2, ones3];

  int option1 = 0, option2 = 0,
  option3 = 0, option4 = 0,
  option5 = 0, option6 = 0,
  option7 = 0, option8 = 0;

  // Assigning 1's to all
  // string at position 'i'.
  if (ones1 > 0 && ones2 > 0 &&
      ones3 > 0)

    // 2^(n-1-i) is the value
    // added to the total
    option1 = (1 << ((n - 1) - i)) +
               maxXorValue(i + 1, s1,
                           s2, s3,
                           ones1 - 1,
                           ones2 - 1,
                           ones3 - 1, n);

  // Assigning 1's to
  // strings 1 & 2
  if (ones1 > 0 && ones2 > 0 &&
     (n - i > ones3))
    option2 = 0 + maxXorValue(i + 1, s1, s2,
                              s3, ones1 - 1,
                              ones2 - 1,
                              ones3, n);

  // Assigning 1's to strings 2 & 3
  if (ones2 > 0 && ones3 > 0 &&
     (n - i > ones1))
    option3 = 0 + maxXorValue(i + 1, s1, s2,
                              s3, ones1,
                              ones2 - 1,
                              ones3 - 1, n);

  // Assigning 1's to strings 3 & 1
  if (ones3 > 0 && ones1 > 0 &&
     (n - i > ones2))
    option4 = 0 + maxXorValue(i + 1, s1, s2,
                              s3, ones1 - 1,
                              ones2,
                              ones3 - 1, n);

  // Assigning 1 to string 1
  if (ones1 > 0 && (n - i > ones2) &&
     (n - i > ones3))
    option5 = (1 << ((n - 1) - i)) +
               maxXorValue(i + 1, s1,
                           s2,s3,
                           ones1 - 1,
                           ones2, ones3, n);

  // Assigning 1 to string 2
  if (ones2 > 0 && (n - i > ones3) &&
     (n - i > ones1))
    option6 = (1 << ((n - 1) - i)) +
               maxXorValue(i + 1, s1,
                           s2, s3,
                           ones1,
                           ones2 - 1,
                           ones3, n);

  // Assigning 1 to string 3.
  if (ones3 > 0 && (n - i > ones2) &&
     (n - i > ones1))
    option7 = (1 << ((n - 1) - i)) +
               maxXorValue(i + 1, s1,
                           s2, s3,
                           ones1,
                           ones2,
                           ones3 - 1, n);

  // Assigning 0 to all the strings
  if ((n - i > ones2) &&
      (n - i > ones3) &&
      (n - i > ones1))
    option8 = 0 + maxXorValue(i + 1,
                              s1, s2,
                              s3, ones1,
                              ones2, ones3, n);

  // Take the maximum amongst all of
  // the above solutions
  return dp[i, ones1,
            ones2, ones3] = Math.Max(option1,
                            Math.Max(option2,
                            Math.Max(option3,
                            Math.Max(option4,
                            Math.Max(option5,
                            Math.Max(option6,
                            Math.Max(option7,
                                     option8)))))));
}

// Function to get the count
// of ones in the string s
static int onesCount(String s)
{
  int count = 0;

  // Traverse the string
  foreach(char x in s.ToCharArray())
  {
    if (x == '1')
      ++count;
  }

  // Return the count
  return count;
}

// Utility Function to find the maximum
// XOR value after rearranging the digits
static void maxXORUtil(String s1, String s2,
                       String s3, int n)
{  
  // Find the count of ones in
  // each of the strings
  int ones1 = onesCount(s1);
  int ones2 = onesCount(s2);
  int ones3 = onesCount(s3);

  // Initialize dp table with -1
  for(int i = 0; i < 20; i++)
  {
    for(int j = 0; j < 20; j++)
    {
      for(int l = 0; l < 20; l++)
        for(int k = 0; k < 20; k++)
          dp[i, j, l, k] =- 1;
    }
  }

  // Function Call
  Console.WriteLine(maxXorValue(0, s1, s2, s3,
                                ones1, ones2,
                                ones3, n));
}

// Driver code
public static void Main(String[] args)
{
  String s1 = "11110";
  String s2 = "10101";
  String s3 = "00111";

  int n = s1.Length;

  // Function call
  maxXORUtil(s1, s2, s3, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Dp table to store the sub-problems
let dp = new Array(20);
for(let i = 0; i < 20; i++)
{
    dp[i] = new Array(20);
    for(let j = 0; j < 20; j++)
    {
        dp[i][j] = new Array(20);
        for(let k = 0; k < 20; k++)
        {
            dp[i][j][k] = new Array(20);
            for(let l = 0; l < 20; l++)
            {
                dp[i][j][k][l] = -1;
            }
        }
    }
}

// Function to find the maximum XOR
// value after rearranging the digits
function maxXorValue(i, s1, s2, s3, ones1,
                     ones2, ones3, n)
{

    // Base Case
    if (i >= n)
        return 0;

    // Return if already calculated
    if (dp[i][ones1][ones2][ones3] != -1)
        return dp[i][ones1][ones2][ones3];

    let option1 = 0, option2 = 0,
        option3 = 0, option4 = 0,
        option5 = 0, option6 = 0,
        option7 = 0, option8 = 0;

    // Assigning 1's to all string at
    // position 'i'.
    if (ones1 > 0 && ones2 > 0 &&
        ones3 > 0)

        // 2^(n-1-i) is the value
        // added to the total
        option1 = (1 << ((n - 1) - i)) +
              maxXorValue(i + 1, s1, s2,
                          s3, ones1 - 1,
                              ones2 - 1,
                              ones3 - 1, n);

    // Assigning 1's to strings 1 & 2
    if (ones1 > 0 && ones2 > 0 &&
       (n - i > ones3))
        option2 = 0 + maxXorValue(i + 1, s1, s2,
                                  s3, ones1 - 1,
                                      ones2 - 1,
                                      ones3, n);

    // Assigning 1's to strings 2 & 3
    if (ones2 > 0 && ones3 > 0 &&
       (n - i > ones1))
        option3 = 0 + maxXorValue(i + 1, s1, s2,
                                  s3, ones1,
                                  ones2 - 1,
                                  ones3 - 1, n);

    // Assigning 1's to strings 3 & 1
    if (ones3 > 0 && ones1 > 0 &&
       (n - i > ones2))
        option4 = 0 + maxXorValue(i + 1, s1, s2,
                                  s3, ones1 - 1,
                                  ones2,
                                  ones3 - 1, n);

    // Assigning 1 to string 1
    if (ones1 > 0 && (n - i > ones2) &&
       (n - i > ones3))
        option5 = (1 << ((n - 1) - i)) +
                   maxXorValue(i + 1, s1, s2,
                               s3, ones1 - 1,
                               ones2, ones3, n);

    // Assigning 1 to string 2
    if (ones2 > 0 && (n - i > ones3) &&
       (n - i > ones1))
        option6 = (1 << ((n - 1) - i)) +
                   maxXorValue(i + 1, s1,
                               s2, s3, ones1,
                               ones2 - 1,
                               ones3, n);

    // Assigning 1 to string 3.
    if (ones3 > 0 && (n - i > ones2) &&
       (n - i > ones1))
        option7 = (1 << ((n - 1) - i)) +
                  maxXorValue(i + 1, s1,
                              s2, s3, ones1,
                              ones2,
                              ones3 - 1, n);

    // Assigning 0 to all the strings
    if ((n - i > ones2) && (n - i > ones3) &&
        (n - i > ones1))
        option8 = 0 + maxXorValue(i + 1, s1,
                                  s2, s3, ones1,
                                  ones2, ones3, n);

    // Take the maximum amongst all of
    // the above solutions
    return dp[i][ones1][ones2][ones3] =
        Math.max(option1,
                 Math.max(option2,
                     Math.max(option3,
                        Math.max(option4,
                             Math.max(option5,
                                 Math.max(option6,
                                     Math.max(option7,
                                              option8)))))));
}

// Function to get the count of ones
// in the string s
function onesCount(s)
{
    let count = 0;

    // Traverse the string
    for(let x = 0; x < s.length; x++)
    {
        if (s[x] == '1')
            ++count;
    }

    // Return the count
    return count;
}

// Utility Function to find the maximum
// XOR value after rearranging the digits
function maxXORUtil(s1, s2, s3, n)
{

    // Find the count of ones in
    // each of the strings
    let ones1 = onesCount(s1);
    let ones2 = onesCount(s2);
    let ones3 = onesCount(s3);

    // Function Call
    document.write(maxXorValue(0, s1, s2, s3,
                               ones1, ones2,
                               ones3, n));
}

// Driver code
let s1 = "11110";
let s2 = "10101";
let s3 = "00111";
let n = s1.length;

// Function call
maxXORUtil(s1, s2, s3, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
30
```

***时间复杂度:**O(N<sup>4</sup>)*
***辅助空间:** O(N)*