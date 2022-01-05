# 检查一个数是否可以写成‘k’个质数的和

> 原文:[https://www . geesforgeks . org/check-number-can-writed-sum-k-prime-numbers/](https://www.geeksforgeeks.org/check-number-can-written-sum-k-prime-numbers/)

给定两个数 N 和 K，我们需要找出‘N’是否可以写成‘K’素数之和。
给定 N < = 10^9

**示例:**

```
Input  : N = 10 K = 2
Output : Yes 
        10 can be written as 5 + 5

Input  : N = 2 K = 2
Output : No
```

想法是用[哥德巴赫猜想](https://www.geeksforgeeks.org/program-for-goldbachs-conjecture-two-primes-with-given-sum/)说每一个偶数(大于 2)都可以表示为两个素数之和。
**如果 N > = 2K 且 K = 1:** 如果 N 是素数
**则答案为是如果 N > = 2K 且 K = 2:** 如果 N 是偶数则答案为是(哥德巴赫猜想)如果 N 是奇数则答案为否如果 N-2 不是素数则答案为是。这是因为我们知道奇数+奇数=偶数，偶数+奇数=奇数。所以当 N 是奇数，K = 2 时，一个数必须是 2，因为它是唯一的偶数素数，所以现在答案取决于 N-2 是否是奇数。
**如果 N > = 2K，K > = 3:** 答案始终为是。当 N 为偶数时 N–2 *(K-2)也为偶数，所以 N–2 *(K–2)可以写成两个素数之和(哥德巴赫猜想)p，q，N 可以写成 2，2 …..K–2 倍，p，q .当 N 为奇数时，N–3-2 *(K–3)为偶数，因此可以写成两个素数的和 p，q 和 N 可以写成 2，2 …..K-3 次，3，p，q

## C++

```
// C++ implementation to check if N can be
// written as sum of k primes
#include<bits/stdc++.h>
using namespace std;

// Checking if a number is prime or not
bool isprime(int x)
{

    // check for numbers from 2 to sqrt(x)
    // if it is divisible return false
    for (int i = 2; i * i <= x; i++)
        if (x % i == 0)
            return false;
    return true;
}

// Returns true if N can be written as sum
// of K primes
bool isSumOfKprimes(int N, int K)
{
    // N < 2K directly return false
    if (N < 2*K)
        return false;

    // If K = 1 return value depends on primality of N
    if (K == 1)
        return isprime(N);

    if (K == 2)
    {
        // if N is even directly return true;
        if (N % 2 == 0)
            return true;

        // If N is odd, then one prime must
        // be 2\. All other primes are odd
        // and cannot have a pair sum as even.
        return isprime(N - 2);
    }

    // If K >= 3 return true;
    return true;
}

// Driver function
int main()
{
    int n = 10, k = 2;
    if (isSumOfKprimes (n, k))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if N can be
// written as sum of k primes
public class Prime
{
    // Checking if a number is prime or not
    static boolean isprime(int x)
    {
        // check for numbers from 2 to sqrt(x)
        // if it is divisible return false
        for (int i=2; i*i<=x; i++)
            if (x%i == 0)

                return false;
        return true;
    }

    // Returns true if N can be written as sum
    // of K primes
    static boolean isSumOfKprimes(int N, int K)
    {
        // N < 2K directly return false
        if (N < 2*K)
            return false;

        // If K = 1 return value depends on primality of N
        if (K == 1)
            return isprime(N);

        if (K == 2)
        {
            // if N is even directly return true;
            if (N%2 == 0)
                return true;

            // If N is odd, then one prime must
            // be 2\. All other primes are odd
            // and cannot have a pair sum as even.
            return isprime(N - 2);
        }

        // If K >= 3 return true;
        return true;
    }

    public static void main (String[] args)
    {
        int n = 10, k = 2;
        if (isSumOfKprimes (n, k))
            System.out.print("Yes");
        else
            System.out.print("No");
    }
}
// Contributed by Saket Kumar
```

## 蟒蛇 3

```
# Python implementation to check
# if N can be written as sum of
# k primes

# Checking if a number is prime
# or not

def isprime(x):

    # check for numbers from 2
    # to sqrt(x) if it is divisible
    # return false
    i = 2
    while(i * i <= x):
        if (x % i == 0):
            return 0
        i += 1
    return 1

# Returns true if N can be written
# as sum of K primes

def isSumOfKprimes(N, K):

    # N < 2K directly return false
    if (N < 2 * K):
        return 0

    # If K = 1 return value depends
    # on primality of N
    if (K == 1):
        return isprime(N)

    if (K == 2):

        # if N is even directly
        # return true;
        if (N % 2 == 0):
            return 1

        # If N is odd, then one
        # prime must be 2\. All
        # other primes are odd
        # and cannot have a pair
        # sum as even.
        return isprime(N - 2)

    # If K >= 3 return true;
    return 1

# Driver function
n = 15
k = 2
if (isSumOfKprimes(n, k)):
    print("Yes")
else:
    print("No")

# This code is Contributed by Sam007.
```

## C#

```
// C# implementation to check if N can be
// written as sum of k primes
using System;

class GFG {

    // Checking if a number is prime or not
    static bool isprime(int x)
    {
        // check for numbers from 2 to sqrt(x)
        // if it is divisible return false
        for (int i = 2; i * i <= x; i++)
            if (x % i == 0)

                return false;
        return true;
    }

    // Returns true if N can be written as sum
    // of K primes
    static bool isSumOfKprimes(int N, int K)
    {
        // N < 2K directly return false
        if (N < 2 * K)
            return false;

        // If K = 1 return value depends on primality of N
        if (K == 1)
            return isprime(N);

        if (K == 2)
        {
            // if N is even directly return true;
            if (N % 2 == 0)
                return true;

            // If N is odd, then one prime must
            // be 2\. All other primes are odd
            // and cannot have a pair sum as even.
            return isprime(N - 2);
        }

        // If K >= 3 return true;
        return true;
    }

    // Driver function
    public static void Main ()
    {
        int n = 10, k = 2;
        if (isSumOfKprimes (n, k))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// if N can be written as sum
// of k primes

// Checking if a number
// is prime or not
function isprime($x)
{
    // check for numbers from 2
    // to sqrt(x) if it is
    // divisible return false
    for ($i = 2; $i * $i <= $x; $i++)
        if ($x % $i == 0)
            return false;
    return true;
}

// Returns true if N can be
// written as sum of K primes
function isSumOfKprimes($N, $K)
{
    // N < 2K directly return false
    if ($N < 2 * $K)
        return false;

    // If K = 1 return value
    // depends on primality of N
    if ($K == 1)
        return isprime($N);

    if ($K == 2)
    {
        // if N is even directly
        // return true;
        if ($N % 2 == 0)
            return true;

        // If N is odd, then one prime
        // must be 2\. All other primes
        // are odd and cannot have a
        // pair sum as even.
        return isprime($N - 2);
    }

    // If K >= 3 return true;
    return true;
}

// Driver Code
$n = 10; $k = 2;
if (isSumOfKprimes ($n, $k))
    echo "Yes";
else
    echo"No" ;

// This code is contributed by vt
?>
```

## java 描述语言

```
<script>
// javascript implementation to check if N can be
// written as sum of k primes

    // Checking if a number is prime or not
    function isprime(x)
    {

        // check for numbers from 2 to sqrt(x)
        // if it is divisible return false
        for (i = 2; i * i <= x; i++)
            if (x % i == 0)

                return false;
        return true;
    }

    // Returns true if N can be written as sum
    // of K primes
    function isSumOfKprimes(N, K)
    {

        // N < 2K directly return false
        if (N < 2 * K)
            return false;

        // If K = 1 return value depends on primality of N
        if (K == 1)
            return isprime(N);

        if (K == 2)
        {

            // if N is even directly return true;
            if (N % 2 == 0)
                return true;

            // If N is odd, then one prime must
            // be 2\. All other primes are odd
            // and cannot have a pair sum as even.
            return isprime(N - 2);
        }

        // If K >= 3 return true;
        return true;
    }

    // Driver code
        var n = 10, k = 2;
        if (isSumOfKprimes(n, k))
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by gauravrajput1
</script>
```

**输出:**

```
Yes
```

本文由 **Ayush Jha** 投稿，如果你喜欢 GeeksforGeeks 并且愿意投稿，也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。