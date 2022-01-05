# 将给定的十进制数转换成不可约分数

> 原文:[https://www . geesforgeks . org/convert-given-decimal-number-in-an-不可约分数/](https://www.geeksforgeeks.org/convert-given-decimal-number-into-an-irreducible-fraction/)

给定一个十进制数 **N** ，任务是将 N 转换成等价的不可约分数。

> 不可约分数是分子和分母都是同素的分数，即它们除了 1 之外没有其他公约数。

**示例:**

> **输入:** N = 4.50
> **输出:** 9/2
> **说明:**
> 小数点后 9/2 写成 4.5
> 
> **输入:** N = 0.75
> **输出:** 3/4
> **说明:**
> 小数点后 3/4 写成 0.75

**方法:**按照下面给出的步骤解决问题。

*   获取十进制数“n”的**整数值**和**小数部分**。
*   考虑精度值为 10 <sup>9</sup> 将小数的小数部分转换为整数等价物。
*   计算分数部分的积分当量和精度值的 GCD。
*   用分数部分的积分当量除以 GCD 值计算**分子**。通过将精度值除以 GCD 值来计算**分母**。
*   从获得的混合馏分中，将其转化为不适当的馏分。

> 例如 N = 4.50，整数值= 4，小数部分= 0.50
> 
> 考虑精度值为(10 <sup>9</sup> )即精度值= 1000000000
> 
> 计算 GCD(0.50 * 10 <sup>9</sup> ，10<sup>9</sup>)= 50000000
> 
> 计算**分子** = (0.50

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive function to
// return GCD of a and b
long long gcd(long long a, long long b)
{
    if (a == 0)
        return b;
    else if (b == 0)
        return a;
    if (a < b)
        return gcd(a, b % a);
    else
        return gcd(b, a % b);
}

// Function to convert decimal to fraction
void decimalToFraction(double number)
{
    // Fetch integral value of the decimal
    double intVal = floor(number);

    // Fetch fractional part of the decimal
    double fVal = number - intVal;

    // Consider precision value to
    // convert fractional part to
    // integral equivalent
    const long pVal = 1000000000;

    // Calculate GCD of integral
    // equivalent of fractional
    // part and precision value
    long long gcdVal
        = gcd(round(fVal * pVal), pVal);

    // Calculate num and deno
    long long num
        = round(fVal * pVal) / gcdVal;
    long long deno = pVal / gcdVal;

    // Print the fraction
    cout << (intVal * deno) + num
         << "/" << deno << endl;
}

// Driver Code
int main()
{
    double N = 4.5;

    decimalToFraction(N);

    return 0;
}
```

## C

```
// C implementation of the above approach
#include <math.h>
#include <stdio.h>

int gcfFinder(int a, int b)
{ // gcf finder
    int gcf = 1;
    for (int i = 1; i <= a && i <= b; i++)
    {
        if (a % i == 0 && b % i == 0)
        {
            gcf = i;
        }
    }
    return gcf;
}

int shortform(int* a, int* b)
{
    for (int i = 2; i <= *a && i <= *b; i++)
    {
        if (*a % i == 0 && *b % i == 0)
        {
            *a = *a / i;
            *b = *b / i;
        }
    }
    return 0;
}

// Driver Code
int main(void)
{
    // converting decimal into fraction.
    double a = 4.50;

    int c = 10000;
    double b = (a - floor(a)) * c;
    int d = (int)floor(a) * c + (int)(b + .5f);

    while (1)
    {
        if (d % 10 == 0)
        {
            d = d / 10;
            c = c / 10;
        }
        else
            break;
    }
    int* i = &d;
    int* j = &c;
    int t = 0;
    while (t != 1)
    {
        int gcf = gcfFinder(d, c);
        if (gcf == 1)
        {
            printf("%d/%d\n", d, c);
            t = 1;
        }
        else
        {
            shortform(i, j);
        }
    }
    return 0;
}
// this code is contributed by harsh sinha username-
// harshsinha03
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Recursive function to
// return GCD of a and b
static long gcd(long a, long b)
{
    if (a == 0)
        return b;
    else if (b == 0)
        return a;
    if (a < b)
        return gcd(a, b % a);
    else
        return gcd(b, a % b);
}

// Function to convert decimal to fraction
static void decimalToFraction(double number)
{

    // Fetch integral value of the decimal
    double intVal = Math.floor(number);

    // Fetch fractional part of the decimal
    double fVal = number - intVal;

    // Consider precision value to
    // convert fractional part to
    // integral equivalent
    final long pVal = 1000000000;

    // Calculate GCD of integral
    // equivalent of fractional
    // part and precision value
    long gcdVal = gcd(Math.round(
                      fVal * pVal), pVal);

    // Calculate num and deno
    long num = Math.round(fVal * pVal) / gcdVal;
    long deno = pVal / gcdVal;

    // Print the fraction
    System.out.println((long)(intVal * deno) +
                           num + "/" + deno);
}

// Driver Code
public static void main(String s[])
{
    double N = 4.5;
    decimalToFraction(N);
}   
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import floor

# Recursive function to
# return GCD of a and b
def gcd(a, b):

    if (a == 0):
        return b
    elif (b == 0):
        return a
    if (a < b):
        return gcd(a, b % a)
    else:
        return gcd(b, a % b)

# Function to convert decimal to fraction
def decimalToFraction(number):

    # Fetch integral value of the decimal
    intVal = floor(number)

    # Fetch fractional part of the decimal
    fVal = number - intVal

    # Consider precision value to
    # convert fractional part to
    # integral equivalent
    pVal = 1000000000

    # Calculate GCD of integral
    # equivalent of fractional
    # part and precision value
    gcdVal = gcd(round(fVal * pVal), pVal)

    # Calculate num and deno
    num= round(fVal * pVal) // gcdVal
    deno = pVal // gcdVal

    # Print the fraction
    print((intVal * deno) + num, "/", deno)

# Driver Code
if __name__ == '__main__':

    N = 4.5

    decimalToFraction(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Recursive function to
// return GCD of a and b
static long gcd(long a, long b)
{
    if (a == 0)
        return b;
    else if (b == 0)
        return a;
    if (a < b)
        return gcd(a, b % a);
    else
        return gcd(b, a % b);
}

// Function to convert decimal to fraction
static void decimalToFraction(double number)
{

    // Fetch integral value of the decimal
    double intVal = Math.Floor(number);

    // Fetch fractional part of the decimal
    double fVal = number - intVal;

    // Consider precision value to
    // convert fractional part to
    // integral equivalent
    long pVal = 1000000000;

    // Calculate GCD of integral
    // equivalent of fractional
    // part and precision value
    long gcdVal = gcd((long)Math.Round(
                    fVal * pVal), pVal);

    // Calculate num and deno
    long num = (long)Math.Round(fVal * pVal) / gcdVal;
    long deno = pVal / gcdVal;

    // Print the fraction
    Console.WriteLine((long)(intVal * deno) +
                          num + "/" + deno);
}

// Driver Code
public static void Main(String []s)
{
    double N = 4.5;

    decimalToFraction(N);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Recursive function to
// return GCD of a and b
function gcd(a, b)
{
    if (a == 0)
        return b;
    else if (b == 0)
        return a;
    if (a < b)
        return gcd(a, b % a);
    else
        return gcd(b, a % b);
}

// Function to convert decimal to fraction
function decimalToFraction(number)
{

    // Fetch letegral value of the decimal
    let letVal = Math.floor(number);

    // Fetch fractional part of the decimal
    let fVal = number - letVal;

    // Consider precision value to
    // convert fractional part to
    // letegral equivalent
    let pVal = 1000000000;

    // Calculate GCD of letegral
    // equivalent of fractional
    // part and precision value
    let gcdVal = gcd(Math.round(
                      fVal * pVal), pVal);

    // Calculate num and deno
    let num = Math.round(fVal * pVal) / gcdVal;
    let deno = pVal / gcdVal;

    // Print the fraction
    document.write((letVal * deno) +
                           num + "/" + deno);
}

    // Driver Code

    let N = 4.5;
    decimalToFraction(N);

</script>
```

**Output:** 

```
9/2
```

***时间复杂度:** O(log min(a，b))*
***辅助空间:** O(1)*