# 素数三元组

> 原文:[https://www.geeksforgeeks.org/prime-triplet/](https://www.geeksforgeeks.org/prime-triplet/)

**素数三元组**是一组三个[素数](https://www.geeksforgeeks.org/prime-numbers/)的形式( **p，p+2，p+6** )或( **p，p+4，p+6** )。这是三个素数最接近的分组，因为每三个连续奇数中有一个是三的倍数，因此除了(2，3，5)和(3，5，7)之外，不是素数(除了 3 本身)。

**示例:**

```
Input : n = 15
Output : 5 7 11
         7 11 13

Input : n = 25
Output : 5 7 11
         7 11 13
         11 13 17
         13 17 19
         17 19 23
```

一个简单的解决方案是遍历从 1 到 n-6 的所有数字。对于每个数字，我检查我，我+2，我+6，还是我，我+4，我+6 是素数。如果是，打印三胞胎。

一个有效的解决方法是厄拉多塞的[筛首先找到所有的素数，这样我们就可以快速检查一个数是否是素数。
以下是实施办法。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

## C++

```
// C++ program to find prime triplets smaller
// than or equal to n.
#include <bits/stdc++.h>
using namespace std;

// function to detect prime number
// here we have used sieve method
// https://www.geeksforgeeks.org/sieve-of-eratosthenes/
// to detect prime number
void sieve(int n, bool prime[])
{
    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// function to print prime triplets
void printPrimeTriplets(int n)
{
    // Finding all primes from 1 to n
    bool prime[n + 1];
    memset(prime, true, sizeof(prime));
    sieve(n, prime);

    cout << "The prime triplets from 1 to "
          << n << "are :" << endl;
    for (int i = 2; i <= n-6; ++i) {

        // triplets of form (p, p+2, p+6)
        if (prime[i] && prime[i + 2] && prime[i + 6])
            cout << i << " " << (i + 2) << " " << (i + 6) << endl;

        // triplets of form (p, p+4, p+6)
        else if (prime[i] && prime[i + 4] && prime[i + 6])
            cout << i << " " << (i + 4) << " " << (i + 6) << endl;
    }
}

int main()
{
    int n = 25;
    printPrimeTriplets(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find prime triplets
// smaller than or equal to n.
import java.io.*;
import java.util.*;

class GFG {

// function to detect prime number
// here we have used sieve method
// https://www.geeksforgeeks.org/sieve-of-eratosthenes/
// to detect prime number
    static void sieve(int n, boolean prime[])
    {
        for (int p = 2; p * p <= n; p++) {

            // If prime[p] is not changed,
            //then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }
    }

    // function to print prime triplets
    static void printPrimeTriplets(int n)
    {
        // Finding all primes from 1 to n
        boolean prime[]=new boolean[n + 1];
        Arrays.fill(prime,true);
        sieve(n, prime);

        System.out.println("The prime triplets"+
                           " from 1 to " + n + "are :");

        for (int i = 2; i <= n-6; ++i) {

            // triplets of form (p, p+2, p+6)
            if (prime[i] && prime[i + 2] && prime[i + 6])
                System.out.println( i + " " + (i + 2) +
                                    " " + (i + 6));

            // triplets of form (p, p+4, p+6)
            else if (prime[i] && prime[i + 4] &&
                     prime[i + 6])

                System.out.println(i + " " + (i + 4) +
                                   " " + (i + 6));
        }
    }

    public static void main(String args[])
    {
        int n = 25;
        printPrimeTriplets(n);
    }
}

 /*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to find
# prime triplets smaller
# than or equal to n.

# function to detect prime number
# using sieve method
# https://www.geeksforgeeks.org/sieve-of-eratosthenes/
# to detect prime number
def sieve(n, prime) :

    p = 2

    while (p * p <= n ) :

        # If prime[p] is not changed
        # , then it is a prime
        if (prime[p] == True) :

            # Update all multiples of p
            i = p * 2

            while ( i <= n ) :
                prime[i] = False
                i = i + p

        p = p + 1

# function to print
# prime triplets
def printPrimeTriplets(n) :

    # Finding all primes
    # from 1 to n
    prime = [True] * (n + 1)
    sieve(n, prime)

    print( "The prime triplets from 1 to ",
                               n , "are :")

    for i in range(2, n - 6 + 1) :

        # triplets of form (p, p+2, p+6)
        if (prime[i] and prime[i + 2] and
                            prime[i + 6]) :
            print( i , (i + 2) , (i + 6))

        # triplets of form (p, p+4, p+6)
        elif (prime[i] and prime[i + 4] and
                            prime[i + 6]) :
            print(i , (i + 4) , (i + 6))

# Driver code
n = 25
printPrimeTriplets(n)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find prime
// triplets smaller than or
// equal to n.
using System;

class GFG
{

// function to detect
// prime number
static void sieve(int n,
                  bool[] prime)
{
    for (int p = 2;
             p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == false)
        {

            // Update all multiples of p
            for (int i = p * 2;
                     i <= n; i += p)
                prime[i] = true;
        }
    }
}

// function to print
// prime triplets
static void printPrimeTriplets(int n)
{
    // Finding all primes
    // from 1 to n
    bool[] prime = new bool[n + 1];
    sieve(n, prime);

    Console.WriteLine("The prime triplets " +
                               "from 1 to " +
                               n + " are :");

    for (int i = 2; i <= n - 6; ++i)
    {

        // triplets of form (p, p+2, p+6)
        if (!prime[i] &&
            !prime[i + 2] &&
            !prime[i + 6])
            Console.WriteLine(i + " " + (i + 2) +
                                  " " + (i + 6));

        // triplets of form (p, p+4, p+6)
        else if (!prime[i] &&
                 !prime[i + 4] &&
                 !prime[i + 6])
            Console.WriteLine(i + " " + (i + 4) +
                                  " " + (i + 6));
    }
}

// Driver Code
public static void Main()
{
    int n = 25;
    printPrimeTriplets(n);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find prime
// triplets smaller than or
// equal to n.

// function to print
// prime triplets
function printPrimeTriplets($n)
{
    // Finding all primes
    // from 1 to n
    $prime = array_fill(0, $n + 1, true);

    // to detect prime number
    for ($p = 2; $p * $p <= $n; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2; $i <= $n; $i += $p)
                $prime[$i] = false;
        }
    }

    echo "The prime triplets from 1 to " .
                          $n . " are :\n";
    for ($i = 2; $i <= $n-6; ++$i)
    {

        // triplets of form (p, p+2, p+6)
        if ($prime[$i] && $prime[$i + 2] &&
                          $prime[$i + 6])
            echo $i. " " . ($i + 2) .
                     " " . ($i + 6) . "\n";

        // triplets of form (p, p+4, p+6)
        else if ($prime[$i] && $prime[$i + 4] &&
                               $prime[$i + 6])
            echo $i. " " . ($i + 4) .
                     " " . ($i + 6) . "\n";
    }
}

// Driver Code
$n = 25;
printPrimeTriplets($n);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>
// Javascript program to find prime
// triplets smaller than or
// equal to n.

// function to print
// prime triplets
function printPrimeTriplets(n)
{
    // Finding all primes
    // from 1 to n
    let prime = new Array(n + 1).fill(true);

    // to detect prime number
    for (let p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (let i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    document.write("The prime triplets from 1 to " + n + " are :<br>");
    for (let i = 2; i <= n-6; ++i)
    {

        // triplets of form (p, p+2, p+6)
        if (prime[i] && prime[i + 2] &&
                        prime[i + 6])
            document.write(i + " " + (i + 2) +
                    " " + (i + 6) + "<br>");

        // triplets of form (p, p+4, p+6)
        else if (prime[i] && prime[i + 4] &&
                            prime[i + 6])
            document.write(i + " " + (i + 4) +
                    " " + (i + 6) + "<br>");
    }
}

// Driver Code
let n = 25;
printPrimeTriplets(n);

// This code is contributed by gfgking
</script>
```

**输出:**

```
The prime triplets from 1 to 25 are :
5 7 11
7 11 13
11 13 17
13 17 19
17 19 23
```