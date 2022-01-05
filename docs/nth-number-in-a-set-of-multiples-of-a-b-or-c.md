# A、B 或 C 的倍数集合中的第 n 个数

> 原文:[https://www . geesforgeks . org/n-a-B-或-c 的倍数集合中的第 n 个数字/](https://www.geeksforgeeks.org/nth-number-in-a-set-of-multiples-of-a-b-or-c/)

给定四个整数 **N** 、 **A** 、 **B** 和 **C** 。任务是打印包含 **A** 、 **B** 或 **C** 倍数的集合中的 **N <sup>第</sup>** 号。
**例:**

> **输入:** A = 2，B = 3，C = 5，N = 8
> **输出:** 10
> 2，3，4，5，6，8，9， **10** ，12，14，…
> **输入:** A = 2，B = 3，C = 5，N = 100
> **输出:** 136

**天真的方法:**从 **1** 开始遍历，直到找到可被**A****B**或 **C** 整除的 **N <sup>第</sup>T7】元素。
**有效方法:**给定一个数，我们可以求出 **A** 、 **B** 或 **C** 的除数。现在，[二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以用来找**N<sup>th</sup>T28】数，这个数可以被 **A** 、 **B** 或者 **C** 整除。
所以，如果数字是 num 那么
**计数=(num/A)+(num/B)+(num/C)–(num/LCM(A，B))–(num/LCM(C，B))–(num/LCM(A，C))–(num/LCM(A，B，C))**
下面是上述方法的实现:**** 

## C++

```
// C++ program to find nth term
// divisible by a, b or c

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

// Function to return the count of integers
// from the range [1, num] which are
// divisible by either a, b or c
long divTermCount(long a, long b, long c, long num)
{
    // Calculate the number of terms divisible by a, b
    // and c then remove the terms which are divisible
    // by both (a, b) or (b, c) or (c, a) and then
    // add the numbers which are divisible by a, b and c
    return ((num / a) + (num / b) + (num / c)
            - (num / ((a * b) / gcd(a, b)))
            - (num / ((c * b) / gcd(c, b)))
            - (num / ((a * c) / gcd(a, c)))
            + (num / ((((a*b)/gcd(a, b))* c) / gcd(((a*b)/gcd(a, b)), c))));
}

// Function for binary search to find the
// nth term divisible by a, b or c
int findNthTerm(int a, int b, int c, long n)
{
    // Set low to 1 and high to LONG_MAX
    long low = 1, high = LONG_MAX, mid;

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
    long a = 2, b = 3, c = 5, n = 100;

    cout << findNthTerm(a, b, c, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find nth term
// divisible by a, b or c
class GFG
{

    // Function to return
    // gcd of a and b
    static long gcd(long a, long b)
    {
        if (a == 0)
        {
            return b;
        }
        return gcd(b % a, a);
    }

    // Function to return the count of integers
    // from the range [1, num] which are
    // divisible by either a, b or c
    static long divTermCount(long a, long b,
                             long c, long num)
    {
        // Calculate the number of terms divisible by a, b
        // and c then remove the terms which are divisible
        // by both (a, b) or (b, c) or (c, a) and then
        // add the numbers which are divisible by a, b and c
        return ((num / a) + (num / b) + (num / c) -
                (num / ((a * b) / gcd(a, b))) -
                (num / ((c * b) / gcd(c, b))) -
                (num / ((a * c) / gcd(a, c))) +
                (num / ((a * b * c) / gcd(gcd(a, b), c))));
    }

    // Function for binary search to find the
    // nth term divisible by a, b or c
    static long findNthTerm(int a, int b, int c, long n)
    {

        // Set low to 1 and high to LONG_MAX
        long low = 1, high = Long.MAX_VALUE, mid;

        while (low < high)
        {
            mid = low + (high - low) / 2;

            // If the current term is less than
            // n then we need to increase low
            // to mid + 1
            if (divTermCount(a, b, c, mid) < n)
            {
                low = mid + 1;
            }

            // If current term is greater than equal to
            // n then high = mid
            else
            {
                high = mid;
            }
        }
        return low;
    }

    // Driver code
    public static void main(String args[])
    {
        int a = 2, b = 3, c = 5, n = 100;

        System.out.println(findNthTerm(a, b, c, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find nth term
# divisible by a, b or c
import sys

# Function to return gcd of a and b
def gcd(a, b):

    if (a == 0):
        return b;

    return gcd(b % a, a);

# Function to return the count of integers
# from the range [1, num] which are
# divisible by either a, b or c
def divTermCount(a, b, c, num):

    # Calculate the number of terms divisible by a, b
    # and c then remove the terms which are divisible
    # by both (a, b) or (b, c) or (c, a) and then
    # add the numbers which are divisible by a, b and c
    return ((num / a) + (num / b) + (num / c) -
                (num / ((a * b) / gcd(a, b))) -
                (num / ((c * b) / gcd(c, b))) -
                (num / ((a * c) / gcd(a, c))) +
                (num / ((a * b * c) / gcd(gcd(a, b), c))));

# Function for binary search to find the
# nth term divisible by a, b or c
def findNthTerm(a, b, c, n):

    # Set low to 1 and high to LONG_MAX
    low = 1; high = sys.maxsize; mid = 0;

    while (low < high):
        mid = low + (high - low) / 2;

        # If the current term is less than
        # n then we need to increase low
        # to mid + 1
        if (divTermCount(a, b, c, mid) < n):
            low = mid + 1;

        # If current term is greater than equal to
        # n then high = mid
        else:
            high = mid;

    return int(low);

# Driver code
a = 2; b = 3; c = 5; n = 100;

print(findNthTerm(a, b, c, n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find nth term
// divisible by a, b or c
using System;

class GFG
{

    // Function to return
    // gcd of a and b
    static long gcd(long a, long b)
    {
        if (a == 0)
        {
            return b;
        }
        return gcd(b % a, a);
    }

    // Function to return the count of integers
    // from the range [1, num] which are
    // divisible by either a, b or c
    static long divTermCount(long a, long b,
                             long c, long num)
    {
        // Calculate the number of terms divisible by a, b
        // and c then remove the terms which are divisible
        // by both (a, b) or (b, c) or (c, a) and then
        // add the numbers which are divisible by a, b and c
        return ((num / a) + (num / b) + (num / c) -
                (num / ((a * b) / gcd(a, b))) -
                (num / ((c * b) / gcd(c, b))) -
                (num / ((a * c) / gcd(a, c))) +
                (num / ((a * b * c) / gcd(gcd(a, b), c))));
    }

    // Function for binary search to find the
    // nth term divisible by a, b or c
    static long findNthTerm(int a, int b,
                            int c, long n)
    {

        // Set low to 1 and high to LONG_MAX
        long low = 1, high = long.MaxValue, mid;

        while (low < high)
        {
            mid = low + (high - low) / 2;

            // If the current term is less than
            // n then we need to increase low
            // to mid + 1
            if (divTermCount(a, b, c, mid) < n)
            {
                low = mid + 1;
            }

            // If current term is greater than equal to
            // n then high = mid
            else
            {
                high = mid;
            }
        }
        return low;
    }

    // Driver code
    public static void Main(String []args)
    {
        int a = 2, b = 3, c = 5, n = 100;

        Console.WriteLine(findNthTerm(a, b, c, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find nth term
// divisible by a, b or c

// Function to return
// gcd of a and b
function gcd( a,  b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

// Function to return the count of integers
// from the range [1, num] which are
// divisible by either a, b or c
function divTermCount( a,  b,  c,  num)
{
    // Calculate the number of terms divisible by a, b
    // and c then remove the terms which are divisible
    // by both (a, b) or (b, c) or (c, a) and then
    // add the numbers which are divisible by a, b and c
    return parseInt(((num / a) + (num / b) + (num / c)
            - (num / ((a * b) / gcd(a, b)))
            - (num / ((c * b) / gcd(c, b)))
            - (num / ((a * c) / gcd(a, c)))
            + (num / ((((a*b)/gcd(a, b))* c)/
            gcd(((a*b)/gcd(a, b)), c)))));
}

// Function for binary search to find the
// nth term divisible by a, b or c
function findNthTerm( a,  b,  c,  n)
{
    // Set low to 1 and high to LONG_MAX
     var low = 1, high = Number.MAX_SAFE_INTEGER , mid;

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

var a = 2, b = 3, c = 5, n = 100;
document.write(parseInt(findNthTerm(a, b, c, n)));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
136
```