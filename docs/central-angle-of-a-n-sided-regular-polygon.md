# 正多边形的中心角

> 原文:[https://www . geesforgeks . org/正多边形中心角/](https://www.geeksforgeeks.org/central-angle-of-a-n-sided-regular-polygon/)

给定一个代表 N 边正多边形的整数 **N** ，任务是找出多边形中心的边所成的角，即中心角。

> **中心角**是由形成一条边和中心的两个顶点形成的角度。

**示例:**

> **输入:** N = 6
> **输出:** 60
> **解释:**
> 多边形是一个 60 度角的六边形。
> 
> **输入:** N = 5
> **输出:** 72
> **解释:**
> 多边形是一个角为 72 度的五边形。

**方法:**想法是观察由于有一个正多边形，形成的所有中心角都将相等。
所有的中心角加起来是 360 度(一整圈)，所以中心角的度量是 360 度除以边数。

> 因此，**中心角= 360 / N 度**，其中 **N** 为边数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate central
// angle of a polygon
double calculate_angle(double n)
{
    // Calculate the angle
    double total_angle = 360;
    return total_angle / n;
}

// Driver code
int main()
{
    double N = 5;
    cout << calculate_angle(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to calculate central
// angle of a polygon
static double calculate_angle(double n)
{

    // Calculate the angle
    double total_angle = 360;
    return total_angle / n;
}

// Driver code
public static void main(String[] args)
{
    double N = 5;

    System.out.println(calculate_angle(N));
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate central
# angle of a polygon
def calculate_angle(n):

    # Calculate the angle
    total_angle = 360;
    return (total_angle // n)

# Driver code 
N = 5

print(calculate_angle(N))

# This code is contributed by rameshtravel07
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate central
// angle of a polygon
static double calculate_angle(double n)
{

    // Calculate the angle
    double total_angle = 360;
    return total_angle / n;
}

// Driver code
public static void Main()
{
    double N = 5;

    Console.WriteLine(calculate_angle(N));
}
}

// This code is contributed by Ankita saini
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate central
// angle of a polygon
function calculate_angle(n)
{

    // Calculate the angle
    var total_angle = 360;
    return total_angle / n;
}

// Driver code
var N = 5;

document.write(calculate_angle(N));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
72
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*