# 确定球面镜焦距的程序

> 原文:[https://www . geesforgeks . org/program-decision-焦距-球面镜/](https://www.geeksforgeeks.org/program-determine-focal-length-spherical-mirror/)

写一个程序来确定球面镜的焦距。
焦距是镜中心到主焦点的距离。为了确定球面镜的焦距，我们应该知道球面镜的曲率半径。从顶点到曲率中心的距离称为曲率半径。
焦距为曲率半径的一半。
**配方:**

```
F =   ( R / 2 )      for concave mirror
F = - ( R / 2 )      for convex mirror
```

示例:

```
For a convex mirror
Input : R = 30 
Output : F = 15

For a convex mirror
Input : R = 25
Output : F = - 12.5
```

## C++

```
// C++ program to determine
// the focal length of a
// of a spherical mirror
#include<iostream>
using namespace std;

// Determines focal length
// of a spherical concave
// mirror
float focal_length_concave(float R)
{
    return R / 2 ;
}

// Determines focal length of a
// spherical convex mirror
float focal_length_convex(float R)
{
    return - ( R / 2 ) ;
}

// Driver function
int main()
{
    float R = 30 ;    
    cout << "Focal length of spherical"
         << "concave mirror is : "
         << focal_length_concave(R)
         << " units\n";
    cout << "Focal length of spherical"
         << "convex mirror is : "
         << focal_length_convex(R)
         << " units";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to determine
// the focal length of a
// of a spherical mirror
import java.util.*;
import java.lang.*;

public class GfG{
    // Determines focal length
    // of a spherical concave
    // mirror
    public static float focal_length_concave(float R)
    {
        return R / 2 ;
    }

    // Determines focal length of a
    // spherical convex mirror
    public static float focal_length_convex(float R)
    {
        return - ( R / 2 ) ;
    }

    // Driver function
    public static void main(String argc[])
    {
        float R = 30 ;

        System.out.print("Focal length of" +
                         "spherical concave"+
                         "mirror is : "+
                         focal_length_concave(R) +
                         " units\n");

        System.out.println("Focal length of"+
                           "spherical convex"+
                           "mirror is : "+
                           focal_length_convex(R) +
                           " units");
    }
}

/* This code is contributed by Sagar Shukla */
```

## 计算机编程语言

```
# Python3 program to determine
# the focal length of a
# of a spherical mirrorr

# Determines focal length of
# a spherical concave mirror
def focal_length_concave(R):
    return R / 2

# Determines focal length of
# a spherical convex mirror
def focal_length_convex(R):
    return - ( R/ 2 )

# Driver function
R = 30 ;
print("Focal length of spherical concave mirror is :",
        focal_length_concave(R)," units")
print("Focal length of spherical convex mirror is : ",
        focal_length_convex(R)," units")
```

## C#

```
// C# program to determine the focal
// length of a of a spherical mirror
using System;

class GfG {

    // Determines focal length of a
    // spherical concave mirror
    public static float focal_length_concave(float R)
    {
        return R / 2 ;
    }

    // Determines focal length of a
    // spherical convex mirror
    public static float focal_length_convex(float R)
    {
        return - ( R / 2 ) ;
    }

    // Driver function
    public static void Main(String[] argc)
    {
        float R = 30 ;
        Console.Write("Focal length of" +
                      "spherical concave" +
                      "mirror is : " +
                      focal_length_concave(R) +
                      " units\n");

        Console.Write("Focal length of" +
                      "spherical convex" +
                      "mirror is : " +
                      focal_length_convex(R) +
                      " units");
    }
}

/* This code is contributed by parashar */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP program to determine
// the focal length of a
// of a spherical mirror

// Determines focal length
// of a spherical concave
// mirror

function focal_length_concave($R)
{
    return $R / 2 ;
}

// Determines focal length of a
// spherical convex mirror
function focal_length_convex($R)
{
    return - ( $R / 2 ) ;
}

// Driver function

    $R = 30 ;    
    echo "Focal length of spherical",
              "concave mirror is : ",
            focal_length_concave($R),
                          " units\n";

    echo "Focal length of spherical",
              " convex mirror is : ",
             focal_length_convex($R),
                            " units";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// javascript program to determine
// the focal length of a
// of a spherical mirror

// Determines focal length
    // of a spherical concave
    // mirror
    function focal_length_concave(R)
    {
        return R / 2 ;
    }

    // Determines focal length of a
    // spherical convex mirror
    function focal_length_convex(R)
    {
        return - ( R / 2 ) ;
    }

// Driver Function

         let R = 30 ;

        document.write("Focal length of" +
                         "spherical concave"+
                         "mirror is : "+
                         focal_length_concave(R) +
                         " units" + "<br/>");

        document.write("Focal length of"+
                           "spherical convex"+
                           "mirror is : "+
                           focal_length_convex(R) +
                           " units");

     // This code is contributed by susmitakundugoaldanga.
</script>
```

输出:

```
Focal length of spherical concave mirror is 15 units
Focal length of spherical convex mirror is -15 units
```