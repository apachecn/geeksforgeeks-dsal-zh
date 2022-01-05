# 给定数的第 k 个质因数

> 原文:[https://www . geesforgeks . org/k-th-质因数-给定数/](https://www.geeksforgeeks.org/k-th-prime-factor-given-number/)

给定两个数字 n 和 k，打印 n 的所有质因数中的第 k 个质因数，例如，如果输入数字是 15，k 是 2，那么输出应该是“5”。如果 k 是 3，那么输出应该是“-1”(质因数少于 k)。
**例** :

```
Input : n = 225, k = 2        
Output : 3
Prime factors are 3 3 5 5\. Second
prime factor is 3.

Input : n = 81, k = 5
Output : -1
Prime factors are 3 3 3 3
```

一个**简单的解决方法**是先找到 n 的素因子，在找到素因子的同时，记录计数。如果计数变成 k，我们返回当前质因数。

## C++

```
// Program to print kth prime factor
# include<bits/stdc++.h>
using namespace std;

// A function to generate prime factors of a
// given number n and return k-th prime factor
int kPrimeFactor(int n, int k)
{
    // Find the number of 2's that divide k
    while (n%2 == 0)
    {
        k--;
        n = n/2;
        if (k == 0)
         return 2;
    }

    // n must be odd at this point.  So we can skip
    // one element (Note i = i +2)
    for (int i = 3; i <= sqrt(n); i = i+2)
    {
        // While i divides n, store i and divide n
        while (n%i == 0)
        {
            if (k == 1)
              return i;

            k--;
            n = n/i;
        }
    }

    // This condition is to handle the case where
    // n is a prime number greater than 2
    if (n > 2 && k == 1)
        return n;

    return -1;
}

// Driver Program
int main()
{
    int n = 12, k = 3;
    cout << kPrimeFactor(n, k) << endl;
    n = 14, k = 3;
    cout << kPrimeFactor(n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Program to print kth prime factor
import java.io.*;
import java.math.*;

class GFG{

    // A function to generate prime factors
    // of a given number n and return k-th
    // prime factor
    static int kPrimeFactor(int n, int k)
    {
        // Find the number of 2's that
        // divide k
        while (n % 2 == 0)
        {
            k--;
            n = n / 2;
            if (k == 0)
             return 2;
        }

        // n must be odd at this point.
        // So we can skip one element
        // (Note i = i +2)
        for (int i = 3; i <= Math.sqrt(n); i = i + 2)
        {
            // While i divides n, store i
            // and divide n
            while (n % i == 0)
            {
                if (k == 1)
                  return i;

                k--;
                n = n / i;
            }
        }

        // This condition is to handle the
        // case where n is a prime number
        // greater than 2
        if (n > 2 && k == 1)
            return n;

        return -1;
    }

    // Driver Program
    public static void main(String args[])
    {
        int n = 12, k = 3;
        System.out.println(kPrimeFactor(n, k));
        n = 14; k = 3;
        System.out.println(kPrimeFactor(n, k));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 计算机编程语言

```
# Python Program to print kth prime factor
import math

# A function to generate prime factors of a
# given number n and return k-th prime factor
def kPrimeFactor(n,k) :

    # Find the number of 2's that divide k
    while (n % 2 == 0) :
        k = k - 1
        n = n / 2
        if (k == 0) :
            return 2

    # n must be odd at this point. So we can
    # skip one element (Note i = i +2)
    i = 3
    while i <= math.sqrt(n) :

        # While i divides n, store i and divide n
        while (n % i == 0) :
            if (k == 1) :
                return i

            k = k - 1
            n = n / i

        i = i + 2

    # This condition is to handle the case
    # where n is a prime number greater than 2
    if (n > 2 and k == 1) :
        return n

    return -1

# Driver Program
n = 12
k = 3
print(kPrimeFactor(n, k))

n = 14
k = 3
print(kPrimeFactor(n, k))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Program to print kth prime factor.
using System;

class GFG {

    // A function to generate prime factors
    // of a given number n and return k-th
    // prime factor
    static int kPrimeFactor(int n, int k)
    {

        // Find the number of 2's that
        // divide k
        while (n % 2 == 0)
        {
            k--;
            n = n / 2;

            if (k == 0)
                return 2;
        }

        // n must be odd at this point.
        // So we can skip one element
        // (Note i = i +2)
        for (int i = 3; i <= Math.Sqrt(n);
                                i = i + 2)
        {

            // While i divides n, store i
            // and divide n
            while (n % i == 0)
            {
                if (k == 1)
                    return i;

                k--;
                n = n / i;
            }
        }

        // This condition is to handle the
        // case where n is a prime number
        // greater than 2
        if (n > 2 && k == 1)
            return n;

        return -1;
    }

    // Driver Program
    public static void Main()
    {

        int n = 12, k = 3;
        Console.WriteLine(kPrimeFactor(n, k));

        n = 14; k = 3;
        Console.WriteLine(kPrimeFactor(n, k));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print kth prime factor

// A function to generate prime
// factors of a  given number n
// and return k-th prime factor
function kPrimeFactor($n, $k)
{

    // Find the number of 2's
    // that divide k
    while ($n%2 == 0)
    {
        $k--;
        $n = $n/2;
        if ($k == 0)
        return 2;
    }

    // n must be odd at this point.
    // So we can skip one element
    // (Note i = i +2)
    for($i = 3; $i <= sqrt($n); $i = $i+2)
    {

        // While i divides n,
        // store i and divide n
        while ($n % $i == 0)
        {
            if ($k == 1)
            return $i;

            $k--;
            $n = $n / $i;
        }
    }

    // This condition is to
    // handle the case where
    // n is a prime number
    // greater than 2
    if ($n > 2 && $k == 1)
        return $n;

    return -1;
}

// Driver Code
{
    $n = 12;
    $k = 3;
    echo kPrimeFactor($n, $k),"\n" ;
    $n = 14;
    $k = 3;
    echo kPrimeFactor($n, $k) ;
    return 0;
}

// This code contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript Program to print kth prime factor

    // A function to generate prime factors
    // of a given number n and return k-th
    // prime factor
    function kPrimeFactor(n, k)
    {

        // Find the number of 2's that
        // divide k
        while (n % 2 == 0)
        {
            k--;
            n = n / 2;
            if (k == 0)
             return 2;
        }

        // n must be odd at this point.
        // So we can skip one element
        // (Note i = i +2)
        for (let i = 3; i <= Math.sqrt(n); i = i + 2)
        {

            // While i divides n, store i
            // and divide n
            while (n % i == 0)
            {
                if (k == 1)
                  return i;

                k--;
                n = n / i;
            }
        }

        // This condition is to handle the
        // case where n is a prime number
        // greater than 2
        if (n > 2 && k == 1)
            return n;

        return -1;
    }

// Driver code   

    let n = 12, k = 3;
    document.write(kPrimeFactor(n, k) + "<br/>");
    n = 14; k = 3;
    document.write(kPrimeFactor(n, k));

// This code is contributed by susmitakundugoaldanga.

</script>
```

**输出:**

```
3
-1
```

一个**有效的解决方案**是使用厄拉多塞的[筛子。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)注意，当我们需要多个测试用例的第 k 个质因数时，这个解决方案是有效的。对于单个案例，以前的方法更好。
思路是做预处理，在给定范围内存储所有数字的[最小质因数。一旦我们在一个数组中存储了最少的素因子，我们就可以通过重复地用最少的素因子除 n 来找到第 k 个素因子，同时它是可分的，然后对减少的 n 重复这个过程](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/) 

## C++

```
// C++ program to find k-th prime factor using Sieve Of
// Eratosthenes. This program is efficient when we have
// a range of numbers.
#include<bits/stdc++.h>

using namespace std;
const int MAX = 10001;

// Using SieveOfEratosthenes to find smallest prime
// factor of all the numbers.
// For example, if MAX is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
void sieveOfEratosthenes(int s[])
{
    // Create a boolean array "prime[0..MAX]" and
    // initialize all entries in it as false.
    vector <bool> prime(MAX+1, false);

    // Initializing smallest factor equal to 2
    // for all the even numbers
    for (int i=2; i<=MAX; i+=2)
        s[i] = 2;

    // For odd numbers less then equal to n
    for (int i=3; i<=MAX; i+=2)
    {
        if (prime[i] == false)
        {
            // s(i) for a prime is the number itself
            s[i] = i;

            // For all multiples of current prime number
            for (int j=i; j*i<=MAX; j+=2)
            {
                if (prime[i*j] == false)
                {
                    prime[i*j] = true;

                    // i is the smallest prime factor for
                    // number "i*j".
                    s[i*j] = i;
                }
            }
        }
    }
}

// Function to generate prime factors and return its
// k-th prime factor. s[i] stores least prime factor
// of i.
int kPrimeFactor(int n, int k, int s[])
{
    // Keep dividing n by least prime factor while
    // either n is not 1 or count of prime factors
    // is not k.
    while (n > 1)
    {
        if (k == 1)
          return s[n];

        // To keep track of count of prime factors
        k--;

        // Divide n to find next prime factor
        n /= s[n];
    }

    return -1;
}

// Driver Program
int main()
{
    // s[i] is going to store prime factor
    // of i.
    int s[MAX+1];
    memset(s, -1, sizeof(s));
    sieveOfEratosthenes(s);

    int n = 12, k = 3;
    cout << kPrimeFactor(n, k, s) << endl;
    n = 14, k = 3;
    cout << kPrimeFactor(n, k, s) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find k-th prime factor
// using Sieve Of Eratosthenes. This
// program is efficient when we have
// a range of numbers.
class GFG
{
static int MAX = 10001;

// Using SieveOfEratosthenes to find smallest prime
// factor of all the numbers.
// For example, if MAX is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
static void sieveOfEratosthenes(int []s)
{

    // Create a boolean array "prime[0..MAX]" and
    // initialize all entries in it as false.
    boolean[] prime=new boolean[MAX+1];

    // Initializing smallest factor equal to 2
    // for all the even numbers
    for (int i = 2; i <= MAX; i += 2)
        s[i] = 2;

    // For odd numbers less then equal to n
    for (int i = 3; i <= MAX; i += 2)
    {
        if (prime[i] == false)
        {
            // s(i) for a prime is the number itself
            s[i] = i;

            // For all multiples of current prime number
            for (int j = i; j * i <= MAX; j += 2)
            {
                if (prime[i * j] == false)
                {
                    prime[i * j] = true;

                    // i is the smallest prime factor for
                    // number "i*j".
                    s[i * j] = i;
                }
            }
        }
    }
}

// Function to generate prime factors
// and return its k-th prime factor.
// s[i] stores least prime factor of i.
static int kPrimeFactor(int n, int k, int []s)
{
    // Keep dividing n by least
    // prime factor while either
    // n is not 1 or count of
    // prime factors is not k.
    while (n > 1)
    {
        if (k == 1)
        return s[n];

        // To keep track of count of prime factors
        k--;

        // Divide n to find next prime factor
        n /= s[n];
    }
    return -1;
}

// Driver code
public static void main (String[] args)
{

    // s[i] is going to store prime factor
    // of i.
    int[] s = new int[MAX + 1];
    sieveOfEratosthenes(s);

    int n = 12, k = 3;
    System.out.println(kPrimeFactor(n, k, s));
    n = 14;
    k = 3;
    System.out.println(kPrimeFactor(n, k, s));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# python3 program to find k-th prime factor using Sieve Of
# Eratosthenes. This program is efficient when we have
# a range of numbers.

MAX = 10001

# Using SieveOfEratosthenes to find smallest prime
# factor of all the numbers.
# For example, if MAX is 10,
# s[2] = s[4] = s[6] = s[10] = 2
# s[3] = s[9] = 3
# s[5] = 5
# s[7] = 7
def sieveOfEratosthenes(s):

# Create a boolean array "prime[0..MAX]" and
# initialize all entries in it as false.
    prime=[False for i in range(MAX+1)]

    # Initializing smallest factor equal to 2
    # for all the even numbers
    for i in range(2,MAX+1,2):
        s[i] = 2;

    # For odd numbers less then equal to n
    for i in range(3,MAX,2):
        if (prime[i] == False):
        # s(i) for a prime is the number itself
            s[i] = i

        # For all multiples of current prime number
            for j in range(i,MAX+1,2):
                if j*j> MAX:
                    break
                if (prime[i*j] == False):
                    prime[i*j] = True

                    # i is the smallest prime factor for
                    # number "i*j".
                    s[i*j] = i

# Function to generate prime factors and return its
# k-th prime factor. s[i] stores least prime factor
# of i.
def kPrimeFactor(n, k, s):
    # Keep dividing n by least prime factor while
    # either n is not 1 or count of prime factors
    # is not k.
    while (n > 1):

        if (k == 1):
            return s[n]

        # To keep track of count of prime factors
        k-=1

        # Divide n to find next prime factor
        n //= s[n]

    return -1

# Driver Program

# s[i] is going to store prime factor
# of i.
s=[-1 for i in range(MAX+1)]

sieveOfEratosthenes(s)

n = 12
k = 3
print(kPrimeFactor(n, k, s))

n = 14
k = 3
print(kPrimeFactor(n, k, s))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find k-th prime factor
// using Sieve Of Eratosthenes. This
// program is efficient when we have
// a range of numbers and we
using System;
class GFG
{
static int MAX = 10001;

// Using SieveOfEratosthenes to find
// smallest prime factor of all the
// numbers. For example, if MAX is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
static void sieveOfEratosthenes(int []s)
{
    // Create a boolean array "prime[0..MAX]"
    // and initialize all entries in it as false.
    bool[] prime = new bool[MAX + 1];

    // Initializing smallest factor equal
    // to 2 for all the even numbers
    for (int i = 2; i <= MAX; i += 2)
        s[i] = 2;

    // For odd numbers less then equal to n
    for (int i = 3; i <= MAX; i += 2)
    {
        if (prime[i] == false)
        {
            // s(i) for a prime is the
            // number itself
            s[i] = i;

            // For all multiples of current
            // prime number
            for (int j = i; j * i <= MAX; j += 2)
            {
                if (prime[i * j] == false)
                {
                    prime[i * j] = true;

                    // i is the smallest prime factor
                    // for number "i*j".
                    s[i * j] = i;
                }
            }
        }
    }
}

// Function to generate prime factors
// and return its k-th prime factor.
// s[i] stores least prime factor of i.
static int kPrimeFactor(int n, int k, int []s)
{
    // Keep dividing n by least prime
    // factor while either n is not 1
    // or count of prime factors is not k.
    while (n > 1)
    {
        if (k == 1)
        return s[n];

        // To keep track of count of
        // prime factors
        k--;

        // Divide n to find next prime factor
        n /= s[n];
    }

    return -1;
}

// Driver Code
static void Main()
{
    // s[i] is going to store prime 
    // factor of i.
    int[] s = new int[MAX + 1];
    sieveOfEratosthenes(s);

    int n = 12, k = 3;
    Console.WriteLine(kPrimeFactor(n, k, s));
    n = 14;
    k = 3;
    Console.WriteLine(kPrimeFactor(n, k, s));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find k-th prime factor
// using Sieve Of Eratosthenes. This program
// is efficient when we have a range of numbers.

$MAX = 10001;

// Using SieveOfEratosthenes to find
// smallest prime factor of all the numbers.
// For example, if MAX is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
function sieveOfEratosthenes(&$s)
{
    global $MAX;

    // Create a boolean array "prime[0..MAX]"
    // and initialize all entries in it as false.
    $prime = array_fill(0, $MAX + 1, false);

    // Initializing smallest factor equal
    // to 2 for all the even numbers
    for ($i = 2; $i <= $MAX; $i += 2)
        $s[$i] = 2;

    // For odd numbers less then equal to n
    for ($i = 3; $i <= $MAX; $i += 2)
    {
        if ($prime[$i] == false)
        {
            // s(i) for a prime is the
            // number itself
            $s[$i] = $i;

            // For all multiples of current
            // prime number
            for ($j = $i; $j * $i <= $MAX; $j += 2)
            {
                if ($prime[$i * $j] == false)
                {
                    $prime[$i * $j] = true;

                    // i is the smallest prime
                    // factor for number "i*j".
                    $s[$i * $j] = $i;
                }
            }
        }
    }
}

// Function to generate prime factors and
// return its k-th prime factor. s[i] stores
// least prime factor of i.
function kPrimeFactor($n, $k, $s)
{
    // Keep dividing n by least prime
    // factor while either n is not 1
    // or count of prime factors is not k.
    while ($n > 1)
    {
        if ($k == 1)
        return $s[$n];

        // To keep track of count of
        // prime factors
        $k--;

        // Divide n to find next prime factor
        $n = (int)($n / $s[$n]);
    }

    return -1;
}

// Driver Code

// s[i] is going to store prime
// factor of i.
$s = array_fill(0, $MAX + 1, -1);
sieveOfEratosthenes($s);

$n = 12;
$k = 3;
print(kPrimeFactor($n, $k, $s) . "\n");

$n = 14;
$k = 3;
print(kPrimeFactor($n, $k, $s));

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript program to find k-th prime factor
// using Sieve Of Eratosthenes. This
// program is efficient when we have
// a range of numbers.

var MAX = 10001;

// Using SieveOfEratosthenes to find smallest prime
// factor of all the numbers.
// For example, if MAX is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
function sieveOfEratosthenes(s)
{

    // Create a boolean array "prime[0..MAX]" and
    // initialize all entries in it as false.
    prime=Array.from({length: MAX+1}, (_, i) => false);

    // Initializing smallest factor equal to 2
    // for all the even numbers
    for (i = 2; i <= MAX; i += 2)
        s[i] = 2;

    // For odd numbers less then equal to n
    for (i = 3; i <= MAX; i += 2)
    {
        if (prime[i] == false)
        {
            // s(i) for a prime is the number itself
            s[i] = i;

            // For all multiples of current prime number
            for (j = i; j * i <= MAX; j += 2)
            {
                if (prime[i * j] == false)
                {
                    prime[i * j] = true;

                    // i is the smallest prime factor for
                    // number "i*j".
                    s[i * j] = i;
                }
            }
        }
    }
}

// Function to generate prime factors
// and return its k-th prime factor.
// s[i] stores least prime factor of i.
function kPrimeFactor(n , k , s)
{
    // Keep dividing n by least
    // prime factor while either
    // n is not 1 or count of
    // prime factors is not k.
    while (n > 1)
    {
        if (k == 1)
        return s[n];

        // To keep track of count of prime factors
        k--;

        // Divide n to find next prime factor
        n /= s[n];
    }
    return -1;
}

// Driver code

// s[i] is going to store prime factor
// of i.
var s = Array.from({length: MAX + 1}, (_, i) => 0);
sieveOfEratosthenes(s);

var n = 12, k = 3;
document.write(kPrimeFactor(n, k, s)+"<br>");
n = 14;
k = 3;
document.write(kPrimeFactor(n, k, s));

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
3
-1
```

本文由**阿夫扎尔·安萨里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。