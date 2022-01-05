# 程序寻找通过 2 点的线

> 原文:[https://www . geesforgeks . org/program-find-line-passing-2-points/](https://www.geeksforgeeks.org/program-find-line-passing-2-points/)

给定坐标平面上的两个点 P 和 Q，求通过这两个点的直线的方程。
这种转换在很多几何算法中非常有用，比如求直线的交点，求三角形的[圆心](http://mathworld.wolfram.com/Circumcenter.html)，求三角形的[燃烧子](https://en.wikipedia.org/wiki/Incenter)等等…

示例:

```
Input : P(3, 2)
        Q(2, 6)
Output : 4x + 1y = 14

Input : P(0, 1)
        Q(2, 4)
Output : 3x + -2y = -2
```

让给定的两点为 P(x <sub>1</sub> 、y <sub>1</sub> )和 Q(x <sub>2</sub> 、y <sub>2</sub> )。现在，我们找到这些点形成的线的方程。
任意一条线都可以表示为，
ax + by = c
让两点满足给定的线。所以，我们有，
斧 <sub>1</sub> +乘 <sub>1</sub> = c
斧 <sub>2</sub> +乘 <sub>2</sub> = c

我们可以设置以下值，以便所有方程都成立，

```
a = y2 - y1
b = x1 - x2
c = ax1 + by1
```

这些可以通过首先直接获得斜率，然后找到直线的截距来导出。或者这些也可以通过简单的观察巧妙地推导出来，如下所示:

**推导:**

```
ax1 + by1 = c ...(i)
ax2 + by2 = c ...(ii)
Equating (i) and (ii),
ax1 + by1 = ax2 + by2
=> a(x1 - x2) = b(y2 - y1)
Thus, for equating LHS and RHS, we can simply have,
a = (y2 - y1)
AND
b = (x1 - x2)
so that we have,
(y2 - y1)(x1 - x2) = (x1 - x2)(y2 - y1)
AND
Putting these values in (i), we get,
c = ax1 + by1 
```

因此，我们现在有 a，b 和 c 的值，这意味着我们有坐标平面上的直线。

## C++

```
// C++ Implementation to find the line passing
// through two points
#include <iostream>
using namespace std;

// This pair is used to store the X and Y
// coordinate of a point respectively
#define pdd pair<double, double>

// Function to find the line given two points
void lineFromPoints(pdd P, pdd Q)
{
    double a = Q.second - P.second;
    double b = P.first - Q.first;
    double c = a * (P.first) + b * (P.second);

    if (b < 0) {
        cout << "The line passing through points P and Q "
                "is: "
             << a << "x - " << b << "y = " << c << endl;
    }
    else {
        cout << "The line passing through points P and Q "
                "is: "
             << a << "x + " << b << "y = " << c << endl;
    }
}

// Driver code
int main()
{
    pdd P = make_pair(3, 2);
    pdd Q = make_pair(2, 6);
    lineFromPoints(P, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation to find the line passing
// through two points
class GFG {

    // This pair is used to store the X and Y
    // coordinate of a point respectively
    static class Pair {
        int first, second;

        public Pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

    // Function to find the line given two points
    static void lineFromPoints(Pair P, Pair Q)
    {
        int a = Q.second - P.second;
        int b = P.first - Q.first;
        int c = a * (P.first) + b * (P.second);

        if (b < 0) {
            System.out.println(
                "The line passing through points P and Q is: "
                + a + "x - " + b + "y = " + c);
        }
        else {
            System.out.println(
                "The line passing through points P and Q is: "
                + a + "x + " + b + "y = " + c);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        Pair P = new Pair(3, 2);
        Pair Q = new Pair(2, 6);
        lineFromPoints(P, Q);
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 Implementation to find the line passing
# through two points

# This pair is used to store the X and Y
# coordinate of a point respectively
# define pdd pair<double, double>

# Function to find the line given two points

def lineFromPoints(P, Q):

    a = Q[1] - P[1]
    b = P[0] - Q[0]
    c = a*(P[0]) + b*(P[1])

    if(b < 0):
        print("The line passing through points P and Q is:",
              a, "x - ", b, "y = ", c, "\n")
    else:
        print("The line passing through points P and Q is: ",
              a, "x + ", b, "y = ", c, "\n")

# Driver code
if __name__ == '__main__':
    P = [3, 2]
    Q = [2, 6]
    lineFromPoints(P, Q)

# This code is contributed by ash264
```

## C#

```
// C# Implementation to find the line passing
// through two points
using System;

class GFG {

    // This pair is used to store the X and Y
    // coordinate of a point respectively
    public class Pair {
        public int first, second;

        public Pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

    // Function to find the line given two points
    static void lineFromPoints(Pair P, Pair Q)
    {
        int a = Q.second - P.second;
        int b = P.first - Q.first;
        int c = a * (P.first) + b * (P.second);

        if (b < 0) {
            Console.WriteLine(
                "The line passing through points P and Q is: "
                + a + "x - " + b + "y = " + c);
        }
        else {
            Console.WriteLine(
                "The line passing through points P and Q is: "
                + a + "x + " + b + "y = " + c);
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        Pair P = new Pair(3, 2);
        Pair Q = new Pair(2, 6);
        lineFromPoints(P, Q);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// line passing through two points

// Function to find the line given two points
function lineFromPoints(P, Q)
{
    var a = Q[1] - P[1]
    var b = P[0] - Q[0]
    var c = a*(P[0]) + b*(P[1])

    if (b < 0)
        document.write("The line passing through " +
                       "points P and Q is:  " + a +
                       "x - " + b + "y = " + c + "<br>")
    else
        document.write("The line passing through " +
                       "points P and Q is:  "+ a + 
                       "x + " + b + "y = " + c + "<br>")
}

// Driver code
var P = [ 3, 2 ]
var Q = [ 2, 6 ]

lineFromPoints(P, Q)

// This code is contributed by akshitsaxenaa09

</script>
```

**输出:**

```
The line passing through points P and Q is: 4x + 1y = 14
```

本文由**安雅金达尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。