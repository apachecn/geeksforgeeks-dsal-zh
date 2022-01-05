# 质数递归程序

> 原文:[https://www . geesforgeks . org/recursive-program-prime-number/](https://www.geeksforgeeks.org/recursive-program-prime-number/)

给定一个数 n，检查是否是[质数](https://www.geeksforgeeks.org/prime-numbers/)或者不使用递归。
示例:

```
Input : n = 11
Output : Yes

Input : n = 15
Output : No
```

这个想法是基于[学校检查素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)的方法。

## C++

```
// CPP Program to find whether a Number  
// is Prime or Not using Recursion
#include <bits/stdc++.h>
using namespace std;

// Returns true if n is prime, else
// return false.
// i is current divisor to check.
bool isPrime(int n, int i = 2)
{
    // Base cases
    if (n <= 2)
        return (n == 2) ? true : false;
    if (n % i == 0)
        return false;
    if (i * i > n)
        return true;

    // Check for next divisor
    return isPrime(n, i + 1);
}

// Driver Program
int main()
{
    int n = 15;
    if (isPrime(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java Program to find whether a Number
// is Prime or Not using Recursion
import java.util.*;

class GFG {

    // Returns true if n is prime, else
    // return false.
    // i is current divisor to check.
    static boolean isPrime(int n, int i)
    {

        // Base cases
        if (n <= 2)
            return (n == 2) ? true : false;
        if (n % i == 0)
            return false;
        if (i * i > n)
            return true;

        // Check for next divisor
        return isPrime(n, i + 1);
    }

    // Driver program to test above function
    public static void main(String[] args)
    {

        int n = 15;

        if (isPrime(n, 2))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Python 3 Program to find whether
# a Number is Prime or Not using
# Recursion

# Returns true if n is prime, else
# return false.
# i is current divisor to check.
def isPrime(n, i = 2):

    # Base cases
    if (n <= 2):
        return True if(n == 2) else False
    if (n % i == 0):
        return False
    if (i * i > n):
        return true

    # Check for next divisor
    return isPrime(n, i + 1)

# Driver Program
n = 15
if (isPrime(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# Program to find whether a Number
// is Prime or Not using Recursion
using System;

class GFG
{
    // Returns true if n is prime, else
    // return false.
    // i is current divisor to check.
    static bool isPrime(int n, int i)
    {

        // Base cases
        if (n <= 2)
            return (n == 2) ? true : false;
        if (n % i == 0)
            return false;
        if (i * i > n)
            return true;

        // Check for next divisor
        return isPrime(n, i + 1);
    }

    // Driver code
    static void Main()
    {
    int n = 15;

        if (isPrime(n, 2))
            Console.Write("Yes");
        else
            Console.Write("No");
    }

}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find whether a Number
// is Prime or Not using Recursion

// Returns true if n is prime, else
// return false.
// i is current divisor to check.
function isPrime($n, $i = 2)
{
    // Base cases
    if ($n <= 2)
        return ($n == 2) ? true : false;
    if ($n % $i == 0)
        return false;
    if ($i * $i > $n)
        return true;

    // Check for next divisor
    return isPrime($n, $i + 1);
}

// Driver Code
$n = 15;
if (isPrime($n))
    echo("Yes");
else
    echo("No");

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript  program to find whether a Number
// is Prime or Not using Recursion

    // Returns true if n is prime, else
    // return false.
    // i is current divisor to check.
    function isPrime(n, i)
    {

        // Base cases
        if (n <= 2)
            return (n == 2) ? true : false;
        if (n % i == 0)
            return false;
        if (i * i > n)
            return true;

        // Check for next divisor
        return isPrime(n, i + 1);
    }

// Driver code

       let n = 15;

        if (isPrime(n, 2))
            document.write("Yes");
        else
            document.write("No");

</script>
```

**Output:** 

```
No
```