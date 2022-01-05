# 按行排序的二进制矩阵中最左边至少有一个 1 的列

> 原文:[https://www . geeksforgeeks . org/最左边一列至少一行一位排序二进制矩阵/](https://www.geeksforgeeks.org/leftmost-column-with-atleast-one-1-in-a-row-wise-sorted-binary-matrix/)

给定一个包含 0 和 1 的二进制矩阵 **mat[][]** ，矩阵的每一行按非递减顺序排序，任务是找到矩阵最左边的列，其中至少有一个 1。
**注:**如无此列返回-1。
**示例:**

```
Input: 
mat[2][2] = { {0, 0},
              {1, 1} }
Output: 1
Explanation: 
The 1st column of the
matrix contains atleast a 1.

Input: 
mat[2][2] = {{0, 0},
             {0, 0}}
Output: -1
Explanation:
There is no such column which 
contains atleast one 1.
```

**方法:**想法是迭代矩阵的所有行，并在第一次出现该行中的 1 时，[二分搜索法](https://www.geeksforgeeks.org/binary-search/)遍历它们。矩阵行中第一个 1 出现的最少次数将是问题的理想解决方案。
以下是上述方法的实施:

## C++

```
// C++ implementation to find the
// Leftmost Column with atleast a
// 1 in a sorted binary matrix

#include <bits/stdc++.h>

#define N 3
using namespace std;

// Function to search for the
// leftmost column of the matrix
// with atleast a 1 in sorted
// binary matrix
int search(int mat[][3], int n, int m)
{
    int i, a = INT_MAX;

    // Loop to iterate over all the
    // rows of the matrix
    for (i = 0; i < n; i++) {
        int low = 0;
        int high = m - 1;
        int mid;
        int ans = INT_MAX;

        // Binary Search to find the
        // leftmost occurence of the 1
        while (low <= high) {
            mid = (low + high) / 2;

            // Condition if the column
            // contains the 1 at this
            // position of matrix
            if (mat[i][mid] == 1) {

                if (mid == 0) {
                    ans = 0;
                    break;
                }
                else if (mat[i][mid - 1] == 0) {
                    ans = mid;
                    break;
                }
            }

            if (mat[i][mid] == 1)
                high = mid - 1;
            else
                low = mid + 1;
        }

        // If there is a better solution
        // then update the answer
        if (ans < a)
            a = ans;
    }

    // Condition if the solution
    // doesn't exist in the matrix
    if (a == INT_MAX)
        return -1;
    return a+1;
}

// Driver Code
int main()
{
    int mat[3][3] = { 0, 0, 0,
                    0, 0, 1,
                    0, 1, 1 };
    cout << search(mat, 3, 3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Leftmost Column with atleast a
// 1 in a sorted binary matrix
import java.util.*;

class GFG{

static final int N = 3;

// Function to search for the
// leftmost column of the matrix
// with atleast a 1 in sorted
// binary matrix
static int search(int mat[][], int n, int m)
{
    int i, a = Integer.MAX_VALUE;

    // Loop to iterate over all the
    // rows of the matrix
    for(i = 0; i < n; i++)
    {
       int low = 0;
       int high = m - 1;
       int mid;
       int ans = Integer.MAX_VALUE;

       // Binary Search to find the
       // leftmost occurence of the 1
       while (low <= high)
       {
           mid = (low + high) / 2;

           // Condition if the column
           // contains the 1 at this
           // position of matrix
           if (mat[i][mid] == 1)
           {
               if (mid == 0)
               {
                   ans = 0;
                   break;
               }
               else if (mat[i][mid - 1] == 0)
               {
                   ans = mid;
                   break;
               }
           }
           if (mat[i][mid] == 1)
               high = mid - 1;
           else
               low = mid + 1;
       }

       // If there is a better solution
       // then update the answer
       if (ans < a)
           a = ans;
    }

    // Condition if the solution
    // doesn't exist in the matrix
    if (a == Integer.MAX_VALUE)
        return -1;
    return a + 1;
}

// Driver Code
public static void main(String[] args)
{
    int mat[][] = { { 0, 0, 0 },
                    { 0, 0, 1 },
                    { 0, 1, 1 } };

    System.out.print(search(mat, 3, 3));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# Leftmost Column with atleast a
# 1 in a sorted binary matrix
import sys
N = 3

# Function to search for the
# leftmost column of the matrix
# with atleast a 1 in sorted
# binary matrix
def search(mat, n, m):

    a = sys.maxsize

    # Loop to iterate over all the
    # rows of the matrix
    for i in range (n):
        low = 0
        high = m - 1
        ans = sys.maxsize

        # Binary Search to find the
        # leftmost occurence of the 1
        while (low <= high):
            mid = (low + high) // 2

            # Condition if the column
            # contains the 1 at this
            # position of matrix
            if (mat[i][mid] == 1):

                if (mid == 0):
                    ans = 0
                    break

                elif (mat[i][mid - 1] == 0):
                    ans = mid
                    break

            if (mat[i][mid] == 1):
                high = mid - 1
            else:
                low = mid + 1

        # If there is a better solution
        # then update the answer
        if (ans < a):
            a = ans

    # Condition if the solution
    # doesn't exist in the matrix
    if (a == sys.maxsize):
        return -1
    return a + 1

# Driver Code
if __name__ == "__main__":

    mat = [[0, 0, 0],
           [0, 0, 1],
           [0, 1, 1]]
    print(search(mat, 3, 3))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation to find the leftmost 
// column with atleast a 1 in a sorted
// binary matrix
using System;

class GFG{

//static readonly int N = 3;

// Function to search for the leftmost 
// column of the matrix with atleast a
//  1 in sorted binary matrix
static int search(int [,]mat, int n, int m)
{
    int i, a = int.MaxValue;

    // Loop to iterate over all the
    // rows of the matrix
    for(i = 0; i < n; i++)
    {
       int low = 0;
       int high = m - 1;
       int mid;
       int ans = int.MaxValue;

       // Binary Search to find the
       // leftmost occurence of the 1
       while (low <= high)
       {
           mid = (low + high) / 2;

           // Condition if the column
           // contains the 1 at this
           // position of matrix
           if (mat[i, mid] == 1)
           {
               if (mid == 0)
               {
                   ans = 0;
                   break;
               }
               else if (mat[i, mid - 1] == 0)
               {
                   ans = mid;
                   break;
               }
           }
           if (mat[i, mid] == 1)
               high = mid - 1;
           else
               low = mid + 1;
       }

       // If there is a better solution
       // then update the answer
       if (ans < a)
           a = ans;
    }

    // Condition if the solution
    // doesn't exist in the matrix
    if (a == int.MaxValue)
        return -1;
    return a + 1;
}

// Driver Code
public static void Main(String[] args)
{
    int [,]mat = { { 0, 0, 0 },
                   { 0, 0, 1 },
                   { 0, 1, 1 } };

    Console.Write(search(mat, 3, 3));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// Leftmost Column with atleast a
// 1 in a sorted binary matrix

var N = 3;

// Function to search for the
// leftmost column of the matrix
// with atleast a 1 in sorted
// binary matrix
function search(mat, n, m)
{
    var i, a = 1000000000;

    // Loop to iterate over all the
    // rows of the matrix
    for (i = 0; i < n; i++) {
        var low = 0;
        var high = m - 1;
        var mid;
        var ans = 1000000000;

        // Binary Search to find the
        // leftmost occurence of the 1
        while (low <= high) {
            mid = parseInt((low + high) / 2);

            // Condition if the column
            // contains the 1 at this
            // position of matrix
            if (mat[i][mid] == 1) {

                if (mid == 0) {
                    ans = 0;
                    break;
                }
                else if (mat[i][mid - 1] == 0) {
                    ans = mid;
                    break;
                }
            }

            if (mat[i][mid] == 1)
                high = mid - 1;
            else
                low = mid + 1;
        }

        // If there is a better solution
        // then update the answer
        if (ans < a)
            a = ans;
    }

    // Condition if the solution
    // doesn't exist in the matrix
    if (a == 1000000000)
        return -1;
    return a+1;
}

// Driver Code
var mat = [[0, 0, 0],
                [0, 0, 1],
                [0, 1, 1]];
document.write( search(mat, 3, 3));

</script>
```

**Output:** 

```
2
```

**性能分析:**

*   **时间复杂度:** O(N*logN)
*   **辅助空间:** O(1)