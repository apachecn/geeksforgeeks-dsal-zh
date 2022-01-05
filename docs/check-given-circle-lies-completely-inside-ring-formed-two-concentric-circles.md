# 检查给定的圆是否完全位于两个同心圆形成的环内

> 原文:[https://www . geesforgeks . org/check-given-circle-lies-完全在环内-形成-两个同心圆/](https://www.geeksforgeeks.org/check-given-circle-lies-completely-inside-ring-formed-two-concentric-circles/)

给定半径为 R 和 R 的两个圆，它们的中心都在原点。现在，给定另一个半径为 r1 且圆心在(x1，y1)的圆。检查第三个圆(半径为 r1 的圆)是否完全位于半径为 r 和 r 的两个圆形成的环内。
示例:

```
Input : r = 8 R = 4
        r1 = 2 x1 = 6 y1 = 0
Output : yes

Input : r = 8 R = 4 
        r1 = 2 x1 = 5 y1 = 0
Output : no
```

**重要提示:**同心圆是那些圆心相同的圆。位于两个同心圆之间的区域称为环或圆环。

![circle (1)](img/b6f4ed5a1774652f15fb1430e235be86.png)

**例:**
有两个同心圆，圆心在原点(0，0)，半径为 r = 8，R = 4。
1。)圆圈 1 和 2 位于环内。
2。)圈 3 和圈 4 在圈外。
完整的图形如下所示:

![circle](img/1850f6e995b9f5b68648880967aa62ec.png)

**方法:**
这个问题可以用 [**勾股定理**](https://en.wikipedia.org/wiki/Pythagorean_theorem) 来解决。用毕达哥拉斯定理计算圆心和原点之间的距离，假设用“dis”表示。
计算完距离后，只需检查(dis–R1)>= r 和(dis + r1) < = R 的值。如果这两个条件都成立，则圆完全位于环内。

## C++

```
// CPP code to check if a circle
// lies in the ring
#include <bits/stdc++.h>
using namespace std;

// Function to check if circle
// lies in the ring
bool checkcircle(int r, int R, int r1,
                        int x1, int y1)
{
    // distance between center of circle
    // center of concentric circles(origin)
    // using Pythagoras theorem
    int dis = sqrt(x1*x1+y1*y1);

    // Condition to check if circle is
    // strictly inside the ring
    return (dis-r1 >= R && dis+r1 <= r);
}

// Driver Code
int main()
{
    // Both circle with radius 'r'
    // and 'R' have center (0,0)
    int r = 8, R = 4, r1 = 2, x1 = 6, y1 = 0;   
    if (checkcircle(r, R, r1, x1, y1))
       cout << "yes" << endl;
    else
       cout << "no" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check if a
// circle lies in the ring
import java.io.*;

class ring
{
    // Function to check if circle
    // lies in the ring
    public static boolean checkcircle(int r, int R,
                            int r1, int x1, int y1)
    {
        // distance between center of circle
        // center of concentric circles(origin)
        // using Pythagoras theorem
        int dis = (int)Math.sqrt(x1 * x1 +
                                 y1 * y1);

         // Condition to check if circle
         // is strictly inside the ring
        return (dis - r1 >= R && dis + r1 <= r);
    }

    // Driver Code
    public static void main(String args[])
    {
        // Both circle with radius 'r'
        // and 'R' have center (0,0)
        int r = 8, R = 4, r1 = 2, x1 = 6, y1 = 0;

        if (checkcircle(r, R, r1, x1, y1))
            System.out.println("yes");
        else
            System.out.println("no");
    }
}
```

## 蟒蛇 3

```
# Python3 code to check if
# a circle  lies in the ring
import math

# Function to check if circle
# lies in the ring
def checkcircle(r, R, r1, x1, y1):

    # distance between center of circle
    # center of concentric circles(origin)
    # using Pythagoras theorem
    dis = int(math.sqrt(x1 * x1 + y1 * y1))

    # Condition to check if circle is
    # strictly inside the ring
    return (dis-r1 >= R and dis+r1 <= r)

# Driver Code

# Both circle with radius 'r'
# and 'R' have center (0,0)
r = 8; R = 4; r1 = 2; x1 = 6; y1 = 0
if (checkcircle(r, R, r1, x1, y1)):
    print("yes")
else:
    print("no")

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# code to check if a
// circle lies in the ring
using System;

class ring {

    // Function to check if circle
    // lies in the ring
    public static bool checkcircle(int r, int R,
                         int r1, int x1, int y1)
    {
        // distance between center of circle
        // center of concentric circles(origin)
        // using Pythagoras theorem
        int dis = (int)Math.Sqrt(x1 * x1 + y1 * y1);

        // Condition to check if circle
        // is strictly inside the ring
        return (dis - r1 >= R && dis + r1 <= r);
    }

    // Driver Code
    public static void Main()
    {
        // Both circle with radius 'r'
        // and 'R' have center (0, 0)
        int r = 8, R = 4, r1 = 2, x1 = 6, y1 = 0;

        if (checkcircle(r, R, r1, x1, y1))
            Console.WriteLine("yes");
        else
            Console.WriteLine("no");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check if a circle
// lies in the ring

// Function to check if circle
// lies in the ring
function checkcircle($r, $R, $r1,
                         $x1, $y1)
{

    // distance between center of circle
    // center of concentric circles(origin)
    // using Pythagoras theorem
    $dis = sqrt($x1 * $x1 + $y1 * $y1);

    // Condition to check if circle is
    // strictly inside the ring
    return ($dis-$r1 >= $R && $dis + $r1 <= $r);
}

    // Driver Code
    // Both circle with radius 'r'
    // and 'R' have center (0,0)
    $r = 8; $R = 4;
    $r1 = 2; $x1 = 6;
    $y1 = 0;
    if (checkcircle($r, $R, $r1, $x1, $y1))

    echo "yes" ,"\n";
    else
    echo "no" ,"\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
// JavaScript program code to check if a
// circle lies in the ring

// Function to check if circle
    // lies in the ring
    function checkcircle(r, R, r1, x1, y1)
    {
        // distance between center of circle
        // center of concentric circles(origin)
        // using Pythagoras theorem
        let dis = Math.sqrt(x1 * x1 +
                                 y1 * y1);

         // Condition to check if circle
         // is strictly inside the ring
        return (dis - r1 >= R && dis + r1 <= r);
    }

// Driver Code

        // Both circle with radius 'r'
        // and 'R' have center (0,0)
        let r = 8, R = 4, r1 = 2, x1 = 6, y1 = 0;

        if (checkcircle(r, R, r1, x1, y1))
            document.write("yes");
        else
            document.write("no");

// This code is contributed by splevel62.
</script>
```

**Output:** 

```
yes
```

**时间复杂度:** O(1)

**辅助空间:** O(1)