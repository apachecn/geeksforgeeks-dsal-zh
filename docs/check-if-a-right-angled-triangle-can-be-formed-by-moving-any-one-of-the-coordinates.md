# 检查移动任意一个坐标

是否可以形成直角三角形

> 原文:[https://www . geesforgeks . org/check-if-a-直角三角形-可以通过移动任意一个坐标来形成/](https://www.geeksforgeeks.org/check-if-a-right-angled-triangle-can-be-formed-by-moving-any-one-of-the-coordinates/)

给定三角形的三个坐标 **(x1，y1)** 、 **(x2，y2)** 、 **(x3，y3)** 。任务是通过仅将一个点精确移动距离 1，找出三角形是否可以转换为**直角**三角形。
如果可以使三角形**成直角**，则打印**“可能”**，否则打印**“不可能”**。
如果三角形已经是**直角**，也要上报。
**例:**

> **输入:**
> x1 = -1，y1 = 0
> x2 = 2，y2 = 0
> x3 = 0，y3 = 1
> **输出:**可能
> 第一坐标 **(-1，0)** 可改为 **(0，0)** 并使其成为**直角**。
> **输入:**
> x1 = 36，y1 = 1
> x2 = -17，y2 = -54
> x3 = -19，y3 = 55
> **输出:**可能

**逼近:**
众所周知，对于边长为 **a** 、 **b** 和 **c** 的三角形，如果下列等式成立，则三角形将为**直角**:**a<sup>2</sup>+b<sup>2</sup>= c<sup>2</sup>**
所以对于三角形的每个坐标，找出所有的边和
如果上述条件不成立，那么需要进行以下操作-
我们需要将所有坐标逐一更改 1，并检查它是否是直角三角形的有效组合。
看一下，可以有 4 种可能的组合将每个坐标改变 1。它们是 **(-1，0)，(0，1)，(1，0)，(0，-1)** 。因此，运行一个循环，对每个坐标逐一应用这些更改，并检查公式**a<sup>2</sup>+b<sup>2</sup>= c<sup>2</sup>T34】是否正确。
如果是真的，那么可以将三角形变换成**直角**三角形，否则不行。
下面是上面代码的实现:** 

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Storing all the possible
// changes to make the triangle
// right-angled
int dx[] = { -1, 0, 1, 0 };
int dy[] = { 0, 1, 0, -1 };

// Function to check if the triangle
// is right-angled or not
int ifRight(int x1, int y1,
            int x2, int y2,
            int x3, int y3)
{

    int a = ((x1 - x2) * (x1 - x2))
            + ((y1 - y2) * (y1 - y2));

    int b = ((x1 - x3) * (x1 - x3))
            + ((y1 - y3) * (y1 - y3));

    int c = ((x2 - x3) * (x2 - x3))
            + ((y2 - y3) * (y2 - y3));

    if ((a == (b + c) && a != 0 && b != 0 && c != 0)
        || (b == (a + c) && a != 0 && b != 0 && c != 0)
        || (c == (a + b) && a != 0 && b != 0 && c != 0)) {
        return 1;
    }

    return 0;
}

// Function to check if the triangle
// can be transformed to right-angled
void isValidCombination(int x1, int y1,
                        int x2, int y2,
                        int x3, int y3)
{
    int x, y;

    // Boolean variable to
    // return true or false
    bool possible = 0;

    // If it is already right-angled
    if (ifRight(x1, y1,
                x2, y2,
                x3, y3)) {
        cout << "ALREADY RIGHT ANGLED";
        return;
    }
    else {

        // Applying the changes on the
        // co-ordinates
        for (int i = 0; i < 4; i++) {

            // Applying on the first
            // co-ordinate
            x = dx[i] + x1;
            y = dy[i] + y1;

            if (ifRight(x, y,
                        x2, y2,
                        x3, y3)) {
                cout << "POSSIBLE";
                return;
            }

            // Applying on the second
            // co-ordinate
            x = dx[i] + x2;
            y = dy[i] + y2;

            if (ifRight(x1, y1,
                        x, y,
                        x3, y3)) {
                cout << "POSSIBLE";
                return;
            }

            // Applying on the third
            // co-ordinate
            x = dx[i] + x3;
            y = dy[i] + y3;

            if (ifRight(x1, y1,
                        x2, y2,
                        x, y)) {
                cout << "POSSIBLE";
                return;
            }
        }
    }

    // If can't be transformed
    if (!possible)
        cout << "NOT POSSIBLE" << endl;
}

// Driver Code
int main()

{
    int x1 = -49, y1 = 0;
    int x2 = 0, y2 = 50;
    int x3 = 0, y3 = -50;

    isValidCombination(x1, y1,
                       x2, y2,
                       x3, y3);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Storing all the possible
// changes to make the triangle
// right-angled
static int dx[] = { -1, 0, 1, 0 };
static int dy[] = { 0, 1, 0, -1 };

// Function to check if the triangle
// is right-angled or not
static boolean ifRight(int x1, int y1,
                       int x2, int y2,
                       int x3, int y3)
{
    int a = ((x1 - x2) * (x1 - x2)) +
            ((y1 - y2) * (y1 - y2));

    int b = ((x1 - x3) * (x1 - x3)) +
            ((y1 - y3) * (y1 - y3));

    int c = ((x2 - x3) * (x2 - x3)) +
            ((y2 - y3) * (y2 - y3));

    if ((a == (b + c) && a != 0 && b != 0 && c != 0) ||
        (b == (a + c) && a != 0 && b != 0 && c != 0) ||
        (c == (a + b) && a != 0 && b != 0 && c != 0))
    {
        return true;
    }
    return false;
}

// Function to check if the triangle
// can be transformed to right-angled
static void isValidCombination(int x1, int y1,
                               int x2, int y2,
                               int x3, int y3)
{
    int x, y;

    // Boolean variable to
    // return true or false
    boolean possible = false;

    // If it is already right-angled
    if (ifRight(x1, y1, x2, y2, x3, y3))
    {
        System.out.print("ALREADY RIGHT ANGLED");
        return;
    }
    else
    {

        // Applying the changes on the
        // co-ordinates
        for (int i = 0; i < 4; i++)
        {

            // Applying on the first
            // co-ordinate
            x = dx[i] + x1;
            y = dy[i] + y1;

            if (ifRight(x, y, x2, y2, x3, y3))
            {
                System.out.print("POSSIBLE");
                return;
            }

            // Applying on the second
            // co-ordinate
            x = dx[i] + x2;
            y = dy[i] + y2;

            if (ifRight(x1, y1, x, y, x3, y3))
            {
                System.out.print("POSSIBLE");
                return;
            }

            // Applying on the third
            // co-ordinate
            x = dx[i] + x3;
            y = dy[i] + y3;

            if (ifRight(x1, y1, x2, y2, x, y))
            {
                System.out.print("POSSIBLE");
                return;
            }
        }
    }

    // If can't be transformed
    if (!possible)
        System.out.println("NOT POSSIBLE");
}

// Driver Code
public static void main(String[] args)
{
    int x1 = -49, y1 = 0;
    int x2 = 0, y2 = 50;
    int x3 = 0, y3 = -50;

    isValidCombination(x1, y1, x2, y2, x3, y3);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Storing all the possible
# changes to make the triangle
# right-angled
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

# Function to check if the triangle
# is right-angled or not
def ifRight(x1, y1, x2, y2, x3, y3):

    a = ((x1 - x2) * (x1 - x2)) + \
        ((y1 - y2) * (y1 - y2))

    b = ((x1 - x3) * (x1 - x3)) + \
        ((y1 - y3) * (y1 - y3))

    c = ((x2 - x3) * (x2 - x3)) + \
        ((y2 - y3) * (y2 - y3))

    if ((a == (b + c) and a != 0 and b != 0 and c != 0) or
        (b == (a + c) and a != 0 and b != 0 and c != 0) or
        (c == (a + b) and a != 0 and b != 0 and c != 0)):
        return 1

# Function to check if the triangle
# can be transformed to right-angled
def isValidCombination(x1, y1, x2, y2, x3, y3):

    x, y = 0, 0

    # Boolean variable to
    # return true or false
    possible = 0

    # If it is already right-angled
    if (ifRight(x1, y1, x2, y2, x3, y3)):
        print("ALREADY RIGHT ANGLED")
        return

    else:

        # Applying the changes on the
        # co-ordinates
        for i in range(4):

            # Applying on the first
            # co-ordinate
            x = dx[i] + x1
            y = dy[i] + y1

            if (ifRight(x, y, x2, y2, x3, y3)):
                print("POSSIBLE")
                return

            # Applying on the second
            # co-ordinate
            x = dx[i] + x2
            y = dy[i] + y2

            if (ifRight(x1, y1, x, y, x3, y3)):
                print("POSSIBLE")
                return

            # Applying on the third
            # co-ordinate
            x = dx[i] + x3
            y = dy[i] + y3

            if (ifRight(x1, y1, x2, y2, x, y)):
                print("POSSIBLE")
                return

    # If can't be transformed
    if (possible == 0):
        print("NOT POSSIBLE")

# Driver Code
x1 = -49
y1 = 0
x2 = 0
y2 = 50
x3 = 0
y3 = -50

isValidCombination(x1, y1, x2, y2, x3, y3)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Storing all the possible
    // changes to make the triangle
    // right-angled
    static int []dx = { -1, 0, 1, 0 };
    static int []dy = { 0, 1, 0, -1 };

    // Function to check if the triangle
    // is right-angled or not
    static bool ifRight(int x1, int y1,
                        int x2, int y2,
                        int x3, int y3)
    {
        int a = ((x1 - x2) * (x1 - x2)) +
                ((y1 - y2) * (y1 - y2));

        int b = ((x1 - x3) * (x1 - x3)) +
                ((y1 - y3) * (y1 - y3));

        int c = ((x2 - x3) * (x2 - x3)) +
                ((y2 - y3) * (y2 - y3));

        if ((a == (b + c) && a != 0 && b != 0 && c != 0) ||
            (b == (a + c) && a != 0 && b != 0 && c != 0) ||
            (c == (a + b) && a != 0 && b != 0 && c != 0))
        {
            return true;
        }
        return false;
    }

    // Function to check if the triangle
    // can be transformed to right-angled
    static void isValidCombination(int x1, int y1,
                                   int x2, int y2,
                                   int x3, int y3)
    {
        int x, y;

        // Boolean variable to
        // return true or false
        bool possible = false;

        // If it is already right-angled
        if (ifRight(x1, y1, x2, y2, x3, y3))
        {
            Console.WriteLine("ALREADY RIGHT ANGLED");
            return;
        }
        else
        {

            // Applying the changes on the
            // co-ordinates
            for (int i = 0; i < 4; i++)
            {

                // Applying on the first
                // co-ordinate
                x = dx[i] + x1;
                y = dy[i] + y1;

                if (ifRight(x, y, x2, y2, x3, y3))
                {
                    Console.WriteLine("POSSIBLE");
                    return;
                }

                // Applying on the second
                // co-ordinate
                x = dx[i] + x2;
                y = dy[i] + y2;

                if (ifRight(x1, y1, x, y, x3, y3))
                {
                    Console.WriteLine("POSSIBLE");
                    return;
                }

                // Applying on the third
                // co-ordinate
                x = dx[i] + x3;
                y = dy[i] + y3;

                if (ifRight(x1, y1, x2, y2, x, y))
                {
                    Console.Write("POSSIBLE");
                    return;
                }
            }
        }

        // If can't be transformed
        if (!possible)
            Console.WriteLine("NOT POSSIBLE");
    }

    // Driver Code
    static public void Main ()
    {
        int x1 = -49, y1 = 0;
        int x2 = 0, y2 = 50;
        int x3 = 0, y3 = -50;

        isValidCombination(x1, y1, x2, y2, x3, y3);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of
// the above approach

// Storing all the possible
// changes to make the triangle
// right-angled
let dx = [ -1, 0, 1, 0 ];
let dy = [ 0, 1, 0, -1 ];

// Function to check if the triangle
// is right-angled or not
function ifRight(x1, y1, x2, y2,
            x3, y3)
{

    let a = ((x1 - x2) * (x1 - x2))
            + ((y1 - y2) * (y1 - y2));

    let b = ((x1 - x3) * (x1 - x3))
            + ((y1 - y3) * (y1 - y3));

    let c = ((x2 - x3) * (x2 - x3))
            + ((y2 - y3) * (y2 - y3));

    if ((a == (b + c) && a != 0 && b != 0 && c != 0)
        || (b == (a + c) && a != 0 && b != 0 && c != 0)
        || (c == (a + b) && a != 0 && b != 0 && c != 0)) {
        return 1;
    }

    return 0;
}

// Function to check if the triangle
// can be transformed to right-angled
function isValidCombination(x1, y1,
                        x2, y2,
                        x3, y3)
{
    let x, y;

    // Boolean variable to
    // return true or false
    let possible = 0;

    // If it is already right-angled
    if (ifRight(x1, y1,
                x2, y2,
                x3, y3)) {
        document.write("ALREADY RIGHT ANGLED");
        return;
    }
    else {

        // Applying the changes on the
        // co-ordinates
        for (let i = 0; i < 4; i++) {

            // Applying on the first
            // co-ordinate
            x = dx[i] + x1;
            y = dy[i] + y1;

            if (ifRight(x, y,
                        x2, y2,
                        x3, y3)) {
                document.write("POSSIBLE");
                return;
            }

            // Applying on the second
            // co-ordinate
            x = dx[i] + x2;
            y = dy[i] + y2;

            if (ifRight(x1, y1,
                        x, y,
                        x3, y3)) {
                document.write("POSSIBLE");
                return;
            }

            // Applying on the third
            // co-ordinate
            x = dx[i] + x3;
            y = dy[i] + y3;

            if (ifRight(x1, y1,
                        x2, y2,
                        x, y)) {
                document.write("POSSIBLE");
                return;
            }
        }
    }

    // If can't be transformed
    if (!possible)
        document.write("NOT POSSIBLE<br>");
}

// Driver Code
    let x1 = -49, y1 = 0;
    let x2 = 0, y2 = 50;
    let x3 = 0, y3 = -50;

    isValidCombination(x1, y1,
                       x2, y2,
                       x3, y3);

</script>
```

**Output:** 

```
POSSIBLE
```