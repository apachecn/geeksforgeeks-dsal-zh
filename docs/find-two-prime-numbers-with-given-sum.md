# 求两个给定和的素数

> 原文:[https://www . geesforgeks . org/find-two-prime-numbers-with-given-sum/](https://www.geeksforgeeks.org/find-two-prime-numbers-with-given-sum/)

给定一个偶数(大于 2)，打印两个素数，它们的和等于给定的数。可能有几种可能的组合。只打印第一对这样的。
有意思的一点是，根据[哥德巴赫猜想](https://en.wikipedia.org/wiki/Goldbach's_conjecture)，解总是存在的。
**示例:**

```
Input: n = 74
Output: 3 71

Input : n = 1024
Output: 3 1021

Input: n = 66
Output: 5 61

Input: n = 9990
Output: 17 9973
```

其思想是利用厄拉多塞的[筛找出所有小于或等于给定数 N 的素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)一旦我们有了一个告诉所有素数的数组，我们就可以遍历这个数组，找到给定和的对。

## C++

```
// C++ program to find a prime number pair whose
// sum is equal to given number
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
    for (int i=2; i<=n; i++)
        isPrime[i] = true;

    for (int p=2; p*p<=n; p++)
    {
        // If isPrime[p] is not changed, then it is
        // a prime
        if (isPrime[p] == true)
        {
            // Update all multiples of p
            for (int i=p*p; i<=n; i += p)
                isPrime[i] = false;
        }
    }
}

// Prints a prime pair with given sum
void findPrimePair(int n)
{
    // Generating primes using Sieve
    bool isPrime[n+1];
    SieveOfEratosthenes(n, isPrime);

    // Traversing all numbers to find first
    // pair
    for (int i=0; i<n; i++)
    {
        if (isPrime[i] && isPrime[n-i])
        {
            cout << i << " " << (n-i);
            return;
        }
    }
}

// Driven program
int main()
{
    int n = 74;
    findPrimePair(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a prime number pair whose
// sum is equal to given number
// Java program to print super primes less than
// or equal to n.

class GFG
{
    // Generate all prime numbers less than n.
    static boolean SieveOfEratosthenes(int n, boolean isPrime[])
    {
        // Initialize all entries of boolean
        // array as true. A value in isPrime[i]
        // will finally be false if i is Not a
        // prime, else true bool isPrime[n+1];
        isPrime[0] = isPrime[1] = false;
        for (int i = 2; i <= n; i++)
            isPrime[i] = true;

        for (int p = 2; p * p <= n; p++)
        {
            // If isPrime[p] is not changed,
            // then it is a prime
            if (isPrime[p] == true)
            {
                // Update all multiples of p
                for (int i = p * p; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
        return false;
    }

    // Prints a prime pair with given sum
    static void findPrimePair(int n)
    {
        // Generating primes using Sieve
        boolean isPrime[]=new boolean[n + 1];
        SieveOfEratosthenes(n, isPrime);

        // Traversing all numbers to find first
        // pair
        for (int i = 0; i < n; i++)
        {
            if (isPrime[i] && isPrime[n - i])
            {
                System.out.print(i + " " + (n - i));
                return;
            }
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 74;
        findPrimePair(n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 program to find a prime number
# pair whose sum is equal to given number
# Python 3 program to print super primes
# less than or equal to n.

# Generate all prime numbers less than n.
def SieveOfEratosthenes(n, isPrime):

    # Initialize all entries of boolean
    # array as True. A value in isPrime[i]
    # will finally be False if i is Not a
    # prime, else True bool isPrime[n+1]
    isPrime[0] = isPrime[1] = False
    for i in range(2, n+1):
        isPrime[i] = True

    p = 2
    while(p*p <= n):

        # If isPrime[p] is not changed,
        # then it is a prime
        if (isPrime[p] == True):

            # Update all multiples of p
            i = p*p
            while(i <= n):
                isPrime[i] = False
                i += p
        p += 1

# Prints a prime pair with given sum
def findPrimePair(n):

    # Generating primes using Sieve
    isPrime = [0] * (n+1)
    SieveOfEratosthenes(n, isPrime)

    # Traversing all numbers to find
    # first pair
    for i in range(0, n):

        if (isPrime[i] and isPrime[n - i]):

            print(i,(n - i))
            return

# Driven program
n = 74
findPrimePair(n)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find a prime number pair whose
// sum is equal to given number
// C# program to print super primes less than
// or equal to n.
using System;

class GFG
{
    // Generate all prime numbers less than n.
    static bool SieveOfEratosthenes(int n, bool []isPrime)
    {
        // Initialize all entries of boolean
        // array as true. A value in isPrime[i]
        // will finally be false if i is Not a
        // prime, else true bool isPrime[n+1];
        isPrime[0] = isPrime[1] = false;
        for (int i = 2; i <= n; i++)
            isPrime[i] = true;

        for (int p = 2; p * p <= n; p++)
        {
            // If isPrime[p] is not changed,
            // then it is a prime
            if (isPrime[p] == true)
            {
                // Update all multiples of p
                for (int i = p * p; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
        return false;
    }

    // Prints a prime pair with given sum
    static void findPrimePair(int n)
    {
        // Generating primes using Sieve
        bool []isPrime=new bool[n + 1];
        SieveOfEratosthenes(n, isPrime);

        // Traversing all numbers to find first
        // pair
        for (int i = 0; i < n; i++)
        {
            if (isPrime[i] && isPrime[n - i])
            {
                Console.Write(i + " " + (n - i));
                return;
            }
        }
    }

    // Driver code
    public static void Main ()
    {
        int n = 74;
        findPrimePair(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a prime
// number pair whose sum is equal
// to given number

// Generate all prime numbers
// less than n.
function SieveOfEratosthenes($n, &$isPrime)
{
    // Initialize all entries of
    // boolean array as true. A value
    // in isPrime[i] will finally
    // be false if i is Not a prime,
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
            for ($i = $p * $p;
                 $i <= $n; $i += $p)
                $isPrime[$i] = false;
        }
    }
}

// Prints a prime pair with given sum
function findPrimePair($n)
{
    // Generating primes using Sieve
    $isPrime = array_fill(0, $n + 1, NULL);
    SieveOfEratosthenes($n, $isPrime);

    // Traversing all numbers
    // to find first pair
    for ($i = 0; $i < $n; $i++)
    {
        if ($isPrime[$i] &&
            $isPrime[$n - $i])
        {
            echo $i . " " . ($n - $i);
            return;
        }
    }
}

// Driver Code
$n = 74;
findPrimePair($n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find a prime number pair whose
// sum is equal to given number
// Java program to print super primes less than
// or equal to n.

    // Generate all prime numbers less than n.
    function SieveOfEratosthenes(n,isPrime)
    {
        // Initialize all entries of boolean
        // array as true. A value in isPrime[i]
        // will finally be false if i is Not a
        // prime, else true bool isPrime[n+1];
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
                for (let i = p * p; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
        return false;
    }

    // Prints a prime pair with given sum
    function findPrimePair(n)
    {
        // Generating primes using Sieve
        let isPrime = new Array(n+1);
        for(let i=0;i<n+1;i++)
        {
            isPrime[i]=false;
        }
        SieveOfEratosthenes(n, isPrime);

        // Traversing all numbers to find first
        // pair
        for (let i = 0; i < n; i++)
        {
            if (isPrime[i] && isPrime[n - i])
            {
                document.write(i + " " + (n - i));
                return;
            }
        }
    }

    // Driver code
    let  n = 74;
    findPrimePair(n);

    // This code is contributed by rag2127

</script>
```

**输出:**

```
3 71
```

本文由**拉克什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。