# 检查一个数字是否是费马伪素数

> 原文:[https://www . geesforgeks . org/check-if-a-number-is-Fermat-伪素数/](https://www.geeksforgeeks.org/check-if-a-number-is-fermat-pseudoprime/)

给定一个数字 **N** 和一个基数 **A** 。任务是检查该数是否是基数的费马伪素数。
如果
，数字 N 被称为费马伪素数

> 1.A > 1
> 2。n 是一个复合数
> 3。N 除 A<sup>N-1</sup>–1。

**例:**

> **输入:** N = 645，a = 2
> **输出:** 1
> 645 = 3*5*43，因此它是一个复合数
> 也是 645 除 2^(644)-1
> 因此它是一个费马伪素数。
> **输入:** N = 6，a = 2
> **输出:** 0

**进场:**进场是检查以下情况:

*   检查 A 是否大于 1。
*   [检查 N 是否为复合数](https://www.geeksforgeeks.org/composite-number/)。
*   检查 N 是否除以 A<sup>N-1</sup>–1。

如果上述所有条件都满足，那么 N 是基 a 的费马伪素数
下面是上述方法的实现:

## C++

```
// C++ program to check if N is Fermat pseudoprime
// to the base A or not
#include <bits/stdc++.h>
using namespace std;

// Function to check if the given number is composite
bool checkcomposite(int n)
{
    // Check if there is any divisor of n less than sqrt(n)
    for (int i = 2; i <= sqrt(n); i++) {
        if (n % i == 0)
            return 1;
    }
    return 0;
}

// Effectively calculate (x^y) modulo mod
int power(int x, int y, int mod)
{

    // Initialize result
    int res = 1;

    while (y) {

        // If power is odd, then update the answer
        if (y & 1)
            res = (res * x) % mod;

        // Square the number and reduce
        // the power to its half
        y = y >> 1;
        x = (x * x) % mod;
    }

    // Return the result
    return res;
}

// Function to check for Fermat Pseudoprime
bool Check(int n, int a)
{

    // If it is composite and satisfy Fermat criterion
    if (a>1 && checkcomposite(n) && power(a, n - 1, n) == 1)
        return 1;

    // Else return 0
    return 0;
}

// Driver code
int main()
{

    int N = 645;
    int a = 2;

   //  Function call
    cout << Check(N, a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if N is Fermat pseudoprime
// to the base A or not
class GFG
{

    // Function to check if
    // the given number is composite
    static boolean checkcomposite(int n)
    {
        // Check if there is any divisor of n
        // less than sqrt(n)
        for (int i = 2; i <= Math.sqrt(n); i++)
        {
            if (n % i == 0)
            {
                return true;
            }
        }
        return false;
    }

    // Effectively calculate (x^y) modulo mod
    static int power(int x, int y, int mod)
    {

        // Initialize result
        int res = 1;

        while (y != 0)
        {

            // If power is odd,
            // then update the answer
            if ((y & 1) == 1)
            {
                res = (res * x) % mod;
            }

            // Square the number and reduce
            // the power to its half
            y = y >> 1;
            x = (x * x) % mod;
        }

        // Return the result
        return res;
    }

    // Function to check for Fermat Pseudoprime
    static int Check(int n, int a)
    {

        // If it is composite and
        // satisfy Fermat criterion
        if (a > 1 && checkcomposite(n)
                && power(a, n - 1, n) == 1)
        {
            return 1;
        }

        // Else return 0
        return 0;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 645;
        int a = 2;

        // Function call
        System.out.println(Check(N, a));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to check if N is Fermat pseudoprime
# to the base A or not

from math import sqrt

# Function to check if the given number is composite
def checkcomposite(n):

    # Check if there is any divisor of n less than sqrt(n)
    for i in range(2,int(sqrt(n))+1,1):
        if (n % i == 0):
            return 1
    return 0

# Effectively calculate (x^y) modulo mod
def power(x, y, mod):
    # Initialize result
    res = 1

    while (y):
        # If power is odd, then update the answer
        if (y & 1):
            res = (res * x) % mod

        # Square the number and reduce
        # the power to its half
        y = y >> 1
        x = (x * x) % mod

    # Return the result
    return res

# Function to check for Fermat Pseudoprime
def Check(n,a):
    # If it is composite and satisfy Fermat criterion
    if (a>1 and checkcomposite(n) and power(a, n - 1, n) == 1):
        return 1

    # Else return 0
    return 0

# Driver code
if __name__ == '__main__':
    N = 645
    a = 2

    # Function call
    print(Check(N, a))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to check if N is Fermat pseudoprime
// to the base A or not
using System;

class GFG
{

    // Function to check if
    // the given number is composite
    static bool checkcomposite(int n)
    {
        // Check if there is any divisor of n
        // less than sqrt(n)
        for (int i = 2; i <= Math.Sqrt(n); i++)
        {
            if (n % i == 0)
                return true;
        }
        return false;
    }

    // Effectively calculate (x^y) modulo mod
    static int power(int x, int y, int mod)
    {

        // Initialize result
        int res = 1;

        while (y != 0)
        {

            // If power is odd, then update the answer
            if ((y & 1) == 1)
                res = (res * x) % mod;

            // Square the number and reduce
            // the power to its half
            y = y >> 1;
            x = (x * x) % mod;
        }

        // Return the result
        return res;
    }

    // Function to check for Fermat Pseudoprime
    static int Check(int n, int a)
    {

        // If it is composite and satisfy Fermat criterion
        if (a > 1 && checkcomposite(n) &&
                     power(a, n - 1, n) == 1)
            return 1;

        // Else return 0
        return 0;
    }

    // Driver code
    static public void Main ()
    {
        int N = 645;
        int a = 2;

        // Function call
        Console.WriteLine(Check(N, a));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to check if
// N is Fermat pseudoprime
// to the base A or not

// Function to check if the given
// number is composite
function checkcomposite(n)
{
    // Check if there is any divisor
    // of n less than sqrt(n)
    for (let i = 2; i <= Math.sqrt(n); i++)
    {
        if (n % i == 0)
            return 1;
    }
    return 0;
}

// Effectively calculate (x^y) modulo mod
function power(x, y, mod)
{

    // Initialize result
    let res = 1;

    while (y) {

        // If power is odd, then update the answer
        if (y & 1)
            res = (res * x) % mod;

        // Square the number and reduce
        // the power to its half
        y = y >> 1;
        x = (x * x) % mod;
    }

    // Return the result
    return res;
}

// Function to check for Fermat Pseudoprime
function Check(n, a)
{

    // If it is composite and satisfy
    // Fermat criterion
    if (a>1 && checkcomposite(n) &&
    power(a, n - 1, n) == 1)
        return 1;

    // Else return 0
    return 0;
}

// Driver code

    let N = 645;
    let a = 2;

       //  Function call
    document.write(Check(N, a));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(sqrt(N))