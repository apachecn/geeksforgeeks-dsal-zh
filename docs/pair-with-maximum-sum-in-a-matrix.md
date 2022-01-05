# 与矩阵中的最大和配对

> 原文:[https://www . geeksforgeeks . org/matrix 中最大和配对/](https://www.geeksforgeeks.org/pair-with-maximum-sum-in-a-matrix/)

给定一个有 N 行 M 列正整数的 NxM 矩阵。任务是求矩阵中和最大的对的和。
**例** :

```
Input : mat[N][M] = {{1, 2, 3, 4},
                 {25, 6, 7, 8},
                 {9, 10, 11, 12},
                 {13, 14, 15, 16}}
Output : 41
Pair (25, 16) has the maximum sum

Input : mat[N][M] = {{1, 2, 3},
                 {4, 6, 7},
                 {9, 10, 5}}
Output : 19
```

**简单方法**:简单的方法是遍历矩阵两次，找到第一个最大值和第二个最大值元素，返回它们的和。
**更好的方法**:更好的方法是在矩阵的单次遍历中找到第一个和第二个最大值。

```
1) Initialize two variables first and second to INT_MIN as,
   first = second = INT_MIN
2) Start traversing the matrix,
   a) If the current element in array say mat[i][j] is greater
      than first. Then update first and second as,
      second = first
      first = mat[i][j]
   b) If the current element is in between first and second,
      then update second to store the value of current variable as
      second = mat[i][j]
3) Return sum of both first and second maximum.
```

以下是上述方法的实现:

## C++

```
// C++ program to find maximum sum
// pair in a matrix

#include <bits/stdc++.h>
using namespace std;

#define N 4 // Rows
#define M 4 // Columns

// Function to find maximum sum
// pair from matrix
int maxSumPair(int mat[N][M])
{
    int max1 = INT_MIN; // First max
    int max2 = INT_MIN; // Second max

    // Traverse the matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            if (mat[i][j] > max1) {
                max2 = max1; // second max = first max
                max1 = mat[i][j]; // first max = current
            }
            // If second max is between current element
            // and first max
            else if (mat[i][j] > max2 && mat[i][j] <= max1) {
                max2 = mat[i][j];
            }
        }
    }

    return max1 + max2;
}

// Driver Code
int main()
{

    // matrix
    int mat[N][M] = { { 1, 2, 3, 4 },
                      { 25, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 } };

    cout << maxSumPair(mat) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum sum
// pair in a matrix
import java.io.*;

class GFG {

static int  N = 4; // Rows
static int M = 4; // Columns

// Function to find maximum sum
// pair from matrix
static int maxSumPair(int [][]mat)
{
    int max1 = Integer.MIN_VALUE; // First max
    int max2 = Integer.MIN_VALUE; // Second max

    // Traverse the matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            if (mat[i][j] > max1) {
                max2 = max1; // second max = first max
                max1 = mat[i][j]; // first max = current
            }
            // If second max is between current element
            // and first max
            else if (mat[i][j] > max2 && mat[i][j] <= max1) {
                max2 = mat[i][j];
            }
        }
    }

    return max1 + max2;
}

// Driver Code

    public static void main (String[] args) {
            // matrix
    int [][]mat = { { 1, 2, 3, 4 },
                    { 25, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 16 } };

    System.out.println(maxSumPair(mat));
    }
}
// This code is contributed
// by shs
```

## 蟒蛇 3

```
# Python 3 program to find maximum sum
# pair in a matrix
import sys

N = 4 # Rows
M = 4 # Columns

# Function to find maximum sum
# pair from matrix
def maxSumPair(mat):

    max1 = -sys.maxsize - 1 # First max
    max2 = -sys.maxsize - 1 # Second max

    # Traverse the matrix
    for i in range(0, N):
        for j in range (0, M):
            if (mat[i][j] > max1):
                max2 = max1 # second max = first max
                max1 = mat[i][j] # first max = current

            # If second max is between current
            # element and first max
            elif (mat[i][j] > max2 and
                  mat[i][j] <= max1):
                max2 = mat[i][j]

    return max1 + max2

# Driver Code

# matrix
mat = [ [1, 2, 3, 4 ],
        [25, 6, 7, 8 ],
        [9, 10, 11, 12 ],
        [13, 14, 15, 16 ]]

print(maxSumPair(mat))

# This code is contributed
# by ihritik
```

## C#

```
// C# program to find maximum sum
// pair in a matrix
using System;
public class GFG {

static int  N = 4; // Rows
static int M = 4; // Columns

// Function to find maximum sum
// pair from matrix
static int maxSumPair(int [,]mat)
{
    int max1 = int.MinValue; // First max
    int max2 = int.MinValue; // Second max

    // Traverse the matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            if (mat[i,j] > max1) {
                max2 = max1; // second max = first max
                max1 = mat[i,j]; // first max = current
            }
            // If second max is between current element
            // and first max
            else if (mat[i,j] > max2 && mat[i,j] <= max1) {
                max2 = mat[i,j];
            }
        }
    }

    return max1 + max2;
}

// Driver Code

    public static void Main () {
            // matrix
    int [,]mat = { { 1, 2, 3, 4 },
                    { 25, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 16 } };

    Console.WriteLine(maxSumPair(mat));
    }
}
// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum sum
// pair in a $matrix

$N = 4; // Rows
$M = 4; // Columns

// Function to find maximum sum
// pair from $matrix
function maxSumPair($mat)
{
    global $N;
    global $M;
    $max1 = PHP_INT_MIN; // First max
    $max2 = PHP_INT_MIN; // Second max

    // Traverse the $matrix
    for ($i = 0; $i < $N; $i++)
    {
        for ($j = 0; $j < $M; $j++)
        {
            if ($mat[$i][$j] > $max1)
            {
                $max2 = $max1; // second max = first max
                $max1 = $mat[$i][$j]; // first max = current
            }

            // If second max is between current
            // element and first max
            else if ($mat[$i][$j] > $max2 &&
                     $mat[$i][$j] <= $max1)
            {
                $max2 = $mat[$i][$j];
            }
        }
    }

    return $max1 + $max2;
}

// Driver Code

// matrix
$mat = array(array(1, 2, 3, 4 ),
             array(25, 6, 7, 8 ),
             array(9, 10, 11, 12 ),
             array(13, 14, 15, 16 ));

echo maxSumPair($mat);

// This code is contributed
// by ihritik
?>
```

## java 描述语言

```
<script>

// JavaScript program to find maximum sum
// pair in a matrix

var N = 4; // Rows
var M = 4; // Columns

// Function to find maximum sum
// pair from matrix
function maxSumPair(mat)
{
    var max1 = -1000000000; // First max
    var max2 = -1000000000; // Second max

    // Traverse the matrix
    for (var i = 0; i < N; i++) {
        for (var j = 0; j < M; j++) {
            if (mat[i][j] > max1) {
                max2 = max1; // second max = first max
                max1 = mat[i][j]; // first max = current
            }
            // If second max is between current element
            // and first max
            else if (mat[i][j] > max2 && mat[i][j] <= max1) {
                max2 = mat[i][j];
            }
        }
    }

    return max1 + max2;
}

// Driver Code

// matrix
var mat = [ [ 1, 2, 3, 4 ],
                [ 25, 6, 7, 8 ],
                [ 9, 10, 11, 12 ],
                [ 13, 14, 15, 16 ] ];

document.write(maxSumPair(mat));

</script>
```

**Output:** 

```
41
```