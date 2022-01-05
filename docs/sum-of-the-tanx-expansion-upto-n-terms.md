# 扩展至 N 项的 Tan(x)之和

> 原文:[https://www . geesforgeks . org/sum-the-tanx-expansion-up-n-terms/](https://www.geeksforgeeks.org/sum-of-the-tanx-expansion-upto-n-terms/)

给定两个整数 **N** 和 **X** 。任务是找到 **tan(x)** 系列到 **N** 项的和。
**该系列:**

> x+x<sup>3</sup>/3+2x<sup>5</sup>/15+17x<sup>7</sup>/315+62x<sup>9</sup>/2835……..

**例:**

> **输入:** N = 6，X = 1
> **输出:**展开的值为 1.55137626113259
> **输入:** N = 4，X = 2
> **输出:**展开的值为 1.52063492063426

**进场:**
谭(x)的展开在这里显示。用一个简单的循环计算每个术语，得到所需的答案。

## C++

```
// CPP program to find tan(x) expansion
#include <bits/stdc++.h>
using namespace std;

// Function to find factorial of a number
int fac(int num)
{
    if (num == 0)
        return 1;

    // To store factorial of a number
    int fact = 1;
    for (int i = 1; i <= num; i++)
        fact = fact * i;

    // Return the factorial of a number
    return fact;
}

// Function to find tan(x) upto n terms
void Tanx_expansion(int terms, int x)
{
    // To store value of the expansion
    double sum = 0;

    for (int i = 1; i <= terms; i += 1) {
        // This loops here calculate Bernoulli number
        // which is further used to get the coefficient
        // in the expansion of tan x
        double B = 0;
        int Bn = 2 * i;
        for (int k = 0; k <= Bn; k++) {
            double temp = 0;
            for (int r = 0; r <= k; r++)
                temp = temp + pow(-1, r) * fac(k) * pow(r, Bn)
                                     / (fac(r) * fac(k - r));

            B = B + temp / ((double)(k + 1));
        }
        sum = sum + pow(-4, i) * (1 - pow(4, i)) * B *
                               pow(x, 2 * i - 1) / fac(2 * i);
    }

    // Print the value of expansion
    cout << setprecision(10) << sum;
}

// Driver code
int main()
{
    int n = 6, x = 1;

    // Function call
    Tanx_expansion(n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find tan(x) expansion
class GFG
{

// Function to find factorial of a number
static int fac(int num)
{
    if (num == 0)
        return 1;

    // To store factorial of a number
    int fact = 1;
    for (int i = 1; i <= num; i++)
        fact = fact * i;

    // Return the factorial of a number
    return fact;
}

// Function to find tan(x) upto n terms
static void Tanx_expansion(int terms, int x)
{
    // To store value of the expansion
    double sum = 0;

    for (int i = 1; i <= terms; i += 1)
    {

        // This loops here calculate Bernoulli number
        // which is further used to get the coefficient
        // in the expansion of tan x
        double B = 0;
        int Bn = 2 * i;
        for (int k = 0; k <= Bn; k++)
        {
            double temp = 0;
            for (int r = 0; r <= k; r++)
                temp = temp + Math.pow(-1, r) * fac(k) *
                              Math.pow(r, Bn) / (fac(r) *
                                                 fac(k - r));

            B = B + temp / ((double)(k + 1));
        }
        sum = sum + Math.pow(-4, i) *
               (1 - Math.pow(4, i)) * B *
                    Math.pow(x, 2 * i - 1) / fac(2 * i);
    }

    // Print the value of expansion
    System.out.printf("%.9f", sum);
}

// Driver code
public static void main(String[] args)
{
    int n = 6, x = 1;

    // Function call
    Tanx_expansion(n, x);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find tan(x) expansion

# Function to find factorial of a number
def fac(num):
    if (num == 0):
        return 1;

    # To store factorial of a number
    fact = 1;
    for i in range(1, num + 1):
        fact = fact * i;

    # Return the factorial of a number
    return fact;

# Function to find tan(x) upto n terms
def Tanx_expansion(terms, x):

    # To store value of the expansion
    sum = 0;

    for i in range(1, terms + 1):

        # This loops here calculate Bernoulli number
        # which is further used to get the coefficient
        # in the expansion of tan x
        B = 0;
        Bn = 2 * i;
        for k in range(Bn + 1):
            temp = 0;
            for r in range(0, k + 1):
                temp = temp + pow(-1, r) * fac(k) \
                    * pow(r, Bn) / (fac(r) * fac(k - r));

            B = B + temp / ((k + 1));

        sum = sum + pow(-4, i) * (1 - pow(4, i)) \
            * B * pow(x, 2 * i - 1) / fac(2 * i);

    # Print the value of expansion
    print("%.9f" %(sum));

# Driver code
if __name__ == '__main__':
    n, x = 6, 1;

    # Function call
    Tanx_expansion(n, x);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to find tan(x) expansion
using System;

class GFG
{

// Function to find factorial of a number
static int fac(int num)
{
    if (num == 0)
        return 1;

    // To store factorial of a number
    int fact = 1;
    for (int i = 1; i <= num; i++)
        fact = fact * i;

    // Return the factorial of a number
    return fact;
}

// Function to find tan(x) upto n terms
static void Tanx_expansion(int terms, int x)
{
    // To store value of the expansion
    double sum = 0;

    for (int i = 1; i <= terms; i += 1)
    {

        // This loop here calculates
        // Bernoulli number which is
        // further used to get the coefficient
        // in the expansion of tan x
        double B = 0;
        int Bn = 2 * i;
        for (int k = 0; k <= Bn; k++)
        {
            double temp = 0;
            for (int r = 0; r <= k; r++)
                temp = temp + Math.Pow(-1, r) * fac(k) *
                              Math.Pow(r, Bn) / (fac(r) *
                                                 fac(k - r));

            B = B + temp / ((double)(k + 1));
        }
        sum = sum + Math.Pow(-4, i) *
               (1 - Math.Pow(4, i)) * B *
                    Math.Pow(x, 2 * i - 1) / fac(2 * i);
    }

    // Print the value of expansion
    Console.Write("{0:F9}", sum);
}

// Driver code
public static void Main(String[] args)
{
    int n = 6, x = 1;

    // Function call
    Tanx_expansion(n, x);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find tan(x) expansion

// Function to find factorial of a number
function fac(num)
{
    if (num == 0)
        return 1;

    // To store factorial of a number
    let fact = 1;
    for (let i = 1; i <= num; i++)
        fact = fact * i;

    // Return the factorial of a number
    return fact;
}

// Function to find tan(x) upto n terms
function Tanx_expansion(terms, x)
{
    // To store value of the expansion
    let sum = 0;

    for (let i = 1; i <= terms; i += 1) {
        // This loops here calculate Bernoulli number
        // which is further used to get the coefficient
        // in the expansion of tan x
        let B = 0;
        let Bn = 2 * i;
        for (let k = 0; k <= Bn; k++) {
            let temp = 0;
            for (let r = 0; r <= k; r++)
                temp = temp + Math.pow(-1, r) * fac(k) * Math.pow(r, Bn)
                                    / (fac(r) * fac(k - r));

            B = B + temp / (k + 1);
        }
        sum =sum + Math.pow(-4, i) * (1 - Math.pow(4, i)) * B *
                            Math.pow(x, 2 * i - 1) / fac(2 * i);
    }

    // Print the value of expansion
    document.write(sum.toFixed(10));
}

// Driver code

    let n = 6, x = 1;

    // Function call
    Tanx_expansion(n, x);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
1.551373344
```