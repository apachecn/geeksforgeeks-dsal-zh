# 加到 X 上的最小值，至少是 N 的 Y %

> 原文:[https://www . geeksforgeeks . org/最低增值率/至少为 y % n/](https://www.geeksforgeeks.org/minimum-value-to-be-added-to-x-such-that-it-is-at-least-y-percent-of-n/)

给定三个整数 **N** 、 **X** 和 **Y** ，任务是找出应该加到 **X** 上的最小整数，使其至少为 **N** 的 **Y** 。

**示例:**

> **输入:** N = 10，X = 2，Y = 40
> **输出:**2
> X 加 2 得到 4，4 是 10 的 40%
> 
> **输入:** N = 10，X = 2，Y = 20
> **输出:** 0
> X 已经是 10 的 20%

**方法:**找到**值= (N * Y) / 100** ，这是 **N** 的 **Y** 百分比。现在为了使 **X** 等于 **val** ，**val–X**必须加到 **X** 上，前提是 **X < val** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required value
// that must be added to x so that
// it is at least y percent of n
int minValue(int n, int x, int y)
{

    // Required value
    float val = (y * n) / 100;

    // If x is already >= y percent of n
    if (x >= val)
        return 0;
    else
        return (ceil(val) - x);
}

// Driver code
int main()
{
    int n = 10, x = 2, y = 40;
    cout << minValue(n, x, y);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.lang.Math;

class GFG
{

// Function to return the required value
// that must be added to x so that
// it is at least y percent of n
static int minValue(int n, int x, int y)
{

    // Required value
    float val = (y * n) / 100;

    // If x is already >= y percent of n
    if (x >= val)
        return 0;
    else
        return (int)(Math.ceil(val)-x);
}

// Driver code
public static void main(String[] args)
{
    int n = 10, x = 2, y = 40;
    System.out.println(minValue(n, x, y));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
import math

# Function to return the required value
# that must be added to x so that
# it is at least y percent of n
def minValue(n, x, y):

    # Required value
    val = (y * n)/100

    # If x is already >= y percent of n
    if x >= val:
        return 0
    else:
        return math.ceil(val) - x

# Driver code
n = 10; x = 2; y = 40
print(minValue(n, x, y))

# This code is contributed by Shrikant13
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the required value
    // that must be added to x so that
    // it is at least y percent of n
    static int minValue(int n, int x, int y)
    {

        // Required value
        float val = (y * n) / 100;

        // If x is already >= y percent of n
        if (x >= val)
            return 0;
        else
            return (int)(Math.Ceiling(val)-x) ;
    }

    // Driver code
    public static void Main()
    {
        int n = 10, x = 2, y = 40;
        Console.WriteLine((int)minValue(n, x, y));
    }
}

// This code is contributed by Ryuga.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// php implementation of the approach
// Function to return the required value
// that must be added to x so that
// it is at least y percent of n
function minValue($n, $x, $y)
{

    // Required value
    $val = ($y * $n) / 100;

    // If x is already >= y percent of n
    if ($x >= $val)
        return 0;
    else
        return (ceil($val) - $x);
}

// Driver code
{
    $n = 10; $x = 2; $y = 40;
    echo(minValue($n, $x, $y));
}

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the required value
// that must be added to x so that
// it is at least y percent of n
function minValue(n, x, y)
{

    // Required value
    let val = (y * n) / 100;

    // If x is already >= y percent of n
    if (x >= val)
        return 0;
    else
        return (Math.ceil(val) - x);
}

// Driver code
let n = 10, x = 2, y = 40;

document.write(minValue(n, x, y));

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(1)