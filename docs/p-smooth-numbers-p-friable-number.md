# 平滑数字或易碎数字

> 原文:[https://www . geesforgeks . org/p-smooth-numbers-p-fraible-number/](https://www.geeksforgeeks.org/p-smooth-numbers-p-friable-number/)

a**P-光滑数**或**P-脆性数**是一个最大质因数小于或等于 P 的整数，给定 N 和 P，我们需要编写一个程序来检查它是否 P-脆性。
示例:

```
Input : N = 24   ,  P = 7  
Output : YES
Explanation : The prime divisors of 24 are 2 and 3 only. 
              Hence its largest prime factor is 3 which 
              is less than or equal to 7, it is P-friable. 

Input : N = 22   ,  P = 5 
Output : NO
Explanation : The prime divisors are 11 and 2, hence 11>5,
              so it is not a P-friable number. 
```

方法是[质因数分解数字](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)并存储所有质因数的最大值。如果一个数可以被整除，我们首先把它除以 2，然后从 3 迭代到 Sqrt(n)，得到一个素数除以一个特定数的次数，这个特定数每次减少 n/i，如果它除以 n，就存储质因数 I，我们把我们的数 n 除以它对应的最小质因数，直到 n 变成 1。如果在 n > 2 的末尾，它意味着它是一个质数，所以我们也把它存储为质因数。最后将最大因子与 p 进行比较，检查它是否为 p 光滑数。

## C++

```
// CPP program to check if a number is
// a p-smooth number or not
#include <iostream>
#include<math.h>
using namespace std;

// function to check if number n
// is a P-smooth number or not
bool check(int n, int p)
{
    int maximum = -1;

    // prime factorise it by 2
    while (!(n % 2))
    {
        // if the number is divisible by 2
        maximum = max(maximum, 2);
        n = n/2;
    }

    // check for all the possible numbers
    // that can divide it
    for (int i = 3; i <= sqrt(n); i += 2)
    {
        // prime factorize it by i
        while (n % i == 0)
        {  
            // stores the maximum if maximum
            // and i, if i divides the number
            maximum = max(maximum,i);
            n = n / i;
        }
    }

    // if n at the end is a prime number,
    // then it a divisor itself
    if (n > 2)
        maximum = max(maximum, n);

    return (maximum <= p);
}

// Driver program to test above function
int main()
{
    int n = 24, p = 7;

    if (check(n, p))
        cout << "yes";
    else
        cout << "no";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number is
// a p-smooth number or not

import java.lang.*;

class GFG{

// function to check if number n
// is a P-smooth number or not

static boolean check(int n, int p)
{
    int maximum = -1;

    // prime factorise it by 2
    while ((n % 2) == 0)
    {
        // if the number is divisible by 2
        maximum = Math.max(maximum, 2);
        n = n/2;
    }

    // check for all the possible numbers
    // that can divide it
    for (int i = 3; i <= Math.sqrt(n); i += 2)
    {
        // prime factorize it by i
        while (n % i == 0)
        {
            // stores the maximum if maximum
            // and i, if i divides the number
            maximum = Math.max(maximum,i);
            n = n / i;
        }
    }

    // if n at the end is a prime number,
    // then it a divisor itself
    if (n > 2)
        maximum = Math.max(maximum, n);

    return (maximum <= p);
}

// Driver program to test
// above function
public static void main(String[] args)
{
    int n = 24, p = 7;

    if (check(n, p))
        System.out.println("yes");
    else
        System.out.println("no");

}
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python 3 program to
# check if a number is
# a p-smooth number or not

import math

# function to check if number n
# is a P-smooth number or not
def check(n, p) :

    maximum = -1

    # prime factorise it by 2
    while (not(n % 2)):

        # if the number is divisible by 2
        maximum = max(maximum, 2)
        n = int(n/2)

    # check for all the possible numbers
    # that can divide it
    for i in range(3,int(math.sqrt(n)), 2):

        # prime factorize it by i
        while (n % i == 0) :

            # stores the maximum if maximum
            # and i, if i divides the number
            maximum = max(maximum,i)
            n = int(n / i)

    # if n at the end is a prime number,
    # then it a divisor itself
    if (n > 2):
        maximum = max(maximum, n)

    return (maximum <= p)

# Driver program to test above function
n = 24
p = 7
if (check(n, p)):
    print( "yes" )
else:
    print( "no" )

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to check if a number is
// a p-smooth number or not
using System;

class GFG {

    // function to check if number n
    // is a P-smooth number or not

    static bool check(int n, int p)
    {
        int maximum = -1;

        // prime factorise it by 2
        while ((n % 2) == 0)
        {
            // if the number is divisible by 2
            maximum = Math.Max(maximum, 2);
            n = n / 2;
        }

        // check for all the possible numbers
        // that can divide it
        for (int i = 3; i <= Math.Sqrt(n); i += 2)
        {
            // prime factorize it by i
            while (n % i == 0)
            {
                // stores the maximum if maximum
                // and i, if i divides the number
                maximum = Math.Max(maximum, i);
                n = n / i;
            }
        }

        // if n at the end is a prime number,
        // then it a divisor itself
        if (n > 2)
            maximum = Math.Max(maximum, n);

        return (maximum <= p);
    }

    // Driver program to test
    // above function
    public static void Main()
    {
        int n = 24, p = 7;

        if (check(n, p))
            Console.Write("yes");
        else
            Console.Write("no");

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number is
// a p-smooth number or not

// function to check if number n
// is a P-smooth number or not
function check($n, $p)
{
    $maximum = -1;

    // prime factorise it by 2
    while (!($n % 2))
    {
        // if the number is
        // divisible by 2
        $maximum = max($maximum, 2);
        $n = $n / 2;
    }

    // check for all the possible
    // numbers that can divide it
    for ($i = 3; $i <= sqrt($n); $i += 2)
    {

        // prime factorize it by i
        while ($n % $i == 0)
        {
            // stores the maximum if maximum
            // and i, if i divides the number
            $maximum = max($maximum, $i);
            $n = $n / $i;
        }
    }

    // if n at the end is a prime number,
    // then it a divisor itself
    if ($n > 2)
        $maximum = max($maximum, $n);

    return ($maximum <= $p);
}

// Driver Code
$n = 24; $p = 7;

if (check($n, $p))
    echo("yes");
else
    echo("no");

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to check if a number is
// a p-smooth number or not

    // function to check if number n
    // is a P-smooth number or not
    function check(n, p)
    {
        let maximum = -1;

        // prime factorise it by 2
        while (!(n % 2))
        {

            // if the number is divisible by 2
            maximum = Math.max(maximum, 2)
            n = n/2;
        }

        // check for all the possible numbers
        // that can divide it
        var i;
        for (i = 3; i*i <= n; i += 2)
        {

            // prime factorize it by i
            while (n % i == 0)
            {  

                // stores the maximum if maximum
                // and i, if i divides the number
                maximum = Math.max(maximum, i);
                n = n / i;
            }
        }

        // if n at the end is a prime number,
        // then it a divisor itself
        if (n > 2)
            maximum = Math.max(maximum, n);

        if (maximum <= p)
            return true;
        else
            return false;
    }

    // Driver Code
    let n = 24, p = 7;
    if (check(n, p))
        document.write("yes");
    else
        document.write("no");

    // This code is contributed by ajaykrsharma132.
</script>
```

输出:

```
yes
```

**参考**:
T3】http://oeis.org/wiki/P-smooth_numbersT5】