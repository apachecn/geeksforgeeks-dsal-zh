# 恶作剧号码

> 原文:[https://www.geeksforgeeks.org/hoax-number/](https://www.geeksforgeeks.org/hoax-number/)

给定一个数字“n”，检查它是否是一个骗局数字。
一个**骗局数字**被定义为一个复合数字，其位数之和等于其不同质因数的位数之和。这里可以注意到，1 不被认为是质数，因此它不包括在不同质因数的数字总和中。
**示例:**

```
Input : 22
Output : A Hoax Number
Explanation : The distinct prime factors of 22 
are 2 and 11\. The sum of their digits are 4, 
i.e 2 + 1 + 1 and sum of digits of 22 is also 4.

Input : 84
Output : A Hoax Number
Explanation : The distinct prime factors of 84 
are 2, 3 and 7\. The sum of their digits are 12, 
i.e 2 + 3 + 4 and sum of digits of 84 is also 12.

Input : 19
Output : Not a Hoax Number
Explanation : By definition, a hoax number is 
a composite number.
```

骗局数字的定义与[史密斯数字](https://www.geeksforgeeks.org/smith-number/)的定义非常相似。事实上，一些恶作剧数字也是史密斯数字。很明显，那些在素数分解中没有重复因子的骗局数字，即[平方自由数](https://www.geeksforgeeks.org/square-free-number/)也是合格的史密斯数。
**实现**
**1)** 首先生成数字‘n’的所有不同质因数。
**2)** 如果‘n’不是素数，求第 1 步得到的因子的位数之和。
**(3)**求‘n’位数之和。
**(4)**检查步骤 2 和 3 得到的和是否相等。
**5)** 如果总和相等，‘n’就是一个骗局数字。

## C++

```
// CPP code to check if a number is a hoax
// number or not.
#include <bits/stdc++.h>
using namespace std;
// Function to find distinct prime factors
// of given number n
vector<int> primeFactors(int n)
{
    vector<int> res;
    if (n % 2 == 0) {
        while (n % 2 == 0)
            n = n / 2;
        res.push_back(2);
    }

    // n is odd at this point, since it is no
    // longer divisible by 2\. So we can test
    // only for the odd numbers, whether they
    // are factors of n
    for (int i = 3; i <= sqrt(n); i = i + 2) {

        // Check if i is prime factor
        if (n % i == 0) {
            while (n % i == 0)
                n = n / i;
            res.push_back(i);
        }
    }

    // This condition is to handle the case
    // when n is a prime number greater than 2
    if (n > 2)
        res.push_back(n);
    return res;
}

// Function to calculate sum of digits of
// distinct prime factors of given number n
// and sum of digits of number n and compare
// the sums obtained
bool isHoax(int n)
{
    // Distinct prime factors of n are being
    // stored in vector pf
    vector<int> pf = primeFactors(n);

    // If n is a prime number, it cannot be a
    // hoax number
    if (pf[0] == n)
        return false;

    // Finding sum of digits of distinct prime
    // factors of the number n
    int all_pf_sum = 0;   
    for (int i = 0; i < pf.size(); i++) {

        // Finding sum of digits in current
        // prime factor pf[i].
        int pf_sum;
        for (pf_sum = 0; pf[i] > 0;
             pf_sum += pf[i] % 10, pf[i] /= 10)
            ;

        all_pf_sum += pf_sum;
    }

    // Finding sum of digits of number n
    int sum_n;
    for (sum_n = 0; n > 0; sum_n += n % 10,
                                  n /= 10)
        ;

    // Comparing the two calculated sums
    return sum_n == all_pf_sum;
}

// Driver Method
int main()
{
    int n = 84;
    if (isHoax(n))
        cout << "A Hoax Number\n";
    else
        cout << "Not a Hoax Number\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if a number is
// a hoax number or not.
import java.io.*;
import java.util.*;

public class GFG {

    // Function to find distinct
    // prime factors of given
    // number n
    static List<Integer> primeFactors(int n)
    {
        List<Integer> res = new ArrayList<Integer>();
        if (n % 2 == 0)
        {
            while (n % 2 == 0)
                n = n / 2;
            res.add(2);
        }

        // n is odd at this point,
        // since it is no longer
        // divisible by 2\. So we
        // can test only for the
        // odd numbers, whether they
        // are factors of n
        for (int i = 3; i <= Math.sqrt(n);
                                i = i + 2)
        {

            // Check if i is prime factor
            if (n % i == 0)
            {
                while (n % i == 0)
                    n = n / i;
                res.add(i);
            }
        }

        // This condition is to
        // handle the case when
        // n is a prime number
        // greater than 2
        if (n > 2)
            res.add(n);
        return res;
    }

    // Function to calculate
    // sum of digits of distinct
    // prime factors of given
    // number n and sum of
    // digits of number n and
    // compare the sums obtained
    static boolean isHoax(int n)
    {

        // Distinct prime factors
        // of n are being
        // stored in vector pf
        List<Integer> pf = primeFactors(n);

        // If n is a prime number,
        // it cannot be a hoax number
        if (pf.get(0) == n)
            return false;

        // Finding sum of digits of distinct
        // prime factors of the number n
        int all_pf_sum = 0;
        for (int i = 0; i < pf.size(); i++)
        {

            // Finding sum of digits in current
            // prime factor pf[i].
            int pf_sum;
            for (pf_sum = 0; pf.get(i) > 0;
                pf_sum += pf.get(i) % 10,
                   pf.set(i,pf.get(i) / 10));

            all_pf_sum += pf_sum;
        }

        // Finding sum of digits of number n
        int sum_n;
        for (sum_n = 0; n > 0; sum_n += n % 10,
                                    n /= 10)
            ;

        // Comparing the two calculated sums
        return sum_n == all_pf_sum;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 84;
        if (isHoax(n))
            System.out.print( "A Hoax Number\n");
        else
            System.out.print("Not a Hoax Number\n");
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 蟒蛇 3

```
# Python3 code to check if a number is a hoax
# number or not.
import math

