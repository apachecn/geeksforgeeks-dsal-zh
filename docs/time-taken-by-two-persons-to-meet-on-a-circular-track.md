# 两人在环形轨道上相遇所用的时间

> 原文:[https://www . geeksforgeeks . org/两人环形跑道上相遇的时间/](https://www.geeksforgeeks.org/time-taken-by-two-persons-to-meet-on-a-circular-track/)

给定整数 **L** 、 **S1** 和 **S2** 其中 **L** 是以米为单位的圆形轨道的长度， **S1** 和 **S2** 是两个人在给定轨道上从同一起点开始以公里/小时为单位向同一方向移动的速度。任务是找到以下:

*   他们第一次见面的时间。
*   将在起点相遇的时间。

**例:**

> **输入:** L = 30，S1 = 5，S2 = 2
> **输出:【T10 小时后第一次相遇
> 30 小时后在起点相遇
> T7】输入:** L = 10，S1 = 1，S2 = 2
> **输出:**10 小时后第一次相遇
> 10 小时后在起点相遇

**进场:**

*   计算他们第一次见面的时间。
    *   首先计算相对速度，即**S1-S2**。
    *   然后用公式**时间=距离/相对速度**。
*   计算他们在起点再次相遇的时间。
    *   首先，用公式**时间=轨迹长度/速度**计算出两者覆盖一轮圆形轨迹所需的时间，即 **T1** 和 **T2** 。
    *   然后计算 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 知道他们在起点再次相遇的时间。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the time when both the
// persons will meet at the starting point
int startingPoint(int Length, int Speed1, int Speed2)
{
    int result1 = 0, result2 = 0;

    // Time to cover 1 round by both
    int time1 = Length / Speed1;
    int time2 = Length / Speed2;

    result1 = __gcd(time1, time2);

    // Finding LCM to get the meeting point
    result2 = time1 * time2 / (result1);

    return result2;
}

// Function to return the time when both
// the persons will meet for the first time
float firstTime(int Length, int Speed1, int Speed2)
{
    float result = 0;

    int relativeSpeed = abs(Speed1 - Speed2);

    result = ((float)Length / relativeSpeed);

    return result;
}

// Driver Code
int main()
{
    int L = 30, S1 = 5, S2 = 2;

    // Calling function
    float first_Time = firstTime(L, S1, S2);
    int starting_Point = startingPoint(L, S1, S2);

    cout << "Met first time after "
         << first_Time << " hrs" << endl;
    cout << "Met at starting point after "
         << starting_Point << " hrs" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
public class GFG {

// Function to return the time when both the
// persons will meet at the starting point
    static int startingPoint(int Length, int Speed1, int Speed2) {
        int result1 = 0, result2 = 0;

        // Time to cover 1 round by both
        int time1 = Length / Speed1;
        int time2 = Length / Speed2;

        result1 = __gcd(time1, time2);

        // Finding LCM to get the meeting point
        result2 = time1 * time2 / (result1);

        return result2;
    }

    static int __gcd(int a, int b) {
        if (b == 0) {
            return a;
        }
        return __gcd(b, a % b);

    }
// Function to return the time when both
// the persons will meet for the first time

    static float firstTime(int Length, int Speed1, int Speed2) {
        float result = 0;

        int relativeSpeed = Math.abs(Speed1 - Speed2);

        result = ((float) Length / relativeSpeed);

        return result;
    }

// Driver Code
    public static void main(String[] args) {
        int L = 30, S1 = 5, S2 = 2;

        // Calling function
        float first_Time = firstTime(L, S1, S2);
        int starting_Point = startingPoint(L, S1, S2);

        System.out.println("Met first time after "
                + first_Time + " hrs");
        System.out.println("Met at starting point after "
                + starting_Point + " hrs");

    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach

# import gcd() from math lib
from math import gcd

# Function to return the time when both the
# persons will meet at the starting point
def startingPoint(Length, Speed1, Speed2) :

    result1 = 0
    result2 = 0

    # Time to cover 1 round by both
    time1 = Length // Speed1
    time2 = Length // Speed2

    result1 = gcd(time1, time2)

    # Finding LCM to get the meeting point
    result2 = time1 * time2 // (result1)

    return result2

# Function to return the time when both
# the persons will meet for the first time
def firstTime(Length, Speed1, Speed2) :

    result = 0

    relativeSpeed = abs(Speed1 - Speed2)

    result = Length / relativeSpeed

    return result

# Driver Code
if __name__ == "__main__" :

    L = 30
    S1 = 5
    S2 = 2

    # Calling function
    first_Time = firstTime(L, S1, S2)
    starting_Point = startingPoint(L, S1, S2)

    print("Met first time after", first_Time, "hrs")
    print("Met at starting point after",
                  starting_Point, "hrs")

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of above approach
using System;

public class GFG {

// Function to return the time when both the
// persons will meet at the starting point
    static int startingPoint(int Length, int Speed1, int Speed2) {
        int result1 = 0, result2 = 0;

        // Time to cover 1 round by both
        int time1 = Length / Speed1;
        int time2 = Length / Speed2;

        result1 = __gcd(time1, time2);

        // Finding LCM to get the meeting point
        result2 = time1 * time2 / (result1);

        return result2;
    }

    static int __gcd(int a, int b) {
        if (b == 0) {
            return a;
        }
        return __gcd(b, a % b);

    }
// Function to return the time when both
// the persons will meet for the first time

    static float firstTime(int Length, int Speed1, int Speed2) {
        float result = 0;

        int relativeSpeed = Math.Abs(Speed1 - Speed2);

        result = ((float) Length / relativeSpeed);

        return result;
    }

// Driver Code
    public static void Main() {
        int L = 30, S1 = 5, S2 = 2;

        // Calling function
        float first_Time = firstTime(L, S1, S2);
        int starting_Point = startingPoint(L, S1, S2);

        Console.WriteLine("Met first time after "
                + first_Time + " hrs");
        Console.WriteLine("Met at starting point after "
                + starting_Point + " hrs");

    }
}
/*This code is contributed by 29AjayKumar*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

function gcd ($a, $b)
{
    return $b ? gcd($b, $a % $b) : $a;
}

// Function to return the time
// when both the persons will
// meet at the starting point
function startingPoint($Length, $Speed1,
                                $Speed2)
{
    $result1 = 0;
    $result2 = 0;

    // Time to cover 1 round by both
    $time1 = $Length / $Speed1;
    $time2 = $Length / $Speed2;

    $result1 = gcd($time1, $time2);

    // Finding LCM to get the
    // meeting point
    $result2 = $time1 * $time2 / ($result1);

    return $result2;
}

// Function to return the time when both
// the persons will meet for the first time
function firstTime($Length, $Speed1, $Speed2)
{
    $result = 0;

    $relativeSpeed = abs($Speed1 - $Speed2);

    $result = ((float)$Length /
                      $relativeSpeed);

    return $result;
}

// Driver Code
$L = 30;
$S1 = 5;
$S2 = 2;

// Calling function
$first_Time = firstTime($L, $S1, $S2);
$starting_Point = startingPoint($L, $S1, $S2);

echo "Met first time after ".
    $first_Time ." hrs" ."\n";
echo "Met at starting point after ".
    $starting_Point . " hrs" ."\n";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// javascript implementation of above approach

    // Function to return the time when both the
    // persons will meet at the starting point
    function startingPoint(Length , Speed1 , Speed2)
    {
        var result1 = 0, result2 = 0;

        // Time to cover 1 round by both
        var time1 = Length / Speed1;
        var time2 = Length / Speed2;

        result1 = __gcd(time1, time2);

        // Finding LCM to get the meeting point
        result2 = time1 * time2 / (result1);

        return result2;
    }

    function __gcd(a , b)
    {
        if (b == 0)
        {
            return a;
        }
        return __gcd(b, a % b);

    }

    // Function to return the time when both
    // the persons will meet for the first time
    function firstTime(Length , Speed1 , Speed2)
    {
        var result = 0;
        var relativeSpeed = Math.abs(Speed1 - Speed2);
        result = ( Length / relativeSpeed);
        return result;
    }

    // Driver Code   
    var L = 30, S1 = 5, S2 = 2;

        // Calling function
        var first_Time = firstTime(L, S1, S2);
        var starting_Point = startingPoint(L, S1, S2);

        document.write("Met first time after " + first_Time + " hrs<br/>");
        document.write("Met at starting point after " + starting_Point + " hrs");

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
Met first time after 10 hrs
Met at starting point after 30 hrs
```

**时间复杂度:** O(1)

**辅助空间:** O(1)