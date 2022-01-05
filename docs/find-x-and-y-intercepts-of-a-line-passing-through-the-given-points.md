# 求通过给定点的直线的 X 和 Y 截距

> 原文:[https://www . geeksforgeeks . org/find-x-and-y-截取通过给定点的线/](https://www.geeksforgeeks.org/find-x-and-y-intercepts-of-a-line-passing-through-the-given-points/)

给定 2D 平面上的两个点，任务是找到通过给定点的直线的**x-截距**和**y-截距**。
**例:**

> **输入:**分[][] = {{5，2}，{2，7}}
> **输出:**
> 6.2
> 10.333333333333334
> **输入:**分[][] = {{3，2}，{2，4}}
> **输出:**
> 4.0
> 8.0

**进场:**

*   用给定点求斜率。
*   将斜率的值放在线的表达式中，即 **y = mx + c** 。
*   现在使用公式 **y = mx + c** 中任意给定点的值，求出 **c** 的值
*   要找到 x 截距，将 **y = 0** 放入 **y = mx + c** 。
*   要找到 y 截距，将 **x = 0** 放入 **y = mx + c** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the X and Y intercepts
// of the line passing through
// the given points
void getXandYintercept(int P[], int Q[])
{
    int a = P[1] - Q[1];
    int b = P[0] - Q[0];

    // if line is parallel to y axis
    if (b == 0) {
        cout << P[0] << endl; // x - intercept will be p[0]
        cout << "infinity"; // y - intercept will be infinity
        return;
    }

    // if line is parallel to x axis
    if (a == 0) {
        cout << "infinity"; // x - intercept will be infinity
        cout << P[1] << endl; // y - intercept will be p[1]
        return;
    }

    // Slope of the line
    double m = a / (b * 1.0);

    // y = mx + c in where c is unknown
    // Use any of the given point to find c
    int x = P[0];
    int y = P[1];
    double c = y - m * x;

    // For finding the x-intercept put y = 0
    y = 0;
    double r = (y - c) / (m * 1.0);
    cout << r << endl;

    // For finding the y-intercept put x = 0
    x = 0;
    y = m * x + c;
    printf("%.8f", c);
}

// Driver code
int main()
{
    int p1[] = { 5, 2 };
    int p2[] = { 2, 7 };
    getXandYintercept(p1, p2);
    return 0;
}

// This code is contributed by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to find the X and Y intercepts
    // of the line passing through
    // the given points
    static void getXandYintercept(int P[],
                                  int Q[])
    {
        int a = P[1] - Q[1];
        int b = P[0] - Q[0];

        // if line is parallel to y axis
        if (b == 0) {

            // x - intercept will be p[0]
            System.out.println(P[0]);

            // y - intercept will be infinity
            System.out.println("infinity");
            return;
        }

        // if line is parallel to x axis
        if (a == 0) {

            // x - intercept will be infinity 
            System.out.println("infinity");

            // y - intercept will be p[1]
            System.out.println(P[1]);
            return;
        }

        // Slope of the line
        double m = a / (b * 1.0);

        // y = mx + c in where c is unknown
        // Use any of the given point to find c
        int x = P[0];
        int y = P[1];
        double c = y - m * x;

        // For finding the x-intercept put y = 0
        y = 0;
        double r = (y - c) / (m * 1.0);
        System.out.println(r);

        // For finding the y-intercept put x = 0
        x = 0;
        y = (int)(m * x + c);
        System.out.print(c);
    }

    // Driver code
    public static void main(String[] args)
    {
        int p1[] = { 5, 2 };
        int p2[] = { 2, 7 };
        getXandYintercept(p1, p2);
    }
}

// This code is contributed by kanugargng
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the X and Y intercepts
# of the line passing through
# the given points
def getXandYintercept(P, Q):

    a = P[1] - Q[1]
    b = P[0] - Q[0]

    # if line is parallel to y axis
    if b == 0:
        print(P[0])         # x - intercept will be p[0]
        print("infinity")   # y - intercept will be infinity
        return

    # if line is parallel to x axis
    if a == 0:
        print("infinity")     # x - intercept will be infinity
        print(P[1])           # y - intercept will be p[1]
        return

    # Slope of the line
    m = a / b

    # y = mx + c in where c is unknown
    # Use any of the given point to find c
    x = P[0]
    y = P[1]
    c = y-m * x

    # For finding the x-intercept put y = 0
    y = 0
    x =(y-c)/m
    print(x)

    # For finding the y-intercept put x = 0
    x = 0
    y = m * x + c
    print(y)

# Driver code
p1 = [5, 2]
p2 = [7, 2]
getXandYintercept(p1, p2)
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to find the X and Y intercepts
    // of the line passing through
    // the given points
    static void getXandYintercept(int[] P,
                                  int[] Q)
    {
        int a = P[1] - Q[1];
        int b = P[0] - Q[0];

        // if line is parallel to y axis
        if (b == 0) {
            Console.WriteLine(P[0]); // x - intercept will be p[0]
            Console.WriteLine("infinity"); // y - intercept will be infinity
            return;
        }

        // if line is parallel to x axis
        if (a == 0) {
            Console.WriteLine("infinity"); // x - intercept will be infinity
            Console.WriteLine(P[1]); // y - intercept will be p[1]
            return;
        }

        // Slope of the line
        double m = a / (b * 1.0);

        // y = mx + c in where c is unknown
        // Use any of the given point to find c
        int x = P[0];
        int y = P[1];
        double c = y - m * x;

        // For finding the x-intercept put y = 0
        y = 0;
        double r = (y - c) / (m * 1.0);
        Console.WriteLine(r);

        // For finding the y-intercept put x = 0
        x = 0;
        y = (int)(m * x + c);
        Console.WriteLine(c);
    }

    // Driver code
    public static void Main()
    {
        int[] p1 = { 5, 2 };
        int[] p2 = { 2, 7 };
        getXandYintercept(p1, p2);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to find the X and Y intercepts
    // of the line passing through
    // the given points
    function getXandYintercept(P, Q)
    {
        let a = P[1] - Q[1];
        let b = P[0] - Q[0];

        // if line is parallel to y axis
        if (b == 0) {
            document.write(P[0] + "</br>"); // x - intercept will be p[0]
            document.write("infinity" + "</br>"); // y - intercept will be infinity
            return;
        }

        // if line is parallel to x axis
        if (a == 0) {
            document.write("infinity" + "</br>"); // x - intercept will be infinity
            document.write(P[1] + "</br>"); // y - intercept will be p[1]
            return;
        }

        // Slope of the line
        let m = a / (b * 1.0);

        // y = mx + c in where c is unknown
        // Use any of the given point to find c
        let x = P[0];
        let y = P[1];
        let c = y - m * x;

        // For finding the x-intercept put y = 0
        y = 0;
        let r = (y - c) / (m * 1.0);
        document.write(r + "</br>");

        // For finding the y-intercept put x = 0
        x = 0;
        y = parseInt(m * x + c, 10);
        document.write(c.toFixed(11) + "</br>");
    }

    let p1 = [ 5, 2 ];
    let p2 = [ 2, 7 ];
    getXandYintercept(p1, p2);

</script>
```

**Output:** 

```
6.2
10.33333333333
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)