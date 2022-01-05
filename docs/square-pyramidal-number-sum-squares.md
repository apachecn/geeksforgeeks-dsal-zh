# 方形金字塔数(平方和)

> 原文:[https://www . geesforgeks . org/square-金字塔形-数字-总和-平方/](https://www.geeksforgeeks.org/square-pyramidal-number-sum-squares/)

方形金字塔数字表示第一自然数的平方和[。最初的几个方形金字塔数字是 1、5、14、30、55、91、140、204、285、385、506、……
从几何学上讲，这些数字代表要堆叠起来形成方形底部金字塔的球体数量。请参见](https://www.geeksforgeeks.org/sum-of-squares-of-first-n-natural-numbers/)[本维基图片](https://en.wikipedia.org/wiki/Square_pyramidal_number#/media/File:Square_pyramidal_number.svg)以获得更多清晰信息。
给定一个数字 s (1 < = s < = 1000000000)。如果 s 是前 n 个自然数的平方和，则打印 n，否则打印-1。
**举例:**

```
Input : 14
Output : 3
Explanation : 1*1 + 2*2 + 3*3 = 14

Input : 26
Output : -1
```

一个**简单的解决方法**是从 1 开始遍历所有数字，计算当前总和。如果当前和等于给定和，那么我们返回真，否则返回假。

## C++

```
// C++ program to check if a
// given number is sum of
// squares of natural numbers.
#include <iostream>
using namespace std;

// Function to find if the
// given number is sum of
// the squares of first n
// natural numbers
int findS(int s)
{
    int sum = 0;

    // Start adding squares of
    // the numbers from 1
    for (int n = 1; sum < s; n++)
    {
        sum += n * n;

        // If sum becomes equal to s
        // return n
        if (sum == s)
            return n;
    }

    return -1;
}

// Drivers code
int main()
{
    int s = 13;
    int n = findS(s);
    n == -1 ? cout << "-1" : cout << n;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a
// given number is sum of
// squares of natural numbers.
class GFG
{

    // Function to find if the
    // given number is sum of
    // the squares of first
    // n natural numbers
    static int findS(int s)
    {
        int sum = 0;

        // Start adding squares of
        // the numbers from 1
        for (int n = 1; sum < s; n++)
        {
            sum += n * n;

            // If sum becomes equal to s
            // return n
            if (sum == s)
                return n;
        }

        return -1;
    }

    // Drivers code
    public static void main(String[] args)
    {

        int s = 13;
        int n = findS(s);
        if (n == -1)
            System.out.println("-1");
        else
            System.out.println(n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find if
# the given number is sum of
# the squares of first
# n natural numbers

# Function to find if the given
# number is sum of the squares
# of first n natural numbers
def findS (s):
    _sum = 0
    n = 1

    # Start adding squares of
    # the numbers from 1
    while(_sum < s):
        _sum += n * n
        n+= 1
    n-= 1

    # If sum becomes equal to s
    # return n
    if _sum == s:
        return n
    return -1

# Driver code
s = 13
n = findS (s)
if n == -1:
    print("-1")
else:
    print(n)
```

## C#

```
// C# program to check if a given
// number is sum of squares of
// natural numbers.
using System;

class GFG
{

    // Function to find if the given
    // number is sum of the squares
    // of first n natural numbers
    static int findS(int s)
    {
        int sum = 0;

        // Start adding squares of
        // the numbers from 1
        for (int n = 1; sum < s; n++)
        {
            sum += n * n;

            // If sum becomes equal
            // to s return n
            if (sum == s)
                return n;
        }

        return -1;
    }

    // Drivers code
    public static void Main()
    {
        int s = 13;

        int n = findS(s);

        if(n == -1)
            Console.Write("-1") ;
        else
            Console.Write(n);
    }
}
// This code is contribute by
// Smitha Dinesh Semwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// given number is sum of
// squares of natural numbers.

// Function to find if the given number
// is sum of the squares of first n
// natural numbers
function findS($s)
{
    $sum = 0;

    // Start adding squares of
    // the numbers from 1
    for ($n = 1; $sum < $s; $n++)
    {
        $sum += $n * $n;

        // If sum becomes equal to s
        // return n
        if ($sum == $s)
            return $n;
    }

    return -1;
}

// Drivers code
$s = 13;
$n = findS($s);
if($n == -1)
    echo("-1");
else
    echo($n);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript to check if a
// given number is sum of
// squares of natural numbers.

    // Function to find if the
    // given number is sum of
    // the squares of first
    // n natural numbers
    function findS(s)
    {
        let sum = 0;

        // Start adding squares of
        // the numbers from 1
        for (let n = 1; sum < s; n++)
        {
            sum += n * n;

            // If sum becomes equal to s
            // return n
            if (sum == s)
                return n;
        }

        return -1;
    }

// Driver code
        let s = 13;
        let n = findS(s);
        if (n == -1)
            document.write("-1");
        else
            document.write(n);

// This code is contributed by souravghosh0416.
</script>
```

**输出:**T2】

```
-1
```

一个**替代方案**是使用[牛顿拉夫森法](https://www.geeksforgeeks.org/program-for-newton-raphson-method/)。
我们知道[前 n 个自然数](https://www.geeksforgeeks.org/sum-of-squares-of-first-n-natural-numbers/)的平方和为 **n * (n + 1) * (2*n + 1) / 6** 。
我们可以把解写成
k *(k+1)*(2 * k+1)/6 = s
k *(k+1)*(2 * k+1)–6s = 0
我们可以用牛顿拉夫森法求上述三次方程的根，然后检查根是否为整数。