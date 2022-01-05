# 莫比乌斯函数程序

> 原文:[https://www.geeksforgeeks.org/program-mobius-function/](https://www.geeksforgeeks.org/program-mobius-function/)

[莫比乌斯函数](https://en.wikipedia.org/wiki/M%C3%B6bius_function) ![\mu(n)     ](img/0a67abcea712ad4d692e3e70f6856a5f.png "Rendered by QuickLaTeX.com")是一个用于组合学的[乘法函数](https://en.wikipedia.org/wiki/Completely_multiplicative_function)。它有三个可能的值之一-1、0 和 1。
![For \ any \ positive \ integer \ n, \\ \(\mu(n) = \begin{cases} 1 & \text{ if } n=1, \\ 0 & \text{ if } a^2 \mid n \text{ for some } a > 1 \text{ (i.e., } n \text{ has a squared prime factor)}, \\ (-1)^k & \text { if } n \text{ is the product of } k \text{ distinct primes.} \ _\square \end{cases}\)     ](img/7348bec4f823f2345294eea5de95536e.png "Rendered by QuickLaTeX.com")
**例:**

```
Input : 6
Output : 1
Solution: Prime Factors: 2 3.
Therefore p = 2, (-1)^p = 1

Input: 49
Output: 0
Solution: Prime Factors: 7 ( occurs twice). 
Since the prime factor occurs twice answer
is 0\. 

Input: 3
Output: -1
Solution: Prime Factors: 3\. Therefore p = 1, 
(-1) ^ p =-1

Input : 78
Output : 1
Solution: Prime Factors: 3, 13\. Therefore p = 2, 
(-1)^p = 1
```

**方法 1(简单)**
我们迭代所有小于或等于 n 的数，对于每个数，我们检查它是否除以 n，如果是，我们检查它是否也是素数。如果两个条件都满足，我们检查它的平方是否也除以 n，如果是，我们返回 0。如果平方不除，我们增加质因数的计数。最后，如果有偶数个素因子，我们返回 1，如果有奇数个素因子，我们返回-1。

## C++

```
// CPP Program to evaluate Mobius Function
// M(N) = 1 if N = 1
// M(N) = 0 if any prime factor of N is contained twice
// M(N) = (-1)^(no of distinct prime factors)
#include<iostream>
using namespace std;

// Function to check if n is prime or not
bool isPrime(int n)
{
    if (n < 2)
        return false;
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0)
            return false;   
    return true;
}

int mobius(int N)
{
    // Base Case
    if (N == 1)
        return 1;

    // For a prime factor i check if i^2 is also
    // a factor.
    int p = 0;
    for (int i = 1; i <= N; i++) {
        if (N % i == 0 && isPrime(i)) {

            // Check if N is divisible by i^2
            if (N % (i * i) == 0)
                return 0;
            else

                // i occurs only once, increase f
                p++;
        }
    }

    // All prime factors are contained only once
    // Return 1 if p is even else -1
    return (p % 2 != 0)? -1 : 1;
}

// Driver code
int main()
{
    int N = 17;
    cout << "Mobius Functions M(N) at N = " << N << " is: "
         << mobius(N) << endl;
    cout << "Mobius Functions M(N) at N = " << 25 << " is: "
         << mobius(25) << endl;
    cout << "Mobius Functions M(N) at N = " << 6 << " is: "
         << mobius(6) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for mobious function
import java.io.*;
public class GFG {

    // C# Program to evaluate Mobius
    // Function: M(N) = 1 if N = 1
    // M(N) = 0 if any prime factor
    // of N is contained twice
    // M(N) = (-1)^(no of distinct
    // prime factors)

    // Function to check if n is
    // prime or not
    static boolean isPrime(int n)
    {
        if (n < 2)
            return false;
        for (int i = 2; i * i <= n; i++)
            if (n % i == 0)
                return false;
        return true;
    }

    static int mobius(int N)
    {
        // Base Case
        if (N == 1)
            return 1;

        // For a prime factor i check if
        // i^2 is also a factor.
        int p = 0;
        for (int i = 1; i <= N; i++) {
            if (N % i == 0 && isPrime(i)) {

                // Check if N is divisible by i^2
                if (N % (i * i) == 0)
                    return 0;
                else

                    // i occurs only once, increase f
                    p++;
            }
        }

        // All prime factors are contained only
        // once Return 1 if p is even else -1
        return (p % 2 != 0) ? -1 : 1;
    }

    // Driver code
    static public void main(String[] args)
    {
        int N = 17;
        System.out.println("Mobius Functions M(N) at " +
                      " N = " + N + " is: "    + mobius(N));
        System.out.println("Mobius Functions M(N) at " +
                        " N = " + 25 + " is: " + mobius(25));
        System.out.println("Mobius Functions M(N) at " +
                          " N = " + 6 + " is: " + mobius(6));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python Program to
# evaluate Mobius def
# M(N) = 1 if N = 1
# M(N) = 0 if any
# prime factor of
# N is contained twice
# M(N) = (-1)^(no of
# distinct prime factors)

# def to check if
# n is prime or not
def isPrime(n) :

    if (n < 2) :
        return False
    for i in range(2, n + 1) :
        if (i * i <= n and n % i == 0) :
            return False
    return True

def mobius(N) :

    # Base Case
    if (N == 1) :
        return 1

    # For a prime factor i
    # check if i^2 is also
    # a factor.
    p = 0
    for i in range(1, N + 1) :
        if (N % i == 0 and
                isPrime(i)) :

            # Check if N is
            # divisible by i^2
            if (N % (i * i) == 0) :
                return 0
            else :

                # i occurs only once,
                # increase f
                p = p + 1

    # All prime factors are
    # contained only once
    # Return 1 if p is even
    # else -1
    if(p % 2 != 0) :
        return -1
    else :
        return 1

# Driver Code
N = 17
print ("Mobius defs M(N) at N = {} is: {}" .
         format(N, mobius(N)),end = "\n")
print ("Mobius defs M(N) at N = {} is: {}" .
        format(25, mobius(25)),end = "\n")
print ("Mobius defs M(N) at N = {} is: {}" .
          format(6, mobius(6)),end = "\n")

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# Program to evaluate Mobius Function
using System;

public class GFG
{

    // M(N) = 1 if N = 1
    // M(N) = 0 if any prime factor
    // of N is contained twice
    // M(N) = (-1)^(no of distinct
    // prime factors)

    // Function to check if n is
    // prime or not
    static bool isPrime(int n)
    {
        if (n == 2)
        return true;

        if (n % 2 == 0)
        return false;
        for (int i = 3; i * i <= n / 2; i += 2)
            if (n % i == 0)
            return false;
        return true;
    }

    static int mobius(int N)
    {

        // Base Case
        if (N == 1)
        return 1;

        // For a prime factor i check
        // if i^2 is also a factor.
        int p = 0;
        for (int i = 2; i <= N; i++)
        {
            if (N % i == 0 && isPrime(i)) {

                // Check if N is divisible by i^2
                if (N % (i * i) == 0)
                return 0;
                else

                // i occurs only once, increase f
                p++;
            }
        }

        // All prime factors are contained only
        // once Return 1 if p is even else -1
        return (p % 2 != 0) ? -1 : 1;
    }

    // Driver code
    static public void Main()
    {

        Console.WriteLine("Mobius Functions M(N) at " +
                         "N = " + 17 + " is: " + mobius(17));
        Console.WriteLine("Mobius Functions M(N) at " +
                         "N = " + 25 + " is: " + mobius(25));
        Console.WriteLine("Mobius Functions M(N) at " +
                          "N = " + 6 + " is: " + mobius(6));

    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to evaluate Mobius Function
// M(N) = 1 if N = 1
// M(N) = 0 if any prime factor of
// N is contained twice
// M(N) = (-1)^(no of distinct prime factors)

// Function to check if n is prime or not
function isPrime($n)
{
    if ($n < 2)
        return false;
    for ($i = 2; $i * $i <= $n; $i++)
        if ($n % $i == 0)
            return false;
    return true;
}

function mobius($N)
{

    // Base Case
    if ($N == 1)
        return 1;

    // For a prime factor i
    // check if i^2 is also
    // a factor.
    $p = 0;
    for ($i = 1; $i <= $N; $i++) {
        if ($N % $i == 0 && isPrime($i)) {

            // Check if N is divisible by i^2
            if ($N % ($i * $i) == 0)
                return 0;
            else

                // i occurs only once, increase f
                $p++;
        }
    }

    // All prime factors are
    // contained only once
    // Return 1 if p is even
    // else -1
    return ($p % 2 != 0) ? -1 : 1;
}

    // Driver Code
    $N = 17;
    echo "Mobius Functions M(N) at N = " ,$N , " is: "
                                  , mobius($N) ,"\n";
    echo "Mobius Functions M(N) at N = " ,25, " is: "
                                  , mobius(25),"\n" ;
    echo "Mobius Functions M(N) at N = " ,6, " is: "
                                       , mobius(6) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program for mobious function

  //  JavaScript Program to evaluate Mobius
    // Function: M(N) = 1 if N = 1
    // M(N) = 0 if any prime factor
    // of N is contained twice
    // M(N) = (-1)^(no of distinct
    // prime factors)

    // Function to check if n is
    // prime or not
    function isPrime(n)
    {
        if (n < 2)
            return false;
        for (let i = 2; i * i <= n; i++)
            if (n % i == 0)
                return false;
        return true;
    }

    function mobius(N)
    {
        // Base Case
        if (N == 1)
            return 1;

        // For a prime factor i check if
        // i^2 is also a factor.
        let p = 0;
        for (let i = 1; i <= N; i++) {
            if (N % i == 0 && isPrime(i)) {

                // Check if N is divisible by i^2
                if (N % (i * i) == 0)
                    return 0;
                else

                    // i occurs only once, increase f
                    p++;
            }
        }

        // All prime factors are contained only
        // once Return 1 if p is even else -1
        return (p % 2 != 0) ? -1 : 1;
    }

// Driver code   

        let N = 17;
        document.write("Mobius Functions M(N) at " +
                      " N = " + N + " is: "    + mobius(N) + "<br/>");
        document.write("Mobius Functions M(N) at " +
                        " N = " + 25 + " is: " + mobius(25) + "<br/>");
        document.write("Mobius Functions M(N) at " +
                          " N = " + 6 + " is: " + mobius(6) + "<br/>");

</script>
```

**输出:**

```
Mobius Functions M(N) at N = 17 is: -1
Mobius Functions M(N) at N = 25 is: 0
Mobius Functions M(N) at N = 6 is: 1
```

**方法 2(高效)**
这个想法是基于[高效程序打印给定数字的所有质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。有趣的是，我们在这里不需要内部 while 循环，因为如果一个数除了不止一次，我们可以立即返回 0。

## C++

```
// Program to print all prime factors
# include <bits/stdc++.h>
using namespace std;

// Returns value of mobius()
int mobius(int n)
{
    int p = 0;

    // Handling 2 separately
    if (n%2 == 0)
    {
        n = n/2;
        p++;

        // If 2^2 also divides N
        if (n % 2 == 0)
           return 0;
    }

    // Check for all other prime factors
    for (int i = 3; i <= sqrt(n); i = i+2)
    {
        // If i divides n
        if (n%i == 0)
        {
            n = n/i;
            p++;

            // If i^2 also divides N
            if (n % i == 0)
               return 0;
        }
    }

    return (p % 2 == 0)? -1 : 1;
}

// Driver code
int main()
 {
    int N = 17;
    cout << "Mobius Functions M(N) at N = " << N << " is: "
         << mobius(N) << endl;
    cout << "Mobius Functions M(N) at N = " << 25 << " is: "
         << mobius(25) << endl;
    cout << "Mobius Functions M(N) at N = " << 6 << " is: "
         << mobius(6) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all prime factors
import java.io.*;

class GFG {

    // Returns value of mobius()
    static int mobius(int n)
    {
        int p = 0;

        // Handling 2 separately
        if (n % 2 == 0)
        {
            n = n / 2;
            p++;

            // If 2^2 also divides N
            if (n % 2 == 0)
                return 0;
        }

        // Check for all other prime factors
        for (int i = 3; i <= Math.sqrt(n);
                                    i = i+2)
        {
            // If i divides n
            if (n % i == 0)
            {
                n = n / i;
                p++;

                // If i^2 also divides N
                if (n % i == 0)
                    return 0;
            }
        }

        return (p % 2 == 0)? -1 : 1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int N = 17;
        System.out.println( "Mobius Functions"
               + " M(N) at N = " + N + " is: "
                                 + mobius(N));
        System.out.println ("Mobius Functions"
               + "M(N) at N = " + 25 + " is: "
                                + mobius(25));
        System.out.println( "Mobius Functions"
                + "M(N) at N = " + 6 + " is: "
                                 + mobius(6));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python Program to evaluate
# Mobius def M(N) = 1 if N = 1
# M(N) = 0 if any prime factor
# of N is contained twice
# M(N) = (-1)^(no of distinct
# prime factors)
import math

# def to check if n
# is prime or not
def isPrime(n) :

    if (n < 2) :
        return False
    for i in range(2, n + 1) :
        if (n % i == 0) :
            return False
        i = i * i
    return True

def mobius(n) :

    p = 0

    # Handling 2 separately
    if (n % 2 == 0) :

        n = int(n / 2)
        p = p + 1

        # If 2^2 also
        # divides N
        if (n % 2 == 0) :
            return 0

    # Check for all
    # other prime factors
    for i in range(3, int(math.sqrt(n)) + 1) :

        # If i divides n
        if (n % i == 0) :

            n = int(n / i)
            p = p + 1

            # If i^2 also
            # divides N
            if (n % i == 0) :
                return 0
        i = i + 2   

    if(p % 2 == 0) :
        return -1
    else :
        return 1

# Driver Code
N = 17
print ("Mobius defs M(N) at N = {} is: {}\n" .
                        format(N, mobius(N)));
print ("Mobius defs M(N) at N = 25 is: {}\n" .
                          format(mobius(25)));
print ("Mobius defs M(N) at N = 6 is: {}\n" .
                          format(mobius(6)));

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to print all prime factors
using System;
class GFG {

    // Returns value of mobius()
    static int mobius(int n)
    {
        int p = 0;

        // Handling 2 separately
        if (n % 2 == 0)
        {
            n = n / 2;
            p++;

            // If 2^2 also divides N
            if (n % 2 == 0)
                return 0;
        }

        // Check for all other prime factors
        for (int i = 3; i <= Math.Sqrt(n);
                                    i = i+2)
        {
            // If i divides n
            if (n % i == 0)
            {
                n = n / i;
                p++;

                // If i^2 also divides N
                if (n % i == 0)
                    return 0;
            }
        }

        return (p % 2 == 0)? -1 : 1;
    }

    // Driver Code
    public static void Main ()
    {
        int N = 17;
        Console.WriteLine( "Mobius Functions"
              + " M(N) at N = " + N + " is: "
                                + mobius(N));
        Console.WriteLine("Mobius Functions"
             + "M(N) at N = " + 25 + " is: "
                                + mobius(25));
        Console.WriteLine( "Mobius Functions"
               + "M(N) at N = " + 6 + " is: "
                                + mobius(6));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print
// all prime factors

// Returns value of mobius()
function mobius( $n)
{
    $p = 0;

    // Handling 2 separately
    if ($n % 2 == 0)
    {
        $n = $n / 2;
        $p++;

        // If 2^2 also divides N
        if ($n % 2 == 0)
        return 0;
    }

    // Check for all
    // other prime factors
    for ( $i = 3; $i <= sqrt($n); $i = $i + 2)
    {

        // If i divides n
        if ($n % $i == 0)
        {
            $n = $n / $i;
            $p++;

            // If i^2 also divides N
            if ($n % $i == 0)
            return 0;
        }
    }

    return ($p % 2 == 0)? -1 : 1;
}

    // Driver code
    $N = 17;
    echo "Mobius Functions M(N) at N = ", $N, " is: "
        , mobius($N),"\n" ;
    echo "Mobius Functions M(N) at N = " , 25 , " is: "
        , mobius(25),"\n";
    echo "Mobius Functions M(N) at N = " , 6 , " is: "
        , mobius(6) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // JavaScript program to print all prime factors

    // Returns value of mobius()
    function mobius(n)
    {
        let p = 0;

        // Handling 2 separately
        if (n % 2 == 0)
        {
            n = parseInt(n / 2, 10);
            p++;

            // If 2^2 also divides N
            if (n % 2 == 0)
                return 0;
        }

        // Check for all other prime factors
        for (let i = 3; i <= Math.sqrt(n); i = i+2)
        {
            // If i divides n
            if (n % i == 0)
            {
                n = parseInt(n / i, 10);
                p++;

                // If i^2 also divides N
                if (n % i == 0)
                    return 0;
            }
        }

        return (p % 2 == 0)? -1 : 1;
    }

    let N = 17;
    document.write( "Mobius Functions"
                      + " M(N) at N = " + N + " is: "
                      + mobius(N) + "</br>");
    document.write("Mobius Functions"
                      + "M(N) at N = " + 25 + " is: "
                      + mobius(25) + "</br>");
    document.write( "Mobius Functions"
                      + "M(N) at N = " + 6 + " is: "
                      + mobius(6));

</script>
```

**输出:**

```
Mobius Functions M(N) at N = 17 is: -1
Mobius Functions M(N) at N = 25 is: 0
Mobius Functions M(N) at N = 6 is: 1
```

**参考文献**
1)[http://mathworld.wolfram.com/MoebiusFunction.html](http://mathworld.wolfram.com/MoebiusFunction.html)T5】2)[https://en.wikipedia.org/wiki/M%C3%B6bius_function](https://en.wikipedia.org/wiki/M%C3%B6bius_function)T8】3)[https://en . Wikipedia . org/wiki/complete _ 乘法 _function](https://en.wikipedia.org/wiki/Completely_multiplicative_function)