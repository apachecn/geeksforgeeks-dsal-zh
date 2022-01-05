# GCD、LCM 和分配属性

> 原文:[https://www . geesforgeks . org/gcd-LCM-distributed-property/](https://www.geeksforgeeks.org/gcd-lcm-distributive-property/)

给定三个整数 x，y，z，任务是计算 **GCD(LCM(x，y)，LCM(x，z))** 的值。
其中， [GCD](https://www.geeksforgeeks.org/lcm-and-hcf/) =最大公约数， [LCM](https://www.geeksforgeeks.org/lcm-and-hcf/) =最小公倍数
示例:

```
Input: x = 15, y = 20, z = 100
Output: 60

Input: x = 30, y = 40, z = 400
Output: 120
```

一种解决方法是通过[找到 GCD(x，y)](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) ，利用它我们找到 LCM(x，y)。类似地，我们找到 LCM(x，z)，然后我们最终找到所获得结果的 GCD。
一个有效的方法可以通过以下事实来实现:分布式的以下版本成立:
GCD(LCM (x，y)，LCM (x，z)) = LCM(x，GCD(y，z))
例如，GCD(LCM(3，4)，LCM(3，10)) = LCM(3，GCD(4，10)) = LCM(3，2) = 6
这减少了我们计算给定问题陈述的工作。

## C++

```
// C++ program to compute value of GCD(LCM(x,y), LCM(x,z))
#include<bits/stdc++.h>
using namespace std;

// Returns value of  GCD(LCM(x,y), LCM(x,z))
int findValue(int x, int y, int z)
{
    int g = __gcd(y, z);

    // Return LCM(x, GCD(y, z))
    return (x*g)/__gcd(x, g);
}

int main()
{
    int x = 30, y = 40, z = 400;
    cout << findValue(x, y, z);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compute value
// of GCD(LCM(x,y), LCM(x,z))

class GFG
{
    // Recursive function to
    // return gcd of a and b
    static int __gcd(int a, int b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
        return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }

    // Returns value of GCD(LCM(x,y), LCM(x,z))
    static int findValue(int x, int y, int z)
    {
        int g = __gcd(y, z);

        // Return LCM(x, GCD(y, z))
        return (x*g) / __gcd(x, g);
    }

    // Driver code
    public static void main (String[] args)
    {
        int x = 30, y = 40, z = 400;
        System.out.print(findValue(x, y, z));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to compute
# value of GCD(LCM(x,y), LCM(x,z))

# Recursive function to
# return gcd of a and b
def __gcd(a,b):

    # Everything divides 0
    if (a == 0 or b == 0):
        return 0

    # base case
    if (a == b):
        return a

    # a is greater
    if (a > b):
        return __gcd(a-b, b)
    return __gcd(a, b-a)

# Returns value of
#  GCD(LCM(x,y), LCM(x,z))
def findValue(x, y, z):

    g = __gcd(y, z)

    # Return LCM(x, GCD(y, z))
    return (x*g)/__gcd(x, g)

# driver code
x = 30
y = 40
z = 400
print("%d"%findValue(x, y, z))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to compute value
// of GCD(LCM(x,y), LCM(x,z))
using System;

class GFG {

    // Recursive function to
    // return gcd of a and b
    static int __gcd(int a, int b)
    {

        // Everything divides 0
        if (a == 0 || b == 0)
        return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }

    // Returns value of GCD(LCM(x,y),
    // LCM(x,z))
    static int findValue(int x, int y, int z)
    {
        int g = __gcd(y, z);

        // Return LCM(x, GCD(y, z))
        return (x*g) / __gcd(x, g);
    }

    // Driver code
    public static void Main ()
    {
        int x = 30, y = 40, z = 400;

        Console.Write(findValue(x, y, z));
    }
}

// This code is contributed by
// Smitha Dinesh Semwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to compute value
// of GCD(LCM(x,y), LCM(x,z))

// Recursive function to
// return gcd of a and b
function __gcd( $a, $b)
{

    // Everything divides 0
    if ($a == 0 or $b == 0)
    return 0;

    // base case
    if ($a == $b)
        return $a;

    // a is greater
    if ($a > $b)
        return __gcd($a - $b, $b);
    return __gcd($a, $b - $a);
}

// Returns value of GCD(LCM(x,y),
// LCM(x,z))
function findValue($x, $y, $z)
{
    $g = __gcd($y, $z);

    // Return LCM(x, GCD(y, z))
    return ($x * $g)/__gcd($x, $g);
}

    // Driver Code
    $x = 30;
    $y = 40;
    $z = 400;
    echo findValue($x, $y, $z);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// JavaScript program to compute value of GCD(LCM(x,y), LCM(x,z))
function __gcd( a,  b)
    {
        // Everything divides 0
        if (a == 0 || b == 0)
        return 0;

        // base case
        if (a == b)
            return a;

        // a is greater
        if (a > b)
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }
// Returns value of  GCD(LCM(x,y), LCM(x,z))
function findValue(x, y, z)
{
    let g = __gcd(y, z);

    // Return LCM(x, GCD(y, z))
    return (x*g)/__gcd(x, g);
}

    let x = 30, y = 40, z = 400;
    document.write( findValue(x, y, z));

// This code contributed by gauravrajput1

</script>
```

输出:

```
120
```

作为旁注，反之亦然，即 gcd(x，lcm(y，z)) = lcm(gcd(x，y)，gcd(x，z)
**参考:**
[https://en . Wikipedia . org/wiki/distributed _ property # Other _ examples](https://en.wikipedia.org/wiki/Distributive_property#Other_examples)
本文由 **Mazhar Imam Khan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。