# 给定点矩形的坐标位于

内

> 原文:[https://www . geesforgeks . org/坐标-矩形-给定点-位于-内部/](https://www.geeksforgeeks.org/coordinates-rectangle-given-points-lie-inside/)

给定两个具有 n 个元素的数组 X[]和 Y[]，其中(Xi，易)表示坐标系上的一个点，找到最小的矩形，使得来自给定输入的所有点都位于该矩形内，并且矩形的边必须平行于坐标轴。打印获得的矩形的所有四个坐标。
**注:** n > = 4(我们至少有 4 个点作为输入)。
示例:

```
Input : X[] = {1, 3, 0, 4},  y[] = {2, 1, 0, 2}
Output : {0, 0}, {0, 2}, {4, 2}, {4, 0}

Input : X[] = {3, 6, 1, 9, 13, 0, 4}, Y[] = {4, 2, 6, 5, 2, 3, 1}
Output : {0, 1}, {0, 6}, {13, 6}, {13, 1} 
```

要找到最小的矩形，可以采用两种基本方法:

1.  将坐标平面的原点视为最小的矩形，如果点不在当前矩形内，则根据点的坐标值逐步扩展它。这个概念需要一点复杂的逻辑来找到精确的最小矩形。
2.  这背后的一个非常简单有效的逻辑是在所有给定点中找到最小的以及最大的 x & y 坐标，然后这些值的所有可能的四种组合，得到所需矩形的四个点，分别为{Xmin，Ymin}、{Xmin，Ymax}、{Xmax，Ymax}、{Xmax，Ymin}。

## C++

```
// Program to find smallest rectangle
// to conquer all points
#include <bits/stdc++.h>
using namespace std;

// function to print coordinate of smallest rectangle
void printRect(int X[], int Y[], int n)
{
    // find Xmax and Xmin
    int Xmax = *max_element(X, X + n);
    int Xmin = *min_element(X, X + n);

    // find Ymax and Ymin
    int Ymax = *max_element(Y, Y + n);
    int Ymin = *min_element(Y, Y + n);

    // print all four coordinates
    cout << "{" << Xmin << ", " << Ymin << "}" << endl;
    cout << "{" << Xmin << ", " << Ymax << "}" << endl;
    cout << "{" << Xmax << ", " << Ymax << "}" << endl;
    cout << "{" << Xmax << ", " << Ymin << "}" << endl;
}

// driver program
int main()
{
    int X[] = { 4, 3, 6, 1, -1, 12 };
    int Y[] = { 4, 1, 10, 3, 7, -1 };
    int n = sizeof(X) / sizeof(X[0]);

    printRect(X, Y, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find smallest rectangle
// to conquer all points
import java.util.Arrays;
import java.util.Collections;

class GFG {

    // function to print coordinate of smallest rectangle
    static void printRect(Integer X[], Integer Y[], int n)
    {

        // find Xmax and Xmin
        int Xmax = Collections.max(Arrays.asList(X));
        int Xmin = Collections.min(Arrays.asList(X));

        // find Ymax and Ymin
        int Ymax = Collections.max(Arrays.asList(Y));
        int Ymin = Collections.min(Arrays.asList(Y));

        // print all four coordinates
        System.out.println("{" + Xmin + ", " + Ymin + "}");
        System.out.println("{" + Xmin + ", " + Ymax + "}");
        System.out.println("{" + Xmax + ", " + Ymax + "}");
        System.out.println("{" + Xmax + ", " + Ymin + "}");
    }

    //Driver code
    public static void main (String[] args)
    {

        Integer X[] = { 4, 3, 6, 1, -1, 12 };
        Integer Y[] = { 4, 1, 10, 3, 7, -1 };
        int n = X.length;

        printRect(X, Y, n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Program to find smallest rectangle
# to conquer all points

# function to print coordinate of smallest rectangle
def printRect(X, Y, n):

    # find Xmax and Xmin
    Xmax = max(X)
    Xmin = min(X)

    # find Ymax and Ymin
    Ymax = max(Y)
    Ymin = min(Y)

    # print all four coordinates
    print("{",Xmin,", ",Ymin,"}",sep="" )
    print("{",Xmin,", ",Ymax,"}",sep="" )
    print("{",Xmax,", ",Ymax,"}",sep="" )
    print("{",Xmax,", ",Ymin,"}",sep="" )

# driver program
X = [4, 3, 6, 1, -1, 12]
Y =  [4, 1, 10, 3, 7, -1]
n = len(X)
printRect(X, Y, n)
# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// Program to find smallest rectangle
// to conquer all points
using System.Linq;
using System;

public class GFG{

    // function to print coordinate
    // of smallest rectangle
    static void printRect(int[] X,
                        int[] Y, int n)
    {

        // find Xmax and Xmin
        int Xmax = X.Max();
        int Xmin = X.Min();

        // find Ymax and Ymin
        int Ymax = Y.Max();
        int Ymin = Y.Min();

        // print all four coordinates
        Console.WriteLine("{" + Xmin + ", "
                             + Ymin + "}");

        Console.WriteLine("{" + Xmin + ", "
                             + Ymax + "}");

        Console.WriteLine("{" + Xmax + ", "
                             + Ymax + "}");

        Console.WriteLine("{" + Xmax + ", "
                             + Ymin + "}");
    }

    // Driver code
    static public void Main ()
    {
        int[] X = { 4, 3, 6, 1, -1, 12 };
        int[] Y = { 4, 1, 10, 3, 7, -1 };
        int n = X.Length;

        printRect(X, Y, n);
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find smallest
// rectangle to conquer all points

// function to print coordinate
// of smallest rectangle
function printRect($X, $Y, $n)
{

    // find Xmax and Xmin
    $Xmax = max($X);
    $Xmin = min($X);

    // find Ymax and Ymin
    $Ymax = max($Y);
    $Ymin = min($Y);

    // print all four coordinates
    echo "{" , $Xmin , ", " , $Ymin , "}","\n";
    echo "{" , $Xmin , ", " , $Ymax , "}" ,"\n";
    echo "{" , $Xmax , ", " , $Ymax , "}","\n";
    echo "{" , $Xmax , ", " , $Ymin , "}" ;
}

    // Driver Code
    $X = array(4, 3, 6, 1, -1, 12);
    $Y = array(4, 1, 10, 3, 7, -1);
    $n =count($X);
    printRect($X, $Y, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Program to find smallest rectangle
// to conquer all points

// function to print coordinate of smallest rectangle
function printRect(X, Y, n)
{
    // find Xmax and Xmin
    var Xmax = X.reduce((a,b) => Math.max(a,b));
    var Xmin = X.reduce((a,b) => Math.min(a,b));

    // find Ymax and Ymin
    var Ymax =  Y.reduce((a,b) => Math.max(a,b));
    var Ymin = Y.reduce((a,b) => Math.min(a,b));

    // print all four coordinates
    document.write( "{" + Xmin + ", " + Ymin + "}" + "<br>");
    document.write( "{" + Xmin + ", " + Ymax + "}" + "<br>");
    document.write( "{" + Xmax + ", " + Ymax + "}" + "<br>");
    document.write( "{" + Xmax + ", " + Ymin + "}" + "<br>");
}

// driver program
var X = [ 4, 3, 6, 1, -1, 12 ];
var Y = [ 4, 1, 10, 3, 7, -1 ];
var n = X.length;

printRect(X, Y, n);

</script>
```

**Output:** 

```
{-1, -1}
{-1, 10}
{12, 10}
{12, -1}
```