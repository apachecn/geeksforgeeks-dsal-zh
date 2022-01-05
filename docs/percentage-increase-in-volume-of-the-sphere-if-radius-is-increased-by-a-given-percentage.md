# 如果半径增加给定的百分比

，球体体积增加的百分比

> 原文:[https://www . geesforgeks . org/如果半径增加给定的百分比，球体体积增加的百分比/](https://www.geeksforgeeks.org/percentage-increase-in-volume-of-the-sphere-if-radius-is-increased-by-a-given-percentage/)

这里给定的是一个球体，它的半径增加了给定的百分比。任务是找出球体体积增加的百分比。
**例:**

```
Input: x = 10
Output: 33.1%

Input: x = 50
Output: 237.5%
```

**接近** :

*   让，球体的半径= **a**
*   给定百分比增加= **x%**
*   增加前的体积= **4/3*πa^3**
*   增加后的新半径= **a + ax/100**
*   所以，**新卷= 4/3*π(a^3+(ax/100)^3+3a^3x/100+3a^3x^2/10000)**
*   成交量变化=**4/3*π((ax/100)^3+3a^3x/100+3a^3x^2/10000)**
*   成交量增长百分比=**(4/3*π*((ax/100)^3+3a^3x/100+3a^3x^2/10000)/4/3*π*a^3)* 100 = x^3/10000+3x+3x^2/100**

![   ](img/20c0826ae6e1a1a19e29a5a2ab0b2f84.png "Rendered by QuickLaTeX.com")

## C++

```
// C++ program to find percentage increase
// in the volume of the sphere
// if radius is increased by a given percentage

#include <bits/stdc++.h>
using namespace std;

void newvol(double x)
{
    cout << "percentage increase in the"
         << " volume of the sphere is "
         << pow(x, 3) / 10000 + 3 * x
                + (3 * pow(x, 2)) / 100
         << "%" << endl;
}

// Driver code
int main()
{
    double x = 10;
    newvol(x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find percentage increase
// in the volume of the sphere
// if radius is increased by a given percentage
import java.io.*;

class GFG
{

static void newvol(double x)
{
    System.out.print( "percentage increase in the"
        + " volume of the sphere is "
        +( Math.pow(x, 3) / 10000 + 3 * x
                + (3 * Math.pow(x, 2)) / 100)
        + "%");
}

// Driver code
public static void main (String[] args)
{
        double x = 10;
    newvol(x);
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to find percentage increase
# in the volume of the sphere
# if radius is increased by a given percentage

def newvol(x):

    print("percentage increase in the"
        " volume of the sphere is "
        ,pow(x, 3) / 10000 + 3 * x
                + (3 * pow(x, 2)) / 100
            ,"%")

# Driver code
x = 10.0
newvol(x)

# This code is contributed mohit kumar 29
```

## C#

```
// C# program to find percentage increase
// in the volume of the sphere
// if radius is increased by a given percentage
using System;

class GFG
{

static void newvol(double x)
{
    Console.WriteLine( "percentage increase in the"
        + " volume of the sphere is "
        +( Math.Pow(x, 3) / 10000 + 3 * x
                + (3 * Math.Pow(x, 2)) / 100)
        + "%");
}

// Driver code
public static void Main ()
{
    double x = 10;
    newvol(x);
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
// javascript program to find percentage increase
// in the volume of the sphere
// if radius is increased by a given percentage
function newvol(x)
{
    document.write( "percentage increase in the"
        + " volume of the sphere is "
        +( Math.pow(x, 3) / 10000 + 3 * x
                + (3 * Math.pow(x, 2)) / 100)
        + "%");
}

// Driver code
var x = 10;
newvol(x);

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
percentage increase in the volume of the sphere is 33.1%
```