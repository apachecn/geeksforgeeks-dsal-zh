# 使用递归的 2 个数字的乘积

> 原文:[https://www . geesforgeks . org/product-2-numbers-use-recursion/](https://www.geeksforgeeks.org/product-2-numbers-using-recursion/)

给定两个数 x 和 y，用递归求积。
**例:**

```
Input : x = 5, y = 2
Output : 10

Input : x = 100, y = 5
Output : 500
```

**方法**
1)如果 x 小于 y，交换两个变量值
2)递归求 y 乘以 x 的和
3)如果其中任何一个变为零，返回 0

## C++

```
// C++ Program to find Product
// of 2 Numbers using Recursion
#include <bits/stdc++.h>
using namespace std;

// recursive function to calculate
// multiplication of two numbers
int product(int x, int y)
{
    // if x is less than
    // y swap the numbers
    if (x < y)
        return product(y, x);

    // iteratively calculate
    // y times sum of x
    else if (y != 0)
        return (x + product(x, y - 1));

    // if any of the two numbers is
    // zero return zero
    else
        return 0;
}

// Driver Code
int main()
{
    int x = 5, y = 2;
    cout << product(x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find Product
// of 2 Numbers using Recursion
import java.io.*;
import java.util.*;

class GFG
{

    // recursive function to calculate
    // multiplication of two numbers
    static int product(int x, int y)
    {
        // if x is less than
        // y swap the numbers
        if (x < y)
            return product(y, x);

        // iteratively calculate
        // y times sum of x
        else if (y != 0)
            return (x + product(x, y - 1));

        // if any of the two numbers is
        // zero return zero
        else
            return 0;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int x = 5, y = 2;
        System.out.println(product(x, y));
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 to find Product of
# 2 Numbers using Recursion

# recursive function to calculate
# multiplication of two numbers
def product( x , y ):
    # if x is less than y swap
    # the numbers
    if x < y:
        return product(y, x)

    # iteratively calculate y
    # times sum of x
    elif y != 0:
        return (x + product(x, y - 1))

    # if any of the two numbers is
    # zero return zero
    else:
        return 0

# Driver code
x = 5
y = 2
print( product(x, y))

# This code is contributed
# by Abhishek Sharma44.
```

## C#

```
// C# Program to find Product
// of 2 Numbers using Recursion
using System;

class GFG
{

    // recursive function to calculate
    // multiplication of two numbers
    static int product(int x, int y)
    {
        // if x is less than
        // y swap the numbers
        if (x < y)
            return product(y, x);

        // iteratively calculate
        // y times sum of x
        else if (y != 0)
            return (x + product(x, y - 1));

        // if any of the two numbers is
        // zero return zero
        else
            return 0;
    }

    // Driver code
    public static void Main ()
    {
        int x = 5, y = 2;
        Console.WriteLine(product(x, y));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find Product
// of 2 Numbers using Recursion

// recursive function to calculate
// multiplication of two numbers
function product($x, $y)
{
    // if x is less than 
    // y swap thenumbers
    if ($x < $y)
        return product($y, $x);

    // iteratively calculate
    // y times sum of x
    else if ($y != 0)
        return ($x + product($x, $y - 1));

    // if any of the two numbers is
    // zero return zero
    else
        return 0;
}

// Driver Code
$x = 5; $y = 2;
echo(product($x, $y));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// JavaScript program to find Product
// of 2 Numbers using Recursion

// recursive function to calculate
// multiplication of two numbers
function product(x, y)
{
    // if x is less than 
    // y swap thenumbers
    if (x < y)
        return product(y, x);

    // iteratively calculate
    // y times sum of x
    else if (y != 0)
        return (x + product(x, y - 1));

    // if any of the two numbers is
    // zero return zero
    else
        return 0;
}

// Driver Code
let x = 5;
let y = 2;
document.write(product(x, y));

// This code is contributed by mohan.

</script>
```

**输出:**

```
10
```