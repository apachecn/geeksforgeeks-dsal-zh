# 按反序打印从 1 到 N 的质数

> 原文:[https://www . geesforgeks . org/print-prime-numbers-1-n-逆序/](https://www.geeksforgeeks.org/print-prime-numbers-1-n-reverse-order/)

给定一个数 N，以相反的顺序打印所有小于或等于 N 的素数。
比如 N 是 9，输出应该是“7、5、3、2”。
**例:**

```
Input :  N = 5
Output : 5 3 2

Input : N = 20
Output : 19 17 13 11 7 5 3 2
```

一个简单的解决方案是从 N 遍历到 1。每一个数字，用[学法检查是否是素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。如果数字是质数，打印出来。
一个有效的解决方案是使用厄拉多塞的[筛子。我们高效地找到从 1 到 N 的所有数字，然后打印出来。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ program to print all primes between 1
// to N in reverse order using Sieve of
// Eratosthenes
#include <bits/stdc++.h>
using namespace std;

void Reverseorder(int n)
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i
    // is Not a prime, else true.
    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers in reverse order
    for (int p = n; p >= 2; p--)
        if (prime[p])
            cout << p << " ";
}

// Driver Program
int main()
{
    // static input
    int N = 25;

    // to display
    cout << "Prime number in reverse order" << endl;

    if (N == 1)
        cout << "No prime no exist in this range";
    else
        Reverseorder(N); // calling the function

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all primes between 1
// to N in reverse order using Sieve of
// Eratosthenes
import java.io.*;
import java.util.*;

class GFG {
    static void reverseorder(int n)
    {

        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value
        // in prime[i] will finally be false if i
        // is Not a prime, else true.
        boolean prime[] = new boolean[n + 1];
        for (int i = 0; i < n; i++)
            prime[i] = true;

        for (int p = 2; p * p <= n; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }

        // Print all prime numbers
        for (int i = n; i >= 2; i--)
            if (prime[i] == true)
                System.out.print(i + " ");
    }

    // Driver Program to test above function
    public static void main(String args[])
    {
        // static input
        int N = 25;
        // To display
        System.out.println("Prime number in reverse order");

        if (N == 1)
            System.out.println("No prime no exist in this range");
        else
            reverseorder(N); // calling the function
    }
}
```

## 蟒蛇 3

```
# Python3 program to print all primes
# between 1 to N in reverse order
# using Sieve of Eratosthenes
def Reverseorder(n):

    # Create a boolean array "prime[0..n]"
    # and initialize all entries it as true.
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.
    prime = [True] * (n + 1);

    p = 2;
    while(p * p <= n):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range((p * 2), (n + 1), p):
                prime[i] = False;
        p += 1;

    # Print all prime numbers in
    # reverse order
    for p in range(n, 1, -1):
        if (prime[p]):
            print(p, end = " ");

# Driver Code

# static input
N = 25;

# to display
print("Prime number in reverse order");

if (N == 1):
    print("No prime no exist in this range");
else:
    Reverseorder(N); # calling the function

# This code is contributed by mits
```

## C#

```
// C# program to print all primes between 1
// to N in reverse order using Sieve of
// Eratosthenes
using System;

class GFG {

    static void reverseorder(int n)
    {

        // Create a boolean array "prime[0..n]"
        // and initialize all entries it as
        // true. A value in prime[i] will
        // finally be false if i is Not a
        // prime, else true.
        bool []prime = new bool[n + 1];

        for (int i = 0; i < n; i++)
            prime[i] = true;

        for (int p = 2; p * p <= n; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= n;
                                     i += p)
                    prime[i] = false;
            }
        }

        // Print all prime numbers
        for (int i = n; i >= 2; i--)
            if (prime[i] == true)
                Console.Write(i + " ");
    }

    // Driver code
    public static void Main()
    {

        // static input
        int N = 25;

        // To display
        Console.WriteLine("Prime number in"
                       + " reverse order");

        if (N == 1)
            Console.WriteLine("No prime no"
                + " exist in this range");
        else

            // calling the function
            reverseorder(N);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print all primes
// between 1 to N in reverse order
// using Sieve of Eratosthenes

function Reverseorder($n)
{
    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    $prime = array_fill(0, $n + 1, true);

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

    // Print all prime numbers in
    // reverse order
    for ($p = $n; $p >= 2; $p--)
        if ($prime[$p])
            echo $p." ";
}

// Driver Code

// static input
$N = 25;

// to display
echo "Prime number in reverse order\n";

if ($N == 1)
    echo "No prime no exist in this range";
else
    Reverseorder($N); // calling the function

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to print all primes between 1
// to N in reverse order using Sieve of
// Eratosthenes

function Reverseorder( n)
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i
    // is Not a prime, else true.
     let prime = new Array(n + 1);
        for (let i = 0; i < n; i++)
            prime[i] = true;

    for (let p = 2; p * p <= n; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (let i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers in reverse order
    for (let p = n; p >= 2; p--)
        if (prime[p])
            document.write(p + " ");
}

// Driver Code

// static input
let N = 25;

// to display
document.write("Prime number in reverse order" + "</br>");

if (N == 1)
    document.write("No prime no exist in this range");
else
    Reverseorder(N); // calling the function

</script>
```

**Output:** 

```
Prime number in reverse order
23 19 17 13 11 7 5 3 2
```