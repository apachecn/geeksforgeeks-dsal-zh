# 找到包含一个或多个给定字符串的最短二进制字符串

> 原文:[https://www . geesforgeks . org/find-最短二进制字符串-包含给定字符串的一个或多个出现次数/](https://www.geeksforgeeks.org/find-the-shortest-binary-string-containing-one-or-more-occurrences-of-given-strings/)

给定两个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)、 **S1** 和 **S2** ，任务是生成一个新的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)(长度尽可能最小)，可以表示为一个或多个 **S1** 以及 **S2** 的出现。如果无法生成这样的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)，则在输出中返回 **-1** 。请注意，结果字符串不得包含不完整的字符串 S1 或 S2。

> 例如**“1111”**可以作为**“11”****“1111”**的合成串，因为它是**“1111”**的 1 次出现，也可以判断为**“11”**的 2 次出现。

**示例:**

> **输入:**S1 =“1010”，S2 =“101010”
> **输出:**10101010101010
> **解释:**结果串为 3 次出现 S1，2 次出现 S2。
> 
> **输入:**S1 =“000”，S2 =“101”
> **输出:** -1
> **说明:**不可能构造这样的字符串。

**方法:**如果有可能做成这样的[弦](https://www.geeksforgeeks.org/category/data-structures/c-strings/)，那么它的长度就是 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 的长度[弦](https://www.geeksforgeeks.org/category/data-structures/c-strings/)T8】S1 和 **S2** 的长度。因为只有这样，才能表述为[弦](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S1** 和 **S2** 的最小倍数。按照以下步骤解决问题:

*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/) **重复(int k，string S)** 并执行以下任务:
    *   将[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **r** 初始化为[空字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)。
    *   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K】**并执行以下步骤:
        *   将[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** 附加到变量**r**中
    *   返回[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **r** 作为答案。
*   将变量 **x** 和 **y** 初始化为[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S1** 和 **S2 的长度。**
*   将变量 **gcd** 初始化为 **x** 和**y**的[GCD](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/)T4
*   调用[函数](https://www.geeksforgeeks.org/functions-in-c/) **重复(y/gcd，s1)** 多次形成[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S1** 并将其存储到变量 **A** 中。
*   调用[函数](https://www.geeksforgeeks.org/functions-in-c/) **重复(x/gcd，s2)** 多次形成[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S2** 并将其存储到变量 **B** 中。
*   如果 **A** 等于 **B、**则打印其中任意一个作为答案，否则打印**“否”。**

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to form the resultant string
string repeat(int k, string S)
{
    string r = "";
    while (k--) {
        r += S;
    }
    return r;
}

// Function to find if any such string
// exists or not. If yes, find it
void find(string s1, string s2)
{
    int x = s1.size(), y = s2.size();

    // GCD of x and y
    int gcd = __gcd(x, y);

    // Form the resultant strings
    string A = repeat(y / gcd, s1);
    string B = repeat(x / gcd, s2);

    // If both the strings are same,
    // then print the answer
    if (A == B) {
        cout << A;
    }
    else {
        cout << "-1";
    }
}

// Driver Code
int main()
{

    // Initializing strings
    string s1 = "1010", s2 = "101010";

    find(s1, s2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {
    public static int GCD(int a, int b)
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
            return GCD(a - b, b);
        return GCD(a, b - a);
    }

    public static String repeat(int k, String S)
    {
        String r = "";
        while (k--!=0) {
            r += S;
        }
        return r;
    }

    // Function to find if any such string
    // exists or not. If yes, find it
    public static void find(String s1, String s2)
    {
        int x = s1.length(), y = s2.length();

        // GCD of x and y
        int gcd = GCD(x, y);

        // Form the resultant strings
        String A = repeat(y / gcd, s1);
        String B = repeat(x / gcd, s2);

        // If both the strings are same,
        // then print the answer
        if (A.equals(B)) {
            System.out.println(A);
        }
        else {
            System.out.println("-1");
        }
    }

    // Driver Code

    public static void main(String[] args)
    {

        // Initializing strings
        String s1 = "1010", s2 = "101010";

        find(s1, s2);
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python program for the above approach
import math

# Function to form the resultant string
def repeat(k, S):
    r = ""
    while (k):
        r += S
        k-=1
    return r

# Function to find if any such string
# exists or not. If yes, find it
def find(s1, s2):

    x = len(s1)
    y = len(s2)

    # GCD of x and y
    gcd = math.gcd(x, y)

    # Form the resultant strings
    A = repeat(y // gcd, s1)
    B = repeat(x // gcd, s2)

    # If both the strings are same,
    # then print answer
    if (A == B):
        print(A)
    else:
        print("-1")

# Driver Code

# Initializing strings
s1 = "1010"
s2 = "101010"

find(s1, s2)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    public static int GCD(int a, int b)
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
            return GCD(a - b, b);
        return GCD(a, b - a);
    }

    public static string repeat(int k, string S)
    {
        string r = "";
        while (k--!=0) {
            r += S;
        }
        return r;
    }

    // Function to find if any such string
    // exists or not. If yes, find it
    public static void find(string s1, string s2)
    {
        int x = s1.Length, y = s2.Length;

        // GCD of x and y
        int gcd = GCD(x, y);

        // Form the resultant strings
        string A = repeat(y / gcd, s1);
        string B = repeat(x / gcd, s2);

        // If both the strings are same,
        // then print the answer
        if (A.Equals(B)) {
            Console.Write(A);
        }
        else {
            Console.Write("-1");
        }
    }

// Driver Code
public static void Main()
{
    // Initializing strings
        string s1 = "1010", s2 = "101010";

        find(s1, s2);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach
function GCD(a, b)
{

    // Everything divides 0
    if (a == 0)
        return b;
    if (b == 0)
        return a;

    // Base case
    if (a == b)
        return a;

    // a is greater
    if (a > b)
        return GCD(a - b, b);

    return GCD(a, b - a);
}

// Function to form the resultant string
function repeat(k, S)
{
    var r = "";
    while (k-- != 0)
    {
        r += S;
    }
    return r;
}

// Function to find if any such string
// exists or not. If yes, find it
function find(s1, s2)
{
    var x = s1.length, y = s2.length;

    // GCD of x and y
    var gcd = GCD(x, y);

    // Form the resultant strings
    var A = repeat(y / gcd, s1);
    var B = repeat(x / gcd, s2);

    // If both the strings are same,
    // then print the answer
    if (A == B)
    {
        document.write(A);
    }
    else
    {
        document.write("-1");
    }
}

// Driver Code

// Initializing strings
var s1 = "1010", s2 = "101010";

find(s1, s2);

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
101010101010
```

***时间复杂度:** O(m + n + log(max(m，n))】*
***辅助空间:** O(n)(用于存储字符串 A & B)*