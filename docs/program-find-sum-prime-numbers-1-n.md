# 计算 1 到 n 之间素数之和的程序

> 原文:[https://www . geesforgeks . org/program-find-sum-prime-numbers-1-n/](https://www.geeksforgeeks.org/program-find-sum-prime-numbers-1-n/)

写一个程序，找出 1 到 n 之间所有质数的和。
**例:**

```
Input : 10
Output : 17
Explanation : Primes between 1 to 10 : 2, 3, 5, 7.

Input : 11
Output : 28
Explanation : Primes between 1 to 11 : 2, 3, 5, 7, 11.
```

一个**简单的解决方案**是遍历所有从 1 到 n 的数字。对于每个数字，[检查它是否是一个质数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。如果是，将其添加到结果中。
一个**高效的解决方案**是使用厄拉多塞的[筛找出从 t 到 n 的所有素数，然后进行求和。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ program to find sum of primes in
// range from 1 to n.
#include <bits/stdc++.h>
using namespace std;

// Returns sum of primes in range from
// 1 to n.
int sumOfPrimes(int n)
{
    // Array to store prime numbers
    bool prime[n + 1];

    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    memset(prime, true, n + 1);

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Return sum of primes generated through
    // Sieve.
    int sum = 0;
    for (int i = 2; i <= n; i++)
        if (prime[i])
            sum += i;
    return sum;
}

// Driver code
int main()
{
    int n = 11;
    cout << sumOfPrimes(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// sum of primes in
// range from 1 to n.
import java.io.*;
import java.util.*;

class GFG {

    // Returns sum of primes
    // in range from
    // 1 to n.
    static int sumOfPrimes(int n)
    {
        // Array to store prime numbers
        boolean prime[]=new boolean[n + 1];

        // Create a boolean array "prime[0..n]"
        // and initialize all entries it as true.
        // A value in prime[i] will finally be
        // false if i is Not a prime, else true.
        Arrays.fill(prime, true);

        for (int p = 2; p * p <= n; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }

        // Return sum of primes generated through
        // Sieve.
        int sum = 0;
        for (int i = 2; i <= n; i++)
            if (prime[i])
                sum += i;
        return sum;
    }

   // Driver code
    public static void main(String args[])
    {
        int n = 11;
        System.out.print(sumOfPrimes(n));
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 计算机编程语言

```
# Python program to find sum of primes
# in range from 1 to n.

# Returns sum of primes in range from
# 1 to n

def sumOfPrimes(n):
    # list to store prime numbers
    prime = [True] * (n + 1)

    # Create a boolean array "prime[0..n]"
    # and initialize all entries it as true.
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.

    p = 2
    while p * p <= n:
        # If prime[p] is not changed, then
        # it is a prime
        if prime[p] == True:
            # Update all multiples of p
            i = p * 2
            while i <= n:
                prime[i] = False
                i += p
        p += 1   

    # Return sum of primes generated through
    # Sieve.
    sum = 0
    for i in range (2, n + 1):
        if(prime[i]):
            sum += i
    return sum

# Driver code
n = 11
print sumOfPrimes(n)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program to find
// sum of primes in
// range from 1 to n.
using System;

class GFG {

    // Returns sum of primes
    // in range from
    // 1 to n.
    static int sumOfPrimes(int n)
    {

        // Array to store prime numbers
        bool []prime=new bool[n + 1];

        // Create a boolean array "prime[0..n]"
        // and initialize all entries it as true.
        // A value in prime[i] will finally be
        // false if i is Not a prime, else true.
        for(int i = 0; i < n + 1; i++)
        prime[i] = true;

        for (int p = 2; p * p <= n; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true)
            {

                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }

        // Return sum of primes
        // generated  through Sieve.
        int sum = 0;
        for (int i = 2; i <= n; i++)
            if (prime[i])
                sum += i;
        return sum;
    }

    // Driver code
    public static void Main()
    {
        int n = 11;
        Console.Write(sumOfPrimes(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// sum of primes in
// range from 1 to n.

// Returns sum of primes
// in range from 1 to n.
function sumOfPrimes($n)
{
    // Array to store prime
    // numbers bool prime[n + 1];
    // Create a boolean array
    // "prime[0..n]" and initialize
    // all entries it as true.
    // A value in prime[i] will
    // finally be false if i is Not
    // a prime, else true.

    $prime = array_fill(0, $n + 1, true);
    for ($p = 2;
         $p * $p <= $n; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2;
                 $i <= $n; $i += $p)
                $prime[$i] = false;
        }
    }

    // Return sum of primes
    // generated through Sieve.
    $sum = 0;
    for ($i = 2; $i <= $n; $i++)
        if ($prime[$i])
            $sum += $i;
    return $sum;
}

// Driver code
$n = 11;
echo sumOfPrimes($n);

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to find
    // sum of primes in
    // range from 1 to n.

    // Returns sum of primes
    // in range from
    // 1 to n.
    function sumOfPrimes(n)
    {

        // Array to store prime numbers
        let prime = new Array(n + 1);

        // Create a boolean array "prime[0..n]"
        // and initialize all entries it as true.
        // A value in prime[i] will finally be
        // false if i is Not a prime, else true.
        for(let i = 0; i < n + 1; i++)
            prime[i] = true;

        for (let p = 2; p * p <= n; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true)
            {

                // Update all multiples of p
                for (let i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }

        // Return sum of primes
        // generated  through Sieve.
        let sum = 0;
        for (let i = 2; i <= n; i++)
            if (prime[i])
                sum += i;
        return sum;
    }

    let n = 11;
      document.write(sumOfPrimes(n));

</script>
```

**输出:**

```
28
```

本文由 **Rohit Thapliyal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。