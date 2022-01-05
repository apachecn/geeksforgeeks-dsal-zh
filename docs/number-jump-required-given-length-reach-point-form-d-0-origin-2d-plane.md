# 从 2D 平面原点到达形式点(d，0)所需的给定长度的跳跃次数

> 原文:[https://www . geesforgeks . org/number-jump-required-给定长度-到达点-form-d-0-origin-2d-plane/](https://www.geeksforgeeks.org/number-jump-required-given-length-reach-point-form-d-0-origin-2d-plane/)

给定三个正整数 **a，b** 和 **d** 。您当前位于无限 2D 坐标平面上的原点(0，0)。你可以在 2D 平面上的任意点上跳跃，距离你当前位置的欧几里得距离等于 **a** 或 **b** 。任务是找到从(0，0)到达(d，0)所需的最小跳转次数。
示例:

```
Input : a = 2, b = 3, d = 1 
Output : 2
First jump of length a = 2, (0, 0) -> (1/2, √15/2)
Second jump of length a = 2, (1/2, √15/2) -> (1, 0)
Thus, only two jump are required to reach 
(1, 0) from (0, 0).

Input : a = 3, b = 4, d = 11 
Output : 3
(0, 0) -> (4, 0) using length b = 4
(4, 0) -> (8, 0) using length b = 4
(8, 0) -> (11, 0) using length a = 3
```

首先，观察我们不需要找到中间点，我们只需要所需的最小跳跃次数。
因此，从(0，0)开始，我们将沿着(d，0)的方向移动，即垂直移动，长度的跳跃等于 **max(a，b)** ，直到当前位置坐标和(d，0)之间的欧几里得距离变得小于 **max(a，b)** 或等于 0。这将使每次跳跃所需的最小跳跃次数增加 1。所以这个值可以通过**楼层(d/max(a，b))** 找到。
现在，对于剩下的距离，如果(d，0)是 **a** 欧几里得距离，我们将进行一次长度为 **a** 的跳跃，到达(d，0)。因此，在这种情况下，所需的最小跳跃次数将增加 1。
现在来解决剩余距离不等于 **a** 的情况。让剩下的距离为 **x** 。另外，观察 x 将大于 0 且小于**最大值(a，b)** ，因此，0<x<2 *最大值(a，b)。我们可以分两步到达(d，0)。
**如何？**
让我们试着建立一个三角形 ABC，这样 A 是我们当前的位置，B 是目标位置，即(d，0)，C 是点，这样 AC = BC = max(a，B)。而这对于三角形是可能的，因为两边 AC + BC 之和大于三边 AB。所以，一个跳转是从 A 到 C，另一个跳转是从 C 到 b
下面是这个方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Return the minimum jump of length either a or b
// required to reach (d, 0) from (0, 0).
int minJumps(int a, int b, int d)
{
    // Assigning maximum of a and b to b
    // and assigning minimum of a and b to a.
    int temp = a;
    a = min(a, b);
    b = max(temp, b);

    // if d is greater than or equal to b.
    if (d >= b)
        return (d + b - 1) / b;

    // if d is 0
    if (d == 0)
        return 0;

    // if d is equal to a.
    if (d == a)
        return 1;

    // else make triangle, and only 2
    // steps required.
    return 2;
}

int main()
{
    int a = 3, b = 4, d = 11;
    cout << minJumps(a, b, d) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the minimum number
// of jump required to reach
// (d, 0) from (0, 0).
import java.io.*;

class GFG {

    // Return the minimum jump of length either a or b
    // required to reach (d, 0) from (0, 0).
    static int minJumps(int a, int b, int d)
    {
        // Assigning maximum of a and b to b
        // and assigning minimum of a and b to a.
        int temp = a;
        a = Math.min(a, b);
        b = Math.max(temp, b);

        // if d is greater than or equal to b.
        if (d >= b)
            return (d + b - 1) / b;

        // if d is 0
        if (d == 0)
            return 0;

        // if d is equal to a.
        if (d == a)
            return 1;

        // else make triangle, and only 2
        // steps required.
        return 2;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a = 3, b = 4, d = 11;
        System.out.println(minJumps(a, b, d));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 code to find the minimum
# number of jump required to reach
# (d, 0) from (0, 0)

def minJumps(a, b, d):

    temp = a
    a = min(a, b)
    b = max(temp, b)

    if (d >= b):
        return (d + b - 1) / b

    # if d is 0
    if (d == 0):
        return 0

    # if d is equal to a.
    if (d == a):
        return 1

    # else make triangle, and
    # only 2  steps required.
    return 2

# Driver Code
a, b, d = 3, 4, 11
print (int(minJumps(a, b, d)))

# This code is contributed by _omg
```

## C#

```
// C# code to find the minimum number
// of jump required to reach
// (d, 0) from (0, 0).
using System;

class GFG {

    // Return the minimum jump of length either a or b
    // required to reach (d, 0) from (0, 0).
    static int minJumps(int a, int b, int d)
    {
        // Assigning maximum of a and b to b
        // and assigning minimum of a and b to a.
        int temp = a;
        a = Math.Min(a, b);
        b = Math.Max(temp, b);

        // if d is greater than or equal to b.
        if (d >= b)
            return (d + b - 1) / b;

        // if d is 0
        if (d == 0)
            return 0;

        // if d is equal to a.
        if (d == a)
            return 1;

        // else make triangle, and only 2
        // steps required.
        return 2;
    }

    // Driver code
    public static void Main()
    {
        int a = 3, b = 4, d = 11;
        Console.WriteLine(minJumps(a, b, d));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the minimum
// number of jump required to
// reach (d, 0) from (0, 0).

// Return the minimum jump
// of length either a or b
// required to reach (d, 0)
// from (0, 0).
function minJumps( $a, $b, $d)
{

    // Assigning maximum of
    // a and b to b and
    // assigning minimum of
    // a and b to a.
    $temp = $a;
    $a = min($a, $b);
    $b = max($temp, $b);

    // if d is greater than
    // or equal to b.
    if ($d >= $b)
        return ($d + $b - 1) / $b;

    // if d is 0
    if ($d == 0)
        return 0;

    // if d is equal to a.
    if ($d == $a)
        return 1;

    // else make triangle,
    // and only 2
    // steps required.
    return 2;
}

    // Driver Code
    $a = 3;
    $b = 4;
    $d = 11;
    echo floor(minJumps($a, $b, $d));

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript  program to find the minimum number
// of jump required to reach
// (d, 0) from (0, 0).

    // Return the minimum jump of length either a or b
    // required to reach (d, 0) from (0, 0).
    function minJumps(a, b, d)
    {
        // Assigning maximum of a and b to b
        // and assigning minimum of a and b to a.
        let temp = a;
        a = Math.min(a, b);
        b = Math.max(temp, b);

        // if d is greater than or equal to b.
        if (d >= b)
            return (d + b - 1) / b;

        // if d is 0
        if (d == 0)
            return 0;

        // if d is equal to a.
        if (d == a)
            return 1;

        // else make triangle, and only 2
        // steps required.
        return 2;
    }

// Driver Code

        let a = 3, b = 4, d = 11;
        document.write(Math.floor(minJumps(a, b, d)));

</script>
```

**输出:**

```
3
```