# 求一个数的偶数因子之和

> 原文:[https://www.geeksforgeeks.org/find-sum-even-factors-number/](https://www.geeksforgeeks.org/find-sum-even-factors-number/)

给定一个数 n，任务是求一个数的偶因子和。
示例:

```
Input : 30
Output : 48
Even dividers sum 2 + 6 + 10 + 30 = 48

Input : 18
Output : 26
Even dividers sum 2 + 6 + 18 = 26
```

先决条件:[因子之和](https://www.geeksforgeeks.org/sum-factors-number/)
如前所述，一个数的因子之和为
设 p1，p2，… pk 为 n 的素因子，设 a1，a2，..ak 是 p1，p2，..pk 分别除以 n，即我们可以把 n 写成**n =(P1<sup>a1</sup>)*(p2<sup>a2</sup>)*……(PK<sup>AK</sup>)**。

```
Sum of divisors = (1 + p1 + p12 ... p1a1) * 
                  (1 + p2 + p22 ... p2a2) *
                  ...........................
                  (1 + pk + pk2 ... pkak) 
```

如果数是奇数，那么没有偶数因子，所以我们简单地返回 0。
如果数是偶数，我们用上面的公式。我们只需要忽略 2 <sup>0</sup> 。所有其他项相乘产生偶数因子和。例如，考虑 n = 18。可以写成 2 <sup>1</sup> 3 <sup>2</sup> 全因子的太阳是(2<sup>0</sup>+2<sup>1</sup>)*(3<sup>0</sup>+3<sup>1</sup>+3<sup>2</sup>)。如果我们去掉 2 <sup>0</sup> ，那么我们得到的是
偶数因子之和(2)*(1+3+3 <sup>2</sup> ) = 26。
去掉偶数因子中的奇数，我们忽略那么 2 <sup>0</sup> whaich 就是 1。经过这一步，我们只得到偶数因子。注意 2 是唯一的偶数素数。
以下是上述办法的实施情况。

## C++

```
// Formula based CPP program to find sum of all
// divisors of n.
#include <bits/stdc++.h>
using namespace std;

// Returns sum of all factors of n.
int sumofFactors(int n)
{
    // If n is odd, then there are no even factors.
    if (n % 2 != 0)
       return 0;

    // Traversing through all prime factors.
    int res = 1;
    for (int i = 2; i <= sqrt(n); i++) {

        // While i divides n, print i and divide n
        int count = 0, curr_sum = 1, curr_term = 1;
        while (n % i == 0) {
            count++;

            n = n / i;

            // here we remove the 2^0 that is 1.  All
            // other factors
            if (i == 2 && count == 1)
                curr_sum = 0;

            curr_term *= i;
            curr_sum += curr_term;
        }

        res *= curr_sum;
    }

    // This condition is to handle the case when n
    // is a prime number.
    if (n >= 2)
        res *= (1 + n);

    return res;
}

// Driver code
int main()
{
    int n = 18;
    cout << sumofFactors(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Formula based Java program to 
// find sum of all divisors of n.
import java.util.*;
import java.lang.*;

public class GfG{

    // Returns sum of all factors of n.
    public static int sumofFactors(int n)
    {
        // If n is odd, then there
        // are no even factors.
        if (n % 2 != 0)
            return 0;

        // Traversing through all prime
        // factors.
        int res = 1;
        for (int i = 2; i <= Math.sqrt(n); i++)
        {
            int count = 0, curr_sum = 1;
            int curr_term = 1;

            // While i divides n, print i and
            // divide n
            while (n % i == 0)
            {
                count++;

                n = n / i;

                // here we remove the 2^0 that
                // is 1\. All other factors
                if (i == 2 && count == 1)
                    curr_sum = 0;

                curr_term *= i;
                curr_sum += curr_term;
            }

            res *= curr_sum;
        }

        // This condition is to handle the 
        // case when n is a prime number.
        if (n >= 2)
            res *= (1 + n);

        return res;
    }

    // Driver function
    public static void main(String argc[]){
        int n = 18;
        System.out.println(sumofFactors(n));
    }

}

/* This code is contributed by Sagar Shukla */
```

## 蟒蛇 3

```
# Formula based Python3
# program to find sum
# of alldivisors of n.
import math

# Returns sum of all
# factors of n.
def sumofFactors(n) :

    # If n is odd, then
    # there are no even
    # factors.
    if (n % 2 != 0) :
        return 0

    # Traversing through
    # all prime factors.
    res = 1
    for i in range(2, (int)(math.sqrt(n)) + 1) :

        # While i divides n
        # print i and divide n
        count = 0
        curr_sum = 1
        curr_term = 1
        while (n % i == 0) :
            count= count + 1

            n = n // i

            # here we remove the
            # 2^0 that is 1\. All
            # other factors
            if (i == 2 and count == 1) :
                curr_sum = 0

            curr_term = curr_term * i
            curr_sum = curr_sum + curr_term

        res = res * curr_sum

    # This condition is to
    # handle the case when
    # n is a prime number.
    if (n >= 2) :
        res = res * (1 + n)

    return res

# Driver code
n = 18
print(sumofFactors(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// Formula based C# program to
// find sum of all divisors of n.
using System;

public class GfG {

    // Returns sum of all factors of n.
    public static int sumofFactors(int n)
    {
        // If n is odd, then there
        // are no even factors.
        if (n % 2 != 0)
            return 0;

        // Traversing through all prime factors.
        int res = 1;
        for (int i = 2; i <= Math.Sqrt(n); i++)
        {
            int count = 0, curr_sum = 1;
            int curr_term = 1;

            // While i divides n, print i
            // and divide n
            while (n % i == 0)
            {
                count++;

                n = n / i;

                // here we remove the 2^0 that
                // is 1\. All other factors
                if (i == 2 && count == 1)
                    curr_sum = 0;

                curr_term *= i;
                curr_sum += curr_term;
            }

            res *= curr_sum;
        }

        // This condition is to handle the
        // case when n is a prime number.
        if (n >= 2)
            res *= (1 + n);

        return res;
    }

    // Driver Code
    public static void Main() {
        int n = 18;
        Console.WriteLine(sumofFactors(n));
    }

}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Formula based php program to find sum
// of all divisors of n.

// Returns sum of all factors of n.
function sumofFactors($n)
{

    // If n is odd, then there are no
    // even factors.
    if ($n % 2 != 0)
    return 0;

    // Traversing through all prime factors.
    $res = 1;
    for ($i = 2; $i <= sqrt($n); $i++) {

        // While i divides n, print i
        // and divide n
        $count = 0;
        $curr_sum = 1;
        $curr_term = 1;
        while ($n % $i == 0) {
            $count++;

            $n = floor($n / $i);

            // here we remove the 2^0
            // that is 1\. All other
            // factors
            if ($i == 2 && $count == 1)
                $curr_sum = 0;

            $curr_term *= $i;
            $curr_sum += $curr_term;
        }

        $res *= $curr_sum;
    }

    // This condition is to handle the
    // case when n is a prime number.
    if ($n >= 2)
        $res *= (1 + $n);

    return $res;
}

// Driver code
    $n = 18;
    echo sumofFactors($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program to 
// find sum of all divisors of n.

   // Returns sum of all factors of n.
    function sumofFactors(n)
    {
        // If n is odd, then there
        // are no even factors.
        if (n % 2 != 0)
            return 0;

        // Traversing through all prime
        // factors.
        let res = 1;
        for (let i = 2; i <= Math.sqrt(n); i++)
        {
            let count = 0, curr_sum = 1;
            let curr_term = 1;

            // While i divides n, print i and
            // divide n
            while (n % i == 0)
            {
                count++;

                n = n / i;

                // here we remove the 2^0 that
                // is 1\. All other factors
                if (i == 2 && count == 1)
                    curr_sum = 0;

                curr_term *= i;
                curr_sum += curr_term;
            }

            res *= curr_sum;
        }

        // This condition is to handle the 
        // case when n is a prime number.
        if (n >= 2)
            res *= (1 + n);

        return res;
    }

// Driver Function

         let n = 18;
        document.write(sumofFactors(n));

    // This code is contributed by susmitakundugoaldanga.
</script>
```

输出:

```
26
```