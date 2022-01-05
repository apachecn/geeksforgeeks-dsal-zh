# 程序求字符串中字符 ASCII 值的异或

> 原文:[https://www . geesforgeks . org/program-to-find-of-xor-of-ascii-values-in-a-string/](https://www.geeksforgeeks.org/program-to-find-the-xor-of-ascii-values-of-characters-in-a-string/)

给定一个字符串 **str** ，任务是找出字符串中字符的 ASCII 值的异或。
**例:**

> **输入:** str = "Geeks"
> **输出:** 95
> ASCII 值 G = 71
> ASCII 值 e = 101
> ASCII 值 e = 101
> ASCII 值 k = 107
> ASCII 值 s = 115
> ascii 值 xor = 71 ^ 101 ^ 101 ^ 107 ^ 115 = 95
> **输入**

**做法:**思路是[逐个找出每个字符](https://www.geeksforgeeks.org/program-print-ascii-value-character/)的 ASCII 值，再找出这些值的 [XOR 值。
以下是上述方法的实现:](https://www.geeksforgeeks.org/calculate-xor-1-n/) 

## C++

```
// C++ program to find XOR of ASCII
// value of characters in string

#include <bits/stdc++.h>
using namespace std;

// Function to find the XOR of ASCII
// value of characters in string
int XorAscii(string str, int len)
{

    // store value of first character
    int ans = int(str[0]);

    for (int i = 1; i < len; i++) {

        // Traverse string to find the XOR
        ans = (ans ^ (int(str[i])));
    }

    // Return the XOR
    return ans;
}

// Driver code
int main()
{

    string str = "geeksforgeeks";
    int len = str.length();
    cout << XorAscii(str, len) << endl;

    str = "GfG";
    len = str.length();
    cout << XorAscii(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find XOR of ASCII
// value of characters in String
class GFG{

// Function to find the XOR of ASCII
// value of characters in String
static int XorAscii(String str, int len)
{

    // store value of first character
    int ans = (str.charAt(0));

    for (int i = 1; i < len; i++) {

        // Traverse String to find the XOR
        ans = (ans ^ ((str.charAt(i))));
    }

    // Return the XOR
    return ans;
}

// Driver code
public static void main(String[] args)
{

    String str = "geeksforgeeks";
    int len = str.length();
    System.out.print(XorAscii(str, len) +"\n");

    str = "GfG";
    len = str.length();
    System.out.print(XorAscii(str, len));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find XOR of ASCII
# value of characters in str1ing

# Function to find the XOR of ASCII
# value of characters in str1ing
def XorAscii(str1, len1):

    # store value of first character
    ans = ord(str1[0])

    for i in range(1,len1):

        # Traverse str1ing to find the XOR
        ans = (ans ^ (ord(str1[i])))

    # Return the XOR
    return ans

# Driver code
str1 = "geeksforgeeks"
len1 = len(str1)
print(XorAscii(str1, len1))

str1 = "GfG"
len1 = len(str1)
print(XorAscii(str1, len1))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find XOR of ASCII
// value of characters in String
using System;

class GFG{

// Function to find the XOR of ASCII
// value of characters in String
static int XorAscii(String str, int len)
{

    // store value of first character
    int ans = (str[0]);

    for (int i = 1; i < len; i++) {

        // Traverse String to find the XOR
        ans = (ans ^ ((str[i])));
    }

    // Return the XOR
    return ans;
}

// Driver code
public static void Main(String[] args)
{

    String str = "geeksforgeeks";
    int len = str.Length;
    Console.Write(XorAscii(str, len) +"\n");

    str = "GfG";
    len = str.Length;
    Console.Write(XorAscii(str, len));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find XOR of ASCII
// value of characters in string

// Function to find the XOR of ASCII
// value of characters in string
function XorAscii(str, len)
{

    // store value of first character
    let ans = str.codePointAt(0);

    for (let i = 1; i < len; i++) {

        // Traverse string to find the XOR
        ans = (ans ^ (str.codePointAt(i)));
    }

    // Return the XOR
    return ans;
}

// Driver code

    let str = "geeksforgeeks";
    let len = str.length;
    document.write(XorAscii(str, len) + "<br>");

    str = "GfG";
    len = str.length;
    document.write(XorAscii(str, len));

</script>
```

**Output:** 

```
123
102
```

**时间复杂度:** **O(N)** ，其中 N 为字符串长度。