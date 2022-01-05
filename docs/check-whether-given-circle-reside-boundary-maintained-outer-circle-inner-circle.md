# 检查给定的圆是否位于另外两个圆所保持的边界内

> 原文:[https://www . geesforgeks . org/check-是否-给定-圆-驻留-边界-维护-外圆-内圆/](https://www.geeksforgeeks.org/check-whether-given-circle-reside-boundary-maintained-outer-circle-inner-circle/)

给定外圆半径 R 和内圆半径 R，从同一中心做圆，并在它们之间形成边界。现在，给定 X，Y 坐标，该坐标表示要用半径 rad 形成的新圆的中心，您的任务是检查以坐标 X，Y 为中心的圆是否能适合形成的圆的边界。
示例:

```
Input : R = 8, r = 4
x = 5, y = 3, rad = 1
Output : Fits

Input :  R = 8, r = 4
x = 5, y = 3,  rad = 3.
Output : Doesn't Fit
```

![Check whether given circle resides in boundary maintained by two other circles](img/09ab8334abecc367ba9119d4d7e9c3c7.png)

1–不拟合
2–拟合
思路是计算圆心(0，0)与被检圆坐标的距离。如果距离+半径(待检圆)小于或等于外半径，距离-半径(待检圆)大于或等于外圆半径-半径内圆
则符合。

下面是实现:

## C++

```
// CPP program to check whether circle with given 
// co-ordinates reside within the boundary 
// of outer circle and inner circle
#include <bits/stdc++.h>
using namespace std;

// function to check if given circle fit in 
// boundary or not 
void fitOrNotFit(int R, int r, int x, int y,
                                 int rad) {

    // Distance from the center
    double val = sqrt(pow(x, 2) + pow(y, 2));

    // Checking the corners of circle
    if (val + rad <= R && val - rad >= R - r)    
        cout << "Fits\n";    
    else
        cout << "Doesn't Fit\n";
}

// driver program
int main()
{
    // Radius of outer circle and inner circle
    // respectively
    int R = 8, r = 4;

    // Co-ordinates and radius of the circle
    // to be checked 
    int x = 5, y = 3, rad = 3;
    fitOrNotFit(R, r, x, y, rad);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check whether circle with given 
// co-ordinates reside within the boundary 
// of outer circle and inner circle
import java.util.*;

class GFG
{
// function to check if given circle fit in 
// boundary or not 
static void fitOrNotFit(int R, int r, int x, int y,
                                        int rad)
{
    // Distance from the center
    double val = Math.sqrt(Math.pow(x, 2) + 
                           Math.pow(y, 2));

    // Checking the corners of circle
    if (val + rad <= R && val - rad >= R - r) 
        System.out.println("Fits"); 
    else
    System.out.println("Doesn't Fit");     
}

// driver program
public static void main (String[] args)
{
    // Radius of outer circle and inner circle
    // respectively
    int R = 8, r = 4;

    // Co-ordinates and radius of the circle
    // to be checked 
    int x = 5, y = 3, rad = 3;
    fitOrNotFit(R, r, x, y, rad);
}
}
/* This Code is contributed by Kriti Shukla */
```

## 蟒蛇 3

```
# Python3 program to check
# whether circle with given 
# co-ordinates reside
# within the boundary 
# of outer circle
# and inner circle

import math

# function to check if
# given circle fit in 
# boundary or not 
def fitOrNotFit(R, r, x, y, rad) :

    # Distance from the center
    val = math.sqrt(math.pow(x, 2) + math.pow(y, 2)) 

    # Checking the corners of circle
    if (val + rad <= R and val - rad >= R - r) :
        print("Fits\n")  
    else:
        print("Doesn't Fit") 

# driver program

# Radius of outer circle and inner circle
# respectively
R = 8
r = 4 

# Co-ordinates and radius of the circle
# to be checked 
x = 5
y = 3
rad = 3 

fitOrNotFit(R, r, x, y, rad) 

# This code is contributed by 
# Smitha Dinesh Semwal
```

## C#

```
// C# program to check whether circle with given 
// co-ordinates reside within the boundary 
// of outer circle and inner circle
using System;

class GFG
{
    // function to check if given circle fit in 
    // boundary or not 
    static void fitOrNotFit(int R, int r, int x, int y,
                                            int rad)
    {
        // Distance from the center
        double val = Math.Sqrt(Math.Pow(x, 2) + 
                               Math.Pow(y, 2));

        // Checking the corners of circle
        if (val + rad <= R && val - rad >= R - r) 
            Console.WriteLine("Fits"); 
        else
        Console.WriteLine("Doesn't Fit");     
    }

    // Driver program
    public static void Main ()
    {
        // Radius of outer circle and inner circle
        // respectively
        int R = 8, r = 4;

        // Co-ordinates and radius of the circle
        // to be checked 
        int x = 5, y = 3, rad = 3;
        fitOrNotFit(R, r, x, y, rad);
    }
}

// This Code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check whether
// circle with given co-ordinates 
// reside within the boundary 
// of outer circle and inner circle

// function to check if given  
// circle fit in boundary or not 
function fitOrNotFit($R, $r, $x, $y,
                               $rad) 
{

    // Distance from the center
    $val = sqrt(pow($x, 2) + pow($y, 2));

    // Checking the corners of circle
    if ($val + $rad <= $R && $val - 
                  $rad >= $R - $r) 
        echo"Fits\n"; 
    else
        echo "Doesn't Fit\n";
}

    // Driver Code

    // Radius of outer circle and 
    // inner circle respectively
    $R = 8; $r = 4;

    // Co-ordinates and radius of 
    // the circle to be checked 
    $x = 5; $y = 3; $rad = 3;
    fitOrNotFit($R, $r, $x, $y, $rad);

// This Code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

// Javascript program to check whether circle with given 
// co-ordinates reside within the boundary 
// of outer circle and inner circle

// function to check if given circle fit in 
// boundary or not 
function fitOrNotFit(R, r, x, y, rad) {

    // Distance from the center
    var val = Math.sqrt(Math.pow(x, 2) + Math.pow(y, 2));

    // Checking the corners of circle
    if (val + rad <= R && val - rad >= R - r)    
        document.write( "Fits<br>");    
    else
        document.write( "Doesn't Fit<br>");
}

// driver program
// Radius of outer circle and inner circle
// respectively
var R = 8, r = 4;

// Co-ordinates and radius of the circle
// to be checked 
var x = 5, y = 3, rad = 3;
fitOrNotFit(R, r, x, y, rad);

</script>
```

输出:

```
Doesn't Fit
```

本文由 [**罗希特·塔普利亚尔**](https://www.hackerrank.com/rohit_thapliyal) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。