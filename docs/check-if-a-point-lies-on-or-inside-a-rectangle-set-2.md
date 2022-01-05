# 检查一个点是否位于矩形内| Set-2

> 原文:[https://www . geeksforgeeks . org/check-如果一个点位于矩形集 2 上或矩形集 2 内/](https://www.geeksforgeeks.org/check-if-a-point-lies-on-or-inside-a-rectangle-set-2/)

给定矩形左下角和右上角的坐标。检查点(x，y)是否位于该矩形内。

**示例:**

> **输入:**左下角:(0，0)，右上角:(10，8)，点:(1，5)
> **输出:**是
> 
> **输入:**左下角:(-1，4)，右上角:(2，3)，点:(0，4)
> **输出:**否

这个问题已经在[之前的帖子](https://www.geeksforgeeks.org/check-whether-given-point-lies-inside-rectangle-not/)中讨论过了。在这篇文章中，我们讨论了一种新的方法。

**进场:**以上问题可以通过观察解决。当且仅当一个点的 x 坐标位于矩形的给定右下坐标和左上坐标的 x 坐标之间，y 坐标位于给定右下坐标和左上坐标的 y 坐标之间时，该点位于矩形内部或不位于矩形内部。

下面是上述方法的实现:

## C++

```
// CPP program to Check if a
// point lies on or inside a rectangle | Set-2
#include <bits/stdc++.h>
using namespace std;

// function to find if given point
// lies inside a given rectangle or not.
bool FindPoint(int x1, int y1, int x2,
               int y2, int x, int y)
{
    if (x > x1 and x < x2 and y > y1 and y < y2)
        return true;

    return false;
}

// Driver code
int main()
{
    // bottom-left and top-right
    // corners of rectangle
    int x1 = 0, y1 = 0, x2 = 10, y2 = 8;

    // given point
    int x = 1, y = 5;

    // function call
    if (FindPoint(x1, y1, x2, y2, x, y))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Check if
// a point lies on or inside
// a rectangle | Set-2
class GFG
{

// function to find if given point
// lies inside a given rectangle or not.
static boolean FindPoint(int x1, int y1, int x2,
                         int y2, int x, int y)
{
if (x > x1 && x < x2 &&
    y > y1 && y < y2)
    return true;

return false;
}

// Driver code
public static void main(String[] args)
{

    // bottom-left and top-right
    // corners of rectangle
    int x1 = 0, y1 = 0,
        x2 = 10, y2 = 8;

    // given point
    int x = 1, y = 5;

    // function call
    if (FindPoint(x1, y1, x2, y2, x, y))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python3 program to Check
# if a point lies on or
# inside a rectangle | Set-2

# function to find if
# given point lies inside
# a given rectangle or not.
def FindPoint(x1, y1, x2,
              y2, x, y) :
    if (x > x1 and x < x2 and
        y > y1 and y < y2) :
        return True
    else :
        return False

# Driver code
if __name__ == "__main__" :

    # bottom-left and top-right
    # corners of rectangle.
    # use multiple assignment
    x1 , y1 , x2 , y2 = 0, 0, 10, 8

    # given point
    x, y = 1, 5

    # function call
    if FindPoint(x1, y1, x2,
                 y2, x, y) :
        print("Yes")
    else :
        print("No")

# This code is contributed
# by Ankit Rai
```

## C#

```
// C# program to Check if a
// point lies on or inside
// a rectangle | Set-2
using System;

class GFG
{

// function to find if given
// point lies inside a given
// rectangle or not.
static bool FindPoint(int x1, int y1, int x2,
                      int y2, int x, int y)
{
if (x > x1 && x < x2 &&
    y > y1 && y < y2)
    return true;

return false;
}

// Driver code
public static void Main()
{

    // bottom-left and top-right
    // corners of rectangle
    int x1 = 0, y1 = 0,
        x2 = 10, y2 = 8;

    // given point
    int x = 1, y = 5;

    // function call
    if (FindPoint(x1, y1, x2, y2, x, y))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Check if
// a point lies on or inside
// a rectangle | Set-2

// function to find if given
// point lies inside a given
// rectangle or not.
function FindPoint($x1, $y1, $x2,
                   $y2, $x, $y)
{
    if ($x > $x1 and $x < $x2 and
        $y > $y1 and $y < $y2)
        return true;

    return false;
}

// Driver code

// bottom-left and top-right
// corners of rectangle
$x1 = 0; $y1 = 0;
$x2 = 10; $y2 = 8;

// given point
$x = 1; $y = 5;

// function call
if (FindPoint($x1, $y1, $x2,
              $y2, $x, $y))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// Javascript program to Check if a
// point lies on or inside a rectangle | Set-2

// function to find if given point
// lies inside a given rectangle or not.
function FindPoint(x1, y1, x2,
            y2, x, y)
{
    if (x > x1 && x < x2 && y > y1 && y < y2)
        return true;

    return false;
}

// Driver code

    // bottom-left and top-right
    // corners of rectangle
    let x1 = 0, y1 = 0, x2 = 10, y2 = 8;

    // given point
    let x = 1, y = 5;

    // function call
    if (FindPoint(x1, y1, x2, y2, x, y))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
Yes
```

**时间复杂度:** O(1)

**辅助空间:** O(1)