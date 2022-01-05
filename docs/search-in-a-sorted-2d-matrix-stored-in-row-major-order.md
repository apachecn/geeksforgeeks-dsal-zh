# 在排序的 2D 矩阵中搜索(以行主顺序存储)

> 原文:[https://www . geesforgeks . org/search-in-a-sorted-2d-matrix-stored-in-row-major-order/](https://www.geeksforgeeks.org/search-in-a-sorted-2d-matrix-stored-in-row-major-order/)

给定一个整数“K”和一个按行排序的二维矩阵，即该矩阵具有以下性质:

*   每行中的整数从左到右排序。
*   每行的第一个整数大于前一行的最后一个整数。

任务是找出整数“K”是否存在于矩阵中。如果存在，则打印“找到”，否则打印“未找到”。
**例:**

```
Input: mat = {
  {1,   3,  5,  7},
  {10, 11, 16, 20},
  {23, 30, 34, 50}}
  K = 3
Output: Found

Input: mat = {
  {1,   3,  5,  7},
  {10, 11, 16, 20},
  {23, 30, 34, 50}}
  K = 13
Output: Not found
```

我们已经讨论了排序矩阵中[搜索元素的一个实现。这篇文章提供了一个更好的实现。
**进场:**思路是用各个击破的方式解决这个问题。](https://www.geeksforgeeks.org/search-element-sorted-matrix/) 

*   首先应用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到特定的行，即“K”位于该行的第一个和最后一个元素之间。
*   然后在该行上应用简单的二分搜索法来查找该行中是否存在“K”。

以下是上述方法的实现:

## C++

```
// C++ program to find whether
// a given element is present
// in the given 2-D matrix
#include <bits/stdc++.h>
using namespace std;

#define M 3
#define N 4

// Basic binary search to
// find an element in a 1-D array
bool binarySearch1D(int arr[], int K)
{
    int low = 0;
    int high = N - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;

        // if element found return true
        if (arr[mid] == K)
            return true;

        // if middle less than K then
        // skip the left part of the
        // array else skip the right part
        if (arr[mid] < K)
            low = mid + 1;
        else
            high = mid - 1;
    }

    // if not found return false
    return false;
}

// Function to search an element
// in a matrix based on
// Divide and conquer approach
bool searchMatrix(int matrix[M][N], int K)
{
    int low = 0;
    int high = M - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;

        // if the element lies in the range
        // of this row then call
        // 1-D binary search on this row
        if (K >= matrix[mid][0]
            && K <= matrix[mid][N - 1])
            return binarySearch1D(matrix[mid], K);

        // if the element is less then the
        // starting element of that row then
        // search in upper rows else search
        // in the lower rows
        if (K < matrix[mid][0])
            high = mid - 1;
        else
            low = mid + 1;
    }

    // if not found
    return false;
}

// Driver code
int main()
{
    int matrix[M][N] = { { 1, 3, 5, 7 },
                         { 10, 11, 16, 20 },
                         { 23, 30, 34, 50 } };
    int K = 3;
    if (searchMatrix(matrix, K))
        cout << "Found" << endl;
    else
        cout << "Not found" << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find whether
// a given element is present
// in the given 2-D matrix

public class GFG {

    static final int M = 3;
    static final int N = 4;

    // Basic binary search to
    // find an element in a 1-D array
    static boolean binarySearch1D(int arr[], int K)
    {
        int low = 0;
        int high = N - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;

            // if element found return true
            if (arr[mid] == K) {
                return true;
            }

            // if middle less than K then
            // skip the left part of the
            // array else skip the right part
            if (arr[mid] < K) {
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }

        // if not found return false
        return false;
    }

    // Function to search an element
    // in a matrix based on
    // Divide and conquer approach
    static boolean searchMatrix(int matrix[][], int K)
    {
        int low = 0;
        int high = M - 1;
        while (low <= high) {
            int mid = low + (high - low) / 2;

            // if the element lies in the range
            // of this row then call
            // 1-D binary search on this row
            if (K >= matrix[mid][0]
                && K <= matrix[mid][N - 1]) {
                return binarySearch1D(matrix[mid], K);
            }

            // if the element is less then the
            // starting element of that row then
            // search in upper rows else search
            // in the lower rows
            if (K < matrix[mid][0]) {
                high = mid - 1;
            }
            else {
                low = mid + 1;
            }
        }

        // if not found
        return false;
    }

    // Driver code
    public static void main(String args[])
    {
        int matrix[][] = { { 1, 3, 5, 7 },
                           { 10, 11, 16, 20 },
                           { 23, 30, 34, 50 } };
        int K = 3;
        if (searchMatrix(matrix, K)) {
            System.out.println("Found");
        }
        else {
            System.out.println("Not found");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find whether a given
# element is present in the given 2-D matrix

M = 3
N = 4

# Basic binary search to find an element
# in a 1-D array
def binarySearch1D(arr, K):
    low = 0
    high = N - 1
    while (low <= high):
        mid = low + int((high - low) / 2)

        # if element found return true
        if (arr[mid] == K):
            return True

        # if middle less than K then skip
        # the left part of the array
        # else skip the right part
        if (arr[mid] < K):
            low = mid + 1
        else:
            high = mid - 1

    # if not found return false
    return False

# Function to search an element in a matrix
# based on Divide and conquer approach
def searchMatrix(matrix, K):
    low = 0
    high = M - 1
    while (low <= high):
        mid = low + int((high - low) / 2)

        # if the element lies in the range
        # of this row then call
        # 1-D binary search on this row
        if (K >= matrix[mid][0] and
            K <= matrix[mid][N - 1]):
            return binarySearch1D(matrix[mid], K)

        # if the element is less then the
        # starting element of that row then
        # search in upper rows else search
        # in the lower rows
        if (K < matrix[mid][0]):
            high = mid - 1
        else:
            low = mid + 1

    # if not found
    return False

# Driver code
if __name__ == '__main__':
    matrix = [[1, 3, 5, 7],
              [10, 11, 16, 20],
              [23, 30, 34, 50]]
    K = 3
    if (searchMatrix(matrix, K)):
        print("Found")
    else:
        print("Not found")

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to find whether
// a given element is present
// in the given 2-D matrix
using System;

class GFG
{

    static int M = 3;
    static int N = 4;

    // Basic binary search to
    // find an element in a 1-D array
    static bool binarySearch1D(int []arr, int K)
    {
        int low = 0;
        int high = N - 1;
        while (low <= high)
        {
            int mid = low + (high - low) / 2;

            // if element found return true
            if (arr[mid] == K)
            {
                return true;
            }

            // if middle less than K then
            // skip the left part of the
            // array else skip the right part
            if (arr[mid] < K)
            {
                low = mid + 1;
            }
            else
            {
                high = mid - 1;
            }
        }

        // if not found return false
        return false;
    }

    // Function to search an element
    // in a matrix based on
    // Divide and conquer approach
    static bool searchMatrix(int [,]matrix, int K)
    {
        int low = 0;
        int high = M - 1;
        while (low <= high)
        {
            int mid = low + (high - low) / 2;

            // if the element lies in the range
            // of this row then call
            // 1-D binary search on this row
            if (K >= matrix[mid,0]
                && K <= matrix[mid,N - 1])
            {
                return binarySearch1D(GetRow(matrix,mid), K);
            }

            // if the element is less then the
            // starting element of that row then
            // search in upper rows else search
            // in the lower rows
            if (K < matrix[mid,0])
            {
                high = mid - 1;
            }
            else
            {
                low = mid + 1;
            }
        }

        // if not found
        return false;
    }
    public static int[] GetRow(int[,] matrix, int row)
    {
        var rowLength = matrix.GetLength(1);
        var rowVector = new int[rowLength];

        for (var i = 0; i < rowLength; i++)
        rowVector[i] = matrix[row, i];

        return rowVector;
    }

    // Driver code
    public static void Main(String []args)
    {
        int [,]matrix = { { 1, 3, 5, 7 },
                        { 10, 11, 16, 20 },
                        { 23, 30, 34, 50 } };
        int K = 3;
        if (searchMatrix(matrix, K)) {
            Console.WriteLine("Found");
        }
        else {
        Console.WriteLine("Not found");
        }
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php program to find whether a given
// element is present in the given 2-D matrix
$M = 3;
$N = 4;

// Basic binary search to find an element
// in a 1-D array
function binarySearch1D($arr, $K)
{

    $low = 0;
    $high = $GLOBALS['N'] - 1;
    while ($low <= $high) {
        $mid = $low + (int)($high - $low) / 2;

// if element found return true
        if ($arr[$mid] == $K)
            return True;

// if middle less than K then skip
// the left part of the array
// else skip the right part
        if ($arr[$mid] < $K)
            $low = $mid + 1;
        else
            $high = $mid - 1;
    }
// if not found return false
    return False;
}

// Function to search an element in a matrix
// based on Divide and conquer approach
function searchMatrix($matrix, $K)
{

    $low = 0;
    $high = $GLOBALS['M']-1;
    while ($low <= $high)
    {
        $mid = $low + (int)($high - $low) / 2;

// if the element lies in the range
// of this row then call
// 1-D binary search on this row
        if ($K >= $matrix[$mid][0] && $K <= $matrix[$mid][$GLOBALS['N'] - 1])
            return binarySearch1D($matrix[$mid], $K);

// if the element is less then the
// starting element of that row then
// search in upper rows else search
// in the lower rows
        if ($K < $matrix[$mid][0])
            $high = $mid - 1;
        else
            $low = $mid + 1;
    }

// if not found
    return False;
}

// Driver code

$matrix = array([1, 3, 5, 7],
                [10, 11, 16, 20],
                [23, 30, 34, 50]);
$K = 3;
$M = 3;
$N = 4;
if (searchMatrix($matrix, $K))
echo "Found";
else
echo "Not found";

// This code is contributed by
// Srathore
?>
```

## java 描述语言

```
<script>

// Javascript program to find whether
// a given element is present
// in the given 2-D matrix

var M = 3;
var N = 4;

// Basic binary search to
// find an element in a 1-D array
function binarySearch1D(arr, K)
{
    var low = 0;
    var high = N - 1;
    while (low <= high) {
        var mid = low + parseInt((high - low) / 2);

        // if element found return true
        if (arr[mid] == K)
            return true;

        // if middle less than K then
        // skip the left part of the
        // array else skip the right part
        if (arr[mid] < K)
            low = mid + 1;
        else
            high = mid - 1;
    }

    // if not found return false
    return false;
}

// Function to search an element
// in a matrix based on
// Divide and conquer approach
function searchMatrix(matrix, K)
{
    var low = 0;
    var high = M - 1;
    while (low <= high) {
        var mid = low + parseInt((high - low) / 2);

        // if the element lies in the range
        // of this row then call
        // 1-D binary search on this row
        if (K >= matrix[mid][0]
            && K <= matrix[mid][N - 1])
            return binarySearch1D(matrix[mid], K);

        // if the element is less then the
        // starting element of that row then
        // search in upper rows else search
        // in the lower rows
        if (K < matrix[mid][0])
            high = mid - 1;
        else
            low = mid + 1;
    }

    // if not found
    return false;
}

// Driver code
var matrix = [ [ 1, 3, 5, 7 ],
                     [ 10, 11, 16, 20 ],
                     [ 23, 30, 34, 50 ] ];
var K = 3;
if (searchMatrix(matrix, K))
    document.write( "Found" );
else
    document.write( "Not found" );

</script>
```

**Output:** 

```
Found
```