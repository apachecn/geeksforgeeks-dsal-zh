# 给定 N 个不平行于 X 轴或 Y 轴的点的行数

> 原文:[https://www . geesforgeks . org/给定 n 点不平行于 x 轴或 y 轴的行数/](https://www.geeksforgeeks.org/number-of-lines-from-given-n-points-not-parallel-to-x-or-y-axis/)

给定 **2D** 平面上的 N 个不同整数点。任务是统计由给定的 **N** 点形成的不平行于 **X** 或 **Y** 轴的线的数量。

**示例:**

> **输入:**点数[][] = {{1，2}，{1，5}，{1，15}，{2，10}}
> **输出:** 3
> 选择的配对为{(1，2)，(2，10)}，{(1，5)，(2，10)}，{(1，15)，(2，10)}。
> 
> **输入:**点[][] = {{1，2}，{2，5}，{3，15}}
> **输出:** 3
> 选择任意一对点。

**进场:**

1.  我们知道
    *   任意两点连接而成的直线，如果有相同的 **Y** 坐标，将平行于 **X 轴**
    *   如果它们有相同的 **X** 坐标，它将平行于 **Y 轴**。
2.  可由 N 个点形成的线段总数= ![\binom{N}{2}= \frac{N*(N-1)}{2}      ](img/b5012176d3fcb3c7b3a90523c874cbe8.png "Rendered by QuickLaTeX.com")

3.  现在我们将排除那些平行于 **X 轴**或 **Y 轴**的线段。
4.  对于每个 **X** 坐标和 **Y** 坐标，计算点数并排除末端的那些线段。

下面是上述方法的实现:

## C++

```
// C++ program to find the number
// of lines which are formed from
// given N points and not parallel
// to X or Y axis

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of lines
// which are formed from given N points
// and not parallel to X or Y axis
int NotParallel(int p[][2], int n)
{
    // This will store the number of points has
    // same x or y coordinates using the map as
    // the value of coordinate can be very large
    map<int, int> x_axis, y_axis;

    for (int i = 0; i < n; i++) {

        // Counting frequency of each x and y
        // coordinates
        x_axis[p[i][0]]++;
        y_axis[p[i][1]]++;
    }

    // Total number of pairs can be formed
    int total = (n * (n - 1)) / 2;

    for (auto i : x_axis) {
        int c = i.second;

        // We can not choose pairs from these as
        // they have same x coordinatethus they
        // will result line segment
        // parallel to y axis
        total -= (c * (c - 1)) / 2;
    }

    for (auto i : y_axis) {
        int c = i.second;

        // we can not choose pairs from these as
        // they have same y coordinate thus they
        // will result line segment
        // parallel to x-axis
        total -= (c * (c - 1)) / 2;
    }

    // Return the required answer
    return total;
}

// Driver Code
int main()
{

    int p[][2] = { { 1, 2 },
                   { 1, 5 },
                   { 1, 15 },
                   { 2, 10 } };

    int n = sizeof(p) / sizeof(p[0]);

    // Function call
    cout << NotParallel(p, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// of lines which are formed from
// given N points and not parallel
// to X or Y axis
import java.util.*;

class GFG{

// Function to find the number of lines
// which are formed from given N points
// and not parallel to X or Y axis
static int NotParallel(int p[][], int n)
{
    // This will store the number of points has
    // same x or y coordinates using the map as
    // the value of coordinate can be very large
    HashMap<Integer,Integer> x_axis = new HashMap<Integer,Integer>();
    HashMap<Integer,Integer> y_axis = new HashMap<Integer,Integer>();

    for (int i = 0; i < n; i++) {

        // Counting frequency of each x and y
        // coordinates
        if(x_axis.containsKey(p[i][0]))
            x_axis.put(p[i][0], x_axis.get(p[i][0])+1);
        else
            x_axis.put(p[i][0], 1);
        if(y_axis.containsKey(p[i][1]))
            y_axis.put(p[i][1], y_axis.get(p[i][1])+1);
        else
            y_axis.put(p[i][1], 1);
    }

    // Total number of pairs can be formed
    int total = (n * (n - 1)) / 2;

    for (Map.Entry<Integer,Integer> i : x_axis.entrySet()) {
        int c = i.getValue();

        // We can not choose pairs from these as
        // they have same x coordinatethus they
        // will result line segment
        // parallel to y axis
        total -= (c * (c - 1)) / 2;
    }

    for (Map.Entry<Integer,Integer> i : y_axis.entrySet()) {
        int c = i.getValue();

        // we can not choose pairs from these as
        // they have same y coordinate thus they
        // will result line segment
        // parallel to x-axis
        total -= (c * (c - 1)) / 2;
    }

    // Return the required answer
    return total;
}

// Driver Code
public static void main(String[] args)
{

    int p[][] = { { 1, 2 },
                   { 1, 5 },
                   { 1, 15 },
                   { 2, 10 } };

    int n = p.length;

    // Function call
    System.out.print(NotParallel(p, n));

}
}

// This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to find the number
// of lines which are formed from
// given N points and not parallel
// to X or Y axis
using System;
using System.Collections.Generic;

class GFG{

// Function to find the number of lines
// which are formed from given N points
// and not parallel to X or Y axis
static int NotParallel(int [,]p, int n)
{
    // This will store the number of points has
    // same x or y coordinates using the map as
    // the value of coordinate can be very large
    Dictionary<int,int> x_axis = new Dictionary<int,int>();
    Dictionary<int,int> y_axis = new Dictionary<int,int>();

    for (int i = 0; i < n; i++) {

        // Counting frequency of each x and y
        // coordinates
        if(x_axis.ContainsKey(p[i, 0]))
            x_axis[p[i, 0]] = x_axis[p[i, 0]] + 1;
        else
            x_axis.Add(p[i, 0], 1);
        if(y_axis.ContainsKey(p[i, 1]))
            y_axis[p[i, 1]] = y_axis[p[i, 1]] + 1;
        else
            y_axis.Add(p[i, 1], 1);
    }

    // Total number of pairs can be formed
    int total = (n * (n - 1)) / 2;

    foreach (KeyValuePair<int,int> i in x_axis) {
        int c = i.Value;

        // We can not choose pairs from these as
        // they have same x coordinatethus they
        // will result line segment
        // parallel to y axis
        total -= (c * (c - 1)) / 2;
    }

    foreach (KeyValuePair<int,int> i in y_axis) {
        int c = i.Value;

        // we can not choose pairs from these as
        // they have same y coordinate thus they
        // will result line segment
        // parallel to x-axis
        total -= (c * (c - 1)) / 2;
    }

    // Return the required answer
    return total;
}

// Driver Code
public static void Main(String[] args)
{

    int [,]p = { { 1, 2 },
                   { 1, 5 },
                   { 1, 15 },
                   { 2, 10 } };

    int n = p.GetLength(0);

    // Function call
    Console.Write(NotParallel(p, n)); 
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the number
# of lines which are formed from
# given N points and not parallel
# to X or Y axis

# Function to find the number of lines
# which are formed from given N points
# and not parallel to X or Y axis
def NotParallel(p, n) :

    # This will store the number of points has
    # same x or y coordinates using the map as
    # the value of coordinate can be very large
    x_axis  = {}; y_axis = {};

    for i in range(n) :

        # Counting frequency of each x and y
        # coordinates
        if p[i][0] not in x_axis :
            x_axis[p[i][0]] = 0;

        x_axis[p[i][0]] += 1;

        if p[i][1] not in y_axis :
            y_axis[p[i][1]] = 0;

        y_axis[p[i][1]] += 1;

    # Total number of pairs can be formed
    total = (n * (n - 1)) // 2;

    for i in x_axis :
        c =  x_axis[i];

        # We can not choose pairs from these as
        # they have same x coordinatethus they
        # will result line segment
        # parallel to y axis
        total -= (c * (c - 1)) // 2;

    for i in y_axis :
        c = y_axis[i];

        # we can not choose pairs from these as
        # they have same y coordinate thus they
        # will result line segment
        # parallel to x-axis
        total -= (c * (c - 1)) // 2;

    # Return the required answer
    return total;

# Driver Code
if __name__ == "__main__" :

    p = [ [ 1, 2 ],
            [1, 5 ],
            [1, 15 ],
            [ 2, 10 ] ];

    n = len(p);

    # Function call
    print(NotParallel(p, n));

    # This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program to find the number
// of lines which are formed from
// given N points and not parallel
// to X or Y axis

// Function to find the number of lines
// which are formed from given N points
// and not parallel to X or Y axis
function NotParallel(p, n)
{
    // This will store the number of points has
    // same x or y coordinates using the map as
    // the value of coordinate can be very large
    var x_axis = new Map(), y_axis = new Map();

    for (var i = 0; i < n; i++) {

        // Counting frequency of each x and y
        // coordinates
        if(x_axis.has(p[i][0]))
            x_axis.set(p[i][0], x_axis.get(p[i][0])+1)
        else
            x_axis.set(p[i][0], 1)

        if(y_axis.has(p[i][1]))
            y_axis.set(p[i][1], y_axis.get(p[i][1])+1)
        else
            y_axis.set(p[i][1], 1)
    }

    // Total number of pairs can be formed
    var total = (n * (n - 1)) / 2;

    x_axis.forEach((value, key) => {

        var c = value;

        // We can not choose pairs from these as
        // they have same x coordinatethus they
        // will result line segment
        // parallel to y axis
        total -= (c * (c - 1)) / 2;
    });

    y_axis.forEach((value, key) => {

        var c = value;

        // we can not choose pairs from these as
        // they have same y coordinate thus they
        // will result line segment
        // parallel to x-axis
        total -= (c * (c - 1)) / 2;
    });

    // Return the required answer
    return total;
}

// Driver Code
var p = [ [ 1, 2 ],
               [ 1, 5 ],
               [ 1, 15 ],
               [ 2, 10 ] ];
var n = p.length;

// Function call
document.write( NotParallel(p, n));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)*

***辅助空间:**O(N)*T4】