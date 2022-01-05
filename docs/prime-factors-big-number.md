# 一个大数的质因数

> 原文:[https://www.geeksforgeeks.org/prime-factors-big-number/](https://www.geeksforgeeks.org/prime-factors-big-number/)

给定一个数字 N，打印所有质因数及其幂。这里 N <= 10^18
**例:**

```
Input : 250 
Output : 2  1
         5  3
Explanation: The prime factors of 250 are 2
and 5\. 2 appears once in the prime factorization 
of and 5 is thrice in it. 

Input : 1000000000000000000
Output : 2  18
         5  18
Explanation: The prime factors of 1000000000000000000
are 2 and 5\. The prime factor 2 appears 18 times in 
the prime factorization. 5 appears 18 times. 
```

我们不能对单个大数使用[screen 的实现](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)，因为它需要比例空间。我们首先计算 2 是给定数的因子的次数，然后我们从 **3 迭代到 Sqrt(n)** 得到一个素数除以一个特定数的次数，这个特定数每次减少 n/i，我们将我们的数 n(其素因子分解将被计算)除以它对应的最小素因子，直到 n 变成 1。如果在 n > 2 的末尾，它意味着它是一个质数，所以我们打印那个特定的数。

## C++

```
// CPP program to print prime factors and their
// powers.
#include <bits/stdc++.h>
using namespace std;

// function to calculate all the prime factors and
// count of every prime factor
void factorize(long long n)
{
    int count = 0;

    // count the number of times 2 divides
    while (!(n % 2)) {
        n >>= 1; // equivalent to n=n/2;
        count++;
    }

    // if 2 divides it
    if (count)
        cout << 2 << "  " << count << endl;

    // check for all the possible numbers that can
    // divide it
    for (long long i = 3; i <= sqrt(n); i += 2) {
        count = 0;
        while (n % i == 0) {
            count++;
            n = n / i;
        }
        if (count)
            cout << i << "  " << count << endl;
    }

    // if n at the end is a prime number.
    if (n > 2)
        cout << n << "  " << 1 << endl;
}

// driver program to test the above function
int main()
{
    long long n = 1000000000000000000;
    factorize(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to print prime
// factors and their powers.

class GFG {

// function to calculate all the
// prime factors and count of
// every prime factor
    static void factorize(long n) {
        int count = 0;

        // count the number of times 2 divides
        while (!(n % 2 > 0)) {
            // equivalent to n=n/2;
            n >>= 1;

            count++;
        }

        // if 2 divides it
        if (count > 0) {
            System.out.println("2" + " " + count);
        }

        // check for all the possible
        // numbers that can divide it
        for (long i = 3; i <= (long) Math.sqrt(n); i += 2) {
            count = 0;
            while (n % i == 0) {
                count++;
                n = n / i;
            }
            if (count > 0) {
                System.out.println(i + " " + count);
            }
        }

        // if n at the end is a prime number.
        if (n > 2) {
            System.out.println(n + " " + "1");
        }
    }

    public static void main(String[] args) {
        long n = 1000000000000000000L;
        factorize(n);
    }
}

/*This code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python3 program to print prime factors
# and their powers.
import math

# Function to calculate all the prime
# factors and count of every prime factor
def factorize(n):
    count = 0;

    # count the number of
    # times 2 divides
    while ((n % 2 > 0) == False):

        # equivalent to n = n / 2;
        n >>= 1;
        count += 1;

    # if 2 divides it
    if (count > 0):
        print(2, count);

    # check for all the possible
    # numbers that can divide it
    for i in range(3, int(math.sqrt(n)) + 1):
        count = 0;
        while (n % i == 0):
            count += 1;
            n = int(n / i);
        if (count > 0):
            print(i, count);
        i += 2;

    # if n at the end is a prime number.
    if (n > 2):
        print(n, 1);

# Driver Code
n = 1000000000000000000;
factorize(n);

# This code is contributed by mits
```

## C#

```
// C# program to print prime
// factors and their powers.
using System;

public class GFG
{

// function to calculate all the
// prime factors and count of
// every prime factor
static void factorize(long n)
{
    int count = 0;

    // count the number of times 2 divides
    while (! (n % 2 > 0))
    {
        // equivalent to n=n/2;
        n >>= 1;

        count++;
    }

    // if 2 divides it
    if (count > 0)
        Console.WriteLine("2" + " " +count);

    // check for all the possible
    // numbers that can divide it
    for (long i = 3; i <= (long)
         Math.Sqrt(n); i += 2)
    {
        count = 0;
        while (n % i == 0) {
            count++;
            n = n / i;
        }
        if (count > 0)
            Console.WriteLine(i + " " + count);
    }

    // if n at the end is a prime number.
    if (n > 2)
        Console.WriteLine(n +" " + "1" );
}

    // Driver Code
    static public void Main ()
    {
        long n = 1000000000000000000;
        factorize(n);

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print prime
// factors and their powers.

// function to calculate all
// the prime factors and count
// of every prime factor
function factorize($n)
{
    $count = 0;

    // count the number of
    // times 2 divides
    while (!($n % 2))
    {
        // equivalent to n = n / 2;
        $n >>= 1;
        $count++;
    }

    // if 2 divides it
    if ($count)
        echo(2 . " " . $count . "\n");

    // check for all the possible
    // numbers that can divide it
    for ($i = 3; $i <= sqrt($n); $i += 2)
    {
        $count = 0;
        while ($n % $i == 0)
        {
            $count++;
            $n = $n / $i;
        }
        if ($count)
            echo($i . " " . $count);
    }

    // if n at the end is a prime number.
    if ($n > 2)
        echo($n . " " . 1);
}

// Driver Code
$n = 1000000000000000000;
factorize($n);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to print prime factors and their
// powers.

// function to calculate all the prime factors and
// count of every prime factor
function factorize(n)
{
    var count = 0;

    // count the number of times 2 divides
    while ((n % 2)==0) {
        n = parseInt(n/2) // equivalent to n=n/2;
        count++;
    }

    // if 2 divides it
    if (count)
        document.write( 2 + "  " + count + "<br>");

    // check for all the possible numbers that can
    // divide it
    for (var i = 3; i <= parseInt(Math.sqrt(n)); i += 2) {
        count = 0;
        while (n % i == 0) {
            count++;
            n = parseInt(n / i);
        }
        if (count!=0)
            document.write( i + "  " + count + "<br>");
    }

    // if n at the end is a prime number.
    if (n > 2)
        document.write( n + "  " + 1 + "<br>");
}

// driver program to test the above function
var n = 1000000000000000000;
factorize(n);

</script>
```

**输出:**

```
2 18
5 18
```

**时间复杂度:** O(sqrt(n))。