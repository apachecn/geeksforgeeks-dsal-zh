# 打印所有小于它的质数四胞胎

> 原文:[https://www . geesforgeks . org/print-all-prime-四个小于它的数字的小字母/](https://www.geeksforgeeks.org/print-all-prime-quadruplet-of-a-number-less-than-it/)

给定一个正整数 n，在![n  ](img/31d70d7c99878a33c601d487c9b6eb43.png "Rendered by QuickLaTeX.com")下方打印每一个素数四元组。
[**素数四胞胎:**](https://en.wikipedia.org/wiki/Prime_quadruplet) 在数学中，素数四胞胎是一组四个素数的形式 **{** ***p，p+2，p+6，p+8*** **}** 。
**例:**

```
Input : N = 15
Output : 5  7  11  13

Input : N = 20
Output :  5  7  11  13
           11 13 17  19
```

一个**简单的解决方案**生成 n 以内的所有 Prime 四胞胎，就是遍历从 i=1 到 n 的所有正整数‘I’，检查 I，i+2，i+6 和 i+8 是否为 Prime。
一个**有效的解决方案**是使用厄拉多塞筛在一定范围内预先计算数组中的所有素数。
**接近** :

1.  使用厄拉多塞筛预先计算质数([指的是](https://www.geeksforgeeks.org/sieve-of-eratosthenes/))
2.  从 i=0 遍历到 n-7，检查 I，i+2，i+6 和 i+8 是否也是素数。
3.  如果是，则打印 I，i+2，i+6，i+8，
    否则增加 I 并再次检查

以下是上述思路的实现:

## C++

```
// CPP Program to print prime quadruplet

#include <bits/stdc++.h>
using namespace std;

#define MAX 100000

bool prime[MAX];

// Utility function to generate prime numbers
void sieve()
{
    // Sieve Of Eratosthenes for generating
    // prime number.
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p < MAX; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to print Prime quadruplet
void printPrimeQuad(int n)
{

    for (int i = 0; i < n - 7; i++) {

        if (prime[i] && prime[i + 2] && prime[i + 6]
            && prime[i + 8]) {

            cout << i << " " << i + 2 << " " << i + 6
                 << " " << i + 8 << "\n";
        }
    }
}

// Driver Code
int main()
{
    sieve();
    int n = 20;

    printPrimeQuad(20);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to print prime Quarduplet in a range
import java.util.Arrays;
import java.util.Collections;

class GFG {

    static final int MAX = 1000000;
    static boolean[] prime = new boolean[MAX];

    // utility function to generate prime number
    public static void sieve()
    {
        // Sieve Of Eratosthenes for generating
        // prime number.

        // memset(prime, true, sizeof(prime));
        Arrays.fill(prime, true);

        for (int p = 2; p * p < MAX; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i < MAX; i += p)
                    prime[i] = false;
            }
        }
    }

    // function to print prime Quadruplet
    static void printPrimeQuad(int n)
    {
        for (int i = 0; i < n - 7; i++) {

            if (prime[i] && prime[i + 2] && prime[i + 6]
                && prime[i + 8]) {

                System.out.println(i + " " + (i + 2) + " "
                                   + (i + 6) + " " + (i + 8));
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 20;

        sieve();

        printPrimeQuad(n);
    }
}
```

## 蟒蛇 3

```
# Python3 Program to print
# prime quadruplet

# from math lib import sqrt method
from math import sqrt

MAX = 100000

# Sieve Of Eratosthenes for generating
# prime number.
prime = [True] * MAX

# Utility function to generate
# prime numbers
def sieve() :

    for p in range(2, int(sqrt(MAX)) + 1) :

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p] == True :

            # Update all multiples of p
            for i in range(p * 2 , MAX, p) :
                prime[i] = False

# Function to print Prime quadruplet
def printPrimeQuad(n) :

    for i in range(n - 7) :

        if ( prime[i] and prime[i + 2] and prime[i + 6]
            and prime[i + 8]) :

            print(i,i + 2,i + 6,i + 8)

# Driver code
if __name__ == "__main__" :

    sieve()
    n = 20

    printPrimeQuad(20)

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# code to print prime Quarduplet in a range

using System;

class GFG {

     const int MAX = 1000000;
    static bool[] prime = new bool[MAX];

    // utility function to generate prime number
    public static void sieve()
    {
        // Sieve Of Eratosthenes for generating
        // prime number.

        // memset(prime, true, sizeof(prime));
        for(int i=0;i<MAX;i++) prime[i]=true;

        for (int p = 2; p * p < MAX; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i < MAX; i += p)
                    prime[i] = false;
            }
        }
    }

    // function to print prime Quadruplet
    static void printPrimeQuad(int n)
    {
        for (int i = 0; i < n - 7; i++) {

            if (prime[i] && prime[i + 2] && prime[i + 6]
                && prime[i + 8]) {

                Console.WriteLine(i + " " + (i + 2) + " "
                                   + (i + 6) + " " + (i + 8));
            }
        }
    }

    // Driver Code
    public static void Main()
    {
        int n = 20;

        sieve();

        printPrimeQuad(n);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print prime quadruplet
$MAX = 100000;

// Sieve Of Eratosthenes for generating
// prime number.
$prime = array_fill(0, $MAX, true);

// Utility function to generate
// prime numbers
function sieve()
{
    global $MAX, $prime;

    for ($p = 2; $p * $p < $MAX; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2; $i < $MAX; $i += $p)
                $prime[$i] = false;
        }
    }
}

// Function to print Prime quadruplet
function printPrimeQuad($n)
{
    global $MAX, $prime;
    for ($i = 0; $i < $n - 7; $i++)
    {

        if ($prime[$i] && $prime[$i + 2] &&
            $prime[$i + 6] && $prime[$i + 8])
        {

            echo $i . " " . ($i + 2) . " " .
                ($i + 6) . " " . ($i + 8) . "\n";
        }
    }
}

// Driver Code
sieve();
$n = 20;

printPrimeQuad(20);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript Program to print prime quadruplet

var MAX = 100000;

var prime = Array(MAX).fill(true);

// Utility function to generate prime numbers
function sieve()
{
    // Sieve Of Eratosthenes for generating
    // prime number.

    for (var p = 2; p * p < MAX; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (var i = p * 2; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to print Prime quadruplet
function printPrimeQuad(n)
{

    for (var i = 0; i < n - 7; i++) {

        if (prime[i] && prime[i + 2] && prime[i + 6]
            && prime[i + 8]) {

            document.write( i + " " + (i + 2) + " "
            + (i + 6) + " " + (i + 8) + "<br>");
        }
    }
}

// Driver Code
sieve();
var n = 20;
printPrimeQuad(20);

</script>
```

**Output:** 

```
5 7 11 13
11 13 17 19
```

**另见:**

*   [孪生素数](https://www.geeksforgeeks.org/twin-prime-numbers/)
*   [素数三元组](https://www.geeksforgeeks.org/prime-triplet/)
*   [性感质数](https://www.geeksforgeeks.org/sexy-prime/)
*   [堂兄 Prime](https://www.geeksforgeeks.org/check-whether-the-given-numbers-are-cousin-prime-or-not/)
*   [平衡质数](https://www.geeksforgeeks.org/balanced-prime/)