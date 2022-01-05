# 平方自由数

> 原文:[https://www.geeksforgeeks.org/square-free-number/](https://www.geeksforgeeks.org/square-free-number/)

给定一个数字，检查它是否是平方自由的。如果一个数没有质因数不止一次地除以它，也就是说，一个质因数除以 n 的最大幂是 1，那么这个数就是平方自由数。前几个平方自由数是 1、2、3、5、6、7、10、11、13、14、15、17、19、21、22、23、26、29、30、31、33、34、35、37、38、39……
示例:

```
Input : n = 10
Output : Yes
10 can be factorized as 2*5\. Since
no prime factor appears more than
once, it is a square free number.

Input :  n = 20
Output : No
20 can be factorized as 2 * 2 * 5.
Since prime factor appears more than
once, it is not a square free number.
```

思路很简单，我们一个个[找到所有质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。对于每个质因数，我们检查它的平方是否也除以 n。如果是，那么我们返回 false。最后，如果我们没有找到一个能被不止一次整除的质因数，我们就返回 false。

## C++

```
// C++ Program to print
// all prime factors
# include <bits/stdc++.h>
using namespace std;

// Returns true if n is a square free
// number, else returns false.
bool isSquareFree(int n)
{
    if (n % 2 == 0)
       n = n/2;

    // If 2 again divides n, then n is
    // not a square free number.
    if (n % 2 == 0)
       return false;

    // n must be odd at this point.  So we can 
    // skip one element (Note i = i +2)
    for (int i = 3; i <= sqrt(n); i = i+2)
    {
        // Check if i is a prime factor
        if (n % i == 0)
        {
           n = n/i;

           // If i again divides, then
           // n is not square free
           if (n % i == 0)
               return false;
        }
    }

    return true;
}

/* Driver program to test above function */
int main()
{
    int n = 10;
    if (isSquareFree(n))
       cout << "Yes";
    else
       cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print
// all prime factors

class GFG {

    // Returns true if n is a square free
    // number, else returns false.
    static boolean isSquareFree(int n)
    {
        if (n % 2 == 0)
        n = n / 2;

        // If 2 again divides n, then n is
        // not a square free number.
        if (n % 2 == 0)
        return false;

        // n must be odd at this point. So we can
        // skip one element (Note i = i +2)
        for (int i = 3; i <= Math.sqrt(n); i = i + 2)
        {
            // Check if i is a prime factor
            if (n % i == 0)
            {
                n = n / i;

                // If i again divides, then
                // n is not square free
                if (n % i == 0)
                    return false;
            }
        }

        return true;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int n = 10;
        if (isSquareFree(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by prerna saini.
```

## 蟒蛇 3

```
# Python3 Program to print
# all prime factors
from math import sqrt

# Returns true if n is
# a square free number,
# else returns false.
def isSquareFree(n):

    if n % 2 == 0:
        n = n / 2

    # If 2 again divides n,
    # then n is not a square
    # free number.
    if n % 2 == 0:
        return False

    # n must be odd at this
    # point. So we can skip
    # one element
    # (Note i = i + 2)
    for i in range(3, int(sqrt(n) + 1)):

        # Check if i is a prime
        # factor
        if n % i == 0:
            n = n / i

        # If i again divides, then
        # n is not square free
        if n % i == 0:
            return False
    return True

# Driver program
n = 10

if isSquareFree(n):
    print ("Yes")
else:
    print ("No")

# This code is contributed by Shreyanshi Arun.
```

## C#

```
// C# Program to print
// all prime factors
using System;

class GFG {

    // Returns true if n is a square free
    // number, else returns false.
    static bool isSquareFree(int n)
    {
        if (n % 2 == 0)
        n = n / 2;

        // If 2 again divides n, then n is
        // not a square free number.
        if (n % 2 == 0)
        return false;

        // n must be odd at this point. So we can
        // skip one element (Note i = i +2)
        for (int i = 3; i <= Math.Sqrt(n); i = i + 2)
        {
            // Check if i is a prime factor
            if (n % i == 0)
            {
                n = n / i;

                // If i again divides, then
                // n is not square free
                if (n % i == 0)
                    return false;
            }
        }

        return true;
    }

    // Driver program
    public static void Main()
    {
        int n = 10;
        if (isSquareFree(n))
        Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print
// all prime factors

// Returns true if n is a square free
// number, else returns false.
function isSquareFree($n)
{
    if ($n % 2 == 0)
        $n = $n / 2;

    // If 2 again divides n, then n is
    // not a square free number.
    if ($n % 2 == 0)
        return false;

    // n must be odd at this
    // point. So we can skip 
    // one element (Note i = i +2)
    for ($i = 3; $i <= sqrt($n);
                   $i = $i + 2)
    {

        // Check if i is a prime factor
        if ($n % $i == 0)
        {
            $n = $n / $i;

            // If i again divides, then
            // n is not square free
            if ($n % $i == 0)
                return false;
        }
    }

    return true;
}

// Driver Code
$n = 10;
if (isSquareFree($n))
    echo("Yes");
else
    echo("No");

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to print
// all prime factors

    // Returns true if n is a square free
    // number, else returns false.
    function isSquareFree(n)
    {
        if (n % 2 == 0)
        n = n / 2;

        // If 2 again divides n, then n is
        // not a square free number.
        if (n % 2 == 0)
        return false;

        // n must be odd at this point. So we can
        // skip one element (Note i = i +2)
        for (let i = 3; i <= Math.sqrt(n); i = i + 2)
        {
            // Check if i is a prime factor
            if (n % i == 0)
            {
                n = n / i;

                // If i again divides, then
                // n is not square free
                if (n % i == 0)
                    return false;
            }
        }

        return true;
    }

// Driver code

       let n = 10;
        if (isSquareFree(n))
            document.write("Yes");
        else
            document.write("No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(sqrt(N))
最坏的情况下当数字是一个完美的平方，那么就会有 sqrt(n)/2 次迭代。