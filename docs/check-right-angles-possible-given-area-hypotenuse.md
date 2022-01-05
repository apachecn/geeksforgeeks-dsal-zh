# 检查给定区域和斜边的直角三角形是否可能

> 原文:[https://www . geesforgeks . org/check-直角-可能-给定面积-斜边/](https://www.geeksforgeeks.org/check-right-angles-possible-given-area-hypotenuse/)

给定面积和斜边，如果直角三角形可以存在，目标是打印所有边，否则打印-1。我们需要按升序打印所有面。

示例:

```
Input  : 6 5
Output : 3 4 5

Input  : 10 6
Output : -1 
```

我们已经在下面的帖子中讨论了这个问题的解决方案。
[从给定的斜边和面积中找出直角三角形的所有边|集合 1](https://www.geeksforgeeks.org/find-sides-right-angled-triangle-given-hypotenuse-area/)
在这篇文章中，讨论了一个具有以下逻辑的新解法。
假设两个未知边为 a 和 b
面积:A = 0.5 * a * b
斜边正方形:H^2 = a^2 + b^2
代入 b，重新排列得到 h<sup>2</sup>= a<sup>2</sup>+(4 * a<sup>2</sup>)/a<sup>2</sup>t16】， 我们得到方程 A<sup>4</sup>–(H<sup>2</sup>)(A<sup>2</sup>)+4 *(A<sup>2</sup>)
这个方程的判别式 D 将是 D = H<sup>4</sup>–16 *(A<sup>2</sup>)
如果 D = 0，那么根由线性方程公式给出，根=(-b+-sqrt(D))/2 *

## C++

```
// C++ program to check existence of
// right triangle.
#include <bits/stdc++.h>
using namespace std;

// Prints three sides of a right triangle
// from given area and hypotenuse if triangle
// is possible, else prints -1.
void findRightAngle(int A, int H)
{
    // Descriminant of the equation
    long D = pow(H, 4) - 16 * A * A;

    if (D >= 0)
    {
        // applying the linear equation
        // formula to find both the roots
        long root1 = (H * H + sqrt(D)) / 2;
        long root2 = (H * H - sqrt(D)) / 2;

        long a = sqrt(root1);
        long b = sqrt(root2);

        if (b >= a)
        cout << a << " " << b << " " << H;
        else
        cout << b << " " << a << " " << H;
    }
    else
        cout << "-1";
}

// Driver code
int main()
{
    findRightAngle(6, 5);

}

// This code is contributed By Anant Agarwal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check existence of
// right triangle.

class GFG {

    // Prints three sides of a right triangle
    // from given area and hypotenuse if triangle
    // is possible, else prints -1.
    static void findRightAngle(double A, double H)
    {
        // Descriminant of the equation
        double D = Math.pow(H, 4) - 16 * A * A;

        if (D >= 0)
        {
            // applying the linear equation
            // formula to find both the roots
            double root1 = (H * H + Math.sqrt(D)) / 2;
            double root2 = (H * H - Math.sqrt(D)) / 2;

            double a = Math.sqrt(root1);
            double b = Math.sqrt(root2);
            if (b >= a)
                System.out.print(a + " " + b + " " + H);
            else
                System.out.print(b + " " + a + " " + H);
        }
        else
            System.out.print("-1");
    }

    // Driver code
    public static void main(String arg[])
    {
        findRightAngle(6, 5);
    }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to check existence of
# right triangle.
from math import sqrt

# Prints three sides of a right triangle
# from given area and hypotenuse if triangle
# is possible, else prints -1.
def findRightAngle(A, H):

    # Descriminant of the equation
    D = pow(H,4) - 16 * A * A
    if D >= 0:

        # applying the linear equation
        # formula to find both the roots
        root1 = (H * H + sqrt(D))/2
        root2 = (H * H - sqrt(D))/2

        a = sqrt(root1)
        b = sqrt(root2)
        if b >= a:
            print a, b, H
        else:
            print b, a, H
    else:
        print "-1"

# Driver code
# Area is 6 and hypotenuse is 5.
findRightAngle(6, 5)
```

## C#

```
// C# program to check existence of
// right triangle.
using System;

class GFG {

    // Prints three sides of a right triangle
    // from given area and hypotenuse if triangle
    // is possible, else prints -1.
    static void findRightAngle(double A, double H)
    {

        // Descriminant of the equation
        double D = Math.Pow(H, 4) - 16 * A * A;

        if (D >= 0) {

            // applying the linear equation
            // formula to find both the roots
            double root1 = (H * H + Math.Sqrt(D)) / 2;
            double root2 = (H * H - Math.Sqrt(D)) / 2;

            double a = Math.Sqrt(root1);
            double b = Math.Sqrt(root2);

            if (b >= a)
                Console.WriteLine(a + " " + b + " " + H);
            else
                Console.WriteLine(b + " " + a + " " + H);
        }
        else
            Console.WriteLine("-1");
    }

    // Driver code
    public static void Main()
    {
        findRightAngle(6, 5);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check existence of
// right triangle.

// Prints three sides of a right triangle
// from given area and hypotenuse if
// triangle is possible, else prints -1.
function findRightAngle($A, $H)
{

    // Descriminant of the equation
    $D = pow($H, 4) - 16 * $A * $A;

    if ($D >= 0)
    {

        // applying the linear equation
        // formula to find both the roots
        $root1 = ($H * $H + sqrt($D)) / 2;
        $root2 = ($H * $H - sqrt($D)) / 2;

        $a = sqrt($root1);
        $b = sqrt($root2);

        if ($b >= $a)
            echo $a , " ", $b , " " , $H;
        else
        echo $b , " " , $a , " " , $H;
    }
    else
        echo "-1";
}

    // Driver code
    findRightAngle(6, 5);

// This code is contributed By Anuj_67
?>
```

## java 描述语言

```
<script>

// Javascript program to check existence of
// right triangle.

// Prints three sides of a right triangle
// from given area and hypotenuse if triangle
// is possible, else prints -1.
function findRightAngle(A,H)
{
    // Descriminant of the equation
    let D = Math.pow(H, 4) - 16 * A * A;

    if (D >= 0)
    {
        // applying the linear equation
        // formula to find both the roots
        let root1 = (H * H + Math.sqrt(D)) / 2;
        let root2 = (H * H - Math.sqrt(D)) / 2;

        let a = Math.sqrt(root1);
        let b = Math.sqrt(root2);

        if (b >= a)
       document.write(a + " " + b + " " + H+"<br/>");
        else
       document.write(b + " " + a + " " + H+"<br/>");
    }
    else
        document.write("-1");
}

// Driver code

    findRightAngle(6, 5);

// This code contributed by Rajput-Ji

</script>
```

**输出:**

```
3 4 5
```

本文由 **Harshit Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。