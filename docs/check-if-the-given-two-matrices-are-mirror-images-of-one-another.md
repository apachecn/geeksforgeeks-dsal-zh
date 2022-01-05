# 检查给定的两个矩阵是否是彼此的镜像

> 原文:[https://www . geeksforgeeks . org/check-如果给定的两个矩阵是彼此的镜像/](https://www.geeksforgeeks.org/check-if-the-given-two-matrices-are-mirror-images-of-one-another/)

给定两个大小为 **NxN** 的矩阵 **mat1[][]** 和 **mat2[][]** 。任务是找出给定的两个矩阵是否是彼此的镜像。如果给定的两个矩阵是镜像，则打印“**是”**，否则打印“**否”**。

> 如果对于矩阵的任何有效索引(I，j):
> ，大小为 N*N 的两个矩阵 **mat1** 和 **mat2** 被称为彼此的镜像
> 
> ```
> mat1[i][j] = mat2[i][N-j-1]
> ```
> 
> ![](https://media.geeksforgeeks.org/wp-content/uploads/20200906132655/mirror.png)

**示例:**

> **输入:**
> mat1[][] = {{1，2，3}，{3，4，5}，{6，7，8}}，
> mat2[][] = {{3，2，1}，{5，4，3}，{8，7，6 } }
> T5】输出:是
> 
> **输入:**
> mat1 = {{1，2，3}，{5，4，1}，{6，7，2 } }；
> mat2 = {{3，2，1}，{5，4，1}，{2，7，6 } }；
> **输出:**否

**方法:**该方法基于这样的观察，即只有当第一个矩阵的每行元素等于另一个矩阵的元素的反转行时，该矩阵才是另一个矩阵的镜像。请遵循以下步骤:

*   从头到尾逐行遍历矩阵 **mat1[][]** ，从头到尾逐行遍历 **mat2[][]** 。
*   遍历时，如果发现 **mat1[][]** 的任意元素不等于 **mat2[][]** 处的元素，则打印“否”
*   遍历两个矩阵后，如果发现所有元素都相等，则打印“是”。

以下是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check whether the
// two matrices are mirror
// of each other
void mirrorMatrix(int mat1[][4],
                  int mat2[][4], int N)
{
    // Initialising row and column of
    // second matrix
    int row = 0;
    int col = 0;

    bool isMirrorImage = true;

    // Iterating over the matrices
    for (int i = 0; i < N; i++) {

        // Check row of first matrix with
        // reversed row of second matrix
        for (int j = N - 1; j >= 0; j--) {

            // If the element is not equal
            if (mat2[row][col] != mat1[i][j]) {
                isMirrorImage = false;
            }

            // Increment column
            col++;
        }

        // Reset column to 0
        // for new row
        col = 0;

        // Increment row
        row++;
    }

    if (isMirrorImage)
        cout << "Yes";
    else
        cout << "No";
}

// Driver code
int main()
{
    // Given 2 matrices
    int N = 4;
    int mat1[][4] = { { 1, 2, 3, 4 },
                      { 0, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 } };

    int mat2[][4] = { { 4, 3, 2, 1 },
                      { 8, 7, 6, 0 },
                      { 12, 11, 10, 9 },
                      { 16, 15, 14, 13 } };

    // Function Call
    mirrorMatrix(mat1, mat2, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;
class GFG{

// Function to check whether the
// two matrices are mirror
// of each other
static void mirrorMatrix(int mat1[][],
                         int mat2[][], int N)
{
  // Initialising row and column of
  // second matrix
  int row = 0;
  int col = 0;

  boolean isMirrorImage = true;

  // Iterating over the matrices
  for (int i = 0; i < N; i++)
  {
    // Check row of first matrix with
    // reversed row of second matrix
    for (int j = N - 1; j >= 0; j--)
    {
      // If the element is not equal
      if (mat2[row][col] != mat1[i][j])
      {
        isMirrorImage = false;
      }

      // Increment column
      col++;
    }

    // Reset column to 0
    // for new row
    col = 0;

    // Increment row
    row++;
  }

  if (isMirrorImage)
    System.out.print("Yes");
  else
    System.out.print("No");
}

// Driver code
public static void main(String[] args)
{
  // Given 2 matrices
  int N = 4;
  int mat1[][] = {{1, 2, 3, 4},
                  {0, 6, 7, 8},
                  {9, 10, 11, 12},
                  {13, 14, 15, 16}};

  int mat2[][] = {{4, 3, 2, 1},
                  {8, 7, 6, 0},
                  {12, 11, 10, 9},
                  {16, 15, 14, 13}};

  // Function Call
  mirrorMatrix(mat1, mat2, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to check whether the
# two matrices are mirror
# of each other
def mirrorMatrix(mat1, mat2, N):

    # Initialising row and column of
    # second matrix
    row = 0
    col = 0

    isMirrorImage = True

    # Iterating over the matrices
    for i in range(N):

        # Check row of first matrix with
        # reversed row of second matrix
        for j in range(N - 1, -1, -1):

            # If the element is not equal
            if (mat2[row][col] != mat1[i][j]):
                isMirrorImage = False

            # Increment column
            col += 1

        # Reset column to 0
        # for new row
        col = 0

        # Increment row
        row += 1

    if (isMirrorImage):
        print("Yes")
    else:
        print("No")

# Driver code
if __name__ == '__main__':

    # Given 2 matrices
    N = 4
    mat1 = [ [ 1, 2, 3, 4 ],
             [ 0, 6, 7, 8 ],
             [ 9, 10, 11, 12 ],
             [ 13, 14, 15, 16 ] ]

    mat2 = [ [ 4, 3, 2, 1 ],
             [ 8, 7, 6, 0 ],
             [ 12, 11, 10, 9 ],
             [ 16, 15, 14, 13 ] ]

    # Function call
    mirrorMatrix(mat1, mat2, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function to check whether the
// two matrices are mirror
// of each other
static void mirrorMatrix(int[,] mat1,
                         int [,]mat2, int N)
{
  // Initialising row and column of
  // second matrix
  int row = 0;
  int col = 0;

  bool isMirrorImage = true;

  // Iterating over the matrices
  for (int i = 0; i < N; i++)
  {
    // Check row of first matrix with
    // reversed row of second matrix
    for (int j = N - 1; j >= 0; j--)
    {
      // If the element is not equal
      if (mat2[row, col] != mat1[i, j])
      {
        isMirrorImage = false;
      }

      // Increment column
      col++;
    }

    // Reset column to 0
    // for new row
    col = 0;

    // Increment row
    row++;
  }

  if (isMirrorImage)
    Console.Write("Yes");
  else
    Console.Write("No");
}

// Driver code
public static void Main(String[] args)
{
  // Given 2 matrices
  int N = 4;
  int [,]mat1 = {{1, 2, 3, 4},
                 {0, 6, 7, 8},
                 {9, 10, 11, 12},
                 {13, 14, 15, 16}};

  int [,]mat2 = {{4, 3, 2, 1},
                 {8, 7, 6, 0},
                 {12, 11, 10, 9},
                 {16, 15, 14, 13}};

  // Function Call
  mirrorMatrix(mat1, mat2, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

// Function to check whether the
// two matrices are mirror
// of each other
function mirrorMatrix(mat1, mat2, N)
{
    // Initialising row and column of
    // second matrix
    let row = 0;
    let col = 0;

    let isMirrorImage = true;

    // Iterating over the matrices
    for (let i = 0; i < N; i++) {

        // Check row of first matrix with
        // reversed row of second matrix
        for (let j = N - 1; j >= 0; j--) {

            // If the element is not equal
            if (mat2[row][col] != mat1[i][j]) {
                isMirrorImage = false;
            }

            // Increment column
            col++;
        }

        // Reset column to 0
        // for new row
        col = 0;

        // Increment row
        row++;
    }

    if (isMirrorImage)
        document.write("Yes");
    else
        document.write("No");
}

// Driver code
    // Given 2 matrices
    let N = 4;
    let mat1 = [ [ 1, 2, 3, 4 ],
                      [ 0, 6, 7, 8 ],
                      [ 9, 10, 11, 12 ],
                      [ 13, 14, 15, 16 ] ];

    let mat2 = [ [ 4, 3, 2, 1 ],
                      [ 8, 7, 6, 0 ],
                      [ 12, 11, 10, 9 ],
                      [ 16, 15, 14, 13 ] ];

    // Function Call
    mirrorMatrix(mat1, mat2, N);

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*