# Function to find distinct prime factors
# of given number n
def primeFactors(n) :
    res = []
    if (n % 2 == 0) :
        while (n % 2 == 0) :
            n = int(n / 2)
        res.append(2)

    # n is odd at this point, since it is no
    # longer divisible by 2\. So we can test
    # only for the odd numbers, whether they
    # are factors of n
    for i in range(3,int(math.sqrt(n)),2):
        # Check if i is prime factor
        if (n % i == 0) :
            while (n % i == 0) :
                n = int(n / i)
            res.append(i)

    # This condition is to handle the case
    # when n is a prime number greater than 2
    if (n > 2) :
        res.append(n)
    return res

# Function to calculate sum of digits of
# distinct prime factors of given number n
# and sum of digits of number n and compare
# the sums obtained
def isHoax(n) :
    # Distinct prime factors of n are being
    # stored in vector pf
    pf = primeFactors(n)

    # If n is a prime number, it cannot be a
    # hoax number
    if (pf[0] == n) :
        return False

    # Finding sum of digits of distinct prime
    # factors of the number n
    all_pf_sum = 0
    for i in range(0,len(pf)):

        # Finding sum of digits in current
        # prime factor pf[i].
        pf_sum = 0
        while (pf[i] > 0):
            pf_sum += pf[i] % 10
            pf[i] = int(pf[i] / 10)

        all_pf_sum += pf_sum

    # Finding sum of digits of number n
    sum_n = 0;
    while (n > 0):
        sum_n += n % 10
        n = int(n / 10)

    # Comparing the two calculated sums
    return sum_n == all_pf_sum

# Driver Method
n = 84;
if (isHoax(n)):
    print ("A Hoax Number\n")
else:
    print ("Not a Hoax Number\n")

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# code to check if a number is
// a hoax number or not.
using System;
using System.Collections.Generic;

class GFG {

    // Function to find distinct
    // prime factors of given
    // number n
    static List<int> primeFactors(int n)
    {
        List<int> res = new List<int>();
        if (n % 2 == 0)
        {
            while (n % 2 == 0)
                n = n / 2;
            res.Add(2);
        }

        // n is odd at this point,
        // since it is no longer
        // divisible by 2\. So we
        // can test only for the
        // odd numbers, whether they
        // are factors of n
        for (int i = 3; i <= Math.Sqrt(n);
                                i = i + 2)
        {

            // Check if i is prime factor
            if (n % i == 0)
            {
                while (n % i == 0)
                    n = n / i;
                res.Add(i);
            }
        }

        // This condition is to
        // handle the case when
        // n is a prime number
        // greater than 2
        if (n > 2)
            res.Add(n);
        return res;
    }

    // Function to calculate
    // sum of digits of distinct
    // prime factors of given
    // number n and sum of
    // digits of number n and
    // compare the sums obtained
    static bool isHoax(int n)
    {

        // Distinct prime factors
        // of n are being
        // stored in vector pf
        List<int> pf = primeFactors(n);

        // If n is a prime number,
        // it cannot be a hoax number
        if (pf[0] == n)
            return false;

        // Finding sum of digits of distinct
        // prime factors of the number n
        int all_pf_sum = 0;
        for (int i = 0; i < pf.Count; i++)
        {

            // Finding sum of digits in current
            // prime factor pf[i].
            int pf_sum;
            for (pf_sum = 0; pf[i] > 0;
                pf_sum += pf[i] % 10, pf[i] /= 10);

            all_pf_sum += pf_sum;
        }

        // Finding sum of digits of number n
        int sum_n;
        for (sum_n = 0; n > 0; sum_n += n % 10,
                                     n /= 10)
            ;

        // Comparing the two calculated sums
        return sum_n == all_pf_sum;
    }

