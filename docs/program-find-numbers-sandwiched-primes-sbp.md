# 检查一个数字是否夹在素数之间

> 原文:[https://www . geesforgeks . org/program-find-numbers-夹心-primes-sbp/](https://www.geeksforgeeks.org/program-find-numbers-sandwiched-primes-sbp/)

如果一个数的后一个数和前一个数都是[素数](https://www.geeksforgeeks.org/prime-numbers/)，那么这个数就被称为夹在素数之间。所以，夹在中间的数是两个质数。
给定一个数 n，我们需要检查这个数是否夹在素数之间。
示例:

```
Input :  642
Output : Yes
Explanation : 641 and 643 are both prime numbers

Input :  6
Output : Yes
Explanation : 5 and 7 both are prime numbers

Input : 9
Output : No
Explanation : 8 and 10 both are non-prime numbers
```

想法很简单，我们检查 n-1 和 n-2 是否是素数。

## C++

```
// CPP Program to check whether a number is
// sandwiched between two primes or not
#include<iostream>
#include <cmath>
using namespace std;

// returns true if number n is prime
bool isPrime(int n)
{
    // 0 and 1 both are non-primes
    if (n == 0 || n == 1) return false;

    // finding square root of n
    int root = sqrt(n);

    // checking if n has any
    // factor upto square root of n
    // if yes its not prime
    for (int i=2;i<=root;i++)
        if (n%i == 0)
            return false;
    return true;
}

bool isSandwitched(int n)
{
    return (isPrime(n-1) && isPrime(n+1));
}

// Driver's Code
int main()
{
   int n = 642;
   cout << n << " : ";
   if (isSandwitched(n))
       cout<<"Yes\n";
   else
       cout<<"No\n";

   n = 9;
   cout<< n << " : ";
   if (isSandwitched(n))
       cout << "Yes\n";
   else
       cout << "No\n";

     return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java Program to check whether
// a number is  sandwiched between
// two primes or not

import java.io.*;

class GFG {

    // returns true if number n is prime
    static boolean isPrime(int n)
    {
        // 0 and 1 both are non-primes
        if (n == 0 || n == 1) return false;

        // finding square root of n
        int root = (int)Math.sqrt(n);

        // checking if n has any
        // factor upto square root of n
        // if yes its not prime
        for (int i = 2; i <= root; i++)
            if (n % i == 0)
                return false;
        return true;
    }

    static boolean isSandwitched(int n)
    {
        return (isPrime(n - 1) && isPrime(n + 1));
    }

    // Driver's Code
    public static void main (String[] args)
    {
        int n = 642;
        System.out.print ( n + " : ");
        if (isSandwitched(n))
            System.out.println("Yes");
        else
            System.out.println("No");

        n = 9;
        System.out.print(n + " : ");
        if (isSandwitched(n))
            System.out.println( "Yes");
        else
            System.out.println ("No");

    }
}

// This article is contributed by vt_m.
```

## 蟒蛇 3

```
# Python Program to check
# whether a number is
# sandwiched between
# two primes or not

import math

# returns true if number n is prime
def isPrime(n):

    # 0 and 1 both are non-primes
    if (n == 0 or n == 1):
       return False

    # finding square root of n
    root = int(math.sqrt(n))

    # checking if n has any
    # factor upto square root of n
    # if yes its not prime
    for i in range(2 ,root+1):
        if (n%i == 0):
             return False
    return True

def isSandwitched(n):

    return (isPrime(n-1) and isPrime(n+1))

# driver Function
n = 642
print(n , end=" : ")
if (isSandwitched(n)):
    print("Yes")
else:
    print("No")

n = 9
print(n , end= " : ")
if (isSandwitched(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by Gitanjali.
```

## C#

```
// C# Program to check whether
// a number is sandwiched between
// two primes or not
using System;

class GFG {

    // returns true if number n is prime
    static bool isPrime(int n)
    {

        // 0 and 1 both are non-primes
        if (n == 0 || n == 1)
           return false;

        // finding square root of n
        int root = (int)Math.Sqrt(n);

        // checking if n has any factor
        // upto square root of n if yes
        // its not prime
        for (int i = 2; i <= root; i++)
            if (n % i == 0)
                return false;
        return true;
    }

    static bool isSandwitched(int n)
    {
        return (isPrime(n - 1) && isPrime(n + 1));
    }

    // Driver Code
    public static void Main ()
    {
        int n = 642;
        Console.Write( n + " : ");
        if (isSandwitched(n))
           Console.WriteLine("Yes");
        else
           Console.Write("No");

        n = 9;
            Console.Write(n + " : ");
        if (isSandwitched(n))
            Console.Write("Yes");
        else
             Console.Write ("No");

    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check whether a number is
// sandwiched between two primes or not

// returns true if number n is prime
function isPrime($n)
{

    // 0 and 1 both are non-primes
    if ($n == 0 || $n == 1)
        return false;

    // finding square root of n
    $root = sqrt($n);

    // checking if n has any
    // factor upto square root of n
    // if yes its not prime
    for ($i = 2; $i <= $root; $i++)
        if ($n % $i == 0)
            return false;
    return true;
}

function isSandwitched($n)
{
    return (isPrime($n - 1) &&
            isPrime($n + 1));
}

    // Driver Code
    $n = 642;
    echo $n , " : ";
    if (isSandwitched($n))
        echo "Yes\n";
    else
        echo "No\n";

    $n = 9;
    echo $n, " : ";
    if (isSandwitched($n))
        echo "Yes\n";
    else
        echo "No\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to check whether
// a number is  sandwiched between
// two primes or not

   // returns true if number n is prime
    function isPrime(n)
    {
        // 0 and 1 both are non-primes
        if (n == 0 || n == 1) return false;

        // finding square root of n
        let root = Math.sqrt(n);

        // checking if n has any
        // factor upto square root of n
        // if yes its not prime
        for (let i = 2; i <= root; i++)
            if (n % i == 0)
                return false;
        return true;
    }

    function isSandwitched(n)
    {
        return (isPrime(n - 1) && isPrime(n + 1));
    }

// Driver code

        let n = 642;
        document.write ( n + " : ");
        if (isSandwitched(n))
            document.write("Yes" + "<br/>");
        else
            document.write("No" + "<br/>");

        n = 9;
        document.write(n + " : ");
        if (isSandwitched(n))
            document.write( "Yes" + "<br/>");
        else
            document.write ("No" + "<br/>");

</script>
```

**输出:**

```
642 : Yes
9 : No
```