# 在平面图中求区域数的程序

> 原文:[https://www . geesforgeks . org/program-to-find-in-region-in-plane-graph/](https://www.geeksforgeeks.org/program-to-find-the-number-of-region-in-planar-graph/)

给定两个整数 **V** 和 **E** ，它们表示一个[平面图](https://www.geeksforgeeks.org/mathematics-planar-graphs-graph-coloring/)的顶点和边的数量。任务是找出平面图的区域数。

**平面图:**平面图是指没有边互相交叉的图，或者可以画在没有边交叉的平面上的图称为平面图。

**区域:**当绘制一个没有边交叉的平面图时，图的边和顶点将平面划分为区域。

**示例:**

> **输入:** V = 4，E = 5
> T3】输出: R = 3
> 
> ![](img/f83d2c1f52a4d645a1bd393d999282e4.png)
> 
> **输入:** V = 3，E = 3
> T3】输出: R = 2

**方法:**欧拉求出平面图中区域的数量与图中顶点数和边数的函数关系，即

![](img/16d5b272db2b40dafd4adf77d2a3c036.png)

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number
// of regions in a Planar Graph
int Regions(int Vertices, int Edges)
{
    int R = Edges + 2 - Vertices;

    return R;
}

// Driver code
int main()
{
    int V = 5, E = 7;

    cout << Regions(V, E);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG {

    // Function to return the number
    // of regions in a Planar Graph
    static int Regions(int Vertices, int Edges)
    {
        int R = Edges + 2 - Vertices;

        return R;
    }

    // Driver code
    public static void main(String[] args)
    {

        int V = 5, E = 7;
        System.out.println(Regions(V, E));
    }
}

// This code is contributed by akt_mit
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number
# of regions in a Planar Graph
def Regions(Vertices, Edges) :

    R = Edges + 2 - Vertices;

    return R;

# Driver code
if __name__ == "__main__" :

    V = 5; E = 7;

    print(Regions(V, E));

# This code is contributed
# by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the number
    // of regions in a Planar Graph
    static int Regions(int Vertices, int Edges)
    {
        int R = Edges + 2 - Vertices;

        return R;
    }

    // Driver code
    static public void Main()
    {

        int V = 5, E = 7;
        Console.WriteLine(Regions(V, E));
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number
// of regions in a Planar Graph
function Regions($Vertices, $Edges)
{
    $R = $Edges + 2 - $Vertices;

    return $R;
}

// Driver code
$V = 5; $E = 7;
echo(Regions($V, $E));

// This code is contributed
// by Code_Mech
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the number
// of regions in a Planar Graph
function Regions(Vertices, Edges)
{
    var R = Edges + 2 - Vertices;

    return R;
}

// Driver code
var V = 5, E = 7;

document.write( Regions(V, E));

// This code is contributed by itsok

</script>
```

**Output:** 

```
4
```