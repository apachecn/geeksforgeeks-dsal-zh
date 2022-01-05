# 计算时针和分针之间的角度

> 原文:[https://www . geesforgeks . org/compute-angle-时针-分针/](https://www.geeksforgeeks.org/calculate-angle-hour-hand-minute-hand/)

这个问题被称为[时钟角度问题](http://en.wikipedia.org/wiki/Clock_angle_problem)，我们需要找到模拟时钟在给定时间的指针之间的角度。
**例:**

```
Input: 
h = 12:00
m = 30.00
Output: 
165 degree

Input: 
h = 3.00
m = 30.00
Output: 
75 degree
```

思路是以 12:00 (h = 12，m = 0)为参考。以下是详细的步骤。

1.计算时针相对于 12:00 的角度，以小时和分钟为单位。
2。计算分针相对于 12:00 的角度，以小时和分钟为单位。
3。两个角度的区别就是两只手的角度。

**如何计算相对于 12:00 的两个角度？**
分针 60 分钟移动 360 度(或 1 分钟移动 6 度)，时针 12 小时移动 360 度(或 1 分钟移动 0.5 度)。在 h 小时和 m 分钟内，分针将移动(h*60 + m)*6，时针将移动(h*60 + m)*0.5。

## C++

```
// C++ program to find angle between hour and minute hands
#include <bits/stdc++.h>
using namespace std;

// Utility function to find minimum of two integers
int min(int x, int y)
{
    return (x < y)? x: y;

}

int calcAngle(double h, double m)
{
    // validate the input
    if (h <0 || m < 0 || h >12 || m > 60)
        printf("Wrong input");

    if (h == 12) h = 0;
    if (m == 60)
     {
      m = 0;
      h += 1;
       if(h>12)
        h = h-12;
     }

    // Calculate the angles moved
    // by hour and minute hands
    // with reference to 12:00
    float hour_angle = 0.5 * (h * 60 + m);
    float minute_angle = 6 * m;

    // Find the difference between two angles
    float angle = abs(hour_angle - minute_angle);

    // Return the smaller angle of two possible angles
    angle = min(360 - angle, angle);

    return angle;
}

// Driver Code
int main()
{
    cout << calcAngle(9, 60) << endl;
    cout << calcAngle(3, 30) << endl;
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// C program to find angle between hour and minute hands
#include <stdio.h>
#include <stdlib.h>

// Utility function to find minimum of two integers
int min(int x, int y) { return (x < y)? x: y; }

int calcAngle(double h, double m)
{
    // validate the input
    if (h <0 || m < 0 || h >12 || m > 60)
        printf("Wrong input");

    if (h == 12) h = 0;
    if (m == 60)
     {
      m = 0;
      h += 1;
       if(h>12)
        h = h-12;
     }

    // Calculate the angles moved by hour and minute hands
    // with reference to 12:00
    int hour_angle = 0.5 * (h*60 + m);
    int minute_angle = 6*m;

    // Find the difference between two angles
    int angle = abs(hour_angle - minute_angle);

    // Return the smaller angle of two possible angles
    angle = min(360-angle, angle);

    return angle;
}

// Driver Code
int main()
{
    printf("%d n", calcAngle(9, 60));
    printf("%d n", calcAngle(3, 30));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find angle between hour and minute hands
import java.io.*;

class GFG
{
    // Function to calculate the angle
    static int calcAngle(double h, double m)
    {
        // validate the input
        if (h <0 || m < 0 || h >12 || m > 60)
            System.out.println("Wrong input");

        if (h == 12)
            h = 0;
             if (m == 60)
       {
        m = 0;
        h += 1;
        if(h>12)
          h = h-12;
        }

        // Calculate the angles moved by hour and minute hands
        // with reference to 12:00
        int hour_angle = (int)(0.5 * (h*60 + m));
        int minute_angle = (int)(6*m);

        // Find the difference between two angles
        int angle = Math.abs(hour_angle - minute_angle);

        // smaller angle of two possible angles
        angle = Math.min(360-angle, angle);

        return angle;
    }

    // Driver Code
    public static void main (String[] args)
    {
        System.out.println(calcAngle(9, 60)+" degree");
        System.out.println(calcAngle(3, 30)+" degree");
    }
}

// Contributed by Pramod Kumar
```

## 计算机编程语言

```
# Python program to find angle
# between hour and minute hands

# Function to Calculate angle b/w
# hour hand and minute hand
def calcAngle(h,m):

        # validate the input
        if (h < 0 or m < 0 or h > 12 or m > 60):
            print('Wrong input')

        if (h == 12):
            h = 0
        if (m == 60):
            m = 0
            h += 1;
            if(h>12):
                   h = h-12;

        # Calculate the angles moved by
        # hour and minute hands with
        # reference to 12:00
        hour_angle = 0.5 * (h * 60 + m)
        minute_angle = 6 * m

        # Find the difference between two angles
        angle = abs(hour_angle - minute_angle)

        # Return the smaller angle of two
        # possible angles
        angle = min(360 - angle, angle)

        return angle

# Driver Code
h = 9
m = 60
print('Angle ', calcAngle(h,m))

# This code is contributed by Danish Raza
```

## C#

```
// C# program to find angle between
// hour and minute hands
using System;

class GFG {

    // Function to calculate the angle
    static int calcAngle(double h, double m)
    {
        // validate the input
        if (h < 0 || m < 0 ||
            h > 12 || m > 60)
            Console.Write("Wrong input");

        if (h == 12)
            h = 0;

       if (m == 60)
       {
        m = 0;
        h += 1;
        if(h>12)
          h = h-12;
       }

        // Calculate the angles moved by hour and
        // minute hands with reference to 12:00
        int hour_angle = (int)(0.5 * (h * 60 + m));
        int minute_angle = (int)(6 * m);

        // Find the difference between two angles
        int angle = Math.Abs(hour_angle - minute_angle);

        // smaller angle of two possible angles
        angle = Math.Min(360 - angle, angle);

        return angle;
    }

    // Driver code
    public static void Main ()
    {
        Console.WriteLine(calcAngle(9, 60));
        Console.Write(calcAngle(3, 30));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// angle between hour
// and minute hands

// Utility function to
// find minimum of two
// integers
function mintwo($x, $y)
{
    return ($x < $y) ?
                  $x : $y;
}

function calcAngle($h, $m)
{
    // validate the input
    if ($h <0 || $m < 0 ||
        $h >12 || $m > 60)
        echo "Wrong input";

    if ($h == 12) $h = 0;
    if ($m == 60) {
        $m = 0;
        $h += 1;
        if($h>12)
          $h = $h-12;
    }

    // Calculate the angles
    // moved by hour and
    // minute hands with
    // reference to 12:00
    $hour_angle = 0.5 *
                  ($h * 60 + $m);
    $minute_angle = 6 * $m;

    // Find the difference
    // between two angles
    $angle = abs($hour_angle -
                 $minute_angle);

    // Return the smaller angle
    // of two possible angles
    $angle = min(360 - $angle,
                       $angle);

    return $angle;
}

// Driver Code
echo calcAngle(9, 60), "\n";
echo calcAngle(3, 30), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program to find angle between hour and minute hands

// Utility function to find minimum of two integers
function min(x, y)
{
    return (x < y)? x: y;

}

function calcAngle(h, m)
{
    // validate the input
    if (h <0 || m < 0 || h >12 || m > 60)
        document.write("Wrong input");

    if (h == 12) h = 0;
    if (m == 60)
    {
    m = 0;
    h += 1;
    if(h>12)
        h = h-12;
    }

    // Calculate the angles moved
    // by hour and minute hands
    // with reference to 12:00
    let hour_angle = 0.5 * (h * 60 + m);
    let minute_angle = 6 * m;

    // Find the difference between two angles
    let angle = Math.abs(hour_angle - minute_angle);

    // Return the smaller angle of two possible angles
    angle = min(360 - angle, angle);

    return angle;
}

// Driver Code
    document.write(calcAngle(9, 60) + "<br>");
    document.write(calcAngle(3, 30) + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output**

```
60
75
```

**时间复杂度:** O(1)

**辅助空间:**O(1)
T3】练习:找到时针和分针重合的所有时间。
本文由**阿诗班萨尔**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息