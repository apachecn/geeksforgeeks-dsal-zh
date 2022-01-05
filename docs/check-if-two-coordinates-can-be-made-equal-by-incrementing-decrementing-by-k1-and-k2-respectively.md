# 通过分别增加/减少 K1 和 K2 来检查两个坐标是否相等

> 原文:[https://www . geeksforgeeks . org/check-if-two-coordinate-can-equal-by-递增-递减-k1-和-k2-分别/](https://www.geeksforgeeks.org/check-if-two-coordinates-can-be-made-equal-by-incrementing-decrementing-by-k1-and-k2-respectively/)

给定两个整数坐标 **(X1，Y1)** 和 **(X2，Y2)** 以及两个正整数 **K1** 和 **K2** ，任务是通过多次执行以下步骤来检查两个坐标是否可以相等:

*   从 **(X1，Y1)** 的任一或两个坐标中加上或减去 **K1** 。
*   从 **(X2，Y2)** 的任一或两个坐标中加上或减去 **K2** 。

如果可以使 **(X1，Y1)****(X2，Y2)** 相等，则打印**是**。否则，打印**否**。

**示例:**

> **输入:** X1 = 10，Y1 = 10，X2 = 18，Y2 = 13，K1 = 3，K2 = 4
> **输出:**是
> **说明:**
> 以下是可以使两个坐标相等的招式:
> 
> 1.  将点(X1，Y1)移动为(10，10) - > (10，13)。
> 2.  将点(X2，Y2)移动为(18，13) -> (14，13) -> (10，13)
> 
> 通过以上操作，可以使两个坐标相等，然后打印是。
> 
> **输入:** X1 = 10，Y1 = 10，X2 = 18，Y2 = 13，K1 = 10，K2 = 10
> T3】输出:否

**进场:**这个问题可以用 [**贪心进场**](https://www.geeksforgeeks.org/greedy-algorithms/) 来解决，基于观察 **(X1，Y1)** 点为**n1**x 方向可以走位，而 **(X2，Y2)** 点为**N2**x 方向可以走位，那么表达式可以写成:

> n1 * K1+N2 * K2 = ABS(X1–X2)，
> 
> 其中 n1 和 n2 是非负整数。

同样，y 方向也可以写成:

> n3 * K1+n4 * K2 = ABS(Y1–Y2)，
> …其中 n3 和 n4 为非负整数。

现在可以看出，问题已经化简为求上面的方程是否有解。如果两个方程都有非负解，则打印**“是”**。否则，打印**‘否’**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if both can be merged
int twoPointsReachable(int X1, int Y1, int X2, int Y2,
                       int K1, int K2)
{

    // Calculate gcd of K1, K2
    int g = __gcd(K1, K2);

    // Solve for the X-axis
    bool reachableOnX = 0;

    // Calculate distance between the
    // X-coordinates
    int X_distance = abs(X1 - X2);

    // Check the divisibility
    if (X_distance % g == 0) {
        reachableOnX = 1;
    }

    // Solve for the Y-axis
    bool reachableOnY = 0;

    // Calculate distance on between
    // X coordinates
    int Y_distance = abs(Y1 - Y2);

    // Check for the divisibility
    if (Y_distance % g == 0) {
        reachableOnY = 1;
    }

    // Check if both solutions exist
    if (reachableOnY && reachableOnX) {
        cout << "Yes"
             << "\n";
    }
    else {
        cout << "No"
             << "\n";
    }
    return 0;
}

// Driver Code
int main()
{
    // Given Input
    int X1 = 10, Y1 = 10, X2 = 18;
    int Y2 = 13, K1 = 3, K2 = 4;

    // Function Call
    twoPointsReachable(X1, X2, Y1, Y2, K1, K2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG{

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);

    }

// Function to check if both can be merged
static int twoPointsReachable(int X1, int Y1, int X2, int Y2,
                    int K1, int K2)
{

    // Calculate gcd of K1, K2
    int g = __gcd(K1, K2);

    // Solve for the X-axis
    boolean reachableOnX = (g == 0);

    // Calculate distance between the
    // X-coordinates
    int X_distance = Math.abs(X1 - X2);

    // Check the divisibility
    if (X_distance % g == 0) {
        reachableOnX = (g == 1);
    }

    // Solve for the Y-axis
    boolean reachableOnY = (g == 0);

    // Calculate distance on between
    // X coordinates
    int Y_distance = Math.abs(Y1 - Y2);

    // Check for the divisibility
    if (Y_distance % g == 0) {
        reachableOnY = (g == 1);
    }

    // Check if both solutions exist
    if (reachableOnY && reachableOnX) {
        System.out.print("Yes");
    }
    else {
        System.out.print("No");
    }
    return 0;
}

// Driver Code
public static void main (String[] args)
{

    // Given Input
    int X1 = 10, Y1 = 10, X2 = 18;
    int Y2 = 13, K1 = 3, K2 = 4;

    // Function Call
    twoPointsReachable(X1, X2, Y1,
                    Y2, K1, K2);

}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# python program for the above approach
# Function to check if both can be merged
from math import *

def twoPointsReachable(X1, Y1, X2, Y2, K1, K2):

    # Calculate gcd of K1, K2
    g = gcd(K1, K2)

    # Solve for the X-axis
    reachableOnX = 0

    # Calculate distance between the
    # X-coordinates
    X_distance = abs(X1 - X2)

    # Check the divisibility
    if (X_distance % g == 0):
        reachableOnX = 1

    # Solve for the Y-axis
    reachableOnY = 0

    # Calculate distance on between
    # X coordinates
    Y_distance = abs(Y1 - Y2)

    # Check for the divisibility
    if (Y_distance % g == 0):
        reachableOnY = 1

    # Check if both solutions exist
    if (reachableOnY and reachableOnX):
        print("Yes")
    else:
        print("No")

    return 0

# Driver Code
# Given Input
X1 = 10
Y1 = 10
X2 = 18
Y2 = 13
K1 = 3
K2 = 4

# Function Call
twoPointsReachable(X1, X2, Y1, Y2, K1, K2)

# This code is contributed by anudeep23042002
```

## C#

```
// C++ program for the above approach
using System;

public class GFG {

    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);
    }

    // Function to check if both can be merged
    static int twoPointsReachable(int X1, int Y1, int X2,
                                  int Y2, int K1, int K2)
    {

        // Calculate gcd of K1, K2
        int g = __gcd(K1, K2);

        // Solve for the X-axis
        bool reachableOnX = Convert.ToBoolean(0);

        // Calculate distance between the
        // X-coordinates
        int X_distance = Math.Abs(X1 - X2);

        // Check the divisibility
        if (X_distance % g == 0) {
            reachableOnX = Convert.ToBoolean(1);
        }

        // Solve for the Y-axis
        bool reachableOnY = Convert.ToBoolean(0);

        // Calculate distance on between
        // X coordinates
        int Y_distance = Math.Abs(Y1 - Y2);

        // Check for the divisibility
        if (Y_distance % g == 0) {
            reachableOnY = Convert.ToBoolean(1);
        }

        // Check if both solutions exist
        if (reachableOnY && reachableOnX) {
            Console.Write("Yes");
        }
        else {
            Console.Write("No");
        }
        return 0;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Given Input
        int X1 = 10, Y1 = 10, X2 = 18;
        int Y2 = 13, K1 = 3, K2 = 4;

        // Function Call
        twoPointsReachable(X1, X2, Y1, Y2, K1, K2);
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach
        function __gcd(a, b)
        {

            // Everything divides 0
            if (a == 0)
                return b;
            if (b == 0)
                return a;

            // base case
            if (a == b)
                return a;

            // a is greater
            if (a > b)
                return __gcd(a - b, b);
            return __gcd(a, b - a);
        }

        // Function to check if both can be merged
        function twoPointsReachable(X1, Y1, X2, Y2,
            K1, K2) {

            // Calculate gcd of K1, K2
            let g = __gcd(K1, K2);

            // Solve for the X-axis
            let reachableOnX = 0;

            // Calculate distance between the
            // X-coordinates
            let X_distance = Math.abs(X1 - X2);

            // Check the divisibility
            if (X_distance % g == 0) {
                reachableOnX = 1;
            }

            // Solve for the Y-axis
            let reachableOnY = 0;

            // Calculate distance on between
            // X coordinates
            let Y_distance = Math.abs(Y1 - Y2);

            // Check for the divisibility
            if (Y_distance % g == 0) {
                reachableOnY = 1;
            }

            // Check if both solutions exist
            if (reachableOnY && reachableOnX) {
                document.write("Yes" + "<br>");
            }
            else {
                document.write("No" + "<br>");
            }
            return 0;
        }

        // Driver Code

        // Given Input
        let X1 = 10, Y1 = 10, X2 = 18;
        let Y2 = 13, K1 = 3, K2 = 4;

        // Function Call
        twoPointsReachable(X1, X2, Y1,
            Y2, K1, K2);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(log(max(K1，K2))*
***辅助空间:** O(1)*