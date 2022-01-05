# 用 N 个坐标点检查是否能形成一条直线

> 原文:[https://www . geeksforgeeks . org/check-a-直线是否可以使用-n-坐标点形成/](https://www.geeksforgeeks.org/check-whether-a-straight-line-can-be-formed-using-n-co-ordinate-points/)

给定一个由 **N** 坐标点组成的数组 **arr[]** ，任务是检查是否可以使用这些坐标点形成一条直线。

> **输入:** arr[] = {{0，0}、{1，1}、{2，2}}
> **输出:**是
> **说明:**
> 每两点斜率相同。那就是 1。
> 因此，可以利用这些点形成直线。
> 
> **输入:** arr[] = {{0，1}，{2，0}}
> **输出:**是
> **说明:**
> 坐标系中的两点总是形成一条直线。

**逼近:**思路是求数组中每一对点之间的直线的[斜率，如果每一对点的斜率相同，那么这几个点就连成一条直线。](https://www.geeksforgeeks.org/program-find-slope-line/)

```
// Slope of line formed by 
// two points (y2, y1), (x2, x1)

Slope of Line = y2 - y1
               ---------
                x2 - x1
```

下面是上述方法的实现:

## C++

```
// C++ implementation to check
// if a straight line
// can be formed using N points

#include <bits/stdc++.h>

using namespace std;

// Function to check if a straight line
// can be formed using N points
bool isStraightLinePossible(
    vector<pair<int, int> > arr, int n)
{
    // First pair of point (x0, y0)
    int x0 = arr[0].first;
    int y0 = arr[0].second;

    // Second pair of point (x1, y1)
    int x1 = arr[1].first;
    int y1 = arr[1].second;

    int dx = x1 - x0, dy = y1 - y0;

    // Loop to iterate over the points
    for (int i = 0; i < n; i++) {
        int x = arr[i].first, y = arr[i].second;
        if (dx * (y - y1) != dy * (x - x1)){
            cout << "NO";
            return false;
        }
    }
    cout << "YES";
    return true;
}

// Driver Code
int main()
{
    // Array of points
    vector<pair<int, int> > arr =
    { { 0, 0 }, { 1, 1 }, { 3, 3 }, { 2, 2 } };
    int n = 4;

    // Function Call
    isStraightLinePossible(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// if a straight line can be
// formed using N points
import java.util.*;

class GFG{

static class pair
{
    int first, second;
    pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to check if a straight line
// can be formed using N points
static void isStraightLinePossible(
       ArrayList<pair> arr, int n)
{

    // First pair of point (x0, y0)
    int x0 = arr.get(0).first;
    int y0 = arr.get(0).second;

    // Second pair of point (x1, y1)
    int x1 = arr.get(1).first;
    int y1 = arr.get(1).second;

    int dx = x1 - x0, dy = y1 - y0;

    // Loop to iterate over the points
    for(int i = 0; i < n; i++)
    {
        int x = arr.get(i).first;
        int y = arr.get(i).second;
        if (dx * (y - y1) != dy * (x - x1))
        {
            System.out.println("NO");
        }
    }
    System.out.println("YES");
}

// Driver code
public static void main(String[] args)
{

    // Array of points
    ArrayList<pair> arr = new ArrayList<>();
    arr.add(new pair(0, 0));
    arr.add(new pair(1, 1));
    arr.add(new pair(3, 3));
    arr.add(new pair(2, 2));

    int n = 4;

    // Function Call
    isStraightLinePossible(arr, n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to check
# if a straight line can be formed
# using N points

# Function to check if a straight line
# can be formed using N points
def isStraightLinePossible(arr, n):

    # First pair of point (x0, y0)
    x0 = arr[0][0]
    y0 = arr[0][1]

    # Second pair of point (x1, y1)
    x1 = arr[1][0]
    y1 = arr[1][1]

    dx = x1 - x0
    dy = y1 - y0

    # Loop to iterate over the points
    for i in range(n):
        x = arr[i][0]
        y = arr[i][1]

        if (dx * (y - y1) != dy * (x - x1)):
            print("NO", end = "")
            return False

    print("YES", end = "")
    return True

# Driver code

# Array of points
arr = [ [ 0, 0 ], [ 1, 1 ],
        [ 3, 3 ], [ 2, 2 ] ]
n = 4

# Function Call
isStraightLinePossible(arr, n)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation to check
// if a straight line can be
// formed using N points
using System;
using System.Collections.Generic;

class GFG{

public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to check if a straight line
// can be formed using N points
static void isStraightLinePossible(
    List<pair> arr, int n)
{

    // First pair of point (x0, y0)
    int x0 = arr[0].first;
    int y0 = arr[0].second;

    // Second pair of point (x1, y1)
    int x1 = arr[1].first;
    int y1 = arr[1].second;

    int dx = x1 - x0, dy = y1 - y0;

    // Loop to iterate over the points
    for(int i = 0; i < n; i++)
    {
        int x = arr[i].first;
        int y = arr[i].second;

        if (dx * (y - y1) != dy * (x - x1))
        {
            Console.WriteLine("NO");
        }
    }
    Console.WriteLine("YES");
}

// Driver code
public static void Main(String[] args)
{

    // Array of points
    List<pair> arr = new List<pair>();

    arr.Add(new pair(0, 0));
    arr.Add(new pair(1, 1));
    arr.Add(new pair(3, 3));
    arr.Add(new pair(2, 2));

    int n = 4;

    // Function call
    isStraightLinePossible(arr, n);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach
// Function to check if a straight line
// can be formed using N points
function isStraightLinePossible( arr, n)
{
    // First pair of point (x0, y0)
    var x0 = arr[0][0];
    var y0 = arr[0][1];

    // Second pair of point (x1, y1)
    var x1 = arr[1][0];
    var y1 = arr[1][1];

    var dx = x1 - x0;
    var dy = y1 - y0;

    // Loop to iterate over the points
    for (var i = 0; i < n; i++) {
        var x = arr[i][0], y = arr[i][1];
        if (dx * (y - y1) != dy * (x - x1)){
            document.write("NO");
            return false;
        }
    }
    document.write("YES");
    return true;
}

// Driver Code
// Array of points
var arr = [[ 0, 0 ], [ 1, 1 ], [ 3, 3 ], [ 2, 2 ]];
var n = 4;

// Function Call
isStraightLinePossible(arr, n);
</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(N)

**辅助空间:** O(1)