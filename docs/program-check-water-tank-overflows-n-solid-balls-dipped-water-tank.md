# 当 n 个固体球浸入水箱时，检查水箱是否溢出的程序

> 原文:[https://www . geesforgeks . org/program-check-水箱-溢流-n-固球-浸渍-水箱/](https://www.geeksforgeeks.org/program-check-water-tank-overflows-n-solid-balls-dipped-water-tank/)

给定圆柱形水箱的尺寸、球形固体球和水箱中的水量，检查当球浸入水箱时水箱是否会溢出。
**例:**

```
input : H = 10, r =  5
        h = 5
        N = 2, R = 2
output : Not in overflow state
Explanation :
water tank capacity = 3.14 * r * r * H
                    = 3.14 * 5 * 5 * 10
                    = 785 

volume of water in tank = 3.14 * r * r * h
                        = 3.14 * 5 * 5 * 5
                        = 392.5

Volume of balls = N * (4/3) * 3.14 * R * R * R
                = 2 * (4/3) * 3.14 * 2 * 2 * 2
                = 67.02
Total volume of water + dip balls = 392.5 + 67.02
                                  = 459.52

Total volume (459.02) < tank capacity (785)
So, there is no overflow in tank

input : H = 5, r = 3 
        h = 3
        N = 3, R = 2
output : Overflow
Explanation:
water tank capacity = 3.14 * r * r * H
                    = 3.14 * 3 * 3 * 5
                    = 141.3

volume of water in tank = 3.14 * r * r * h
                        = 3.14 * 3 * 3 * 3
                        = 84.78

volume of balls = N * (4/3) * 3.14 * R * R * R
                = 3 * (4/3) * 3.14 * 2 * 2 * 2
                = 100.48

Total volume of water + dip balls = 84.78 + 100.48
                                  = 185.26

Total volume (185.26) > tank capacity (141.3)
So, tank will overflow
```

**方法:**
当固体球浸入水中时，水位增加，因此水的体积也会增加。
增加水量=浸球总体积
圆柱体体积= 3.14 * r * r * h
式中:R:水箱半径
h:水箱高度
球数为 n
球呈球体形状
球体体积=(4/3)* 3.14 * R * R
式中:R:球体(实心球)半径
浸完所有球后， 如果水和所有球的总体积小于或等于水箱容量的总体积，则水箱中不会有溢流，否则会有溢流。
以下是上述方法的实施:

## C++

```
// C++ Program to check if water tank
// overflows when n solid balls are
// dipped in the water tank
#include <bits/stdc++.h>
using namespace std;

// function to find if tak will
// overflow or not
void overflow(int H, int r, int h,
              int N, int R)
{
    // cylinder capacity
    float tank_cap = 3.14 * r * r * H;

    // volume of water in tank
    float water_vol = 3.14 * r * r * h;

    // volume of n balls
    float balls_vol = N * (4 / 3) * 3.14 * R * R * R;

    // total volume of water
    // and n dipped balls
    float vol = water_vol + balls_vol;

    /* condition to check if tank is in
    overflow state or not */
    if (vol > tank_cap) {
        cout << "Overflow" << endl;
    }
    else {
        cout << "Not in overflow state"
             << endl;
    }
}

// main function
int main()
{
    // giving dimensions
    int H = 10, r = 5, h = 5,
        N = 2, R = 2;

    // calling function
    overflow(H, r, h, N, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Program to check if
// water tank overflows
import java.util.*;

class GFG {

    // function to find if tak will
    // overflow or not
    static void overflow(int H, int r, int h,
                         int N, int R)
    {
        // cylinder capacity
        double tank_cap = 3.14 * r * r * H;

        // volume of water in tank
        double water_vol = 3.14 * r * r * h;

        // volume of n balls
        double balls_vol = N * (4 / 3) * 3.14 * R * R * R;

        // total volume of water
        // and n dipped balls
        double vol = water_vol + balls_vol;

        /* condition to check if tank is in
        overflow state or not */
        if (vol > tank_cap) {
            System.out.println("Overflow");
        }
        else {
            System.out.println("Not in overflow state");
        }
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        // giving dimensions
        int H = 10, r = 5, h = 5,
            N = 2, R = 2;

        // calling function
        overflow(H, r, h, N, R);
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python code to check if water tank
# overflows when n solid balls are
# dipped in the water tank

# function to find if tak will
# overflow or not
def overflow( H, r, h, N, R ):

    # cylinder capacity
    tank_cap = 3.14 * r * r * H

    # volume of water in tank
    water_vol = 3.14 * r * r * h

    # volume of n balls
    balls_vol = N * (4 / 3) * 3.14 * R * R * R

    # total volume of water
    # and n dipped balls
    vol = water_vol + balls_vol

    # condition to check if tank is in
    # overflow state or not
    if vol > tank_cap:
        print("Overflow")
    else:
        print("Not in overflow state")

# Driver code

# giving dimensions
H = 10
r = 5
h = 5
N = 2
R = 2

# calling function
overflow (H, r, h, N, R)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# Code for Program to check if
// water tank overflows
using System;

class GFG {

    // function to find if tak will
    // overflow or not
    static void overflow(int H, int r, int h,
                         int N, int R)
    {
        // cylinder capacity
        double tank_cap = 3.14 * r * r * H;

        // volume of water in tank
        double water_vol = 3.14 * r * r * h;

        // volume of n balls
        double balls_vol = N * (4 / 3) * 3.14 * R * R * R;

        // total volume of water
        // and n dipped balls
        double vol = water_vol + balls_vol;

        /* condition to check if tank is in
        overflow state or not */
        if (vol > tank_cap) {
            Console.WriteLine("Overflow");
        }
        else {
            Console.WriteLine("Not in overflow state");
        }
    }

    /* Driver program to test above function */
    public static void Main()
    {
        // giving dimensions
        int H = 10, r = 5, h = 5,
            N = 2, R = 2;

        // calling function
        overflow(H, r, h, N, R);
    }
}

// This code is contributed by vt_M.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check if water tank
// overflows when n solid balls are
// dipped in the water tank

// function to find if tank
// will overflow or not

function overflow($H, $r, $h,
                      $N, $R)
{
    // cylinder capacity
    $tank_cap = 3.14 * $r *
                  $r * $H;

    // volume of water in tank
    $water_vol = 3.14 * $r *
                   $r * $h;

    // volume of n balls
    $balls_vol = $N * (4/3) *
                  3.14 * $R *
                     $R * $R;

    // total volume of water
    // and n dipped balls
    $vol = $water_vol + $balls_vol;

    // condition to check if tank
    // is in overflow state or not
    if($vol > $tank_cap)
    {
        echo "Overflow", "\n";
    }
    else
    {
        echo "Not in overflow state", "\n";

    }
}

// Driver Code
// giving dimensions
$H = 10; $r = 5; $h = 5;
$N = 2; $R = 2;

// calling function    
overflow ($H, $r, $h, $N, $R);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// JavaScript program for Program to check if
// water tank overflows

    // function to find if tak will
    // overflow or not
    function overflow(H, r, h,
                         N, R)
    {
        // cylinder capacity
        let tank_cap = 3.14 * r * r * H;

        // volume of water in tank
        let water_vol = 3.14 * r * r * h;

        // volume of n balls
        let balls_vol = N * (4 / 3) * 3.14 * R * R * R;

        // total volume of water
        // and n dipped balls
        let vol = water_vol + balls_vol;

        /* condition to check if tank is in
        overflow state or not */
        if (vol > tank_cap) {
            document.write("Overflow");
        }
        else {
            document.write("Not in overflow state");
        }
    } 

// Driver Code

         // giving dimensions
        let H = 10, r = 5, h = 5,
            N = 2, R = 2;

        // calling function
        overflow(H, r, h, N, R);

// This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
Not in overflow state
```