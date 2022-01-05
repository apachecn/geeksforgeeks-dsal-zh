# 将公里/小时转换为英里/小时的程序，反之亦然

> 原文:[https://www . geesforgeks . org/program-convert-kmhr-mileshr-反之亦然/](https://www.geeksforgeeks.org/program-convert-kmhr-mileshr-vice-versa/)

给定以公里/小时为单位的速度，将其转换为米/小时，米/小时转换为公里/小时

示例:

```
Input : 150 (km/hr)
Output : 93.21 

Input : 100 (m/hr)
Output : 160.92693917
```

kph 到 mph 的转换公式为–

```
1 kilo-meter = 0.621371192 miles
```

mph 到 kph 的转换公式是–

```
1 miles = 1.60934 kilo-meter
```

## c++

```
// Cpp program for conversion of
// kmph to mph and vice versa
#include <bits/stdc++.h>
using namespace std;

// Function to convert kmph to mph
double kmphTOmph(double kmph)
{
    return 0.6214 * kmph;
}
// Function to convert mph to kmph
double mphTOkmph(double mph)
{
    return mph * 1.60934;
}

// Driver code to check the above function
int main()
{
    double kmph = 150;
    double mph = 100;
    cout << "the speed in mph is " << kmphTOmph(kmph) << endl;
    cout << "the speed in kmph is " << mphTOkmph(mph);

    return 0;
}
```

## Java

```
// Java program for the conversion
// kmph to mph and vice versa
import java.io.*;
class GFG {

    // Function to convert kmph to mph
    static double kmphTOmph(double kmph)
    {
        return 0.6214 * kmph;
    }

    // Function to convert mph to kmph
    static double mphTOkmph(double mph)
    {
        return mph * 1.60934;
    }
    // Driver code to check the above function
    public static void main(String[] args)
    {
        double kmph = 150;
        double mph = 100;
        System.out.println("speed in miles/hr is " + kmphTOmph(kmph));
        System.out.println("speed in km/hr is " + mphTOkmph(mph));
    }
}
```

## Python

```
# Python program for the conversion
# kmph to mph and vice versa

# Function to convert kmph to mph
def kmphTOmph(kmph):
    mph = 0.6214 * kmph
    return mph

# Function to convert mph to kmph   
def mphTOkmph(mph):
    kmph =(float)(mph * 1.60934)
    return kmph

kmph = 150
mph = 100
print "speed in miles / hr is ", kmphTOmph(kmph)

print "speed in km / hr is ", mphTOkmph(mph)
```

## c#

```
// C# program for the conversion
// kmph to mph and vice versa
using System;

class GFG {

    // Function to convert kmph to mph
    static double kmphTOmph(double kmph)
    {
        return 0.6214 * kmph;
    }

    // Function to convert mph to kmph
    static double mphTOkmph(double mph)
    {
        return mph * 1.60934;
    }

    // Driver code to check the above function
    public static void Main()
    {
        double kmph = 150;
        double mph = 100;
        Console.WriteLine("speed in miles/hr is " + kmphTOmph(kmph));
        Console.WriteLine("speed in km/hr is " + mphTOkmph(mph));
    }
}

// This code is contributed by vt_m
```

## PHP

```
<?php
// PHP program for conversion of
// kmph to mph and vice versa

// Function to convert
// kmph to mph
function kmphTOmph($kmph)
{
    return 0.6214 * $kmph;
}

// Function to convert
// mph to kmph
function mphTOkmph($mph)
{
    return $mph * 1.60934;
}

    // Driver Code
    $kmph = 150;
    $mph = 100;
    echo "speed in mph is " ,
          kmphTOmph($kmph),"\n";
    echo "speed in kmph is " ,
               mphTOkmph($mph);

// This code is contributed by anuj_67.
?>
```

## Javascript

```
<script>

// javascript program for the conversion
// kmph to mph and vice versa

// Function to convert kmph to mph
function kmphTOmph(kmph)
{ 
    return (0.6214 * kmph);
}

// Function to convert mph to kmph
function mphTOkmph(mph)
{
    return (1.60934 * mph) ;
}

// Driver Code
var kmph = 150
var mph = 100
 document.write("speed in miles/hr is " + kmphTOmph(kmph) + "<br>");
 document.write("speed in km/hr is " + mphTOkmph(mph));

  // This code is contributed by bunnyram19.
</script>
```

T31】

**输出:**

```
speed in miles/hr is  93.21
speed in km/hr is  160.934
```