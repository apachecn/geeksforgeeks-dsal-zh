# 统计所有平方和大于给定数 S 的子矩阵

> 原文:[https://www . geesforgeks . org/count-all-square-sub-matrix-sum-大于给定数字-s/](https://www.geeksforgeeks.org/count-all-square-sub-matrix-with-sum-greater-than-the-given-number-s/)

给定一个矩阵 **mat[][]** 和两个整数 **K** 和 **S** ，任务是计算所有 **K x K** 子矩阵，使得子矩阵中所有元素的和大于或等于 **S** 。

**示例:**

```
Input: K = 2, S = 15
mat[][] = {{1, 2, 3}, 
           {4, 5, 6},
           {7, 8, 9}} 
Output: 3
Explanation:
In the given matrix there are 3 sub-matrix
Sub-Matrix 1: (0, 1) to (1, 2)
Sum = 2 + 3 + 5 + 6 = 16
Sub-matrix 2: (1, 0) to (2, 1)
Sum = 4 + 5 + 7 + 8 = 24
Sub-matrix 3: (1, 1) to (2, 2)
Sum = 5 + 6 + 8 + 9 = 28

Input: K = 3, S = 35
arr[][] = {{1, 7, 1, 1, 1}, 
           {2, 2, 2, 2, 2}, 
           {3, 9, 6, 7, 3}, 
           {4, 3, 2, 4, 5}, 
           {5, 1, 5, 3, 1}}
Output: 5
```

**天真法:**迭代所有可能的大小子矩阵**K×K**求每个矩阵的和。如果任何子矩阵的和大于给定的和 **S** ，则计数增加 1。

**有效方法:**思想是预先计算矩阵的[前缀和，使得每个子矩阵和的和可以在 O(1)时间内计算出来。最后，迭代矩阵的所有可能位置，并使用](https://www.geeksforgeeks.org/prefix-sum-2d-array/)[包含和排除原则](https://www.geeksforgeeks.org/inclusion-exclusion-principle-and-programming-applications/)从该位置检查大小为**K×K**的子矩阵的和。如果总和大于给定的总和，则将该子矩阵的计数增加 1。

下面是上述方法的实现:

## C++

```
// C++ program to count total number
// of k x k sub matrix whose sum is
// greater than the given number S

#include <iostream>

using namespace std;

#define dim 5

// Function to create Prefix sum
// matrix from the given matrix
void createTable(int mtrx[][dim],
     int k, int p, int dp[][dim])
{
    // Store first value in table
    dp[0][0] = mtrx[0][0];

    // Initialize first row of matrix
    for (int j = 1; j < dim; j++) {
        dp[0][j] = mtrx[0][j] +
                 dp[0][j - 1];
    }

    // Initialize first column of matrix
    for (int i = 1; i < dim; i++) {
        dp[i][0] = mtrx[i][0] +
                 dp[i - 1][0];
    }

    // Initialize rest table with sum
    for (int i = 1; i < dim; i++) {
        for (int j = 1; j < dim; j++) {
            dp[i][j] = mtrx[i][j] +
               dp[i - 1][j] + dp[i][j - 1] -
                          dp[i - 1][j - 1];
        }
    }
}

// Utility Function to count the submatrix
// whose sum is greater than the S
int countSubMatrixUtil(int dp[][dim],
                        int k, int p)
{
    int count = 0;
    int subMatSum = 0;

    // Loop to iterate over all the
    // possible positions of the
    // given matrix mat[][]
    for (int i = k - 1; i < dim; i++) {
        for (int j = k - 1; j < dim;
                                j++) {
            if (i == (k - 1) || j == (k - 1)) {

                // Condition to check, if K x K
                // is first sub matrix
                if (i == (k - 1) && j == (k - 1)) {
                    subMatSum = dp[i][j];
                }
                // Condition to check sub-matrix
                // has no margin at top
                else if (i == (k - 1)) {
                    subMatSum = dp[i][j] - dp[i][j - k];
                }
                // Condition when sub matrix
                // has no margin at left
                else {
                    subMatSum = dp[i][j] - dp[i - k][j];
                }
            }
            // Condition when submatrix has
            // margin at top and left
            else {
                subMatSum = dp[i][j] - dp[i - k][j] -
                    dp[i][j - k] + dp[i - k][j - k];
            }

            // Increment count, If sub matrix
            // sum is greater than S
            if (subMatSum >= p) {
                count++;
            }
        }
    }
    return count;
}
// Function to count submatrix of
// size k x k such that sum if
// greater than or equal to S
int countSubMatrix(int mtrx[][dim], int k, int p)
{
    int dp[dim][dim];

    // For loop to initialize prefix sum
    // matrix with zero, initially
    for (int i = 0; i < dim; i++) {
        for (int j = 0; j < dim; j++) {
            dp[i][j] = 0;
        }
    }

    // Function to create the
    // prefix sum  matrix
    createTable(mtrx, k, p, dp);
    return countSubMatrixUtil(dp, k, p);
}

// Driver Code
int main()
{
    int mtrx[dim][dim] = {
        { 1, 7, 1, 1, 1 },
        { 2, 2, 2, 2, 2 },
        { 3, 9, 6, 7, 3 },
        { 4, 3, 2, 4, 5 },
        { 5, 1, 5, 3, 1 }
    };
    int k = 3;
    int p = 35;

    // Print total number of sub matrix
    cout << countSubMatrix(mtrx, k, p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count total number
// of k x k sub matrix whose sum is
// greater than the given number S
import java.util.*;

class GFG{

static final int dim = 5;

// Function to create prefix sum
// matrix from the given matrix
static void createTable(int mtrx[][],
                        int k, int p,
                        int dp[][])
{

    // Store first value in table
    dp[0][0] = mtrx[0][0];

    // Initialize first row of matrix
    for(int j = 1; j < dim; j++)
    {
        dp[0][j] = mtrx[0][j] +
                     dp[0][j - 1];
    }

    // Initialize first column of matrix
    for(int i = 1; i < dim; i++)
    {
        dp[i][0] = mtrx[i][0] +
                 dp[i - 1][0];
    }

    // Initialize rest table with sum
    for(int i = 1; i < dim; i++)
    {
        for(int j = 1; j < dim; j++)
        {
            dp[i][j] = mtrx[i][j] +
                         dp[i - 1][j] +
                         dp[i][j - 1] -
                         dp[i - 1][j - 1];
        }
    }
}

// Utility Function to count the submatrix
// whose sum is greater than the S
static int countSubMatrixUtil(int dp[][],
                              int k, int p)
{
    int count = 0;
    int subMatSum = 0;

    // Loop to iterate over all the
    // possible positions of the
    // given matrix mat[][]
    for(int i = k - 1; i < dim; i++)
    {
        for(int j = k - 1; j < dim; j++)
        {
            if (i == (k - 1) || j == (k - 1))
            {

                // Condition to check, if K x K
                // is first sub matrix
                if (i == (k - 1) && j == (k - 1))
                {
                    subMatSum = dp[i][j];
                }

                // Condition to check sub-matrix
                // has no margin at top
                else if (i == (k - 1))
                {
                    subMatSum = dp[i][j] -
                                dp[i][j - k];
                }

                // Condition when sub matrix
                // has no margin at left
                else
                {
                    subMatSum = dp[i][j] -
                                dp[i - k][j];
                }
            }

            // Condition when submatrix has
            // margin at top and left
            else
            {
                subMatSum = dp[i][j] - dp[i - k][j] -
                            dp[i][j - k] +
                            dp[i - k][j - k];
            }

            // Increment count, If sub matrix
            // sum is greater than S
            if (subMatSum >= p)
            {
                count++;
            }
        }
    }
    return count;
}

// Function to count submatrix of
// size k x k such that sum if
// greater than or equal to S
static int countSubMatrix(int mtrx[][],
                          int k, int p)
{
    int [][]dp = new int[dim][dim];

    // For loop to initialize prefix sum
    // matrix with zero, initially
    for(int i = 0; i < dim; i++)
    {
        for(int j = 0; j < dim; j++)
        {
            dp[i][j] = 0;
        }
    }

    // Function to create the
    // prefix sum matrix
    createTable(mtrx, k, p, dp);

    return countSubMatrixUtil(dp, k, p);
}

// Driver Code
public static void main(String[] args)
{
    int mtrx[][] = { { 1, 7, 1, 1, 1 },
                     { 2, 2, 2, 2, 2 },
                     { 3, 9, 6, 7, 3 },
                     { 4, 3, 2, 4, 5 },
                     { 5, 1, 5, 3, 1 } };
    int k = 3;
    int p = 35;

    // Print total number of sub matrix
    System.out.print(countSubMatrix(mtrx, k, p));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to count total number
# of k x k sub matrix whose sum is
# greater than the given number S

dim = 5

# Function to create prefix sum
# matrix from the given matrix
def createTable(mtrx, k, p, dp):

    # Store first value in table
    dp[0][0] = mtrx[0][0]

    # Initialize first row of matrix
    for j in range(1, dim):
        dp[0][j] = mtrx[0][j] + dp[0][j - 1]

    # Initialize first column of matrix
    for i in range(1, dim):
        dp[i][0] = mtrx[i][0] + dp[i - 1][0]

    # Initialize rest table with sum
    for i in range(1, dim):
        for j in range(1, dim):
            dp[i][j] = (mtrx[i][j] +
                        dp[i - 1][j] +
                        dp[i][j - 1] -
                        dp[i - 1][j - 1])

# Utility function to count the submatrix
# whose sum is greater than the S
def countSubMatrixUtil(dp, k, p):

    count = 0
    subMatSum = 0

    # Loop to iterate over all the
    # possible positions of the
    # given matrix mat[][]
    for i in range(k - 1, dim):
        for j in range(k - 1, dim, 1):
            if (i == (k - 1) or j == (k - 1)):

                # Condition to check, if K x K
                # is first sub matrix
                if (i == (k - 1) and j == (k - 1)):
                    subMatSum = dp[i][j]

                # Condition to check sub-matrix
                # has no margin at top
                elif (i == (k - 1)):
                    subMatSum = dp[i][j] - dp[i][j - k]

                # Condition when sub matrix
                # has no margin at left
                else:
                    subMatSum = dp[i][j] - dp[i - k][j]

            # Condition when submatrix has
            # margin at top and left
            else:
                subMatSum = (dp[i][j] -
                             dp[i - k][j] -
                             dp[i][j - k] +
                             dp[i - k][j - k])

            # Increment count, If sub matrix
            # sum is greater than S
            if (subMatSum >= p):
                count += 1

    return count

# Function to count submatrix of
# size k x k such that sum if
# greater than or equal to S
def countSubMatrix(mtrx, k, p):

    dp = [[0 for i in range(dim)]
             for j in range(dim)]

    # For loop to initialize prefix sum
    # matrix with zero, initially
    for i in range(dim):
        for j in range(dim):
            dp[i][j] = 0

    # Function to create the
    # prefix sum matrix
    createTable(mtrx, k, p, dp)

    return countSubMatrixUtil(dp, k, p)

# Driver Code
if __name__ == '__main__':

    mtrx = [ [ 1, 7, 1, 1, 1 ],
             [ 2, 2, 2, 2, 2 ],
             [ 3, 9, 6, 7, 3 ],
             [ 4, 3, 2, 4, 5 ],
             [ 5, 1, 5, 3, 1 ] ]
    k = 3
    p = 35

    # Print total number of sub matrix
    print(countSubMatrix(mtrx, k, p))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program to count total number
// of k x k sub matrix whose sum is
// greater than the given number S
using System;

class GFG{

static readonly int dim = 5;

// Function to create prefix sum
// matrix from the given matrix
static void createTable(int [,]mtrx,
                        int k, int p,
                        int [,]dp)
{

    // Store first value in table
    dp[0, 0] = mtrx[0, 0];

    // Initialize first row of matrix
    for(int j = 1; j < dim; j++)
    {
        dp[0, j] = mtrx[0, j] +
                     dp[0, j - 1];
    }

    // Initialize first column of matrix
    for(int i = 1; i < dim; i++)
    {
        dp[i, 0] = mtrx[i, 0] +
                 dp[i - 1, 0];
    }

    // Initialize rest table with sum
    for(int i = 1; i < dim; i++)
    {
        for(int j = 1; j < dim; j++)
        {
            dp[i, j] = mtrx[i, j] +
                         dp[i - 1, j] +
                         dp[i, j - 1] -
                         dp[i - 1, j - 1];
        }
    }
}

// Utility Function to count the submatrix
// whose sum is greater than the S
static int countSubMatrixUtil(int [,]dp,
                              int k, int p)
{
    int count = 0;
    int subMatSum = 0;

    // Loop to iterate over all the
    // possible positions of the
    // given matrix [,]mat
    for(int i = k - 1; i < dim; i++)
    {
        for(int j = k - 1; j < dim; j++)
        {
            if (i == (k - 1) || j == (k - 1))
            {

                // Condition to check, if K x K
                // is first sub matrix
                if (i == (k - 1) && j == (k - 1))
                {
                    subMatSum = dp[i, j];
                }

                // Condition to check sub-matrix
                // has no margin at top
                else if (i == (k - 1))
                {
                    subMatSum = dp[i, j] -
                                dp[i, j - k];
                }

                // Condition when sub matrix
                // has no margin at left
                else
                {
                    subMatSum = dp[i, j] -
                                dp[i - k, j];
                }
            }

            // Condition when submatrix has
            // margin at top and left
            else
            {
                subMatSum = dp[i, j] - dp[i - k, j] -
                            dp[i, j - k] +
                            dp[i - k, j - k];
            }

            // Increment count, If sub matrix
            // sum is greater than S
            if (subMatSum >= p)
            {
                count++;
            }
        }
    }
    return count;
}

// Function to count submatrix of
// size k x k such that sum if
// greater than or equal to S
static int countSubMatrix(int [,]mtrx,
                          int k, int p)
{
    int [,]dp = new int[dim, dim];

    // For loop to initialize prefix sum
    // matrix with zero, initially
    for(int i = 0; i < dim; i++)
    {
        for(int j = 0; j < dim; j++)
        {
            dp[i, j] = 0;
        }
    }

    // Function to create the
    // prefix sum matrix
    createTable(mtrx, k, p, dp);

    return countSubMatrixUtil(dp, k, p);
}

// Driver Code
public static void Main(String[] args)
{
    int [,]mtrx = { { 1, 7, 1, 1, 1 },
                    { 2, 2, 2, 2, 2 },
                    { 3, 9, 6, 7, 3 },
                    { 4, 3, 2, 4, 5 },
                    { 5, 1, 5, 3, 1 } };
    int k = 3;
    int p = 35;

    // Print total number of sub matrix
    Console.Write(countSubMatrix(mtrx, k, p));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to count total number
// of k x k sub matrix whose sum is
// greater than the given number S

var dim = 5;

// Function to create Prefix sum
// matrix from the given matrix
function createTable(mtrx,  k, p, dp)
{
    // Store first value in table
    dp[0][0] = mtrx[0][0];

    // Initialize first row of matrix
    for (var j = 1; j < dim; j++) {
        dp[0][j] = mtrx[0][j] +
                 dp[0][j - 1];
    }

    // Initialize first column of matrix
    for (var i = 1; i < dim; i++) {
        dp[i][0] = mtrx[i][0] +
                 dp[i - 1][0];
    }

    // Initialize rest table with sum
    for (var i = 1; i < dim; i++) {
        for (var j = 1; j < dim; j++) {
            dp[i][j] = mtrx[i][j] +
               dp[i - 1][j] + dp[i][j - 1] -
                          dp[i - 1][j - 1];
        }
    }
}

// Utility Function to count the submatrix
// whose sum is greater than the S
function countSubMatrixUtil(dp, k, p)
{
    var count = 0;
    var subMatSum = 0;

    // Loop to iterate over all the
    // possible positions of the
    // given matrix mat[][]
    for (var i = k - 1; i < dim; i++) {
        for (var j = k - 1; j < dim;
                                j++) {
            if (i == (k - 1) || j == (k - 1)) {

                // Condition to check, if K x K
                // is first sub matrix
                if (i == (k - 1) && j == (k - 1)) {
                    subMatSum = dp[i][j];
                }
                // Condition to check sub-matrix
                // has no margin at top
                else if (i == (k - 1)) {
                    subMatSum = dp[i][j] - dp[i][j - k];
                }
                // Condition when sub matrix
                // has no margin at left
                else {
                    subMatSum = dp[i][j] - dp[i - k][j];
                }
            }
            // Condition when submatrix has
            // margin at top and left
            else {
                subMatSum = dp[i][j] - dp[i - k][j] -
                    dp[i][j - k] + dp[i - k][j - k];
            }

            // Increment count, If sub matrix
            // sum is greater than S
            if (subMatSum >= p) {
                count++;
            }
        }
    }
    return count;
}
// Function to count submatrix of
// size k x k such that sum if
// greater than or equal to S
function countSubMatrix(mtrx, k, p)
{
    var dp = Array.from(Array(dim), ()=>Array(dim));

    // For loop to initialize prefix sum
    // matrix with zero, initially
    for (var i = 0; i < dim; i++) {
        for (var j = 0; j < dim; j++) {
            dp[i][j] = 0;
        }
    }

    // Function to create the
    // prefix sum  matrix
    createTable(mtrx, k, p, dp);
    return countSubMatrixUtil(dp, k, p);
}

// Driver Code
var mtrx = [
    [ 1, 7, 1, 1, 1 ],
    [ 2, 2, 2, 2, 2 ],
    [ 3, 9, 6, 7, 3 ],
    [ 4, 3, 2, 4, 5 ],
    [ 5, 1, 5, 3, 1 ]
];
var k = 3;
var p = 35;
// Print total number of sub matrix
document.write( countSubMatrix(mtrx, k, p));

</script>
```

**Output:** 

```
5
```

**时间复杂度:**O(M * N)
T3】辅助空间: O(M * N)