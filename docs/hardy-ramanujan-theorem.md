# 哈迪-拉马努扬定理

> 原文:[https://www.geeksforgeeks.org/hardy-ramanujan-theorem/](https://www.geeksforgeeks.org/hardy-ramanujan-theorem/)

Hardy Ramanujam 定理指出，对于**大多数自然数 n**
来说，n 的素因子的数量将近似为 log(log(n)】示例:

> 5192 有 2 个不同的素因子和 log(log(5192))= 2.1615
> 51242183 有 3 个不同的素因子和 log(log(51242183)) = 2.8765

正如声明所引用的，这只是一个近似值。还有**反例**比如

> 510510 有 7 个不同的质因数，但是 log(log(510510))= 2.5759
> 1048576 有 1 个质因数，但是 log(log(1048576)) = 2.62922

这个定理主要用于近似算法，它的证明引出了概率论中更大的概念。

## C++

```
// CPP program to count all prime factors
#include <bits/stdc++.h>
using namespace std;

// A function to count prime factors of
// a given number n
int exactPrimeFactorCount(int n)
{
    int count = 0;

    if (n % 2 == 0) {
        count++;
        while (n % 2 == 0)
            n = n / 2;
    }

    // n must be odd at this point. So we can skip
    // one element (Note i = i +2)
    for (int i = 3; i <= sqrt(n); i = i + 2) {
        if (n % i == 0) {
            count++;
            while (n % i == 0)
                n = n / i;
        }
    }

    // This condition is to handle the case when n
    // is a prime number greater than 2
    if (n > 2)
        count++;
    return count;
}

// driver function
int main()
{
    int n = 51242183;
    cout << "The number of distinct prime factors is/are "
         << exactPrimeFactorCount(n) << endl;
    cout << "The value of log(log(n)) is "
         << log(log(n)) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all prime factors
import java.io.*;

class GFG {

    // A function to count prime factors of
    // a given number n
    static int exactPrimeFactorCount(int n)
    {
        int count = 0;

        if (n % 2 == 0) {
            count++;
            while (n % 2 == 0)
                n = n / 2;
        }

        // n must be odd at this point. So we can skip
        // one element (Note i = i +2)
        for (int i = 3; i <= Math.sqrt(n); i = i + 2)
        {
            if (n % i == 0) {
                count++;
                while (n % i == 0)
                    n = n / i;
            }
        }

        // This condition is to handle the case
        // when n is a prime number greater than 2
        if (n > 2)
            count++;
        return count;
    }

    // driver function
    public static void main (String[] args)
    {
        int n = 51242183;
        System.out.println( "The number of distinct "
                            + "prime factors is/are "
            + exactPrimeFactorCount(n));
        System.out.println( "The value of log(log(n))"
                   + " is " + Math.log(Math.log(n))) ;
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to count all
# prime factors
import math

# A function to count
# prime factors of
# a given number n
def exactPrimeFactorCount(n) :
    count = 0
    if (n % 2 == 0) :
        count = count + 1
        while (n % 2 == 0) :
            n = int(n / 2)

    # n must be odd at this
    # point. So we can skip
    # one element (Note i = i +2)
    i = 3

    while (i <= int(math.sqrt(n))) :
        if (n % i == 0) :    
            count = count + 1
            while (n % i == 0) :
                n = int(n / i)
        i = i + 2

    # This condition is to
    # handle the case when n
    # is a prime number greater
    # than 2
    if (n > 2) :
        count = count + 1
    return count

# Driver Code
n = 51242183
print ("The number of distinct prime factors is/are {}".
       format(exactPrimeFactorCount(n), end = "\n"))
print ("The value of log(log(n)) is {0:.4f}"
            .format(math.log(math.log(n))))

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# program to count all prime factors
using System;

class GFG {

    // A function to count prime factors of
    // a given number n
    static int exactPrimeFactorCount(int n)
    {
        int count = 0;

        if (n % 2 == 0) {
            count++;
            while (n % 2 == 0)
                n = n / 2;
        }

        // n must be odd at this point. So
        // we can skip one element
        // (Note i = i +2)
        for (int i = 3; i <= Math.Sqrt(n);
                                 i = i + 2)
        {
            if (n % i == 0) {
                count++;
                while (n % i == 0)
                    n = n / i;
            }
        }

        // This condition is to handle the
        // case when n is a prime number
        // greater than 2
        if (n > 2)
            count++;

        return count;
    }

    // Driver function
    public static void Main ()
    {
        int n = 51242183;

        Console.WriteLine( "The number of"
        + " distinct prime factors is/are "
              + exactPrimeFactorCount(n));

        Console.WriteLine( "The value of "
                       + "log(log(n)) is "
                + Math.Log(Math.Log(n))) ;
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all prime factors

// A function to count
// prime factors of
// a given number n
function exactPrimeFactorCount($n)
{
    $count = 0;

    if ($n % 2 == 0)
    {
        $count++;
        while ($n % 2 == 0)
            $n = $n / 2;
    }

    // n must be odd at this
    // point. So we can skip
    // one element (Note i = i +2)
    for($i = 3; $i <= sqrt($n); $i = $i + 2)
    {
        if ($n % $i == 0)
        {
            $count++;
            while ($n % $i == 0)
                $n = $n / $i;
        }
    }

    // This condition is to
    // handle the case when n
    // is a prime number greater
    // than 2
    if ($n > 2)
        $count++;
    return $count;
}

    // Driver Code
    $n = 51242183;
    echo "The number of distinct prime".
         " factors is/are ",exactPrimeFactorCount($n),"\n";

    echo "The value of log(log(n)) ".
         "is ",log(log($n)),"\n";

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
// Javascript program to count all prime factors

// A function to count
// prime factors of
// a given number n
function exactPrimeFactorCount(n)
{
    let count = 0;

    if (n % 2 == 0)
    {
        count++;
        while (n % 2 == 0)
            n = n / 2;
    }

    // n must be odd at this
    // point. So we can skip
    // one element (Note i = i +2)
    for(let i = 3; i <= Math.sqrt(n); i = i + 2)
    {
        if (n % i == 0)
        {
            count++;
            while (n % i == 0)
                n = n / i;
        }
    }

    // This condition is to
    // handle the case when n
    // is a prime number greater
    // than 2
    if (n > 2)
        count++;
    return count;
}

    // Driver Code
    let n = 51242183;
    document.write("The number of distinct prime factors is/are " +
                   exactPrimeFactorCount(n) + "<br>");

    document.write("The value of log(log(n)) is "+ Math.log(Math.log(n)) + "<br>");

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
The number of distinct prime factors is/are 3
The value of log(log(n)) is 2.8765
```