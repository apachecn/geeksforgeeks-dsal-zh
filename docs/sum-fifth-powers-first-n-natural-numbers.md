# 前 n 个自然数的五次幂之和

> 原文:[https://www . geesforgeks . org/sum-五次幂-第一-n-自然数/](https://www.geeksforgeeks.org/sum-fifth-powers-first-n-natural-numbers/)

写一个程序求前 n 个自然数 1<sup>5</sup>+2<sup>5</sup>+3<sup>5</sup>+4<sup>5</sup>+……。+ n <sup>5</sup> 直到第 n 个学期。
示例:

```

Input  : 4
Output : 1300
15 + 25 + 35 + 45 = 1300 

Input  : 6
Output : 
15 + 25 + 35 + 45 + 52 + 65
```

**天真的方法:-** 在这个简单的求前 n 个自然数的五次幂的方法中，迭代一个从 1 到 n 次的循环。比如假设 n=5。并存储在和变量中。
(1 * 1 * 1 * 1 * 1)+(2 * 2 * 2 * 2 * 2)+(3 * 3 * 3 * 3 * 3 * 3)+(4 * 4 * 4 * 4 * 4)= 1300

## C++

```
// CPP Program to find the sum of fifth powers
// of first n natural numbers
#include <bits/stdc++.h>
using namespace std;

// calculate the sum of fifth power of
// first n natural numbers
long long int fifthPowerSum(int n)
{
    long long int sum = 0;
    for (int i = 1; i <= n; i++)
        sum = sum + (i * i * i * i * i);
    return sum;
}

// Driven Program
int main()
{
    int n = 6;
    cout << fifthPowerSum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// sum of fifth  powers of
// first n natural numbers
import java.io.*;

class GFG
{
    // calculate the sum of fifth
    // power of first n natural
    // numbers
    static long fifthPowerSum(int n)
    {
        long sum = 0;
        for (int i = 1; i <= n; i++)
            sum = sum + (i * i * i * i * i);
        return sum;
    }

    // Driven Program
    public static void main(String args[])
    {
        int n = 6;
        System.out.println(fifthPowerSum(n));
    }
}

// This code is contributed by
// Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 Program to find the
# sum of fifth powers of first
# n natural numbers

# calculate the sum of fifth
# power of first n natural
# numbers
def fifthPowerSum(n) :

    sm = 0

    for i in range(1, n+1) :
        sm = sm + (i * i * i * i * i)

    return sm

# Driven Program
n = 6
print(fifthPowerSum(n))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# Program to find the
// sum of fifth powers of
// first n natural numbers
using System;

class GFG
{
    // calculate the sum of fifth
    // power of first n natural
    // numbers
    static long fifthPowerSum(int n)
    {
        long sum = 0;
        for (int i = 1; i <= n; i++)
            sum = sum + (i * i * i * i * i);

        return sum;
    }

    // Driven Program
    public static void Main()
    {
        int n = 6;
        Console.Write(fifthPowerSum(n));
    }
}

// This code is contributed by
// vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find
// the sum of fifth powers
// of first n natural numbers

// calculate the sum of
// fifth power of
// first n natural numbers
function fifthPowerSum($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum = $sum + ($i * $i * $i *
                             $i * $i);
    return $sum;
}

// Driver Code
$n = 6;
echo(fifthPowerSum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// javascript Program to find the sum of fifth powers
// of first n natural numbers

// calculate the sum of fifth power of
// first n natural numbers
function fifthPowerSum( n)
{
    let sum = 0;
    for (let i = 1; i <= n; i++)
        sum = sum + (i * i * i * i * i);
    return sum;
}

// Driven Program

    let n = 6;
     document.write(fifthPowerSum(n));

// This code contributed by aashish1995

</script>
```

输出:

```
 12201
```

**时间复杂度:** O(N)
**有效方法:-** 一个有效的解决方案是使用直接的数学公式:

```
(2*n<sup>6+6*n5+5*n4 - n2)/12</sup> 

OR (Can also be written as)

(1/6)n<sup>6 + (1/2)n5 + (5/12)n4 – (1/12)n2\.</sup> 
```

## C++

```
// CPP Program to find the sum of fifth power
// of first n natural numbers
#include <bits/stdc++.h>
using namespace std;

// calculate the sum of fifth power of first n natural numbers
long long int fifthPowerSum(int n)
{
    return ((2 * n * n * n * n * n * n) +
           (6 * n * n * n * n * n) +
           (5 * n * n * n * n) -
           (n * n)) / 12;
}

// Driven Program
int main()
{
    int n = 5;
    cout << fifthPowerSum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the sum of fifth power
// of first n natural numbers
import java.io.*;

class GFG {

    // calculate the sum of fifth power
    //of first n natural numbers
    static long fifthPowerSum(int n)
    {
        return ((2 * n * n * n * n * n * n) +
            (6 * n * n * n * n * n) +
            (5 * n * n * n * n) -
            (n * n)) / 12;
    }

    // Driven Program
    public static void main(String args[])
    {
        int n = 5;
        System.out.println(fifthPowerSum(n));
    }
}

 /*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 Program to find the
# sum of fifth power of first
# n natural numbers

# Calculate the sum of fifth
# power of first n natural
# numbers
def fifthPowerSum(n) :
    return ((2 * n * n * n * n * n * n) +
            (6 * n * n * n * n * n) +
            (5 * n * n * n * n) -
            (n * n)) // 12

# Driven Program
n = 5
print(fifthPowerSum(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Program to find the sum
// of fifth power of first n
// natural numbers
using System;

class GFG {

    // calculate the sum of fifth power
    // of first n natural numbers
    static long fifthPowerSum(int n)
    {
        return ((2 * n * n * n * n * n * n) +
            (6 * n * n * n * n * n) +
            (5 * n * n * n * n) -
            (n * n)) / 12;
    }

    // Driven Program
    public static void Main()
    {
        int n = 5;
        Console.Write(fifthPowerSum(n));
    }
}

/*This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find
// the sum of fifth power
// of first n natural numbers

// calculate the sum of
// fifth power of first
// n natural numbers
function fifthPowerSum($n)
{
    return ((2 * $n * $n * $n * $n * $n * $n) +
            (6 * $n * $n * $n * $n * $n) +
            (5 * $n * $n * $n * $n) -
            ($n * $n)) / 12;
}

// Driver Code
$n = 5;
echo(fifthPowerSum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// JavaScript Program to find the sum of fifth power
// of first n natural numbers

// calculate the sum of fifth power of first n natural numbers
function fifthPowerSum(n)
{
    return ((2 * n * n * n * n * n * n) +
        (6 * n * n * n * n * n) +
        (5 * n * n * n * n) -
        (n * n)) / 12;
}

// Driven Program

    let n = 5;
    document.write(fifthPowerSum(n) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
 4425
```

**时间复杂度:O(1)**