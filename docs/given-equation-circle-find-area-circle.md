# 给定一个圆作为弦的方程，求面积

> 原文:[https://www . geesforgeks . org/给定-方程-圆-查找-面积-圆/](https://www.geeksforgeeks.org/given-equation-circle-find-area-circle/)

给出圆心在原点(0，0)且半径为 R 的圆**X<sup>2</sup>+Y<sup>2</sup>= R<sup>2</sup>T7】的方程，任务是求圆的面积。
**举例:**** 

```
Input : 
X*X + Y*Y = 25
Output :
The area of circle centered at origin  is : 78.55

Input : 
X*X + Y*Y = 64
Output :
The area of circle centered at origin  is : 201.088
```

## 方法

*   给定一个方程 X<sup>2</sup>+Y<sup>2</sup>= R<sup>2</sup>，并将其存储为字符串“str”。
*   计算字符串的长度并将其存储到“len”中。
*   从 0 到 len-1 开始循环，并检查字符串[I]= = = ' = '。
*   将“=”后的字符存储到字符串变量 st 中。
*   将字符串“st”转换为数字并存储到“radius_square”中。
*   用公式**π* R<sup>2</sup>**求圆的面积(乘以π)。

## C++

```
// C++ program to find area of circle
// when equation of circle give.

#include <bits/stdc++.h>
#define PI 3.142
using namespace std;

// Function to find the area
double findArea(double radius)
{
    return PI * pow(radius, 2);
}

// Function to return the value of radius
static double findradius(string str)
{

    // Initialization
    double radius = 0;

    // For storing the value of R*R
    string st = "";

    // For counting the number of
    // spaces in the string
    int c = 0;

    // calculate the length of the
    int len = str.length();

    // getting the value of R*R
    // After = sign
    for (int i = 0; i < len; i++) {
        if (str[i] == '=') {
            c = 1;
        }
        else if (c == 1 && str[i] != ' ') {
            st = st + str[i];
        }
    }

    // Converting the digits into integer
    // Taking square root of that number
    radius = (double)sqrt(stoi(st));
    return radius;
}

int main()
{

    // Static input for equation
    // of circle
    string str = "X*X + Y*Y = 100";

    // calling the Function
    double radius = findradius(str);

    // Display the result
    cout << "The area of circle " <<
       "centered at origin is : " <<
           findArea(radius) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find area of circle
// when equation of circle give.
import java.io.*;

public class GFG {

    static double PI = 3.142;

    // Function to find the area
    static double findArea(double radius)
    {
        return PI * Math.pow(radius, 2);
    }

    // Function to return the value of radius
    static double findradius(String str)
    {
        double radius = 0;

        // For storing the value of radius * radius
        String st = "";

        // For counting the number of spaces
        // in the string
        int c = 0;

        // calculate the length of the
        int len = str.length();

        // getting the value of radius * radius
        // After = sign
        for (int i = 0; i < len; i++) {
            if (str.charAt(i) == '=') {
                c = 1;
            }
            else if (c == 1 && str.charAt(i) != ' ')
            {
                st = st + str.charAt(i);
            }
        }

        // Converting the digits into integer
        // Taking square root of that number
        if (c == 1)
            radius = (double)Math.sqrt(
                            Integer.parseInt(st));
        return radius;
    }

    public static void main(String[] args)
    {

        // Static input for equation of circle
        String str = "X*X + Y*Y = 100";

        // calling the Function
        double radius = findradius(str);

        // Display the result
        System.out.println("The area of circle"
                  + " centered at origin is : "
                              + findArea(radius));
    }
}
```

## 蟒蛇 3

```
# python program to find area of circle
# when equation of circle give.

import math

# Function to find the area
def findArea(radius):

    return math.pi * pow(radius, 2)

# Function to return the value of radius
def findradius(str):

    #Initialization
    radius = 0

    # For storing the value of R*R
    st = ""

    # For counting the number of
    # spaces in the string
    c = 0

    # calculate the length of the
    Len = len(str)

    # getting the value of R*R
    # After = sign
    for i in range(0, Len):
        if (str[i] == '='):
            c = 1
        elif (c == 1 and str[i] != ' '):
            st = st + str[i]

    # Converting the digits into integer
    # Taking square root of that number
    radius = float(math.sqrt(float(st)))
    return radius

# Static input for equation
# of circle
str = "X*X + Y*Y = 100"

# calling the Function
radius = findradius(str)

# Display the result
print( "The area of circle " ,
"centered at origin is : " ,
    (findArea(radius)))

# This code is contributed by Sam007.
```

## C#

```
// C# program to find area of circle
// when equation of circle give.
using System;

class GFG
{
    // Function to find the area
    static double findArea(double radius)
    {
        return Math.PI * Math.Pow(radius, 2);
    }

    // Function to return the value of radius
    static double findradius(string str)
    {
        double radius = 0;

        // For storing the value
        // of radius * radius
        String st = "";

        // For counting the number
        // of spaces in the string
        int c = 0;

        // calculate the length of the
        int len = str.Length;

        // getting the value of radius * radius
        // After = sign
        for (int i = 0; i < len; i++)
        {
            if (str[i] == '=')
            {
                c = 1;
            }
            else if (c == 1 && str[i] != ' ')
            {
                st = st + str[i];
            }
        }

        // Converting the digits into integer
        // Taking square root of that number
        if (c == 1)
            radius = (double)Math.Sqrt(
                        int.Parse(st));
        return radius;
    }

    // Driver code
    public static void Main()
    {
        // Static input for equation of circle
        string str = "X*X + Y*Y = 100";

        // calling the Function
        double radius = findradius(str);

        // Display the result
        Console.WriteLine("The area of circle" +
                          " centered at origin is : " +
                          System.Math.Round(findArea(radius),1));
    }
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>

// JavaScript program to find area of circle
// when equation of circle give.

    let PI = 3.142;

    // Function to find the area
    function findArea(radius)
    {
        return PI * Math.pow(radius, 2);
    }

    // Function to return the value of radius
    function findradius(str)
    {
        let radius = 0;

        // For storing the value of radius * radius
        let st = "";

        // For counting the number of spaces
        // in the string
        let c = 0;

        // calculate the length of the
        let len = str.length;

        // getting the value of radius * radius
        // After = sign
        for (let i = 0; i < len; i++) {
            if (str[i] == '=') {
                c = 1;
            }
            else if (c == 1 && str[i] != ' ')
            {
                st = st + str[i];
            }
        }

        // Converting the digits into integer
        // Taking square root of that number
        if (c == 1)
            radius = Math.sqrt(
                            parseInt(st));
        return radius;
    }

// Driver program

        // Static input for equation of circle
        let str = "X*X + Y*Y = 100";

        // calling the Function
        let radius = findradius(str);

        // Display the result
        document.write("The area of circle"
                  + " centered at origin is : "
                              + findArea(radius));

        // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
The area of circle centered at origin is : 314.2
```