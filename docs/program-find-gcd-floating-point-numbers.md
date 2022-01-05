# 求浮点数 GCD 的程序

> 原文:[https://www . geesforgeks . org/program-find-gcd-floating-numbers/](https://www.geeksforgeeks.org/program-find-gcd-floating-point-numbers/)

两个或多个不全为零的数的[最大公约数(GCD)](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 是除以每个数的最大正数。
**例:**

```
Input  : 0.3, 0.9
Output : 0.3

Input  : 0.48, 0.108
Output : 0.012
```

解决这个问题最简单的方法是:
**a = 1.20**
**b = 22.5**
把每一个没有小数的数字表示为素数的乘积我们得到:
**120**![=2^3*3*5   ](img/321896b660091b9ef616e1d7e2a967b0.png "Rendered by QuickLaTeX.com")
2250![=2*3^2*5^3   ](img/fc0fffae7faac94a47ef814faeeed41f.png "Rendered by QuickLaTeX.com")T15】现在，120 和 2250 的汉化 f = 2 * 3 * 5 = 30
**因此该算法表明，如果从一个较大的数字中减去较小的数字，两个数字的 GCD 不会改变。** 

## C++

```
// CPP code for finding the GCD of two floating
// numbers.
#include <bits/stdc++.h>
using namespace std;

// Recursive function to return gcd of a and b
double gcd(double a, double b)
{
    if (a < b)
        return gcd(b, a);

    // base case
    if (fabs(b) < 0.001)
        return a;

    else
        return (gcd(b, a - floor(a / b) * b));
}

// Driver Function.
int main()
{
    double a = 1.20, b = 22.5;
    cout << gcd(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA code for finding the GCD of
// two floating numbers.
import java.io.*;

class GFG {

    // Recursive function to return gcd
    // of a and b
    static double gcd(double a, double b)
    {
        if (a < b)
            return gcd(b, a);

        // base case
        if (Math.abs(b) < 0.001)
            return a;

        else
            return (gcd(b, a -
                   Math.floor(a / b) * b));
    }

    // Driver Function.
    public static void main(String args[])
    {
        double a = 1.20, b = 22.5;
        System.out.printf("%.1f" ,gcd(a, b));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 计算机编程语言

```
# Python code for finding the GCD of
# two floating numbers.

import math

# Recursive function to return gcd
# of a and b
def gcd(a,b) :
    if (a < b) :
        return gcd(b, a)

    # base case
    if (abs(b) < 0.001) :
        return a
    else :
        return (gcd(b, a - math.floor(a / b) * b))

# Driver Function.
a = 1.20
b = 22.5
print('{0:.1f}'.format(gcd(a, b)))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# code for finding the GCD of
// two floating numbers.
using System;

class GFG {

    // Recursive function to return gcd
    // of a and b
    static float  gcd(double a, double b)
    {
        if (a < b)
            return gcd(b, a);

        // base case
        if (Math.Abs(b) < 0.001)
            return (float)a;

        else
            return (float)(gcd(b, a -
                Math.Floor(a / b) * b));
    }

    // Driver Function.
    public static void Main()
    {
        double a = 1.20, b = 22.5;

        Console.WriteLine(gcd(a, b));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code for finding the GCD
// of two floating numbers.

// Recursive function to
// return gcd of a and b
function gcd($a, $b)
{
    if ($a < $b)
        return gcd($b, $a);

    // base case
    if (abs($b) < 0.001)
        return $a;

    else
        return (gcd($b, $a -
              floor($a / $b) * $b));
}

// Driver Code
$a = 1.20;
$b = 22.5;
echo gcd($a, $b);

// This code is contributed
// by aj_36
?>
```

## java 描述语言

```
<script>
// javascript code for finding the GCD of
// two floating numbers.

    // Recursive function to return gcd
    // of a and b
    function gcd(a , b)
    {
        if (a < b)
            return gcd(b, a);

        // base case
        if (Math.abs(b) < 0.001)
            return a;
        else
            return (gcd(b, a - Math.floor(a / b) * b));
    }

    // Driver Function.   
    var a = 1.20, b = 22.5;
    document.write( gcd(a, b).toFixed(1));

// This code is contributed by aashish1995
</script>
```

**输出:**

```
0.3
```

本文由 **Abhishek Sharma** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。