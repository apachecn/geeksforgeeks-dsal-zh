# 左截断素数

> 原文:[https://www.geeksforgeeks.org/left-truncatable-prime/](https://www.geeksforgeeks.org/left-truncatable-prime/)

一个**左截断素数**是一个素数，在给定的基数(比如 10)中不包含 0，并且当前导(“左”)数字被连续移除时，它仍然是素数。例如，317 是可左截断的素数，因为 317、17 和 7 都是素数。总共有 4260 个可左截断的素数。
任务是检查给定的数(N > 0)是否是可左截断的素数。
示例:

```
Input: 317
Output: Yes

Input: 293
Output: No
293 is not left-truncatable prime because 
numbers formed are 293, 93 and 3\. Here, 293 
and 3 are prime but 93 is not prime.
```

其思想是首先检查数字是否包含 0 作为数字，并计算给定数字 N 中的位数，如果包含 0，则返回 false，否则使用厄拉多塞[筛生成所有小于或等于给定数字 N 的素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)。一旦我们生成了所有这样的素数，然后我们检查当前导(“左”)数字被连续移除时，这个数是否仍然是素数。
以下是上述办法的实施情况。

## C++

```
// Program to check whether a given number
// is left-truncatable prime or not.
#include<bits/stdc++.h>
using namespace std;

/* Function to calculate x raised to the power y */
int power(int x, unsigned int y)
{
    if (y == 0)
        return 1;
    else if (y%2 == 0)
        return power(x, y/2)*power(x, y/2);
    else
        return x*power(x, y/2)*power(x, y/2);
}

// Generate all prime numbers less than n.
bool sieveOfEratosthenes(int n, bool isPrime[])
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
            for (int i=p*2; i<=n; i += p)
                isPrime[i] = false;
        }
    }
}

// Returns true if n is right-truncatable, else false
bool leftTruPrime(int n)
{
    int temp = n, cnt = 0, temp1;

    // Counting number of digits in the
    // input number and checking whether it
    // contains 0 as digit or not.
    while (temp)
    {
        cnt++; // counting number of digits.

        temp1 = temp%10; // checking whether digit is 0 or not
        if (temp1==0)
            return false; // if digit is 0, return false.
        temp = temp/10;
    }

    // Generating primes using Sieve
    bool isPrime[n+1];
    sieveOfEratosthenes(n, isPrime);

    // Checking whether the number remains prime
    // when the leading ("left") digit is successively
    // removed
    for (int i=cnt; i>0; i--)
    {
        // Checking number by successively removing
        // leading ("left") digit.
        /* n=113, cnt=3
        i=3 mod=1000 n%mod=113
        i=2 mod=100 n%mod=13
        i=3 mod=10 n%mod=3 */
        int mod=  power(10,i);

        if (!isPrime[n%mod]) // checking prime
            return false; // if not prime, return false
    }
    return true; // if remains prime, return true
}

// Driver program
int main()
{
    int n = 113;

    if (leftTruPrime(n))
        cout << n << " is left truncatable prime" << endl;
    else
        cout << n << " is not left truncatable prime" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to check whether
// a given number is left
// truncatable prime or not.
import java.io.*;

class GFG {

    // Function to calculate x
    // raised to the power y
    static int power(int x,int y)
    {
        if (y == 0)
            return 1;
        else if (y%2 == 0)
            return power(x, y/2)
                   *power(x, y/2);
        else
            return x*power(x, y/2)
                   *power(x, y/2);
    }

    // Generate all prime
    // numbers less than n.
    static void sieveOfEratosthenes
                (int n, boolean isPrime[])
    {

        // Initialize all entries of boolean
        // array as true. A value in isPrime[i]
        // will finally be false if i is Not
        // a prime, else true bool isPrime[n+1];
        isPrime[0] = isPrime[1] = false;
        for (int i = 2; i <= n; i++)
            isPrime[i] = true;

        for (int p = 2; p*p <= n; p++)
        {
            // If isPrime[p] is not changed,
            // then it is a prime
            if (isPrime[p] == true)
            {

                // Update all multiples of p
                for (int i = p*2; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // Returns true if n is
    // right-truncatable, else false
    static boolean leftTruPrime(int n)
    {
        int temp = n, cnt = 0, temp1;

        // Counting number of digits in the
        // input number and checking whether
        // it contains 0 as digit or not.
        while (temp != 0)
        {
            // counting number of digits.
            cnt++;

            temp1 = temp%10;

            // checking whether digit is
            // 0 or not
            if (temp1 == 0)
                return false;
            temp = temp/10;
        }

        // Generating primes using Sieve
        boolean isPrime[] = new boolean[n+1];
        sieveOfEratosthenes(n, isPrime);

        // Checking whether the number
        // remains prime when the leading
        // ("left") digit is successively removed
        for (int i = cnt; i > 0; i--)
        {
            // Checking number by successively
            // removing leading ("left") digit.
            /* n=113, cnt=3
            i=3 mod=1000 n%mod=113
            i=2 mod=100 n%mod=13
            i=3 mod=10 n%mod=3 */
            int mod =  power(10,i);

            if (!isPrime[n%mod])
                return false;
        }

        // if remains prime, return true
        return true;
    }

    // Driver program
    public static void main(String args[])
    {
        int n = 113;

        if (leftTruPrime(n))
            System.out.println
                   (n+" is left truncatable prime");
        else
            System.out.println
                   (n+" is not left truncatable prime");
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python3 Program to
# check whether a
# given number is left
# truncatable prime
# or not.

# Function to calculate
# x raised to the power y
def power(x, y) :

    if (y == 0) :
        return 1
    elif (y % 2 == 0) :
        return(power(x, y // 2) *
               power(x, y // 2))
    else :
        return(x * power(x, y // 2) *
                power(x, y // 2))

# Generate all prime
# numbers less than n.
def sieveOfEratosthenes(n, isPrime) :

    # Initialize all entries
    # of boolean array
    # as true. A value in
    # isPrime[i] will finally
    # be false if i is Not a
    # prime, else true
    # bool isPrime[n+1];
    isPrime[0] = isPrime[1] = False
    for i in range(2, n+1) :
        isPrime[i] = True

    p=2
    while(p * p <= n) :

        # If isPrime[p] is not
        # changed, then it is
        # a prime
        if (isPrime[p] == True) :

            # Update all multiples
            # of p
            i=p*2
            while(i <= n) :
                isPrime[i] = False
                i = i + p

        p = p + 1

# Returns true if n is
# right-truncatable,
# else false
def leftTruPrime(n) :
    temp = n
    cnt = 0

    # Counting number of
    # digits in the input
    # number and checking
    # whether it contains
    # 0 as digit or not.
    while (temp != 0) :

        # counting number
        # of digits.
        cnt=cnt + 1

        # checking whether
        # digit is 0 or not
        temp1 = temp % 10;
        if (temp1 == 0) :

            # if digit is 0,
            # return false.
            return False

        temp = temp // 10

    # Generating primes
    # using Sieve
    isPrime = [None] * (n + 1)
    sieveOfEratosthenes(n, isPrime)

    # Checking whether the
    # number remains prime
    # when the leading
    # ("left") digit is
    # successively removed
    for i in range(cnt, 0, -1) :

        # Checking number by
        # successively removing
        # leading ("left") digit.
        # n=113, cnt=3
        # i=3 mod=1000 n%mod=113
        # i=2 mod=100 n%mod=13
        # i=3 mod=10 n%mod=3
        mod = power(10, i)

        # checking prime
        if (isPrime[n % mod] != True) :

            # if not prime,
            # return false
            return False

    # if remains prime
    # , return true
    return True

# Driver program
n = 113

if (leftTruPrime(n)) :
    print(n, "is left truncatable prime")
else :
    print(n, "is not left truncatable prime")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// Program to check whether
// a given number is left
// truncatable prime or not.
using System;

class GFG {

    // Function to calculate x
    // raised to the power y
    static int power(int x, int y)
    {
        if (y == 0)
            return 1;
        else if (y%2 == 0)
            return power(x, y/2)
                   *power(x, y/2);
        else
            return x*power(x, y/2)
                   *power(x, y/2);
    }

    // Generate all prime
    // numbers less than n.
    static void sieveOfEratosthenes
                (int n, bool []isPrime)
    {
        // Initialize all entries of boolean
        // array as true. A value in isPrime[i]
        // will finally be false if i is Not
        // a prime, else true bool isPrime[n+1];
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
                for (int i = p * 2; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // Returns true if n is
    // right-truncatable, else false
    static bool leftTruPrime(int n)
    {
        int temp = n, cnt = 0, temp1;

        // Counting number of digits in the
        // input number and checking whether
        // it contains 0 as digit or not.
        while (temp != 0)
        {
            // counting number of digits.
            cnt++;

            temp1 = temp%10;

            // checking whether digit is
            // 0 or not
            if (temp1 == 0)
                return false;
            temp = temp/10;
        }

        // Generating primes using Sieve
        bool []isPrime = new bool[n+1];
        sieveOfEratosthenes(n, isPrime);

        // Checking whether the number
        // remains prime when the leading
        // ("left") digit is successively removed
        for (int i = cnt; i > 0; i--)
        {
            // Checking number by successively
            // removing leading ("left") digit.
            /* n=113, cnt=3
            i=3 mod=1000 n%mod=113
            i=2 mod=100 n%mod=13
            i=3 mod=10 n%mod=3 */
            int mod =  power(10, i);

            if (!isPrime[n%mod])
                return false;
        }

        // if remains prime, return true
        return true;
    }

    // Driver program
    public static void Main()
    {
        int n = 113;

        if (leftTruPrime(n))
            Console.WriteLine
                   (n + " is left truncatable prime");
        else
            Console.WriteLine
                   (n + " is not left truncatable prime");
    }
}

//This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check whether a
// given number is left-truncatable
// prime or not.

/* Function to calculate x raised to
the power y */
function power($x, $y)
{
    if ($y == 0)
        return 1;
    else if ($y % 2 == 0)
        return power($x, $y/2) *
                     power($x, $y/2);
    else
        return $x*power($x, $y/2) *
                     power($x, $y/2);
}

// Generate all prime numbers
// less than n.
function sieveOfEratosthenes($n, $l,
                            $isPrime)
{

    // Initialize all entries of
    // boolean array as true. A
    // value in isPrime[i] will
    // finally be false if i is
    // Not a prime, else true
    // bool isPrime[n+1];
    $isPrime[0] = $isPrime[1] = -1;
    for ($i = 2; $i <= $n; $i++)
        $isPrime[$i] = true;

    for ( $p = 2; $p * $p <= $n; $p++)
    {
        // If isPrime[p] is not
        // changed, then it is
        // a prime
        if ($isPrime[$p] == true)
        {
            // Update all multiples
            // of p
            for ($i = $p * 2; $i <= $n;
                              $i += $p)
                $isPrime[$i] = false;
        }
    }
}

// Returns true if n is
// right-truncatable, else false
function leftTruPrime($n)
{
    $temp = $n; $cnt = 0; $temp1;

    // Counting number of digits in
    // the input number and checking
    // whether it contains 0 as digit
    // or not.
    while ($temp)
    {

        // counting number of digits.
        $cnt++;

        // checking whether digit is
        // 0 or not
        $temp1 = $temp % 10;

        if ($temp1 == 0)

            // if digit is 0, return
            // false.
            return -1;
        $temp = $temp / 10;
    }

    // Generating primes using Sieve
    $isPrime[$n + 1];
    sieveOfEratosthenes($n, $isPrime);

    // Checking whether the number
    // remains prime when the leading
    // ("left") digit is successively
    // removed
    for ($i = $cnt; $i > 0; $i--)
    {
        // Checking number by
        // successively removing
        // leading ("left") digit.
        /* n=113, cnt=3
        i=3 mod=1000 n%mod=113
        i=2 mod=100 n%mod=13
        i=3 mod=10 n%mod=3 */
        $mod= power(10, $i);

        // checking prime
        if (!$isPrime[$n % $mod])

            // if not prime, return
            // false
            return -1;
    }

    // if remains prime, return true
    return true;
}

// Driver program

    $n = 113;

    if (leftTruPrime($n))
        echo $n, " is left truncatable",
                        " prime", "\n";
    else
        echo $n, " is not left ",
              "truncatable prime", "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to check whether
// a given number is left
// truncatable prime or not.

    function power(x, y)
    {
        if (y == 0)
            return 1;
        else if (y%2 == 0)
            return power(x, Math.floor(y/2))
                   *power(x, Math.floor(y/2));
        else
            return x*power(x, Math.floor(y/2))
                   *power(x, Math.floor(y/2));
    }

    // Generate all prime
    // numbers less than n.
    function sieveOfEratosthenes
                (n, isPrime)
    {

        // Initialize all entries of boolean
        // array as true. A value in isPrime[i]
        // will finally be false if i is Not
        // a prime, else true bool isPrime[n+1];
        isPrime[0] = isPrime[1] = false;
        for (let i = 2; i <= n; i++)
            isPrime[i] = true;

        for (let p = 2; p*p <= n; p++)
        {
            // If isPrime[p] is not changed,
            // then it is a prime
            if (isPrime[p] == true)
            {

                // Update all multiples of p
                for (let i = p*2; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // Returns true if n is
    // right-truncatable, else false
    function leftTruPrime(n)
    {
        let temp = n, cnt = 0, temp1;

        // Counting number of digits in the
        // input number and checking whether
        // it contains 0 as digit or not.
        while (temp != 0)
        {
            // counting number of digits.
            cnt++;

            temp1 = temp%10;

            // checking whether digit is
            // 0 or not
            if (temp1 == 0)
                return false;
            temp = Math.floor(temp/10);
        }

        // Generating primes using Sieve
        let isPrime = Array.from({length: n+1}, (_, i) => 0);
        sieveOfEratosthenes(n, isPrime);

        // Checking whether the number
        // remains prime when the leading
        // ("left") digit is successively removed
        for (let i = cnt; i > 0; i--)
        {
            // Checking number by successively
            // removing leading ("left") digit.
            /* n=113, cnt=3
            i=3 mod=1000 n%mod=113
            i=2 mod=100 n%mod=13
            i=3 mod=10 n%mod=3 */
            let mod =  power(10,i);

            if (!isPrime[n%mod])
                return false;
        }

        // if remains prime, return true
        return true;
    }

// Driver Code

    let n = 113;

        if (leftTruPrime(n))
            document.write
                   (n+" is left truncatable prime");
        else
             document.write
                   (n+" is not left truncatable prime");

// This code is contributed by sanjoy_62.
</script>
```

输出:

```
113 is left truncatable prime
```

**最坏情况复杂度:** O(N*N)
**相关文章:**
[右可截断素数](https://www.geeksforgeeks.org/right-truncatable-prime/)
**参考文献:**[https://en.wikipedia.org/wiki/Truncatable_prime](https://en.wikipedia.org/wiki/Truncatable_prime)
本文由 **Rahul Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。