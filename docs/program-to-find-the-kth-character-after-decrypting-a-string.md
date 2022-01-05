# 解密字符串后查找第 kth 个字符的程序

> 原文:[https://www . geesforgeks . org/program-to-find-the-kth-character-after-decryption-a-string/](https://www.geeksforgeeks.org/program-to-find-the-kth-character-after-decrypting-a-string/)

给定一个由字符和数字组成的字符串**和一个整数 **k** ，任务是解密该字符串并返回解密字符串中的 **k <sup>第</sup>** 个字符。
为了解密字符串，逐个字符遍历字符串，如果当前字符是字母，则将其附加到结果字符串中；否则，如果它是数字，则解析该数字，并重复结果字符串的解析次数，然后继续原始字符串。例如，str = "ab2c3 "将被解密为" ababcababcababc "。
**举例:**** 

> **输入:** str = "ab2c3 "，k = 5
> **输出:** c
> 解密后的字符串会是“ababcababc”，而‘c’是第五个字符。
> **输入:** str = "x2y3 "，k = 3
> **输出:** y

**进场:**

*   初始化起始索引 **i = 0** 和 **total_len = 0** 。
*   当 **i** 小于输入字符串的长度时循环，检查当前字符是否是字母。如果是，则将 **total_len** 增加 **1** 并检查总长度是否小于或等于 **k** 如果是，则返回字符串 else increment **i** 。
*   初始化 **n = 0** 再次循环，同时 **i** 小于输入字符串的长度，并且 **i** 不是字母表，解析该数字并增加 **i** ，找到**next _ total _ len = total _ len * n .**
    *   如果 **k < total_len** 那么通过初始化 **pos = k % total_len** 获得角色的位置。
    *   如果找不到位置，则更新**位置= total_len** ，最后在**k<sup>th</sup>T5】位置返回角色。如果没有找到，则返回 **-1** 。**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <cstdlib>
#include <iostream>
using namespace std;

// Function to print kth character of
// String s after decrypting it
char findKthChar(string s, int k)
{

    // Get the length of string
    int len = s.length();

    // Initialise pointer to character
    // of input string to zero
    int i = 0;

    // Total length of resultant string
    int total_len = 0;

    // Traverse the string from starting
    // and check if each character is
    // alphabet then increment total_len
    while (i < len) {
        if (isalpha(s[i])) {

            total_len++;

            // If total_leg equal to k then
            // return string else increment i
            if (total_len == k)
                return s[i];

            i++;
        }

        else {

            // Parse the number
            int n = 0;
            while (i < len && !isalpha(s[i])) {
                n = n * 10 + (s[i] - '0');
                i++;
            }

            // Update next_total_len
            int next_total_len = total_len * n;

            // Get the position of kth character
            if (k <= next_total_len) {
                int pos = k % total_len;

                // Position not found then update
                // position with total_len
                if (!pos) {
                    pos = total_len;
                }

                // Recursively find the kth position
                return findKthChar(s, pos);
            }
            else {

                // Else update total_len
                // by next_total_len
                total_len = next_total_len;
            }
        }
    }

    // Return -1 if character not found
    return -1;
}

// Driver code
int main()
{
    string s = "ab2c3";
    int k = 5;

    cout << findKthChar(s, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GfG
{

// Function to print kth character of
// String s after decrypting it
static Character findKthChar(String s, int k)
{

    // Get the length of string
    int len = s.length();

    // Initialise pointer to character
    // of input string to zero
    int i = 0;

    // Total length of resultant string
    int total_len = 0;

    // Traverse the string from starting
    // and check if each character is
    // alphabet then increment total_len
    while (i < len)
    {
        if (Character.isLetter(s.charAt(i)))
        {

            total_len++;

            // If total_leg equal to k then
            // return string else increment i
            if (total_len == k)
                return s.charAt(i);

            i++;
        }

        else
        {

            // Parse the number
            int n = 0;
            while (i < len && !Character.isLetter(s.charAt(i)))
            {
                n = n * 10 + (s.charAt(i) - '0');
                i++;
            }

            // Update next_total_len
            int next_total_len = total_len * n;

            // Get the position of kth character
            if (k <= next_total_len)
            {
                int pos = k % total_len;

                // Position not found then update
                // position with total_len
                if (pos == 0)
                {
                    pos = total_len;
                }

                // Recursively find the kth position
                return findKthChar(s, pos);
            }
            else
            {

                // Else update total_len
                // by next_total_len
                total_len = next_total_len;
            }
        }
    }

    // Return -1 if character not found
    return ' ';
}

// Driver code
public static void main(String[] args)
{
    String s = "ab2c3";
    int k = 5;

    System.out.println(findKthChar(s, k));
}
}

// This code is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to print kth character of
# String s after decrypting it
def findKthChar(s, k):

    # Get the length of string
    len1 = len(s)

    # Initialise pointer to character
    # of input string to zero
    i = 0

    # Total length of resultant string
    total_len = 0

    # Traverse the string from starting
    # and check if each character is
    # alphabet then increment total_len
    while (i < len1):
        if (s[i].isalpha()):
            total_len += 1

            # If total_leg equal to k then
            # return string else increment i
            if (total_len == k):
                return s[i]

            i += 1

        else:

            # Parse the number
            n = 0
            while (i < len1 and s[i].isalpha() == False):
                n = n * 10 + (ord(s[i]) - ord('0'))
                i += 1

            # Update next_total_len
            next_total_len = total_len * n

            # Get the position of kth character
            if (k <= next_total_len):
                pos = k % total_len

                # Position not found then update
                # position with total_len
                if (pos == 0):
                    pos = total_len

                # Recursively find the kth position
                return findKthChar(s, pos)

            else:

                # Else update total_len
                # by next_total_len
                total_len = next_total_len

    # Return -1 if character not found
    return -1

# Driver code
if __name__ == '__main__':
    s = "ab2c3"
    k = 5

    print(findKthChar(s, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print kth character of
// String s after decrypting it
static char findKthChar(String s, int k)
{

    // Get the length of string
    int len = s.Length;

    // Initialise pointer to character
    // of input string to zero
    int i = 0;

    // Total length of resultant string
    int total_len = 0;

    // Traverse the string from starting
    // and check if each character is
    // alphabet then increment total_len
    while (i < len)
    {
        if (char.IsLetter(s[i]))
        {
            total_len++;

            // If total_leg equal to k then
            // return string else increment i
            if (total_len == k)
                return s[i];

            i++;
        }

        else
        {

            // Parse the number
            int n = 0;
            while (i < len && !char.IsLetter(s[i]))
            {
                n = n * 10 + (s[i] - '0');
                i++;
            }

            // Update next_total_len
            int next_total_len = total_len * n;

            // Get the position of kth character
            if (k <= next_total_len)
            {
                int pos = k % total_len;

                // Position not found then update
                // position with total_len
                if (pos == 0)
                {
                    pos = total_len;
                }

                // Recursively find the kth position
                return findKthChar(s, pos);
            }
            else
            {

                // Else update total_len
                // by next_total_len
                total_len = next_total_len;
            }
        }
    }

    // Return -1 if character not found
    return ' ';
}

// Driver code
public static void Main(String[] args)
{
    String s = "ab2c3";
    int k = 5;

    Console.WriteLine(findKthChar(s, k));
}
}

// This code is contributed by PrinciRaj1992
```

**Output:** 

```
c
```

**时间复杂度:** O(N)

**辅助空间:** O(1)