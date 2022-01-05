# 环形道路上不同交汇点的数量

> 原文:[https://www . geeksforgeeks . org/环形道路上不同会议点的数量/](https://www.geeksforgeeks.org/number-of-distinct-meeting-points-on-a-circular-road/)

考虑两辆车 **A** 和 **B** ，在环形道路上无限行驶(顺时针或逆时针)。考虑到这两辆车的速度 **a** 和 **b** 。如果 a 或 b 为正，表示它们顺时针方向移动，否则它们逆时针方向移动。任务是找出他们会在多少个不同的点相遇。
**举例:**

```
Input : a = 1, b = -1
Output : 2

Explanation
Car A is moving clockwise while Car B is moving anti-clockwise but their
speeds are same, so they will meet at two points i.e at the starting point
and diametrically corresponding opposite point on the road.

Input : a = 1, b = 2
Output : 1
```

**前提条件**:[【gcd】](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)|[【LCM】](https://www.geeksforgeeks.org/c-program-find-lcm-two-numbers/)

**逼近** :
让环形路的周长为 **d** 。
让汽车所花费的时间 **A** 和 **B** 分别为**t<sub>A</sub>T13】和**t<sub>B</sub>T17】。它们的相对速度是**a–b**。
**A** 和 **B** 从起点出发，一段时间后，他们会在起点再次相遇。这个时间可以通过**t<sub>a</sub>T30】和**t<sub>b</sub>T34】的 **LCM** 来计算。在这段时间内，他们可能会在某个需要查明的点相遇。注意，在他们在起点相遇后，他们会继续在同一点相遇。
在起点再次相遇所需的时间将为:******** 

```
T1 = LCM(ta, tb) = LCM(d/a, d/b) = d/GCD(a, b)
```

让他们在时间周期 T <sub>1</sub> 内相遇 **N** 次。
所以，他们连续相遇之间的时间延迟是，比方说 T <sub>2</sub> 可以计算为，

> T <sub>2</sub> = (T <sub>1</sub> / N)。
> 这个时间可以通过计算他们开始后第一次见面的时间来计算。
> 所以，他们第一次见面的时间，
> 所以，T<sub>2</sub>=(d/(a–b))。
> 将 T <sub>1</sub> 除以 T <sub>2</sub> ，我们得到，
> **N =(T<sub>1</sub>/T<sub>2</sub>)=((a–b)/GCD(a，b))**

以下是上述方法的实现:

## C++

```
// CPP Program to find number of distinct point of meet on a circular road
#include <bits/stdc++.h>
using namespace std;

// Returns the GCD of two number.
int gcd(int a, int b)
{
    int c = a % b;
    while (c != 0) {
        a = b;
        b = c;
        c = a % b;
    }
    return b;
}

// Returns the number of distinct meeting points.
int numberOfmeet(int a, int b)
{
    int ans;

    // Find the relative speed.
    if (a > b)
        ans = a - b;
    else
        ans = b - a;

    // convert the negative value to positive.
    if (a < 0)
        a = a * (-1);

    if (b < 0)
        b = b * (-1);

    return ans / gcd(a, b);
}

// Driver Code
int main()
{
    int a = 1, b = -1;

    cout << numberOfmeet(a, b) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find number
// of distinct point of meet
// on a circular road
import java.io.*;

class GFG
{

// Returns the GCD
// of two number.
static int gcd(int a, int b)
{
    int c = a % b;
    while (c != 0)
    {
        a = b;
        b = c;
        c = a % b;
    }
    return b;
}

// Returns the number of
// distinct meeting points.
static int numberOfmeet(int a,
                        int b)
{
    int ans;

    // Find the relative speed.
    if (a > b)
        ans = a - b;
    else
        ans = b - a;

    // convert the negative
    // value to positive.
    if (a < 0)
        a = a * (-1);

    if (b < 0)
        b = b * (-1);

    return ans / gcd(a, b);
}

// Driver Code
public static void main (String[] args)
{
    int a = 1, b = -1;
    System.out.println(numberOfmeet(a, b));
}
}

// This code is contributed by @ajit
```

## 蟒蛇 3

```
# Python3 Program to find
# number of distinct point
# of meet on a circular road
import math

# Returns the number of
# distinct meeting points.
def numberOfmeet(a, b):
    ans = 0;

    # Find the relative speed.
    if (a > b):
        ans = a - b;
    else:
        ans = b - a;

    # convert the negative
    # value to positive.
    if (a < 0):
        a = a * (-1);
    if (b < 0):
        b = b * (-1);
    return int(ans / math.gcd(a, b));

# Driver Code
a = 1;
b = -1;
print(numberOfmeet(a, b));

# This code is contributed by mits
```

## C#

```
// C# Program to find number
// of distinct point of meet
// on a circular road
using System;

class GFG
{

// Returns the GCD
// of two number.
static int gcd(int a, int b)
{
    int c = a % b;
    while (c != 0)
    {
        a = b;
        b = c;
        c = a % b;
    }
    return b;
}

// Returns the number of
// distinct meeting points.
static int numberOfmeet(int a,
                        int b)
{
    int ans;

    // Find the relative speed.
    if (a > b)
        ans = a - b;
    else
        ans = b - a;

    // convert the negative
    // value to positive.
    if (a < 0)
        a = a * (-1);

    if (b < 0)
        b = b * (-1);

    return ans / gcd(a, b);
}

// Driver Code
static public void Main ()
{
    int a = 1, b = -1;
    Console.WriteLine(
            numberOfmeet(a, b));
}
}

// This code is contributed
// by @ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find number
// of distinct point of meet
// on a circular road

// Returns the GCD of two number.
function gcd($a, $b)
{
    $c = $a % $b;
    while ($c != 0)
    {
        $a = $b;
        $b = $c;
        $c = $a % $b;
    }
    return $b;
}

// Returns the number of
// distinct meeting points.
function numberOfmeet($a, $b)
{
    $ans;

    // Find the relative speed.
    if ($a > $b)
        $ans = $a - $b;
    else
        $ans = $b - $a;

    // convert the negative
    // value to positive.
    if ($a < 0)
        $a = $a * (-1);

    if ($b < 0)
        $b = $b * (-1);

    return $ans / gcd($a, $b);
}

// Driver Code
$a = 1;
$b = -1;

echo numberOfmeet($a, $b)."\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript Program to find number of distinct
// point of meet on a circular road

// Returns the GCD of two number.
function gcd(a, b)
{
    var c = a % b;
    while (c != 0) {
        a = b;
        b = c;
        c = a % b;
    }
    return b;
}

// Returns the number of distinct meeting points.
function numberOfmeet(a, b)
{
    var ans;

    // Find the relative speed.
    if (a > b)
        ans = a - b;
    else
        ans = b - a;

    // convert the negative value to positive.
    if (a < 0)
        a = a * (-1);

    if (b < 0)
        b = b * (-1);

    return ans / gcd(a, b);
}

// Driver Code
var a = 1, b = -1;
document.write( numberOfmeet(a, b));

</script>
```

**输出:**

```
2
```