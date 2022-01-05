# 一对线之间的角度

> 原文:[https://www . geesforgeks . org/线对角度/](https://www.geeksforgeeks.org/angle-between-a-pair-of-lines/)

给定两个整数 **M1** 和 **M2** 表示在一点相交的两条线的[斜率，任务是找出这两条线](https://www.geeksforgeeks.org/program-find-slope-line/)之间的[角。](https://en.wikipedia.org/wiki/Line%E2%80%93line_intersection)

**示例:**

> **输入:** M <sub>1</sub> = 1.75，M <sub>2</sub> = 0.27
> **输出:** 45.1455 度
> 
> **输入:** M <sub>1</sub> = 0.5，M <sub>2</sub> = 1.75
> **输出:** 33.6901 度

**逼近:**如果 **θ** 是两条相交直线之间的角度，那么角度 **θ** 可以通过下式计算:

> tano = |(m<sub>2</sub>–m<sub>1</sub>/(1+m<sub>1</sub>* m<sub>2</sub>)|
> =>θ= tan

按照以下步骤解决问题:

*   初始化一个变量，比如 **A** ，来存储两条线之间的角度值。
*   使用上述公式，找到 [**tan(A)**](https://www.geeksforgeeks.org/c-program-to-illustrate-trigonometric-functions/) 的值，并通过取角度的 [tan 逆来更新角度 **A** 的值。](https://www.geeksforgeeks.org/asin-atan-functions-cc-example/)
*   [将角度从弧度转换为度数](https://www.geeksforgeeks.org/program-convert-radian-degree/)。
*   打印 **A** 的数值作为结果，单位为度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define PI 3.14159265

// Function to find the
// angle between two lines
void findAngle(double M1, double M2)
{
    // Store the tan value  of the angle
    double angle = abs((M2 - M1)
                       / (1 + M1 * M2));

    // Calculate tan inverse of the angle
    double ret = atan(angle);

    // Convert the angle from
    // radian to degree
    double val = (ret * 180) / PI;

    // Print the result
    cout << val;
}

// Driver Code
int main()
{
    double M1 = 1.75, M2 = 0.27;

    findAngle(M1, M2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{
    static double PI = 3.14159265;

    // Function to find the
    // angle between two lines
    static void findAngle(double M1, double M2)
    {

        // Store the tan value  of the angle
        double angle = Math.abs((M2 - M1) / (1 + M1 * M2));

        // Calculate tan inverse of the angle
        double ret = Math.atan(angle);

        // Convert the angle from
        // radian to degree
        double val = (ret * 180) / PI;

        // Print the result
        System.out.println(val);
    }

    // Driver Code
    public static void main(String []args)
    {
        double M1 = 1.75, M2 = 0.27;

        findAngle(M1, M2);
    }
}

// This code is contributed by rrrtnx.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import atan

# Function to find the
# angle between two lines
def findAngle(M1, M2):
    PI = 3.14159265

    # Store the tan value  of the angle
    angle = abs((M2 - M1) / (1 + M1 * M2))

    # Calculate tan inverse of the angle
    ret = atan(angle)

    # Convert the angle from
    # radian to degree
    val = (ret * 180) / PI

    # Print the result
    print (round(val, 4))

# Driver Code
if __name__ == '__main__':
    M1 = 1.75
    M2 = 0.27

    findAngle(M1, M2)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{
    static double PI = 3.14159265;

    // Function to find the
    // angle between two lines
    static void findAngle(double M1, double M2)
    {

        // Store the tan value  of the angle
        double angle = Math.Abs((M2 - M1) / (1 + M1 * M2));

        // Calculate tan inverse of the angle
        double ret = Math.Atan(angle);

        // Convert the angle from
        // radian to degree
        double val = (ret * 180) / PI;

        // Print the result
        Console.Write(val);
    }

    // Driver Code
    public static void Main()
    {
        double M1 = 1.75, M2 = 0.27;

        findAngle(M1, M2);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

      // JavaScript program
      // for the above approach
      const PI = 3.14159265;

      // Function to find the
      // angle between two lines
      function findAngle(M1, M2) {
        // Store the tan value of the angle
        var angle = Math.abs((M2 - M1) / (1 + M1 * M2));

        // Calculate tan inverse of the angle
        var ret = Math.atan(angle);

        // Convert the angle from
        // radian to degree
        var val = (ret * 180) / PI;

        // Print the result
        document.write(val.toFixed(4));
      }

      // Driver Code
      var M1 = 1.75,
        M2 = 0.27;
      findAngle(M1, M2);

</script>
```

**Output:** 

```
45.1455
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)