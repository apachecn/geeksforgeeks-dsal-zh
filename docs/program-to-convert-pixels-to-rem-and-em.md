# 将像素转换为 rem 和 em 的程序

> 原文:[https://www . geesforgeks . org/program-to-convert-pixels-to-rem-and-em/](https://www.geeksforgeeks.org/program-to-convert-pixels-to-rem-and-em/)

给定一个以[像素](https://www.geeksforgeeks.org/program-to-convert-centimeters-to-pixels/)表示盒子宽度的整数**像素**，任务是将**像素**转换为以 [rem 和 em](https://www.geeksforgeeks.org/css-units/) 单位测量的它们的等值。

**示例:**

> **输入:**像素= 45
> **输出:** em = 2.812500，rem = 2.812500
> 
> **输入:**像素= 160
> **输出:** em = 10，rem = 10

**逼近:**问题可以基于以下数学关系求解:

> 对于现代浏览器来说，
> 
> *   1 雷姆= 16 px
>     因此，1px = 0.0625 雷姆
> *   1 em = 16 px
>     因此，1 px = 0.0625 em

按照以下步骤解决问题:

*   通过将像素乘以 **0.0625，计算**像素**在 [rem 和 em](https://www.geeksforgeeks.org/css-units/) 中的等值。**
*   以 [rem 和 em](https://www.geeksforgeeks.org/css-units/) 为单位打印像素的等值。

下面是上述方法的实现:

## C++

```
// C++ program to convert
// pixels to rem and em
#include <bits/stdc++.h>
using namespace std;

// Function to convert
// pixels to rem and em
void Conversion(double pixels)
{

    double rem = 0.0625 * pixels;
    double em = 0.0625 * pixels;

    cout << fixed << setprecision(6)
         << "The value in em is " << em << endl;

    cout << fixed << setprecision(6)
         << "The value in rem is " << rem << endl;
}

// Driver Code
int main()
{
    // Input
    double PX = 45;
    Conversion(PX);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert pixel to rem and em

import java.io.*;

class GFG {

    // Function to convert pixel to rem and em
    static double Conversion(double pixel)
    {
        double rem = 0.0625 * pixel;
        double em = 0.0625 * pixel;
        System.out.println("The value in rem is " + rem);
        System.out.println("The value in em is " + em);
        return 0;
    }

    // Driver Code
    public static void main(String args[])
    {
        double pixels = 45;
        Conversion(pixels);
    }
}
```

## 计算机编程语言

```
# Python program to convert pixel to rem and em

# Function to convert pixel to rem and em

def Conversion(pixel):
    rem = 0.0625 * pixel
    em = 0.0625 * pixel
    print "The value in em is", round(em, 2)
    print "The value in rem is", round(rem, 2)

# Driver Code
pixel = 45
Conversion(pixel)
```

## C#

```
// C# program to convert pixel to rem and em
using System;

class GFG {

    // Function to convert pixel to rem and em
    static double Conversion(double pixel)
    {
        double rem = 0.0625 * pixel;
        double em = 0.0625 * pixel;
        Console.WriteLine("The value in em is " + em);
        Console.WriteLine("The value in rem is " + rem);

        return 0;
    }

    // Driver Code
    public static void Main()
    {
        double pixel = 45;
        Conversion(pixel);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP program to convert pixel to rem and em
// Function to convert pixel to rem and em
function Conversion($pixel)
{

    $rem = 0.0625 * $pixel;
      $em =  0.0625 * $pixel;

      echo("The value in em is " . $em . "\n");
    echo("The value in rem is " . $rem . "\n");

}

// Driver Code
$pixel = 45;
Conversion($pixel);
?>
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to convert pixel to rem and em
    function Conversion(pixel)
    {
        let rem = 0.0625 * pixel;
        let em = 0.0625 * pixel;
        document.write(
        "The value in rem is " + rem + "<br/>"
        );
        document.write(
        "The value in em is " + em
        );
        return 0;
    }

    // Driver Code

    let pixels = 45;
    Conversion(pixels);

</script>
```

**Output:** 

```
The value in em is 2.812500
The value in rem is 2.812500
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)