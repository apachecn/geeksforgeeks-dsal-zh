# 检查是否可以创建给定角度的多边形

> 原文:[https://www . geeksforgeeks . org/check-如果有可能创建一个给定角度的多边形/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-create-a-polygon-with-a-given-angle/)

给定一个角度![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")，其中，![1\le a< 180  ](img/0b15f31cc6ca781aa2d1ee5d20177a06.png "Rendered by QuickLaTeX.com")。任务是检查是否有可能做出一个所有内角都等于![a  ](img/c30e654d88f33e45c5463a428b007bce.png "Rendered by QuickLaTeX.com")的正多边形。如果可能，则打印“是”，否则打印“否”(不带引号)。
**示例:**

```
Input: angle = 90
Output: YES
Polygons with sides 4 is
possible with angle 90 degrees.

Input: angle = 30
Output: NO
```

**逼近:**内角定义为正多边形任意两条相邻边之间的夹角。
由![\;Interior\;angle = \frac{180 \times (n-2)}{n}\;  ](img/98193279bdc52d5a79c1e1f06c324b01.png "Rendered by QuickLaTeX.com")给出，其中， **n** 为多边形的边数。
这个可以写成![\;a = \frac{180 \times (n-2)}{n}\;  ](img/29d3974bef5a068407f03ec42f13a635.png "Rendered by QuickLaTeX.com")。
关于重新排列我们得到的术语，![\;n = \frac{360}{180 - a}\;  ](img/c35b4a41cce9316e8d67a13f2a8ace75.png "Rendered by QuickLaTeX.com")。
因此，如果 **n** 是**整数**，则答案为“是”，否则，答案为“否”。
以下是上述方法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether it is possible
// to make a regular polygon with a given angle.
void makePolygon(float a)
{
    // N denotes the number of sides
    // of polygons possible
    float n = 360 / (180 - a);
    if (n == (int)n)
        cout << "YES";
    else
        cout << "NO";
}

// Driver code
int main()
{
    float a = 90;

    // function to print the required answer
    makePolygon(a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{
// Function to check whether
// it is possible to make a
// regular polygon with a given angle.
static void makePolygon(double a)
{
    // N denotes the number of
    // sides of polygons possible
    double n = 360 / (180 - a);
    if (n == (int)n)
        System.out.println("YES");
    else
        System.out.println("NO");
}

// Driver code
public static void main (String[] args)
{
    double a = 90;

    // function to print
    // the required answer
    makePolygon(a);
}
}

// This code is contributed by Bilal
```

## 蟒蛇 3

```
# Python 3 implementation
# of above approach

# Function to check whether
# it is possible to make a
# regular polygon with a
# given angle.
def makePolygon(a) :

    # N denotes the number of sides
    # of polygons possible
    n = 360 / (180 - a)

    if n == int(n) :
        print("YES")

    else :
        print("NO")

# Driver Code
if __name__ == "__main__" :
    a = 90

    # function calling
    makePolygon(a)

# This code is contributed
# by ANKITRAI1
```

## C#

```
// C# implementation of
// above approach
using System;

class GFG
{
// Function to check whether
// it is possible to make a
// regular polygon with a
// given angle.
static void makePolygon(double a)
{
    // N denotes the number of
    // sides of polygons possible
    double n = 360 / (180 - a);
    if (n == (int)n)
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}

// Driver code
static void Main()
{
    double a = 90;

    // function to print
    // the required answer
    makePolygon(a);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to check whether it
// is possible to make a regular
// polygon with a given angle.
function makePolygon($a)
{
    // N denotes the number of
    // sides of polygons possible
    $n = 360 / (180 - $a);
    if ($n == (int)$n)
        echo "YES";
    else
        echo "NO";
}

// Driver code
$a = 90;

// function to print the
// required answer
makePolygon($a);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

      // JavaScript implementation of above approach
      // Function to check whether it is possible
      // to make a regular polygon with a given angle.

      function makePolygon(a)
      {
        // N denotes the number of sides
        // of polygons possible
        var n = parseFloat(360 / (180 - a));
        if (n === parseInt(n))
        document.write("YES");
        else
        document.write("NO");
      }

      // Driver code
      var a = 90;

      // function to print the required answer
      makePolygon(a);

</script>
```

**Output:** 

```
YES
```