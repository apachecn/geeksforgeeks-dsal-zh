# 检查给定的两个数是否为友好对

> 原文:[https://www . geesforgeks . org/check-given-two-number-friendly-pair-not/](https://www.geeksforgeeks.org/check-given-two-number-friendly-pair-not/)

给定两个正整数 **N** 、 **M** 。任务是检查 N 和 M 是否是[友好的一对](https://en.wikipedia.org/wiki/Friendly_number)。

> 在数论中，友好对是两个具有共同丰度指数的数，一个数的除数之和与数本身的比值，即？(n)/n . S . o，两个数字 n 和 m 是友好数字如果
> ？(n)/n =？(m)/m.
> 哪里**？(n)** 是 n 的除数之和。

示例:

```
Input : n = 6, m = 28
Output : Yes
Explanation:
Divisor of 6 are 1, 2, 3, 6.
Divisor of 28 are 1, 2, 4, 7, 14, 28.
Sum of divisor of 6 and 28 are 12 and 56
respectively. Abundancy index of 6 and 28 
are 2\. So they are friendly pair.

Input : n = 18, m = 26
Output : No
```

想法是找到 n 和 m 的除数的[和，并检查 n 和 m 的丰度指数，我们将找到 n 和 m 的](https://www.geeksforgeeks.org/sum-factors-number/)[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)及其除数之和。并通过检查分子和分母是否相等来检查 n 和 m 的丰度指数的简化形式是否相等。为了找到简化形式，我们将分子和分母除以 GCD。
以下是以上想法的实现:

## C++

```
// Check if the given two number
// are friendly pair or not.
#include <bits/stdc++.h>
using namespace std;

// Returns sum of all factors of n.
int sumofFactors(int n)
{

    // Traversing through all prime factors.
    int res = 1;
    for (int i = 2; i <= sqrt(n); i++) {

        int count = 0, curr_sum = 1;
        int curr_term = 1;
        while (n % i == 0) {
            count++;

            // THE BELOW STATEMENT MAKES
            // IT BETTER THAN ABOVE METHOD
            // AS WE REDUCE VALUE OF n.
            n = n / i;

            curr_term *= i;
            curr_sum += curr_term;
        }

        res *= curr_sum;
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2.
    if (n >= 2)
        res *= (1 + n);

    return res;
}

// Function to return gcd of a and b
int gcd(int a, int b)
{
    if (a == 0)
        return b;
    return gcd(b % a, a);
}

// Function to check if the given two
// number are friendly pair or not.
bool checkFriendly(int n, int m)
{
    // Finding the sum of factors of n and m
    int sumFactors_n = sumofFactors(n);
    int sumFactors_m = sumofFactors(m);

    // finding gcd of n and sum of its factors.
    int gcd_n = gcd(n, sumFactors_n);

    // finding gcd of m and sum of its factors.
    int gcd_m = gcd(m, sumFactors_m);

    // checking is numerator and denominator of
    // abundancy index of both number are equal
    // or not.
    if (n / gcd_n == m / gcd_m &&
        sumFactors_n / gcd_n == sumFactors_m / gcd_m)
        return true;

    else
        return false;
}

// Driver code
int main()
{
    int n = 6, m = 28;
    checkFriendly(n, m) ? (cout << "Yes\n") :
                          (cout << "No\n");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if the given two number
// are friendly pair or not.
class GFG {

    // Returns sum of all factors of n.
    static int sumofFactors(int n)
    {

        // Traversing through all prime factors.
        int res = 1;
        for (int i = 2; i <= Math.sqrt(n); i++) {

            int count = 0, curr_sum = 1;
            int curr_term = 1;
            while (n % i == 0) {
                count++;

                // THE BELOW STATEMENT MAKES
                // IT BETTER THAN ABOVE METHOD
                // AS WE REDUCE VALUE OF n.
                n = n / i;

                curr_term *= i;
                curr_sum += curr_term;
            }

            res *= curr_sum;
        }

        // This condition is to handle
        // the case when n is a prime
        // number greater than 2.
        if (n >= 2)
            res *= (1 + n);

        return res;
    }

    // Function to return gcd of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    // Function to check if the given two
    // number are friendly pair or not.
    static boolean checkFriendly(int n, int m)
    {
        // Finding the sum of factors of n and m
        int sumFactors_n = sumofFactors(n);
        int sumFactors_m = sumofFactors(m);

        // finding gcd of n and sum of its factors.
        int gcd_n = gcd(n, sumFactors_n);

        // finding gcd of m and sum of its factors.
        int gcd_m = gcd(m, sumFactors_m);

        // checking is numerator and denominator of
        // abundancy index of both number are equal
        // or not.
        if (n / gcd_n == m / gcd_m &&
            sumFactors_n / gcd_n == sumFactors_m / gcd_m)
            return true;

        else
            return false;
    }

    //driver code
    public static void main (String[] args)
    {
        int n = 6, m = 28;

        if(checkFriendly(n, m))
            System.out.print("Yes\n");
        else
            System.out.print("No\n");
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Check if the given two number
# are friendly pair or not.
import math

# Returns sum of all factors of n.
def sumofFactors(n):

    # Traversing through all prime factors.
    res = 1
    for i in range(2, int(math.sqrt(n)) + 1):

        count = 0; curr_sum = 1; curr_term = 1
        while (n % i == 0):
            count += 1

            # THE BELOW STATEMENT MAKES
            # IT BETTER THAN ABOVE METHOD
            # AS WE REDUCE VALUE OF n.
            n = n // i

            curr_term *= i
            curr_sum += curr_term

        res *= curr_sum

    # This condition is to handle
    # the case when n is a prime
    # number greater than 2.
    if (n >= 2):
        res *= (1 + n)

    return res

# Function to return gcd of a and b
def gcd(a, b):

    if (a == 0):
        return b
    return gcd(b % a, a)

# Function to check if the given two
# number are friendly pair or not.
def checkFriendly(n, m):

    # Finding the sum of factors of n and m
    sumFactors_n = sumofFactors(n)
    sumFactors_m = sumofFactors(m)

    # Finding gcd of n and sum of its factors.
    gcd_n = gcd(n, sumFactors_n)

    # Finding gcd of m and sum of its factors.
    gcd_m = gcd(m, sumFactors_m)

    # checking is numerator and denominator 
    # of abundancy index of both number are
    # equal or not.
    if (n // gcd_n == m // gcd_m and
        sumFactors_n // gcd_n == sumFactors_m // gcd_m):
        return True

    else:
        return False

# Driver code
n = 6; m = 28
if(checkFriendly(n, m)):
    print("Yes")
else:
    print("No")

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# code to check if the
// given two number are
// friendly  pair or not
using System;

class GFG {

    // Returns sum of all
    //factors of n.
    static int sumofFactors(int n)
    {

        // Traversing through all
        // prime factors.
        int res = 1;
        for (int i = 2; i <= Math.Sqrt(n); i++)
        {

            int count = 0, curr_sum = 1;
            int curr_term = 1;
            while (n % i == 0)
            {
                count++;

                // THE BELOW STATEMENT MAKES
                // IT BETTER THAN ABOVE METHOD
                // AS WE REDUCE VALUE OF n.
                n = n / i;

                curr_term *= i;
                curr_sum += curr_term;
            }

            res *= curr_sum;
        }

        // This condition is to handle
        // the case when n is a prime
        // number greater than 2.
        if (n >= 2)
            res *= (1 + n);

        return res;
    }

    // Function to return gcd
    // of a and b
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    // Function to check if the
    // given two number are
    // friendly pair or not
    static bool checkFriendly(int n, int m)
    {
        // Finding the sum of factors
        // of n and m
        int sumFactors_n = sumofFactors(n);
        int sumFactors_m = sumofFactors(m);

        // finding gcd of n and
        // sum of its factors.
        int gcd_n = gcd(n, sumFactors_n);

        // finding gcd of m and sum
        // of its factors.
        int gcd_m = gcd(m, sumFactors_m);

        // checking is numerator and
        // denominator of abundancy
        // index of both number are
        // equal or not
        if (n / gcd_n == m / gcd_m &&
            sumFactors_n / gcd_n ==
            sumFactors_m / gcd_m)
            return true;

        else
            return false;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 6, m = 28;

        if(checkFriendly(n, m))
            Console.Write("Yes\n");
        else
            Console.Write("No\n");
    }
}

// This code is contributed by parshar...
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if the given
// two number are friendly pair or not.

// Returns sum of all factors of n.
function sumofFactors( $n)
{

    // Traversing through all
    // prime factors.
    $res = 1;
    for ($i = 2; $i <= sqrt($n); $i++)
    {

        $count = 0;
        $curr_sum = 1;
        $curr_term = 1;
        while ($n % $i == 0)
        {
            $count++;

            // THE BELOW STATEMENT MAKES
            // IT BETTER THAN ABOVE METHOD
            // AS WE REDUCE VALUE OF n.
            $n = $n / $i;

            $curr_term *= $i;
            $curr_sum += $curr_term;
        }

        $res *= $curr_sum;
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2.
    if ($n >= 2)
        $res *= (1 + $n);

    return $res;
}

// Function to return
// gcd of a and b
function gcd($a, $b)
{
    if ($a == 0)
        return $b;
    return gcd($b % $a, $a);
}

// Function to check if the given two
// number are friendly pair or not.
function checkFriendly($n, $m)
{

    // Finding the sum of
    // factors of n and m
    $sumFactors_n = sumofFactors($n);
    $sumFactors_m = sumofFactors($m);

    // finding gcd of n and
    // sum of its factors.
    $gcd_n = gcd($n, $sumFactors_n);

    // finding gcd of m and
    // sum of its factors.
    $gcd_m = gcd($m, $sumFactors_m);

    // checking is numerator
    // and denominator of
    // abundancy index of
    // both number are equal
    // or not.
    if ($n / $gcd_n == $m / $gcd_m and
        $sumFactors_n / $gcd_n ==
        $sumFactors_m / $gcd_m)
        return true;

    else
        return false;
}

    // Driver code
    $n = 6;
    $m = 28;
    if(checkFriendly($n, $m))
        echo "Yes" ;
    else
        echo "No";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to check if the given two number
// are friendly pair or not.

    // Returns sum of all factors of n.
    function sumofFactors(n)
    {

        // Traversing through all prime factors.
        let res = 1;
        for (let i = 2; i <= Math.sqrt(n); i++) {

            let count = 0, curr_sum = 1;
            let curr_term = 1;
            while (n % i == 0) {
                count++;

                // THE BELOW STATEMENT MAKES
                // IT BETTER THAN ABOVE METHOD
                // AS WE REDUCE VALUE OF n.
                n = n / i;

                curr_term *= i;
                curr_sum += curr_term;
            }

            res *= curr_sum;
        }

        // This condition is to handle
        // the case when n is a prime
        // number greater than 2.
        if (n >= 2)
            res *= (1 + n);

        return res;
    }

    // Function to return gcd of a and b
    function gcd(a, b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    // Function to check if the given two
    // number are friendly pair or not.
    function checkFriendly(n, m)
    {
        // Finding the sum of factors of n and m
        let sumFactors_n = sumofFactors(n);
        let sumFactors_m = sumofFactors(m);

        // finding gcd of n and sum of its factors.
        let gcd_n = gcd(n, sumFactors_n);

        // finding gcd of m and sum of its factors.
        let gcd_m = gcd(m, sumFactors_m);

        // checking is numerator and denominator of
        // abundancy index of both number are equal
        // or not.
        if (n / gcd_n == m / gcd_m &&
            sumFactors_n / gcd_n == sumFactors_m / gcd_m)
            return true;

        else
            return false;
    }

// Driver Code

        let n = 6, m = 28;
        if(checkFriendly(n, m))
            document.write("Yes\n");
        else
            document.write("No\n");

// This code is contributed by avijitmondal1998.
</script>
```

**输出**T2】

```
Yes
```