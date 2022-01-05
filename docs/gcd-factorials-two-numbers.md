# 两个数阶乘的 GCD

> 原文:[https://www.geeksforgeeks.org/gcd-factorials-two-numbers/](https://www.geeksforgeeks.org/gcd-factorials-two-numbers/)

给定两个数 m 和 n，求它们阶乘的 GCD。
**例:**

```
Input : n = 3, m = 4
Output : 6
Explanation:
Factorial of n = 1 * 2 * 3 = 6
Factorial of m = 1 * 2 * 3 * 4 = 24
GCD(6, 24) = 6.

Input : n = 9, m = 5
Output : 20
Explanation:
Factorial of n = 1 * 2 * 3 *4 * 5 * 6 * 7 * 8 
* 9 = 362880
Factorial of m = 1 * 2 * 3 * 4 * 5 = 120
GCD(362880, 120) = 120
```

一个**简单的解决方案**是找到两个数字的[阶乘](https://www.geeksforgeeks.org/factorial-large-number/)。然后找到计算阶乘的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。
一个**有效的解决方案**是基于两个阶乘的 GCD 等于较小的阶乘的事实(注意阶乘具有所有公共项)。
以下是上述方法的实施。

## C++

```
// CPP program to find GCD of factorial of two
// numbers.
#include <bits/stdc++.h>
using namespace std;

int factorial(int x)
{
    if (x <= 1)
        return 1;
    int res = 2;
    for (int i = 3; i <= x; i++)
        res = res * i;
    return res;
}

int gcdOfFactorial(int m, int n)
{
    return factorial(min(m, n));
}

int main()
{
    int m = 5, n = 9;
    cout << gcdOfFactorial(m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find GCD of factorial
// of two numbers.
public class FactorialGCD{

static int factorial(int x)
{
    if (x <= 1)
        return 1;
    int res = 2;
    for (int i = 3; i <= x; i++)
        res = res * i;
    return res;
}

static int gcdOfFactorial(int m, int n)
{
    int min = m < n ? m : n;
    return factorial(min);
}

    /* Driver program to test above functions */
    public static void main (String[] args)
    {
        int m = 5, n = 9;

        System.out.println(gcdOfFactorial(m, n));
    }
}

// This code is contributed by Prerna Saini
```

## 计算机编程语言

```
# Python code to find GCD of factorials of
# two numbers.
import math

def gcdOfFactorial(m, n) :
    return math.factorial(min(m, n))

# Driver code
m = 5
n = 9
print(gcdOfFactorial(m, n))
```

## C#

```
// C# program to find GCD of factorial
// of two numbers.
using System;

public class GFG{

    static int factorial(int x)
    {
        if (x <= 1)
            return 1;

        int res = 2;

        for (int i = 3; i <= x; i++)
            res = res * i;

        return res;
    }

    static int gcdOfFactorial(int m, int n)
    {
        int min = m < n ? m : n;
        return factorial(min);
    }

    /* Driver program to test above functions */
    public static void Main()
    {

        int m = 5, n = 9;

        Console.WriteLine(gcdOfFactorial(m, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find GCD
// of factorial of two numbers.

function factorial($x)
{
    if ($x <= 1)
        return 1;
    $res = 2;
    for ($i = 3; $i <= $x; $i++)
        $res = $res * $i;
    return $res;
}

function gcdOfFactorial($m, $n)
{
    return factorial(min($m, $n));
}

// Driver Code
$m = 5; $n = 9;
echo gcdOfFactorial($m, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to find GCD of factorial
// of two numbers.

    function factorial(x) {
        if (x <= 1)
            return 1;
        var res = 2;
        for (i = 3; i <= x; i++)
            res = res * i;
        return res;
    }

    function gcdOfFactorial(m , n) {
        var min = m < n ? m : n;
        return factorial(min);
    }

    /* Driver program to test above functions */

        var m = 5, n = 9;

        document.write(gcdOfFactorial(m, n));

// This code is contributed by aashish1995

</script>
```

**输出:**

```
120
```