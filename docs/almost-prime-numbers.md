# 几乎素数

> 原文:[https://www.geeksforgeeks.org/almost-prime-numbers/](https://www.geeksforgeeks.org/almost-prime-numbers/)

k-几乎素数是具有恰好 k 个素数因子(不一定是截然不同的)的数。

**例如**，

2, 3, 5, 7, 11 ….(事实上所有质数)都是 1-几乎质数，因为它们只有 1 个质因数(也就是它们自己)。

4, 6, 9….是 2-几乎素数，因为它们正好有 2 个质因数(4 = 2*2，6 = 2*3，9 = 3*3)

同样，32 是一个 5-几乎素数(32 = 2*2*2*2*2)，72 也是(2*2*2*3*3)

所有的 1-几乎素数称为素数，所有的 2-几乎素数称为半素数。
任务是打印前 n 个 k 素数。

**示例:**

```
Input: k = 2, n = 5
Output: 4 6 9 10 14
4 has two prime factors, 2 x 2
6 has two prime factors, 2 x 3
Similarly, 9(3 x 3), 10(2 x 5) and 14(2 x 7)

Input: k = 10, n = 2
Output: 1024 1536
1024 and 1536 are first two numbers with 10
prime factors.
```

我们迭代自然数，并一直打印 k-素数，直到打印的 k-素数的计数小于或等于 n。为了检查一个数是否是 k-素数，我们[找到素数因子的计数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)，如果计数是 k，我们认为这个数是 k-素数。

下面是上述方法的实现:

## C++

```
// Program to print first n numbers that are k-primes
#include<bits/stdc++.h>
using namespace std;

// A function to count all prime factors of a given number
int countPrimeFactors(int n)
{
    int count = 0;

    // Count the number of 2s that divide n
    while (n%2 == 0)
    {
        n = n/2;
        count++;
    }

    // n must be odd at this point. So we can skip one
    // element (Note i = i +2)
    for (int i = 3; i <= sqrt(n); i = i+2)
    {
        // While i divides n, count i and divide n
        while (n%i == 0)
        {
            n = n/i;
            count++;
        }
    }

    // This condition is to handle the case when n is a
    // prime number greater than 2
    if (n > 2)
        count++;

    return(count);
}

// A function to print the first n numbers that are
// k-almost primes.
void printKAlmostPrimes(int k, int n)
{
    for (int i=1, num=2; i<=n; num++)
    {
        // Print this number if it is k-prime
        if (countPrimeFactors(num) == k)
        {
            printf("%d ", num);

            // Increment count of k-primes printed
            // so far
            i++;
        }
    }
    return;
}

/* Driver program to test above function */
int main()
{
    int n = 10, k = 2;
    printf("First %d %d-almost prime numbers : \n",
           n, k);
    printKAlmostPrimes(k, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to print first n numbers that
// are k-primes

import java.io.*;

class GFG {

    // A function to count all prime factors
    // of a given number
    static int countPrimeFactors(int n)
    {

        int count = 0;

        // Count the number of 2s that divide n
        while (n % 2 == 0) {

            n = n / 2;
            count++;
        }

        // n must be odd at this point. So we
        // can skip one element (Note i = i +2)
        for (int i = 3; i <= Math.sqrt(n);
                                  i = i + 2) {

            // While i divides n, count i and
            // divide n
            while (n % i == 0) {

                n = n / i;
                count++;
            }
        }

        // This condition is to handle the case
        // when n is a prime number greater
        // than 2
        if (n > 2)
            count++;

        return (count);
    }

    // A function to print the first n numbers
    // that are k-almost primes.
    static void printKAlmostPrimes(int k, int n)
    {

        for (int i = 1, num = 2; i <= n; num++) {

            // Print this number if it is k-prime
            if (countPrimeFactors(num) == k) {

                System.out.print(num + " ");

                // Increment count of k-primes
                // printed so far
                i++;
            }
        }

        return;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int n = 10, k = 2;
        System.out.println("First " + n + " "
             + k + "-almost prime numbers : ");

        printKAlmostPrimes(k, n);
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 Program to print first
# n numbers that are k-primes
import math

# A function to count all prime
# factors of a given number
def countPrimeFactors(n):
    count = 0;

    # Count the number of
    # 2s that divide n
    while(n % 2 == 0):
        n = n / 2;
        count += 1;

    # n must be odd at this point.
    # So we can skip one
    # element (Note i = i +2)
    i = 3;
    while(i <= math.sqrt(n)):

        # While i divides n,
        # count i and divide n
        while (n % i == 0):
            n = n / i;
            count += 1;
        i = i + 2;

    # This condition is to handle
    # the case when n is a
    # prime number greater than 2
    if (n > 2):
        count += 1;

    return(count);

# A function to print the
# first n numbers that are
# k-almost primes.
def printKAlmostPrimes(k, n):
    i = 1;
    num = 2
    while(i <= n):

        # Print this number if
        # it is k-prime
        if (countPrimeFactors(num) == k):
            print(num, end = "");
            print(" ", end = "");

            # Increment count of
            # k-primes printed
            # so far
            i += 1;
        num += 1;
    return;

# Driver Code
n = 10;
k = 2;
print("First n k-almost prime numbers:");
printKAlmostPrimes(k, n);

# This code is contributed by mits
```

## C#

```
// C# Program to print first n
// numbers that are k-primes
using System;

class GFG
{

    // A function to count all prime 
    // factors of a given number
    static int countPrimeFactors(int n)
    {
        int count = 0;

        // Count the number of 2s that divide n
        while (n % 2 == 0)
        {
            n = n / 2;
            count++;
        }

        // n must be odd at this point. So we
        // can skip one element (Note i = i +2)
        for (int i = 3; i <= Math.Sqrt(n);
                                i = i + 2)
        {

            // While i divides n, count i and
            // divide n
            while (n % i == 0)
            {
                n = n / i;
                count++;
            }
        }

        // This condition is to handle
        // the case when n is a prime
        // number greater than 2
        if (n > 2)
            count++;

        return (count);
    }

    // A function to print the first n
    // numbers that are k-almost primes.
    static void printKAlmostPrimes(int k, int n)
    {

        for (int i = 1, num = 2; i <= n; num++)
        {

            // Print this number if it is k-prime
            if (countPrimeFactors(num) == k)
            {
                   Console.Write(num + " ");

                // Increment count of k-primes
                // printed so far
                i++;
            }
        }

        return;
    }

    // Driver code
    public static void Main()
    {
        int n = 10, k = 2;
        Console.WriteLine("First " + n + " "
            + k + "-almost prime numbers : ");

        printKAlmostPrimes(k, n);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print first
// n numbers that are k-primes

// A function to count all prime
// factors of a given number
function countPrimeFactors($n)
{
    $count = 0;

    // Count the number of
    // 2s that divide n
    while($n % 2 == 0)
    {
        $n = $n / 2;
        $count++;
    }

    // n must be odd at this point.
    // So we can skip one
    // element (Note i = i +2)
    for ($i = 3; $i <= sqrt($n); $i = $i + 2)
    {

        // While i divides n,
        // count i and divide n
        while ($n % $i == 0)
        {
            $n = $n/$i;
            $count++;
        }
    }

    // This condition is to handle
    // the case when n is a
    // prime number greater than 2
    if ($n > 2)
        $count++;

    return($count);
}

// A function to print the
// first n numbers that are
// k-almost primes.
function printKAlmostPrimes($k, $n)
{
    for ($i = 1, $num = 2; $i <= $n; $num++)
    {

        // Print this number if
        // it is k-prime
        if (countPrimeFactors($num) == $k)
        {
            echo($num);
            echo(" ");

            // Increment count of
            // k-primes printed
            // so far
            $i++;
        }
    }
    return;
}

    // Driver Code
    $n = 10;
    $k = 2;
    echo "First $n $k-almost prime numbers:\n";
    printKAlmostPrimes($k, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to print first n numbers that
// are k-primes

    // A function to count all prime factors
    // of a given number
    function countPrimeFactors(n)
    {

        let count = 0;

        // Count the number of 2s that divide n
        while (n % 2 == 0) {

            n = n / 2;
            count++;
        }

        // n must be odd at this point. So we
        // can skip one element (Note i = i +2)
        for (let i = 3; i <= Math.sqrt(n);
                                  i = i + 2) {

            // While i divides n, count i and
            // divide n
            while (n % i == 0) {

                n = n / i;
                count++;
            }
        }

        // This condition is to handle the case
        // when n is a prime number greater
        // than 2
        if (n > 2)
            count++;

        return (count);
    }

    // A function to print the first n numbers
    // that are k-almost primes.
    function printKAlmostPrimes(k, n)
    {

        for (let i = 1, num = 2; i <= n; num++) {

            // Print this number if it is k-prime
            if (countPrimeFactors(num) == k) {

                document.write(num + " ");

                // Increment count of k-primes
                // printed so far
                i++;
            }
        }

        return;
    }

// Driver Code

        let n = 10, k = 2;
        document.write("First " + n + " "
             + k + "-almost prime numbers : " + "<br/>");

        printKAlmostPrimes(k, n);

</script>
```

**Output**

```
First 10 2-almost prime numbers : 
4 6 9 10 14 15 21 22 25 26 
```

**参考文献:**T2】https://en.wikipedia.org/wiki/Almost_prime

本文由**拉希特·贝尔瓦亚尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。