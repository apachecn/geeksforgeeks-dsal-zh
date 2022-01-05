# 嵌入 N 边正多边形的正方形最小边

> 原文:[https://www . geesforgeks . org/n 边嵌入正多边形最小边数/](https://www.geeksforgeeks.org/minimum-side-of-square-embedded-in-regular-polygon-with-n-sides/)

给定一个偶数 **N** ，它代表具有 **N** 顶点的正多边形的边数，任务是找到最小尺寸的正方形，这样给定的**多边形**可以完全嵌入正方形中。

> 多边形是一个凸形图形，有相等的边和相等的角度。所有边都有长度 **1** 。

**嵌入:**将**多边形**放置在正方形中，使得位于 **N** 的内部或边界上的每个点也应该位于正方形的内部或边界上。
**举例:**

> **输入:** N = 4
> **输出:** 1
> **说明:**
> 四边正多边形是边 1 的正方形。
> 给定的多边形可以很容易地嵌入到边为 1 的正方形上。
> **输入:** N = 6
> **输出:** 1.931851653
> **说明:**
> 6 边正多边形是边 1 的六边形。
> 给定的多边形可以很容易地嵌入到边长为 1.931851653 的正方形上。

**方法:**想法是观察在三维平面上，当多边形嵌入正方形时，它可能会旋转。类似的方法已经在[六边形问题](https://www.geeksforgeeks.org/largest-hexagon-that-can-be-inscribed-within-a-square/)和[八边形问题](https://www.geeksforgeeks.org/program-to-find-the-side-of-the-octagon-inscribed-within-the-square/)中讨论过。因此，我们使用数学函数 *sin()* 和 *cos()* 来获取两个轴上每一侧的投影。所有投影的总和是这个问题中所需正方形的最小边。
以下是上述方法的实施:

## C++

```
// C++ program to find the minimum
// side of the square in which
// a regular polygon with even sides
// can completely embed

#include <bits/stdc++.h>
using namespace std;

// PI value in C++ using
// acos function
const double pi = acos(-1.0);

// Function to find the minimum
// side of the square in which
// a regular polygon with even sides
// can completely embed
double nGon(int N)
{

    // Projection angle variation
    // from axes
    double proAngleVar;

    // Projection angle variation
    // when the number of
    // sides are in multiple of 4
    if (N % 4 == 0) {
        proAngleVar
            = pi * (180.0 / N)
              / 180;
    }
    else {
        proAngleVar
            = pi * (180.0 / (2 * N))
              / 180;
    }

    // Distance between the end points
    double negX = 1.0e+99,
           posX = -1.0e+99,
           negY = 1.0e+99,
           posY = -1.0e+99;

    for (int j = 0; j < N; ++j) {

        // Projection from all N points
        // on X-axis
        double px = cos(2 * pi * j / N
                        + proAngleVar);

        // Projection from all N points
        // on Y-axis
        double py = sin(2 * pi * j / N
                        + proAngleVar);

        negX = min(negX, px);
        posX = max(posX, px);
        negY = min(negY, py);
        posY = max(posY, py);
    }

    // Maximum side
    double opt2 = max(posX - negX,
                      posY - negY);

    // Return the portion of side
    // forming the square
    return (double)opt2
           / sin(pi / N) / 2;
}

// Driver code
int main()
{
    int N = 10;
    cout << nGon(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// side of the square in which
// a regular polygon with even sides
// can completely embed
class GFG{

// PI value in Java using
// acos function
static double pi = Math.acos(-1.0);

// Function to find the minimum
// side of the square in which
// a regular polygon with even sides
// can completely embed
static double nGon(int N)
{

    // Projection angle variation
    // from axes
    double proAngleVar;

    // Projection angle variation
    // when the number of
    // sides are in multiple of 4
    if (N % 4 == 0)
    {
        proAngleVar = pi * (180.0 / N) / 180;
    }
    else
    {
        proAngleVar = pi * (180.0 / (2 * N)) / 180;
    }

    // Distance between the end points
    double negX = 1.0e+99,
           posX = -1.0e+99,
           negY = 1.0e+99,
           posY = -1.0e+99;

    for (int j = 0; j < N; ++j)
    {

        // Projection from all N points
        // on X-axis
        double px = Math.cos(2 * pi * j / N +
                                proAngleVar);

        // Projection from all N points
        // on Y-axis
        double py = Math.sin(2 * pi * j / N +
                                proAngleVar);

        negX = Math.min(negX, px);
        posX = Math.max(posX, px);
        negY = Math.min(negY, py);
        posY = Math.max(posY, py);
    }

    // Maximum side
    double opt2 = Math.max(posX - negX,
                           posY - negY);

    // Return the portion of side
    // forming the square
    return (double)opt2 /
            Math.sin(pi / N) / 2;
}

// Driver code
public static void main(String[] args)
{
    int N = 10;
    System.out.printf("%.5f",nGon(N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find the minimum
# side of the square in which
# a regular polygon with even sides
# can completely embed
import math

# PI value in Python 3 using
# acos function
pi = math.acos(-1.0)

# Function to find the minimum
# side of the square in which
# a regular polygon with even sides
# can completely embed
def nGon(N):

    # Projection angle variation
    # from axes
    proAngleVar = 0

    # Projection angle variation
    # when the number of
    # sides are in multiple of 4
    if (N % 4 == 0):
        proAngleVar = (pi * (180.0 / N)
                       / 180)

    else:
        proAngleVar = (pi * (180.0 / (2 * N))
                       / 180)

    # Distance between the end points
    negX = 1.0e+99
    posX = -1.0e+99
    negY = 1.0e+99
    posY = -1.0e+99

    for j in range(N):

        # Projection from all N points
        # on X-axis
        px = math.cos(2 * pi * j / N
                      + proAngleVar)

        # Projection from all N points
        # on Y-axis
        py = math.sin(2 * pi * j / N
                      + proAngleVar)

        negX = min(negX, px)
        posX = max(posX, px)
        negY = min(negY, py)
        posY = max(posY, py)

    # Maximum side
    opt2 = max(posX - negX,
               posY - negY)

    # Return the portion of side
    # forming the square
    return (opt2 / math.sin(pi / N) / 2)

# Driver code
if __name__ == "__main__":

    N = 10
    print('%.5f'%nGon(N))

    # This code is contributed by ukasp.
```

## C#

```
// C# program to find the minimum
// side of the square in which
// a regular polygon with even sides
// can completely embed
using System;
class GFG{

// PI value in Java using
// acos function
static double pi = Math.Acos(-1.0);

// Function to find the minimum
// side of the square in which
// a regular polygon with even sides
// can completely embed
static double nGon(int N)
{

    // Projection angle variation
    // from axes
    double proAngleVar;

    // Projection angle variation
    // when the number of
    // sides are in multiple of 4
    if (N % 4 == 0)
    {
        proAngleVar = pi * (180.0 / N) / 180;
    }
    else
    {
        proAngleVar = pi * (180.0 / (2 * N)) / 180;
    }

    // Distance between the end points
    double negX = 1.0e+99,
           posX = -1.0e+99,
           negY = 1.0e+99,
           posY = -1.0e+99;

    for (int j = 0; j < N; ++j)
    {

        // Projection from all N points
        // on X-axis
        double px = Math.Cos(2 * pi * j / N +
                                proAngleVar);

        // Projection from all N points
        // on Y-axis
        double py = Math.Sin(2 * pi * j / N +
                                proAngleVar);

        negX = Math.Min(negX, px);
        posX = Math.Max(posX, px);
        negY = Math.Min(negY, py);
        posY = Math.Max(posY, py);
    }

    // Maximum side
    double opt2 = Math.Max(posX - negX,
                           posY - negY);

    // Return the portion of side
    // forming the square
    return (double)opt2 /
            Math.Sin(pi / N) / 2;
}

// Driver code
public static void Main()
{
    int N = 10;
    Console.Write(string.Format("{0:F5}", nGon(N)));
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>
// Javascript program to find the minimum
// side of the square in which
// a regular polygon with even sides
// can completely embed

    // PI value in Java using
    // acos function
     let pi = Math.acos(-1.0);

    // Function to find the minimum
    // side of the square in which
    // a regular polygon with even sides
    // can completely embed
    function nGon( N) {

        // Projection angle variation
        // from axes
        let proAngleVar;

        // Projection angle variation
        // when the number of
        // sides are in multiple of 4
        if (N % 4 == 0) {
            proAngleVar = pi * (180.0 / N) / 180;
        } else {
            proAngleVar = pi * (180.0 / (2 * N)) / 180;
        }

        // Distance between the end polets
        let negX = 1.0e+99, posX = -1.0e+99, negY = 1.0e+99, posY = -1.0e+99;

        for ( let j = 0; j < N; ++j) {

            // Projection from all N polets
            // on X-axis
            let px = Math.cos(2 * pi * j / N + proAngleVar);

            // Projection from all N polets
            // on Y-axis
            let py = Math.sin(2 * pi * j / N + proAngleVar);

            negX = Math.min(negX, px);
            posX = Math.max(posX, px);
            negY = Math.min(negY, py);
            posY = Math.max(posY, py);
        }

        // Maximum side
        let opt2 = Math.max(posX - negX, posY - negY);

        // Return the portion of side
        // forming the square
        return  opt2 / Math.sin(pi / N) / 2;
    }

    // Driver code
    let N = 10;
    document.write(nGon(N).toFixed(5));

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
3.19623
```

**时间复杂度:** *O(N)* ，其中 N 为多边形的边数。