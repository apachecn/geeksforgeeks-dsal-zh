# 将弧度转换为度数的程序

> 原文:[https://www . geesforgeks . org/program-convert-radian-degree/](https://www.geeksforgeeks.org/program-convert-radian-degree/)

在进入实际解决方案之前，让我们试着找出什么是度数、弧度以及它们之间的关系。

**弧度:**弧度是角度测量的标准单位，在数学的很多领域都有使用。单位圆的弧长在数值上等于它对着的角度的弧度度量。一弧度刚好低于 57.3 度。

**度:**度(完整的，弧度、弧度或弧度)，通常用(度符号)表示，是平面角度的度量，定义为完整的旋转为 360 度。
关系 2pi*rad = 360 可以用[弧长](https://www.geeksforgeeks.org/arc-length-angle/)的公式推导出来。

与圆半径相同长度的圆弧对着 1 弧度的角。圆周对着 2pi 弧度的角度。

因此，公式为:

```
degree = radian * (180/pi)
where, pi = 22/7
```

**示例:**

```
Input : radian = 20
Output : degree = 1145.4545454545455
Explanation: degree = 20 * (180/pi)

Input : radian = 5
Output : degree = 286.3636363636364
Explanation : degree = 20 * (180/pi)
```

**注:**在本程序中，我们将 pi 的值取为 3.14159，得到三种语言的标准结果。

## C++

```
// C++ code to convert radian to degree
#include <iostream>
using namespace std;

// Function for convertion
double Convert(double radian)
{
    double pi = 3.14159;
    return(radian * (180 / pi));
}

// Driver code
int main()
{
    double radian = 5.0;
    double degree = Convert(radian);

    cout << degree;
    return 0;
}

// This code is contributed by Khushboogoyal499
```

## C

```
// C code to convert radian to degree

#include <stdio.h>

// Function for convertion
double Convert(double radian){
    double pi = 3.14159;
    return(radian * (180/pi));
}

// Driver Code
int main(){
    double radian = 5.0;
    double degree = Convert(radian);
    printf("%.5lf", degree);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to convert radian to degree

import java.io.*;
class GFG {
    // Function for convertion
    static double Convert(double radian){
        double pi = 3.14159;
        return(radian * (180/pi));
    }
    // Driver Code
    public static void main (String[] args) {
        double radian = 5.0;
        double degree = Convert(radian);
        System.out.println("degree = "+ degree);
    }
}
```

## 蟒蛇 3

```
# Python code to convert radian to degree

# Function for convertion
def Convert(radian):
    pi = 3.14159
    # Simply used the formula
    degree = radian * (180/pi)
    return degree

# Driver Code
radian = 5
print("degree =",(Convert(radian)))
```

## C#

```
// C# code to convert radian to degree.
using System;

class GFG {

    // Function for convertion
    static double Convert(double radian){
        double pi = 3.14159;
        return(radian * (180 / pi));
    }

    // Driver Code
    public static void Main () {
        double radian = 5.0;
        double degree = Convert(radian);
        Console.Write("degree = " + degree);
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to convert radian to degree

// Function for convertion
function Convert($radian)
{
    $pi = 3.14159;
    return($radian * (180 / $pi));
}

// Driver Code
$radian = 5.0;
$degree = Convert($radian);
echo( $degree);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// Javascript code to convert radian to degree

// Function for convertion
function Convert(radian){
    let pi = 3.14159;
    return(radian * (180/pi));
}

// Driver Code

    let radian = 5.0;
    let degree = Convert(radian);
    document.write(degree);

// This code is contributed Mayank Tyagi

</script>
```

**输出:**

```
286.47914
```

**参考资料:**
[【https://en . Wikipedia . org/wiki/radian】](https://en.wikipedia.org/wiki/Radian)[【https://en . Wikipedia . org/wiki/degree _(angle)](https://en.wikipedia.org/wiki/Degree_(angle))