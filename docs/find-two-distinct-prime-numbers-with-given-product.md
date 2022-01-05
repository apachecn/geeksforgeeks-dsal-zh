# 用给定的乘积找到两个不同的素数

> 原文:[https://www . geesforgeks . org/find-两个不同的质数-带给定乘积/](https://www.geeksforgeeks.org/find-two-distinct-prime-numbers-with-given-product/)

给定一个数字 N(大于 2)。任务是找到两个不同的素数，它们的乘积等于给定的数。可能有几种可能的组合。只打印第一对这样的。
如果无法将 N 表示为两个不同素数的乘积，则打印“不可能”。

**示例**:

```
Input : N = 15
Output : 3, 5
3 and 5 are both primes and,
3*5 = 15

Input : N = 39
Output : 3, 13
3 and 13 are both primes and,
3*13 = 39
```

其思想是利用厄拉多塞筛找出所有小于或等于给定数 N 的素数。一旦我们有了一个告诉所有素数的数组，我们就可以遍历这个数组来找到一个给定乘积的对。

下面是上述方法的实现:

## C++

```
// C++ program to find a distinct prime number
// pair whose product is equal to given number
#include <bits/stdc++.h>
using namespace std;

// Function to generate all prime
// numbers less than n
bool SieveOfEratosthenes(int n, bool isPrime[])
{
    // Initialize all entries of boolean array
    // as true. A value in isPrime[i] will finally
    // be false if i is Not a prime, else true
    // bool isPrime[n+1];
    isPrime[0] = isPrime[1] = false;
    for (int i = 2; i <= n; i++)
        isPrime[i] = true;

    for (int p = 2; p * p <= n; p++) {
        // If isPrime[p] is not changed, then it is
        // a prime
        if (isPrime[p] == true) {
            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                isPrime[i] = false;
        }
    }
}

// Function to print a prime pair
// with given product
void findPrimePair(int n)
{
    int flag = 0;

    // Generating primes using Sieve
    bool isPrime[n + 1];
    SieveOfEratosthenes(n, isPrime);

    // Traversing all numbers to find first
    // pair
    for (int i = 2; i < n; i++) {
        int x = n / i;

        if (isPrime[i] && isPrime[x] and x != i
            and x * i == n) {
            cout << i << " " << x;
            flag = 1;
            return;
        }
    }

    if (!flag)
        cout << "No such pair found";
}

// Driven Code
int main()
{
    int n = 39;

    findPrimePair(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find a distinct prime number
// pair whose product is equal to given number

class GFG {

    // Function to generate all prime
    // numbers less than n

    static void SieveOfEratosthenes(int n,
                                    boolean isPrime[])
    {
        // Initialize all entries of boolean array
        // as true. A value in isPrime[i] will finally
        // be false if i is Not a prime, else true
        // bool isPrime[n+1];
        isPrime[0] = isPrime[1] = false;
        for (int i = 2; i <= n; i++)
            isPrime[i] = true;

        for (int p = 2; p * p <= n; p++) {
            // If isPrime[p] is not changed, then it is
            // a prime
            if (isPrime[p] == true) {
                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    isPrime[i] = false;
            }
        }
    }

    // Function to print a prime pair
    // with given product
    static void findPrimePair(int n)
    {
        int flag = 0;

        // Generating primes using Sieve
        boolean[] isPrime = new boolean[n + 1];
        SieveOfEratosthenes(n, isPrime);

        // Traversing all numbers to find first
        // pair
        for (int i = 2; i < n; i++) {
            int x = n / i;

            if (isPrime[i] && isPrime[x] && x != i
                && x * i == n) {
                System.out.println(i + " " + x);
                flag = 1;
                return;
            }
        }

        if (flag == 0)
            System.out.println("No such pair found");
    }

    // Driven Code
    public static void main(String[] args)
    {
        int n = 39;

        findPrimePair(n);
    }
}

// This code is contributed by
// ihritik
```

## 蟒蛇 3

```
# Python3 program to find a distinct
# prime number pair whose product
# is equal to given number

# from math lib. import everything
from math import *

# Function to generate all prime
# numbers less than n
def SieveOfEratosthenes(n, isPrime) :

    # Initialize all entries of boolean
    # array as true. A value in isPrime[i]
    # will finally be false if i is Not a
    # prime, else true bool isPrime[n+1];
    isPrime[0], isPrime[1] = False, False

    for i in range(2, n + 1) :
        isPrime[i] = True

    for p in range(2, int(sqrt(n)) + 1) :

        # If isPrime[p] is not changed,
        # then it is a prime
        if isPrime[p] == True :

            for i in range(p * 2, n + 1, p) :
                isPrime[i] = False

# Function to print a prime pair
# with given product
def findPrimePair(n) :

    flag = 0

    # Generating primes using Sieve
    isPrime = [False] * (n + 1)
    SieveOfEratosthenes(n, isPrime)

    # Traversing all numbers to
    # find first pair
    for i in range(2, n) :
        x = int(n / i)

        if (isPrime[i] & isPrime[x] and
             x != i and x * i == n) :
            print(i, x)
            flag = 1
            break

    if not flag :
        print("No such pair found")

# Driver code    
if __name__ == "__main__" :

    # Function calling
    n = 39;

    findPrimePair(n)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find a distinct prime number
// pair whose product is equal to given number
using System;
class GFG
{

// Function to generate all
// prime numbers less than n
static void SieveOfEratosthenes(int n,
                                bool[] isPrime)
{
    // Initialize all entries of bool
    // array as true. A value in
    // isPrime[i] will finally be false
    // if i is Not a prime, else true
    // bool isPrime[n+1];
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

// Function to print a prime
// pair with given product
static void findPrimePair(int n)
{
    int flag = 0;

    // Generating primes using Sieve
    bool[] isPrime = new bool[n + 1];
    SieveOfEratosthenes(n, isPrime);

    // Traversing all numbers to
    // find first pair
    for (int i = 2; i < n; i++)
    {
        int x = n / i;

        if (isPrime[i] && isPrime[x] &&
                x != i && x * i == n)
        {
            Console.Write(i + " " + x);
            flag = 1;
            return;
        }
    }

    if (flag == 0)
        Console.Write("No such pair found");
}

// Driven Code
public static void Main()
{
    int n = 39;

    findPrimePair(n);
}
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find a distinct prime number
// pair whose product is equal to given number

// Function to generate all prime
// numbers less than n
function SieveOfEratosthenes($n, &$isPrime)
{
    // Initialize all entries of boolean
    // array as true. A value in isPrime[i]
    // will finally be false if i is Not a
    // prime, else true bool isPrime[n+1];
    $isPrime[0] = false;
    $isPrime[1] = false;
    for ($i = 2; $i <= $n; $i++)
        $isPrime[$i] = true;

    for ($p = 2; $p * $p <= $n; $p++)
    {
        // If isPrime[p] is not changed,
        // then it is a prime
        if ($isPrime[$p])
        {
            // Update all multiples of p
            for ($i = $p * 2;
                 $i <= $n; $i += $p)
                $isPrime[$i] = false;
        }
    }
}

// Function to print a prime pair
// with given product
function findPrimePair($n)
{
    $flag = 0;

    // Generating primes using Sieve
    $isPrime = array_fill(0, ($n + 1), false);
    SieveOfEratosthenes($n, $isPrime);

    // Traversing all numbers to
    // find first pair
    for ($i = 2; $i < $n; $i++)
    {
        $x = (int)($n / $i);

        if ($isPrime[$i] && $isPrime[$x] and
               $x != $i and $x * $i == $n)
        {
            echo $i . " " . $x;
            $flag = 1;
            return;
        }
    }

    if (!$flag)
        echo "No such pair found";
}

// Driver Code
$n = 39;

findPrimePair($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find a distinct prime number
// pair whose product is equal to given number

// Function to generate all
// prime numbers less than n
function SieveOfEratosthenes(n, isPrime)
{

    // Initialize all entries of bool
    // array as true. A value in
    // isPrime[i] will finally be false
    // if i is Not a prime, else true
    //  isPrime[n+1];
    isPrime[0] = isPrime[1] = false;

    for(var i = 2; i <= n; i++)
        isPrime[i] = true;

    for(var p = 2; p * p <= n; p++)
    {

        // If isPrime[p] is not changed,
        // then it is a prime
        if (isPrime[p] == true)
        {

            // Update all multiples of p
            for(var i = p * 2; i <= n; i += p)
                isPrime[i] = false;
        }
    }
}

// Function to print a prime
// pair with given product
function findPrimePair(n)
{
    var flag = 0;

    // Generating primes using Sieve
    var isPrime = []
    SieveOfEratosthenes(n, isPrime);

    // Traversing all numbers to
    // find first pair
    for(var i = 2; i < n; i++)
    {
        var x = n / i;

        if (isPrime[i] && isPrime[x] &&
                x != i && x * i == n)
        {
            document.write(i + " " + x);
            flag = 1;
            return;
        }
    }

    if (flag == 0)
        document.write("No such pair found");
}

// Driver code
var n = 39;

findPrimePair(n);

// This code is contributed by bunnyram19

</script>
```

**Output:** 

```
3 13
```

**时间复杂度:** O(N*log log(N))

**辅助空间:** O(N)