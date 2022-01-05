# 求 N 以下所有可截断素数之和

> 原文:[https://www . geeksforgeeks . org/find-所有可截断素数之和-低于-n/](https://www.geeksforgeeks.org/find-the-sum-of-all-truncatable-primes-below-n/)

给定一个整数 **N** ，任务是求 **N** 下面所有[可截断素数](https://en.wikipedia.org/wiki/Truncatable_prime)的和。**可截断质数**是一个数字，它是**左可截断质数**(如果前面的(“左”)数字被连续去掉，那么所有结果数都是质数)以及**右可截断质数**(如果最后的(“右”)数字被连续去掉，那么所有结果数都是质数)。

例如，3797 是可左截断的素数，因为 797、97 和 7 是素数。并且，3797 也是可右截断的素数，因为 379、37 和 3 是素数。因此 3797 是一个可截断的素数。

**示例:**

> **输入:** N = 25
> **输出:** 40
> 2、3、5、7、23 是 25 以下唯一可截断的素数。
> 2 + 3 + 5 + 7 + 23 = 40
> 
> **输入:**N = 40
> T3】输出: 77

**方法:**一种有效的方法是使用厄拉多塞的[筛找出所有素数，并对 **N** 以下的每个数检查它是否是可截断素数。如果是，则加到运行总和中。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 1000005

// To check if a number is prime or not
bool prime[N];

// Sieve of Eratosthenes
// function to find all prime numbers
void sieve()
{
    memset(prime, true, sizeof prime);
    prime[1] = false;
    prime[0] = false;

    for (int i = 2; i < N; i++)
        if (prime[i])
            for (int j = i * 2; j < N; j += i)
                prime[j] = false;
}

// Function to return the sum of
// all truncatable primes below n
int sumTruncatablePrimes(int n)
{
    // To store the required sum
    int sum = 0;

    // Check every number below n
    for (int i = 2; i < n; i++) {

        int num = i;
        bool flag = true;

        // Check from right to left
        while (num) {

            // If number is not prime at any stage
            if (!prime[num]) {
                flag = false;
                break;
            }
            num /= 10;
        }

        num = i;
        int power = 10;

        // Check from left to right
        while (num / power) {

            // If number is not prime at any stage
            if (!prime[num % power]) {
                flag = false;
                break;
            }
            power *= 10;
        }

        // If flag is still true
        if (flag)
            sum += i;
    }

    // Return the required sum
    return sum;
}

// Driver code
int main()
{
    int n = 25;
    sieve();
    cout << sumTruncatablePrimes(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    static final int N = 1000005;

    // To check if a number is prime or not
    static boolean prime[] = new boolean[N];

    // Sieve of Eratosthenes
    // function to find all prime numbers
    static void sieve()
    {
        Arrays.fill(prime, true);
        prime[1] = false;
        prime[0] = false;

        for (int i = 2; i < N; i++)
        {
            if (prime[i])
            {
                for (int j = i * 2; j < N; j += i)
                {
                    prime[j] = false;
                }
            }
        }
    }

    // Function to return the sum of
    // all truncatable primes below n
    static int sumTruncatablePrimes(int n)
    {
        // To store the required sum
        int sum = 0;

        // Check every number below n
        for (int i = 2; i < n; i++)
        {

            int num = i;
            boolean flag = true;

            // Check from right to left
            while (num > 0)
            {

                // If number is not prime at any stage
                if (!prime[num])
                {
                    flag = false;
                    break;
                }
                num /= 10;
            }

            num = i;
            int power = 10;

            // Check from left to right
            while (num / power > 0)
            {

                // If number is not prime at any stage
                if (!prime[num % power])
                {
                    flag = false;
                    break;
                }
                power *= 10;
            }

            // If flag is still true
            if (flag)
            {
                sum += i;
            }
        }

        // Return the required sum
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 25;
        sieve();
        System.out.println(sumTruncatablePrimes(n));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach
N = 1000005

# To check if a number is prime or not
prime = [True for i in range(N)]

# Sieve of Eratosthenes
# function to find all prime numbers
def sieve():
    prime[1] = False
    prime[0] = False

    for i in range(2, N):
        if (prime[i]==True):
            for j in range(i * 2, N, i):
                prime[j] = False

# Function to return the sum of
# all truncatable primes below n
def sumTruncatablePrimes(n):

    # To store the required sum
    sum = 0

    # Check every number below n
    for i in range(2, n):

        num = i
        flag = True

        # Check from right to left
        while (num):

            # If number is not prime at any stage
            if (prime[num] == False):
                flag = False
                break

            num //= 10

        num = i
        power = 10

        # Check from left to right
        while (num // power):

            # If number is not prime at any stage
            if (prime[num % power] == False):
                flag = False
                break

            power *= 10

        # If flag is still true
        if (flag==True):
            sum += i

    # Return the required sum
    return sum

# Driver code
n = 25
sieve()
print(sumTruncatablePrimes(n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the above approach.
using System;
using System.Collections.Generic;

class GFG
{

    static int N = 1000005;

    // To check if a number is prime or not
    static Boolean []prime = new Boolean[N];

    // Sieve of Eratosthenes
    // function to find all prime numbers
    static void sieve()
    {
        Array.Fill(prime, true);
        prime[1] = false;
        prime[0] = false;

        for (int i = 2; i < N; i++)
        {
            if (prime[i])
            {
                for (int j = i * 2; j < N; j += i)
                {
                    prime[j] = false;
                }
            }
        }
    }

    // Function to return the sum of
    // all truncatable primes below n
    static int sumTruncatablePrimes(int n)
    {
        // To store the required sum
        int sum = 0;

        // Check every number below n
        for (int i = 2; i < n; i++)
        {

            int num = i;
            Boolean flag = true;

            // Check from right to left
            while (num > 0)
            {

                // If number is not prime at any stage
                if (!prime[num])
                {
                    flag = false;
                    break;
                }
                num /= 10;
            }

            num = i;
            int power = 10;

            // Check from left to right
            while (num / power > 0)
            {

                // If number is not prime at any stage
                if (!prime[num % power])
                {
                    flag = false;
                    break;
                }
                power *= 10;
            }

            // If flag is still true
            if (flag)
            {
                sum += i;
            }
        }

        // Return the required sum
        return sum;
    }

    // Driver code
    public static void Main(String []args)
    {
        int n = 25;
        sieve();
        Console.WriteLine(sumTruncatablePrimes(n));
    }

}

// This code has been contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$N = 10005;

// To check if a number is prime or not
$prime = array_fill(0, $N, true);

// Sieve of Eratosthenes
// function to find all prime numbers
function sieve()
{
    global $prime, $N;
    $prime[1] = false;
    $prime[0] = false;

    for ($i = 2; $i < $N; $i++)
        if ($prime[$i])
            for ($j = $i * 2; $j < $N; $j += $i)
                $prime[$j] = false;
}

// Function to return the sum of
// all truncatable primes below n
function sumTruncatablePrimes($n)
{
    global $prime, $N;

    // To store the required sum
    $sum = 0;

    // Check every number below n
    for ($i = 2; $i < $n; $i++)
    {
        $num = $i;
        $flag = true;

        // Check from right to left
        while ($num)
        {

            // If number is not prime at any stage
            if (!$prime[$num])
            {
                $flag = false;
                break;
            }
            $num = (int)($num / 10);
        }

        $num = $i;
        $power = 10;

        // Check from left to right
        while ((int)($num / $power))
        {

            // If number is not prime at any stage
            if (!$prime[$num % $power])
            {
                $flag = false;
                break;
            }
            $power *= 10;
        }

        // If flag is still true
        if ($flag)
            $sum += $i;
    }

    // Return the required sum
    return $sum;
}

// Driver code
$n = 25;
sieve();
echo sumTruncatablePrimes($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
let N = 1000005;

// To check if a number is prime or not
let prime = new Array(N);

// Sieve of Eratosthenes
// function to find all prime numbers
function sieve()
{
    for(let i = 0; i < prime.length; i++)
    {
        prime[i] = true;
    }
    prime[1] = false;
    prime[0] = false;

    for(let i = 2; i < N; i++)
    {
        if (prime[i])
        {
            for(let j = i * 2; j < N; j += i)
            {
                prime[j] = false;
            }
        }
    }
}

// Function to return the sum of
// all truncatable primes below n
function sumTruncatablePrimes(n)
{

    // To store the required sum
    let sum = 0;

    // Check every number below n
    for(let i = 2; i < n; i++)
    {
        let num = i;
        let flag = true;

        // Check from right to left
        while (num > 0)
        {

            // If number is not prime at any stage
            if (!prime[num])
            {
                flag = false;
                break;
            }
            num = Math.floor(num / 10);
        }

        num = i;
        let power = 10;

        // Check from left to right
        while (num / power > 0)
        {

            // If number is not prime at any stage
            if (!prime[num % power])
            {
                flag = false;
                break;
            }
            power *= 10;
        }

        // If flag is still true
        if (flag)
        {
            sum += i;
        }
    }

    // Return the required sum
    return sum;
}

// Driver code
let n = 25;
sieve();

document.write(sumTruncatablePrimes(n));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
40
```