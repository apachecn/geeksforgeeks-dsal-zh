# 前 n 个自然数的四次幂之和

> 原文:[https://www . geesforgeks . org/sum-四次方-一次-n-自然数/](https://www.geeksforgeeks.org/sum-fourth-powers-first-n-natural-numbers/)

写一个程序求前 n 个自然数 1<sup>4</sup>+2<sup>4</sup>+3<sup>4</sup>+4<sup>4</sup>+……。+ n <sup>4</sup> 至第 n 个学期。
**举例:**

```
Input  : 4
Output : 354
14 + 24 + 34 + 44 = 354

Input  : 6
Output : 2275
14 + 24 + 34 + 44+ 54+ 64 = 2275
```

**天真的方法:-** 简单的求前 n 个自然数的四次幂就是迭代一个从 1 到 n 的循环。比如假设 n=4。
(1 * 1 * 1 * 1)+(2 * 2 * 2 * 2)+(3 * 3 * 3 * 3)+(4 * 4 * 4 * 4)= 354

## C++

```
// CPP Program to find the sum of forth powers
// of first n natural numbers
#include <bits/stdc++.h>
using namespace std;

// Return the sum of forth power of first n
// natural numbers
long long int fourthPowerSum(int n)
{
    long long int sum = 0;
    for (int i = 1; i <= n; i++)
        sum = sum + (i * i * i * i);
    return sum;
}

// Driven Program
int main()
{
    int n = 6;
    cout << fourthPowerSum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// sum of forth powers of
// first n natural numbers
import java.io.*;
import java.util.*;

class GFG {

    // Return the sum of forth
    // power of first n natural
    // numbers
    static long fourthPowerSum(int n)
    {
        long sum = 0;

        for (int i = 1; i <= n; i++)
            sum = sum + (i * i * i * i);

        return sum;
    }

    public static void main (String[] args)
    {
        int n = 6;
        System.out.println(fourthPowerSum(n));

    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 Program to find the
# sum of forth powers of first
# n natural numbers
import math

# Return the sum of forth power of
# first n natural numbers
def fourthPowerSum( n):

    sum = 0
    for i in range(1, n+1) :
        sum = sum + (i * i * i * i)
    return sum
# Driver method
n=6
print (fourthPowerSum(n))

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to find the
// sum of forth powers of
// first n natural numbers
using System;

class GFG {

    // Return the sum of forth power
    // of first n natural numbers
    static long fourthPowerSum(int n)
    {
        long sum = 0;

        for (int i = 1; i <= n; i++)
            sum = sum + (i * i * i * i);

        return sum;
    }

    public static void Main ()
    {
        int n = 6;
        Console.WriteLine(fourthPowerSum(n));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find th
// sum of fourth powers
// of first n natural numbers

// Return the sum of fourth
// power of first n
// natural numbers
function fourthPowerSum($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
        $sum = $sum + ($i * $i * $i * $i);
    return $sum;
}

// Driver Code
$n = 6;
echo(fourthPowerSum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// javascript Program to find the sum of forth powers
// of first n natural numbers

// Return the sum of forth power of first n
// natural numbers
function fourthPowerSum( n)
{
    let sum = 0;
    for (let i = 1; i <= n; i++)
        sum = sum + (i * i * i * i);
    return sum;
}
// Driven Program

    let n = 6;
     document.write(fourthPowerSum(n));

// This code contributed by aashish1995

</script>
```

**输出:**

```
2275
```

时间复杂度:O(n)
**有效方法:-** 一个有效的解决方案是使用直接的数学公式，该公式为 1/30n(n+1)(2n+1)(3n2+3n+1)或者也是写(1/5)n<sup>5</sup>+(1/2)n<sup>4</sup>+(1/3)n<sup>3</sup>–(1/30)n .这个解决方案需要 O(1)个时间。

## C++

```
// CPP Program to find the sum of forth power of first
// n natural numbers
#include <bits/stdc++.h>
using namespace std;

// Return the sum of forth power of first n natural
// numbers
long long int fourthPowerSum(int n)
{
    return ((6 * n * n * n * n * n) +
            (15 * n * n * n * n) +
            (10 * n * n * n) - n) / 30;
}

// Driven Program
int main()
{
    int n = 6;
    cout << fourthPowerSum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the
// sum of forth powers of
// first n natural numbers
import java.io.*;
import java.util.*;

class GFG {

    // Return the sum of
    // forth power of first
    // n natural numbers
    static long fourthPowerSum(int n)
    {
        return ((6 * n * n * n * n * n) +
                (15 * n * n * n * n) +
                (10 * n * n * n) - n) / 30;
    }

    public static void main (String[] args)
    {
        int n = 6;

        System.out.println(fourthPowerSum(n));

    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 Program to
# find the sum of
# forth powers of
# first n natural numbers
import math

# Return the sum of
# forth power of
# first n natural
# numbers
def fourthPowerSum(n):

    return ((6 * n * n * n * n * n) +
            (15 * n * n * n * n) +
            (10 * n * n * n) - n) / 30

# Driver method
n=6
print (fourthPowerSum(n))

# This code is contributed by Gitanjali.
```

## C#

```
// C# Program to find the
// sum of forth powers of
// first n natural numbers
using System;

class GFG {

    // Return the sum of
    // forth power of first
    // n natural numbers
    static long fourthPowerSum(int n)
    {
        return ((6 * n * n * n * n * n) +
                (15 * n * n * n * n) +
                (10 * n * n * n) - n) / 30;
    }

    public static void Main ()
    {
        int n = 6;

        Console.Write(fourthPowerSum(n));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the sum
// of fourth power of first
// n natural numbers

// Return the sum of fourth
// power of first n natural
// numbers
function fourthPowerSum($n)
{
    return ((6 * $n * $n * $n * $n * $n) +
            (15 * $n * $n * $n * $n) +
            (10 * $n * $n * $n) - $n) / 30;
}

// Driver Code
$n = 6;
echo(fourthPowerSum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// javascript Program to find the
// sum of forth powers of
// first n natural numbers

// Return the sum of
// forth power of first
// n natural numbers
function fourthPowerSum(n)
{
    return ((6 * n * n * n * n * n) +
            (15 * n * n * n * n) +
            (10 * n * n * n) - n) / 30;
}

var n = 6;

document.write(fourthPowerSum(n));

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
2275
```

时间复杂度:O(1)