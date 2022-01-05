# 无塔网格中最大的区域

> 原文:[https://www . geeksforgeeks . org/最大网格面积-无边界塔/](https://www.geeksforgeeks.org/largest-area-in-a-grid-unbounded-by-towers/)

给定表示网格尺寸的两个整数 **L** 和 **W** ，以及长度为 **N** 的两个数组 **X[]** 和 **Y[]** ，表示网格上位置 **(X[i]，Y[i])、**其中**(0<= I<= N–1)。**任务是找到野外最大的没有塔防御的无界区域。

**示例:**

> ***输入:** L = 15，W = 8，N = 3 X[] = {3，11，8} Y[] = {8，2，6}*
> **输出:** 12
> **说明:**
> 塔的坐标为(3，8)、(11，2)和(8，6)。
> 观察没有任何塔保护的电网的最大区域在单元(4，3)、(7，3)、(7，5)和(4，5)内。因此，该零件的面积为 12。
> 
> ***输入:** L = 3，W = 3，N = 1 X[] = {1} Y[] = {1}*
> **输出:** 4
> **解释:**
> 观察没有任何塔守护的电网最大面积为 4。

**天真方法:**按照以下步骤解决问题:

*   用 **0s 初始化尺寸为 **L * W** 的**矩阵**。**
*   遍历 **X[]** 和 **Y[]，**，对于每一个 **(X[i]，Y[i])** ，将 **X[i] <sup>第</sup>** 行和 **Y[i] <sup>第</sup>** 列中的所有单元格标记为 1，表示在 **(X[i]，Y[i])** 被塔守护。
*   然后遍历矩阵，对于每个单元，找到未被保护的最大子矩阵，即由 0 组成的最大子矩阵。打印相应的区域。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**高效方法:**上述方法可以使用以下[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)进行优化:

*   对坐标列表 **X[]** 和 **Y[]** 进行排序。
*   计算 X 坐标之间的空格，即 **dX[] = {X <sub>1</sub> ，X<sub>2</sub>–X<sub>1</sub>，…。，X<sub>N</sub>–X<sub>(N-1)</sub>、(L+1)–X<sub>N</sub>}**。同样，计算 Y 坐标之间的间距， **dY[] = {Y <sub>1</sub> ，Y<sub>2</sub>–Y<sub>1</sub>，…。，Y<sub>N</sub>–Y<sub>(N-1)</sub>、(W+1)–Y<sub>N</sub>}**。
*   遍历 **dX[]** 和 **dY[]** 并计算它们各自的最大值。
*   计算它们最大值的乘积，并将其打印为所需的最长无界区域。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <algorithm>
#include <iostream>
using namespace std;

// Function to calculate the largest
// area unguarded by towers
void maxArea(int point_x[], int point_y[], int n,
             int length, int width)
{
    // Sort the x-coordinates of the list
    sort(point_x, point_x + n);

    // Sort the y-coordinates of the list
    sort(point_y, point_y + n);

    // dx --> maximum uncovered
    // tiles in x coordinates
    int dx = point_x[0];

    // dy --> maximum uncovered
    // tiles in y coordinates
    int dy = point_y[0];

    // Calculate the maximum uncovered
    // distances for both  x and y coordinates
    for (int i = 1; i < n; i++) {
        dx = max(dx, point_x[i]
                         - point_x[i - 1]);

        dy = max(dy, point_y[i]
                         - point_y[i - 1]);
    }

    dx = max(dx, (length + 1)
                     - point_x[n - 1]);

    dy = max(dy, (width + 1)
                     - point_y[n - 1]);

    // Largest unguarded area is
    // max(dx)-1 * max(dy)-1
    cout << (dx - 1) * (dy - 1);

    cout << endl;
}

// Driver Code
int main()
{
    // Length and width of the grid
    int length = 15, width = 8;

    // No of guard towers
    int n = 3;

    // Array to store the x and
    // y coordinates
    int point_x[] = { 3, 11, 8 };
    int point_y[] = { 8, 2, 6 };

    // Function call
    maxArea(point_x, point_y,
            n, length, width);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to calculate the largest
// area unguarded by towers
static void maxArea(int[] point_x, int[] point_y,
                    int n, int length, int width)
{

    // Sort the x-coordinates of the list
    Arrays.sort(point_x);

    // Sort the y-coordinates of the list
    Arrays.sort(point_y);

    // dx --> maximum uncovered
    // tiles in x coordinates
    int dx = point_x[0];

    // dy --> maximum uncovered
    // tiles in y coordinates
    int dy = point_y[0];

    // Calculate the maximum uncovered
    // distances for both  x and y coordinates
    for(int i = 1; i < n; i++)
    {
        dx = Math.max(dx, point_x[i] -
                          point_x[i - 1]);
        dy = Math.max(dy, point_y[i] -
                          point_y[i - 1]);
    }

    dx = Math.max(dx, (length + 1) -
                    point_x[n - 1]);

    dy = Math.max(dy, (width + 1) -
                   point_y[n - 1]);

    // Largest unguarded area is
    // max(dx)-1 * max(dy)-1
    System.out.println((dx - 1) * (dy - 1));
}

// Driver Code
public static void main(String[] args)
{

    // Length and width of the grid
    int length = 15, width = 8;

    // No of guard towers
    int n = 3;

    // Array to store the x and
    // y coordinates
    int point_x[] = { 3, 11, 8 };
    int point_y[] = { 8, 2, 6 };

    // Function call
    maxArea(point_x, point_y, n,
            length, width);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the largest
# area unguarded by towers
def maxArea(point_x, point_y, n,
            length, width):

  # Sort the x-coordinates of the list
  point_x.sort()

  # Sort the y-coordinates of the list
  point_y.sort()

  # dx --> maximum uncovered
  # tiles in x coordinates
  dx = point_x[0]

  # dy --> maximum uncovered
  # tiles in y coordinates
  dy = point_y[0]

  # Calculate the maximum uncovered
  # distances for both  x and y coordinates
  for i in range(1, n):
      dx = max(dx, point_x[i] - 
                   point_x[i - 1])
      dy = max(dy, point_y[i] -
                   point_y[i - 1])

  dx = max(dx, (length + 1) -
             point_x[n - 1])

  dy = max(dy, (width + 1) -
            point_y[n - 1])

  # Largest unguarded area is
  # max(dx)-1 * max(dy)-1
  print((dx - 1) * (dy - 1))

# Driver Code
if __name__ == "__main__":

  # Length and width of the grid
  length = 15
  width = 8

  # No of guard towers
  n = 3

  # Array to store the x and
  # y coordinates
  point_x = [ 3, 11, 8 ]
  point_y = [ 8, 2, 6 ]

  # Function call
  maxArea(point_x, point_y, n,
          length, width)

# This code is contributed by akhilsaini
```

## C#

```
// C# Program for the above approach
using System;

class GFG{

// Function to calculate the largest
// area unguarded by towers
static void maxArea(int[] point_x, int[] point_y,
                    int n, int length, int width)
{

    // Sort the x-coordinates of the list
    Array.Sort(point_x);

    // Sort the y-coordinates of the list
    Array.Sort(point_y);

    // dx --> maximum uncovered
    // tiles in x coordinates
    int dx = point_x[0];

    // dy --> maximum uncovered
    // tiles in y coordinates
    int dy = point_y[0];

    // Calculate the maximum uncovered
    // distances for both  x and y coordinates
    for(int i = 1; i < n; i++)
    {
        dx = Math.Max(dx, point_x[i] -
                          point_x[i - 1]);
        dy = Math.Max(dy, point_y[i] -
                          point_y[i - 1]);
    }
    dx = Math.Max(dx, (length + 1) -
                    point_x[n - 1]);

    dy = Math.Max(dy, (width + 1) -
                   point_y[n - 1]);

    // Largest unguarded area is
    // max(dx)-1 * max(dy)-1
    Console.WriteLine((dx - 1) * (dy - 1));
}

// Driver Code
static public void Main()
{

    // Length and width of the grid
    int length = 15, width = 8;

    // No of guard towers
    int n = 3;

    // Array to store the x and
    // y coordinates
    int[] point_x = { 3, 11, 8 };
    int[] point_y = { 8, 2, 6 };

    // Function call
    maxArea(point_x, point_y, n,
            length, width);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to calculate the largest
// area unguarded by towers
function maxArea(polet_x, polet_y,
                    n, length, width)
{

    // Sort the x-coordinates of the list
    polet_x.sort((a, b) => a - b);;

    // Sort the y-coordinates of the list
    polet_y.sort((a, b) => a - b);;

    // dx --> maximum uncovered
    // tiles in x coordinates
    let dx = polet_x[0];

    // dy --> maximum uncovered
    // tiles in y coordinates
    let dy = polet_y[0];

    // Calculate the maximum uncovered
    // distances for both  x and y coordinates
    for(let i = 1; i < n; i++)
    {
        dx = Math.max(dx, polet_x[i] -
                          polet_x[i - 1]);
        dy = Math.max(dy, polet_y[i] -
                          polet_y[i - 1]);
    }

    dx = Math.max(dx, (length + 1) -
                    polet_x[n - 1]);

    dy = Math.max(dy, (width + 1) -
                   polet_y[n - 1]);

    // Largest unguarded area is
    // max(dx)-1 * max(dy)-1
    document.write((dx - 1) * (dy - 1));
}

// Driver Code

     // Length and width of the grid
    let length = 15, width = 8;

    // No of guard towers
    let n = 3;

    // Array to store the x and
    // y coordinates
    let polet_x = [ 3, 11, 8 ];
    let polet_y = [ 8, 2, 6 ];

    // Function call
    maxArea(polet_x, polet_y, n,
            length, width);

</script>
```

**Output:** 

```
12
```

***时间复杂度:** (N * log N)*
***辅助空间:** O(1)*