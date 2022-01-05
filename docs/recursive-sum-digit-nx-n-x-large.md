# n^x 数字的递归和，其中 n 和 x 非常大

> 原文:[https://www . geesforgeks . org/recursive-sum-digit-NX-n-x-large/](https://www.geeksforgeeks.org/recursive-sum-digit-nx-n-x-large/)

给定非常大的数字 n 和 x，我们需要找到 n^x 数的和，例如:

```
If n^x < 10    
    digSum(n^x) = n^x
Else         
    digSum(n^x) = Sum(digSum(n^x))
```

示例:

```
Input :  5  4
Output :  4
We know 54 = 625
Sum of digits in 625 = 6 + 2 + 5 = 13
Sum of digits in 13 = 1 + 3 = 4

Input :  546878 56422
Output :  7
```

先决条件:[数字的递归和](https://www.geeksforgeeks.org/finding-sum-of-digits-of-a-number-until-sum-becomes-single-digit/)。
想法是:
每 6 个指数后重复的位数总和。
让 SoD(n) = a
让 b = x % 6
然后
SoD(n^x) = SoD(a^b)除了当 a = 3&6
sod(n^x = 9 for all x>1，当 a = 3 & 6
时

## C++

```
// CPP Code for Sum of
// digit of n^x where
// n and x are very large
#include <bits/stdc++.h>
using namespace std;

// function to get sum
// of digits of a number
     long digSum(long n)
    {
        if (n == 0)
            return 0;
        return (n % 9 == 0)
                ? 9 : (n % 9);
    }

    // function to return sum
     long PowDigSum(long n, long x)
    {

        // Find sum of digits in n
        long sum = digSum(n);

        // Find remainder of exponent
        long rem = x % 6;

        if ((sum == 3 || sum == 6)
                         && x > 1)
            return 9;

        else if (x == 1)
             return sum;

        else if (x == 0)
             return 1;

        else if (rem == 0)
             return digSum((long)pow(sum, 6));

        else
            return digSum((long)pow(sum, rem));
    }

// Driver code
int main()
{
   int n = 33333;
   int x = 332654;
   cout << PowDigSum(n, x);
    return 0;
}

// This code is contributed by Gitanjali.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code for
// Sum of digit of
// n^x where n and
// x are very large
import java.util.*;

class GFG {

    // function to get sum
    // of digits of a number
    static long digSum(long n)
    {
        if (n == 0)
            return 0;
        return (n % 9 == 0) ? 9 : (n % 9);
    }

    // function to return sum
    static long PowDigSum(long n, long x)
    {
        // Find sum of digits in n
        long sum = digSum(n);

        // Find remainder of exponent
        long rem = x % 6;

        if ((sum == 3 || sum == 6) && x > 1)
            return 9;

        else if (x == 1)
            return sum;

        else if (x == 0)
            return 1;

        else if (rem == 0)
            return digSum((long)Math.pow(sum, 6));

        else
            return digSum((long)Math.pow(sum, rem));
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {

        int n = 33333;
        int x = 332654;

        System.out.println(PowDigSum(n, x));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 Code for Sum
# of digit of n^x
import math

# function to get
# sum of digits of
# a number
def digSum(n):
    if (n == 0):
        return 0
    if n % 9==0 :
        return 9
    else:
        return (n % 9)

# function to return sum
def PowDigSum(n, x):
    # Find sum of
    # digits in n
    sum = digSum(n)

    # Find remainder
    # of exponent
    rem = x % 6

    if ((sum == 3 or sum == 6) and x > 1):
            return 9

    elif (x == 1):
            return sum

    elif (x == 0):
            return 1

    elif (rem == 0):
        return digSum(math.pow(sum, 6))

    else:
        return digSum(math.pow(sum, rem))

# Driver method
n = 33333
x = 332654
print (PowDigSum(n, x))

# This code is contributed by Gitanjali
```

## C#

```
// C# Code for Sum of digit of
// n^x where n and x are very large
using System;

class GFG {

    // Function to get sum
    // of digits of a number
    static long digSum(long n)
    {
        if (n == 0)
            return 0;
        return (n % 9 == 0) ? 9 : (n % 9);
    }

    // Function to return sum
    static long PowDigSum(long n, long x)
    {
        // Find sum of digits in n
        long sum = digSum(n);

        // Find remainder of exponent
        long rem = x % 6;

        if ((sum == 3 || sum == 6) && x > 1)
            return 9;

        else if (x == 1)
            return sum;

        else if (x == 0)
            return 1;

        else if (rem == 0)
            return digSum((long)Math.Pow(sum, 6));

        else
            return digSum((long)Math.Pow(sum, rem));
    }

    // Driver Code
    public static void Main()
    {
        int n = 33333;
        int x = 332654;

        Console.WriteLine(PowDigSum(n, x));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Code for Sum of
// digit of n^x where
// function to get sum
// of digits of a number

function digSum($n)
    {
        if ($n == 0)
            return 0;
        return ($n % 9 == 0)
                ? 9 : ($n % 9);
    }

    // function to return sum
    function PowDigSum($n, $x)
    {

        // Find sum of digits in n
        $sum = digSum($n);

        // Find remainder of exponent
        $rem = $x % 6;

        if (($sum == 3 || $sum == 6)
                        && $x > 1)
            return 9;

        else if ($x == 1)
            return $sum;

        else if ($x == 0)
            return 1;

        else if ($rem == 0)
            return digSum(pow($sum, 6));

        else
            return digSum(pow($sum, $rem));
    }

    // Driver code
    $n = 33333;
    $x = 332654;
    echo PowDigSum($n, $x);

// This code is contributed by aj_36.
?>
```

## java 描述语言

```
<script>

// JavaScript Code for Sum of
// digit of n^x where
// n and x are very large

// function to get sum
// of digits of a number
     function digSum(n)
    {
        if (n == 0)
            return 0;
        return (n % 9 == 0)
                ? 9 : (n % 9);
    }

    // function to return sum
     function PowDigSum(n, x)
    {

        // Find sum of digits in n
        let sum = digSum(n);

        // Find remainder of exponent
        let rem = x % 6;

        if ((sum == 3 || sum == 6)
                         && x > 1)
            return 9;

        else if (x == 1)
             return sum;

        else if (x == 0)
             return 1;

        else if (rem == 0)
             return digSum(Math.pow(sum, 6));

        else
            return digSum(Math.pow(sum, rem));
    }

// Driver code
let n = 33333;
let x = 332654;
document.write(PowDigSum(n, x));

</script>
```

**输出:**

```
9
```