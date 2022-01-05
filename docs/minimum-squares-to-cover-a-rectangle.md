# 覆盖矩形的最小正方形

> 原文:[https://www . geesforgeks . org/最小正方形覆盖矩形/](https://www.geeksforgeeks.org/minimum-squares-to-cover-a-rectangle/)

给定一个长度为 **l** 和宽度为 **b** 的矩形，我们需要找到能够覆盖矩形表面的最小正方形数，假设每个正方形都有一条长度为 **a** 的边。允许覆盖大于矩形的表面，但必须覆盖矩形。不允许打破广场。
**举例:**

```
Input : 1 2 3
Output :1
We have a 3x3 square and we need
to make a rectangles of size 1x2.
So we need only square to cover the
rectangle.

Input : 11 23 14
Output :2
```

实际上最佳填充矩形的唯一方法是排列每个正方形，使其与矩形的边平行。所以我们只需要找到正方形的数量就可以完全覆盖矩形的长度和宽度。
矩形的长度为 **l** ，如果正方形的边长为 **a** 除 **l** ，则必须有 **l/a** 正方形来覆盖 **l** 的全长。如果 **l** 不能被 **a** 整除，我们需要在 **l/a** 上加上 **1** ，将其四舍五入。为此我们可以使用 **ceil 函数**，因为 ceil(x)返回大于或等于 x 的最小整数。
我们可以对矩形宽度做同样的处理，取宽度上的方块数为 **ceil(b/a)** 。
所以，方块总数= **ceil(m/a) * ceil(n/a)** 。

## C++

```
// C++ program to find the minimum number
// of squares to cover the surface of the
// rectangle with given dimensions
#include <bits/stdc++.h>
using namespace std;
int squares(int l, int b, int a)
{
    // function to count
    // the number of squares that can
    // cover the surface of the rectangle
    return ceil(l / (double)a) * ceil(b / (double)a);
}

// Driver code
int main()
{
    int l = 11, b = 23, a = 14;
    cout << squares(l, b, a) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum number
// of squares to cover the surface of the
// rectangle with given dimensions
class GFG 
{
static int squares(int l, int b, int a)
{

// function to count
// the number of squares that can
// cover the surface of the rectangle
return (int)(Math.ceil(l / (double)a) *
             Math.ceil(b / (double)a));
}

// Driver code
public static void main(String[] args) 
{
    int l = 11, b = 23, a = 14;
    System.out.println(squares(l, b, a));
}
}

// This code is contributed by ChitraNayal
```

## 蟒蛇 3

```
# Python3 program to find the minimum number
# of squares to cover the surface of the
# rectangle with given dimensions
import math

def squares(l, b, a):

    # function to count
    # the number of squares that can
    # cover the surface of the rectangle
    return math.ceil(l / a) * math.ceil(b / a)

# Driver code
if __name__ == "__main__":
    l = 11
    b = 23
    a = 14
    print(squares(l, b, a))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find the minimum number
// of squares to cover the surface of the
// rectangle with given dimensions
using System;

class GFG
{
static int squares(int l, int b, int a)
{

// function to count
// the number of squares that can
// cover the surface of the rectangle
return (int)(Math.Ceiling(l / (double)a) * 
             Math.Ceiling(b / (double)a));
}

// Driver code
public static void Main() 
{
    int l = 11, b = 23, a = 14;
    Console.Write(squares(l, b, a));
}
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php 
// PHP program to find the minimum number
// of squares to cover the surface of the
// rectangle with given dimensions

function squares($l, $b, $a)
{
    // function to count
    // the number of squares that can
    // cover the surface of the rectangle
    return ceil($l / (double)$a) *
           ceil($b / (double)$a);
}

// Driver code
$l = 11;
$b = 23;
$a = 14;
echo squares($l, $b, $a);

// This code is contributed 
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// javascript program to find the minimum number
// of squares to cover the surface of the
// rectangle with given dimensions

function squares(l , b , a)
{

    // function to count
    // the number of squares that can
    // cover the surface of the rectangle
    return parseInt(Math.ceil(l / a) *
                 Math.ceil(b / a));
}

// Driver code

var l = 11, b = 23, a = 14;
document.write(squares(l, b, a));

// This code is contributed by Amit Katiyar 

</script>
```

**Output:** 

```
2
```