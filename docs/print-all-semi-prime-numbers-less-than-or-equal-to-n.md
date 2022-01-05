# 打印所有小于或等于 N 的半素数

> 原文:[https://www . geesforgeks . org/print-all-semi-prime-numbers-小于或等于 n/](https://www.geeksforgeeks.org/print-all-semi-prime-numbers-less-than-or-equal-to-n/)

给定一个整数 **N** ，任务是打印所有的[半素数](https://www.geeksforgeeks.org/check-whether-number-semiprime-not/) **≤ N** 。
半素数是可以表示为两个不同素数乘积的整数。
比如 **15 = 3 * 5** 是**半素数**但是 **9 = 3 * 3 不是**。

**示例:**

> **输入:**N = 20
> T3】输出: 6 10 14 15
> 
> **输入:**N = 50
> T3】输出: 6 10 14 15 21 22 26 33 34 35 38 39 46

**先决条件:**

*   [伊拉斯索森筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   [检查一个数是否是半素数](https://www.geeksforgeeks.org/check-whether-number-semiprime-not/)

**方法:**对于每一个数字 **< N** ，计算它所具有的质因数的数量。如果素数的个数是 **2** ，那么这个数就是一个半素数，因为所有的半素数只有 **2** 个素数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to create Sieve for Semi Prime Numbers
vector<int> createSemiPrimeSieve(int n)
{
    int v[n + 1];

    // This array will initially store the indexes
    // After performing below operations if any
    // element of array becomes 1 this means
    // that the given index is a semi-prime number

    // Storing indices in each element of vector
    for (int i = 1; i <= n; i++)
        v[i] = i;

    int countDivision[n + 1];

    for (int i = 0; i < n + 1; i++)
        countDivision[i] = 2;

    // This array will initially be initialized by 2 and
    // will just count the divisions of a number
    // As a semiprime number has only 2 prime factors
    // which means after dividing by the 2 prime numbers
    // if the index countDivision[x] = 0 and v[x] = 1
    // this means that x is a semiprime number

    // If number a is prime then its
    // countDivision[a] = 2 and v[a] = a

    for (int i = 2; i <= n; i++) {

        // If v[i] != i this means that it is
        // not a prime number as it contains
        // a divisor which has already divided it
        // same reason if countDivision[i] != 2

        if (v[i] == i && countDivision[i] == 2) {

            // j goes for each factor of i
            for (int j = 2 * i; j <= n; j += i) {
                if (countDivision[j] > 0) {

                    // Dividing the number by i
                    // and storing the dividend
                    v[j] = v[j] / i;

                    // Decreasing the countDivision
                    countDivision[j]--;
                }
            }
        }
    }

    // A new vector to store all Semi Primes
    vector<int> res;

    for (int i = 2; i <= n; i++) {

        // If a number becomes one and
        // its countDivision becomes 0
        // it means the number has
        // two prime divisors
        if (v[i] == 1 && countDivision[i] == 0)
            res.push_back(i);
    }

    return res;
}

// Driver code
int main()
{
    int n = 16;
    vector<int> semiPrime = createSemiPrimeSieve(n);

    // Print all semi-primes
    for (int i = 0; i < semiPrime.size(); i++)
        cout << semiPrime[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

// Java implementation of the approach
class GFG
{

    // Function to create Sieve for Semi Prime Numbers
    static Vector<Integer> createSemiPrimeSieve(int n)
    {
        int v[] = new int[n + 1];

        // This array will initially store the indexes
        // After performing below operations if any
        // element of array becomes 1 this means
        // that the given index is a semi-prime number
        // Storing indices in each element of vector
        for (int i = 1; i <= n; i++)
        {
            v[i] = i;
        }

        int countDivision[] = new int[n + 1];

        for (int i = 0; i < n + 1; i++)
        {
            countDivision[i] = 2;
        }

        // This array will initially be initialized by 2 and
        // will just count the divisions of a number
        // As a semiprime number has only 2 prime factors
        // which means after dividing by the 2 prime numbers
        // if the index countDivision[x] = 0 and v[x] = 1
        // this means that x is a semiprime number
        // If number a is prime then its
        // countDivision[a] = 2 and v[a] = a
        for (int i = 2; i <= n; i++)
        {

            // If v[i] != i this means that it is
            // not a prime number as it contains
            // a divisor which has already divided it
            // same reason if countDivision[i] != 2
            if (v[i] == i && countDivision[i] == 2)
            {

                // j goes for each factor of i
                for (int j = 2 * i; j <= n; j += i)
                {
                    if (countDivision[j] > 0)
                    {

                        // Dividing the number by i
                        // and storing the dividend
                        v[j] = v[j] / i;

                        // Decreasing the countDivision
                        countDivision[j]--;
                    }
                }
            }
        }

        // A new vector to store all Semi Primes
        Vector<Integer> res = new Vector<>();

        for (int i = 2; i <= n; i++)
        {

            // If a number becomes one and
            // its countDivision becomes 0
            // it means the number has
            // two prime divisors
            if (v[i] == 1 && countDivision[i] == 0) {
                res.add(i);
            }
        }

        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 16;
        Vector<Integer> semiPrime = createSemiPrimeSieve(n);

        // Print all semi-primes
        for (int i = 0; i < semiPrime.size(); i++)
        {
            System.out.print(semiPrime.get(i) + " ");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to create Sieve for Semi Prime Numbers
def createSemiPrimeSieve(n):
    v = [0 for i in range(n + 1)]

    # This array will initially store the indexes
    # After performing below operations if any
    # element of array becomes 1 this means
    # that the given index is a semi-prime number

    # Storing indices in each element of vector
    for i in range(1, n + 1):
        v[i] = i

    countDivision = [0 for i in range(n + 1)]

    for i in range(n + 1):
        countDivision[i] = 2

    # This array will initially be initialized by 2 and
    # will just count the divisions of a number
    # As a semiprime number has only 2 prime factors
    # which means after dividing by the 2 prime numbers
    # if the index countDivision[x] = 0 and v[x] = 1
    # this means that x is a semiprime number

    # If number a is prime then its
    # countDivision[a] = 2 and v[a] = a

    for i in range(2, n + 1, 1):

        # If v[i] != i this means that it is
        # not a prime number as it contains
        # a divisor which has already divided it
        # same reason if countDivision[i] != 2
        if (v[i] == i and countDivision[i] == 2):

            # j goes for each factor of i
            for j in range(2 * i, n + 1, i):
                if (countDivision[j] > 0):

                    # Dividing the number by i
                    # and storing the dividend
                    v[j] = int(v[j] / i)

                    # Decreasing the countDivision
                    countDivision[j] -= 1

    # A new vector to store all Semi Primes
    res = []

    for i in range(2, n + 1, 1):

        # If a number becomes one and
        # its countDivision becomes 0
        # it means the number has
        # two prime divisors
        if (v[i] == 1 and countDivision[i] == 0):
            res.append(i)

    return res

# Driver code
if __name__ == '__main__':
    n = 16
    semiPrime = createSemiPrimeSieve(n)

    # Print all semi-primes
    for i in range(len(semiPrime)):
        print(semiPrime[i], end = " ")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;

class GFG
{

// Function to create Sieve for Semi Prime Numbers
static ArrayList createSemiPrimeSieve(int n)
{
    int[] v = new int[n + 1];

    // This array will initially store the indexes
    // After performing below operations if any
    // element of array becomes 1 this means
    // that the given index is a semi-prime number

    // Storing indices in each element of vector
    for (int i = 1; i <= n; i++)
        v[i] = i;

    int[] countDivision = new int[n + 1];

    for (int i = 0; i < n + 1; i++)
        countDivision[i] = 2;

    // This array will initially be initialized by 2 and
    // will just count the divisions of a number
    // As a semiprime number has only 2 prime factors
    // which means after dividing by the 2 prime numbers
    // if the index countDivision[x] = 0 and v[x] = 1
    // this means that x is a semiprime number

    // If number a is prime then its
    // countDivision[a] = 2 and v[a] = a

    for (int i = 2; i <= n; i++)
    {

        // If v[i] != i this means that it is
        // not a prime number as it contains
        // a divisor which has already divided it
        // same reason if countDivision[i] != 2

        if (v[i] == i && countDivision[i] == 2)
        {

            // j goes for each factor of i
            for (int j = 2 * i; j <= n; j += i)
            {
                if (countDivision[j] > 0)
                {

                    // Dividing the number by i
                    // and storing the dividend
                    v[j] = v[j] / i;

                    // Decreasing the countDivision
                    countDivision[j]--;
                }
            }
        }
    }

    // A new vector to store all Semi Primes
    ArrayList res = new ArrayList();

    for (int i = 2; i <= n; i++)
    {

        // If a number becomes one and
        // its countDivision becomes 0
        // it means the number has
        // two prime divisors
        if (v[i] == 1 && countDivision[i] == 0)
            res.Add(i);
    }

    return res;
}

// Driver code
static void Main()
{
    int n = 16;
    ArrayList semiPrime = createSemiPrimeSieve(n);

    // Print all semi-primes
    for (int i = 0; i < semiPrime.Count; i++)
        Console.Write((int)semiPrime[i]+" ");
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to create Sieve for Semi Prime Numbers
function createSemiPrimeSieve($n)
{
    $v = array_fill(0, $n + 1, 0);

    // This array will initially store the indexes
    // After performing below operations if any
    // element of array becomes 1 this means
    // that the given index is a semi-prime number

    // Storing indices in each element of vector
    for ($i = 1; $i <= $n; $i++)
        $v[$i] = $i;

    $countDivision = array_fill(0, $n + 1, 0);

    for ($i = 0; $i < $n + 1; $i++)
        $countDivision[$i] = 2;

    // This array will initially be initialized by 2 and
    // will just count the divisions of a number
    // As a semiprime number has only 2 prime factors
    // which means after dividing by the 2 prime numbers
    // if the index countDivision[x] = 0 and $v[x] = 1
    // this means that x is a semiprime number

    // If number a is prime then its
    // countDivision[a] = 2 and $v[a] = a

    for ($i = 2; $i <= $n; $i++)
    {

        // If v[i] != i this means that it is
        // not a prime number as it contains
        // a divisor which has already divided it
        // same reason if countDivision[i] != 2

        if ($v[$i] == $i && $countDivision[$i] == 2)
        {

            // j goes for each factor of i
            for ($j = 2 * $i; $j <= $n; $j += $i)
            {
                if ($countDivision[$j] > 0)
                {

                    // Dividing the number by i
                    // and storing the dividend
                    $v[$j] = $v[$j] / $i;

                    // Decreasing the countDivision
                    $countDivision[$j]--;
                }
            }
        }
    }

    // A new vector to store all Semi Primes
    $res = array();

    for ($i = 2; $i <= $n; $i++)
    {

        // If a number becomes one and
        // its countDivision becomes 0
        // it means the number has
        // two prime divisors
        if ($v[$i] == 1 && $countDivision[$i] == 0)
            array_push($res, $i);
    }

    return $res;
}

// Driver code
$n = 16;
$semiPrime= array();
$semiPrime = createSemiPrimeSieve($n);

// Print all semi-primes
for ($i = 0; $i < count($semiPrime); $i++)
    echo $semiPrime[$i], " ";

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to create Sieve for Semi Prime Numbers
function createSemiPrimeSieve(n)
{
    let v = new Array(n + 1).fill(0);

    // This array will initially store the indexes
    // After performing below operations if any
    // element of array becomes 1 this means
    // that the given index is a semi-prime number

    // Storing indices in each element of vector
    for (let i = 1; i <= n; i++)
        v[i] = i;

    let countDivision = new Array(n + 1).fill(0);

    for (let i = 0; i < n + 1; i++)
        countDivision[i] = 2;

    // This array will initially be initialized by 2 and
    // will just count the divisions of a number
    // As a semiprime number has only 2 prime factors
    // which means after dividing by the 2 prime numbers
    // if the index countDivision[x] = 0 and v[x] = 1
    // this means that x is a semiprime number

    // If number a is prime then its
    // countDivision[a] = 2 and v[a] = a

    for (let i = 2; i <= n; i++)
    {

        // If v[i] != i this means that it is
        // not a prime number as it contains
        // a divisor which has already divided it
        // same reason if countDivision[i] != 2

        if (v[i] == i && countDivision[i] == 2)
        {

            // j goes for each factor of i
            for (let j = 2 * i; j <= n; j += i)
            {
                if (countDivision[j] > 0)
                {

                    // Dividing the number by i
                    // and storing the dividend
                    v[j] = v[j] / i;

                    // Decreasing the countDivision
                    countDivision[j]--;
                }
            }
        }
    }

    // A new vector to store all Semi Primes
    let res = new Array();

    for (let i = 2; i <= n; i++)
    {

        // If a number becomes one and
        // its countDivision becomes 0
        // it means the number has
        // two prime divisors
        if (v[i] == 1 && countDivision[i] == 0)
            res.push(i);
    }

    return res;
}

// Driver code
let n = 16;
let semiPrime= new Array();
semiPrime = createSemiPrimeSieve(n);

// Print all semi-primes
for (let i = 0; i < semiPrime.length; i++)
    document.write(semiPrime[i] + " ");

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
6 10 14 15
```