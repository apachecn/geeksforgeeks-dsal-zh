# 检查一根弦是否可以由另一根弦最多顺时针旋转 X 次形成

> 原文:[https://www . geesforgeks . org/check-if-a-string-can-formed-from-other-string-by-至多-x-circular-顺时针移动其字符/](https://www.geeksforgeeks.org/check-if-a-string-can-be-formed-from-another-string-by-at-most-x-circular-clockwise-shifts-of-its-characters/)

给定一个整数 **X** 和两个字符串 **S1** 和 **S2** ，任务是检查字符串 **S1** 是否可以通过顺时针旋转字符 X 次转换为字符串 **S2** 。

> **输入:**S1 =“ABCD”，S2 =“dddd”，X = 3
> **输出:**是
> **解释:**
> 给定字符串 S1 可以转换为字符串 S2 为-
> 字符“a”–移位 3 次–“d”
> 字符“b”–移位 2 次–“d”
> 字符“c”–移位 1 次–“d”
> 字符“d”–移位 0 次–“d”
> 
> **输入:**S1 =“you”，S2 =“ara”，X = 6
> **输出:**是
> **说明:**
> 给定字符串 S1 可以转换为字符串 S2 为–
> 字符“y”–循环移位 2 次–“a”
> 字符“o”–移位 3 次–“r”
> 字符“u”–循环移位 6 次–“a”

**方法:**思路是遍历字符串并针对每个索引，找到两个字符串各自索引处字符的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)之间的差异。如果差值小于 0，那么对于循环移位，加 26 得到实际差值。如果对于任何一个指标，差值超过 **X** ，那么 **S2** 就不能由 **S1** 形成，否则有可能。
以下是上述方法的实施:

## C++

```
// C++ implementation to check
// that a given string can be
// converted to another string
// by circular clockwise shift
// of each character by atmost
// X times

#include <bits/stdc++.h>
using namespace std;

// Function to check that all
// characters of s1 can be
// converted to s2 by circular
// clockwise shift atmost X times
void isConversionPossible(string s1,
                          string s2, int x)
{
    int diff, n;
    n = s1.length();

    // Check for all characters of
    // the strings whether the
    // difference between their
    // ascii values is less than
    // X or not
    for (int i = 0; i < n; i++) {

        // If both the characters
        // are same
        if (s1[i] == s2[i])
            continue;

        // Calculate the difference
        // between the ASCII values
        // of the characters
        diff = (int(s2[i] - s1[i])
                + 26)
               % 26;

        // If difference exceeds X
        if (diff > x) {
            cout << "NO" << endl;
            return;
        }
    }

    cout << "YES" << endl;
}

// Driver Code
int main()
{
    string s1 = "you";
    string s2 = "ara";

    int x = 6;

    // Function call
    isConversionPossible(s1, s2, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// that a given string can be
// converted to another string
// by circular clockwise shift
// of each character by atmost
// X times
import java.io.*;
import java.util.*;

class GFG{

// Function to check that all
// characters of s1 can be
// converted to s2 by circular
// clockwise shift atmost X times
static void isConversionPossible(String s1,
                                 String s2,
                                 int x)
{
    int diff = 0, n;
    n = s1.length();

    // Check for all characters of
    // the strings whether the
    // difference between their
    // ascii values is less than
    // X or not
    for(int i = 0; i < n; i++)
    {

       // If both the characters
       // are same
       if (s1.charAt(i) == s2.charAt(i))
           continue;

       // Calculate the difference
       // between the ASCII values
       // of the characters
       diff = ((int)(s2.charAt(i) -
                     s1.charAt(i)) + 26) % 26;

       // If difference exceeds X
       if (diff > x)
       {
           System.out.println("NO");
           return;
       }
    }
    System.out.println("YES");
}

// Driver Code
public static void main (String[] args)
{
    String s1 = "you";
    String s2 = "ara";

    int x = 6;

    // Function call
    isConversionPossible(s1, s2, x);
}
}

// This code is contributed by Ganeshchowdharysadanala
```

## 蟒蛇 3

```
# Python3 implementation to check
# that the given string can be
# converted to another string
# by circular clockwise shift

# Function to check that the
# string s1 can be converted
# to s2 by clockwise circular
# shift of all characters of
# str1 atmost X times
def isConversionPossible(s1, s2, x):
    n = len(s1)
    s1 = list(s1)
    s2 = list(s2)

    for i in range(n):

        # Difference between the
        # ASCII numbers of characters
        diff = ord(s2[i]) - ord(s1[i])

        # If both characters
        # are the same
        if diff == 0:
            continue

        # Condition to check if the
        # difference less than 0 then
        # find the circular shift by
        # adding 26 to it
        if diff < 0:
            diff = diff + 26
        # If difference between
        # their ASCII values
        # exceeds X
        if diff > x:
            return False

    return True

# Driver Code
if __name__ == "__main__":
    s1 = "you"
    s2 = "ara"
    x = 6

    # Function Call
    result = isConversionPossible(s1, s2, x)

    if result:
        print("YES")
    else:
        print("NO")
```

## C#

```
// C# implementation to check
// that a given string can be
// converted to another string
// by circular clockwise shift
// of each character by atmost
// X times
using System;

class GFG{

// Function to check that all
// characters of s1 can be
// converted to s2 by circular
// clockwise shift atmost X times
static void isConversionPossible(String s1,
                                 String s2,
                                 int x)
{
    int diff = 0, n;
    n = s1.Length;

    // Check for all characters of
    // the strings whether the
    // difference between their
    // ascii values is less than
    // X or not
    for(int i = 0; i < n; i++)
    {

        // If both the characters
        // are same
        if (s1[i] == s2[i])
            continue;

        // Calculate the difference
        // between the ASCII values
        // of the characters
        diff = ((int)(s2[i] -
                      s1[i]) + 26) % 26;

        // If difference exceeds X
        if (diff > x)
        {
            Console.Write("NO");
            return;
        }
    }
    Console.Write("YES");
}

// Driver Code
public static void Main ()
{
    String s1 = "you";
    String s2 = "ara";

    int x = 6;

    // Function call
    isConversionPossible(s1, s2, x);
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// Javascript implementation to check
// that a given string can be
// converted to another string
// by circular clockwise shift
// of each character by atmost
// X times

// Function to check that all
// characters of s1 can be
// converted to s2 by circular
// clockwise shift atmost X times
function isConversionPossible(s1,s2,x)
{
    let diff = 0, n;
    n = s1.length;

    // Check for all characters of
    // the strings whether the
    // difference between their
    // ascii values is less than
    // X or not
    for(let i = 0; i < n; i++)
    {

       // If both the characters
       // are same
       if (s1[i] == s2[i])
           continue;

       // Calculate the difference
       // between the ASCII values
       // of the characters
       diff = ((s2[i].charCodeAt(0) -
                     s1[i].charCodeAt(0)) + 26) % 26;

       // If difference exceeds X
       if (diff > x)
       {
           document.write("NO<br>");
           return;
       }
    }
    document.write("YES<br>");
}

// Driver Code
let s1 = "you";
let s2 = "ara";
let x = 6;

// Function call
isConversionPossible(s1, s2, x);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(N)，N =长度(S1)

**辅助空间:** O(1)