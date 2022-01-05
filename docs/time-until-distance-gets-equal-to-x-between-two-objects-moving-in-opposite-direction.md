# 两个反向运动的物体之间的距离达到 X 的时间

> 原文:[https://www . geesforgeks . org/time-to-distance-get-equal-x-在两个物体之间-反向移动/](https://www.geeksforgeeks.org/time-until-distance-gets-equal-to-x-between-two-objects-moving-in-opposite-direction/)

考虑两个人分别以 **U 米/秒**和 **V 米/秒**的速度反向移动。任务是找出需要多长时间才能使它们之间的距离达到 X 米。
**例:**

> **输入:** U = 3，V = 3，X = 3
> **输出:**0.5
> 0.5 秒后，A 民警距离 1.5 米
> 与 B 民警距离 1.5 米方向相反
> 两民警距离为 1.5 + 1.5 = 3
> **输入:** U = 5，V = 2，X = 4
> **输出:** 0

**进场:**可以用**距离=速度*时间**求解。这里，距离将等于给定的范围，即**距离= X** ，速度将是两个速度的总和，因为它们以相反的方向移动，即**速度= U + V** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the time for which
// the two policemen can communicate
double getTime(int u, int v, int x)
{
    double speed = u + v;

    // time = distance / speed
    double time = x / speed;
    return time;
}

// Driver code
int main()
{
    double u = 3, v = 3, x = 3;
    cout << getTime(u, v, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the time for which
    // the two policemen can communicate
    static double getTime(int u, int v, int x)
    {
        double speed = u + v;

        // time = distance / speed
        double time = x / speed;
        return time;
    }

    // Driver code
    public static void main(String[] args)
    {
        int u = 3, v = 3, x = 3;
        System.out.println(getTime(u, v, x));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the time
# for which the two policemen
# can communicate
def getTime(u, v, x):

    speed = u + v

    # time = distance / speed
    time = x / speed
    return time

# Driver code
if __name__ == "__main__":

    u, v, x = 3, 3, 3
    print(getTime(u, v, x))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the time for which
    // the two policemen can communicate
    static double getTime(int u, int v, int x)
    {
        double speed = u + v;

        // time = distance / speed
        double time = x / speed;
        return time;
    }

    // Driver code
    public static void Main()
    {
        int u = 3, v = 3, x = 3;
        Console.WriteLine(getTime(u, v, x));
    }
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the time for which
// the two policemen can communicate
function getTime($u, $v, $x)
{
    $speed = $u + $v;

    // time = distance / speed
    $time = $x / $speed;
    return $time;
}

// Driver code
$u = 3; $v = 3; $x = 3;
echo getTime($u, $v, $x);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// JavaScript implementation of the approach

// Function to return the time for which
// the two policemen can communicate
function getTime(u, v, x)
{
    let speed = u + v;

    // time = distance / speed
    let time = x / speed;
    return time;
}

// Driver code
    let u = 3, v = 3, x = 3;
    document.write(getTime(u, v, x));

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
0.5
```