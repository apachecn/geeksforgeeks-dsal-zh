# 求一个数的奇数因子之和

> 原文:[https://www.geeksforgeeks.org/find-sum-odd-factors-number/](https://www.geeksforgeeks.org/find-sum-odd-factors-number/)

给定一个数 n，任务是找到奇数因子和。
**例:**

```
Input : n = 30
Output : 24
Odd dividers sum 1 + 3 + 5 + 15 = 24 

Input : 18
Output : 13
Odd dividers sum 1 + 3 + 9 = 13
```

先决条件:[一个数的所有因子之和](https://www.geeksforgeeks.org/sum-factors-number/)
如前所述[前一篇](https://www.geeksforgeeks.org/sum-factors-number)中，一个数的因子之和为
让 p <sub>1</sub> ，p <sub>2</sub> ，… p <sub>k</sub> 为 n 的[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)，让 a <sub>1</sub> ，a <sub>2</sub> ，..a <sub>k</sub> 为 p<sub>1</sub>p<sub>2</sub>的最高幂，..p <sub>k</sub> 分别表示除 n，即我们可以把 n 写成**n =(p<sub>1</sub>T29】aT31<sup>1</sup>T34】)*(p<sub>2</sub>T37】aT39<sup>2</sup>T42】)*……(p<sub>k</sub>T45】aT47<sup>k</sup>** 

```
Sum of divisors = (1 + p1 + p12 ... p1a<sup>1</sup>) * 
                  (1 + p2 + p22 ... p2a<sup>2</sup>) *
                  .............................................
                  (1 + pk + pk2 ... pka<sup>k</sup>) 
```

要求奇数因子的和，我们只需忽略偶数因子及其幂。例如，考虑 n = 18。可以写成 2 <sup>1</sup> 3 <sup>2</sup> ，全因子的太阳为(1)*(1 + 2)*(1 + 3 + 3 <sup>2</sup> )。奇数因子之和(1)*(1+3+3 <sup>2</sup> ) = 13。
为了去掉所有偶数因子，我们在 n 可被 2 整除的情况下，反复对 n 进行除法运算。经过这一步，我们只得到奇数因子。注意 2 是唯一的偶数素数。

## C++

```
// Formula based CPP program
// to find sum of all
// divisors of n.
#include <bits/stdc++.h>
using namespace std;

// Returns sum of all factors of n.
int sumofoddFactors(int n)
{
    // Traversing through all
    // prime factors.
    int res = 1;

    // ignore even factors by
    // removing all powers of
    // 2
    while (n % 2 == 0)
        n = n / 2;

    for (int i = 3; i <= sqrt(n); i++)
    {

        // While i divides n, print
        // i and divide n
        int count = 0, curr_sum = 1;
        int curr_term = 1;
        while (n % i == 0) {
            count++;

            n = n / i;

            curr_term *= i;
            curr_sum += curr_term;
        }

        res *= curr_sum;
    }

    // This condition is to handle
    // the case when n is a prime
    // number.
    if (n >= 2)
        res *= (1 + n);

    return res;
}

// Driver code
int main()
{
    int n = 30;
    cout << sumofoddFactors(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Formula based Java program
// to find sum of all divisors
// of n.
import java.io.*;
import java.math.*;

class GFG {

    // Returns sum of all
    // factors of n.
    static int sumofoddFactors(int n)
    {
        // Traversing through
        // all prime factors.
        int res = 1;

        // ignore even factors by
        // removing all powers
        // of 2
        while (n % 2 == 0)
            n = n / 2;

        for (int i = 3; i <= Math.sqrt(n); i++)
        {

            // While i divides n, print i
            // and divide n
            int count = 0, curr_sum = 1;
            int curr_term = 1;
            while (n % i == 0)
            {
                count++;

                n = n / i;

                curr_term *= i;
                curr_sum += curr_term;
            }

            res *= curr_sum;

        }

        // This condition is to handle
        // the case when n is a
        // prime number.
        if (n >= 2)
            res *= (1 + n);

        return res;
    }

    // Driver code
    public static void main(String args[])
                        throws IOException
    {
        int n = 30;
        System.out.println(sumofoddFactors(n));
    }
}

/* This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Formula based Python3 program
# to find sum of all divisors
# of n.
import math

# Returns sum of all factors
# of n.
def sumofoddFactors( n ):

    # Traversing through all
    # prime factors.
    res = 1

    # ignore even factors by
    # of 2
    while n % 2 == 0:
        n = n // 2

    for i in range(3, int(math.sqrt(n) + 1)):

        # While i divides n, print
        # i and divide n
        count = 0
        curr_sum = 1
        curr_term = 1
        while n % i == 0:
            count+=1

            n = n // i
            curr_term *= i
            curr_sum += curr_term

        res *= curr_sum

    # This condition is to
    # handle the case when
    # n is a prime number.
    if n >= 2:
        res *= (1 + n)

    return res

# Driver code
n = 30
print(sumofoddFactors(n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// Formula based C# program to
// find sum of all divisors of n.
using System;

class GFG {

    // Returns sum of all
    // factors of n.
    static int sumofoddFactors(int n)
    {
        // Traversing through
        // all prime factors.
        int res = 1;

        // ignore even factors by
        // removing all powers
        // of 2
        while (n % 2 == 0)
            n = n / 2;

        for (int i = 3; i <= Math.Sqrt(n); i++)
        {
            // While i divides n, print i
            // and divide n
            int count = 0, curr_sum = 1;
            int curr_term = 1;
            while (n % i == 0)
            {
                count++;
                n = n / i;

                curr_term *= i;
                curr_sum += curr_term;
            }

            res *= curr_sum;
        }

        // This condition is to handle
        // the case when n is a
        // prime number.
        if (n >= 2)
            res *= (1 + n);

        return res;
    }

    // Driver code
    public static void Main(String[] argc)
    {
        int n = 30;
        Console.Write(sumofoddFactors(n));
    }
}

/* This code is contributed by parashar...*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Formula based PHP program
// to find sum of all
// divisors of n.

// Returns sum of all factors of n.
function sumofoddFactors($n)
{
    // Traversing through all
    // prime factors.
    $res = 1;

    // ignore even factors by
    // removing all powers of
    // 2
    while ($n % 2 == 0)
        $n = $n / 2;

    for ($i = 3; $i <= sqrt($n); $i++)
    {

        // While i divides n, print
        // i and divide n
        $count = 0; $curr_sum = 1;
        $curr_term = 1;
        while ($n % $i == 0)
        {
            $count++;

            $n = $n / $i;

            $curr_term *= $i;
            $curr_sum += $curr_term;
        }

        $res *= $curr_sum;
    }

    // This condition is to
    // handle the case when
    // n is a prime number.
    if ($n >= 2)
        $res *= (1 + $n);

    return $res;
}

// Driver code
$n = 30;
echo sumofoddFactors($n);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Formula based Javascript program
// to find sum of all
// divisors of n.

// Returns sum of all factors of n.
function sumofoddFactors(n)
{
    // Traversing through all
    // prime factors.
    let res = 1;

    // ignore even factors by
    // removing all powers of
    // 2
    while (n % 2 == 0)
        n = n / 2;

    for (let i = 3; i <= Math.sqrt(n); i++)
    {

        // While i divides n, print
        // i and divide n
        let count = 0;
        let curr_sum = 1;
        let curr_term = 1;
        while (n % i == 0)
        {
            count++;

            n = n / i;

            curr_term *= i;
            curr_sum += curr_term;
        }

        res *= curr_sum;
    }

    // This condition is to
    // handle the case when
    // n is a prime number.
    if (n >= 2)
        res *= (1 + n);

    return res;
}

// Driver code
let n = 30;
document.write(sumofoddFactors(n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
24
```