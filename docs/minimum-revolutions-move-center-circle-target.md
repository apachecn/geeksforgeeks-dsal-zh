# 将圆心移动到目标的最小转数

> 原文:[https://www . geesforgeks . org/minimum-revolutions-move-center-circle-target/](https://www.geeksforgeeks.org/minimum-revolutions-move-center-circle-target/)

给定半径为 r 且圆心在点(x1，y1)的圆和给定的点(x2，y2)。任务是用最少的步数将圆心从给定的中心(x1，y1)移动到目标(x2，y2)。在一个步骤中，我们可以在圆的边界上的任何一点放置一个大头针，然后围绕那个大头针旋转圆任意角度，最后移除大头针。
**例:**

```
Input : r = 2 
        x1 = 0, y1 = 0
        x2 = 0, y2 = 4
Output :1

Input  : r = 1
         x1 = 1, y1 = 1,
         x2 = 4, y2 = 4 
Output : 3
```

让我们考虑两个中心之间的直线。很明显，要以最大距离移动中心，我们需要绕直线旋转 180 度。所以我们每次可以移动中心的最大距离是 2 * r，让我们继续每次以 2 * r 的距离移动中心，直到两个圆相交。现在很明显，我们可以通过围绕两个圆的交点之一旋转中心，使其移动到最终位置，直到到达最终目的地。
每次我们使圆移动 2 * r 次，除了最后一次移动，它将是< 2 * r。让两点之间的初始距离为 d。问题的解决方案将是 ceil(d/2*r)。

## C++

```
// C++ program to find minimum number of
// revolutions to reach a target center
#include<bits/stdc++.h>
using namespace std;

// Minimum revolutions to move center from
// (x1, y1) to (x2, y2)
int minRevolutions(double r, int x1, int y1,
                             int x2, int y2)
{
    double d = sqrt((x1 - x2)*(x1 - x2) +
                    (y1 - y2)*(y1 - y2));
    return ceil(d/(2*r));
}

// Driver code
int main()
{
    int r = 2, x1 = 0, y1 = 0, x2 = 0, y2 = 4;
    cout << minRevolutions(r, x1, y1, x2, y2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of
// revolutions to reach a target center
class GFG {

    // Minimum revolutions to move center
    // from (x1, y1) to (x2, y2)
    static double minRevolutions(double r,
         int x1, int y1, int x2, int y2)
    {

        double d = Math.sqrt((x1 - x2)
                   * (x1 - x2) + (y1 - y2)
                   * (y1 - y2));

        return Math.ceil(d / (2 * r));
    }

    // Driver Program to test above function
    public static void main(String arg[]) {

        int r = 2, x1 = 0, y1 = 0;
        int x2 = 0, y2 = 4;

        System.out.print((int)minRevolutions(r,
                              x1, y1, x2, y2));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# minimum number of
# revolutions to reach
# a target center
import math

# Minimum revolutions to move center from
# (x1, y1) to (x2, y2)
def minRevolutions(r,x1,y1,x2,y2):

    d = math.sqrt((x1 -x2)*(x1 - x2) +
         (y1 - y2)*(y1 - y2))
    return math.ceil(d/(2*r))

# Driver code

r = 2
x1 = 0
y1 = 0
x2 = 0
y2 = 4

print(minRevolutions(r, x1, y1, x2, y2))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find minimum number of
// revolutions to reach a target center
using System;

class GFG {

    // Minimum revolutions to move center
    // from (x1, y1) to (x2, y2)
    static double minRevolutions(double r,
            int x1, int y1, int x2, int y2)
    {

        double d = Math.Sqrt((x1 - x2)
                * (x1 - x2) + (y1 - y2)
                * (y1 - y2));

        return Math.Ceiling(d / (2 * r));
    }

    // Driver Program to test above function
    public static void Main()
    {
        int r = 2, x1 = 0, y1 = 0;
        int x2 = 0, y2 = 4;

        Console.Write((int)minRevolutions(r,
                            x1, y1, x2, y2));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// number of revolutions to reach
// a target center

// Minimum revolutions to move
// center from (x1, y1) to (x2, y2)
function minRevolutions($r, $x1, $y1,
                            $x2, $y2)
{
    $d = sqrt(($x1 - $x2) * ($x1 - $x2) +
              ($y1 - $y2) * ($y1 - $y2));
    return ceil($d / (2 * $r));
}

// Driver code
$r = 2; $x1 = 0; $y1 = 0; $x2 = 0; $y2 = 4;
echo minRevolutions($r, $x1, $y1, $x2, $y2);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// Javascript program to find minimum number of
// revolutions to reach a target center

// Minimum revolutions to move center from
// (x1, y1) to (x2, y2)
function minRevolutions(r, x1, y1, x2, y2)
{
    let d = Math.sqrt((x1 - x2)*(x1 - x2) +
                    (y1 - y2)*(y1 - y2));
    return Math.ceil(d/(2*r));
}

// Driver code
    let r = 2, x1 = 0, y1 = 0, x2 = 0, y2 = 4;
    document.write(minRevolutions(r, x1, y1, x2, y2));

</script>
```

**输出:**

```
 1
```

**时间复杂度:** O(1)
本文由 [**拉克什·库马尔**](https://www.facebook.com/Rakesh2raj) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。