# 二进制矩阵中相应行和列中具有相等设置位计数的计数位置

> 原文：[https://www.geeksforgeeks.org/count-positions-in-binary-matrix-having-equal-count-of-set-bits-in-corresponding-row-and-column/](https://www.geeksforgeeks.org/count-positions-in-binary-matrix-having-equal-count-of-set-bits-in-corresponding-row-and-column/)

给定一个布尔型矩阵`mat[][]`，大小为`M * N`，任务是从矩阵中打印索引的计数，该矩阵的相应行和列包含相同数量的设置位。

**示例**：

> **输入**；`mat[][] = {{0, 1}, {1, 1}}`
> **输出**：2
> **说明**：
> 位置`(0, 0)`在相应的行`{(0, 0), (0, 1)}`和列`{(0, 0), (1, 0)}`中包含 1 个设置位。
> 位置`(1, 1)`在相应的行`{(1, 0), (1, 1)}`和列`{(0, 1), (1, 1)}`中包含 2 个设置位。
> 
> **输入**：`mat[][] = {{0, 1, 1, 0}, {0, 1, 0, 0}, {1, 0, 1, 0}}`
> **输出**：5

**朴素的方法**：解决的最简单方法是计算和存储给定矩阵的每一行和每一列的元素中存在的设置位的数量。 然后，遍历矩阵，并针对每个位置，检查行和列的设置位计数是否相等。 对于发现上述条件为真的每个索引，增加 ***计数*** 。 完全遍历矩阵后，打印**计数**的最终值。

**时间复杂度**：`O(N ^ 2)`

**辅助空间**：`O(N ^ 2)`

**有效方法**：要优化上述方法，请按照以下步骤操作：

*   分别初始化两个临时数组`row[]`和`col[]`，大小分别为`N`和`M`。

*   遍历矩阵`mat[][]`。 如果`mat[i][j]`等于 **1**，则检查每个索引`(i, j)`。 如果确定为真，则将`row[i]`和`col[j]`递增 **1**。

*   再次遍历矩阵`mat[][]`。 如果`row[i]`和`col[j]`是否相等，请检查每个索引`(i, j)`。 如果发现为真，则增加**计数**。

*   打印**计数**的最终值。

下面是上述方法的实现：

## C++ 14

```

// C++14 program to implement
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of indices in
// from the given binary matrix having equal
// count of set bits in its row and column
int countPosition(vector<vector<int>> mat)
{
    int n = mat.size();
    int m = mat[0].size();

    // Stores count of set bits in
    // coressponding column and row
    vector<int> row(n);
    vector<int> col(m);

    // Traverse matrix
    for(int i = 0; i < n; i++) 
    {
        for(int j = 0; j < m; j++) 
        {

            // Since 1 contains a set bit
            if (mat[i][j] == 1) 
            {

                // Update count of set bits
                // for current row and col
                col[j]++;
                row[i]++;
            }
        }
    }

    // Stores the count of
    // required indices
    int count = 0;

    // Traverse matrix
    for(int i = 0; i < n; i++) 
    {
        for(int j = 0; j < m; j++)
        {

            // If current row and column
            // has equal count of set bits
            if (row[i] == col[j]) 
            {
                count++;
            }
        }
    }

    // Return count of
    // required position
    return count;
}

// Driver Code
int main()
{
    vector<vector<int>> mat = { { 0, 1 },
                                { 1, 1 } };

    cout << (countPosition(mat));
}

// This code is contributed by mohit kumar 29

```

## Java

```java

// Java Program to implement
// above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to return the count of indices in
    // from the given binary matrix having equal
    // count of set bits in its row and column
    static int countPosition(int[][] mat)
    {

        int n = mat.length;
        int m = mat[0].length;

        // Stores count of set bits in
        // coressponding column and row
        int[] row = new int[n];
        int[] col = new int[m];

        // Traverse matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {

                // Since 1 contains a set bit
                if (mat[i][j] == 1) {

                    // Update count of set bits
                    // for current row and col
                    col[j]++;
                    row[i]++;
                }
            }
        }

        // Stores the count of
        // required indices
        int count = 0;

        // Traverse matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {

                // If current row and column
                // has equal count of set bits
                if (row[i] == col[j]) {
                    count++;
                }
            }
        }

        // Return count of
        // required position
        return count;
    }

    // Driver Code
    public static void main(
        String[] args)
    {

        int mat[][] = { { 0, 1 },
                        { 1, 1 } };

        System.out.println(
            countPosition(mat));
    }
}

```

## Python3

```py

# Python3 program to implement
# the above approach

# Function to return the count 
# of indices in from the given 
# binary matrix having equal
# count of set bits in its
# row and column
def countPosition(mat):

    n = len(mat)
    m = len(mat[0])

    # Stores count of set bits in
    # coressponding column and row
    row = [0] * n
    col = [0] * m

    # Traverse matrix
    for i in range(n):
        for j in range(m):

            # Since 1 contains a set bit
            if (mat[i][j] == 1):

                # Update count of set bits
                # for current row and col
                col[j] += 1
                row[i] += 1

    # Stores the count of
    # required indices
    count = 0

    # Traverse matrix
    for i in range(n):
        for j in range(m):

            # If current row and column
            # has equal count of set bits
            if (row[i] == col[j]):
                count += 1

    # Return count of
    # required position
    return count

# Driver Code
mat = [ [ 0, 1 ],
        [ 1, 1 ] ]

print(countPosition(mat))

# This code is contributed by sanjoy_62

```

## C#

```cs

// C# Program to implement
// above approach
using System;
class GFG{

// Function to return the count of indices in
// from the given binary matrix having equal
// count of set bits in its row and column
static int countPosition(int[,] mat)
{

  int n = mat.GetLength(0);
  int m = mat.GetLength(1);

  // Stores count of set bits in
  // coressponding column and row
  int[] row = new int[n];
  int[] col = new int[m];

  // Traverse matrix
  for (int i = 0; i < n; i++) 
  {
    for (int j = 0; j < m; j++) 
    {
      // Since 1 contains a set bit
      if (mat[i, j] == 1) 
      {
        // Update count of set bits
        // for current row and col
        col[j]++;
        row[i]++;
      }
    }
  }

  // Stores the count of
  // required indices
  int count = 0;

  // Traverse matrix
  for (int i = 0; i < n; i++) 
  {
    for (int j = 0; j < m; j++) 
    {
      // If current row and column
      // has equal count of set bits
      if (row[i] == col[j]) 
      {
        count++;
      }
    }
  }

  // Return count of
  // required position
  return count;
}

// Driver Code
public static void Main(String[] args)
{
  int [,]mat = {{0, 1},
                {1, 1}};
  Console.WriteLine(countPosition(mat));
}
}

// This code is contributed by Rajput-Ji

```

**输出**： 

```
2

```

**时间复杂度**：`O(N * M)`

**辅助空间**：`O(N + M)`



* * *

* * *



