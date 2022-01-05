# 将度数转换为弧度的程序

> 原文:[https://www . geesforgeks . org/program-to-convert-degree-to-radian/](https://www.geeksforgeeks.org/program-to-convert-degree-to-radian/)

给定**度**中的角度，任务是将其转换为弧度。
**例:**

```
Input: degree = 45 
Output: radian = 0.785398

Input: degree = 58
Output: radian = 1.01229
```

**进场:**
**弧度:**弧度是测量角度的 SI 单位，主要用于三角学。弧度是由圆弧定义的。一整圈刚好超过 6 弧度(大约 6.28)。一弧度刚好低于 57.3 度。
**度:**度通常用(度符号)表示，是平面角度的度量，定义为整个旋转为 360 度。因为完整的旋转等于 2 *π弧度，所以一个度数相当于π/180 弧度。
弧度转换成度数的公式为:

```
radian = degree * (pi/180) 
where pi = 22/7
```

以下是上述方法的实现:

## C++

```
// C++ program to convert degree to radian

#include <iostream>
#include <math.h>
using namespace std;

// Function for conversion
double Convert(double degree)
{
    double pi = 3.14159265359;
    return (degree * (pi / 180));
}

// Driver code
int main()
{
    double degree = 30;
    double radian = Convert(degree);
    cout << radian;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert degree to radian
import java.io.*;
import java.util.*;

class GFG {

// Function for conversion
static double Convert(double degree)
{
    double pi = 3.14159265359;

    return (degree * (pi / 180));
}

// Driver code
public static void main(String[] args)
{
    double degree = 30;
    double radian = Convert(degree);

    System.out.printf("%.6f", radian);
}
}

// This code is contributed by coder001   
```

## 蟒蛇 3

```
# Python3 program to convert degree to radian

# Function for conversion
def Convert(degree):

    pi = 3.14159265359;
    return (degree * (pi / 180));

# Driver code
degree = 30;
radian = Convert(degree);
print(radian);

# This code is contributed by Code_Mech
```

## C#

```
// C# program to convert degree to radian
using System;

class GFG{

// Function for conversion
static double Convert(double degree)
{
    double pi = 3.14159265359;

    return (degree * (pi / 180));
}

// Driver code
public static void Main()
{
    double degree = 30;
    double radian = Convert(degree);

    Console.Write("{0:F6}", radian);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to convert degree to radian

// Function for conversion
function Convert(degree)
{
    let pi = 3.14159265359;
    return (degree * (pi / 180));
}

// Driver code

    let degree = 30;
    let radian = Convert(degree);
    document.write(radian);

// This code is contributed Mayank Tyagi

</script>
```

**Output:** 

```
0.523599
```