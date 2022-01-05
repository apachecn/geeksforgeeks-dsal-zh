# 求最接近 a^b 的 x 的倍数

> 原文:[https://www . geesforgeks . org/find-x 的倍数最接近 ab/](https://www.geeksforgeeks.org/find-the-multiple-of-x-which-is-closest-to-ab/)

给定三个整数 **a** 、 **b** 、 **x** ，任务是得到最接近 **a <sup>b</sup>** 的 **x** 的倍数。
**示例:**

> **输入:** a = 5，b = 4，x = 3
> **输出:** 624
> 5 <sup>4</sup> = 625，624 是最接近 625
> **的 3 的倍数输入:** a = 349，b = 1，x = 4
> **输出:** 348

**进场:**

*   计算**a<sup>b</sup>T3，并将其存储在变量 say **num** 中。**
*   然后，计算 **⌊num / x⌋** 并将其存储在变量**楼层**中。
*   现在左边最近的元素将是 **closestLeft = x * floor** 。
*   右边最接近的元素是 **closestRight = x *(楼层+ 1)** 。
*   最后，其中最接近的数字将是**min(num–closestLeft，closestRight–num)**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the multiple of x
// which is closest to a^b
ll getClosest(int a, int b, int x)
{
    ll num = pow(a, b);

    int floor = num / x;

    // Closest element on the left
    ll numOnLeft = x * floor;

    // Closest element on the right
    ll numOnRight = x * (floor + 1);

    // If numOnLeft is closer than numOnRight
    if ((num - numOnLeft) < (numOnRight - num))
        return numOnLeft;

    // If numOnRight is the closest
    else
        return numOnRight;
}

// Driver code
int main()
{
    int a = 349, b = 1, x = 4;
    cout << getClosest(a, b, x) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach

public class GFG {

// Function to return the multiple of x
// which is closest to a^b
    static long getClosest(int a, int b, int x) {
        long num = (long) Math.pow(a, b);

        int floor = (int) (num / x);

        // Closest element on the left
        long numOnLeft = x * floor;

        // Closest element on the right
        long numOnRight = x * (floor + 1);

        // If numOnLeft is closer than numOnRight
        if ((num - numOnLeft) < (numOnRight - num)) {
            return numOnLeft;
        } // If numOnRight is the closest
        else {
            return numOnRight;
        }
    }

    public static void main(String[] args) {
        int a = 349, b = 1, x = 4;
        System.out.println(getClosest(a, b, x));

    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the multiple of x
# which is closest to a^b
def getClosest(a, b, x) :
    num = pow(a, b)

    floor = num // x

    # Closest element on the left
    numOnLeft = x * floor

    # Closest element on the right
    numOnRight = x * (floor + 1)

    # If numOnLeft is closer than numOnRight
    if ((num - numOnLeft) <
        (numOnRight - num)):
        return numOnLeft

    # If numOnRight is the closest
    else :
        return numOnRight

# Driver code
if __name__ == "__main__" :

    a, b, x = 349, 1, 4
    print(getClosest(a, b, x))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

// #define ll long long int

class GFG
{
// Function to return the multiple of x
// which is closest to a^b
static long getClosest(int a, int b, int x)
{
    int num = (int)Math.Pow(a, b);

    int floor = (int)(num / x);

    // Closest element on the left
    int numOnLeft = (int)(x * floor);

    // Closest element on the right
    int numOnRight = (int)(x * (floor + 1));

    // If numOnLeft is closer than numOnRight
    if ((num - numOnLeft) < (numOnRight - num))
        return numOnLeft;

    // If numOnRight is the closest
    else
        return numOnRight;
}

// Driver code
public static void Main()
{
    int a = 349, b = 1, x = 4;
    Console.WriteLine(getClosest(a, b, x));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return the multiple of x
// which is closest to a^b
function getClosest($a, $b, $x)
{
    $num = pow($a, $b);

    $floor = (int)($num / $x);

    // Closest element on the left
    $numOnLeft = $x * $floor;

    // Closest element on the right
    $numOnRight = $x * ($floor + 1);

    // If numOnLeft is closer than numOnRight
    if (($num - $numOnLeft) <
        ($numOnRight - $num))
        return $numOnLeft;

    // If numOnRight is the closest
    else
        return ceil($numOnRight);
}

// Driver code
$a = 349;
$b = 1;
$x = 4;
echo getClosest($a, $b, $x);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the multiple of x
// which is closest to a^b
function getClosest( a,  b,  x)
{
    let num = Math.pow(a, b);

    let floor = Math.floor(num / x);

    // Closest element on the left
    let numOnLeft = x * floor;

    // Closest element on the right
    let numOnRight = x * (floor + 1);

    // If numOnLeft is closer than numOnRight
    if ((num - numOnLeft) < (numOnRight - num))
        return numOnLeft;

    // If numOnRight is the closest
    else
        return numOnRight;
}

    // Driver Code

    let a = 349, b = 1, x = 4;
    document.write(getClosest(a, b, x) + "</br>");

</script>
```

**Output:** 

```
348
```