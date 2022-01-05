# 给定点组平行于 X 轴和 Y 轴的直线形成的最大矩形面积

> 原文:[https://www . geeksforgeeks . org/给定点集平行于 x 轴和 y 轴的最大矩形面积/](https://www.geeksforgeeks.org/area-of-the-largest-rectangle-formed-by-lines-parallel-to-x-and-y-axis-from-given-set-of-points/)

给定一个由代表 **N** 点坐标的 **N** 对整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是从给定的一组点中找出由平行于 **X** 和 **Y** 轴的直线形成的最大矩形的面积。

**示例:**

> **输入:** arr[] = {{0，0}，{1，1}}
> **输出:** 1
> **说明:**最大矩形的面积是坐标(0，0)、(0，1)、(1，0)、(1，1)形成的 1。
> 
> **输入:** arr[] = {{-2，0}，{2，0}，{4，0}，{4，2}}
> **输出:** 8
> **解释**:最大可能矩形的面积是 8(长= 4，宽= 2)乘以坐标(-2，0)，(2，0)，(2，2)，(-2，2)。

**方法:**使用[排序技术](https://www.geeksforgeeks.org/sorting-algorithms/)可以解决问题。按照以下步骤解决问题:

1.  将 **X** 和 **Y** 坐标存储在两个不同的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)中，比如说 **x[]** 和 **y[]** 。
2.  [排序](https://www.geeksforgeeks.org/sort-c-stl/)数组 **x[]** 和 **y[]** 。
3.  从两个数组中找出最大相邻差，并存储在变量 **X_Max** 和 **Y_Max 中。**
4.  最大可能矩形面积是 **X_Max** 和 **Y_Max 的乘积。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the area of the largest
// rectangle formed by lines parallel to X
// and Y axis from given set of points
int maxRectangle(vector<vector<int> > sequence,
                 int size)
{
    // Initialize two arrays
    long long int X_Cord[size], Y_Cord[size];

    // Store x and y coordinates
    for (int i = 0; i < size; i++) {
        X_Cord[i] = sequence[i][0];
        Y_Cord[i] = sequence[i][1];
    }

    // Sort arrays
    sort(X_Cord, X_Cord + size);
    sort(Y_Cord, Y_Cord + size);

    // Initialize max differences
    long long int X_Max = 0, Y_Max = 0;

    // Find max adjacent differences
    for (int i = 0; i < size - 1; i++) {
        X_Max = max(X_Max, X_Cord[i + 1]
                               - X_Cord[i]);
        Y_Max = max(Y_Max, Y_Cord[i + 1]
                               - Y_Cord[i]);
    }

    // Return answer
    return X_Max * Y_Max;
}

// Driver Code
int main()
{
    // Given points
    vector<vector<int> > point
        = { { -2, 0 }, { 2, 0 }, { 4, 0 }, { 4, 2 } };

    // Total points
    int n = point.size();

    // Function call
    cout << maxRectangle(point, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to return the area of the largest
// rectangle formed by lines parallel to X
// and Y axis from given set of points
static int maxRectangle(int[][] sequence,
                        int size)
{

    // Initialize two arrays
    int[] X_Cord = new int[size];
    int[] Y_Cord = new int[size];

    // Store x and y coordinates
    for(int i = 0; i < size; i++)
    {
        X_Cord[i] = sequence[i][0];
        Y_Cord[i] = sequence[i][1];
    }

    // Sort arrays
    Arrays.sort(X_Cord);
    Arrays.sort(Y_Cord);

    // Initialize max differences
    int X_Max = 0, Y_Max = 0;

    // Find max adjacent differences
    for(int i = 0; i < size - 1; i++)
    {
        X_Max = Math.max(X_Max, X_Cord[i + 1] -
                                X_Cord[i]);
        Y_Max = Math.max(Y_Max, Y_Cord[i + 1] -
                                Y_Cord[i]);
    }

    // Return answer
    return X_Max * Y_Max;
}

// Driver Code
public static void main(String[] args)
{

    // Given points
    int[][] point = { { -2, 0 }, { 2, 0 },
                      { 4, 0 }, { 4, 2 } };

    // Total points
    int n = point.length;

    // Function call
    System.out.print(maxRectangle(point, n));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to return the
# area of the largest
# rectangle formed by lines
# parallel to X and Y axis
# from given set of points
def maxRectangle(sequence, size):

    # Initialize two arrays
    X_Cord = [0] * size
    Y_Cord = [0] * size

    # Store x and y coordinates
    for i in range(size):
        X_Cord[i] = sequence[i][0]
        Y_Cord[i] = sequence[i][1]

    # Sort arrays
    X_Cord.sort()
    Y_Cord.sort()

    # Initialize max differences
    X_Max = 0
    Y_Max = 0

    # Find max adjacent differences
    for i in range(size - 1):
        X_Max = max(X_Max,
                    X_Cord[i + 1] -
                    X_Cord[i])
        Y_Max = max(Y_Max,
                    Y_Cord[i + 1] -
                    Y_Cord[i])

    # Return answer
    return X_Max * Y_Max

# Driver Code
if __name__ == "__main__":

    # Given points
    point = [[-2, 0], [2, 0],
             [4, 0], [4, 2]]

    # Total points
    n = len(point)

    # Function call
    print(maxRectangle(point, n))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to return the area of the largest
// rectangle formed by lines parallel to X
// and Y axis from given set of points
static int maxRectangle(int[,] sequence,
                        int size)
{

    // Initialize two arrays
    int[] X_Cord = new int[size];
    int[] Y_Cord = new int[size];

    // Store x and y coordinates
    for(int i = 0; i < size; i++)
    {
        X_Cord[i] = sequence[i, 0];
        Y_Cord[i] = sequence[i, 1];
    }

    // Sort arrays
    Array.Sort(X_Cord);
    Array.Sort(Y_Cord);

    // Initialize max differences
    int X_Max = 0, Y_Max = 0;

    // Find max adjacent differences
    for(int i = 0; i < size - 1; i++)
    {
        X_Max = Math.Max(X_Max, X_Cord[i + 1] -
                                X_Cord[i]);
        Y_Max = Math.Max(Y_Max, Y_Cord[i + 1] -
                                Y_Cord[i]);
    }

    // Return answer
    return X_Max * Y_Max;
}

// Driver Code
public static void Main(String[] args)
{

    // Given points
    int[,] point = { { -2, 0 }, { 2, 0 },
                     { 4, 0 }, { 4, 2 } };

    // Total points
    int n = point.GetLength(0);

    // Function call
    Console.Write(maxRectangle(point, n));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to return the area of the largest
// rectangle formed by lines parallel to X
// and Y axis from given set of polets
function maxRectangle(sequence, size)
{

    // Initialize two arrays
    let X_Cord = [];
    let Y_Cord = [];

    // Store x and y coordinates
    for(let i = 0; i < size; i++)
    {
        X_Cord[i] = sequence[i][0];
        Y_Cord[i] = sequence[i][1];
    }

    // Sort arrays
    X_Cord.sort();
    Y_Cord.sort();

    // Initialize max differences
    let X_Max = 0, Y_Max = 0;

    // Find max adjacent differences
    for(let i = 0; i < size - 1; i++)
    {
        X_Max = Math.max(X_Max, X_Cord[i + 1] -
                                X_Cord[i]);
        Y_Max = Math.max(Y_Max, Y_Cord[i + 1] -
                                Y_Cord[i]);
    }

    // Return answer
    return X_Max * Y_Max;
}

// Driver Code

    // Given points
    let point = [[ -2, 0 ], [ 2, 0 ],
                 [ 4, 0 ], [ 4, 2 ]];

    // Total points
    let n = point.length;

    // Function call
    document.write(maxRectangle(point, n));

</script>
```

**Output:** 

```
8
```

***时间复杂度:** O(N*log(N))其中 N 为总点数。*
***辅助空间:** O(N)*