    // Driver Code
    public static void Main()
    {
        int n = 84;
        if (isHoax(n))
            Console.Write( "A Hoax Number\n");
        else
            Console.Write("Not a Hoax Number\n");
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check if a number
// is a hoax number or not.

// Function to find distinct prime
// factors of given number n
function primeFactors($n)
{
    $res = array();
    if ($n % 2 == 0)
    {
        while ($n % 2 == 0)
            $n = (int)$n / 2;
        array_push($res, 2);
    }

    // n is odd at this point, since
    // it is no longer divisible by 2.
    // So we can test only for the odd
    // numbers, whether they are factors of n
    for ($i = 3; $i <= sqrt($n); $i = $i + 2)
    {

        // Check if i is prime factor
        if ($n % $i == 0)
        {
            while ($n % $i == 0)
                $n = (int)$n / $i;
            array_push($res, $i);
        }
    }

    // This condition is to handle
    // the case when n is a prime
    // number greater than 2
    if ($n > 2)
        array_push($res, $n);
    return $res;
}

// Function to calculate sum
// of digits of distinct prime
// factors of given number n
// and sum of digits of number
// n and compare the sums obtained
function isHoax($n)
{
    // Distinct prime factors
    // of n are being stored
    // in vector pf
    $pf = primeFactors($n);

    // If n is a prime number,
    // it cannot be a hoax number
    if ($pf[0] == $n)
        return false;

    // Finding sum of digits of distinct
    // prime factors of the number n
    $all_pf_sum = 0;
    for ($i = 0; $i < count($pf); $i++)
    {

        // Finding sum of digits in
        // current prime factor pf[i].
        $pf_sum;
        for ($pf_sum = 0; $pf[$i] > 0;
              $pf_sum += $pf[$i] % 10,
                       $pf[$i] /= 10)
            ;

        $all_pf_sum += $pf_sum;
    }

    // Finding sum of digits of number n
    for ($sum_n = 0; $n > 0;
          $sum_n += $n % 10, $n /= 10)
        ;

    // Comparing the two calculated sums
    return $sum_n == $all_pf_sum;
}

// Driver Code
$n = 84;
if (isHoax($n))
    echo ("A Hoax Number\n");
else
    echo ("Not a Hoax Number\n");

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript code to check if a number is a hoax
// number or not.

// Function to find distinct prime factors
// of given number n
function primeFactors(n)
{
    var res =[];
    if (n % 2 == 0) {
        while (n % 2 == 0)
            n = parseInt(n / 2);
        res.push(2);
    }

    // n is odd at this point, since it is no
    // longer divisible by 2\. So we can test
    // only for the odd numbers, whether they
    // are factors of n
    for (var i = 3; i <= Math.sqrt(n); i = i + 2) {

        // Check if i is prime factor
        if (n % i == 0) {
            while (n % i == 0)
                n = parseInt(n / i);
            res.push(i);
        }
    }

    // This condition is to handle the case
    // when n is a prime number greater than 2
    if (n > 2)
        res.push(n);
    return res;
}

// Function to calculate sum of digits of
// distinct prime factors of given number n
// and sum of digits of number n and compare
// the sums obtained
function isHoax(n)
{
    // Distinct prime factors of n are being
    // stored in vector pf
    var pf = primeFactors(n);

    // If n is a prime number, it cannot be a
    // hoax number
    if (pf[0] == n)
        return false;

    // Finding sum of digits of distinct prime
    // factors of the number n
    var all_pf_sum = 0;   
    for (var i = 0; i < pf.length; i++) {

        // Finding sum of digits in current
        // prime factor pf[i].
        var pf_sum;
        for (pf_sum = 0; pf[i] > 0;
             pf_sum += pf[i] % 10, pf[i] = parseInt(pf[i]/10))
            ;

        all_pf_sum += pf_sum;
    }

    // Finding sum of digits of number n
    var sum_n;
    for (sum_n = 0; n > 0; sum_n += n % 10,
                                  n = parseInt(n/10))
        ;

    // Comparing the two calculated sums
    return sum_n == all_pf_sum;
}

// Driver Method
var n = 84;
if (isHoax(n))
    document.write( "A Hoax Number");
else
    document.write( "Not a Hoax Number");

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
A Hoax Number
```