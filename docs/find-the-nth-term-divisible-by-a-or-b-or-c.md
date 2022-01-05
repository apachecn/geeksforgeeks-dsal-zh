# 找到可被 a 或 b 或 c 整除的第 n 项

> 原文:[https://www . geeksforgeeks . org/find-第 n 个术语-可被-a 或-b 或-c 除尽/](https://www.geeksforgeeks.org/find-the-nth-term-divisible-by-a-or-b-or-c/)

给定四个整数 **a** 、 **b** 、 **c** 和 **N** 。任务是找到可被 **a** 、 **b** 或 **c** 整除的 **N <sup>第</sup>** 项。
**例:**

> **输入:** a = 2，b = 3，c = 5，N = 10
> **输出:** 14
> 序列为 2，3，4，5，6，8，9，10，12，14，15，16……
> **输入:** a = 3，b = 5，c = 7，N = 10
> **输出:** 18

**天真方法:**一个简单的方法是遍历所有术语，从 **1** 开始，直到我们找到所需的 **N <sup>th</sup>** 术语，该术语可被**A****b**或 **c** 整除。该解决方案的时间复杂度为 0(N)。
**高效途径:**思路是用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)。在这里，我们可以通过使用以下公式来计算从 **1** 到**数**有多少个数可以被 **a** 、 **b** 或 **c** 整除:**(num/a)+(num/b)+(num/c)–(num/LCM(a，b))–(num/LCM(b，c))–(num/LCM(a，c)) + (num / lcm(a)**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return
// gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return the lcm of a and b
int lcm(int a, int b)
{
    return (a * b) / gcd(a, b);
}

// Function to return the count of numbers
// from 1 to num which are divisible by a, b or c
int divTermCount(int a, int b, int c, int num)
{

    // Calculate number of terms divisible by a and
    // by b and by c then, remove the terms which is are
    // divisible by both a and b, both b and c, both
    // c and a and then add which are divisible by a and
    // b and c
    return ((num / a) + (num / b) + (num / c)
            - (num / lcm(a, b))
            - (num / lcm(b, c))
            - (num / lcm(a, c))
            + (num / lcm(a, lcm(b, c))));
}

// Function to find the nth term
// divisible by a, b or c
// by using binary search
int findNthTerm(int a, int b, int c, int n)
{

    // Set low to 1 and high to max (a, b, c) * n
    int low = 1, high = INT_MAX, mid;

    while (low < high) {
        mid = low + (high - low) / 2;

        // If the current term is less than
        // n then we need to increase low
        // to mid + 1
        if (divTermCount(a, b, c, mid) < n)
            low = mid + 1;

        // If current term is greater than equal to
        // n then high = mid
        else
            high = mid;
    }

    return low;
}

// Driver code
int main()
{
    int a = 2, b = 3, c = 5, n = 10;

    cout << findNthTerm(a, b, c, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return
    // gcd of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    // Function to return the lcm of a and b
    static int lcm(int a, int b)
    {
        return (a * b) / gcd(a, b);
    }

    // Function to return the count of numbers
    // from 1 to num which are divisible by a, b or c
    static int divTermCount(int a, int b, int c, int num)
    {

        // Calculate number of terms divisible by a and
        // by b and by c then, remove the terms which is are
        // divisible by both a and b, both b and c, both
        // c and a and then add which are divisible by a and
        // b and c
        return ((num / a) + (num / b) + (num / c)
                - (num / lcm(a, b))
                - (num / lcm(b, c))
                - (num / lcm(a, c))
                + (num / lcm(a, lcm(b, c))));
    }

    // Function to find the nth term
    // divisible by a, b or c
    // by using binary search
    static int findNthTerm(int a, int b, int c, int n)
    {

        // Set low to 1 and high to max (a, b, c) * n
        int low = 1, high = Integer.MAX_VALUE, mid;

        while (low < high) {
            mid = low + (high - low) / 2;

            // If the current term is less than
            // n then we need to increase low
            // to mid + 1
            if (divTermCount(a, b, c, mid) < n)
                low = mid + 1;

            // If current term is greater than equal to
            // n then high = mid
            else
                high = mid;
        }

        return low;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a = 2, b = 3, c = 5, n = 10;

        System.out.println(findNthTerm(a, b, c, n));

    }
}

// This code is contributed by
// Rajnis09
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return
# gcd of a and b
def gcd(a, b):

    if (a == 0):
        return b

    return gcd(b % a, a)

# Function to return the lcm of a and b
def lcm(a, b):

    return ((a * b) // gcd(a, b))

# Function to return the count of numbers
# from 1 to num which are divisible by a, b or c
def divTermCount(a, b, c, num):

    # Calculate number of terms divisible by a and
    # by b and by c then, remove the terms which is are
    # divisible by both a and b, both b and c, both
    # c and a and then add which are divisible by a and
    # b and c
    return ((num // a) + (num // b) + (num // c)
            - (num // lcm(a, b))
            - (num // lcm(b, c))
            - (num // lcm(a, c))
            + (num // lcm(a, lcm(b, c))))

# Function to find the nth term
# divisible by a, b or c
# by using binary search
def findNthTerm(a, b, c, n):

    # Set low to 1 and high to max (a, b, c) * n
    low = 1
    high = 10**9
    mid=0

    while (low < high):
        mid = low + (high - low) // 2

        # If the current term is less than
        # n then we need to increase low
        # to mid + 1
        if (divTermCount(a, b, c, mid) < n):
            low = mid + 1

        # If current term is greater than equal to
        # n then high = mid
        else:
            high = mid

    return low

# Driver code
a = 2
b = 3
c = 5
n = 10

print(findNthTerm(a, b, c, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return
    // gcd of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    // Function to return the lcm of a and b
    static int lcm(int a, int b)
    {
        return (a * b) / gcd(a, b);
    }

    // Function to return the count of numbers
    // from 1 to num which are divisible by a, b or c
    static int divTermCount(int a, int b, int c, int num)
    {

        // Calculate number of terms divisible by a and
        // by b and by c then, remove the terms which is are
        // divisible by both a and b, both b and c, both
        // c and a and then add which are divisible by a and
        // b and c
        return ((num / a) + (num / b) + (num / c)
                - (num / lcm(a, b))
                - (num / lcm(b, c))
                - (num / lcm(a, c))
                + (num / lcm(a, lcm(b, c))));
    }

    // Function to find the nth term
    // divisible by a, b or c
    // by using binary search
    static int findNthTerm(int a, int b, int c, int n)
    {

        // Set low to 1 and high to max (a, b, c) * n
        int low = 1, high = int.MaxValue, mid;

        while (low < high) {
            mid = low + (high - low) / 2;

            // If the current term is less than
            // n then we need to increase low
            // to mid + 1
            if (divTermCount(a, b, c, mid) < n)
                low = mid + 1;

            // If current term is greater than equal to
            // n then high = mid
            else
                high = mid;
        }

        return low;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int a = 2, b = 3, c = 5, n = 10;

        Console.WriteLine(findNthTerm(a, b, c, n));

    }
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return
// gcd of a and b
function gcd(a, b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return the lcm of a and b
function lcm(a, b)
{
    return parseInt((a * b) / gcd(a, b));
}

// Function to return the count of numbers
// from 1 to num which are divisible by a, b or c
function divTermCount(a, b, c, num)
{

    // Calculate number of terms divisible by a and
    // by b and by c then, remove the terms which is are
    // divisible by both a and b, both b and c, both
    // c and a and then add which are divisible by a and
    // b and c
    return (parseInt(num / a) + parseInt(num / b) +
    parseInt(num / c)
            - parseInt(num / lcm(a, b))
            - parseInt(num / lcm(b, c))
            - parseInt(num / lcm(a, c))
            + parseInt(num / lcm(a, lcm(b, c))));
}

// Function to find the nth term
// divisible by a, b or c
// by using binary search
function findNthTerm(a, b, c, n)
{

    // Set low to 1 and high to max (a, b, c) * n
    let low = 1, high = Number.MAX_VALUE, mid;

    while (low < high) {
        mid = low + parseInt((high - low) / 2);

        // If the current term is less than
        // n then we need to increase low
        // to mid + 1
        if (divTermCount(a, b, c, mid) < n)
            low = mid + 1;

        // If current term is greater than equal to
        // n then high = mid
        else
            high = mid;
    }

    return low;
}

// Driver code
    let a = 2, b = 3, c = 5, n = 10;

    document.write(findNthTerm(a, b, c, n));

</script>
```

**Output:** 

```
14
```