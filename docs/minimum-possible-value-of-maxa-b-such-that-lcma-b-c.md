# 最大值(A，B)的最小可能值，使得 LCM(A，B) = C

> 原文:[https://www . geeksforgeeks . org/maxa-b-so-lcma-b-c/](https://www.geeksforgeeks.org/minimum-possible-value-of-maxa-b-such-that-lcma-b-c/)

给定一个整数 **C** ，任务是找到 **max(A，B)** 的最小可能值，使得 **LCM(A，B) = C** 。
**举例:**

> **输入:** C = 6
> **输出:** 3
> 最大值(1，6) = 6
> 最大值(2，3) = 3
> 和最小值(6，3) = 3
> **输入:** C = 9
> **输出:** 9

**方法:**解决这个问题的一个方法是使用[这篇](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)文章中讨论的方法找到给定数的所有因子，然后找到满足给定条件的对 **(A，B)** ，并取这些对的最大值的整体最小值。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the LCM of a and b
int lcm(int a, int b)
{
    return (a / __gcd(a, b) * b);
}

// Function to return the minimized value
int getMinValue(int c)
{
    int ans = INT_MAX;

    // To find the factors
    for (int i = 1; i <= sqrt(c); i++) {

        // To check if i is a factor of c and
        // the minimum possible number
        // satisfying the given conditions
        if (c % i == 0 && lcm(i, c / i) == c) {

            // Update the answer
            ans = min(ans, max(i, c / i));
        }
    }
    return ans;
}

// Driver code
int main()
{
    int c = 6;

    cout << getMinValue(c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class Solution
{
    // Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
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
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }

    // Function to return the LCM of a and b
    static int lcm(int a, int b)
    {
        return (a / __gcd(a, b) * b);
    }

    // Function to return the minimized value
    static int getMinValue(int c)
    {
        int ans = Integer.MAX_VALUE;

        // To find the factors
        for (int i = 1; i <= Math.sqrt(c); i++)
        {

            // To check if i is a factor of c and
            // the minimum possible number
            // satisfying the given conditions
            if (c % i == 0 && lcm(i, c / i) == c)
            {

                // Update the answer
                ans = Math.min(ans, Math.max(i, c / i));
            }
        }
        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int c = 6;

        System.out.println(getMinValue(c));
    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python implementation of the approach
import sys

# Recursive function to return gcd of a and b
def __gcd(a, b):

    # Everything divides 0
    if (a == 0):
        return b;
    if (b == 0):
        return a;

    # base case
    if (a == b):
        return a;

    # a is greater
    if (a > b):
        return __gcd(a - b, b);
    return __gcd(a, b - a);

# Function to return the LCM of a and b
def lcm(a, b):
    return (a / __gcd(a, b) * b);

# Function to return the minimized value
def getMinValue(c):
    ans = sys.maxsize;

    # To find the factors
    for i in range(1, int(pow(c, 1/2)) + 1):

        # To check if i is a factor of c and
        # the minimum possible number
        # satisfying the given conditions
        if (c % i == 0 and lcm(i, c / i) == c):

            # Update the answer
            ans = min(ans, max(i, c / i));
    return int(ans);

# Driver code
if __name__ == '__main__':
    c = 6;

    print(getMinValue(c));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
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
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }

    // Function to return the LCM of a and b
    static int lcm(int a, int b)
    {
        return (a / __gcd(a, b) * b);
    }

    // Function to return the minimized value
    static int getMinValue(int c)
    {
        int ans = int.MaxValue;

        // To find the factors
        for (int i = 1; i <= Math.Sqrt(c); i++)
        {

            // To check if i is a factor of c and
            // the minimum possible number
            // satisfying the given conditions
            if (c % i == 0 && lcm(i, c / i) == c)
            {

                // Update the answer
                ans = Math.Min(ans, Math.Max(i, c / i));
            }
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int c = 6;

        Console.WriteLine(getMinValue(c));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Recursive function to return gcd of a and b
function __gcd(a , b)
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
        return __gcd(a - b, b);
    return __gcd(a, b - a);
}

// Function to return the LCM of a and b
function lcm(a , b)
{
    return (a / __gcd(a, b) * b);
}

// Function to return the minimized value
function getMinValue(c)
{
    var ans = Number.MAX_VALUE;

    // To find the factors
    for (i = 1; i <= Math.sqrt(c); i++)
    {

        // To check if i is a factor of c and
        // the minimum possible number
        // satisfying the given conditions
        if (c % i == 0 && lcm(i, c / i) == c)
        {

            // Update the answer
            ans = Math.min(ans, Math.max(i, c / i));
        }
    }
    return ans;
}

// Driver code

var c = 6;

document.write(getMinValue(c));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
3
```