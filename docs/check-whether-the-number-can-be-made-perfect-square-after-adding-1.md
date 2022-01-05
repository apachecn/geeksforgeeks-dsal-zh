# 加 1 后检查数字是否可以做成完美的正方形

> 原文:[https://www . geesforgeks . org/check-number-can-make-perfect-square-after-add-1/](https://www.geeksforgeeks.org/check-whether-the-number-can-be-made-perfect-square-after-adding-1/)

给定一个整数 **N** ，任务是检查给定数字加 1 后 **N** 是否能做成一个完美的正方形。

**示例:**

> **输入:**3
> T3】输出:是
> 3 + 1 = 4 这是一个完美的正方形即 2 <sup>2</sup>
> 
> **输入:**5
> T3】输出:否
> 5 + 1 = 6 这不是一个完美的正方形。

**逼近:**取 **n + 1** 的平方根，检查 **n + 1** 是否是一个完美的正方形。如果是，那么 **n + 1** 是一个完美的正方形， **n** 是一个阳光的数字。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true
// if x is a perfect square
bool isPerfectSquare(long double x)
{

    // Find floating point value of
    // square root of x
    long double sr = sqrt(x);

    // If square root is an integer
    return ((sr - floor(sr)) == 0);
}

// Function that returns true
// if n is a sunny number
bool isSunnyNum(int n)
{

    // If (n + 1) is a perfect square
    if (isPerfectSquare(n + 1))
        return true;
    return false;
}

// Driver code
int main()
{
    int n = 3;

    if (isSunnyNum(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function that returns true
    // if x is a perfect square
    static boolean isPerfectSquare(double x)
    {

        // Find floating point value of
        // square root of x
        double sr = Math.sqrt(x);

        // If square root is an integer
        return ((sr - Math.floor(sr)) == 0);
    }

    // Function that returns true
    // if n is a sunny number
    static boolean isSunnyNum(int n)
    {

        // If (n + 1) is a perfect square
        if (isPerfectSquare(n + 1))
            return true;
        return false;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 3;

        if (isSunnyNum(n))
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math as mt

# Function that returns true
# if x is a perfect square
def isPerfectSquare(x):

    # Find floating po value of
    # square root of x
    sr = mt.sqrt(x)

    # If square root is an eger
    return ((sr - mt.floor(sr)) == 0)

# Function that returns true
# if n is a sunny number
def isSunnyNum(n):

    # If (n + 1) is a perfect square
    if (isPerfectSquare(n + 1)):
        return True
    return False

# Driver code
n = 3

if (isSunnyNum(n)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

    // Function that returns true
    // if x is a perfect square
    static bool isPerfectSquare(double x)
    {

        // Find floating point value of
        // square root of x
        double sr = Math.Sqrt(x);

        // If square root is an integer
        return ((sr - Math.Floor(sr)) == 0);
    }

    // Function that returns true
    // if n is a sunny number
    static bool isSunnyNum(int n)
    {

        // If (n + 1) is a perfect square
        if (isPerfectSquare(n + 1))
            return true;
        return false;
    }

    // Driver code
    public static void Main ()
    {
        int n = 3;

        if (isSunnyNum(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true
// if x is a perfect square
function isPerfectSquare($x)
{

    // Find floating point value of
    // square root of x
    $sr = sqrt($x);

    // If square root is an integer
    return (($sr - floor($sr)) == 0);
}

// Function that returns true
// if n is a sunny number
function isSunnyNum($n)
{

    // If (n + 1) is a perfect square
    if (isPerfectSquare($n + 1))
        return true;
    return false;
}

// Driver code
$n = 3;

if (isSunnyNum($n))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true
// if x is a perfect square
function isPerfectSquare(x)
{

    // Find floating point value of
    // square root of x
    let sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function that returns true
// if n is a sunny number
function isSunnyNum(n)
{

    // If (n + 1) is a perfect square
    if (isPerfectSquare(n + 1))
        return true;

    return false;
}

// Driver code
let n = 3;

if (isSunnyNum(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
Yes
```