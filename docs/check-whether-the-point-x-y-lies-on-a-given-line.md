# 检查点(x，y)是否位于给定的线上

> 原文:[https://www . geesforgeks . org/check-the-point-x-y-lies-on-给定线路/](https://www.geeksforgeeks.org/check-whether-the-point-x-y-lies-on-a-given-line/)

给定直线方程的 **m** 和 **c** 的值 **y = (m * x) + c** ，任务是找出点 **(x，y)** 是否位于给定直线上。

**示例:**

> **输入:** m = 3，c = 2，x = 1，y = 5
> **输出:**是
> m * x + c = 3 * 1 + 2 = 3 + 2 = 5 等于 y
> 因此，给定点满足直线方程
> 
> **输入:** m = 5，c = 2，x = 2，y = 5
> T3】输出:否

**逼近:**为了给定点位于直线上，它必须满足直线方程。检查 **y = (m * x) + c** 是否成立。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that return true if
// the given point lies on the given line
bool pointIsOnLine(int m, int c, int x, int y)
{
    // If (x, y) satisfies the equation of the line
    if (y == ((m * x) + c))
        return true;

    return false;
}

// Driver code
int main()
{
    int m = 3, c = 2;
    int x = 1, y = 5;

    if (pointIsOnLine(m, c, x, y))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

// Function that return true if
// the given point lies on the given line
static boolean pointIsOnLine(int m, int c,
                        int x, int y)
{
    // If (x, y) satisfies the equation
    // of the line
    if (y == ((m * x) + c))
        return true;

    return false;
}

// Driver code
public static void main(String[] args)
{
    int m = 3, c = 2;
    int x = 1, y = 5;

    if (pointIsOnLine(m, c, x, y))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that return true if the
# given point lies on the given line
def pointIsOnLine(m, c, x, y):

    # If (x, y) satisfies the
    # equation of the line
    if (y == ((m * x) + c)):
        return True;

    return False;

# Driver code
m = 3; c = 2;
x = 1; y = 5;

if (pointIsOnLine(m, c, x, y)):
    print("Yes");
else:
    print("No");

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that return true if
// the given point lies on the given line
static bool pointIsOnLine(int m, int c,
                          int x, int y)
{
    // If (x, y) satisfies the equation
    // of the line
    if (y == ((m * x) + c))
        return true;

    return false;
}

// Driver code
public static void Main()
{
    int m = 3, c = 2;
    int x = 1, y = 5;

    if (pointIsOnLine(m, c, x, y))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that return true if the
// given point lies on the given line
function pointIsOnLine($m, $c, $x, $y)
{

    // If (x, y) satisfies the equation
    // of the line
    if ($y == (($m * $x) + $c))
        return true;

    return false;
}

// Driver code
$m = 3; $c = 2;
$x = 1; $y = 5;

if (pointIsOnLine($m, $c, $x, $y))
    echo "Yes";
else
    echo "No";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that return true if
// the given point lies on the given line
function pointIsOnLine(m, c, x, y)
{

    // If (x, y) satisfies the equation
    // of the line
    if (y == ((m * x) + c))
        return true;

    return false;
}

// Driver code
var m = 3, c = 2;
var x = 1, y = 5;

if (pointIsOnLine(m, c, x, y))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by Rajput-Ji

</script>
```

**Output:** 

```
Yes
```