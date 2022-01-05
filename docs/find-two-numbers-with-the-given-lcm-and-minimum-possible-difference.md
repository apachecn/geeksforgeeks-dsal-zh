# 用给定的 LCM 和最小可能差找到两个数字

> 原文:[https://www . geeksforgeeks . org/find-两个数字加上给定的 lcm 和最小可能差/](https://www.geeksforgeeks.org/find-two-numbers-with-the-given-lcm-and-minimum-possible-difference/)

给定一个整数 **X** ，任务是找到两个整数 **A** 和 **B** ，使得 **LCM(A，B) = X** ，并且 **A** 和 **B** 之间的差值最小。
**示例:**

> **输入:** X = 6
> **输出:** 2 3
> LCM(2，3) = 6 和(3–2)= 1
> 这是最小可能。
> **输入** X = 7
> **输出:** 1 7

**方法:**解决这个问题的一种方法是使用[这篇](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)文章中讨论的方法找到给定数的所有因子，然后找到满足给定条件且具有最小可能差的配对 **(A，B)** 。
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

// Function to find and print the two numbers
void findNums(int x)
{

    int ans;

    // To find the factors
    for (int i = 1; i <= sqrt(x); i++) {

        // To check if i is a factor of x and
        // the minimum possible number
        // satisfying the given conditions
        if (x % i == 0 && lcm(i, x / i) == x) {

            ans = i;
        }
    }
    cout << ans << " " << (x / ans);
}

// Driver code
int main()
{
    int x = 12;

    findNums(x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the LCM of a and b
    static int lcm(int a, int b)
    {
        return (a / __gcd(a, b) * b);
    }

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Function to find and print the two numbers
    static void findNums(int x)
    {

        int ans = -1;

        // To find the factors
        for (int i = 1; i <= Math.sqrt(x); i++)
        {

            // To check if i is a factor of x and
            // the minimum possible number
            // satisfying the given conditions
            if (x % i == 0 && lcm(i, x / i) == x)
            {

                ans = i;
            }
        }
        System.out.print(ans + " " + (x / ans));
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 12;

        findNums(x);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import gcd as __gcd, sqrt, ceil

# Function to return the LCM of a and b
def lcm(a, b):
    return (a // __gcd(a, b) * b)

# Function to find and print the two numbers
def findNums(x):

    ans = 0

    # To find the factors
    for i in range(1, ceil(sqrt(x))):

        # To check if i is a factor of x and
        # the minimum possible number
        # satisfying the given conditions
        if (x % i == 0 and lcm(i, x // i) == x):

            ans = i

    print(ans, (x//ans))

# Driver code
x = 12

findNums(x)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the LCM of a and b
    static int lcm(int a, int b)
    {
        return (a / __gcd(a, b) * b);
    }

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Function to find and print the two numbers
    static void findNums(int x)
    {

        int ans = -1;

        // To find the factors
        for (int i = 1; i <= Math.Sqrt(x); i++)
        {

            // To check if i is a factor of x and
            // the minimum possible number
            // satisfying the given conditions
            if (x % i == 0 && lcm(i, x / i) == x)
            {

                ans = i;
            }
        }
        Console.Write(ans + " " + (x / ans));
    }

    // Driver code
    public static void Main(String[] args)
    {
        int x = 12;

        findNums(x);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the LCM of a and b
function lcm(a,b)
{
     return (a / __gcd(a, b) * b);
}

function __gcd(a,b)
{
     return b == 0 ? a : __gcd(b, a % b);
}

// Function to find and print the two numbers
function findNums(x)
{
    let ans = -1;

        // To find the factors
        for (let i = 1; i <= Math.sqrt(x); i++)
        {

            // To check if i is a factor of x and
            // the minimum possible number
            // satisfying the given conditions
            if (x % i == 0 && lcm(i, Math.floor(x / i)) == x)
            {

                ans = i;
            }
        }
        document.write(ans + " " + Math.floor(x / ans));
}

// Driver code
let x = 12;
findNums(x);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
3 4
```