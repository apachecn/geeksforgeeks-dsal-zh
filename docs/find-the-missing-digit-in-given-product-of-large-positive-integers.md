# 找出给定的大正整数乘积中缺失的数字

> 原文:[https://www . geesforgeks . org/find-给定大正整数乘积中缺少的数字/](https://www.geeksforgeeks.org/find-the-missing-digit-in-given-product-of-large-positive-integers/)

给定字符串形式的两个大整数 **A** 和 **B** 以及字符串形式的它们的乘积 **C** ，使得乘积的一个数字被 **X** 替换，任务是在乘积 **C** 中找到被替换的数字。

**示例:**

> **输入:** A = 51840，B = 273581，C = 1418243×040
> **输出:** 9
> **说明:**
> 整数 A 和 B 的乘积为 51840 * 273581 = 14182439040。通过与 C 进行比较，可以得出被替换的数字是 9。因此，打印 9。
> 
> **输入:** A = 123456789，B = 987654321，C = 12193263111×635269
> **输出:** 2

**天真方法:**解决给定问题的最简单方法是使用本文[中讨论的方法](https://www.geeksforgeeks.org/multiply-large-numbers-represented-as-strings/)找到两个大整数 A 和 B 的乘积，然后将其与 C 进行比较，以找到结果缺失的数字 **X** 。

***时间复杂度:**O((log<sub>10</sub>A)*(log<sub>10</sub>B))*
***辅助空间:**O(log<sub>10</sub>A+log<sub>10</sub>B)*

**高效方法:**上述方法也可以通过使用以下观察值进行优化:

> 假设 N 是一个整数，N = a<sub>m</sub>a<sub>m-1</sub>a<sub>m-2</sub>……。a<sub>2</sub>a<sub>1</sub>a<sub>0</sub>其中 a <sub>x</sub> 代表 x <sup>第</sup>位数字。现在，N 可以表示为:
> =>N = a<sub>m</sub>* 10<sup>m</sup>+a<sub>m-1</sub>* 10<sup>m-1</sup>+……+a<sub>1</sub>* 10+a<sub>0</sub>
> 
> 在上式中用 11 执行模运算:
> 
> => N (mod 11) =..+a<sub>1</sub>(-1)+a<sub>0</sub>(mod 11)【自 10≦-1(mod 11)】
> =>N(mod 11)= T(mod 11)其中 T = a<sub>0</sub>–<sub>a<sub>1</sub>+a<sub>2</sub>……+(-1)</sub>

因此，从上面的等式中， **A * B = C** 可以转化为 **(A % 11) * (B % 11) = (C % 11)** ，其中等式的左手边是一个常数值，右手边将是一个等式中的一个变量 **X** ，可以求解得到 **X** 的值。在与 **11** 进行模运算后， **X** 可能会有负值，在这种情况下，考虑 **X** 的正值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the replaced digit
// in the product of a*b
int findMissingDigit(string a, string b,
                     string c)
{
    // Keeps track of the sign of the
    // current digit
    int w = 1;

    // Stores the value of a % 11
    int a_mod_11 = 0;

    // Find the value of a mod 11 for
    // large value of a as per the
    // derived formula
    for (int i = a.size() - 1; i >= 0; i--) {
        a_mod_11 = (a_mod_11 + w * (a[i] - '0')) % 11;
        w = w * -1;
    }

    // Stores the value of b % 11
    int b_mod_11 = 0;
    w = 1;

    // Find the value of b mod 11 for
    // large value of a as per the
    // derived formula
    for (int i = b.size() - 1;
         i >= 0; i--) {

        b_mod_11 = (b_mod_11
                    + w * (b[i] - '0'))
                   % 11;
        w = w * -1;
    }

    // Stores the value of c % 11
    int c_mod_11 = 0;

    // Keeps track of the sign of x
    bool xSignIsPositive = true;
    w = 1;

    for (int i = c.size() - 1; i >= 0; i--) {

        // If the current digit is the
        // missing digit, then keep
        // the track of its sign
        if (c[i] == 'x') {
            xSignIsPositive = (w == 1);
        }
        else {
            c_mod_11 = (c_mod_11
                        + w * (c[i] - '0'))
                       % 11;
        }
        w = w * -1;
    }

    // Find the value of x using
    // the derived equation
    int x = ((a_mod_11 * b_mod_11)
             - c_mod_11)
            % 11;

    // Check if x has a negative sign
    if (!xSignIsPositive) {
        x = -x;
    }

    // Return positive equivaluent
    // of x mod 11
    return (x % 11 + 11) % 11;
}

// Driver Code
int main()
{
    string A = "123456789";
    string B = "987654321";
    string C = "12193263111x635269";
    cout << findMissingDigit(A, B, C);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find the replaced digit
    // in the product of a*b
    public static int findMissingDigit(String a, String b, String c)
    {

        // Keeps track of the sign of the
        // current digit
        int w = 1;

        // Stores the value of a % 11
        int a_mod_11 = 0;

        // Find the value of a mod 11 for
        // large value of a as per the
        // derived formula
        for (int i = a.length() - 1; i >= 0; i--) {
            a_mod_11 = (a_mod_11 + w * (a.charAt(i) - '0')) % 11;
            w = w * -1;
        }

        // Stores the value of b % 11
        int b_mod_11 = 0;
        w = 1;

        // Find the value of b mod 11 for
        // large value of a as per the
        // derived formula
        for (int i = b.length() - 1; i >= 0; i--) {

            b_mod_11 = (b_mod_11 + w * (b.charAt(i) - '0')) % 11;
            w = w * -1;
        }

        // Stores the value of c % 11
        int c_mod_11 = 0;

        // Keeps track of the sign of x
        boolean xSignIsPositive = true;
        w = 1;

        for (int i = c.length() - 1; i >= 0; i--) {

            // If the current digit is the
            // missing digit, then keep
            // the track of its sign
            if (c.charAt(i) == 'x') {
                xSignIsPositive = (w == 1);
            } else {
                c_mod_11 = (c_mod_11 + w * (c.charAt(i) - '0')) % 11;
            }
            w = w * -1;
        }

        // Find the value of x using
        // the derived equation
        int x = ((a_mod_11 * b_mod_11) - c_mod_11) % 11;

        // Check if x has a negative sign
        if (!xSignIsPositive) {
            x = -x;
        }

        // Return positive equivaluent
        // of x mod 11
        return (x % 11 + 11) % 11;
    }

    // Driver Code
    public static void main(String args[]) {
        String A = "123456789";
        String B = "987654321";
        String C = "12193263111x635269";
        System.out.println(findMissingDigit(A, B, C));

    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python3 Program to implement the above approach

# Function to find the replaced digit
# in the product of a*b
def findMissingDigit(a, b, c):

    # Keeps track of the sign of the
    # current digit
    w = 1

    # Stores the value of a % 11
    a_mod_11 = 0

    # Find the value of a mod 11 for
    # large value of a as per the
    # derived formula
    for i in range(len(a) - 1, -1, -1):
        a_mod_11 = (a_mod_11 + w * (ord(a[i]) - ord('0'))) % 11
        w = w * -1

    # Stores the value of b % 11
    b_mod_11 = 0
    w = 1

    # Find the value of b mod 11 for
    # large value of a as per the
    # derived formula
    for i in range(len(b) - 1, -1, -1):
        b_mod_11 = (b_mod_11 + w * (ord(b[i]) - ord('0'))) % 11
        w = w * -1

    # Stores the value of c % 11
    c_mod_11 = 0

    # Keeps track of the sign of x
    xSignIsPositive = True
    w = 1

    for i in range(len(c) - 1, -1, -1):
        # If the current digit is the
        # missing digit, then keep
        # the track of its sign
        if (c[i] == 'x'):
            xSignIsPositive = (w == 1)
        else:
            c_mod_11 = (c_mod_11 + w * (ord(c[i]) - ord('0'))) % 11
        w = w * -1

    # Find the value of x using
    # the derived equation
    x = ((a_mod_11 * b_mod_11) - c_mod_11) % 11

    # Check if x has a negative sign
    if (not xSignIsPositive):
        x = -x

    # Return positive equivaluent
    # of x mod 11
    return (x % 11 + 11) % 11

A = "123456789"
B = "987654321"
C = "12193263111x635269"
print(findMissingDigit(A, B, C))

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the replaced digit
// in the product of a*b
static int findMissingDigit(string a, string b,
                     string c)
{

    // Keeps track of the sign of the
    // current digit
    int w = 1;

    // Stores the value of a % 11
    int a_mod_11 = 0;

    // Find the value of a mod 11 for
    // large value of a as per the
    // derived formula
    for (int i = a.Length - 1; i >= 0; i--) {
        a_mod_11 = (a_mod_11 + w * ((int)a[i] - 48)) % 11;
        w = w * -1;
    }

    // Stores the value of b % 11
    int b_mod_11 = 0;
    w = 1;

    // Find the value of b mod 11 for
    // large value of a as per the
    // derived formula
    for (int i = b.Length - 1;
         i >= 0; i--) {

        b_mod_11 = (b_mod_11
                    + w * ((int)b[i] - 48))
                   % 11;
        w = w * -1;
    }

    // Stores the value of c % 11
    int c_mod_11 = 0;

    // Keeps track of the sign of x
    bool xSignIsPositive = true;
    w = 1;

    for (int i = c.Length - 1; i >= 0; i--) {

        // If the current digit is the
        // missing digit, then keep
        // the track of its sign
        if (c[i] == 'x') {
            xSignIsPositive = (w == 1);
        }
        else {
            c_mod_11 = (c_mod_11
                        + w * ((int)c[i] - '0'))
                       % 11;
        }
        w = w * -1;
    }

    // Find the value of x using
    // the derived equation
    int x = ((a_mod_11 * b_mod_11)
             - c_mod_11)
            % 11;

    // Check if x has a negative sign
    if (xSignIsPositive == false) {
        x = -x;
    }

    // Return positive equivaluent
    // of x mod 11
    return (x % 11 + 11) % 11;
}

// Driver Code
public static void Main()
{
    string A = "123456789";
    string B = "987654321";
    string C = "12193263111x635269";
    Console.Write(findMissingDigit(A, B, C));
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the replaced digit
        // in the product of a*b
        function findMissingDigit(a, b,
            c)
        {
            // Keeps track of the sign of the
            // current digit
            let w = 1;

            // Stores the value of a % 11
            let a_mod_11 = 0;

            // Find the value of a mod 11 for
            // large value of a as per the
            // derived formula
            for (let i = a.length - 1; i >= 0; i--) {
                a_mod_11 = (a_mod_11 + w * (a[i].charCodeAt(0) - '0'.charCodeAt(0))) % 11;
                w = w * -1;
            }

            // Stores the value of b % 11
            let b_mod_11 = 0;
            w = 1;

            // Find the value of b mod 11 for
            // large value of a as per the
            // derived formula
            for (let i = b.length - 1;
                i >= 0; i--) {

                b_mod_11 = (b_mod_11
                    + w * (b[i].charCodeAt(0) - '0'.charCodeAt(0)))
                    % 11;
                w = w * -1;
            }

            // Stores the value of c % 11
            let c_mod_11 = 0;

            // Keeps track of the sign of x
            let xSignIsPositive = true;
            w = 1;

            for (let i = c.length - 1; i >= 0; i--) {

                // If the current digit is the
                // missing digit, then keep
                // the track of its sign
                if (c[i] == 'x') {
                    xSignIsPositive = (w == 1);
                }
                else {
                    c_mod_11 = (c_mod_11
                        + w * (c[i].charCodeAt(0) - '0'.charCodeAt(0)))
                        % 11;
                }
                w = w * -1;
            }

            // Find the value of x using
            // the derived equation
            let x = ((a_mod_11 * b_mod_11)
                - c_mod_11)
                % 11;

            // Check if x has a negative sign
            if (!xSignIsPositive) {
                x = -x;
            }

            // Return positive equivaluent
            // of x mod 11
            return (x % 11 + 11) % 11;
        }

        // Driver Code
        let A = "123456789";
        let B = "987654321";
        let C = "12193263111x635269";
        document.write(findMissingDigit(A, B, C));

// This code is contributed by Potta Lokesh
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(log<sub>10</sub>A+log<sub>10</sub>B)*
***辅助空间:** O(1)*