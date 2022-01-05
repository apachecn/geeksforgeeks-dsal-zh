# 计算阶乘可被 x 整除但不能被 y 整除的自然数

> 原文:[https://www . geeksforgeeks . org/count-自然数-其-阶乘-整除-x-not-y/](https://www.geeksforgeeks.org/count-natural-numbers-whose-factorials-divisible-x-not-y/)

给定两个数字 x 和 y (x <= y), find out the total number of natural numbers, say i, for which i! is divisible by x but not y. 
**举例:**

```
Input : x = 2, y = 5
Output : 3
There are three numbers, 2, 3 and 4
whose factorials are divisible by x
but not y.

Input: x = 15, y = 25
Output: 5
5! = 120 % 15 = 0 && 120 % 25 != 0
6! = 720 % 15 = 0 && 720 % 25 != 0
7! = 5040 % 15 = 0 && 5040 % 25 != 0
8! = 40320 % 15 = 0 && 40320 % 25 != 0
9! = 362880 % 15 = 0 && 362880 % 25 != 0
So total count = 5

Input: x = 10, y = 15
Output: 0
```

对于所有大于或等于 y 的数，它们的阶乘都可以被 y 整除，所以所有要计数的自然数都必须小于 y
一个**简单的解决方法**就是从 1 迭代到 y-1，对于每一个数，我检查我是否！可被 x 整除，不能被 y 整除，如果我们应用这种幼稚的方法，我们就不会超过 20！或者 21 岁！(long long int 会有上限)
A **更好的解决方案**是基于下图帖子。
[求第一个阶乘可被 x 整除的自然数](https://www.geeksforgeeks.org/find-first-natural-number-whose-factorial-divisible-x/)
我们求第一个阶乘可被 x 整除的自然数！还有 y！使用上述方法。设阶乘可被 x 和 y 整除的第一个自然数分别为 **xf** 和 **yf** 。我们的最终答案将是 YF–xf。这个公式是基于这样一个事实，如果我！可被数字 x 整除，那么(i+1)！，(i+2)！，…也可以被 x 整除
下面是实现。

## C++

```
// C++ program to count natural numbers whose
// factorials are divisible by x but not y.
#include<bits/stdc++.h>
using namespace std;

// GCD function to compute the greatest
// divisor among a and b
int gcd(int a, int b)
{
    if ((a % b) == 0)
        return b;
    return gcd(b, a % b);
}

// Returns first number whose factorial
// is divisible by x.
int firstFactorialDivisibleNumber(int x)
{
   int i = 1;  // Result
   int new_x = x;

   for (i=1; i<x; i++)
   {
       // Remove common factors
       new_x /= gcd(i, new_x);

       // We found first i.
       if (new_x == 1)
          break;
   }
   return i;
}

// Count of natural numbers whose factorials
// are divisible by x but not y.
int countFactorialXNotY(int x, int y)
{
    // Return difference between first natural
    // number whose factorial is divisible by
    // y and first natural number whose factorial
    // is divisible by x.
    return (firstFactorialDivisibleNumber(y) -
            firstFactorialDivisibleNumber(x));
}

// Driver code
int main(void)
{
    int x = 15, y = 25;
    cout << countFactorialXNotY(x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count natural numbers whose
// factorials are divisible by x but not y.

class GFG
{
    // GCD function to compute the greatest
    // divisor among a and b
    static int gcd(int a, int b)
    {
        if ((a % b) == 0)
            return b;
        return gcd(b, a % b);
    }

    // Returns first number whose factorial
    // is divisible by x.
    static int firstFactorialDivisibleNumber(int x)
    {
        int i = 1; // Result
        int new_x = x;

        for (i = 1; i < x; i++)
        {
            // Remove common factors
            new_x /= gcd(i, new_x);

            // We found first i.
            if (new_x == 1)
                break;
        }
        return i;
    }

    // Count of natural numbers whose factorials
    // are divisible by x but not y.
    static int countFactorialXNotY(int x, int y)
    {
        // Return difference between first natural
        // number whose factorial is divisible by
        // y and first natural number whose factorial
        // is divisible by x.
        return (firstFactorialDivisibleNumber(y) -
                firstFactorialDivisibleNumber(x));
    }

    // Driver code
    public static void main (String[] args)
    {
        int x = 15, y = 25;
        System.out.print(countFactorialXNotY(x, y));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to count natural
# numbers whose factorials are
# divisible by x but not y.

# GCD function to compute the greatest
# divisor among a and b
def gcd(a, b):

    if ((a % b) == 0):
        return b

    return gcd(b, a % b)

# Returns first number whose factorial
# is divisible by x.
def firstFactorialDivisibleNumber(x):

    # Result
    i = 1
    new_x = x

    for i in range(1, x):

        # Remove common factors
        new_x /= gcd(i, new_x)

        # We found first i.
        if (new_x == 1):
            break

    return i

# Count of natural numbers whose
# factorials are divisible by x but
# not y.
def countFactorialXNotY(x, y):

    # Return difference between first
    # natural number whose factorial
    # is divisible by y and first
    # natural number whose factorial
    # is divisible by x.
    return (firstFactorialDivisibleNumber(y) -
            firstFactorialDivisibleNumber(x))

# Driver code
x = 15
y = 25

print(countFactorialXNotY(x, y))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to count natural numbers whose
// factorials are divisible by x but not y.
using System;

class GFG
{

    // GCD function to compute the greatest
    // divisor among a and b
    static int gcd(int a, int b)
    {
        if ((a % b) == 0)
            return b;
        return gcd(b, a % b);
    }

    // Returns first number whose factorial
    // is divisible by x.
    static int firstFactorialDivisibleNumber(int x)
    {
        int i = 1; // Result
        int new_x = x;

        for (i = 1; i < x; i++)
        {

            // Remove common factors
            new_x /= gcd(i, new_x);

            // We found first i.
            if (new_x == 1)
                break;
        }

        return i;
    }

    // Count of natural numbers whose factorials
    // are divisible by x but not y.
    static int countFactorialXNotY(int x, int y)
    {

        // Return difference between first natural
        // number whose factorial is divisible by
        // y and first natural number whose factorial
        // is divisible by x.
        return (firstFactorialDivisibleNumber(y) -
                firstFactorialDivisibleNumber(x));
    }

    // Driver code
    public static void Main ()
    {
        int x = 15, y = 25;

        Console.Write(countFactorialXNotY(x, y));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count natural
// numbers whose factorials are
// divisible by x but not y.

// GCD function to compute the
// greatest divisor among a and b
function gcd($a, $b)
{
    if (($a % $b) == 0)
        return $b;
    return gcd($b, $a % $b);
}

// Returns first number whose
// factorial is divisible by x.
function firstFactorialDivisibleNumber($x)
{
    // Result
    $i = 1;
    $new_x = $x;

    for ($i = 1; $i < $x; $i++)
    {
        // Remove common factors
        $new_x /= gcd($i, $new_x);

        // We found first i.
        if ($new_x == 1)
            break;
    }
    return $i;
}

// Count of natural numbers
// whose factorials are divisible
// by x but not y.
function countFactorialXNotY($x, $y)
{
    // Return difference between
    // first natural number whose
    // factorial is divisible by
    // y and first natural number
    // whose factorial is divisible by x.
    return (firstFactorialDivisibleNumber($y) -
            firstFactorialDivisibleNumber($x));
}

// Driver code
$x = 15; $y = 25;
echo(countFactorialXNotY($x, $y));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to Merge two sorted halves of
// array Into Single Sorted Array

    // GCD function to compute the greatest
    // divisor among a and b
    function gcd(a, b)
    {
        if ((a % b) == 0)
            return b;
        return gcd(b, a % b);
    }

    // Returns first number whose factorial
    // is divisible by x.
    function firstFactorialDivisibleNumber(x)
    {
        let i = 1; // Result
        let new_x = x;

        for (i = 1; i < x; i++)
        {
            // Remove common factors
            new_x /= gcd(i, new_x);

            // We found first i.
            if (new_x == 1)
                break;
        }
        return i;
    }

    // Count of natural numbers whose factorials
    // are divisible by x but not y.
    function countFactorialXNotY(x, y)
    {
        // Return difference between first natural
        // number whose factorial is divisible by
        // y and first natural number whose factorial
        // is divisible by x.
        return (firstFactorialDivisibleNumber(y) -
                firstFactorialDivisibleNumber(x));
    }

// Driver code   

        let x = 15, y = 25;
        document.write(countFactorialXNotY(x, y));

</script>
```

**输出:**

```
5
```

本文由 **Shubham Gupta** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。