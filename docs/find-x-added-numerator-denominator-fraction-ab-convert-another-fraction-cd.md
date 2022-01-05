# 求δX，将其加到分数(a/b)的分子和分母上，将其转换成另一个分数(c/d)

> 原文:[https://www . geesforgeks . org/find-x-add-分子-分母-分数-ab-convert-other-分数-cd/](https://www.geeksforgeeks.org/find-x-added-numerator-denominator-fraction-ab-convert-another-fraction-cd/)

给定 a/b 形式的分数，其中 a & b 是正整数。求δX，当它被加到给定分数的分子和分母上时，它将产生一个新的 Ir 可约分数 c/d.
**例:**

```
Input : a = 4, b = 10, c = 1, d = 2
Output : ΔX = 2
Explanation : (a + ΔX)/(b + ΔX) =
 (4 + 2) / (10 + 2) = 6/12 = 1/2 = c/d

Input : a = 4, b = 10, c = 2, d = 5
Output : ΔX = 0
Explanation : (a + ΔX) / (b + ΔX) = 
(4) / (10) = 2 / 5 = c/d
```

为了解决这种类型的问题，而不是仅仅实现一种编程方法，我们必须做一点数学。数学只是必要的如下:

```
As per question we have to find ΔX such that:
=> (a + ΔX) / (b + ΔX) = c / d
=> ad + dΔX = bc + cΔX
=> dΔX - cΔX = bc - ad
=> ΔX (d - c) = bc -ad
=> ΔX = (bc - ad) / (d - c)
```

所以，在寻找δX 的方法中，我们只需要计算

```
*** QuickLaTeX cannot compile formula:

*** Error message:
Error: Nothing to show, formula is empty

```

。

## C++

```
// C++ Program to find deltaX
#include <bits/stdc++.h>
using namespace std;

// function to find delta X
int findDelta(int a, int b, int c, int d)
{
    return (b * c - a * d) / (d - c);
}

// driver program
int main()
{
    int a = 3, b = 9, c = 3, d = 5;

    // u0394X is code for delta sign
    cout << "\u0394X = " << findDelta(a, b, c, d);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to
// find deltaX
import java.io.*;

class GFG
{
    // function to find delta X
    static int findDelta(int a, int b,
                         int c, int d)
    {
        return (b * c - a *
                d) / (d - c);
    }

    // Driver Code
    public static void main(String args[])
    {
        int a = 3, b = 9,
            c = 3, d = 5;

        // u0394X is code
        // for delta sign
        System.out.print("\u0394X = " +
                findDelta(a, b, c, d));
    }
}

// This code is contributed
// by Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python Program to find deltaX
# !/usr/bin/python
# coding=utf-8

# function to find delta X
def findDelta(a, b, c, d) :

    return int((b * c -
                a * d) /
               (d - c));

# Driver Code
a = 3; b = 9;
c = 3; d = 5;

# u0394X is code
# for delta sign
print ("X = {}" .
        format(findDelta(a, b,
                         c, d)));

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# Program to
// find deltaX
using System;

class GFG
{
// function to find delta X
static int findDelta(int a, int b,
                     int c, int d)
{
    return (b * c - a *
            d) / (d - c);
}

// Driver Code
static void Main()
{
    int a = 3, b = 9,
        c = 3, d = 5;

    // u0394X is code
    // for delta sign
    Console.Write("\u0394X = " +
                  findDelta(a, b, c, d));
}
}

// This code is contributed
// by Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find deltaX

// function to find delta X
function findDelta($a, $b,
                   $c, $d)
{
    return ($b * $c -
            $a * $d) / ($d - $c);
}

// Driver Code
$a = 3; $b = 9;
$c = 3; $d = 5;

// u0394X is code for delta sign
echo "?X = ".findDelta($a, $b,
                       $c, $d);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>
// JavaScript Program to
// find deltaX

 // function to find delta X
    function findDelta(a, b, c, d)
    {
        return (b * c - a *
                d) / (d - c);
    }

// Driver Code
        let a = 3, b = 9,
            c = 3, d = 5;

        // u0394X is code
        // for delta sign
        document.write("\u0394X = " +
                findDelta(a, b, c, d));

// This code is contributed by splevel62.
</script>
```

**输出:**

```
ΔX = 6
```