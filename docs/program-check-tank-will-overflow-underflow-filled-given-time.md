# 检查给定时间内储罐是否会溢出、下溢或充满的程序

> 原文:[https://www . geesforgeks . org/program-check-tank-will-overflow-under-filled-给定时间/](https://www.geeksforgeeks.org/program-check-tank-will-overflow-underflow-filled-given-time/)

给定一个具有一定高度和半径的水箱，以及可用于填充水箱的水流量。确定给定时间内油箱是否会溢出。
**注:**每分钟的水量。
示例:

```
       --r=5--
   ----------   ^
   |         |  |
   |         |  |
   |         |  h = 10
   |         |  |
   ----------   ^

   rate_of_flow = 10

Input : given_time = 10.0
Output : Underflow

Input : given_time = 100.0
Output : Overflow
```

**进场:**
圆柱形油箱的容积为(22/7) *半径*半径*高度。首先，找出完全充满油箱所需的时间，然后将其与给定的时间进行比较。如果给定时间大于所需时间，将导致溢出情况。如果给定的时间少于所需的时间，那么它将导致底流状态，否则罐被填满。
以下是上述办法的实施:

## C++

```
// C++ program to check if Tank will
// overflow or not in given time
#include <bits/stdc++.h>
using namespace std;

// function to calculate the volume of tank
float volume(int radius, int height)
{
    return ((22 / 7) * radius * radius * height);
}

// function to print overflow / filled /
// underflow accordingly
void check_and_print(float required_time,
                       float given_time)
{
    if (required_time < given_time)
        cout << "Overflow";
    else if (required_time > given_time)
        cout << "Underflow";
    else
        cout << "Filled";
}

// driver function
int main()
{
    int radius = 5, // radius of the tank
        height = 10, // height of the tank
        rate_of_flow = 10; // rate of flow of water

    float given_time = 70.0; // time given

    // calculate the required time
    float required_time = volume(radius, height) /
                                    rate_of_flow;

    // printing the result
    check_and_print(required_time, given_time);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if Tank will
// overflow or not in given time

class Number
{
    // function to calculate the volume of tank
    public static float volume(int radius, int height)
    {
        return ((22 / 7) * radius * radius * height);
    }

    // function to print overflow / filled /
    // underflow accordingly
    public static void check_and_print(double required_time,
                                       double given_time)
    {
        if (required_time < given_time)
            System.out.print( "Overflow" );
        else if (required_time > given_time)
            System.out.print( "Underflow" );
        else
            System.out.print( "Filled" );
    }

    // driver code
    public static void main(String[] args)
    {
        int radius = 5, // radius of the tank
        height = 10, // height of the tank
        rate_of_flow = 10; // rate of flow of water

        double given_time = 70.0; // time given

        // calculate the required time
        double required_time = volume(radius, height) /
                                    rate_of_flow;

        // printing the result
        check_and_print(required_time, given_time);
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 code to check if Tank will
# overflow or not in given time

# function to calculate the volume of tank
def volume(radius, height):
    return ((22 / 7) * radius * radius * height)

# function to print overflow / filled /
# underflow accordingly
def check_and_print( required_time, given_time):

    if required_time < given_time:
        print( "Overflow")
    elif required_time > given_time:
        print("Underflow")
    else:
        print("Filled")

# driver code
radius = 5 # radius of the tank
height = 10 # height of the tank
rate_of_flow = 10 # rate of flow of water

given_time = 70.0 # time given

# calculate the required time
required_time = volume(radius, height) /rate_of_flow

# printing the result
check_and_print(required_time, given_time)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to check if Tank will
// overflow or not in given time
using System;

class Number {

    // function to calculate the volume of tank
    public static float volume(int radius, int height)
    {
        return ((22 / 7) * radius * radius * height);
    }

    // function to print overflow / filled /
    // underflow accordingly
    public static void check_and_print(double required_time,
                                          double given_time)
    {
        if (required_time < given_time)
            Console.WriteLine("Overflow");
        else if (required_time > given_time)
            Console.WriteLine("Underflow");
        else
            Console.WriteLine("Filled");
    }

    // driver code
    public static void Main()
    {
        int radius = 5, // radius of the tank
            height = 10, // height of the tank
            rate_of_flow = 10; // rate of flow of water

        double given_time = 70.0; // time given

        // calculate the required time
        double required_time = volume(radius, height) / rate_of_flow;

        // printing the result
        check_and_print(required_time, given_time);
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if Tank will
// overflow or not in given time

// function to calculate
// the volume of tank
function volume($radius, $height)
{
    return ((22 / 7) * $radius *
              $radius * $height);
}

// function to print overflow
// / filled / underflow accordingly
function check_and_print($required_time,
                         $given_time)
{
    if ($required_time < $given_time)
        echo("Overflow");
    else if ($required_time > $given_time)
        echo("Underflow");
    else
        echo("Filled");
}

// Driver code

// radius of the tank
$radius = 5;

// height of the tank
$height = 10;

// rate of flow of water
$rate_of_flow = 10;

// time given       
$given_time = 70.0;

// calculate the required time
$required_time = volume($radius, $height) /
                            $rate_of_flow;

// printing the result
check_and_print($required_time, $given_time);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// JavaScript program to check if Tank will
// overflow or not in given time

    // function to calculate the volume of tank
    function volume(radius, height)
    {
        return ((22 / 7) * radius * radius * height);
    }

    // function to print overflow / filled /
    // underflow accordingly
    function check_and_print(required_time,
                                       given_time)
    {
        if (required_time < given_time)
            document.write( "Overflow" );
        else if (required_time > given_time)
            document.write( "Underflow" );
        else
            document.write( "Filled" );
    }

// Driver code

        let radius = 5, // radius of the tank
        height = 10, // height of the tank
        rate_of_flow = 10; // rate of flow of water

        let given_time = 70.0; // time given

        // calculate the required time
        let required_time = volume(radius, height) /
                                    rate_of_flow;

        // printing the result
        check_and_print(required_time, given_time);

</script>
```

**输出:**

```
Underflow
```