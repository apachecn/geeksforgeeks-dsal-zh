# 求直线通过给定点的方程

> 原文:[https://www . geesforgeks . org/find-直线方程-通过给定点/](https://www.geeksforgeeks.org/find-the-equation-of-the-straight-line-passing-through-the-given-points/)

给定一个包含平面内 N 个坐标点的数组 **arr** ，任务是检查坐标点是否位于一条直线上。如果它们位于一条直线上，则打印**是**以及该直线的方程，否则打印**否**。

**示例:**

> **输入:** arr[] = {{1，1}、{2，2}、{3，3}}
> **输出:**
> 是
> 1x- 1y=0
> 
> **输入:** arr[] = {{0，1}，{2，0}}
> **输出:**
> 是
> 2y+x-2 = 0
> 
> **输入:** arr[] = {{1，5}，{2，2}，{4，6}，{3，5}}
> **输出:**否

**方法:**想法是找到可以使用数组中给定的任意一对点形成的直线的方程，如果所有其他点都满足使用这对点形成的直线的方程，那么所有这些点一起形成一条直线。所以，如果所有的点都满足直线方程，那么打印**是**后跟直线方程，否则打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if a straight line
// can be formed using N points
void isStraightLinePossibleEq(
    vector<pair<int, int> > arr,
    int n)
{
    // First pair of point (x0, y0)
    int x0 = arr[0].first;
    int y0 = arr[0].second;

    // Second pair of point (x1, y1)
    int x1 = arr[1].first;
    int y1 = arr[1].second;

    int dx = x1 - x0,
        dy = y1 - y0,
        c = dy * x0 - dx * y0;

    // Loop to iterate over the points
    // and check whether they satisfy
    // the equation or not.
    for (int i = 2; i < n; i++) {
        int x = arr[i].first, y = arr[i].second;
        if ((dx * y) - (dy * x) != c) {
            cout << "No";
            return;
        }
    }
    cout << "Yes" << endl;
    cout << dy << "x-" << dx
         << "y=" << c << "\n";
}

// Driver Code
int main()
{
    // Array of points
    vector<pair<int, int> > arr
        = { { 0, 0 }, { 1, 1 }, { 3, 3 }, { 2, 2 } };
    int N = 2;

    // Function Call
    isStraightLinePossibleEq(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG
{

// Function to check if a straight line
// can be formed using N points
static void isStraightLinePossibleEq(int arr[][], int n)
{
    // First pair of point (x0, y0)
    int x0 = arr[0][0];
    int y0 = arr[0][1];

    // Second pair of point (x1, y1)
    int x1 = arr[1][0];
    int y1 = arr[1][1];

    int dx = x1 - x0,
        dy = y1 - y0,
        c = dy * x0 - dx * y0;

    // Loop to iterate over the points
    // and check whether they satisfy
    // the equation or not.
    for (int i = 2; i < n; i++) {
        int x = arr[i][0], y = arr[i][1];
        if ((dx * y) - (dy * x) != c) {
            System.out.print("No");
            return;
        }
    }
    System.out.print("Yes" + "\n");
    System.out.print(dy + "x-" + dx
         + "y=" + c + "\n");
}

// Driver Code
public static void main(String args[])
{

    // Array of points
    int arr[][] = {{ 0, 0 }, { 1, 1 }, { 3, 3 }, { 2, 2 }};
    int N = 2;

    // Function Call
    isStraightLinePossibleEq(arr, N);

}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to check if a straight line
# can be formed using N points
def isStraightLinePossibleEq(arr, n):

    # First pair of point (x0, y0)
    x0 = arr[0][0]
    y0 = arr[0][1]

    # Second pair of point (x1, y1)
    x1 = arr[1][0]
    y1 = arr[1][1]

    dx = x1 - x0
    dy = y1 - y0
    c = dy * x0 - dx * y0

       # Loop to iterate over the points
       # and check whether they satisfy
       # the equation or not.
    for i in range(2, n):
        x = arr[i][0], y = arr[i][1]
        if (dx * y) - (dy * x) != c:
            print("No")
            return

    print("Yes")
    print(str(dy)+ "x" +"-" + str(dx)+ "y"+ "="+ str(c))

    # Driver Code

    # Array of points
arr = [[0, 0], [1, 1], [3, 3], [2, 2]]
N = 2

# Function Call
isStraightLinePossibleEq(arr, N)

# This code is contributed by Potta Lokesh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Function to check if a straight line
// can be formed using N points
static void isStraightLinePossibleEq(int [,]arr, int n)
{
    // First pair of point (x0, y0)
    int x0 = arr[0, 0];
    int y0 = arr[0, 1];

    // Second pair of point (x1, y1)
    int x1 = arr[1, 0];
    int y1 = arr[1, 1];

    int dx = x1 - x0,
        dy = y1 - y0,
        c = dy * x0 - dx * y0;

    // Loop to iterate over the points
    // and check whether they satisfy
    // the equation or not.
    for (int i = 2; i < n; i++) {
        int x = arr[i, 0], y = arr[i, 1];
        if ((dx * y) - (dy * x) != c) {
            Console.Write("No");
            return;
        }
    }
    Console.Write("Yes" + "\n");
    Console.Write(dy + "x-" + dx
         + "y=" + c + "\n");
}

// Driver Code
public static void Main()
{

    // Array of points
    int[,] arr = new int[4, 2] {{ 0, 0 }, { 1, 1 }, { 3, 3 }, { 2, 2 }};
    int N = 2;

    // Function Call
    isStraightLinePossibleEq(arr, N);

}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to check if a straight line
    // can be formed using N points
    const isStraightLinePossibleEq = (arr, n) => {

        // First pair of point (x0, y0)
        let x0 = arr[0][0];
        let y0 = arr[0][1];

        // Second pair of point (x1, y1)
        let x1 = arr[1][0];
        let y1 = arr[1][1];

        let dx = x1 - x0,
            dy = y1 - y0,
            c = dy * x0 - dx * y0;

        // Loop to iterate over the points
        // and check whether they satisfy
        // the equation or not.
        for (let i = 2; i < n; i++) {
            let x = arr[i][0], y = arr[i][1];
            if ((dx * y) - (dy * x) != c) {
                cout << "No";
                return;
            }
        }
        document.write("Yes<br/>");
        document.write(`${dy}x-${dx}y=${c}<br/>`);
    }

    // Driver Code

    // Array of points
    let arr = [[0, 0], [1, 1], [3, 3], [2, 2]];
    let N = 2;

    // Function Call
    isStraightLinePossibleEq(arr, N);

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
Yes
1x-1y=0
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)