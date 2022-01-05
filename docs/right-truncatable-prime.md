# 右截断素数

> 原文:[https://www.geeksforgeeks.org/right-truncatable-prime/](https://www.geeksforgeeks.org/right-truncatable-prime/)

右截断素数是当最后一个(“右”)数字被连续删除时仍保持素数的素数。例如，239 是右截断素数，因为 239、23 和 2 都是素数。有 83 个右截断素数。
任务是检查给定的数(N > 0)是否为右截质数。
**例:**

```
Input: 239
Output: Yes

Input: 101
Output: No
101 is not right-truncatable prime because 
numbers formed are 101, 10 and 1\. Here, 101 
is prime but 10 and 1 are not prime.
```

其思想是利用厄拉多塞的[筛生成所有小于或等于给定数 N 的素数。一旦我们生成了所有这样的素数，然后我们检查当最后一个(“右”)数字被连续移除时，这个数是否仍然是素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// Program to check
// whether a given number
// is right-truncatable
// prime or not.
#include<bits/stdc++.h>
using namespace std;

// Generate all prime numbers less than n.
bool sieveOfEratosthenes(int n, bool isPrime[])
{
    // Initialize all entries
    // of boolean array as
    // true. A value in
    // isPrime[i] will finally
    // be false if i is Not a
    // prime, else true
    // bool isPrime[n+1];
    isPrime[0] = isPrime[1] = false;
    for( int i = 2; i <= n; i++)
        isPrime[i] = true;

    for (int p = 2; p * p<=n; p++)
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

// Returns true if n is right-truncatable,
// else false
bool rightTruPrime(int n)
{
    // Generating primes using Sieve
    bool isPrime[n+1];
    sieveOfEratosthenes(n, isPrime);

    // Checking whether the number remains
    // prime when the last ("right")
    // digit is successively removed
    while (n)
    {
        if (isPrime[n])
            n = n / 10;
        else
            return false;
    }
    return true;
}

// Driver program
int main()
{
    int n = 59399;
    if (rightTruPrime(n))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check
// right-truncatable
// prime or not.
import java.io.*;

class GFG {

    // Generate all prime
    // numbers less than n.
    static void sieveOfEratosthenes
                (int n, boolean isPrime[])
    {

        // Initialize all entries of
        // boolean array as true. A
        // value in isPrime[i] will
        // finally be false if i is
        // Not a prime, else true
        // bool isPrime[n+1];
        isPrime[0] = isPrime[1] = false;
        for (int i = 2; i <= n; i++)
            isPrime[i] = true;

        for (int p=2; p*p<=n; p++)
        {
            // If isPrime[p] is not
            // changed, then it
            // is a prime
            if (isPrime[p] == true)
            {
                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // Returns true if n is
    // right-truncatable,
    // else false
    static boolean rightTruPrime(int n)
     {

        // Generating primes using Sieve
        boolean isPrime[] = new boolean[n+1];
        sieveOfEratosthenes(n, isPrime);

        // Checking whether the number
        // remains prime when the last (right)
        // digit is successively removed
        while (n != 0)
        {

            if (isPrime[n])
                n = n / 10;
            else
                return false;
        }
        return true;
    }

    // Driver program
    public static void main(String args[])
    {
        int n = 59399;

        if (rightTruPrime(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 Program to check
# whether a given number
# is right-truncatable
# prime or not.

# Generate all prime numbers less than n.
def sieveOfEratosthenes(n,isPrime) :

    # Initialize all entries
    # of boolean array as
    # true. A value in isPrime[i]
    # will finally be false if
    # i is Not a prime, else true
    # bool isPrime[n+1];
    isPrime[0] = isPrime[1] = False
    for i in range(2, n+1) :
        isPrime[i] = True
    p = 2
    while(p * p <= n) :
        # If isPrime[p] is not changed, then it is
        # a prime
        if (isPrime[p] == True) :
            # Update all multiples of p
            i = p * 2
            while(i <= n) :
                isPrime[i] = False
                i = i + p
        p = p + 1

# Returns true if n is right-truncatable, else false
def rightTruPrime(n) :
    # Generating primes using Sieve
    isPrime=[None] * (n+1)
    sieveOfEratosthenes(n, isPrime)

    # Checking whether the
    # number remains prime
    # when the last ("right")
    # digit is successively
    # removed
    while (n != 0) :
        if (isPrime[n]) :
            n = n // 10    
        else :
            return False

    return True

# Driven program
n = 59399
if (rightTruPrime(n)) :
    print("Yes")
else :
    print("No")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# code to check right-
// truncatable prime or not
using System;

class GFG {

    // Generate all prime
    // numbers less than n.
    static void sieveOfEratosthenes(int n, bool[] isPrime)
    {

        // Initialize all entries of
        // boolean array as true. A
        // value in isPrime[i] will
        // finally be false if i is
        // Not a prime, else true
        // bool isPrime[n+1];
        isPrime[0] = isPrime[1] = false;

        for (int i = 2; i <= n; i++)
            isPrime[i] = true;

        for (int p = 2; p * p <= n; p++) {
            // If isPrime[p] is not
            // changed, then it
            // is a prime
            if (isPrime[p] == true) {
                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // Returns true if n is right-
    // truncatable,  else false
    static bool rightTruPrime(int n)
    {

        // Generating primes using Sieve
        bool[] isPrime = new bool[n + 1];
        sieveOfEratosthenes(n, isPrime);

        // Checking whether the number
        // remains prime when last (right)
        // digit is successively removed
        while (n != 0) {

            if (isPrime[n])
                n = n / 10;
            else
                return false;
        }
        return true;
    }

    // Driven program
    public static void Main()
    {
        int n = 59399;

        if (rightTruPrime(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Anant Agarwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to check whether a given number
// is right-truncatable prime or not.

// Generate all prime numbers less than n.
function sieveOfEratosthenes($n, &$isPrime)
{
    // Initialize all entries of boolean
    // array as true. A value in isPrime[i]
    // will finally be false if i is Not a
    // prime, else true bool isPrime[n+1];
    $isPrime[0] = $isPrime[1] = false;

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

// Returns true if n is right-truncatable,
// else false
function rightTruPrime($n)
{
    // Generating primes using Sieve
    $isPrime = array_fill(0, $n + 1, true);
    sieveOfEratosthenes($n, $isPrime);

    // Checking whether the number remains
    // prime when the last ("right")
    // digit is successively removed
    while ($n)
    {
        if ($isPrime[$n])
            $n = (int)($n / 10);
        else
            return false;
    }
    return true;
}

// Driver Code
$n = 59399;
if (rightTruPrime($n))
    echo "Yes\n";
else
    echo "No\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript code to check
// right-truncatable
// prime or not.

    // Generate all prime
    // numbers less than n.
    function sieveOfEratosthenes(n, isPrime)
    {

        // Initialize all entries of
        // boolean array as true. A
        // value in isPrime[i] will
        // finally be false if i is
        // Not a prime, else true
        // bool isPrime[n+1];
        isPrime[0] = isPrime[1] = false;
        for (let i = 2; i <= n; i++)
            isPrime[i] = true;

        for (let p = 2; p * p <= n; p++) {
            // If isPrime[p] is not
            // changed, then it
            // is a prime
            if (isPrime[p] == true) {
                // Update all multiples of p
                for (let i = p * 2; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // Returns true if n is
    // right-truncatable,
    // else false
    function rightTruPrime(n)
    {

        // Generating primes using Sieve
        let isPrime = new Array(n + 1).fill(false);
        sieveOfEratosthenes(n, isPrime);

        // Checking whether the number
        // remains prime when the last (right)
        // digit is successively removed
        while (n != 0) {

            if (isPrime[n])
                n = parseInt(n / 10);
            else
                return false;
        }
        return true;
    }

    // Driver program
    var n = 59399;
    if (rightTruPrime(n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by shikhasingrajput
</script>
```

**输出:**

```
Yes
```

**相关文章:** [左截断撇](https://www.geeksforgeeks.org/left-truncatable-prime/)
T5【参考文献:
[https://en.wikipedia.org/wiki/Truncatable_prime](https://en.wikipedia.org/wiki/Truncatable_prime)
本文由**拉胡尔·阿格沃尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。