# 双素数

> 原文:[https://www.geeksforgeeks.org/twin-prime-numbers/](https://www.geeksforgeeks.org/twin-prime-numbers/)

孪生素数是指两个素数之差为 2 的素数。换句话说，孪生素数是素数差距为 2 的素数。
有时孪生素数一词用于一对孪生素数；这个的另一个名字是素数孪生或素数对。通常这对(2，3)不被认为是一对孪生素数。因为 2 是唯一的偶数素数，所以这一对是唯一相差一的素数对；因此，对于任何其他两个素数，孪生素数的间隔都尽可能地小。
前几对孪生素数是:

```
(3, 5), (5, 7), (11, 13), (17, 19), (29, 31), 
(41, 43), (59, 61), (71, 73), (101, 103), 
(107, 109), (137, 139), …etc.
```

**FACT** :一万以下的孪生素数有 409 个。
除了(3，5)之外，对于某个自然数 n，每个孪生素数对都是(6n–1，6n + 1)的形式；也就是说，两个素数之间的数是 6 的倍数。
示例:

```
Input : n1 = 11, n2 = 13
Output : Twin Prime

Input : n1 = 23, n2 = 37
Output : Not Twin Prime
```

先决条件:[素性测验|第一套(入门和学法)](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)T2】

## C++

```
// CPP program to check twin prime
#include <iostream>
using namespace std;

// Please refer below post for details of this
// function
// https://goo.gl/Wv3fGv
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)  return false;
    if (n <= 3)  return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n%2 == 0 || n%3 == 0) return false;

    for (int i=5; i*i<=n; i=i+6)
        if (n%i == 0 || n%(i+2) == 0)
           return false;

    return true;
}

// Returns true if n1 and n2 are twin primes
bool twinPrime(int n1, int n2)
{
    return (isPrime(n1) && isPrime(n2) &&
                        abs(n1 - n2) == 2);
}

// Driver code
int main()
{
    int n1 = 11, n2 = 13;
    if (twinPrime(n1, n2))
        cout << "Twin Prime" << endl;
    else
        cout << endl
            << "Not Twin Prime" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Twin Prime Numbers
import java.util.*;

class GFG {

    // Please refer below post for
    // details of this function
    // https://goo.gl/Wv3fGv
    static boolean isPrime(int n)
    {
        // Corner cases
        if (n <= 1) return false;
        if (n <= 3) return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Returns true if n1 and n2 are twin primes
    static boolean twinPrime(int n1, int n2)
    {
        return (isPrime(n1) && isPrime(n2) &&
                     Math.abs(n1 - n2) == 2);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int n1 = 11, n2 = 13;

        if (twinPrime(n1, n2))
            System.out.println("Twin Prime");
        else
            System.out.println("Not Twin Prime");
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 code to check twin prime
import math

# Function to check whether a 
# number is prime or not
def isPrime( n ):

    # Corner cases
    if n <= 1:
        return False
    if n <= 3:
        return True

    # This is checked so that we
    # can skip middle five numbers
    # in below loop
    if n%2 == 0 or n%3 == 0:
        return False

    for i in range(5, int(math.sqrt(n)+1), 6):
        if n%i == 0 or n%(i + 2) == 0:
            return False

    return True

# Returns true if n1 and n2 are
# twin primes
def twinPrime(n1 , n2):
    return (isPrime(n1) and isPrime(n2) and
                    abs(n1 - n2) == 2)

# Driver code
n1 = 137
n2 = 139

if twinPrime(n1, n2):
    print("Twin Prime")
else:
    print("Not Twin Prime")

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# Code for Twin Prime Numbers
using System;

class GFG {

    // Please refer below post for
    // details of this function
    // https://goo.gl/Wv3fGv
    static bool isPrime(int n)
    {
        // Corner cases
        if (n <= 1) return false;
        if (n <= 3) return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Returns true if n1 and n2 are twin primes
    static bool twinPrime(int n1, int n2)
    {
        return (isPrime(n1) && isPrime(n2) &&
                    Math.Abs(n1 - n2) == 2);
    }

    // Driver program
    public static void Main()
    {
        int n1 = 11, n2 = 13;

        if (twinPrime(n1, n2))
            Console.WriteLine("Twin Prime");
        else
            Console.WriteLine("Not Twin Prime");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PhP program to check twin prime

// Please refer below post for details
// of this function
// https://goo.gl/Wv3fGv

function isPrime($n)
{

    // Corner cases
    if ($n <= 1) return false;
    if ($n <= 3) return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if ($n % 2 == 0 || $n % 3 == 0)
        return false;

    for ($i = 5; $i * $i <= $n; $i = $i + 6)
        if ($n % $i == 0 || $n % ($i + 2) == 0)
            return false;

    return true;
}

// Returns true if n1 and n2 are twin primes
function twinPrime($n1, $n2)
{
    return (isPrime($n1) && isPrime($n2) &&
                        abs($n1 - $n2) == 2);
}

// Driver code
$n1 = 11; $n2 = 13;
if (twinPrime($n1, $n2))
    echo "Twin Prime", "\n";
else
    echo "\n", "Not Twin Prime", "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript Code for Twin Prime Numbers

    // Please refer below post for
    // details of this function
    // https://goo.gl/Wv3fGv
    function isPrime( n)
    {

        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for ( let i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Returns true if n1 and n2 are twin primes
    function twinPrime( n1, n2) {
        return (isPrime(n1) && isPrime(n2) && Math.abs(n1 - n2) == 2);
    }

    /* Driver program to test above function */

    let n1 = 11, n2 = 13;

    if (twinPrime(n1, n2))
        document.write("Twin Prime");
    else
        document.write("Not Twin Prime");

// This code is contributed by gauravrajput1
</script>
```

输出:

```
Twin Prime
```