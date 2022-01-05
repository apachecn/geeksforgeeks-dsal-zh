# 将给定字符串拆分为赔率:数字 DP

> 原文:[https://www . geeksforgeeks . org/将给定字符串拆分为赔率数字 dp/](https://www.geeksforgeeks.org/split-the-given-string-into-odds-digit-dp/)

**先决条件:** [Digit-DP](https://www.geeksforgeeks.org/digit-dp-introduction/)
给定字符串 **str** 表示一个大数，任务是找到给定字符串可以划分的最小段数，使得每个段都是在 **1 到 10 <sup>9</sup>** 范围内的奇数。
**举例:**

> **输入:**str = " 123456789123456789123 "
> **输出:** 3
> **说明:**
> 该数可分为{123456789，123456789，123}
> **输入:** str = "123456"
> **输出:** -1

**方法:**思路是借助[数字-dp](https://www.geeksforgeeks.org/digit-dp-introduction/) 概念，使用[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)来解决这个问题。因此，定义了一个 **splitDP[]** 数组，其中 splitDP[i]表示长度为“I”的前缀字符串中将其拆分为奇数子部分所需的最小拆分次数。
splitDP[]数组的填充方式如下:

*   循环用于遍历给定字符串的所有索引。
*   对于上述循环中的每个索引“I”，从 1 到 9 迭代另一个循环，以检查来自第(i + j)个索引的子串是否为奇数。
*   如果它形成奇数，则 splitDP[]处的值更新为:

```
splitDP[i + j] = min(splitDP[i + j], 1 + splitDP[i]);
```

*   更新数组的所有值后，最后一个索引处的值是整个字符串的最小拆分数。

以下是上述方法的实现:

## C++

```
// C++ program to split the given string into odds
#include <bits/stdc++.h>
using namespace std;

// Function to check whether a string
// is an odd number or not
bool checkOdd(string number)
{
    int n = number.length();

    int num = number[n - 1] - '0';

    return (num & 1);
}

// A function to find the minimum
// number of segments the given string
// can be divided such that every
// segment is a odd number
int splitIntoOdds(string number)
{
    int numLen = number.length();

    // Declare a splitdp[] array
    // and initialize to -1
    int splitDP[numLen + 1];
    memset(splitDP, -1, sizeof(splitDP));

    // Build the DP table in
    // a bottom-up manner
    for (int i = 1; i <= numLen; i++) {

        // Initially Check if the entire prefix is odd
        if (i <= 9 && checkOdd(number.substr(0, i)))
            splitDP[i] = 1;

        // If the Given Prefix can be split into Odds
        // then for the remaining string from i to j
        // Check if Odd. If yes calculate
        // the minimum split till j
        if (splitDP[i] != -1) {
            for (int j = 1; j <= 9
                            && i + j <= numLen;
                 j++) {

                // To check if the substring from i to j
                // is a odd number or not
                if (checkOdd(number.substr(i, j))) {

                    // If it is an odd number,
                    // then update the dp array
                    if (splitDP[i + j] == -1)
                        splitDP[i + j] = 1 + splitDP[i];

                    else
                        splitDP[i + j] = min(splitDP[i + j],
                                             1 + splitDP[i]);
                }
            }
        }
    }

    // Return the minimum number of splits
    // for the entire string
    return splitDP[numLen];
}

// Driver code
int main()
{
    cout << splitIntoOdds("123456789123456789123") << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to split the given string into odds
class GFG {

    // Function to check whether a string
    // is an odd number or not
    static int checkOdd(String number)
    {
        int n = number.length();

        int num = number.charAt(n - 1) - '0';

        return (num & 1);
    }

    // A function to find the minimum
    // number of segments the given string
    // can be divided such that every
    // segment is a odd number
    static int splitIntoOdds(String number)
    {
        int numLen = number.length();

        // Declare a splitdp[] array
        // and initialize to -1
        int splitDP[] = new int[numLen + 1];

        for(int i= 0; i < numLen + 1; i++)
            splitDP[i] = -1;

        // Build the DP table in
        // a bottom-up manner
        for (int i = 1; i <= numLen; i++) {

            // Initially Check if the entire prefix is odd
            if (i <= 9 && (checkOdd(number.substring(0, i)) == 1))
                splitDP[i] = 1;

            // If the Given Prefix can be split into Odds
            // then for the remaining string from i to j
            // Check if Odd. If yes calculate
            // the minimum split till j
            if (splitDP[i] != -1) {
                for (int j = 1; j <= 9
                                && i + j <= numLen;
                    j++) {

                    // To check if the substring from i to j
                    // is a odd number or not
                    if (checkOdd(number.substring(i, i + j)) == 1) {

                        // If it is an odd number,
                        // then update the dp array
                        if (splitDP[i + j] == -1)
                            splitDP[i + j] = 1 + splitDP[i];

                        else
                            splitDP[i + j] = Math.min(splitDP[i + j],
                                                1 + splitDP[i]);
                    }
                }
            }
        }

        // Return the minimum number of splits
        // for the entire string
        return splitDP[numLen];
    }

    // Driver code
    public static void main (String[] args)
    {
        System.out.println(splitIntoOdds("123456789123456789123"));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to split the given string into odds

# Function to check whether a string
# is an odd number or not
def checkOdd(number):
    n = len(number)
    num = ord(number[n - 1]) - 48
    return (num & 1)

# A function to find the minimum
# number of segments the given string
# can be divided such that every
# segment is a odd number
def splitIntoOdds(number):
    numLen = len(number)

    # Declare a splitdp[] array
    # and initialize to -1
    splitDP = [-1 for i in range(numLen + 1)]

    # Build the DP table in
    # a bottom-up manner
    for i in range(1, numLen + 1):

        # Initially Check if the entire prefix is odd
        if (i <= 9 and checkOdd(number[0:i]) > 0):
            splitDP[i] = 1

        # If the Given Prefix can be split into Odds
        # then for the remaining string from i to j
        # Check if Odd. If yes calculate
        # the minimum split till j
        if (splitDP[i] != -1):
            for j in range(1, 10):
                if(i + j > numLen):
                    break;

                # To check if the substring from i to j
                # is a odd number or not
                if (checkOdd(number[i:i + j])):

                    # If it is an odd number,
                    # then update the dp array
                    if (splitDP[i + j] == -1):
                        splitDP[i + j] = 1 + splitDP[i]
                    else:
                        splitDP[i + j] = min(splitDP[i + j], 1 + splitDP[i])

    # Return the minimum number of splits
    # for the entire string
    return splitDP[numLen]

# Driver code
print(splitIntoOdds("123456789123456789123"))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to split the given string into odds
using System;

class GFG {

    // Function to check whether a string
    // is an odd number or not
    static int checkOdd(string number)
    {
        int n = number.Length;

        int num = number[n - 1] - '0';

        return (num & 1);
    }

    // A function to find the minimum
    // number of segments the given string
    // can be divided such that every
    // segment is a odd number
    static int splitIntoOdds(string number)
    {
        int numLen = number.Length;

        // Declare a splitdp[] array
        // and initialize to -1
        int []splitDP = new int[numLen + 1];

        for(int i= 0; i < numLen + 1; i++)
            splitDP[i] = -1;

        // Build the DP table in
        // a bottom-up manner
        for (int i = 1; i <= numLen; i++) {

            // Initially Check if the entire prefix is odd
            if (i <= 9 && (checkOdd(number.Substring(0, i)) == 1))
                splitDP[i] = 1;

            // If the Given Prefix can be split into Odds
            // then for the remaining string from i to j
            // Check if Odd. If yes calculate
            // the minimum split till j
            if (splitDP[i] != -1) {
                for (int j = 1; j <= 9
                                && i + j <= numLen;
                    j++) {

                    // To check if the substring from i to j
                    // is a odd number or not
                    if (checkOdd(number.Substring(i, j)) == 1) {

                        // If it is an odd number,
                        // then update the dp array
                        if (splitDP[i + j] == -1)
                            splitDP[i + j] = 1 + splitDP[i];

                        else
                            splitDP[i + j] = Math.Min(splitDP[i + j],
                                                1 + splitDP[i]);
                    }
                }
            }
        }

        // Return the minimum number of splits
        // for the entire string
        return splitDP[numLen];
    }

    // Driver code
    public static void Main (string[] args)
    {
        Console.WriteLine(splitIntoOdds("123456789123456789123"));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript program to split the
// given string into odds

    // Function to check whether a string
    // is an odd number or not
    function checkOdd(number)
    {
        let n = number.length;

        let num = number[n - 1] - '0';

        return (num & 1);
    }

    // A function to find the minimum
    // number of segments the given string
    // can be divided such that every
    // segment is a odd number
    function split intoOdds(number)
    {
        let numLen = number.length;

        // Declare a splitdp[] array
        // and initialize to -1
        let splitDP =
        Array.from({length: numLen + 1}, (_, i) => 0);

        for(let i= 0; i < numLen + 1; i++)
            splitDP[i] = -1;

        // Build the DP table in
        // a bottom-up manner
        for (let i = 1; i <= numLen; i++)
        {

            // Initially Check if the
            // entire prefix is odd
            if (i <= 9 &&
            (checkOdd(number.substr(0, i)) == 1))
                splitDP[i] = 1;

            // If the Given Prefix can
            // be split into Odds
            // then for the remaining
            // string from i to j
            // Check if Odd.
            // If yes calculate
            // the minimum split till j
            if (splitDP[i] != -1) {
                for (let j = 1; j <= 9
                      && i + j <= numLen; j++) {

                 // To check if the
                // substring from i to j
               // is a odd number or not
                 if (checkOdd(number.substr(i, i + j)) == 1)
                    {

                  // If it is an odd number,
                 // then update the dp array
                   if (splitDP[i + j] == -1)
                       splitDP[i + j] = 1 + splitDP[i];

                        else
                            splitDP[i + j] =
                            Math.min(splitDP[i + j],
                                        1 + splitDP[i]);
                    }
                }
            }
        }

        // Return the minimum number of splits
        // for the entire string
        return splitDP[numLen];
    }

// Driver code

    document.write(splitintoOdds("123456789123456789123"));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)

**辅助空间:** O(numLen)