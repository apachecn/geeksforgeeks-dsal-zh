# 给定初始角度和每角度增量的多边形的第 n 个角度

> 原文:[https://www . geeksforgeeks . org/n 给定初始角度和每角度增量的多边形角度/](https://www.geeksforgeeks.org/nth-angle-of-a-polygon-whose-initial-angle-and-per-angle-increment-is-given/)

给定四个整数 **N，A，K，n** ，其中 **N** 代表多边形的边数， **A** 代表多边形的初始角度， **K** 代表每增加一个角度，任务是找到具有 **N 条边**的多边形的 **n <sup>第</sup>T11】个角度。如果不可能，则打印 **-1** 。**

[![](img/e314c93ea17d0ac5227022c4b6829983.png)](https://media.geeksforgeeks.org/wp-content/uploads/20200723161016/polygon2.png)

**示例:**

> **输入:** N = 3，A = 30，K = 30，n = 3
> **输出:** 90
> **解释:**
> 三边多边形的第三个角是 90 度，因为所有的角都是 30 度、60 度、90 度。
> 
> **输入:** N = 4，A = 40，K = 30，n = 3
> **输出:** -1
> **说明:**
> 无法创建初始角度为 40，边数为 4 的多边形。

**方法:**想法是观察多边形的角度按照 [**等差数列**](https://www.geeksforgeeks.org/arithmetic-progression/) 增加 **K** 度的差。

*   求出 **N 边多边形**的角和以及**给定多边形**的角和。
*   检查两个值是否相等。如果是，那么第**个角度**是可能的，因此找到第**个角度**。
*   否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to check if the angle
// is possible or not
bool possible(int N, int a, int b, int n)
{
    // Angular sum of a N-sided polygon
    int sum_of_angle = 180 * (N - 2);

    // Angular sum of N-sided given polygon
    int Total_angle = (N * ((2 * a) + (N - 1) * b)) / 2;

    // Check if both sum are equal
    if (sum_of_angle != Total_angle)
        return false;
    else
        return true;
}

// Function to find the nth angle
int nth_angle(int N, int a,
              int b, int n)
{
    int nth = 0;

    // Calculate nth angle
    nth = a + (n - 1) * b;

    // Return the nth angle
    return nth;
}

// Driver Code
int main()
{

    int N = 3, a = 30, b = 30, n = 3;

    // Checks the possibility of the
    // polygon exist or not
    if (possible(N, a, b, n))

        // Print nth angle
        // of the polygon
        cout << nth_angle(N, a, b, n);
    else
        cout << "Not Possible";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if the angle
// is possible or not
static boolean possible(int N, int a,
                        int b, int n)
{

    // Angular sum of a N-sided polygon
    int sum_of_angle = 180 * (N - 2);

    // Angular sum of N-sided given polygon
    int Total_angle = (N * ((2 * a) +
                      (N - 1) * b)) / 2;

    // Check if both sum are equal
    if (sum_of_angle != Total_angle)
        return false;
    else
        return true;
}

// Function to find the nth angle
static int nth_angle(int N, int a,
                     int b, int n)
{
    int nth = 0;

    // Calculate nth angle
    nth = a + (n - 1) * b;

    // Return the nth angle
    return nth;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3, a = 30, b = 30, n = 3;

    // Checks the possibility of the
    // polygon exist or not
    if (possible(N, a, b, n))

        // Print nth angle
        // of the polygon
        System.out.print(nth_angle(N, a, b, n));
    else
        System.out.print("Not Possible");
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the angle
# is possible or not
def possible(N, a, b, n):

    # Angular sum of a N-sided polygon
    sum_of_angle = 180 * (N - 2)

    # Angular sum of N-sided given polygon
    Total_angle = (N * ((2 * a) +
                  (N - 1) * b)) / 2

    # Check if both sum are equal
    if (sum_of_angle != Total_angle):
        return False
    else:
        return True

# Function to find the nth angle
def nth_angle(N, a, b, n):
    nth = 0

    # Calculate nth angle
    nth = a + (n - 1) * b

    # Return the nth angle
    return nth

# Driver Code
if __name__ == '__main__':

    N = 3
    a = 30
    b = 30
    n = 3

    # Checks the possibility of the
    # polygon exist or not
    if (possible(N, a, b, n)):

        # Print nth angle
        # of the polygon
        print(nth_angle(N, a, b, n))
    else:
        print("Not Possible")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to check if the angle
// is possible or not
static bool possible(int N, int a,
                     int b, int n)
{

    // Angular sum of a N-sided polygon
    int sum_of_angle = 180 * (N - 2);

    // Angular sum of N-sided given polygon
    int Total_angle = (N * ((2 * a) +
                      (N - 1) * b)) / 2;

    // Check if both sum are equal
    if (sum_of_angle != Total_angle)
        return false;
    else
        return true;
}

// Function to find the nth angle
static int nth_angle(int N, int a,
                     int b, int n)
{
    int nth = 0;

    // Calculate nth angle
    nth = a + (n - 1) * b;

    // Return the nth angle
    return nth;
}

// Driver Code
public static void Main(string[] args)
{
    int N = 3, a = 30, b = 30, n = 3;

    // Checks the possibility of the
    // polygon exist or not
    if (possible(N, a, b, n))

        // Print nth angle
        // of the polygon
        Console.Write(nth_angle(N, a, b, n));
    else
        Console.Write("Not Possible");
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to check if the angle
// is possible or not
function possible(N, a, b, n)
{
    // Angular sum of a N-sided polygon
    let sum_of_angle = 180 * (N - 2);

    // Angular sum of N-sided given polygon
    let Total_angle = Math.floor((N * ((2 * a) + (N - 1) * b)) / 2);

    // Check if both sum are equal
    if (sum_of_angle != Total_angle)
        return false;
    else
        return true;
}

// Function to find the nth angle
function nth_angle(N, a, b, n)
{
    let nth = 0;

    // Calculate nth angle
    nth = a + (n - 1) * b;

    // Return the nth angle
    return nth;
}

// Driver Code

    let N = 3, a = 30, b = 30, n = 3;

    // Checks the possibility of the
    // polygon exist or not
    if (possible(N, a, b, n))

        // Print nth angle
        // of the polygon
        document.write(nth_angle(N, a, b, n));
    else
        document.write("Not Possible");

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
90
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)