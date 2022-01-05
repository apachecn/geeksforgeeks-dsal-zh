# 检查给定矩阵是否平衡

> 原文:[https://www . geesforgeks . org/check-给定矩阵是否平衡/](https://www.geeksforgeeks.org/check-whether-the-given-matrix-is-balanced-or-not/)

给定尺寸为 **NxM** 的矩阵 **mat[][]** ，任务是检查给定矩阵是否平衡。打印“**平衡”**如果是平衡矩阵，则打印“**不平衡”**。

> 如果矩阵中的所有单元都是平衡的，则该矩阵是平衡的；如果该矩阵中与该单元相邻的单元数量严格大于写入该单元的值，则该矩阵的一个单元是平衡的。
> 相邻单元格是指每个单元格的上、下、左、右单元格中的单元格(如果存在)。

**示例:**

> **输入:** N = 3，M = 3
> mat[][] = {{1，2，3}，
> {4，5，6}，
> {7，8，9}}
> **输出:**不平衡
> **说明:**给定网格的每个单元都不稳定，所以整体网格不平衡。
> **输入:** N = 3，M = 3
> mat[][] = {{1，2，1}，
> {2，3，2}，
> {1，2，1}}
> **输出:** Balanced
> **说明:**给定网格的每个单元都是稳定的，所以整体网格是平衡的。

**进场:**

1.  遍历给定矩阵 **mat[][]** 。
2.  对于矩阵的每个单元，检查所有相邻单元，即**mat[I+1][j]、mat[i][j+1]、mat[i-1][j]、mat[I][j-1]【T1]是否严格小于当前单元。**
3.  对于矩阵的角单元，只有两个相邻的单元，即 **mat[i+1][j]和 mat[i][j+1]** ，检查是否所有这些相邻的单元都严格小于角单元。
4.  对于矩阵的边界单元，有 3 个相邻单元，即 **mat[i-1][j]，mat[i+1][j]，mat[i][j+1]** 检查是否所有这些相邻单元都严格小于边界单元。
5.  如果上述所有条件对矩阵的所有单元都成立，则打印“**平衡”**否则打印“**不平衡”**。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Define size of matrix
#define N 4
#define M 4

// Function to check given matrix
// balanced or unbalanced
string balancedMatrix(int mat[][M])
{

    // Flag for check matrix is balanced
    // or unbalanced
    bool is_balanced = true;

    // Iterate row until condition is true
    for (int i = 0; i < N && is_balanced; i++) {

        // Iterate cols until condition is true
        for (int j = 0; j < M && is_balanced; j++) {

            // Check for corner edge elements
            if ((i == 0 || i == N - 1)
                && (j == 0 || j == M - 1)) {
                if (mat[i][j] >= 2)
                    is_balanced = false;
            }

            // Check for border elements
            else if (i == 0 || i == N - 1
                     || j == 0 || j == M - 1) {
                if (mat[i][j] >= 3)
                    is_balanced = false;
            }
            else {

                // Check for the middle ones
                if (mat[i][j] >= 4)
                    is_balanced = false;
            }
        }
    }

    // Return balanced or not
    if (is_balanced)
        return "Balanced";
    else
        return "Unbalanced";
}

