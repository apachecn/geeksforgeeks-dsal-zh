# 找到我们可以倾斜瓶子而不溅出任何水的最大角度

> 原文:[https://www . geeksforgeeks . org/find-我们可以倾斜瓶子而不会溅出任何水的最大角度/](https://www.geeksforgeeks.org/find-the-maximum-angle-at-which-we-can-tilt-the-bottle-without-spilling-any-water/)

给定一个底部为边 x cm、高 y cm 的正方形的矩形棱柱形状的水瓶，任务是找到当 z 立方 cm 的水倒入瓶中时，我们可以倾斜瓶子而不溅出任何水的最大角度，并围绕底部的一边逐渐倾斜瓶子。

**示例:**

```
Input: x = 2, y = 2, z = 4
Output: 45.00000
Explanation:
This bottle has a cubic shape,
and it is half-full. 
The water gets split when we tilt
the bottle more than 45 degrees.

Input: x = 12, y = 21, z = 10
Output: 89.78346
```

**进场:**
首先，我们需要知道水面始终与地面平行。所以如果瓶子倾斜，水保持与地面平行。
这里有两种情况:-

1.  当水少于瓶子总体积的一半时，那么我们考虑瓶子内部水形成的右下三角形，并借助切线反算出所需的角度。
2.  当水大于或等于瓶子的总体积时，那么我们考虑瓶子内部的空白空间形成的右上三角形。现在我们可以很容易地计算角度。

下面是上述方法的实现:

## C++

```
// C++ program to find the maximum angle
// at which we can tilt the bottle
// without spilling any water

#include <bits/stdc++.h>
using namespace std;

float find_angle(int x, int y, int z)
{

    // Now we have the volume
    // of rectangular prism a*a*b
    int volume = x * x * y;

    float ans = 0;

    // Now we have 2 cases!
    if (z < volume / 2) {

        float d = (x * y * y) / (2.0 * z);

        // Taking the tangent inverse of value d
        // As we want to take out the required angle
        ans = atan(d);
    }
    else {

        z = volume - z;
        float d = (2 * z) / (float)(x * x * x);

        // Taking the tangent inverse of value d
        // As we want to take out the required angle
        ans = atan(d);
    }

    // As of now the angle is in radian.
    // So we have to convert it in degree.
    ans = (ans * 180) / 3.14159265;

    return ans;
}

int main()
{
    // Enter the Base square side length
    int x = 12;

    // Enter the Height of rectangular prism
    int y = 21;

    // Enter the Base square side length
    int z = 10;

    cout << find_angle(x, y, z) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum angle
// at which we can tilt the bottle
// without spilling any water
class GFG
{
    static float find_angle(int x,
                     int y, int z)
    {

        // Now we have the volume
        // of rectangular prism a*a*b
        int volume = x * x * y;

        float ans = 0;

        // Now we have 2 cases!
        if (z < volume / 2)
        {
            float d = (float) ((x * y * y) / (2.0 * z));

            // Taking the tangent inverse of value d
            // As we want to take out the required angle
            ans = (float) Math.atan(d);
        }
        else
        {
            z = volume - z;
            float d = (2 * z) / (float) (x * x * x);

            // Taking the tangent inverse of value d
            // As we want to take out the required angle
            ans = (float) Math.atan(d);
        }

        // As of now the angle is in radian.
        // So we have to convert it in degree.
        ans = (float) ((ans * 180) / 3.14159265);

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Enter the Base square side length
        int x = 12;

        // Enter the Height of rectangular prism
        int y = 21;

        // Enter the Base square side length
        int z = 10;

        System.out.print(find_angle(x, y, z) + "\n");
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find the maximum angle
# at which we can tilt the bottle
# without spilling any water
from math import *

def find_angle(x, y, z) :

    # Now we have the volume
    # of rectangular prism a*a*b
    volume = x * x * y;

    ans = 0;

    # Now we have 2 cases!
    if (z < volume // 2) :

        d = (x * y * y) / (2.0 * z);

        # Taking the tangent inverse of value d
        # As we want to take out the required angle
        ans = atan(d);

    else :

        z = volume - z;
        d = (2 * z) / (float)(x * x * x);

        # Taking the tangent inverse of value d
        # As we want to take out the required angle
        ans = atan(d);

    # As of now the angle is in radian.
    # So we have to convert it in degree.
    ans = (ans * 180) / 3.14159265;

    return round(ans, 4);

# Driver Code
if __name__ == "__main__" :

    # Enter the Base square side length
    x = 12;

    # Enter the Height of rectangular prism
    y = 21;

    # Enter the Base square side length
    z = 10;

    print(find_angle(x, y, z));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the maximum angle
// at which we can tilt the bottle
// without spilling any water
using System;

class GFG
{
    static float find_angle(int x,
                     int y, int z)
    {

        // Now we have the volume
        // of rectangular prism a*a*b
        int volume = x * x * y;

        float ans = 0;

        // Now we have 2 cases!
        if (z < volume / 2)
        {
            float d = (float) ((x * y * y) / (2.0 * z));

            // Taking the tangent inverse of value d
            // As we want to take out the required angle
            ans = (float) Math.Atan(d);
        }
        else
        {
            z = volume - z;
            float d = (2 * z) / (float) (x * x * x);

            // Taking the tangent inverse of value d
            // As we want to take out the required angle
            ans = (float) Math.Atan(d);
        }

        // As of now the angle is in radian.
        // So we have to convert it in degree.
        ans = (float) ((ans * 180) / 3.14159265);

        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Enter the Base square side length
        int x = 12;

        // Enter the Height of rectangular prism
        int y = 21;

        // Enter the Base square side length
        int z = 10;

        Console.Write(find_angle(x, y, z) + "\n");
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript program to find the maximum angle
// at which we can tilt the bottle
// without spilling any water

    function find_angle(x , y , z) {

        // Now we have the volume
        // of rectangular prism a*a*b
        var volume = x * x * y;

        var ans = 0;

        // Now we have 2 cases!
        if (z < volume / 2) {
            var d =  ((x * y * y) / (2.0 * z));

            // Taking the tangent inverse of value d
            // As we want to take out the required angle
            ans =  Math.atan(d);
        } else {
            z = volume - z;
            var d = (2 * z) /  (x * x * x);

            // Taking the tangent inverse of value d
            // As we want to take out the required angle
            ans =  Math.atan(d);
        }

        // As of now the angle is in radian.
        // So we have to convert it in degree.
        ans =  ((ans * 180) / 3.14159265);

        return ans;
    }

    // Driver Code

        // Enter the Base square side length
        var x = 12;

        // Enter the Height of rectangular prism
        var y = 21;

        // Enter the Base square side length
        var z = 10;

        document.write(find_angle(x, y, z).toFixed(4) + "\n");

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
89.7835
```