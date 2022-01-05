# 长、宽、高按固定百分比增加时长方体体积的百分比增加

> 原文:[https://www . geesforgeks . org/如果长宽高按固定百分比增加，长方体的体积增加百分比/](https://www.geeksforgeeks.org/percentage-increase-in-the-volume-of-cuboid-if-length-breadth-and-height-are-increased-by-fixed-percentages/)

给定一个长方体和三个整数 **L** 、 **B** 和 **H** 。如果长方体的长度增加 **L%** ，宽度增加 **B%** ，高度增加 **H%** 。任务是找出长方体体积增加的百分比。
**示例:**

> **输入:** L = 50，B = 20，H = 10
> **输出:** 98%
> **输入:** L = 10，B = 20，H = 30
> **输出:** 71.6%

**逼近:**假设长方体原来的长、宽、高分别为 **l** 、 **b** 和 **h** 。现在，增加的长度将是 **(l + ((L * l) / 100))** 即**增加的长度= l * (1 + (L / 100))** 。同样，增加的宽度和高度将是**增加的宽度= b * (1 + (B / 100))** 和**增加的高度= h * (1 + (H / 100))** 。
现在，计算**原始 ol = l * b * h** 和**增加的体积=增加的长度*增加的读数*增加的高度**。
并且，增加的百分比可以找到为**((增加的体积–原始体积)/原始体积)* 100**

> (((L *(1+(L/100))* B *(1+(B/100))H *(1+(H/100)))–(L * B * H))/(L * B * H))* 100
> ((L * B * H *(1+(L/100))*(1+(B/100))*(H/100))–1)/(L * B * H))* 100
> **((1)**

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the percentage increase
// in the volume of the cuboid
double increaseInVol(double l, double b, double h)
{
    double percentInc = (1 + (l / 100))
                        * (1 + (b / 100))
                        * (1 + (h / 100));
    percentInc -= 1;
    percentInc *= 100;

    return percentInc;
}

// Driver code
int main()
{
    double l = 50, b = 20, h = 10;
    cout << increaseInVol(l, b, h) << "%";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the percentage increase
// in the volume of the cuboid
static double increaseInVol(double l,  
                            double b,
                            double h)
{
    double percentInc = (1 + (l / 100)) *
                        (1 + (b / 100)) *
                        (1 + (h / 100));
    percentInc -= 1;
    percentInc *= 100;

    return percentInc;
}

// Driver code
public static void main(String[] args)
{
    double l = 50, b = 20, h = 10;
    System.out.println(increaseInVol(l, b, h) + "%");
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the percentage increase
# in the volume of the cuboid
def increaseInVol(l, b, h):
    percentInc = ((1 + (l / 100)) *
                  (1 + (b / 100)) *
                  (1 + (h / 100)))
    percentInc -= 1
    percentInc *= 100

    return percentInc

# Driver code
l = 50
b = 20
h = 10
print(increaseInVol(l, b, h), "%")

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the percentage increase
// in the volume of the cuboid
static double increaseInVol(double l,
                            double b,
                            double h)
{
    double percentInc = (1 + (l / 100)) *
                        (1 + (b / 100)) *
                        (1 + (h / 100));
    percentInc -= 1;
    percentInc *= 100;

    return percentInc;
}

// Driver code
public static void Main()
{
    double l = 50, b = 20, h = 10;
    Console.WriteLine(increaseInVol(l, b, h) + "%");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the percentage increase
// in the volume of the cuboid
function increaseInVol(l, b, h)
{
    let percentInc = (1 + (l / 100))
                        * (1 + (b / 100))
                        * (1 + (h / 100));
    percentInc -= 1;
    percentInc *= 100;

    return percentInc;
}

// Driver code
    let l = 50, b = 20, h = 10;
    document.write(increaseInVol(l, b, h) + "%");

</script>
```

**Output:** 

```
98%
```