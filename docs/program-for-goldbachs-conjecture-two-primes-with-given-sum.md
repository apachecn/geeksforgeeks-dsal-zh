# 哥德巴赫猜想程序(给定和的两个素数)

> 原文:[https://www . geeksforgeeks . org/program-for-gold bachs-猜想-两个素数的给定和/](https://www.geeksforgeeks.org/program-for-goldbachs-conjecture-two-primes-with-given-sum/)

哥德巴赫猜想是数学数论中最古老、最著名的未解决问题之一。 ***每一个大于 2 的偶数可以表示为两个素数之和。**T3】*

**示例:**

```
Input :  n = 44
Output :   3 + 41 (both are primes)

Input :  n = 56
Output :  3 + 53  (both are primes) 
```

1.  使用圣达兰的[筛找出质数](https://www.geeksforgeeks.org/sieve-sundaram-print-primes-smaller-n/)
2.  如果没有返回，检查输入的数字是否是大于 2 的偶数。
3.  如果是，那么一个接一个地从 N 中减去一个质数，然后检查差是否也是质数。如果是，那就用总和来表示。

## C++

```
// C++ program to implement Goldbach's conjecture
#include<bits/stdc++.h>
using namespace std;
const int MAX = 10000;

// Array to store all prime less than and equal to 10^6
vector <int> primes;

// Utility function for Sieve of Sundaram
void sieveSundaram()
{
    // In general Sieve of Sundaram, produces primes smaller
    // than (2*x + 2) for a number given number x. Since
    // we want primes smaller than MAX, we reduce MAX to half
    // This array is used to separate numbers of the form
    // i + j + 2*i*j from others where 1 <= i <= j
    bool marked[MAX/2 + 100] = {0};

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for (int i=1; i<=(sqrt(MAX)-1)/2; i++)
        for (int j=(i*(i+1))<<1; j<=MAX/2; j=j+2*i+1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push_back(2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for (int i=1; i<=MAX/2; i++)
        if (marked[i] == false)
            primes.push_back(2*i + 1);
}

// Function to perform Goldbach's conjecture
void findPrimes(int n)
{
    // Return if number is not even or less than 3
    if (n<=2 || n%2 != 0)
    {
        cout << "Invalid Input \n";
        return;
    }

    // Check only upto half of number
    for (int i=0 ; primes[i] <= n/2; i++)
    {
        // find difference by subtracting current prime from n
        int diff = n - primes[i];

        // Search if the difference is also a prime number
        if (binary_search(primes.begin(), primes.end(), diff))
        {
            // Express as a sum of primes
            cout << primes[i] << " + " << diff << " = "
                 << n << endl;
            return;
        }
    }
}

// Driver code
int main()
{
    // Finding all prime numbers before limit
    sieveSundaram();

    // Express number as a sum of two primes
    findPrimes(4);
    findPrimes(38);
    findPrimes(100);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Goldbach's conjecture
import java.util.*;

class GFG
{

static int MAX = 10000;

// Array to store all prime less
// than and equal to 10^6
static ArrayList<Integer> primes = new ArrayList<Integer>();

// Utility function for Sieve of Sundaram
static void sieveSundaram()
{
    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for
    // a number given number x. Since
    // we want primes smaller than MAX,
    // we reduce MAX to half This array is
    // used to separate numbers of the form
    // i + j + 2*i*j from others where 1 <= i <= j
    boolean[] marked = new boolean[MAX / 2 + 100];

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for (int i = 1; i <= (Math.sqrt(MAX) - 1) / 2; i++)
        for (int j = (i * (i + 1)) << 1; j <= MAX / 2; j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.add(2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for (int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.add(2 * i + 1);
}

// Function to perform Goldbach's conjecture
static void findPrimes(int n)
{
    // Return if number is not even or less than 3
    if (n <= 2 || n % 2 != 0)
    {
        System.out.println("Invalid Input ");
        return;
    }

    // Check only upto half of number
    for (int i = 0 ; primes.get(i) <= n / 2; i++)
    {
        // find difference by subtracting
        // current prime from n
        int diff = n - primes.get(i);

        // Search if the difference is
        // also a prime number
        if (primes.contains(diff))
        {
            // Express as a sum of primes
            System.out.println(primes.get(i) +
                        " + " + diff + " = " + n);
            return;
        }
    }
}

// Driver code
public static void main (String[] args)
{
    // Finding all prime numbers before limit
    sieveSundaram();

    // Express number as a sum of two primes
    findPrimes(4);
    findPrimes(38);
    findPrimes(100);
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to implement Goldbach's
# conjecture
import math
MAX = 10000;

# Array to store all prime less
# than and equal to 10^6
primes = [];

# Utility function for Sieve of Sundaram
def sieveSundaram():

    # In general Sieve of Sundaram, produces
    # primes smaller than (2*x + 2) for a
    # number given number x. Since we want
    # primes smaller than MAX, we reduce
    # MAX to half. This array is used to
    # separate numbers of the form i + j + 2*i*j
    # from others where 1 <= i <= j
    marked = [False] * (int(MAX / 2) + 100);

    # Main logic of Sundaram. Mark all
    # numbers which do not generate prime
    # number by doing 2*i+1
    for i in range(1, int((math.sqrt(MAX) - 1) / 2) + 1):
        for j in range((i * (i + 1)) << 1,
                        int(MAX / 2) + 1, 2 * i + 1):
            marked[j] = True;

    # Since 2 is a prime number
    primes.append(2);

    # Print other primes. Remaining primes
    # are of the form 2*i + 1 such that
    # marked[i] is false.
    for i in range(1, int(MAX / 2) + 1):
        if (marked[i] == False):
            primes.append(2 * i + 1);

# Function to perform Goldbach's conjecture
def findPrimes(n):

    # Return if number is not even
    # or less than 3
    if (n <= 2 or n % 2 != 0):
        print("Invalid Input");
        return;

    # Check only upto half of number
    i = 0;
    while (primes[i] <= n // 2):

        # find difference by subtracting
        # current prime from n
        diff = n - primes[i];

        # Search if the difference is also
        # a prime number
        if diff in primes:

            # Express as a sum of primes
            print(primes[i], "+", diff, "=", n);
            return;
        i += 1;

# Driver code

# Finding all prime numbers before limit
sieveSundaram();

# Express number as a sum of two primes
findPrimes(4);
findPrimes(38);
findPrimes(100);

# This code is contributed
# by chandan_jnu
```

## C#

```
// C# program to implement Goldbach's conjecture
using System;
using System.Collections.Generic;

class GFG
{

static int MAX = 10000;

// Array to store all prime less
// than and equal to 10^6
static List<int> primes = new List<int>();

// Utility function for Sieve of Sundaram
static void sieveSundaram()
{
    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for
    // a number given number x. Since
    // we want primes smaller than MAX,
    // we reduce MAX to half This array is
    // used to separate numbers of the form
    // i + j + 2*i*j from others where 1 <= i <= j
    Boolean[] marked = new Boolean[MAX / 2 + 100];

    // Main logic of Sundaram. Mark all numbers which
    // do not generate prime number by doing 2*i+1
    for (int i = 1; i <= (Math.Sqrt(MAX) - 1) / 2; i++)
        for (int j = (i * (i + 1)) << 1; j <= MAX / 2; j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.Add(2);

    // Print other primes. Remaining primes are of the
    // form 2*i + 1 such that marked[i] is false.
    for (int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.Add(2 * i + 1);
}

// Function to perform Goldbach's conjecture
static void findPrimes(int n)
{
    // Return if number is not even or less than 3
    if (n <= 2 || n % 2 != 0)
    {
        Console.WriteLine("Invalid Input ");
        return;
    }

    // Check only upto half of number
    for (int i = 0 ; primes[i] <= n / 2; i++)
    {
        // find difference by subtracting
        // current prime from n
        int diff = n - primes[i];

        // Search if the difference is
        // also a prime number
        if (primes.Contains(diff))
        {
            // Express as a sum of primes
            Console.WriteLine(primes[i] +
                        " + " + diff + " = " + n);
            return;
        }
    }
}

// Driver code
public static void Main (String[] args)
{
    // Finding all prime numbers before limit
    sieveSundaram();

    // Express number as a sum of two primes
    findPrimes(4);
    findPrimes(38);
    findPrimes(100);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement Goldbach's
// conjecture
$MAX = 10000;

// Array to store all prime less than
// and equal to 10^6
$primes = array();

// Utility function for Sieve of Sundaram
function sieveSundaram()
{
    global $MAX, $primes;

    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a
    // number given number x. Since we want
    // primes smaller than MAX, we reduce
    // MAX to half. This array is used to
    // separate numbers of the form i + j + 2*i*j
    // from others where 1 <= i <= j
    $marked = array_fill(0, (int)($MAX / 2) +
                                100, false);

    // Main logic of Sundaram. Mark all
    // numbers which do not generate prime
    // number by doing 2*i+1
    for ($i = 1; $i <= (sqrt($MAX) - 1) / 2; $i++)
        for ($j = ($i * ($i + 1)) << 1;
             $j <= $MAX / 2; $j = $j + 2 * $i + 1)
            $marked[$j] = true;

    // Since 2 is a prime number
    array_push($primes, 2);

    // Print other primes. Remaining primes
    // are of the form 2*i + 1 such that
    // marked[i] is false.
    for ($i = 1; $i <= $MAX / 2; $i++)
        if ($marked[$i] == false)
            array_push($primes, 2 * $i + 1);
}

// Function to perform Goldbach's conjecture
function findPrimes($n)
{
    global $MAX, $primes;

    // Return if number is not even
    // or less than 3
    if ($n <= 2 || $n % 2 != 0)
    {
        print("Invalid Input \n");
        return;
    }

    // Check only upto half of number
    for ($i = 0; $primes[$i] <= $n / 2; $i++)
    {
        // find difference by subtracting
        // current prime from n
        $diff = $n - $primes[$i];

        // Search if the difference is also a
        // prime number
        if (in_array($diff, $primes))
        {
            // Express as a sum of primes
            print($primes[$i] . " + " .
                  $diff . " = " . $n . "\n");
            return;
        }
    }
}

// Driver code

// Finding all prime numbers before limit
sieveSundaram();

// Express number as a sum of two primes
findPrimes(4);
findPrimes(38);
findPrimes(100);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>
// Javascript program to implement Goldbach's
// conjecture
let MAX = 10000;

// Array to store all prime less than
// and equal to 10^6
let primes = new Array();

// Utility function for Sieve of Sundaram
function sieveSundaram()
{  
    // In general Sieve of Sundaram, produces
    // primes smaller than (2*x + 2) for a
    // number given number x. Since we want
    // primes smaller than MAX, we reduce
    // MAX to half. This array is used to
    // separate numbers of the form i + j + 2*i*j
    // from others where 1 <= i <= j
    let marked = new Array(parseInt(MAX / 2) + 100).fill(false);

    // Main logic of Sundaram. Mark all
    // numbers which do not generate prime
    // number by doing 2*i+1
    for (let i = 1; i <= (Math.sqrt(MAX) - 1) / 2; i++)
          for (let j = (i * (i + 1)) << 1;
            j <= MAX / 2; j = j + 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push(2);

    // Print other primes. Remaining primes
    // are of the form 2*i + 1 such that
    // marked[i] is false.
    for (let i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.push(2 * i + 1);
}

// Function to perform Goldbach's conjecture
function findPrimes(n)
{
    // Return if number is not even
    // or less than 3
    if (n <= 2 || n % 2 != 0)
    {
        document.write("Invalid Input <br>");
        return;
    }

    // Check only upto half of number
    for (let i = 0; primes[i] <= n / 2; i++)
    {
        // find difference by subtracting
        // current prime from n
        let diff = n - primes[i];

        // Search if the difference is also a
        // prime number
        if (primes.includes(diff))
        {
            // Express as a sum of primes
            document.write(primes[i] + " + " + diff + " = " + n + "<br>");
            return;
        }
    }
}

// Driver code

// Finding all prime numbers before limit
sieveSundaram();

// Express number as a sum of two primes
findPrimes(4);
findPrimes(38);
findPrimes(100);

// This code is contributed by gfgking
</script>
```

**输出:**

```
2 + 2 = 4
7 + 31 = 38
3 + 97 = 100
```

哥德巴赫数是一个正整数，可以表示为两个奇素数之和。由于 4 是唯一大于 2 的偶数，需要偶数素数 2 才能写成两个素数之和，哥德巴赫猜想陈述的另一种形式是，所有大于 4 的偶数整数都是哥德巴赫数。

本文由 [**萨希尔·查布拉(akku)**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。