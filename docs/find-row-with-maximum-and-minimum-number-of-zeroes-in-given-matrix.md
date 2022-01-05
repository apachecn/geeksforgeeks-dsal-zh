# 在给定矩阵中找到具有最大和最小零个数的行

> 原文:[https://www . geeksforgeeks . org/find-给定矩阵中具有最大和最小零位数的行/](https://www.geeksforgeeks.org/find-row-with-maximum-and-minimum-number-of-zeroes-in-given-matrix/)

给定一个只包含 0 和 1 的 2D 矩阵，其中每行都被排序。任务是找到最大 0 数的行和最小 0 数的行。
**例:**

> **输入:** mat[][] = {
> {0，1，1，1}，
> {0，0，1，1}，
> {1，1，1，1}，
> {0，0，0，0}}
> **输出:**
> 最小零行:3
> 最大零行:4
> **输入:**mat[[]= {
> { 0，1，1，1 } }

**简单方法:**一个简单的方法是对矩阵进行逐行遍历，统计每行的 0 个数，并与 max 和 min 进行比较。最后，返回最大值为 0、最小值为 0 的行的索引。该方法的时间复杂度为 O(M*N)，其中 M 是矩阵中的行数，N 是矩阵中的列数。
**高效的方法:**由于每行都是排序的，我们可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到每行 0 的个数。想法是在每行中找到第一个实例 1 的索引。
该行 0 的计数为:

*   如果行中存在 1，则考虑从零开始的索引，0 的计数将等于行中第一个 1 的索引。
*   如果行中不存在 1，则 0 的计数将为 N，即矩阵中的列总数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define R 4
#define C 4

// Function to find the index of first 1
// in the binary array arr[]
int first(bool arr[], int low, int high)
{
    if (high >= low) {

        // Get the middle index
        int mid = low + (high - low) / 2;

        // Check if the element at middle index is first 1
        if ((mid == 0 || arr[mid - 1] == 0) && arr[mid] == 1)
            return mid;

        // If the element is 0, recur for right side
        else if (arr[mid] == 0)
            return first(arr, (mid + 1), high);

        // If element is not first 1, recur for left side
        else
            return first(arr, low, (mid - 1));
    }
    return -1;
}

// Function to print rows with maximum
// and minimum number of zeroes
void rowWith0s(bool mat[R][C])
{
    // Initialize max values
    int max_row_index = 0, max = INT_MIN;

    // Initialize min values
    int min_row_index = 0, min = INT_MAX;

    // Traverse for each row and count number of 0s
    // by finding the index of first 1
    int i, index;

    for (i = 0; i < R; i++) {
        index = first(mat[i], 0, C - 1);

        int cntZeroes = 0;

        // If index = -1, that is there is no 1
        // in the row, count of zeroes will be C
        if (index == -1) {
            cntZeroes = C;
        }

        // Else, count of zeroes will be index
        // of first 1
        else {
            cntZeroes = index;
        }

        // Find max row index
        if (max < cntZeroes) {
            max = cntZeroes;
            max_row_index = i;
        }

        // Find min row index
        if (min > cntZeroes) {
            min = cntZeroes;
            min_row_index = i;
        }
    }

    cout << "Row with min 0s: " << min_row_index + 1;
    cout << "\nRow with max 0s: " << max_row_index + 1;
}

// Driver code
int main()
{
    bool mat[R][C] = { { 0, 0, 0, 1 },
                       { 0, 1, 1, 1 },
                       { 1, 1, 1, 1 },
                       { 0, 0, 0, 0 } };

    rowWith0s(mat);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

static int R = 4;
static int C = 4;

// Function to find the index of first 1
// in the binary array arr[]
static int first(int arr[], int low, int high)
{
    if (high >= low)
    {

        // Get the middle index
        int mid = low + (high - low) / 2;

        // Check if the element at middle index is first 1
        if ((mid == 0 || arr[mid - 1] == 0) && arr[mid] == 1)
            return mid;

        // If the element is 0, recur for right side
        else if (arr[mid] == 0)
            return first(arr, (mid + 1), high);

        // If element is not first 1, recur for left side
        else
            return first(arr, low, (mid - 1));
    }
    return -1;
}

// Function to print rows with maximum
// and minimum number of zeroes
static void rowWith0s(int mat[][])
{
    // Initialize max values
    int max_row_index = 0, max = Integer.MIN_VALUE;

    // Initialize min values
    int min_row_index = 0, min = Integer.MAX_VALUE;

    // Traverse for each row and count number of 0s
    // by finding the index of first 1
    int i, index;

    for (i = 0; i < R; i++)
    {
        index = first(mat[i], 0, C - 1);

        int cntZeroes = 0;

        // If index = -1, that is there is no 1
        // in the row, count of zeroes will be C
        if (index == -1)
        {
            cntZeroes = C;
        }

        // Else, count of zeroes will be index
        // of first 1
        else
        {
            cntZeroes = index;
        }

        // Find max row index
        if (max < cntZeroes)
        {
            max = cntZeroes;
            max_row_index = i;
        }

        // Find min row index
        if (min > cntZeroes)
        {
            min = cntZeroes;
            min_row_index = i;
        }
    }

        System.out.println ("Row with min 0s: " + (min_row_index + 1));
        System.out.println ("Row with max 0s: " + (max_row_index + 1));
}

// Driver code
public static void main (String[] args)
{

    int mat[][] = { { 0, 0, 0, 1 },
                    { 0, 1, 1, 1 },
                    { 1, 1, 1, 1 },
                    { 0, 0, 0, 0 } };

    rowWith0s(mat);

}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

import sys

R = 4
C = 4

# Function to find the index of first 1
# in the binary array arr[]
def first(arr, low, high) :

    if (high >= low) :

        # Get the middle index
        mid = low + (high - low) // 2;

        # Check if the element at middle index is first 1
        if ((mid == 0 or arr[mid - 1] == 0) and arr[mid] == 1) :
            return mid;

        # If the element is 0, recur for right side
        elif (arr[mid] == 0) :
            return first(arr, (mid + 1), high);

        # If element is not first 1, recur for left side
        else :
            return first(arr, low, (mid - 1));

    return -1;

# Function to print rows with maximum
# and minimum number of zeroes
def rowWith0s(mat) :

    # Initialize max values
    row_index = 0; max = -(sys.maxsize - 1);

    # Initialize min values
    min_row_index = 0; min = sys.maxsize;

    # Traverse for each row and count number of 0s
    # by finding the index of first 1

    for i in range(R) :

        index = first(mat[i], 0, C - 1);

        cntZeroes = 0;

        # If index = -1, that is there is no 1
        # in the row, count of zeroes will be C
        if (index == -1) :
            cntZeroes = C;

        # Else, count of zeroes will be index
        # of first 1
        else :
            cntZeroes = index;

        # Find max row index
        if (max < cntZeroes) :
            max = cntZeroes;
            max_row_index = i;

        # Find min row index
        if (min > cntZeroes) :
            min = cntZeroes;
            min_row_index = i;

    print("Row with min 0s:",min_row_index + 1);
    print("Row with max 0s:", max_row_index + 1);

# Driver code
if __name__ == "__main__" :

    mat = [
            [ 0, 0, 0, 1 ],
            [ 0, 1, 1, 1 ],
            [ 1, 1, 1, 1 ],
            [ 0, 0, 0, 0 ]
        ];

    rowWith0s(mat);

    # This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;    

class GFG
{

static int R = 4;
static int C = 4;

// Function to find the index of first 1
// in the binary array arr[]
static int first(int []arr, int low, int high)
{
    if (high >= low)
    {

        // Get the middle index
        int mid = low + (high - low) / 2;

        // Check if the element at middle index is first 1
        if ((mid == 0 || arr[mid - 1] == 0) && arr[mid] == 1)
            return mid;

        // If the element is 0, recur for right side
        else if (arr[mid] == 0)
            return first(arr, (mid + 1), high);

        // If element is not first 1, recur for left side
        else
            return first(arr, low, (mid - 1));
    }
    return -1;
}

// Function to print rows with maximum
// and minimum number of zeroes
static void rowWith0s(int [,]mat)
{
    // Initialize max values
    int max_row_index = 0, max = int.MinValue;

    // Initialize min values
    int min_row_index = 0, min = int.MaxValue;

    // Traverse for each row and count number of 0s
    // by finding the index of first 1
    int i, index;

    for (i = 0; i < R; i++)
    {
        index = first(GetRow(mat,i), 0, C - 1);

        int cntZeroes = 0;

        // If index = -1, that is there is no 1
        // in the row, count of zeroes will be C
        if (index == -1)
        {
            cntZeroes = C;
        }

        // Else, count of zeroes will be index
        // of first 1
        else
        {
            cntZeroes = index;
        }

        // Find max row index
        if (max < cntZeroes)
        {
            max = cntZeroes;
            max_row_index = i;
        }

        // Find min row index
        if (min > cntZeroes)
        {
            min = cntZeroes;
            min_row_index = i;
        }
    }

        Console.WriteLine ("Row with min 0s: " + (min_row_index + 1));
        Console.WriteLine ("Row with max 0s: " + (max_row_index + 1));
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
public static void Main (String[] args)
{

    int [,]mat = { { 0, 0, 0, 1 },
                    { 0, 1, 1, 1 },
                    { 1, 1, 1, 1 },
                    { 0, 0, 0, 0 } };

    rowWith0s(mat);

}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

var R = 4;
var C = 4;

// Function to find the index of first 1
// in the binary array arr
function first(arr , low , high)
{
    if (high >= low)
    {

        // Get the middle index
        var mid = low + parseInt((high - low) / 2);

        // Check if the element at middle
        // index is first 1
        if ((mid == 0 || arr[mid - 1] == 0) &&
        arr[mid] == 1)
            return mid;

        // If the element is 0, recur for right side
        else if (arr[mid] == 0)
            return first(arr, (mid + 1), high);

        // If element is not first 1,
        // recur for left side
        else
            return first(arr, low, (mid - 1));
    }
    return -1;
}

// Function to prvar rows with maximum
// and minimum number of zeroes
function rowWith0s(mat)
{
    // Initialize max values
    var max_row_index = 0, max = Number.MIN_VALUE;

    // Initialize min values
    var min_row_index = 0, min = Number.MAX_VALUE;

    // Traverse for each row and count number of 0s
    // by finding the index of first 1
    var i, index;

    for (i = 0; i < R; i++)
    {
        index = first(mat[i], 0, C - 1);

        var cntZeroes = 0;

        // If index = -1, that is there is no 1
        // in the row, count of zeroes will be C
        if (index == -1)
        {
            cntZeroes = C;
        }

        // Else, count of zeroes will be index
        // of first 1
        else
        {
            cntZeroes = index;
        }

        // Find max row index
        if (max < cntZeroes)
        {
            max = cntZeroes;
            max_row_index = i;
        }

        // Find min row index
        if (min > cntZeroes)
        {
            min = cntZeroes;
            min_row_index = i;
        }
    }

        document.write("Row with min 0s: " +
        (min_row_index + 1)+"<br/>");
        document.write("Row with max 0s: " +
        (max_row_index + 1));
}

// Driver code

    var mat = [ [ 0, 0, 0, 1 ],
                [ 0, 1, 1, 1 ],
                [ 1, 1, 1, 1 ],
                [ 0, 0, 0, 0 ] ];

    rowWith0s(mat);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
Row with min 0s: 3
Row with max 0s: 4
```