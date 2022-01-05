# 求区域 Z 的平方数，该平方数可以建立在具有分块区域的矩阵中

> 原文:[https://www . geeksforgeeks . org/find-面积平方数-z-哪些可以内置于具有封闭区域的矩阵中/](https://www.geeksforgeeks.org/find-number-of-square-of-area-z-which-can-be-built-in-a-matrix-having-blocked-regions/)

在 **N * N** 矩阵中，某些行和列被阻塞。求区域 **Z** 的方块数，在给定的约束条件下可以在这样的矩阵中构建:

1.  每个小区将贡献 **1** 单位面积， **1** 小区恰好属于 **1** 子网格。
2.  所有单元格都应该是未阻塞的单元格。

被阻挡的行和列由两个阵列**行[]** 和**列[]** 表示。
**例:**

> **输入:** N = 8，Z = 4，row[] = {4，6}，col[] = {3， 8}
> **输出:** 6
> 这里是需要的矩阵:
> 1 1 X 2 2 2 2 X
> 1 1 X 2 2 2 X
> 1 1 X 2 2 2 X
> 3 X 4 4 4 4 X
> X X X X X X X X X X
> 5 5 X 6 6 6 X
> 5 X 6 6 X 6
> 其中 X 代表被阻断的细胞。 1–6 代表未阻挡的矩形区域。
> 对答案的贡献如下:
> 区域 1: 1 区域 4
> 区域 2: 2 区域 4
> 区域 3:无区域 4
> 区域 4:无区域 4
> 区域 5: 1 区域 4
> 区域 6: 2 区域 4

**进场:**

*   这里，实际的矩阵将被分成几个矩形。区域只能在这些矩形中构建。假设存在一个尺寸为 **R * L** 的矩形，那么面积为 **Z** 的区域数将等于 **(R / K) * (L / K)** ，其中 **K** 是 **Z** 的平方根，因为长度为 **L** 的尺寸 **K** 的最大平方是 **L / K** ，宽度也是如此。因此，任务是找到所有这些矩形的尺寸，并计算其中可能的面积数量。
*   为了找到矩形，首先所有被阻挡的行和列已经按照排序顺序给出。现在，考虑第一个被阻止的行和第一个被阻止的列之间的区域。这个地区完全没有封锁。类似地，任何两个连续被阻挡的列之间的区域以及任何两个连续被阻挡的行将形成未阻挡的区域。
*   因此，基本上任何未阻塞的区域将位于任何两个连续的阻塞行和任何两个连续的阻塞列之间。我们可以存储连续阻塞行和连续阻塞列之间的长度，然后我们可以从行数组和列数组中取任意长度并相乘。
*   找到所有这些未被阻挡的区域，然后将大小为 **K * K** 的方块数相加，使其总数尽可能合适。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the number of
// square areas of size K*K
int subgrids(int N, int Z, int row[],
             int col[], int r, int c)
{
    // Row array and column array to
    // store the lengths of differences
    // between consecutive rows/columns
    vector<int> conrow;
    vector<int> concol;

    int K = sqrt(Z);

    // Fill the conrow vector
    conrow.push_back(row[0] - 0 - 1);
    conrow.push_back(N + 1 - row[r - 1] - 1);
    for (int i = 1; i < r; i++) {
        conrow.push_back(row[i] - row[i - 1] - 1);
    }

    // Fill the concol vector
    concol.push_back(col[0] - 0 - 1);
    concol.push_back(N + 1 - col - 1);
    for (int i = 1; i < c; i++) {
        concol.push_back(col[i] - col[i - 1] - 1);
    }

    int row_size = conrow.size();
    int col_size = concol.size();

    // To store the required answer
    int answer = 0;

    // Every pair of row size and column size
    // would result in an unblocked region
    for (int i = 0; i < row_size; i++) {
        for (int j = 0; j < col_size; j++) {
            int total = (concol[j] / K)
                        * (conrow[i] / K);
            answer += (total);
        }
    }

    return answer;
}

// Driver code
int main()
{
    int N = 8, Z = 4;
    int row[] = { 4, 6 };
    int col[] = { 3, 8 };
    int r = sizeof(row) / sizeof(row[0]);
    int c = sizeof(col) / sizeof(col[0]);

    cout << subgrids(N, Z, row, col, r, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to calculate the number of
// square areas of size K*K
static int subgrids(int N, int Z, int row[],
                    int col[], int r, int d)
{
    // Row array and column array to
    // store the lengths of differences
    // between consecutive rows/columns
    Vector<Integer> conrow = new Vector<Integer>();
    Vector<Integer> concol = new Vector<Integer>();

    int K = (int) Math.sqrt(Z);

    // Fill the conrow vector
    conrow.add(row[0] - 0 - 1);
    conrow.add(N + 1 - row[r - 1] - 1);
    for (int i = 1; i < r; i++)
    {
        conrow.add(row[i] - row[i - 1] - 1);
    }

    // Fill the concol vector
    concol.add(col[0] - 0 - 1);
    concol.add(N + 1 - col[d - 1] - 1);
    for (int i = 1; i < d; i++)
    {
        concol.add(col[i] - col[i - 1] - 1);
    }

    int row_size = conrow.size();
    int col_size = concol.size();

    // To store the required answer
    int answer = 0;

    // Every pair of row size and column size
    // would result in an unblocked region
    for (int i = 0; i < row_size; i++)
    {
        for (int j = 0; j < col_size; j++)
        {
            int total = (concol.get(j) / K) *
                        (conrow.get(i) / K);
            answer += (total);
        }
    }
    return answer;
}

// Driver code
public static void main(String[] args)
{
    int N = 8, Z = 4;
    int row[] = { 4, 6 };
    int col[] = { 3, 8 };
    int r = row.length;
    int d = col.length;

    System.out.print(subgrids(N, Z, row, col, r, d));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# Function to calculate the number of
# square areas of size K*K
def subgrids(N, Z, row, col, r, d) :

    # Row array and column array to
    # store the lengths of differences
    # between consecutive rows/columns
    conrow = [];
    concol = [];

    K = int(sqrt(Z));

    # Fill the conrow vector
    conrow.append(row[0] - 0 - 1)
    conrow.append(N + 1 - row[r - 1] - 1)

    for i in range(1, r) :
        conrow.append(row[i] - row[i - 1] - 1);

    # Fill the concol vector
    concol.append(col[0] - 0 - 1)
    concol.append(N + 1 - col[d - 1] - 1)

    for i in range(1, d) :
        concol.append(col[i] - col[i - 1] - 1);

    row_size = len(conrow)
    col_size = len(concol)

    # To store the required answer
    answer = 0

    # Every pair of row size and column size
    # would result in an unblocked region
    for i in range(row_size) :
        for j in range(col_size) :
            total = (concol[j] // K) * \
                    (conrow[i] // K)
            answer += (total)

    return answer

# Driver code
if __name__ == "__main__" :

    N = 8; Z = 4
    row = [ 4, 6 ]
    col = [ 3, 8 ]
    r = len(row)
    d = len(col)

    print(subgrids(N, Z, row, col, r, d))

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to calculate the number of
// square areas of size K*K
static int subgrids(int N, int Z, int []row,
                    int []col, int r, int d)
{
    // Row array and column array to
    // store the lengths of differences
    // between consecutive rows/columns
    List<int> conrow = new List<int>();
    List<int> concol = new List<int>();

    int K = (int) Math.Sqrt(Z);

    // Fill the conrow vector
    conrow.Add(row[0] - 0 - 1);
    conrow.Add(N + 1 - row[r - 1] - 1);
    for (int i = 1; i < r; i++)
    {
        conrow.Add(row[i] - row[i - 1] - 1);
    }

    // Fill the concol vector
    concol.Add(col[0] - 0 - 1);
    concol.Add(N + 1 - col[d - 1] - 1);
    for (int i = 1; i < d; i++)
    {
        concol.Add(col[i] - col[i - 1] - 1);
    }

    int row_size = conrow.Count;
    int col_size = concol.Count;

    // To store the required answer
    int answer = 0;

    // Every pair of row size and column size
    // would result in an unblocked region
    for (int i = 0; i < row_size; i++)
    {
        for (int j = 0; j < col_size; j++)
        {
            int total = (concol[j] / K) *
                        (conrow[i] / K);
            answer += (total);
        }
    }
    return answer;
}

// Driver code
public static void Main(String[] args)
{
    int N = 8, Z = 4;
    int []row = { 4, 6 };
    int []col = { 3, 8 };
    int r = row.Length;
    int d = col.Length;

    Console.Write(subgrids(N, Z, row, col, r, d));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to calculate the number of
// square areas of size K*K
function subgrids(N, Z, row, col, r, c)
{
    // Row array and column array to
    // store the lengths of differences
    // between consecutive rows/columns
    var conrow = [];
    var concol = [];

    var K = Math.sqrt(Z);

    // Fill the conrow vector
    conrow.push(row[0] - 0 - 1);
    conrow.push(N + 1 - row[r - 1] - 1);
    for (var i = 1; i < r; i++) {
        conrow.push(row[i] - row[i - 1] - 1);
    }

    // Fill the concol vector
    concol.push(col[0] - 0 - 1);
    concol.push(N + 1 - col - 1);
    for (var i = 1; i < c; i++) {
        concol.push(col[i] - col[i - 1] - 1);
    }

    var row_size = conrow.length;
    var col_size = concol.length;

    // To store the required answer
    var answer = 0;

    // Every pair of row size and column size
    // would result in an unblocked region
    for (var i = 0; i < row_size; i++) {
        for (var j = 0; j < col_size; j++) {
            var total = parseInt(concol[j] / K)
                        * parseInt(conrow[i] / K);
            answer += (total);
        }
    }

    return answer;
}

// Driver code
var N = 8, Z = 4;
var row = [4, 6];
var col = [3, 8];
var r = row.length;
var c = col.length;
document.write( subgrids(N, Z, row, col, r, c));

</script>
```

**Output:** 

```
6
```