# 1 和 n 之间的孪生素数

> 原文:[https://www . geesforgeks . org/twin-prime-numbers-介于-1 和-n 之间/](https://www.geeksforgeeks.org/twin-prime-numbers-between-1-and-n/)

给定一个整数 n，我们需要打印 1 到 n 之间的所有孪生素数对。A [孪生素数](https://www.geeksforgeeks.org/twin-prime-numbers/)是那些素数并且两个素数之间有两(2)个差的数。换句话说，孪生素数是素数差距为 2 的素数。
有时孪生素数这个词是指一对孪生素数；这个的另一个名字是素数孪生或素数对。通常，这对(2，3)不被认为是一对孪生素数。因为 2 是唯一的偶数素数，所以这一对是唯一相差一的素数对；因此，对于任何其他两个素数，孪生素数的间隔都尽可能地小。
前几对孪生素数是:

```
(3, 5), (5, 7), (11, 13), (17, 19), (29, 31), 
(41, 43), (59, 61), (71, 73), (101, 103), 
(107, 109), (137, 139), …etc.
```

**FACT** :一万以下的孪生素数有 409 个。
示例:

```
Input : n = 15
Output : (3, 5), (5, 7), (11, 13)

Input : 25
Output :(3, 5), (5, 7), (11, 13), (17, 19)
```

**方法:**
使用厄拉多塞的[筛查找所有小于或等于 n 的素数列表，然后再次迭代列表直到 n，只检查第 i <sup>个</sup>数并检查其(i+2) <sup>个</sup>数，如果两者都是素数，则打印两个数，否则继续下一个数以查找孪生素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ program print all twin primes
// using Sieve of Eratosthenes.
#include <bits/stdc++.h>
using namespace std;

void printTwinPrime(int n)
{
    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    // to check for twin prime numbers
    // display the twin primes
    for (int p = 2; p <= n - 2; p++)
        if (prime[p] && prime[p + 2])
            cout << "(" << p << ", " << p + 2 << ")" ;
}

// Driver Program to test above function
int main()
{
    int n = 25;

    // Calling the function
    printTwinPrime(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all Twin Prime
// Numbers using Sieve of Eratosthenes
import java.io.*;

class GFG {

    static void printTwinPrime(int n)
    {
        // Create a boolean array "prime[0..n]"
        // and initialize all entries it as
        // true. A value in prime[i] will
        // finally be false if i is Not a
        // prime, else true.
        boolean prime[] = new boolean[n + 1];

        for (int i = 0; i <= n; i++)
            prime[i] = true;

        for (int p = 2; p * p <= n; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }

        // to check for twin prime numbers
        // display th twin prime
        for (int i = 2; i <= n - 2; i++) {

            if (prime[i] == true &&
                prime[i + 2] == true)

                // Display the result
                System.out.print(" (" + i + ", " +
                                   (i + 2) + ")");
        }
    }

    // Driver Program to test above function
    public static void main(String args[])
    {
        int n = 25;
        printTwinPrime(n);
    }
}
```

## 计算机编程语言

```
# Python program to illustrate...
# To print total number of twin prime
# using Sieve of Eratosthenes

def printTwinPrime(n):

    # Create a boolean array "prime[0..n]"
    # and initialize all entries it as
    # true. A value in prime[i] will
    # finally be false if i is Not a prime,
    # else true.
    prime = [True for i in range(n + 2)]
    p = 2

    while (p * p <= n + 1):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, n + 2, p):
                prime[i] = False
        p += 1

    # check twin prime numbers
    # display the twin prime numbers
    for p in range(2, n-1):
        if prime[p] and prime[p + 2]:
            print("(",p,",", (p + 2), ")" ,end='')

# driver program
if __name__=='__main__':

    # static input
    n = 25

    # Calling the function
    printTwinPrime(n)
```

## C#

```
// C# program to illustrate..
// print all twin primes
// Using Sieve of Eratosthenes
using System;

public class GFG {

    public static void printtwinprime(int n)
    {

        // Create a boolean array "prime[0..n]"
        // and initialize all entries it as
        // true. A value in prime[i] will
        // finally be false if i is Not a
        // prime, else true.
        bool[] prime = new bool[n + 1];

        for (int i = 0; i < n + 1; i++)
            prime[i] = true;

        for (int p = 2; p * p <= n; p++) {
            // If prime[p] is not changed,
            // then it is a prime

            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }

        // check for twin prime numbers
        // To display th result
        for (int i = 2; i <= n - 2; i++) {
            if (prime[i] == true && prime[i + 2] == true)
                Console.Write(" (" + i + ", " + (i + 2) + ")");
        }
    }

    // Driver Code
    public static void Main()
    {
        // static input
        int n = 25;

        // calling the function
        printtwinprime(n);
    }  
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// all twin primes using
// Sieve of Eratosthenes.
function printTwinPrime($n)
{
    // Create a boolean array
    // "prime[0..n]"  and
    // initialize all entries
    // it as true. A value in
    // prime[i] will finally be 
    // false if i is Not a prime,
    // else true.
    $prime = array_fill(0, $n + 1, true);

    for ($p = 2; $p * $p <= $n; $p++)
    {

        // If prime[p] is not
        // changed, then it
        // is a prime
        if ($prime[$p] == true)
        {

            // Update all
            // multiples of p
            for ($i = $p * 2;
                 $i <= $n; $i += $p)
                $prime[$i] = false;
        }
    }

    // to check for twin
    // prime numbers display
    // the twin primes
    for ($p = 2; $p <= $n - 2; $p++)
        if ($prime[$p] &&
            $prime[$p + 2])
            echo "(". $p . ", " .
                  ($p + 2). ")" ;
}

// Driver Code
$n = 25;

// Calling the function
printTwinPrime($n);

// This code is contributed by mits.
?>
```

## java 描述语言

```
<script>

// JavaScript program to print all Twin Prime
// Numbers using Sieve of Eratosthenes

    function printTwinPrime(n)
    {
        // Create a boolean array "prime[0..n]"
        // and initialize all entries it as
        // true. A value in prime[i] will
        // finally be false if i is Not a
        // prime, else true.
        let prime = [];

        for (let i = 0; i <= n; i++)
            prime[i] = true;

        for (let p = 2; p * p <= n; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (let i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }

        // to check for twin prime numbers
        // display th twin prime
        for (let i = 2; i <= n - 2; i++) {

            if (prime[i] == true &&
                prime[i + 2] == true)

                // Display the result
                document.write(" (" + i + ", " +
                                   (i + 2) + ")");
        }
    }
// Driver program

        let n = 25;
        printTwinPrime(n);

        // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
(3, 5)(5, 7)(11, 13)(17, 19)
```