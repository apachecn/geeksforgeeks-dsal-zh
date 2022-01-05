# 打印 N 以下所有安全素数

> 原文:[https://www . geesforgeks . org/print-all-safe-primes-below-n/](https://www.geeksforgeeks.org/print-all-safe-primes-below-n/)

给定一个整数 **N** ，任务是打印**N**T4】安全素数以下的所有安全素数。A **安全素数**是 **(2 * p) + 1** 形式的素数，其中 **p** 也是**素数**。

> 前几个安全素数是 5，7，11，23，47，…

**示例:**

> **输入:**N = 13
> T3】输出:5 7 11
> 5 = 2 * 2+1
> 7 = 2 * 3+1
> 11 = 2 * 5+1
> 
> **输入:**N = 6
> T3】输出: 5 7

**方法:**首先使用厄拉多塞的[筛对所有素数进行预计算直到 **N** ，然后从 **2** 开始检查当前素数是否也是安全素数。如果**是**，则打印，否则跳到下一个质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print first n safe primes
void printSafePrimes(int n)
{
    int prime[n + 1];

    // Initialize all entries of integer array
    // as 1\. A value in prime[i] will finally
    // be 0 if i is Not a prime, else 1
    for (int i = 2; i <= n; i++)
        prime[i] = 1;

    // 0 and 1 are not primes
    prime[0] = prime[1] = 0;

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed, then
        //  it is a prime
        if (prime[p] == 1) {

            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = 0;
        }
    }

    for (int i = 2; i <= n; i++) {

        // If i is prime
        if (prime[i] != 0) {

            // 2p + 1
            int temp = (2 * i) + 1;

            // If 2p + 1 is also a prime
            // then set prime[2p + 1] = 2
            if (temp <= n && prime[temp] != 0)
                prime[temp] = 2;
        }
    }

    for (int i = 5; i <= n; i++)

        // i is a safe prime
        if (prime[i] == 2)
            cout << i << " ";
}

// Driver code
int main()
{
    int n = 20;
    printSafePrimes(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG{

    // Function to print first n safe primes
    static void printSafePrimes(int n)
    {
        int prime[] = new int [n + 1];

        // Initialize all entries of integer array
        // as 1\. A value in prime[i] will finally
        // be 0 if i is Not a prime, else 1
        for (int i = 2; i <= n; i++)
            prime[i] = 1;

        // 0 and 1 are not primes
        prime[0] = prime[1] = 0;

        for (int p = 2; p * p <= n; p++)
        {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == 1)
            {

                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = 0;
            }
        }

        for (int i = 2; i <= n; i++)
        {

            // If i is prime
            if (prime[i] != 0)
            {

                // 2p + 1
                int temp = (2 * i) + 1;

                // If 2p + 1 is also a prime
                // then set prime[2p + 1] = 2
                if (temp <= n && prime[temp] != 0)
                    prime[temp] = 2;
            }
        }

        for (int i = 5; i <= n; i++)

            // i is a safe prime
            if (prime[i] == 2)
                System.out.print(i + " ");
    }

    // Driver code
    public static void main(String []args)
    {
        int n = 20;
        printSafePrimes(n);
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import sqrt

# Function to print first n safe primes
def printSafePrimes(n):
    prime = [0 for i in range(n + 1)]

    # Initialize all entries of integer
    # array as 1\. A value in prime[i]
    # will finally be 0 if i is Not a
    # prime, else 1
    for i in range(2, n + 1):
        prime[i] = 1

    # 0 and 1 are not primes
    prime[0] = prime[1] = 0

    for p in range(2, int(sqrt(n)) + 1, 1):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == 1):

            # Update all multiples of p
            for i in range(p * 2, n + 1, p):
                prime[i] = 0

    for i in range(2, n + 1, 1):

        # If i is prime
        if (prime[i] != 0):

            # 2p + 1
            temp = (2 * i) + 1

            # If 2p + 1 is also a prime
            # then set prime[2p + 1] = 2
            if (temp <= n and prime[temp] != 0):
                prime[temp] = 2

    for i in range(5, n + 1):

        # i is a safe prime
        if (prime[i] == 2):
            print(i, end = " ")

# Driver code
if __name__ == '__main__':
    n = 20
    printSafePrimes(n)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

    // Function to print first n safe primes
    static void printSafePrimes(int n)
    {
        int[] prime = new int [n + 1];

        // Initialize all entries of integer array
        // as 1\. A value in prime[i] will finally
        // be 0 if i is Not a prime, else 1
        for (int i = 2; i <= n; i++)
            prime[i] = 1;

        // 0 and 1 are not primes
        prime[0] = prime[1] = 0;

        for (int p = 2; p * p <= n; p++)
        {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == 1)
            {

                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = 0;
            }
        }

        for (int i = 2; i <= n; i++)
        {

            // If i is prime
            if (prime[i] != 0)
            {

                // 2p + 1
                int temp = (2 * i) + 1;

                // If 2p + 1 is also a prime
                // then set prime[2p + 1] = 2
                if (temp <= n && prime[temp] != 0)
                    prime[temp] = 2;
            }
        }

        for (int i = 5; i <= n; i++)

            // i is a safe prime
            if (prime[i] == 2)
                Console.Write(i + " ");
    }

    // Driver code
    public static void Main()
    {
        int n = 20;
        printSafePrimes(n);
    }
}

// This code is contributed by Ita_c.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print first n safe primes
function printSafePrimes($n)
{
    $prime = array();

    // Initialize all entries of integer array
    // as 1\. A value in prime[i] will finally
    // be 0 if i is Not a prime, else 1
    for ($i = 2; $i <= $n; $i++)
        $prime[$i] = 1;

    // 0 and 1 are not primes
    $prime[0] = $prime[1] = 0;

    for ($p = 2; $p * $p <= $n; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == 1)
        {

            // Update all multiples of p
            for ($i = $p * 2;
                 $i <= $n; $i += $p)
                $prime[$i] = 0;
        }
    }

    for ($i = 2; $i <= $n; $i++)
    {

        // If i is prime
        if ($prime[$i] != 0)
        {

            // 2p + 1
            $temp = (2 * $i) + 1;

            // If 2p + 1 is also a prime
            // then set prime[2p + 1] = 2
            if ($temp <= $n &&
                $prime[$temp] != 0)
                $prime[$temp] = 2;
        }
    }

    for ($i = 5; $i <= $n; $i++)

        // i is a safe prime
        if ($prime[$i] == 2)
            echo $i, " ";
}

// Driver code
$n = 20;
printSafePrimes($n);

// This code is contributed
// by aishwarya.27
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print first n safe primes
function printSafePrimes(n)
{
    let prime = new Array(n + 1);

    // Initialize all entries of integer array
    // as 1\. A value in prime[i] will finally
    // be 0 if i is Not a prime, else 1
    for(let i = 2; i <= n; i++)
        prime[i] = 1;

    // 0 and 1 are not primes
    prime[0] = prime[1] = 0;

    for(let p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == 1)
        {

            // Update all multiples of p
            for(let i = p * 2; i <= n; i += p)
                prime[i] = 0;
        }
    }

    for(let i = 2; i <= n; i++)
    {

        // If i is prime
        if (prime[i] != 0)
        {

            // 2p + 1
            let temp = (2 * i) + 1;

            // If 2p + 1 is also a prime
            // then set prime[2p + 1] = 2
            if (temp <= n && prime[temp] != 0)
                prime[temp] = 2;
        }
    }

    for(let i = 5; i <= n; i++)

        // i is a safe prime
        if (prime[i] == 2)
            document.write(i + " ");
}

// Driver code
let n = 20;
printSafePrimes(n);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
5 7 11
```