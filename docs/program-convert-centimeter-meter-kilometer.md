# 将厘米转换为米和公里的程序

> 原文:[https://www . geesforgeks . org/program-convert-厘米-米-公里/](https://www.geeksforgeeks.org/program-convert-centimeter-meter-kilometer/)

给定厘米长度，任务是将其转换为米和公里。

**示例:**

> 输入:厘米长度= 1000
> 输出:
> 米长度= 10 米
> 公里长度= 0.01 公里
> 
> 输入:厘米长度=6540
> 输出:
> 米长度= 65.4 米
> 公里长度= 0.0654 公里

要使用的公式:

```
1m = 100cm
1km = 100000cm
```

## C++

```
// C++ program to convert centimeter
// into meter and kilometer
#include <bits/stdc++.h>
using namespace std;
int main()
{
    float cm, meter, kilometer;
    cm = 1000;

    // Converting centimeter into meter
    // and kilometer
    meter = cm / 100.0;
    kilometer = cm / 100000.0;

    cout << "Length in meter = " << meter << "m"
         << "\n";

    cout << "Length in Kilometer = " << kilometer << "km"
         << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to convert
// centimeter into meter
// and kilometer
import java.io.*;

class GFG
{
    public static void main (String[] args)
    {
        double cm, meter, kilometer;
        cm = 1000;

        // Converting centimeter
        // into meter and kilometer
        meter = cm / 100.0;
        kilometer = cm / 100000.0;

        System.out.println("Length in meter = " +
                                    meter + "m");

        System.out.println("Length in Kilometer = " +
                                   kilometer + "km");
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to convert
# centimeter into meter
# and kilometer
cm = 1000;

# Converting centimeter
# into meter and kilometer
meter = cm / 100.0;
kilometer = cm / 100000.0;

# Driver Code
print("Length in meter = " ,
               meter , "m");
print("Length in Kilometer = ",
             kilometer , "km");

# This code is contributed
# by mits
```

## C#

```
// C# program to convert
// centimeter into meter
// and kilometer
using System;

class GFG
{

// Driver Code
static public void Main ()
{
    double cm, meter, kilometer;
    cm = 1000;

    // Converting centimeter
    // into meter and kilometer
    meter = cm / 100.0;
    kilometer = cm / 100000.0;

    Console.WriteLine("Length in " +
                        "meter = " +
                       meter + "m");

    Console.WriteLine("Length in " +
                    "Kilometer = " +
                  kilometer + "km");
}
}

// This code is contributed
// by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to convert
// centimeter into meter
// and kilometer

$cm; $meter; $kilometer;
$cm = 1000;

// Converting centimeter into
// meter and kilometer
$meter = $cm / 100.0;
$kilometer = $cm / 100000.0;

echo "Length in meter = " ,
        $meter ,"m" , "\n";

echo "Length in Kilometer = " ,
       $kilometer , "km" ,"\n";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to convert centimeter
// into meter and kilometer
let cm, meter, kilometer;
cm = 1000;

// Converting centimeter into meter
// and kilometer
meter = cm / 100.0;
kilometer = cm / 100000.0;

document.write("Length in meter = " +
               meter + "m" + "</br>");

document.write("Length in Kilometer = " +
               kilometer + "km" + "</br>");

// This code is contributed by jana_sayantan

</script>
```

**输出:**

```
 Length in meter = 10 m
 Length in kilometer = 0.01 km
```