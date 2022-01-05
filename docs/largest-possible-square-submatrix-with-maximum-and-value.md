# 具有最大“与”值的最大可能正方形子矩阵

> 原文:[https://www . geeksforgeeks . org/最大可能平方子矩阵最大值/](https://www.geeksforgeeks.org/largest-possible-square-submatrix-with-maximum-and-value/)

给定一个整数矩阵 **mat [ ][ ]** 维，任务是从给定的矩阵中找到最大可能的正方形矩阵，该矩阵具有最大的[和](https://www.geeksforgeeks.org/bitwise-and-of-all-the-elements-of-array/)值。

> 矩阵的“与”值定义为对矩阵的所有元素执行按位“与”运算后获得的值。

**示例:**

> **输入:** mat [ ][ ] = {{2，3，3}，{2，3，3}，{2，2，2}}
> **输出:** 4
> **解释:**
> 给定的正方形子矩阵的 AND 值为 2。
> 大小为 4 的子矩阵
> {{3，3}
> {3，3}}
> 的最大“与”值为 3。所有其他大小为 4 的正方形子矩阵的“与”值为 2。
> 
> **输入:** mat [ ][ ] =
> {{9，9，9，8}，
> {9，9，9，6}，
> {9，9，9，3}，
> {2，2，2，2}}
> **输出:** 9
> **解释:**
> 大小为 9 的子矩阵
> {{9，9，9}，
> {9，9，9}，

**天真方法:**
从给定矩阵生成所有正方形子矩阵。初始化一个变量**回答**以存储子矩阵的最大&值，另一个变量**计数**以存储子矩阵中的元素数量。打印从所有正方形子矩阵获得的最大与值**答案**对应的**计数**的最大值。

**高效方法:**
按照以下步骤优化上述解决方案:

*   为了最大化& value，我们需要找到一个只包含矩阵中最大元素的子矩阵。这是因为矩阵中最大可能的“与”值是矩阵中存在的最大元素。
*   找出矩阵中存在的最大可能值。
*   使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)方法，只获取由最大矩阵元素填充的最大尺寸子矩阵。
*   创建一个辅助 **dp[][]** ，这样 dp[i][j]存储最大可能的正方形子矩阵 mat[i][j]可以是的一部分，这样子矩阵的 AND 值等于 mat[i][j]。
*   循环关系如下:

> 如果 **mat[i][j]** 等于 **{mat[i-1][j]，mat[i][j-1]，mat[i-1][j-1]}** 那么将这三个值都看作一个正方形子矩阵，并将 DP[i][j]更新为:
> T5【DP[I][j]= min(DP[I-1][j]，DP[i][j-1]，DP[i-1][j-1]) + 1
> 否则，
> T9

*   最后，迭代 dp[][]矩阵，找到每个 mat[i][j]的最大 dp[i][j]，等于数组中的最大元素。

下面是上述方法的实现:

## C++

```
// C++ program to find
// the length of longest
// possible square submatrix
// with maximum AND value
// from the given matrix
#include <bits/stdc++.h>
using namespace std;

// Function to calculate and
// return the length of
// square submatrix with
// maximum AND value
int MAX_value(vector<vector<int> > arr)
{
    // Extract dimensions
    int row = arr.size();
    int col = arr[0].size();

    // Auxiliary array
    int dp[row][col];

    // Initialize auxiliary array
    memset(dp, sizeof(dp), 0);

    // c: Stores the maximum
    // value in the matrix
    // p: Stores the number
    // of elements in the
    // submatrix having
    // maximum AND value
    int i = 0, j = 0;
    int c = arr[0][0], p = 0;
    int d = row;

    // Iterate over the matrix
    // to fill the auxiliary
    // matrix
    for (i = 0; i < d; i++) {
        for (j = 0; j < d; j++) {

            // Find the max element in the
            // matrix side by side
            if (c < arr[i][j]) {
                c = arr[i][j];
            }

            // Fill first row and
            // column with 1's
            if (i == 0 || j == 0) {
                dp[i][j] = 1;
            }
            else {

                // For every cell, check if
                // the elements at the left,
                // top and top left cells
                // from the current cell
                // are equal or not
                if (arr[i - 1][j - 1] == arr[i][j]
                    && arr[i - 1][j] == arr[i][j]
                    && arr[i][j - 1] == arr[i][j]) {

                    // Store the minimum possible
                    // submatrix size these
                    // elements are part of
                    dp[i][j]
                        = min(dp[i - 1][j - 1],
                            min(dp[i - 1][j],
                                dp[i][j - 1]))
                        + 1;
                }
                else {
                    // Store 1 otherwise
                    dp[i][j] = 1;
                }
            }
        }
    }

    for (i = 0; i < d; i++) {
        for (j = 0; j < d; j++) {

            // checking maximum value
            if (arr[i][j] == c) {

                // If the maximum AND
                // value occurs more
                // than once
                if (p < dp[i][j]) {

                    // Update the maximum
                    // size of submatrix
                    p = dp[i][j];
                }
            }
        }
    }
    // final output
    return p * p;
}

// Driver Program
int main()
{
    vector<vector<int> > arr
        = { { 9, 9, 3, 3, 4, 4 },
            { 9, 9, 7, 7, 7, 4 },
            { 1, 2, 7, 7, 7, 4 },
            { 4, 4, 7, 7, 7, 4 },
            { 5, 5, 1, 1, 2, 7 },
            { 2, 7, 1, 1, 4, 4 } };

    cout << MAX_value(arr) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length
// of longest possible square
// submatrix with maximum AND
// value from the given matrix
import java.util.*;

class GFG{

// Function to calculate and return
// the length of square submatrix
// with maximum AND value
static int MAX_value(int [][]arr)
{

    // Extract dimensions
    int row = arr.length;
    int col = arr[0].length;

    // Auxiliary array
    int [][]dp = new int[row][col];

    // c: Stores the maximum
    // value in the matrix
    // p: Stores the number
    // of elements in the
    // submatrix having
    // maximum AND value
    int i = 0, j = 0;
    int c = arr[0][0], p = 0;
    int d = row;

    // Iterate over the matrix
    // to fill the auxiliary
    // matrix
    for(i = 0; i < d; i++)
    {
        for(j = 0; j < d; j++)
        {

            // Find the max element in
            // the matrix side by side
            if (c < arr[i][j])
            {
                c = arr[i][j];
            }

            // Fill first row and
            // column with 1's
            if (i == 0 || j == 0)
            {
                dp[i][j] = 1;
            }
            else
            {

                // For every cell, check if the
                // elements at the left, top and
                // top left cells from the current
                // cell are equal or not
                if (arr[i - 1][j - 1] == arr[i][j] &&
                    arr[i - 1][j] == arr[i][j] &&
                    arr[i][j - 1] == arr[i][j])
                {

                    // Store the minimum possible
                    // submatrix size these
                    // elements are part of
                    dp[i][j] = Math.min(dp[i - 1][j - 1],
                               Math.min(dp[i - 1][j],
                                        dp[i][j - 1])) + 1;
                }
                else
                {

                    // Store 1 otherwise
                    dp[i][j] = 1;
                }
            }
        }
    }
    for(i = 0; i < d; i++)
    {
        for(j = 0; j < d; j++)
        {

            // Checking maximum value
            if (arr[i][j] == c)
            {

                // If the maximum AND
                // value occurs more
                // than once
                if (p < dp[i][j])
                {

                    // Update the maximum
                    // size of submatrix
                    p = dp[i][j];
                }
            }
        }
    }

    // Final output
    return p * p;
}

// Driver code
public static void main(String[] args)
{
    int [][]arr = { { 9, 9, 3, 3, 4, 4 },
                    { 9, 9, 7, 7, 7, 4 },
                    { 1, 2, 7, 7, 7, 4 },
                    { 4, 4, 7, 7, 7, 4 },
                    { 5, 5, 1, 1, 2, 7 },
                    { 2, 7, 1, 1, 4, 4 } };

    System.out.print(MAX_value(arr) + "\n");
}
}

// This code contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to find the length
# of longest possible square submatrix
# with maximum AND value from the given
# matrix

# Function to calculate and return the
# length of square submatrix with
# maximum AND value
def MAX_value(arr):

    # Extract dimensions
    row = len(arr)
    col = len(arr)

    # Auxiliary array
    # Initialize auxiliary array
    dp = [[0 for i in range(col)]
             for j in range(row)]

    # c: Stores the maximum
    # value in the matrix
    # p: Stores the number
    # of elements in the
    # submatrix having
    # maximum AND value
    i, j = 0, 0
    c, p = arr[0][0], 0
    d = row

    # Iterate over the matrix
    # to fill the auxiliary
    # matrix
    for i in range(d):
        for j in range(d):

            # Find the max element in the
            # matrix side by side
            if (c < arr[i][j]):
                c = arr[i][j]

            # Fill first row and
            # column with 1's
            if (i == 0 or j == 0):
                dp[i][j] = 1
            else:

                # For every cell, check if
                # the elements at the left,
                # top and top left cells
                # from the current cell
                # are equal or not
                if (arr[i - 1][j - 1] == arr[i][j] and
                    arr[i - 1][j] == arr[i][j] and
                    arr[i][j - 1] == arr[i][j]):

                    # Store the minimum possible
                    # submatrix size these
                    # elements are part of
                    dp[i][j] = min(dp[i - 1][j - 1],
                               min(dp[i - 1][j],
                                dp[i][j - 1])) + 1
                else:

                    # Store 1 otherwise
                    dp[i][j] = 1

    for i in range(d):
        for j in range(d):

            # Checking maximum value
            if (arr[i][j] == c):

                # If the maximum AND
                # value occurs more
                # than once
                if (p < dp[i][j]):

                    # Update the maximum
                    # size of submatrix
                    p = dp[i][j]

    # Final output
    return p * p

# Driver Code
arr = [ [ 9, 9, 3, 3, 4, 4 ],
        [ 9, 9, 7, 7, 7, 4 ],
        [ 1, 2, 7, 7, 7, 4 ],
        [ 4, 4, 7, 7, 7, 4 ],
        [ 5, 5, 1, 1, 2, 7 ],
        [ 2, 7, 1, 1, 4, 4 ]]

print(MAX_value(arr))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find the length
// of longest possible square
// submatrix with maximum AND
// value from the given matrix
using System;

class GFG{

// Function to calculate and return
// the length of square submatrix
// with maximum AND value
static int MAX_value(int [,]arr)
{

    // Extract dimensions
    int row = arr.GetLength(0);
    int col = arr.GetLength(1);

    // Auxiliary array
    int [,]dp = new int[row, col];

    // c: Stores the maximum
    // value in the matrix
    // p: Stores the number
    // of elements in the
    // submatrix having
    // maximum AND value
    int i = 0, j = 0;
    int c = arr[0, 0], p = 0;
    int d = row;

    // Iterate over the matrix
    // to fill the auxiliary
    // matrix
    for(i = 0; i < d; i++)
    {
        for(j = 0; j < d; j++)
        {

            // Find the max element in
            // the matrix side by side
            if (c < arr[i, j])
            {
                c = arr[i, j];
            }

            // Fill first row and
            // column with 1's
            if (i == 0 || j == 0)
            {
                dp[i, j] = 1;
            }
            else
            {

                // For every cell, check if the
                // elements at the left, top and
                // top left cells from the current
                // cell are equal or not
                if (arr[i - 1, j - 1] == arr[i, j] &&
                    arr[i - 1, j] == arr[i, j] &&
                    arr[i, j - 1] == arr[i, j])
                {

                    // Store the minimum possible
                    // submatrix size these
                    // elements are part of
                    dp[i, j] = Math.Min(dp[i - 1, j - 1],
                               Math.Min(dp[i - 1, j],
                                        dp[i, j - 1])) + 1;
                }
                else
                {

                    // Store 1 otherwise
                    dp[i, j] = 1;
                }
            }
        }
    }
    for(i = 0; i < d; i++)
    {
        for(j = 0; j < d; j++)
        {

            // Checking maximum value
            if (arr[i, j] == c)
            {

                // If the maximum AND
                // value occurs more
                // than once
                if (p < dp[i, j])
                {

                    // Update the maximum
                    // size of submatrix
                    p = dp[i, j];
                }
            }
        }
    }

    // Final output
    return p * p;
}

// Driver code
public static void Main(String[] args)
{
    int [,]arr = { { 9, 9, 3, 3, 4, 4 },
                   { 9, 9, 7, 7, 7, 4 },
                   { 1, 2, 7, 7, 7, 4 },
                   { 4, 4, 7, 7, 7, 4 },
                   { 5, 5, 1, 1, 2, 7 },
                   { 2, 7, 1, 1, 4, 4 } };

    Console.Write(MAX_value(arr) + "\n");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to find the length
// of longest possible square
// submatrix with maximum AND
// value from the given matrix

    // Function to calculate and return
    // the length of square submatrix
    // with maximum AND value
    function MAX_value(arr) {

        // Extract dimensions
        var row = arr.length;
        var col = arr[0].length;

        // Auxiliary array
        var dp = Array(row);
        for(var i = 0;i<row;i++)
        dp[i] = Array(col).fill(0);

        // c: Stores the maximum
        // value in the matrix
        // p: Stores the number
        // of elements in the
        // submatrix having
        // maximum AND value
        var i = 0, j = 0;
        var c = arr[0][0], p = 0;
        var d = row;

        // Iterate over the matrix
        // to fill the auxiliary
        // matrix
        for (i = 0; i < d; i++) {
            for (j = 0; j < d; j++) {

                // Find the max element in
                // the matrix side by side
                if (c < arr[i][j]) {
                    c = arr[i][j];
                }

                // Fill first row and
                // column with 1's
                if (i == 0 || j == 0) {
                    dp[i][j] = 1;
                } else {

                    // For every cell, check if the
                    // elements at the left, top and
                    // top left cells from the current
                    // cell are equal or not
                    if (arr[i - 1][j - 1] == arr[i][j] &&
                    arr[i - 1][j] == arr[i][j] &&
                    arr[i][j - 1] == arr[i][j]) {

                        // Store the minimum possible
                        // submatrix size these
                        // elements are part of
                        dp[i][j] = Math.min(dp[i - 1][j - 1],
                        Math.min(dp[i - 1][j],
                        dp[i][j - 1])) + 1;
                    } else {

                        // Store 1 otherwise
                        dp[i][j] = 1;
                    }
                }
            }
        }
        for (i = 0; i < d; i++) {
            for (j = 0; j < d; j++) {

                // Checking maximum value
                if (arr[i][j] == c) {

                    // If the maximum AND
                    // value occurs more
                    // than once
                    if (p < dp[i][j]) {

                        // Update the maximum
                        // size of submatrix
                        p = dp[i][j];
                    }
                }
            }
        }

        // Final output
        return p * p;
    }

    // Driver code

        var arr = [ [ 9, 9, 3, 3, 4, 4 ],
                    [ 9, 9, 7, 7, 7, 4 ],
                    [ 1, 2, 7, 7, 7, 4 ],
                    [ 4, 4, 7, 7, 7, 4 ],
                    [ 5, 5, 1, 1, 2, 7 ],
                    [ 2, 7, 1, 1, 4, 4 ] ];

        document.write(MAX_value(arr) + "\n");

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*