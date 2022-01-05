# 超级质数

> 原文:[https://www.geeksforgeeks.org/super-prime/](https://www.geeksforgeeks.org/super-prime/)

**超素数**数(也称为**高阶素数**)是在所有素数序列中占据素数位置的素数子序列。前几个超级素数是 3，5，11 和 17。
任务是打印所有小于等于给定正整数 n 的超级素数
**示例:**

```
Input: 7
Output: 3 5 
3 is super prime because it appears at second
position in list of primes (2, 3, 5, 7, 11, 13, 
17, 19, 23, ...) and 2 is also prime. Similarly
5 appears at third position and 3 is a prime.

Input: 17
Output: 3 5 11 17
```

其思想是利用厄拉多塞的[筛生成所有小于或等于给定数 N 的素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)一旦我们生成了所有这样的素数，我们就遍历所有的数，并将其存储在数组中。一旦我们存储了数组中的所有素数，我们就遍历数组并打印所有在数组中占据素数位置的素数。

## C++

```
// C++ program to print super primes less than
// or equal to n.
#include<bits/stdc++.h>
using namespace std;

// Generate all prime numbers less than n.
bool SieveOfEratosthenes(int n, bool isPrime[])
{
    // Initialize all entries of boolean array
    // as true. A value in isPrime[i] will finally
    // be false if i is Not a prime, else true
    // bool isPrime[n+1];
    isPrime[0] = isPrime[1] = false;
    for (int i = 2; i <= n; i++)
        isPrime[i] = true;

    for (int p = 2; p * p <= n; p++)
    {
        // If isPrime[p] is not changed, then it is
        // a prime
        if (isPrime[p] == true)
        {
            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                isPrime[i] = false;
        }
    }
}

// Prints all super primes less than or equal to n.
void superPrimes(int n)
{
    // Generating primes using Sieve
    bool isPrime[n + 1];
    SieveOfEratosthenes(n, isPrime);

    // Storing all the primes generated in a
    // an array primes[]
    int primes[n + 1], j = 0;
    for (int p = 2; p <= n; p++)
    if (isPrime[p])
        primes[j++] = p;

    // Printing all those prime numbers that
    // occupy prime numbered position in
    // sequence of prime numbers.
    for (int k = 0; k < j; k++)
        if (isPrime[k + 1])
            cout << primes[k] << " ";
}

// Driven program
int main()
{
    int n = 241;
    cout << "Super-Primes less than or equal to "
        << n << " are :"<<endl;
    superPrimes(n);
    return 0;
}

// This code is contributed by code_hunt.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print super
// primes less than or equal to n.
import java.io.*;

class GFG {

    // Generate all prime
    // numbers less than n.
    static void SieveOfEratosthenes
                (int n, boolean isPrime[])
    {
        // Initialize all entries of boolean
        // array as true. A value in isPrime[i]
        // will finally be false if i is Not
        // a prime, else true bool isPrime[n+1];
        isPrime[0] = isPrime[1] = false;
        for (int i=2; i<=n; i++)
            isPrime[i] = true;

        for (int p=2; p*p<=n; p++)
        {
            // If isPrime[p] is not changed,
            // then it is a prime
            if (isPrime[p] == true)
            {
                // Update all multiples of p
                for (int i=p*2; i<=n; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // Prints all super primes less
    // than or equal to n.
    static void superPrimes(int n)
    {

        // Generating primes using Sieve
        boolean isPrime[]=new boolean[n+1];
        SieveOfEratosthenes(n, isPrime);

        // Storing all the primes generated
        // in a an array primes[]
        int primes[] = new int[n+1];
        int j = 0;

        for (int p=2; p<=n; p++)
            if (isPrime[p])
                primes[j++] = p;

        // Printing all those prime numbers that
        // occupy prime numbered position in
        // sequence of prime numbers.
        for (int k=0; k<j; k++)
            if (isPrime[k+1])
                System.out.print(primes[k]+ " ");
    }

    // Driven program
    public static void main(String args[])
    {
        int n = 241;
        System.out.println("Super-Primes less than or equal to "
                            +n+" are :");
        superPrimes(n);
    }
}

// This code is contributed by Nikita Tiwari.
```

## 计算机编程语言

```
# Python program to print super primes less than
# or equal to n.

# Generate all prime numbers less than n.
def SieveOfEratosthenes(n, isPrime):
    # Initialize all entries of boolean array
    # as true. A value in isPrime[i] will finally
    # be false if i is Not a prime, else true
    # bool isPrime[n+1]
    isPrime[0] = isPrime[1] = False
    for i in range(2,n+1):
        isPrime[i] = True

    for p in range(2,n+1):
        # If isPrime[p] is not changed, then it is
        # a prime
        if (p*p<=n and isPrime[p] == True):
            # Update all multiples of p
            for i in range(p*2,n+1,p):
                isPrime[i] = False
                p += 1
def superPrimes(n):

    # Generating primes using Sieve
    isPrime = [1 for i in range(n+1)]
    SieveOfEratosthenes(n, isPrime)

    # Storing all the primes generated in a
    # an array primes[]
    primes = [0 for i in range(2,n+1)]
    j = 0
    for p in range(2,n+1):
       if (isPrime[p]):
           primes[j] = p
           j += 1

    # Printing all those prime numbers that
    # occupy prime numbered position in
    # sequence of prime numbers.
    for k in range(j):
        if (isPrime[k+1]):
            print primes[k],

n = 241
print "Super-Primes less than or equal to ", n, " are :n",
superPrimes(n)

# Contributed by: Afzal
```

## C#

```
// Program to print super primes
// less than or equal to n.
using System;

class GFG {

    // Generate all prime
    // numbers less than n.
    static void SieveOfEratosthenes(int n, bool[] isPrime)
    {
        // Initialize all entries of boolean
        // array as true. A value in isPrime[i]
        // will finally be false if i is Not
        // a prime, else true bool isPrime[n+1];
        isPrime[0] = isPrime[1] = false;

        for (int i = 2; i <= n; i++)
            isPrime[i] = true;

        for (int p = 2; p * p <= n; p++) {
            // If isPrime[p] is not changed,
            // then it is a prime
            if (isPrime[p] == true) {
                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // Prints all super primes less
    // than or equal to n.
    static void superPrimes(int n)
    {

        // Generating primes using Sieve
        bool[] isPrime = new bool[n + 1];
        SieveOfEratosthenes(n, isPrime);

        // Storing all the primes generated
        // in a an array primes[]
        int[] primes = new int[n + 1];
        int j = 0;

        for (int p = 2; p <= n; p++)
            if (isPrime[p])
                primes[j++] = p;

        // Printing all those prime numbers
        // that occupy prime number position
        // in sequence of prime numbers.
        for (int k = 0; k < j; k++)
            if (isPrime[k + 1])
                Console.Write(primes[k] + " ");
    }

    // Driven program
    public static void Main()
    {
        int n = 241;
        Console.WriteLine("Super-Primes less than or equal to "
                          + n + " are :");
        superPrimes(n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print super primes
// less than or equal to n.

// Generate all prime numbers less than n.
function SieveOfEratosthenes($n, &$isPrime)
{
    // Initialize all entries of boolean array
    // as true. A value in isPrime[i] will
    // finally be false if i is Not a prime,
    // else true bool isPrime[n+1];
    $isPrime[0] = $isPrime[1] = false;
    for ($i = 2; $i <= $n; $i++)
        $isPrime[$i] = true;

    for ($p = 2; $p * $p <= $n; $p++)
    {
        // If isPrime[p] is not changed,
        // then it is a prime
        if ($isPrime[$p] == true)
        {
            // Update all multiples of p
            for ($i = $p * 2; $i <= $n; $i += $p)
                $isPrime[$i] = false;
        }
    }
}

// Prints all super primes less
// than or equal to n.
function superPrimes($n)
{
    // Generating primes using Sieve
    $isPrime = array_fill(0, $n + 1, false);
    SieveOfEratosthenes($n, $isPrime);

    // Storing all the primes generated
    // in a an array primes[]
    $primes = array_fill(0, $n + 1, 0);
    $j = 0;
    for ($p = 2; $p <= $n; $p++)
    if ($isPrime[$p])
        $primes[$j++] = $p;

    // Printing all those prime numbers
    // that occupy prime numbered position
    // in sequence of prime numbers.
    for ($k = 0; $k < $j; $k++)
        if ($isPrime[$k + 1])
            echo $primes[$k] . " ";
}

// Driver Code
$n = 241;
echo "Super-Primes less than or equal to " .
                            $n . " are :\n";
superPrimes($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to print super
// primes less than or equal to n.

    // Generate all prime
    // numbers less than n.
    function SieveOfEratosthenes
                (n, isPrime)
    {
        // Initialize all entries of boolean
        // array as true. A value in isPrime[i]
        // will finally be false if i is Not
        // a prime, else true bool isPrime[n+1];
        isPrime[0] = isPrime[1] = false;
        for (let i = 2; i <= n; i++)
            isPrime[i] = true;

        for (let p = 2; p * p <= n; p++)
        {
            // If isPrime[p] is not changed,
            // then it is a prime
            if (isPrime[p] == true)
            {
                // Update all multiples of p
                for (let i = p * 2; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // Prints all super primes less
    // than or equal to n.
    function superPrimes(n)
    {

        // Generating primes using Sieve
        let isPrime = [];
        SieveOfEratosthenes(n, isPrime);

        // Storing all the primes generated
        // in a an array primes[]
        let primes = [];
        let j = 0;

        for (let p = 2; p <= n; p++)
            if (isPrime[p] != 0)
                primes[j++] = p;

        // Printing all those prime numbers that
        // occupy prime numbered position in
        // sequence of prime numbers.
        for (let k = 0; k < j; k++)
            if (isPrime[k + 1])
                document.write(primes[k]+ " ");
    }

// Driver Code
        let n = 241;
        document.write("Super-Primes less than or equal to "
                            +n+" are :" + "<br/>");
        superPrimes(n);

// This code is contributed by code_hunt.
</script>
```

**输出:**

```
Super-Primes less than or equal to 241 are :
3 5 11 17 31 41 59 67 83 109 127 157 179 191 211 241 
```

**参考文献:**[【https://en.wikipedia.org/wiki/Super-prime】](https://en.wikipedia.org/wiki/Super-prime)
本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。-