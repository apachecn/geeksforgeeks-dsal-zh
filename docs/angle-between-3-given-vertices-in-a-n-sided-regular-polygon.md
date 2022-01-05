# n 边正多边形中 3 个给定顶点之间的角度

> 原文:[https://www . geesforgeks . org/n 边正多边形中 3 个给定顶点之间的角度/](https://www.geeksforgeeks.org/angle-between-3-given-vertices-in-a-n-sided-regular-polygon/)

给定一个 n 边正多边形和三个顶点 **a1** 、 **a2** 和 **a3** ，任务是求顶点 a2 和顶点 a3 在顶点 a1 处悬挂的角度。

**示例:**

```
Input: n = 6, a1 = 1, a2 = 2, a3 = 4
Output: 90

Input: n = 5, a1 = 1, a2 = 2, a3 = 5
Output: 36
```

**进场:**

1.  n 边正多边形中心边对着的角度为 **360/n** 。
2.  由 k 条边分开的顶点对着的角度变成 **(360*k)/n** 。
3.  顶点之间的弦对着一个角，该角的一半对着第三个顶点的中心，第三个顶点是外接圆圆周上的一个点。
4.  让以这种方式获得的角度为 **a = (180*x)/n** ，其中 k 是 I 和 k 之间的边数。
5.  类似地，对于相反的顶点，我们得到的角度是 **b = (180*y)/n** ，其中 l 是 j 和 k 之间的边数。
6.  因此，三个顶点之间的角度等于**180°-a-b**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function that checks whether given angle
// can be created using any 3 sides
double calculate_angle(int n, int i, int j, int k)
{
    // Initialize x and y
    int x, y;

    // Calculate the number of vertices
    // between i and j, j and k
    if (i < j)
        x = j - i;
    else
        x = j + n - i;
    if (j < k)
        y = k - j;
    else
        y = k + n - j;

    // Calculate the angle subtended
    // at the circumference
    double ang1 = (180 * x) / n;
    double ang2 = (180 * y) / n;

    // Angle subtended at j can be found
    // using the fact that the sum of angles
    // of a triangle is equal to 180 degrees
    double ans = 180 - ang1 - ang2;
    return ans;
}

// Driver code
int main()
{
    int n = 5;
    int a1 = 1;
    int a2 = 2;
    int a3 = 5;

    cout << calculate_angle(n, a1, a2, a3);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that checks whether given angle
// can be created using any 3 sides
static double calculate_angle(int n, int i,
                              int j, int k)
{
    // Initialize x and y
    int x, y;

    // Calculate the number of vertices
    // between i and j, j and k
    if (i < j)
        x = j - i;
    else
        x = j + n - i;
    if (j < k)
        y = k - j;
    else
        y = k + n - j;

    // Calculate the angle subtended
    // at the circumference
    double ang1 = (180 * x) / n;
    double ang2 = (180 * y) / n;

    // Angle subtended at j can be found
    // using the fact that the sum of angles
    // of a triangle is equal to 180 degrees
    double ans = 180 - ang1 - ang2;
    return ans;
}

// Driver code
public static void main (String[] args)
{
    int n = 5;
    int a1 = 1;
    int a2 = 2;
    int a3 = 5;

    System.out.println((int)calculate_angle(n, a1, a2, a3));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that checks whether given angle
# can be created using any 3 sides
def calculate_angle(n, i, j, k):

    # Initialize x and y
    x, y = 0, 0

    # Calculate the number of vertices
    # between i and j, j and k
    if (i < j):
        x = j - i
    else:
        x = j + n - i
    if (j < k):
        y = k - j
    else:
        y = k + n - j

    # Calculate the angle subtended
    # at the circumference
    ang1 = (180 * x) // n
    ang2 = (180 * y) // n

    # Angle subtended at j can be found
    # using the fact that the sum of angles
    # of a triangle is equal to 180 degrees
    ans = 180 - ang1 - ang2
    return ans

# Driver code
n = 5
a1 = 1
a2 = 2
a3 = 5

print(calculate_angle(n, a1, a2, a3))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that checks whether given angle
// can be created using any 3 sides
static double calculate_angle(int n, int i,
                              int j, int k)
{
    // Initialize x and y
    int x, y;

    // Calculate the number of vertices
    // between i and j, j and k
    if (i < j)
        x = j - i;
    else
        x = j + n - i;
    if (j < k)
        y = k - j;
    else
        y = k + n - j;

    // Calculate the angle subtended
    // at the circumference
    double ang1 = (180 * x) / n;
    double ang2 = (180 * y) / n;

    // Angle subtended at j can be found
    // using the fact that the sum of angles
    // of a triangle is equal to 180 degrees
    double ans = 180 - ang1 - ang2;
    return ans;
}

// Driver code
public static void Main ()
{
    int n = 5;
    int a1 = 1;
    int a2 = 2;
    int a3 = 5;

    Console.WriteLine((int)calculate_angle(n, a1, a2, a3));
}
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
// Function that checks whether given angle
// can be created using any 3 sides
function calculate_angle(n , i, j , k)
{
    // Initialize x and y
    var x, y;

    // Calculate the number of vertices
    // between i and j, j and k
    if (i < j)
        x = j - i;
    else
        x = j + n - i;
    if (j < k)
        y = k - j;
    else
        y = k + n - j;

    // Calculate the angle subtended
    // at the circumference
    var ang1 = (180 * x) / n;
    var ang2 = (180 * y) / n;

    // Angle subtended at j can be found
    // using the fact that the sum of angles
    // of a triangle is equal to 180 degrees
    var ans = 180 - ang1 - ang2;
    return ans;
}

// Driver code
var n = 5;
var a1 = 1;
var a2 = 2;
var a3 = 5;

document.write(parseInt(calculate_angle(n, a1, a2, a3)));

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
36
```