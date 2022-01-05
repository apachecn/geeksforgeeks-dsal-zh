# 求 y mod 的值(2 升至 x 次方)

> 原文:[https://www . geesforgeks . org/find-value-of-y-mod-2-raid-to-power-x/](https://www.geeksforgeeks.org/find-value-of-y-mod-2-raised-to-power-x/)

给定两个正整数 x 和 y，我们必须找到 y mod 2 <sup>x</sup> 的值。这是 y 除以 2 <sup>x</sup> 的余数。

**示例:**

```
Input : x = 3, y = 14
Output : 6
Explanation : 14 % 23 =  14 % 8 = 6.

Input : x = 4, y = 14
Output : 14
Explanation : 14 % 24 =  14 % 16 = 14.
```

为了解决这个问题，我们可以使用幂()和模运算符，并且可以很容易地找到余数。
但有几点我们要关心:

*   对于较高的 x 值，如 2 <sup>x</sup> 大于长整型范围，我们不能得到合适的结果。
*   每当 y < 2 <sup>x</sup> 时，余数总是 y。因此，在这种情况下，我们可以限制自己计算值 2 <sup>x</sup> 为:

```
y < 2x
log y < x
// means if log y is less than x, then 
// we can print y as remainder.
```

*   我们可以在一个变量中存储 2 <sup>x</sup> 的 2 <sup>x</sup> 的最大值是 2 <sup>63</sup> 。这意味着对于 x > 63，y 总是小于 2 <sup>x</sup> ，在这种情况下，y mod 2 <sup>x</sup> 的余数就是 y 本身。

记住以上几点，我们可以这样来处理这个问题:

```
if (log y < x)
    return y;
else if (x  < 63)
    return y;
else 
    return (y % (pow(2, x)))
```

**注意:**由于 python 是极限自由的，我们可以直接使用 mod 和 pow()函数

## C++

```
// C++ Program to find the
// value of y mod 2^x
#include <bits/stdc++.h>
using namespace std;

// function to calculate y mod 2^x
long long int yMod(long long int y,
                    long long int x)
{
    // case 1 when y < 2^x
    if (log2(y) < x)
        return y;

    // case 2 when 2^x is out of
    // range means again y < 2^x
    if (x > 63)
        return y;

    // if y > 2^x
    return (y % (1 << x));
}

// driver program
int main()
{
    long long int y = 12345;
    long long int x = 11;   
    cout << yMod(y, x);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find
// the value of y mod 2^x
import java.io.*;

class GFG
{
    // function to calculate
    // y mod 2^x
    static long yMod(long y,   
                     long x)
    {
        // case 1 when y < 2^x
        if ((Math.log(y) /
             Math.log(2)) < x)
            return y;

        // case 2 when 2^x is
        // out of range means
        // again y < 2^x
        if (x > 63)
            return y;

        // if y > 2^x
        return (y % (1 << (int)x));
    }

    // Driver Code
    public static void main(String args[])
    {
        long y = 12345;
        long x = 11;
        System.out.print(yMod(y, x));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Program to find the value
# of y mod 2 ^ x function to
# return y mod 2 ^ x
def yMod(y, x) :    
    return (y % pow(2, x))  

# Driver code
y = 12345
x = 11
print(yMod(y, x))
```

## C#

```
// C# Program to find the
// value of y mod 2^x
using System;

class GFG
{
    // function to calculate
    // y mod 2^x
    static long yMod(long y,
                     long x)
    {
        // case 1 when y < 2^x
        if (Math.Log(y, 2) < x)
            return y;

        // case 2 when 2^x is
        // out of range means
        // again y < 2^x
        if (x > 63)
            return y;

        // if y > 2^x
        return (y % (1 << (int)x));
    }

    // Driver Code
    static void Main()
    {
        long y = 12345;
        long x = 11;
        Console.Write(yMod(y, x));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// value of y mod 2^x

// function to
// calculate y mod 2^x
function yMod($y, $x)
{
    // case 1 when y < 2^x
    if ((log($y) / log(2)) < $x)
        return $y;

    // case 2 when 2^x is
    // out of range means
    // again y < 2^x
    if ($x > 63)
        return $y;

    // if y > 2^x
    return ($y % (1 << $x));
}

// Driver Code
$y = 12345;
$x = 11;
echo (yMod($y, $x));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// value of y mod 2^x

// Function to calculate y mod 2^x
function yMod(y, x)
{

    // Case 1 when y < 2^x
    if ((Math.log(y) / Math.log(2)) < x)
        return y;

    // Case 2 when 2^x is
    // out of range means
    // again y < 2^x
    if (x > 63)
        return y;

    // If y > 2^x
    return (y % (1 << x));
}

// Driver Code
let y = 12345;
let x = 11;

document.write(yMod(y, x));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
57
```

***时间复杂度:** O(x)*

***辅助空间:** O(1)*
[用 2 的幂计算模数除法](https://www.geeksforgeeks.org/compute-modulus-division-by-a-power-of-2-number/)