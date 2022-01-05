# 计算速度、距离和时间

> 原文:[https://www . geesforgeks . org/compute-speed-distance-time/](https://www.geeksforgeeks.org/calculate-speed-distance-time/)

当一个物体以稳定的速度直线运动时，如果我们知道它能走多远，需要多长时间，我们就可以计算出它的速度。这个等式显示了速度、行驶距离和所用时间之间的关系:
速度是距离除以所用时间。
例如，一辆汽车在 2 小时内行驶 30 公里。
速度 30÷2 = 15 公里/小时
使用公式:

```
Distance  = Speed * Time
Time = Distance / Speed
Speed = Distance / Time
```

**例:**

```
Input : distance(km) : 48.5  time(hr) : 2.6
Output : Speed(km / hr) : 18.653846153

Input : speed(km / hr) : 46.0  time(hr) : 3.2
Output : Distance(km) : 147.2

Input : distance(km) : 48.5  speed(km / hr) : 46.0
Output : Time(hr) : 1.0543
```

## C++

```
// C++ Program to calculate speed
// distance and time
#include<iostream>
using namespace std;

// Function to calculate speed
double cal_speed(double dist, double time)
{
   cout << "\n Distance(km) : " << dist ;
   cout << "\n Time(hr) : " << time ;

   return dist / time;
}

// Function to calculate distance traveled
double cal_dis(double speed, double time)
{
   cout << "\n Time(hr) : " << time ;
   cout << "\n Speed(km / hr) : " << speed ;

   return speed * time;
}

// Function to calculate time taken
double cal_time(double dist, double speed)
{
   cout << "\n Distance(km) : "<< dist ;
   cout << "\n Speed(km / hr) : " << speed ;

   return speed * dist ;
}

// Driver function
int main()
{
   // Calling function cal_speed()
   cout << "\n The calculated Speed(km / hr) is : "
               << cal_speed(45.9, 2.0 ) << endl ;

   // Calling function cal_dis()
   cout << "\n The calculated Distance(km) : "
               << cal_dis(62.9, 2.5) << endl ;

   // Calling function cal_time()
   cout << "\n The calculated Time(hr) : "
        << cal_time(48.0, 4.5) << endl ;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to calculate speed
// distance and time

class GFG
{
    // Function to calculate speed
    static double cal_speed(double dist, double time)
    {
        System.out.print("\n Distance(km) : " + dist) ;
        System.out.print("\n Time(hr) : " + time) ;

        return dist / time;
    }

    // Function to calculate distance traveled
    static double cal_dis(double speed, double time)
    {
        System.out.print("\n Time(hr) : " + time) ;
        System.out.print("\n Speed(km / hr) : " + speed) ;

        return speed * time;
    }

    // Function to calculate time taken
    static double cal_time(double dist, double speed)
    {
        System.out.print("\n Distance(km) : "+ dist) ;
        System.out.print("\n Speed(km / hr) : " + speed) ;

        return speed * dist ;
    }

    // Driver code
    public static void main (String[] args)
    {
        // Calling function cal_speed()
        System.out.println("\n The calculated Speed(km / hr) is : "+
                    cal_speed(45.9, 2.0 ));

        // Calling function cal_dis()
        System.out.println("\n The calculated Distance(km) : "+
                    cal_dis(62.9, 2.5));

        // Calling function cal_time()
        System.out.println("\n The calculated Time(hr) : "+
                cal_time(48.0, 4.5));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 Program to calculate speed,
# distance and time

# Function to calculate speed
def cal_speed(dist, time):
    print(" Distance(km) :", dist);
    print(" Time(hr) :", time);
    return dist / time;

# Function to calculate distance traveled
def cal_dis(speed, time):
    print(" Time(hr) :", time) ;
    print(" Speed(km / hr) :", speed);
    return speed * time;

# Function to calculate time taken
def cal_time(dist, speed):
    print(" Distance(km) :", dist);
    print(" Speed(km / hr) :", speed);
    return speed * dist;

# Driver Code

# Calling function cal_speed()
print(" The calculated Speed(km / hr) is :",
                     cal_speed(45.9, 2.0 ));
print("");

# Calling function cal_dis()
print(" The calculated Distance(km) :",
                   cal_dis(62.9, 2.5));
print("");

# Calling function cal_time()
print(" The calculated Time(hr) :",
              cal_time(48.0, 4.5));

# This code is contributed
# by mits
```

## C#

```
// C# Program to calculate speed
// distance and time
using System;

class GFG
{
    // Function to calculate speed
    static double cal_speed(double dist, double time)
    {
        Console.WriteLine(" Distance(km) : " + dist) ;
        Console.WriteLine(" Time(hr) : " + time) ;

        return dist / time;
    }

    // Function to calculate distance traveled
    static double cal_dis(double speed, double time)
    {
        Console.WriteLine(" Time(hr) : " + time) ;
        Console.WriteLine(" Speed(km / hr) : " + speed) ;

        return speed * time;
    }

    // Function to calculate time taken
    static double cal_time(double dist, double speed)
    {
        Console.WriteLine(" Distance(km) : "+ dist) ;
        Console.WriteLine(" Speed(km / hr) : " + speed) ;

        return speed * dist ;
    }

    // Driver code
    public static void Main ()
    {
        // Calling function cal_speed()
    Console.WriteLine(" The calculated Speed(km / hr) is : "+
                    cal_speed(45.9, 2.0 ));

        // Calling function cal_dis()
        Console.WriteLine(" The calculated Distance(km) : "+
                    cal_dis(62.9, 2.5));

        // Calling function cal_time()
        Console.WriteLine(" The calculated Time(hr) : "+
                cal_time(48.0, 4.5));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to calculate
// speed distance and time

// Function to calculate speed
function cal_speed($dist, $time)
{
echo "\n Distance(km) : " . $dist ;
echo "\n Time(hr) : " . $time ;

return $dist / $time;
}

// Function to calculate
// distance traveled
function cal_dis($speed, $time)
{
echo "\n Time(hr) : " . $time ;
echo "\n Speed(km / hr) : " . $speed ;

return $speed * $time;
}

// Function to calculate
// time taken
function cal_time($dist, $speed)
{
echo "\n Distance(km) : " . $dist ;
echo "\n Speed(km / hr) : " . $speed ;

return $speed * $dist ;
}

// Driver Code

// Calling function cal_speed()
echo " The calculated Speed(km / hr) is : ".
                 cal_speed(45.9, 2.0 )."\n";

// Calling function cal_dis()
echo "\n The calculated Distance(km) : ".
                 cal_dis(62.9, 2.5)."\n";

// Calling function cal_time()
echo "\n The calculated Time(hr) : ".
            cal_time(48.0, 4.5)."\n";

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// Javascript Program to calculate speed
// distance and time

    // Function to calculate speed
    function  cal_speed( dist,  time)
    {
        document.write(" Distance(km) : " + dist + "<br>" ) ;
        document.write(" Time(hr) : " + time + "<br>") ;

        return dist / time;
    }

    // Function to calculate distance traveled
    function  cal_dis( speed,  time)
    {
        document.write(" Time(hr) : " + time + "<br>" ) ;
        document.write(" Speed(km / hr) : " + speed + "<br>") ;

        return speed * time;
    }

    // Function to calculate time taken
    function  cal_time( dist,  speed)
    {
        document.write(" Distance(km) : " + dist + "<br>") ;
        document.write(" Speed(km / hr) : " + speed + "<br>" ) ;

        return speed * dist ;
    }

    // Driver code

        // Calling function cal_speed()
    document.write(" The calculated Speed(km / hr) is : "+
                    cal_speed(45.9, 2.0 ) + "<br>");
    document.write("<br>");

        // Calling function cal_dis()
        document.write(" The calculated Distance(km) : "+
                    cal_dis(62.9, 2.5) + "<br>");
        document.write("<br>");    

        // Calling function cal_time()
        document.write(" The calculated Time(hr) : "+
                cal_time(48.0, 4.5) + "<br>");

</script>

```

**输出:**

```
 Distance(km) : 45.9
 Time(hr) : 2
 The calculated Speed(km / hr) is : 22.95

 Time(hr) : 2.5
 Speed(km / hr) : 62.9
 The calculated Distance(km) : 157.25

 Distance(km) : 48
 Speed(km / hr) : 4.5
 The calculated Time(hr) : 216
```