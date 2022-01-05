# 如果高度增加给定的百分比，但半径保持不变，则气缸中的百分比增加

> 原文:[https://www . geeksforgeeks . org/如果高度按给定的百分比增加，但半径保持不变/](https://www.geeksforgeeks.org/percentage-increase-in-the-cylinder-if-the-height-is-increased-by-given-percentage-but-radius-remains-constant/)

这里给定的是一个右圆柱体，它的高度增加了给定的百分比，但半径保持不变。任务是找出气缸容积增加的百分比。
**例:**

```
Input: x = 10
Output: 10%

Input: x = 18.5
Output: 18.5%
```

**接近** :

*   让，圆柱体的半径= **r**
*   气缸高度= **h**
*   给定百分比增加= **x%**
*   所以，旧卷= **π*r^2*h**
*   新高度= **h + hx/100**
*   新卷= **π*r^2*(h + hx/100)**
*   所以，体积增加= **πr^2*(hx/100)**
*   所以体积增加百分比=**(πr^2*(hx/100))/(πr^2*(hx/100))*100**=**x**

![   ](img/20c0826ae6e1a1a19e29a5a2ab0b2f84.png "Rendered by QuickLaTeX.com")

## C++

```
// C++ program to find percentage increase
// in the cylinder if the height
// is increased by given percentage
// but radius remains constant

#include <bits/stdc++.h>
using namespace std;

void newvol(double x)
{
    cout << "percentage increase "
         << "in the volume of the cylinder is "
         << x << "%" << endl;
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
// in the cylinder if the height
// is increased by given percentage
// but radius remains constant
import java.io.*;

class GFG
{

static void newvol(double x)
{
    System.out.print( "percentage increase "
        + "in the volume of the cylinder is "
        + x + "%" );
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
# in the cylinder if the height
# is increased by given percentage
# but radius remains constant

def newvol(x):
    print("percentage increase in the volume of the cylinder is ",x,"%")

# Driver code
x = 10.0
newvol(x)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find percentage increase
// in the cylinder if the height
// is increased by given percentage
// but radius remains constant
using System;

class GFG
{

static void newvol(double x)
{
    Console.WriteLine( "percentage increase "
        + "in the volume of the cylinder is "
        + x + "%" );
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
// in the cylinder if the height
// is increased by given percentage
// but radius remains constant
function newvol(x)
{
    document.write( "percentage increase "
        + "in the volume of the cylinder is "
        + x + "%" );
}

// Driver code
var x = 10;
newvol(x);

// This code is contributed by 29AjayKumar
</script>
```

**输出:**

```
percentage increase in the volume of the cylinder is 10.0%
```