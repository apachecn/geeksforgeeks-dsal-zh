# 访问 N * M 网格所有角落所需的最少步骤

> 原文:[https://www . geeksforgeeks . org/访问 n-n-m-grid 所有角落所需的最少步骤/](https://www.geeksforgeeks.org/minimum-steps-required-to-visit-all-corners-of-an-n-m-grid/)

给定两个整数 **N** 和 **M** 表示一个 **2D** 网格的尺寸，以及两个整数 **R** 和 **C** ，表示一个块在该网格中的位置，任务是从 **(R，C)** 开始，找到访问网格所有角落所需的最小步数。在每一步中，允许移动网格中的相邻边块。

**示例:**

> **输入:** N = 2，M = 2，R = 1，C = 2
> T3】输出: 3
> 
> **说明:**
> (1，2)—>(1，1)—>(2，1)—>(2，2)
> 因此，所需输出为 3。
> 
> **输入:** N = 2，M = 3，R = 2，C = 2
> **输出:** 5
> **解释:**
> (2，2)—>(2，3)—>(1，3)—>(1，2)—>(1，1)—>(2，1)
> 因此，所需输出为 5。

**方法:**根据以下观察，可以解决问题。

> 从(i <sub>1</sub> 、j <sub>1</sub> )开始访问区块(i <sub>2</sub> 、j <sub>2</sub> )所需的最小步数等于 ABS(I<sub>2</sub>–I<sub>1</sub>)+ABS(j<sub>2</sub>–j<sub>1</sub>)

按照下面给出的步骤解决问题:

*   首先，使用上述观察结果，访问需要最少步数的角落。
*   通过顺时针或逆时针遍历网格的边界来访问网格的其他角，这取决于访问角所需的最小步数。
*   最后，打印获得的最小步数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count of steps
// required to visit all the corners of the grid
int min_steps_required(int n, int m, int r, int c)
{

    // Stores corner of the grid
    int i, j;

    // Stores minimum count of steps required
    // to visit the first corner of the grid
    int corner_steps_req = INT_MAX;

    // Checking for leftmost upper corner
    i = 1;
    j = 1;
    corner_steps_req = min(corner_steps_req,
                           abs(r - i) + abs(j - c));

    // Checking for leftmost down corner
    i = n;
    j = 1;
    corner_steps_req = min(corner_steps_req,
                           abs(r - i) + abs(j - c));

    // Checking for rightmost upper corner
    i = 1;
    j = m;
    corner_steps_req = min(corner_steps_req,
                           abs(r - i) + abs(j - c));

    // Checking for rightmost down corner
    i = n;
    j = m;
    corner_steps_req = min(corner_steps_req,
                           abs(r - i) + abs(j - c));

    // Stores minimum count of steps required
    // to visit remaining three corners of the grid
    int minimum_steps = min(2 * (n - 1) + m - 1,
                            2 * (m - 1) + n - 1);

    return minimum_steps + corner_steps_req;
}

// Driver Code
int main()
{

    int n = 3;
    int m = 2;
    int r = 1;
    int c = 1;

    cout << min_steps_required(n, m, r, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement the
// above approach
import java.util.*;
class GFG
{

// Function to find the minimum count of steps
// required to visit all the corners of the grid
static int min_steps_required(int n, int m, int r, int c)
{

    // Stores corner of the grid
    int i, j;

    // Stores minimum count of steps required
    // to visit the first corner of the grid
    int corner_steps_req = Integer.MAX_VALUE;

    // Checking for leftmost upper corner
    i = 1;
    j = 1;
    corner_steps_req = Math.min(corner_steps_req,
                           Math.abs(r - i) + Math.abs(j - c));

    // Checking for leftmost down corner
    i = n;
    j = 1;
    corner_steps_req = Math.min(corner_steps_req,
                           Math.abs(r - i) + Math.abs(j - c));

    // Checking for rightmost upper corner
    i = 1;
    j = m;
    corner_steps_req = Math.min(corner_steps_req,
                           Math.abs(r - i) + Math.abs(j - c));

    // Checking for rightmost down corner
    i = n;
    j = m;
    corner_steps_req = Math.min(corner_steps_req,
                           Math.abs(r - i) + Math.abs(j - c));

    // Stores minimum count of steps required
    // to visit remaining three corners of the grid
    int minimum_steps = Math.min(2 * (n - 1) + m - 1,
                            2 * (m - 1) + n - 1);

    return minimum_steps + corner_steps_req;
}

// Driver Code
public static void main(String[] args)
{
    int n = 3;
    int m = 2;
    int r = 1;
    int c = 1;

    System.out.print(min_steps_required(n, m, r, c));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys
INT_MAX = sys.maxsize;

# Function to find the minimum count of steps
# required to visit all the corners of the grid
def min_steps_required(n, m, r, c) :

    # Stores corner of the grid
    i = 0; j = 0;

    # Stores minimum count of steps required
    # to visit the first corner of the grid
    corner_steps_req = INT_MAX;

    # Checking for leftmost upper corner
    i = 1;
    j = 1;
    corner_steps_req = min(corner_steps_req,
                           abs(r - i) + abs(j - c));

    # Checking for leftmost down corner
    i = n;
    j = 1;
    corner_steps_req = min(corner_steps_req,
                           abs(r - i) + abs(j - c));

    # Checking for rightmost upper corner
    i = 1;
    j = m;
    corner_steps_req = min(corner_steps_req,
                           abs(r - i) + abs(j - c));

    # Checking for rightmost down corner
    i = n;
    j = m;
    corner_steps_req = min(corner_steps_req,
                           abs(r - i) + abs(j - c));

    # Stores minimum count of steps required
    # to visit remaining three corners of the grid
    minimum_steps = min(2 * (n - 1) + m - 1,
                            2 * (m - 1) + n - 1);

    return minimum_steps + corner_steps_req;

# Driver Code
if __name__ == "__main__" :
    n = 3;
    m = 2;
    r = 1;
    c = 1;
    print(min_steps_required(n, m, r, c));

    # This code is contributed by AnkThon
```

## C#

```
// C# program to implement the
// above approach
using System;

class GFG{

// Function to find the minimum count
// of steps required to visit all the
// corners of the grid
static int min_steps_required(int n, int m,
                              int r, int c)
{

    // Stores corner of the grid
    int i, j;

    // Stores minimum count of steps required
    // to visit the first corner of the grid
    int corner_steps_req = int.MaxValue;

    // Checking for leftmost upper corner
    i = 1;
    j = 1;
    corner_steps_req = Math.Min(corner_steps_req,
                                Math.Abs(r - i) +
                                Math.Abs(j - c));

    // Checking for leftmost down corner
    i = n;
    j = 1;
    corner_steps_req = Math.Min(corner_steps_req,
                                Math.Abs(r - i) +
                                Math.Abs(j - c));

    // Checking for rightmost upper corner
    i = 1;
    j = m;
    corner_steps_req = Math.Min(corner_steps_req,
                                Math.Abs(r - i) +
                                Math.Abs(j - c));

    // Checking for rightmost down corner
    i = n;
    j = m;
    corner_steps_req = Math.Min(corner_steps_req,
                                Math.Abs(r - i) +
                                Math.Abs(j - c));

    // Stores minimum count of steps required
    // to visit remaining three corners of the grid
    int minimum_steps = Math.Min(2 * (n - 1) + m - 1,
                                 2 * (m - 1) + n - 1);

    return minimum_steps + corner_steps_req;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 3;
    int m = 2;
    int r = 1;
    int c = 1;

    Console.Write(min_steps_required(n, m, r, c));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to implement the
// above approach

// Function to find the minimum count
// of steps required to visit all the
// corners of the grid

function  min_steps_required( n,  m,  r,  c)
{

    // Stores corner of the grid
    var i, j;

    // Stores minimum count of steps required
    // to visit the first corner of the grid

    var corner_steps_req = Number.MAX_VALUE;

    // Checking for leftmost upper corner

    i = 1;
    j = 1;
    corner_steps_req = Math.min(corner_steps_req,
                                Math.abs(r - i) +
                                Math.abs(j - c));

    // Checking for leftmost down corner
    i = n;
    j = 1;
    corner_steps_req = Math.min(corner_steps_req,
                                Math.abs(r - i) +
                                Math.abs(j - c));

    // Checking for rightmost upper corner
    i = 1;
    j = m;
    corner_steps_req = Math.min(corner_steps_req,
                                Math.abs(r - i) +
                                Math.abs(j - c));

    // Checking for rightmost down corner
    i = n;
    j = m;
    corner_steps_req = Math.min(corner_steps_req,
                                Math.abs(r - i) +
                                Math.abs(j - c));

    // Stores minimum count of steps required
    // to visit remaining three corners of the grid
    var minimum_steps = Math.min(2 * (n - 1) + m - 1,
                                 2 * (m - 1) + n - 1);

    return minimum_steps + corner_steps_req;
}

// Driver Code

    var n = 3;
    var m = 2;
    var r = 1;
    var c = 1;

    document.write(min_steps_required(n, m, r, c));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)