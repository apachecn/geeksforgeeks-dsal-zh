# 将分数降至最低形式

> 原文:[https://www . geeksforgeeks . org/将分数降低到最低形式/](https://www.geeksforgeeks.org/reduce-the-fraction-to-its-lowest-form/)

给定两个整数 **x** 和 **y** ，其中 x 可以被 y 整除，可以用分数 **x/y** 的形式表示。任务是把分数降到最低。
**举例:**

```
Input : x = 16, y = 10
Output : x = 8, y = 5

Input : x = 10, y = 8
Output : x = 5, y = 4
```

**方法:**两个值 **x** 和 **y** 都可以被它们的最大公约数整除。所以如果我们把 x 和 y 从 gcd(x，y)中分开，那么 x 和 y 可以简化成最简单的形式。
以下是上述方法的实现:

## C++

```
// C++ program to reduce a fraction x/y
// to its lowest form

#include <bits/stdc++.h>
using namespace std;

// Function to reduce a fraction to its lowest form
void reduceFraction(int x, int y)
{
    int d;
    d = __gcd(x, y);

    x = x / d;
    y = y / d;

    cout << "x = " << x << ", y = " << y << endl;
}

// Driver Code
int main()
{
    int x = 16;
    int y = 10;

    reduceFraction(x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to reduce a fraction x/y
// to its lowest form
class GFG
{

// Function to reduce a fraction to its lowest form
static void reduceFraction(int x, int y)
{
    int d;
    d = __gcd(x, y);

    x = x / d;
    y = y / d;

    System.out.println("x = " + x + ", y = " + y);
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Driver Code
public static void main(String[] args)
{
    int x = 16;
    int y = 10;

    reduceFraction(x, y);
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to reduce a fraction x/y
# to its lowest form
from math import gcd

# Function to reduce a fraction
# to its lowest form
def reduceFraction(x, y) :

    d = gcd(x, y);

    x = x // d;
    y = y // d;

    print("x =", x, ", y =", y);

# Driver Code
if __name__ == "__main__" :

    x = 16;
    y = 10;

    reduceFraction(x, y);

# This code is contributed by Ryuga
```

## C#

```
// C# program to reduce a fraction x/y
// to its lowest form
using System;

class GFG
{

// Function to reduce a fraction to its lowest form
static void reduceFraction(int x, int y)
{
    int d;
    d = __gcd(x, y);

    x = x / d;
    y = y / d;

    Console.WriteLine("x = " + x + ", y = " + y);
}

static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Driver Code
public static void Main(String[] args)
{
    int x = 16;
    int y = 10;

    reduceFraction(x, y);
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to reduce a fraction x/y
// to its lowest form

// Function to reduce a fraction to its lowest form
function reduceFraction($x, $y)
{
    $d;
    $d = __gcd($x, $y);

    $x = $x / $d;
    $y = $y / $d;

    echo("x = " . $x . ", y = " . $y);
}

function __gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return __gcd($b, $a % $b);

}

// Driver Code
$x = 16;
$y = 10;

reduceFraction($x, $y);

// This code is contributed by Rajput-Ji
?>
```

## java 描述语言

```
<script>

// Javascript program to reduce a fraction x/y
// to its lowest form

// Function to reduce a fraction to its lowest form
function reduceFraction(x, y)
{
    let d;
    d = __gcd(x, y);

    x = parseInt(x / d);
    y = parseInt(y / d);

    document.write("x = " + x + ", y = " + y);
}

function __gcd(a, b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);

}

// Driver Code
    let x = 16;
    let y = 10;

    reduceFraction(x, y);

</script>
```

**输出**:

```
x = 8, y = 5
```