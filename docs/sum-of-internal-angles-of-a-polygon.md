# 多边形内角之和

> 原文:[https://www . geesforgeks . org/多边形内角之和/](https://www.geeksforgeeks.org/sum-of-internal-angles-of-a-polygon/)

给定一个整数 **N** ，任务是求一个 **N 边**多边形的内角之和。一个至少有三条边和三个角的平面图形叫做多边形。
**例:**

> **输入:** N = 3
> **输出:** 180
> 三边多边形为三角形，三角形内角之和
> 为 180。
> **输入:** N = 6
> **输出:** 720

**逼近:**边数为 **N** 的多边形内角之和由**(N–2)* 180**
给出，以下是上述逼近的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of internal
// angles of an n-sided polygon
int sumOfInternalAngles(int n)
{
    if (n < 3)
        return 0;
    return (n - 2) * 180;
}

// Driver code
int main()
{
    int n = 5;

    cout << sumOfInternalAngles(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the sum of internal
    // angles of an n-sided polygon
    static int sumOfInternalAngles(int n)
    {
        if (n < 3)
            return 0;
        return ((n - 2) * 180);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 5;

        System.out.print(sumOfInternalAngles(n));
    }
}
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the sum of internal
    // angles of an n-sided polygon
    static int sumOfInternalAngles(int n)
    {
        if (n < 3)
            return 0;
        return ((n - 2) * 180);
    }

    // Driver code
    public static void Main()
    {
        int n = 5;

        Console.Write(sumOfInternalAngles(n));
    }
}
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the sum of internal
# angles of an n-sided polygon
def sumOfInternalAngles(n):
    if(n < 3):
        return 0
    return ((n - 2) * 180)

# Driver code
n = 5
print(sumOfInternalAngles(n))
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the sum of internal
// angles of an n-sided polygon
function sumOfInternalAngles($n)
{
    if($n < 3)
        return 0;
    return (($n - 2) * 180);
}

// Driver code
$n = 5;
echo(sumOfInternalAngles($n));
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the sum of internal
// angles of an n-sided polygon
function sumOfInternalAngles(n)
{
    if (n < 3)
        return 0;
    return (n - 2) * 180;
}

// Driver code

    let n = 5;

    document.write(sumOfInternalAngles(n));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
540
```