// Driver Code
int main()
{
    // Given Matrix mat[][]
    int mat[N][M] = { { 1, 2, 3, 4 },
                      { 3, 5, 2, 6 },
                      { 5, 3, 6, 1 },
                      { 9, 5, 6, 0 } };

    // Function Call
    cout << balancedMatrix(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

    // Define size of matrix
    static final int N = 4;
    static final int M = 4;

    // Function to check given matrix
    // balanced or unbalanced
    static String balancedMatrix(int mat[][])
    {

        // Flag for check matrix is balanced
        // or unbalanced
        boolean is_balanced = true;

        // Iterate row until condition is true
        for (int i = 0; i < N && is_balanced; i++)
        {

            // Iterate cols until condition is true
            for (int j = 0; j < M && is_balanced; j++)
            {

                // Check for corner edge elements
                if ((i == 0 || i == N - 1) &&
                    (j == 0 || j == M - 1))
                {
                    if (mat[i][j] >= 2)
                        is_balanced = false;
                }

                // Check for border elements
                else if (i == 0 || i == N - 1 ||
                         j == 0 || j == M - 1)
                {
                    if (mat[i][j] >= 3)
                        is_balanced = false;
                }
                else
                {

                    // Check for the middle ones
                    if (mat[i][j] >= 4)
                        is_balanced = false;
                }
            }
        }

        // Return balanced or not
        if (is_balanced)
            return "Balanced";
        else
            return "Unbalanced";
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Matrix mat[][]
        int mat[][] = {{1, 2, 3, 4},
                       {3, 5, 2, 6},
                       {5, 3, 6, 1},
                       {9, 5, 6, 0}};

        // Function Call
        System.out.print(balancedMatrix(mat));
    }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach
# Define the size of the matrix
N = 4
M = 4

# Function to check given matrix
# balanced or unbalanced
def balancedMatrix(mat):

    # Flag for check matrix is balanced
    # or unbalanced
    is_balanced = True

    # Iterate row until condition is true
    i = 0
    while i < N and is_balanced:

        # Iterate cols until condition is true
        j = 0
        while j < N and is_balanced:

            # Check for corner edge elements
            if ((i == 0 or i == N - 1) and
                (j == 0 or j == M - 1)):
                if mat[i][j] >= 2:
                    isbalanced = False

            # Check for border elements
            elif (i == 0 or i == N - 1 or
                  j == 0 or j == M - 1):
                if mat[i][j] >= 3:
                    is_balanced = False

            # Check for the middle ones
            else:
                if mat[i][j] >= 4:
                    is_balanced = False

            j += 1
        i += 1

    # Return balanced or not
    if is_balanced:
        return "Balanced"
    else:
        return "Unbalanced"

# Driver code

# Given matrix mat[][]
mat = [ [ 1, 2, 3, 4 ],
        [ 3, 5, 2, 6 ],
        [ 5, 3, 6, 1 ],
        [ 9, 5, 6, 0 ] ]

# Function call
print(balancedMatrix(mat))

# This code is contributed by Stuti Pathak
```

## C#

```
// C# program for the above approach
using System;
class GFG{

    // Define size of matrix
    static readonly int N = 4;
    static readonly int M = 4;

    // Function to check given matrix
    // balanced or unbalanced
    static String balancedMatrix(int [, ]mat)
    {
        // Flag for check matrix is balanced
        // or unbalanced
        bool is_balanced = true;

        // Iterate row until condition is true
        for (int i = 0; i < N && is_balanced; i++)
        {
            // Iterate cols until condition is true
            for (int j = 0; j < M && is_balanced; j++)
            {

                // Check for corner edge elements
                if ((i == 0 || i == N - 1) &&
                    (j == 0 || j == M - 1))
                {
                    if (mat[i, j] >= 2)
                        is_balanced = false;
                }

                // Check for border elements
                else if (i == 0 || i == N - 1 ||
                         j == 0 || j == M - 1)
                {
                    if (mat[i, j] >= 3)
                        is_balanced = false;
                }
                else
                {
                    // Check for the middle ones
                    if (mat[i, j] >= 4)
                        is_balanced = false;
                }
            }
        }

        // Return balanced or not
        if (is_balanced)
            return "Balanced";
        else
            return "Unbalanced";
    }

    // Driver Code
    public static void Main(String[] args)
    {     
        // Given Matrix [,]mat
        int [, ]mat = {{1, 2, 3, 4},
                       {3, 5, 2, 6},
                       {5, 3, 6, 1},
                       {9, 5, 6, 0}};

        // Function Call
        Console.Write(balancedMatrix(mat));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript Script program to implement
// the above approach

    // Define size of matrix
    let N = 4;
    let M = 4;

    // Function to check given matrix
    // balanced or unbalanced
    function balancedMatrix(mat)
    {

        // Flag for check matrix is balanced
        // or unbalanced
        let is_balanced = true;

        // Iterate row until condition is true
        for (let i = 0; i < N && is_balanced; i++)
        {

            // Iterate cols until condition is true
            for (let j = 0; j < M && is_balanced; j++)
            {

                // Check for corner edge elements
                if ((i == 0 || i == N - 1) &&
                    (j == 0 || j == M - 1))
                {
                    if (mat[i][j] >= 2)
                        is_balanced = false;
                }

                // Check for border elements
                else if (i == 0 || i == N - 1 ||
                         j == 0 || j == M - 1)
                {
                    if (mat[i][j] >= 3)
                        is_balanced = false;
                }
                else
                {

                    // Check for the middle ones
                    if (mat[i][j] >= 4)
                        is_balanced = false;
                }
            }
        }

        // Return balanced or not
        if (is_balanced)
            return "Balanced";
        else
            return "Unbalanced";
    }

// Driver Code

    // Given Matrix mat[][]
        let mat = [[1, 2, 3, 4],
                       [3, 5, 2, 6],
                       [5, 3, 6, 1],
                       [9, 5, 6, 0]];

        // Function Call
        document.write(balancedMatrix(mat));

</script>
```

**Output:** 

```
Unbalanced
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*