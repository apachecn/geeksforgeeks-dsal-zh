# 不使用算术运算符检查 n 是否能被 2 的幂整除

> 原文:[https://www . geesforgeks . org/check-n-除数-2-不使用算术运算符/](https://www.geeksforgeeks.org/check-n-divisible-power-2-without-using-arithmetic-operators/)

给定两个正整数 **n** 和 **m** 。问题是在不使用算术运算符的情况下，检查 **n** 是否可被 **2 <sup>m</sup>** 整除。

示例:

```
Input : n = 8, m = 2
Output : Yes

Input : n = 14, m = 3
Output : No
```

**方法:**如果一个数可以被 2 整除，那么它的最低有效位(LSB)设置为 0，如果可以被 4 整除，那么两个 LSB 设置为 0，如果可以被 8 整除，那么三个 LSB 设置为 0，以此类推。记住这一点，如果**(n&((1<<m)–1)**等于 0，则数字 **n** 可被**2<sup>m</sup>T13】整除。**

## **c++**

```
// C++ implementation to check whether n
// is divisible by pow(2, m)
#include <bits/stdc++.h>

using namespace std;

// function to check whether n
// is divisible by pow(2, m)
bool isDivBy2PowerM(unsigned int n,
                    unsigned int m)
{
    // if expression results to 0, then
    // n is divisible by pow(2, m)
    if ((n & ((1 << m) - 1)) == 0)
        return true;

    // n is not divisible
    return false;
}

// Driver program to test above
int main()
{
    unsigned int n = 8, m = 2;
    if (isDivBy2PowerM(n, m))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## **Java**

```
// JAVA Code for Check if n is divisible 
// by power of 2 without using arithmetic
// operators
import java.util.*;

class GFG {

    // function to check whether n
    // is divisible by pow(2, m)
    static boolean isDivBy2PowerM(int n,
                                    int m)
    {
        // if expression results to 0, then
        // n is divisible by pow(2, m)
        if ((n & ((1 << m) - 1)) == 0)
            return true;

        // n is not divisible
        return false;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
            int n = 8, m = 2;

            if (isDivBy2PowerM(n, m))
                System.out.println("Yes");
            else
                System.out.println("No");
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## **python 3**

**T2**

## **c#**

**T31

```
// C# Code for Check if n is divisible
// by power of 2 without using arithmetic
// operators
using System;

class GFG {

    // function to check whether n
    // is divisible by pow(2, m)
    static bool isDivBy2PowerM(int n, int m)
    {
        // if expression results to 0, then
        // n is divisible by pow(2, m)
        if ((n & ((1 << m) - 1)) == 0)
            return true;

        // n is not divisible
        return false;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int n = 8, m = 2;

        if (isDivBy2PowerM(n, m))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Sam007
```** **PHPT4T37】JavascriptT40**

**输出:**

```
Yes
```