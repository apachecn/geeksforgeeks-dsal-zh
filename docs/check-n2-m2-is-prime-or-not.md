# 检查 n^2-m^2 是否是质数

> 原文:[https://www.geeksforgeeks.org/check-n2-m2-is-prime-or-not/](https://www.geeksforgeeks.org/check-n2-m2-is-prime-or-not/)

给定两个整数 n 和 m，检查 n^2-m^2 是否是素数。n 和 m 可以非常大。

**示例:**

```
Input : n = 6, m = 5
Output : YES

Input : n = 16, m = 13
Output : NO
```

一个简单的解决方案是首先计算 n^2-m^2，然后检查它是否是质数。n^2–m^2 可能非常大–它甚至可能不适合 64 位整数。检查它的素性当然不能天真地进行。

一个更好的解决方案是将 n^2-m^2 表示为(n-m)(n+m)。当且仅当 n-m = 1 且 n+m 是素数时，这是素数。

## C++

```
// CPP program to find n^2 - m^2
// is prime or not.
#include <bits/stdc++.h>
using namespace std;

// Check a number is prime or not
bool isprime(int x)
{
    // run a loop upto square of given number
    for (int i = 2; i * i <= x; i++)
        if (x % i == 0)
            return false;
    return true;
}

// Check if n^2 - m^2 is prime
bool isNSqMinusnMSqPrime(int m, int n)
{
    if (n - m == 1 and isprime(m + n))
        return true;
    else
        return false;
}

// Driver code
int main()
{
    int m = 13, n = 16;
    if (isNSqMinusnMSqPrime(m, n))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n^2 - m^2
// is prime or not.

class GFG
{
        // Check if a number is prime or not
        static boolean isprime(int x)
        {
            // run a loop upto square of given number
            for (int i = 2; i * i <= x; i++)
                if (x % i == 0)
                    return false;
            return true;
        }

        // Check if n^2 - m^2 is prime
        static boolean isNSqMinusnMSqPrime(int m, int n)
        {
            if (n - m == 1 && isprime(m + n))
                return true;
            else
                return false;
        }

        // Driver code
        public static void  main(String [] args)
        {
            int m = 13, n = 16;
            if (isNSqMinusnMSqPrime(m, n))
                System.out.println("YES");
            else
                System.out.println("NO");

        }
}

// This code is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python program to find n^2 - m^2
# is prime or not.

# Check a number is prime or not
def isprime(x):

    # run a loop upto square
    # of given number
    for i in range(2, math.sqrt(x)):
        if (x % i == 0) :
            return False;
    return True;

# Check if n^2 - m^2 is prime
def isNSqMinusnMSqPrime( m, n):

    if (n - m == 1 and isprime(m + n)):
        return True;
    else:
        return False;

# Driver code
m = 13;
n = 16;
if (isNSqMinusnMSqPrime(m, n)) :
    print ( "YES");
else:
    print ("NO");

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# program to find n^2 - m^2
// is prime or not.
using System;

class GFG
{
// Check if a number is prime or not
static bool isprime(int x)
{
    // run a loop upto square
    // of given number
    for (int i = 2; i * i <= x; i++)
        if (x % i == 0)
            return false;
    return true;
}

// Check if n^2 - m^2 is prime
static bool isNSqMinusnMSqPrime(int m,
                                int n)
{
    if (n - m == 1 && isprime(m + n))
        return true;
    else
        return false;
}

// Driver code
public static void Main()
{
    int m = 13, n = 16;
    if (isNSqMinusnMSqPrime(m, n))
        Console.Write("YES");
    else
        Console.Write("NO");
}
}

// This code is contributed
// by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to find n^2 - m^2
// is prime or not.

// Check a number is prime or not
function isprime($x)
{
    // run a loop upto square
    // of given number
    for ( $i = 2; $i * $i <= $x; $i++)
        if ($x % i == 0)
            return false;
    return true;
}

// Check if n^2 - m^2 is prime
function isNSqMinusnMSqPrime($m, $n)
{
    if ($n - $m == 1 and isprime($m + $n))
        return true;
    else
        return false;
}

// Driver code
$m = 13; $n = 16;
if (isNSqMinusnMSqPrime($m, $n))
    echo "YES";
else
    echo "NO";

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// JavaScript program to find n^2 - m^2
// is prime or not.

// Check if a number is prime or not
function isprime(x)
{

    // Run a loop upto square of given number
    for(var i = 2; i * i <= x; i++)
        if (x % i == 0)
            return false;

    return true;
}

// Check if n^2 - m^2 is prime
function isNSqMinusnMSqPrime(m, n)
{
    if (n - m == 1 && isprime(m + n))
        return true;
    else
        return false;
}

// Driver Code
var m = 13, n = 16;

if (isNSqMinusnMSqPrime(m, n))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by Khushboogoyal499

</script>
```

**输出:**

```
NO
```

**时间复杂度:** O(sqrt(n+m))