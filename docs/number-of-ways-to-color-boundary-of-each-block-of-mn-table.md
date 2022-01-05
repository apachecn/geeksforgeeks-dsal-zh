# M * N 表各块颜色边界的方式数

> 原文:[https://www . geeksforgeeks . org/每个 mn 块表的颜色边界的路数/](https://www.geeksforgeeks.org/number-of-ways-to-color-boundary-of-each-block-of-mn-table/)

给定一张 **M * N** 的表格。总共有 M * N 个大小为 1 的正方形。你必须用 3 种颜色橙色、蓝色或黑色给所有正方形的每一面上色，这样每个正方形就有 2 种不同的颜色，而且每种颜色必须出现两次。
表示每个正方形有四条边，其中两条是橙色，两条是蓝色，或者两条是橙色，两条是黑色，或者两条是蓝色，两条是黑色。
**示例:**

> **输入:** N = 1，M = 1
> **输出:** 18
> **解释:**
> 我们可以用三种颜色中的任意一种填充正方形的上半部分和正方形的左半部分。所以路的数量是 3*3，
> 现在填充右边和下面部分，如果上面和左边有相同的颜色，我们只有 2 个选项。
> 如果上半部分和左半部分的颜色不同，那么我们可以用这两种颜色来填充右半部分和下半部分，它还有 2 个选项。向右下方填充的组合数为 2。
> 给正方形上色的一种可能方法是 3*3*2 = 18
> **输入:** N = 3，M = 2
> **输出:** 15552

**进场:**

*   找出填充矩形右上侧的方法。上侧有 M 个单位，右侧有 N 个单位。所以，给矩形的上侧和右侧上色的方法数量是**次方(3，M + N)** ，因为每个方法都有 3 个选项。
*   现在，为了填充每个方块的下方和左侧，每个方块有 2 个选项，那么路的数量是**次方(2，M * N)** 。
*   最终结果是:

```
 Total count = pow(3, M + N ) *  pow(2, M * N)
```

以下是上述方法的实现:

## C++

```
// C++ program to count the number
// of ways to color boundary of
// each block of M*N table.
#include <bits/stdc++.h>
using namespace std;

// Function to compute all way to
// fill the boundary of all sides
// of the unit square
int CountWays(int N, int M)
{
    int count = 1;

    // Count possible ways to fill
    // all upper and left side of
    // the rectangle M*N
    count = pow(3, M + N);

    // Count possible ways to fill
    // all  side of the all squares
    // unit size
    count *= pow(2, M * N);

    return count;
}

// Driver code
int main()
{

    // Number of rows
    int N = 3;

    // Number of columns
    int M = 2;

    cout << CountWays(N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number
// of ways to color boundary of
// each block of M*N table.
import java.util.*;

class GFG{

// Function to compute all way to
// fill the boundary of all sides
// of the unit square
static int CountWays(int N, int M)
{
    int count = 1;

    // Count possible ways to fill
    // all upper and left side of
    // the rectangle M*N
    count = (int)Math.pow(3, M + N);

    // Count possible ways to fill
    // all side of the all squares
    // unit size
    count *= (int)Math.pow(2, M * N);

    return count;
}

// Driver code
public static void main(String args[])
{

    // Number of rows
    int N = 3;

    // Number of columns
    int M = 2;

    System.out.println(CountWays(N, M));
}
}

// This code is contributed by ANKITKUMAR34
```

## 蟒蛇 3

```
# Python3 program to count the number
# of ways to color boundary of
# each block of M*N table.

# Function to compute all way to
# fill the boundary of all sides
# of the unit square
def CountWays(N, M):

    count = 1

    # Count possible ways to fill
    # all upper and left side of
    # the rectangle M*N
    count = pow(3, M + N)

    # Count possible ways to fill
    # all side of the all squares
    # unit size
    count *= pow(2, M * N);

    return count

# Driver code

# Number of rows
N = 3

# Number of columns
M = 2

print(CountWays(N, M))

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# program to count the number
// of ways to color boundary of
// each block of M*N table.
using System;

class GFG{

// Function to compute all way to
// fill the boundary of all sides
// of the unit square
static int CountWays(int N, int M)
{
    int count = 1;

    // Count possible ways to fill
    // all upper and left side of
    // the rectangle M*N
    count = (int)Math.Pow(3, M + N);

    // Count possible ways to fill
    // all side of the all squares
    // unit size
    count *= (int)Math.Pow(2, M * N);

    return count;
}

// Driver code
static void Main()
{

    // Number of rows
    int N = 3;

    // Number of columns
    int M = 2;

    Console.Write(CountWays(N, M));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program to count the number
// of ways to color boundary of
// each block of M*N table.

// Function to compute all way to
// fill the boundary of all sides
// of the unit square
function CountWays(N, M)
{
    var count = 1;

    // Count possible ways to fill
    // all upper and left side of
    // the rectangle M*N
    count = Math.pow(3, M + N);

    // Count possible ways to fill
    // all  side of the all squares
    // unit size
    count *= Math.pow(2, M * N);

    return count;
}

// Driver code
// Number of rows
var N = 3;

// Number of columns
var M = 2;

document.write( CountWays(N, M));

</script>
```

**Output:** 

```
15552
```

时间复杂度:0(对数(m * n))

辅助空间:0(1)