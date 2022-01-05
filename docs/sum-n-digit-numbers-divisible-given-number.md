# 可被给定数字整除的 n 位数之和

> 原文:[https://www . geesforgeks . org/sum-n 位数-可除数-给定数/](https://www.geeksforgeeks.org/sum-n-digit-numbers-divisible-given-number/)

给定 n 和一个数，任务是找出能被给定数整除的 n 位数的和。

示例:

```
Input : n = 2, number = 7
Output : 728
There are thirteen n digit numbers that are divisible by 7.
 Numbers are  : 14+ 21 + 28 + 35 + 42 + 49 + 56 + 63 +70 + 77 + 84 + 91 + 98.

Input : n = 3, number = 7
Output : 70336

Input : n = 3, number = 4
Output : 124200

```

**原生方式:**遍历所有 n 位数。对于每个数字，检查可除性，然后求和。

## C++

```
// Simple CPP program to sum of n digit
// divisible numbers.
#include <cmath>
#include <iostream>
using namespace std;

// Returns sum of n digit numbers
// divisible by 'number'
int totalSumDivisibleByNum(int n, int number)
{
    // compute the first and last term
    int firstnum = pow(10, n - 1);
    int lastnum = pow(10, n);

    // sum of number which having
    // n digit and divisible by number
    int sum = 0;
    for (int i = firstnum; i < lastnum; i++)
        if (i % number == 0)
            sum += i;
    return sum;
}

// Driver code
int main()
{
    int n = 3, num = 7;
    cout << totalSumDivisibleByNum(n, num) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Simple Java program to sum of n digit
// divisible numbers.
import java.io.*;

class GFG {

    // Returns sum of n digit numbers
    // divisible by 'number'
    static int totalSumDivisibleByNum(int n, int number)
    {
        // compute the first and last term
        int firstnum = (int)Math.pow(10, n - 1);
        int lastnum = (int)Math.pow(10, n);

        // sum of number which having
        // n digit and divisible by number
        int sum = 0;
        for (int i = firstnum; i < lastnum; i++)
            if (i % number == 0)
                sum += i;
        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 3, num = 7;
        System.out.println(totalSumDivisibleByNum(n, num));
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Simple Python 3 program to sum 
# of n digit divisible numbers.

# Returns sum of n digit numbers
# divisible by 'number'
def totalSumDivisibleByNum(n, number):

    # compute the first and last term
    firstnum = pow(10, n - 1)
    lastnum = pow(10, n)

    # sum of number which having
    # n digit and divisible by number
    sum = 0
    for i in range(firstnum, lastnum):
        if (i % number == 0):
            sum += i
    return sum

# Driver code
n = 3; num = 7
print(totalSumDivisibleByNum(n, num))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// Simple C# program to sum of n digit
// divisible numbers.
using System;

class GFG {

    // Returns sum of n digit numbers
    // divisible by 'number'
    static int totalSumDivisibleByNum(int n, int number)
    {

        // compute the first and last term
        int firstnum = (int)Math.Pow(10, n - 1);
        int lastnum = (int)Math.Pow(10, n);

        // sum of number which having
        // n digit and divisible by number
        int sum = 0;

        for (int i = firstnum; i < lastnum; i++)
            if (i % number == 0)
                sum += i;

        return sum;
    }

    // Driver code
    public static void Main ()
    {
        int n = 3, num = 7;

        Console.WriteLine(totalSumDivisibleByNum(n, num));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to sum of
// n digit divisible numbers.

// Returns sum of n digit numbers
// divisible by 'number'
function totalSumDivisibleByNum($n, $number)
{

    // compute the first and last term
    $firstnum = pow(10, $n - 1);
    $lastnum = pow(10, $n);

    // sum of number which having
    // n digit and divisible by number
    $sum = 0;
    for ($i = $firstnum; $i < $lastnum; $i++)
        if ($i % $number == 0)
            $sum += $i;
    return $sum;
}

    // Driver code
    $n = 3;$num = 7;
    echo totalSumDivisibleByNum($n, $num) , "\n";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program to sum of n digit
// divisible numbers.

// Returns sum of n digit numbers
// divisible by 'number'
function totalSumDivisibleByNum(n, number)
{

    // compute the first and last term
    let firstnum = Math.pow(10, n - 1);
    let lastnum = Math.pow(10, n);

    // sum of number which having
    // n digit and divisible by number
    let sum = 0;
    for(let i = firstnum; i < lastnum; i++)
        if (i % number == 0)
            sum += i;

    return sum;
}

// Driver Code
let n = 3, num = 7;

document.write(totalSumDivisibleByNum(n, num));

// This code is contributed by chinmoy1997pal

</script>
```

**Output:** 

```
70336
```

**高效方法:**
首先，找出能被给定数整除的 n 位数[个数。然后应用](https://www.geeksforgeeks.org/count-n-digit-numbers-divisible-by-given-number/)[公式计算 AP](https://www.geeksforgeeks.org/program-sum-arithmetic-series/) 之和。

```
    count/2  * (first-term + last-term)
```

## C++

```
// Efficient CPP program to find the sum
// divisible numbers.
#include <cmath>
#include <iostream>
using namespace std;

// find the Sum of having n digit and
// divisible by the number
int totalSumDivisibleByNum(int digit,
                           int number)
{
    // compute the first and last term
    int firstnum = pow(10, digit - 1);
    int lastnum = pow(10, digit);

    // first number which is divisible
    // by given number
    firstnum = (firstnum - firstnum % number)
                                   + number;

    // last number which is divisible
    // by given number
    lastnum = (lastnum - lastnum % number);

    // total divisible number
    int count = ((lastnum - firstnum) /
                               number + 1);

    // return the total sum
    return ((lastnum + firstnum) * count) / 2;
}

int main()
{
    int n = 3, number = 7;
    cout << totalSumDivisibleByNum(n, number);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find the sum
// divisible numbers.
import java.io.*;

class GFG {

    // find the Sum of having n digit and
    // divisible by the number
    static int totalSumDivisibleByNum(int digit,
                                      int number)
    {
        // compute the first and last term
        int firstnum = (int)Math.pow(10, digit - 1);
        int lastnum = (int)Math.pow(10, digit);

        // first number which is divisible
        // by given number
        firstnum = (firstnum - firstnum % number)
                   + number;

        // last number which is divisible
        // by given number
        lastnum = (lastnum - lastnum % number);

        // total divisible number
        int count = ((lastnum - firstnum) /
                                number + 1);

        // return the total sum
        return ((lastnum + firstnum) * count) / 2;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 3, number = 7;
        System.out.println(totalSumDivisibleByNum(n, number));
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Efficient Python3 program to 
# find the sum divisible numbers.

# find the Sum of having n digit
# and divisible by the number
def totalSumDivisibleByNum(digit, number):

    # compute the first and last term
    firstnum = pow(10, digit - 1)
    lastnum = pow(10, digit)

    # first number which is divisible
    # by given number
    firstnum = (firstnum - firstnum % number) + number

    # last number which is divisible
    # by given number
    lastnum = (lastnum - lastnum % number)

    # total divisible number
    count = ((lastnum - firstnum) / number + 1)

    # return the total sum
    return int(((lastnum + firstnum) * count) / 2)

# Driver code
digit = 3; num = 7
print(totalSumDivisibleByNum(digit, num))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// Efficient Java program to find the sum
// divisible numbers.
using System;

class GFG {

    // find the Sum of having n digit and
    // divisible by the number
    static int totalSumDivisibleByNum(int digit,
                                    int number)
    {

        // compute the first and last term
        int firstnum = (int)Math.Pow(10, digit - 1);
        int lastnum = (int)Math.Pow(10, digit);

        // first number which is divisible
        // by given number
        firstnum = (firstnum - firstnum % number)
                + number;

        // last number which is divisible
        // by given number
        lastnum = (lastnum - lastnum % number);

        // total divisible number
        int count = ((lastnum - firstnum) /
                                number + 1);

        // return the total sum
        return ((lastnum + firstnum) * count) / 2;
    }

    // Driver code
    public static void Main ()
    {
        int n = 3, number = 7;

        Console.WriteLine(totalSumDivisibleByNum(n, number));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to find
// the sum divisible numbers.

// find the Sum of having n digit and
// divisible by the number
function totalSumDivisibleByNum($digit,
                                $number)
{

    // compute the first and last term
    $firstnum = pow(10, $digit - 1);
    $lastnum = pow(10, $digit);

    // first number which is divisible
    // by given number
    $firstnum = ($firstnum - $firstnum % $number)
                                       + $number;

    // last number which is divisible
    // by given number
    $lastnum = ($lastnum - $lastnum % $number);

    // total divisible number
    $count = (($lastnum - $firstnum) /
                          $number + 1);

    // return the total sum
    return (($lastnum + $firstnum) *
                         $count) / 2;
}

    // Driver Code
    $n = 3; $number = 7;
    echo totalSumDivisibleByNum($n, $number);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Efficient Javascript program to find
// the sum divisible numbers.

// Find the Sum of having n digit and
// divisible by the number
function totalSumDivisibleByNum(digit, number)
{

    // Compute the first and last term
    let firstnum = Math.pow(10, digit - 1);
    let lastnum = Math.pow(10, digit);

    // First number which is divisible
    // by given number
    firstnum = (firstnum - firstnum %
                 number) + number;

    // Last number which is divisible
    // by given number
    lastnum = (lastnum - lastnum % number);

    // Total divisible number
    let count = ((lastnum - firstnum) /
                   number + 1);

    // Return the total sum
    return ((lastnum + firstnum) * count) / 2;
}

// Driver Code
let n = 3, number = 7;

document.write(totalSumDivisibleByNum(n, number));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
70336
```