# 矩阵中差异最大的一对

> 原文:[https://www . geesforgeks . org/matrix 最大差异配对/](https://www.geeksforgeeks.org/pair-with-maximum-difference-in-a-matrix/)

给定一个有 N 行 M 列的**正整数**的 NxM 矩阵。任务是找到给定矩阵中差异最大的对。
**注**:位置(a，b)和(b，a)的对子被认为是等价的。
**示例** :

```
Input : mat[N][M] = {{1, 2, 3, 4},
                 {25, 6, 7, 8},
                 {9, 10, 11, 12},
                 {13, 14, 15, 16}}
Output : 24
Pair (25, 1) has the maximum difference

Input : mat[N][M] = {{1, 2, 3},
                 {4, 6, 7},
                 {9, 10, 5}}
Output : 9
Pair (10, 1) has the maximum difference.
```

其思想是观察到对具有最大差异的对有贡献的元素是矩阵中的最大和最小元素。所以，找出矩阵中的最大和最小元素，并返回它们之间的差值。
以下是上述方法的实现:

## C++

```
// C++ program to find with maximum
// difference in a matrix

#include <bits/stdc++.h>
using namespace std;

#define N 4 // Rows
#define M 4 // Columns

// Function to find pair with maximum
// difference in a matrix
int maxDifferencePair(int mat[N][M])
{
    int maxElement = INT_MIN; // max
    int minElement = INT_MAX; // min

    // Traverse the matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            // Find max element
            if (mat[i][j] > maxElement) {
                maxElement = mat[i][j];
            }

            // Find min element
            if (mat[i][j] < minElement) {
                minElement = mat[i][j];
            }
        }
    }

    return abs(maxElement - minElement);
}

// Driver Code
int main()
{
    // matrix
    int mat[N][M] = { { 1, 2, 3, 4 },
                      { 25, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 } };

    cout << maxDifferencePair(mat) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find with maximum
// difference in a matrix

import java.io.*;

class GFG {

static int N= 4; // Rows
static int  M = 4; // Columns

// Function to find pair with maximum
// difference in a matrix
static int maxDifferencePair(int mat[][])
{
    int maxElement = Integer.MIN_VALUE; // max
    int minElement = Integer.MAX_VALUE; // min

    // Traverse the matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            // Find max element
            if (mat[i][j] > maxElement) {
                maxElement = mat[i][j];
            }

            // Find min element
            if (mat[i][j] < minElement) {
                minElement = mat[i][j];
            }
        }
    }

    return Math.abs(maxElement - minElement);
}

// Driver Code

    public static void main (String[] args) {
        // matrix
    int mat[][] = { { 1, 2, 3, 4 },
                    { 25, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 16 } };

    System.out.println( maxDifferencePair(mat));
    }
}

// This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python3 program to find with maximum
# difference in a matrix

N = 4 # Rows
M = 4 # Columns

# Function to find pair with maximum
# difference in a matrix
def maxDifferencePair(mat):

    maxElement = -10**9 # max
    minElement = 10**9 # min

    # Traverse the matrix
    for i in range(N):
        for j in range(M):

            # Find max element
            if (mat[i][j] > maxElement):
                maxElement = mat[i][j]

            # Find min element
            if (mat[i][j] < minElement):
                minElement = mat[i][j]

    return abs(maxElement - minElement)

# Driver Code

# matrix
mat = [[ 1, 2, 3, 4 ],
       [ 25, 6, 7, 8 ],
       [ 9, 10, 11, 12 ],
       [ 13, 14, 15, 16]]

print(maxDifferencePair(mat))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# program to find with maximum
// difference in a matrix
using System;

class GFG
{
static int N = 4; // Rows
static int M = 4; // Columns

// Function to find pair with
// maximum difference in a matrix
static int maxDifferencePair(int [,]mat)
{
    int maxElement = int.MinValue; // max
    int minElement = int.MaxValue; // min

    // Traverse the matrix
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {
            // Find max element
            if (mat[i, j] > maxElement)
            {
                maxElement = mat[i, j];
            }

            // Find min element
            if (mat[i, j] < minElement)
            {
                minElement = mat[i, j];
            }
        }
    }

    return Math.Abs(maxElement -
                    minElement);
}

// Driver Code
public static void Main ()
{
    // matrix
    int [,]mat = {{ 1, 2, 3, 4 },
                  { 25, 6, 7, 8 },
                  { 9, 10, 11, 12 },
                  { 13, 14, 15, 16 }};

    Console.WriteLine( maxDifferencePair(mat));
}
}

// This code is contributed
// by inder_verma
```

## java 描述语言

```
<script>

// JavaScript program to find with maximum
// difference in a matrix

let N= 4; // Rows
let M = 4; // Columns

// Function to find pair with maximum
// difference in a matrix
function maxDifferencePair(mat)
{
    let maxElement = Number.MIN_VALUE; // max
    let minElement = Number.MAX_VALUE; // min

    // Traverse the matrix
    for (let i = 0; i < N; i++) {
        for (let j = 0; j < M; j++) {
            // Find max element
            if (mat[i][j] > maxElement) {
                maxElement = mat[i][j];
            }

            // Find min element
            if (mat[i][j] < minElement) {
                minElement = mat[i][j];
            }
        }
    }

    return Math.abs(maxElement - minElement);
}

// Driver Code
let mat = [[ 1, 2, 3, 4 ],
       [ 25, 6, 7, 8 ],
       [ 9, 10, 11, 12 ],
       [ 13, 14, 15, 16]];

document.write( maxDifferencePair(mat));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
24
```