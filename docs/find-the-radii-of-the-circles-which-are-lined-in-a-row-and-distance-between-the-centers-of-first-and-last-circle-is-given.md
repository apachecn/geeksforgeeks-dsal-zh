# 求出排成一行的圆的半径，给出第一个圆和最后一个圆的圆心之间的距离

> 原文:[https://www . geeksforgeeks . org/find-给定第一个和最后一个圆的圆心的半径和距离/](https://www.geeksforgeeks.org/find-the-radii-of-the-circles-which-are-lined-in-a-row-and-distance-between-the-centers-of-first-and-last-circle-is-given/)

这里给出的是外部互相接触的 **n** 个圆，排成一排。给出了第一个圆和最后一个圆的圆心之间的距离。这些圆的半径相等。任务是找到每个圆的半径。
**例:**

```
Input: d = 42, n = 4
Output: The radius of each circle is 7

Input: d = 64, n = 5
Output: The radius of each circle is 8
```

![](img/1f7ae23838a8d2cade09147871966a63.png)

**接近** :
假设有 **n** 个圆，每个圆的长度半径为 **r** 。
让，第一个和最后一个圆之间的距离= **d**
从图中可以明显看出，
**r+r+(n-2)* 2r = d**
**2r+2nr–4r = d**
**2nr–2r = d**
所以，**r = d/(2n-2)**
![The radius of each circle = distance between the first and last circles/(2*no.of circles -2)   ](img/1c3a99572c0ccdf56664342905458b63.png "Rendered by QuickLaTeX.com")

## C++

```
// C++ program to find radii of the circles
// which are lined in a row
// and distance between the
// centers of first and last circle is given

#include <bits/stdc++.h>
using namespace std;

void radius(int n, int d)
{
    cout << "The radius of each circle is "
         << d / (2 * n - 2) << endl;
}

// Driver code
int main()
{
    int d = 42, n = 4;
    radius(n, d);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find radii of the circles
// which are lined in a row
// and distance between the
// centers of first and last circle is given
import java.io.*;

class GFG
{

static void radius(int n, int d)
{
    System.out.print( "The radius of each circle is "
        +d / (2 * n - 2));
}

// Driver code
static public void main (String []args)
{
    int d = 42, n = 4;
    radius(n, d);
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python program to find radii of the circles
# which are lined in a row
# and distance between the
# centers of first and last circle is given

def radius(n, d):
    print("The radius of each circle is ",
        d / (2 * n - 2));

d = 42; n = 4;
radius(n, d);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to find radii of the circles
// which are lined in a row
// and distance between the
// centers of first and last circle is given
using System;

class GFG
{

static void radius(int n, int d)
{
    Console.Write( "The radius of each circle is "
        +d / (2 * n - 2));
}

// Driver code
static public void Main ()
{
    int d = 42, n = 4;
    radius(n, d);
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
// javascript program to find radii of the circles
// which are lined in a row
// and distance between the
// centers of first and last circle is given
function radius(n , d)
{
    document.write( "The radius of each circle is "
        +d / (2 * n - 2));
}

// Driver code
var d = 42, n = 4;
radius(n, d);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
The radius of each circle is 7
```