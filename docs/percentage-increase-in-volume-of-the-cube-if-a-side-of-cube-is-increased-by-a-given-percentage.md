# 如果立方体的一边增加给定的百分比，立方体体积增加的百分比

> 原文:[https://www . geeksforgeeks . org/如果立方体的一面按给定的百分比增加，则立方体的体积增加百分比/](https://www.geeksforgeeks.org/percentage-increase-in-volume-of-the-cube-if-a-side-of-cube-is-increased-by-a-given-percentage/)

这里给定的是一个立方体，它的一边增加了一个给定的百分比。任务是找出立方体体积的增加百分比。
**例:**

```
Input: x = 10
Output: 33.1%

Input: x = 50
Output: 237.5%
```

**接近**T2】

*   在立方体中，所有的边都是相等的，所以，
    **长度=宽度=高度**
*   让立方体的一边= **a**
*   给定百分比增加= **x%**
*   所以，成交量前增= **a^3**
*   增加后，新边= **a + ax/100**
*   所以，新卷=**(a+ax/100)^3**=**a^3+(ax/100)^3+3a^3x/100+3a^3x^2/10000**
*   成交量增加=新量–旧量=**(a^3+(ax/100)^3+3a^3x/100+3a^3x^2/10000)–a^3**=**(ax/100)^3+3a^3x/100+3a^3x^2/10000**
*   所以，成交量增加百分比=**((ax/100)^3+3a^3x/100+3a^3x^2/10000)/a^3)* 100**=**((x/100)^3+3x/100+3x^2/10000)* 100 = x^3/10000+3x+3x^2/100**

![   ](img/20c0826ae6e1a1a19e29a5a2ab0b2f84.png "Rendered by QuickLaTeX.com")
以下是上述方法的实施:

## C++

```
// C++ program to find percentage increase
// in the volume of the cube
// if a side of cube is increased
// by a given percentage

#include <bits/stdc++.h>
using namespace std;

void newvol(double x)
{
    cout << "percentage increase "
         << "in the volume of the cube is "
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
// in the volume of the cube
// if a side of cube is increased
// by a given percentage
import java.io.*;

class GFG
{

static void newvol(double x)
{
    System.out.print( "percentage increase "
    +"in the volume of the cube is "
        + (Math.pow(x, 3) / 10000 + 3 * x
                + (3 * Math.pow(x, 2)) / 100) );
                System.out.print("%");
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
# Python program to find percentage increase
# in the volume of the cube
# if a side of cube is increased
# by a given percentage

def newvol(x):

    print("percentage increase"
            "in the volume of the cube is ",
            ((x**(3)) / 10000 + 3 * x
                + (3 * (x**(2))) / 100),"%");

x = 10;
newvol(x);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to find percentage increase
// in the volume of the cube
// if a side of cube is increased
// by a given percentage
using System;

class GFG
{

static void newvol(double x)
{
    Console.Write( "percentage increase "
    +"in the volume of the cube is "
        + (Math.Pow(x, 3) / 10000 + 3 * x
                + (3 * Math.Pow(x, 2)) / 100) );
                Console.Write("%");
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
// in the volume of the cube
// if a side of cube is increased
// by a given percentage
function newvol( x)
{
    document.write("percentage increase "
         + "in the volume of the cube is "
         + (Math.pow(x, 3) / 10000 + 3 * x
                + (3 * Math.pow(x, 2)) / 100)
         + "%" );
}

// Driver code
    let x = 10;
    newvol(x);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
percentage increase in the volume of the cube is 33.1%
```