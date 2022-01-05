# 直到 n 的最小素数因子

> 原文:[https://www . geeksforgeeks . org/最小质数因子-till-n/](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/)

给定一个数 **n** ，打印从 1 到 n 的所有数的**最小质因数**，整数 n 的最小质因数是除以该数的最小质数。所有偶数的最小质因数是 2。质数是它自己的最小质因数(也是它自己的最大质因数)。
**注:**我们需要打印 1 换 1。
**示例:**

```
Input : 6
Output : Least Prime factor of 1: 1
         Least Prime factor of 2: 2
         Least Prime factor of 3: 3
         Least Prime factor of 4: 2
         Least Prime factor of 5: 5
         Least Prime factor of 6: 2
```

我们可以使用厄拉多塞的变异[筛来解决上述问题。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

1.  创建从 2 到 n 的连续整数列表:(2，3，4，…，n)。
2.  首先，让 I 等于 2，最小的素数。
3.  以 I 为增量从 2i 数到 n 来枚举 I 的倍数，并将它们标记为具有最小质因数 I(如果尚未标记)。也将 I 标记为 I 的最小质因数(I 本身是一个质数)。
4.  在列表中找到第一个比我大的没有标记的数字。如果没有这样的数字，停止。否则，让我现在等于这个新数(它是下一个素数)，并从步骤 3 开始重复。

下面是算法的实现，其中最小素[]保存对应于相应索引的最小素因子的值。

## C++

```
// C++ program to print the least prime factors
// of numbers less than or equal to
// n using modified Sieve of Eratosthenes
#include<bits/stdc++.h>
using namespace std;

void leastPrimeFactor(int n)
{
    // Create a vector to store least primes.
    // Initialize all entries as 0.
    vector<int> least_prime(n+1, 0);

    // We need to print 1 for 1.
    least_prime[1] = 1;

    for (int i = 2; i <= n; i++)
    {
        // least_prime[i] == 0
        // means it i is prime
        if (least_prime[i] == 0)
        {
            // marking the prime number
            // as its own lpf
            least_prime[i] = i;

            // mark it as a divisor for all its
            // multiples if not already marked
            for (int j = i*i; j <= n; j += i)
                if (least_prime[j] == 0)
                   least_prime[j] = i;
        }
    }

    // print least prime factor of
    // of numbers till n
    for (int i = 1; i <= n; i++)
        cout << "Least Prime factor of "
             << i << ": " << least_prime[i] << "\n";
}

// Driver program to test above function
int main()
{
    int n = 10;
    leastPrimeFactor(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the least prime factors
// of numbers less than or equal to
// n using modified Sieve of Eratosthenes

import java.io.*;
import java.util.*;

class GFG
{
    public static void leastPrimeFactor(int n)
    {

        // Create a vector to store least primes.
        // Initialize all entries as 0.
        int[] least_prime = new int[n+1];

        // We need to print 1 for 1.
        least_prime[1] = 1;

        for (int i = 2; i <= n; i++)
        {

            // least_prime[i] == 0
            // means it i is prime
            if (least_prime[i] == 0)
            {

                // marking the prime number
                // as its own lpf
                least_prime[i] = i;

                // mark it as a divisor for all its
                // multiples if not already marked
                for (int j = i*i; j <= n; j += i)
                    if (least_prime[j] == 0)
                        least_prime[j] = i;
            }
        }

        // print least prime factor of
        // of numbers till n
        for (int i = 1; i <= n; i++)
            System.out.println("Least Prime factor of " +
                               + i + ": " + least_prime[i]);
    }
    public static void main (String[] args)
    {
        int n = 10;
        leastPrimeFactor(n);
    }
}

// Code Contributed by Mohit Gupta_OMG <(0_o)>
```

## 蟒蛇 3

```
# Python 3 program to print the
# least prime factors of numbers
# less than or equal to n using
# modified Sieve of Eratosthenes

def leastPrimeFactor(n) :

    # Create a vector to store least primes.
    # Initialize all entries as 0.
    least_prime = [0] * (n + 1)

    # We need to print 1 for 1.
    least_prime[1] = 1

    for i in range(2, n + 1) :

        # least_prime[i] == 0
        # means it i is prime
        if (least_prime[i] == 0) :

            # marking the prime number
            # as its own lpf
            least_prime[i] = i

            # mark it as a divisor for all its
            # multiples if not already marked
            for j in range(i * i, n + 1, i) :
                if (least_prime[j] == 0) :
                    least_prime[j] = i

    # print least prime factor
    # of numbers till n
    for i in range(1, n + 1) :
        print("Least Prime factor of "
              ,i , ": " , least_prime[i] )

# Driver program

n = 10
leastPrimeFactor(n)

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to print the least prime factors
// of numbers less than or equal to
// n using modified Sieve of Eratosthenes
using System;

class GFG
{
    public static void leastPrimeFactor(int n)
    {
        // Create a vector to store least primes.
        // Initialize all entries as 0.
        int []least_prime = new int[n+1];

        // We need to print 1 for 1.
        least_prime[1] = 1;

        for (int i = 2; i <= n; i++)
        {
            // least_prime[i] == 0
            // means it i is prime
            if (least_prime[i] == 0)
            {
                // marking the prime number
                // as its own lpf
                least_prime[i] = i;

                // mark it as a divisor for all its
                // multiples if not already marked
                for (int j = i*i; j <= n; j += i)
                    if (least_prime[j] == 0)
                        least_prime[j] = i;
            }
        }

        // print least prime factor of
        // of numbers till n
        for (int i = 1; i <= n; i++)
            Console.WriteLine("Least Prime factor of " +
                               i + ": " + least_prime[i]);
    }

    // Driver code
    public static void Main ()
    {
        int n = 10;

        // Function calling
        leastPrimeFactor(n);
    }
}

// This code is contributed by Nitin Mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the
// least prime factors of
// numbers less than or equal
// to n using modified Sieve
// of Eratosthenes

function leastPrimeFactor($n)
{
    // Create a vector to
    // store least primes.
    // Initialize all entries
    // as 0.
    $least_prime = array($n + 1);

    for ($i = 0;
         $i <= $n; $i++)
    $least_prime[$i] = 0;

    // We need to
    // print 1 for 1.
    $least_prime[1] = 1;

    for ($i = 2; $i <= $n; $i++)
    {
        // least_prime[i] == 0
        // means it i is prime
        if ($least_prime[$i] == 0)
        {
            // marking the prime
            // number as its own lpf
            $least_prime[$i] = $i;

            // mark it as a divisor
            // for all its multiples
            // if not already marked
            for ($j = $i * $i;
                 $j <= $n; $j += $i)
                if ($least_prime[$j] == 0)
                $least_prime[$j] = $i;
        }
    }

    // print least prime
    // factor of numbers
    // till n
    for ($i = 1; $i <= $n; $i++)
        echo "Least Prime factor of " .
                            $i . ": " .
               $least_prime[$i] . "\n";
}

// Driver Code
$n = 10;
leastPrimeFactor($n);

// This code is contributed
// by Sam007
?>
```

## java 描述语言

```
<script>
// javascript program to print the least prime factors
// of numbers less than or equal to
// n using modified Sieve of Eratosthenes
function leastPrimeFactor( n)
{

    // Create a vector to store least primes.
    // Initialize all entries as 0.
    let least_prime = Array(n+1).fill(0);

    // We need to print 1 for 1.
    least_prime[1] = 1;

    for (let i = 2; i <= n; i++)
    {

        // least_prime[i] == 0
        // means it i is prime
        if (least_prime[i] == 0)
        {

            // marking the prime number
            // as its own lpf
            least_prime[i] = i;

            // mark it as a divisor for all its
            // multiples if not already marked
            for (let j = i*i; j <= n; j += i)
                if (least_prime[j] == 0)
                   least_prime[j] = i;
        }
    }

    // print least prime factor of
    // of numbers till n
    for (let i = 1; i <= n; i++)
       document.write( "Least Prime factor of "
             + i + ": " + least_prime[i] + "<br/>");
}

// Driver program to test above function
    let n = 10;
    leastPrimeFactor(n);

// This code is contributed by Rajput-Ji

</script>
```

**Output**

```
Least Prime factor of 1: 1
Least Prime factor of 2: 2
Least Prime factor of 3: 3
Least Prime factor of 4: 2
Least Prime factor of 5: 5
Least Prime factor of 6: 2
Least Prime factor of 7: 7
Least Prime factor of 8: 2
Least Prime factor of 9: 3
Least Prime factor of 10: 2
```

**时间复杂度:**O(nloglog(n))
T3】辅助空间:O(n)
T6】参考文献:
1。[https://www.geeksforgeeks.org/sieve-of-eratosthenes/](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
2。[https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)
3。[https://oeis.org/wiki/Least_prime_factor_of_n](https://oeis.org/wiki/Least_prime_factor_of_n)
**练习:**
我们能不能把这个算法推广一下，或者用最少 _ 质数[]来找到数字直到 n 的所有质数因子？
本文由 [**阿育什·坎德里**](https://in.linkedin.com/in/ayush-khanduri-b4ab87106) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。