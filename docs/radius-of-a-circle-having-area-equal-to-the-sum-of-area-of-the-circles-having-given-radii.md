# 面积等于给定半径的圆的面积之和的圆的半径

> 原文:[https://www . geeksforgeeks . org/面积等于给定半径圆面积总和的圆半径/](https://www.geeksforgeeks.org/radius-of-a-circle-having-area-equal-to-the-sum-of-area-of-the-circles-having-given-radii/)

给定两个整数 **r1** 和 **r2** ，代表两个圆的半径，任务是求面积等于给定半径的两个圆的面积之和的圆的[半径。](https://www.geeksforgeeks.org/radius-of-the-circle-when-the-width-and-height-of-an-arc-is-given/)

**示例:**

> **输入:**
> R1 = 8
> R2 = 6
> T5】输出:
> 10
> **说明:**
> 半径为 8 的圆面积= 201.061929
> 半径为 6 的圆面积= 113.097335
> 半径为 10 的圆面积= 314.159265
> 
> **输入:**
> R1 = 2
> R2 = 2
> T5】输出:
> 2.82843

**方法:**按照以下步骤解决问题:

1.  计算第一个圆的面积为 **a1 = 3.14 * r1 * r1** 。
2.  计算第二个圆的面积为 **a2 = 3.14 * r2 * r2** 。
3.  因此，第三个圆的面积为 **a1 + a2** 。
4.  第三个圆的半径为 **sqrt(a3 / 3.14)**

下面是以下方法的实现。

## C++14

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate radius of the circle
// having area equal to sum of the area of
// two circles with given radii
double findRadius(double r1, double r2)
{
    double a1, a2, a3, r3;

    // Area of first circle
    a1 = 3.14 * r1 * r1;

    // Area of second circle
    a2 = 3.14 * r2 * r2;

    // Area of third circle
    a3 = a1 + a2;

    // Radius of third circle
    r3 = sqrt(a3 / 3.14);

    return r3;
}

// Driver Code
int main()
{
    // Given radius
    double r1 = 8, r2 = 6;

    // Prints the radius of
    // the required circle
    cout << findRadius(r1, r2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{

// Function to calculate radius of the circle
// having area equal to sum of the area of
// two circles with given radii
static double findRadius(double r1, double r2)
{
    double a1, a2, a3, r3;

    // Area of first circle
    a1 = 3.14 * r1 * r1;

    // Area of second circle
    a2 = 3.14 * r2 * r2;

    // Area of third circle
    a3 = a1 + a2;

    // Radius of third circle
    r3 = Math.sqrt(a3 / 3.14);
    return r3;
}

// Driver code
public static void main(String[] args)
{

    // Given radius
    double r1 = 8, r2 = 6;

    // Prints the radius of
    // the required circle
    System.out.println((int)findRadius(r1, r2));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to calculate radius of the circle
# having area equal to sum of the area of
# two circles with given radii
def findRadius(r1, r2):
    a1, a2, a3, r3 = 0, 0, 0, 0;

    # Area of first circle
    a1 = 3.14 * r1 * r1;

    # Area of second circle
    a2 = 3.14 * r2 * r2;

    # Area of third circle
    a3 = a1 + a2;

    # Radius of third circle
    r3 = ((a3 / 3.14)**(1/2));
    return r3;

# Driver code
if __name__ == '__main__':

    # Given radius
    r1 = 8; r2 = 6;

    # Prints the radius of
    # the required circle
    print(int(findRadius(r1, r2)));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

// Function to calculate radius of the circle
// having area equal to sum of the area of
// two circles with given radii
static double findRadius(double r1, double r2)
{
    double a1, a2, a3, r3;

    // Area of first circle
    a1 = 3.14 * r1 * r1;

    // Area of second circle
    a2 = 3.14 * r2 * r2;

    // Area of third circle
    a3 = a1 + a2;

    // Radius of third circle
    r3 = Math.Sqrt(a3 / 3.14);
    return r3;
}

  // Driver code
  static void Main()
  {

    // Given radius
    double r1 = 8, r2 = 6;

    // Prints the radius of
    // the required circle
    Console.WriteLine((int)findRadius(r1, r2));
  }
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// Javascript program of the above approach

 // Function to calculate radius of the circle
// having area equal to sum of the area of
// two circles with given radii
function findRadius(r1, r2)
{
    let a1, a2, a3, r3;

    // Area of first circle
    a1 = 3.14 * r1 * r1;

    // Area of second circle
    a2 = 3.14 * r2 * r2;

    // Area of third circle
    a3 = a1 + a2;

    // Radius of third circle
    r3 = Math.sqrt(a3 / 3.14);
    return r3;
}

    // Driver Code

    // Given radius
    let r1 = 8, r2 = 6;

    // Prints the radius of
    // the required circle
    document.write(findRadius(r1, r2));

</script>
```

**Output:** 

```
10
```

***时间复杂度** : O(1)*
***空间复杂度:** O(1)*