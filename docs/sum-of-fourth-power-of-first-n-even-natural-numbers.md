# 前 n 个偶数自然数的四次幂之和

> 原文:[https://www . geeksforgeeks . org/一次 n 的四次幂之和偶数自然数/](https://www.geeksforgeeks.org/sum-of-fourth-power-of-first-n-even-natural-numbers/)

写一个程序求前 n 个偶数自然数的四次幂之和。
2<sup>4</sup>+4<sup>4</sup>+6<sup>4</sup>+8<sup>4</sup>+10<sup>4</sup>+……+2n<sup>4</sup>
**示例:**

```
Input  :   3
Output :  1568
24 +44 +64 = 1568
Input  :   6
Output :  36400
24 + 44 + 64 + 84 + 104 + 124 
```

**天真的方法** :-在这个简单的求前 n 个偶数自然数的四次幂的方法中，迭代一个从 1 到 n 的循环。每次迭代都存储在变量中，并持续到(I！=n)。这是一个 O(N)时间复杂度。

## C++

```
// CPP Program to find the sum of fourth powers of
// first n even natural numbers
#include <bits/stdc++.h>
using namespace std;

// calculate the sum of fourth power of first n even
// natural numbers
long long int evenPowerSum(int n)
{
    long long int sum = 0;
    for (int i = 1; i <= n; i++) {

        // made even number
        int j = 2 * i;
        sum = sum + (j * j * j * j);
    }
    return sum;
}

// Driven Program
int main()
{
    int n = 5;
    cout << evenPowerSum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the sum of fourth powers of
// first n even natural numbers

import java.io.*;

class GFG {

    // calculate the sum of fourth power of first
    // n even natural numbers
    static long evenPowerSum(int n)
    {
        long sum = 0;
        for (int i = 1; i <= n; i++)
        {

            // made even number
            int j = 2 * i;
            sum = sum + (j * j * j * j);
        }

        return sum;
    }

    // Driven Program
    public static void main (String[] args) {

        int n = 5;
        System.out.println(evenPowerSum(n));
    }
}

/*This code is contributed by vt_m.*/
```

## 蟒蛇 3

```
# Python3 Program to find
# the sum of fourth powers of
# first n even natural numbers

# calculate the sum of fourth
# power of first n even
# natural numbers
def evenPowerSum(n):
    sum = 0;
    for i in range(1, n + 1):

        # made even number
        j = 2 * i;
        sum = sum + (j * j * j * j);
    return sum;

# Driver Code
n = 5;
print(evenPowerSum(n));

# This is contributed by mits.
```

## C#

```
// C# Program to find the sum of fourth powers of
// first n even natural numbers
using System;

class GFG {

    // calculate the sum of fourth power of
    // first n even natural numbers
    static long evenPowerSum(int n)
    {

        long sum = 0;
        for (int i = 1; i <= n; i++) {

            // made even number
            int j = 2 * i;
            sum = sum + (j * j * j * j);
        }

        return sum;
    }

    // Driven Program
    public static void Main()
    {
        int n = 5;

        Console.Write(evenPowerSum(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// sum of fourth powers of
// first n even natural numbers

// calculate the sum of
// fourth power of first
// n even natural numbers
function evenPowerSum($n)
{
    $sum = 0;
    for ($i = 1; $i <= $n; $i++)
    {

        // made even number
        $j = 2 * $i;
        $sum = $sum + ($j * $j * $j * $j);
    }
    return $sum;
}

// Driver Code
$n = 5;
echo(evenPowerSum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find the sum of fourth powers of
// first n even natural numbers

// calculate the sum of fourth power of first n even
// natural numbers
function evenPowerSum( n)
{
    let sum = 0;
    for (let i = 1; i <= n; i++)
    {

        // made even number
        let j = 2 * i;
        sum = sum + (j * j * j * j);
    }
    return sum;
}

// Driven Program
    let n = 5;
     document.write(evenPowerSum(n));

// This code is contributed by Rajput-Ji

</script>
```

**输出:**

```
 15664
```

**时间复杂度:O(n)**
**有效方法:-** 一个有效的解决方案是使用直接的数学公式，其推导如下，这是只取 O(1)时间复杂度。

> 前 n 个偶数自然数的四次幂之和=**8 *(n *(n+1)*(2 * n+1)(3 * n<sup>2</sup>+3 * n-1))/15**
> **这个公式是怎么用的？**
> [自然数的四次幂之和](https://www.geeksforgeeks.org/sum-fourth-powers-first-n-natural-numbers/)是=(n(n+1)(2n+1)(3n<sup>2</sup>+3n-1))/30
> 我们需要偶数个自然数，所以我们把每个项乘以 2<sup>4</sup>
> = 2<sup>4</sup>(1<sup>4</sup>+2<sup>4</sup>+3<sup>4</sup>+……+1
> =(2<sup>4</sup>+4<sup>4</sup>+6<sup>4</sup>+…………+2n<sup>4</sup>)
> = 2<sup>4</sup>*(四次幂自然数之和)
> = 16 *(n *(n+1)*(2 * n+1)(3 * n<sup>2</sup>+3 * n-1))/30

## C++

```
// CPP Program to find the sum of fourth powers of
// first n even natural numbers
#include <bits/stdc++.h>
using namespace std;

// calculate the sum of fourth power of first n
// even natural numbers
long long int evenPowerSum(int n)
{
    return (8 * n * (n + 1) * (2 * n + 1) *
          (3 * n * n + 3 * n - 1)) / 15;
}

// Driven Program
int main()
{
    int n = 4;
    cout << evenPowerSum(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Program to find the sum of fourth powers of
// first n even natural numbers

import java.io.*;

class GFG {

    // calculate the sum of fourth power of first n
    // even natural numbers
    static long evenPowerSum(int n)
    {
        return (8 * n * (n + 1) * (2 * n + 1) *
                   (3 * n * n + 3 * n - 1)) / 15;
    }

    // Driven Program
    public static void main (String[] args) {

        int n = 4;
        System.out.println(evenPowerSum(n));
    }
}

/* This code is contributed by vt_m. */
```

## 蟒蛇 3

```
# Python3 Program to find
# the sum of fourth powers
# of first n even natural
# numbers

# calculate the sum of
# fourth power of first n
# even natural numbers
def evenPowerSum(n):
    return (8 * n * (n + 1) *
           (2 * n + 1) * (3 *
            n * n + 3 * n - 1)) / 15;

# Driver Code
n = 4;
print (int(evenPowerSum(n)));

# This code is contributed by mits
```

## C#

```
// C# Program to find the sum of fourth powers of
// first n even natural numbers

using System;

class GFG {

    // calculate the sum of fourth power of first n
    // even natural numbers
    static long evenPowerSum(int n)
    {
        return (8 * n * (n + 1) * (2 * n + 1) *
                     (3 * n * n + 3 * n - 1)) / 15;
    }

    // Driven Program
    public static void Main()
    {
        int n = 4;

        Console.Write(evenPowerSum(n));
    }
}

/* This code is contributed by vt_m.*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// sum of fourth powers of
// first n even natural numbers

// calculate the sum of
// fourth power of first n
// even natural numbers
function evenPowerSum($n)
{
    return (8 * $n * ($n + 1) *
           (2 * $n + 1) *
           (3 * $n * $n + 3 *
            $n - 1)) / 15;
}

// Driver Code
$n = 4;
echo(evenPowerSum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript Program to find the sum of fourth powers of
// first n even natural numbers   

// calculate the sum of fourth power of first n
// even natural numbers
    function evenPowerSum(n)
    {
        return (8 * n * (n + 1) * (2 * n + 1)
        * (3 * n * n + 3 * n - 1)) / 15;
    }

    // Driven Program

        var n = 4;
        document.write(evenPowerSum(n));

// This code is contributed by Rajput-Ji

</script>
```

**输出:**

```
5664
```

**时间复杂度:O(1)**