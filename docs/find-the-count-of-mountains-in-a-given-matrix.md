# 计算给定矩阵中的山脉数量

> 原文:[https://www . geesforgeks . org/find-给定矩阵中的山数/](https://www.geeksforgeeks.org/find-the-count-of-mountains-in-a-given-matrix/)

给定一个大小为 **N X N** 的 2D 方块**矩阵**，任务是计算矩阵中的山脉数量。

> 当所有周围的元素(在所有 8 个方向上)都小于给定的元素时，矩阵中的元素被称为山。

**例:**

```
Input: matrix = 
{ { 4, 5, 6 },
  { 2, 1, 3 },
  { 7, 8, 9 } }
Output: 1
Explanation 
Only mountain element = 9\. 
All the neighbouring elements 
1, 3 and 8 are smaller than 9.

Input: matrix = 
{ { 7, 8, 9 },
  { 1, 2, 3 },
  { 4, 5, 6 } }
Output: 2
Explanation
Mountain elements = 6 (2, 3 and 5)
and 9 (8, 2, and 3) 
```

**方法:**想法是迭代矩阵，同时检查所有可能的 8 个方向上的相邻元素。如果元素大于所有元素，则递增计数器变量。最后，退回柜台。

1.  创建一个大小为 **(N + 2) X (N + 2)** 的辅助数组。
2.  用 **INT_MIN** 值填充所有边框元素
3.  在 **N X N** 的剩余数组空间中，复制原矩阵
4.  现在检查一个元素是否大于所有 8 个方向上的元素。
5.  统计这类元素的数量并打印出来。

**例如:**

```
If matrix = 
{ { 7, 8, 9 },
  { 1, 2, 3 },
  { 4, 5, 6 } }

The auxiliary array would be
{ { 0, 0, 0, 0, 0 },
  { 0, 7, 8, 9, 0 },
  { 0, 1, 2, 3, 0 },
  { 0, 4, 5, 6, 0 },
  { 0, 0, 0, 0, 0 } }
```

**以下是上述方法的实施:**

## C++

```
// C++ program find the count of
// mountains in a given Matrix

#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;

// Function to count number of mountains
// in a given matrix of size n
int countMountains(int a[][MAX], int n)
{
    int A[n + 2][n + 2];
    int count = 0;

    // form another matrix with one extra
    // layer of border elements. Border
    // elements will contain INT_MIN value.
    for (int i = 0; i < n + 2; i++) {
        for (int j = 0; j < n + 2; j++) {

            if ((i == 0) || (j == 0)
                || (i == n + 1)
                || (j == n + 1)) {

                // For border elements,
                // set value as INT_MIN
                A[i][j] = INT_MIN;
            }
            else {

                // For rest elements, just copy
                // it into new matrix
                A[i][j] = a[i - 1][j - 1];
            }
        }
    }

    // Check for mountains in the modified matrix
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {

            // check for all directions
            if ((A[i][j] > A[i - 1][j])
                && (A[i][j] > A[i + 1][j])
                && (A[i][j] > A[i][j - 1])
                && (A[i][j] > A[i][j + 1])
                && (A[i][j] > A[i - 1][j - 1])
                && (A[i][j] > A[i + 1][j + 1])
                && (A[i][j] > A[i - 1][j + 1])
                && (A[i][j] > A[i + 1][j - 1])) {
                count++;
            }
        }
    }

    return count;
}

// Driver code
int main()
{
    int a[][MAX] = { { 1, 2, 3 },
                     { 4, 5, 6 },
                     { 7, 8, 9 } };
    int n = 3;

    cout << countMountains(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program find the count of
// mountains in a given Matrix
import java.util.*;

class GFG{

static int MAX = 100;

// Function to count number of mountains
// in a given matrix of size n
static int countMountains(int a[][], int n)
{
    int [][]A = new int[n + 2][n + 2];
    int count = 0;

    // form another matrix with one extra
    // layer of border elements. Border
    // elements will contain Integer.MIN_VALUE value.
    for (int i = 0; i < n + 2; i++) {
        for (int j = 0; j < n + 2; j++) {

            if ((i == 0) || (j == 0)
                || (i == n + 1)
                || (j == n + 1)) {

                // For border elements,
                // set value as Integer.MIN_VALUE
                A[i][j] = Integer.MIN_VALUE;
            }
            else {

                // For rest elements, just copy
                // it into new matrix
                A[i][j] = a[i - 1][j - 1];
            }
        }
    }

    // Check for mountains in the modified matrix
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {

            // check for all directions
            if ((A[i][j] > A[i - 1][j])
                && (A[i][j] > A[i + 1][j])
                && (A[i][j] > A[i][j - 1])
                && (A[i][j] > A[i][j + 1])
                && (A[i][j] > A[i - 1][j - 1])
                && (A[i][j] > A[i + 1][j + 1])
                && (A[i][j] > A[i - 1][j + 1])
                && (A[i][j] > A[i + 1][j - 1])) {
                count++;
            }
        }
    }

    return count;
}

// Driver code
public static void main(String[] args)
{
    int a[][] = { { 1, 2, 3 },
                     { 4, 5, 6 },
                     { 7, 8, 9 } };
    int n = 3;

    System.out.print(countMountains(a, n));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program find the count of
# mountains in a given Matrix
MAX = 100

# Function to count number of mountains
# in a given matrix of size n
def countMountains(a, n):
    A = [[0 for i in range(n+2)] for i in range(n+2)]
    count = 0

    # form another matrix with one extra
    # layer of border elements. Border
    # elements will contain INT_MIN value.
    for i in range(n+2):
        for j in range(n+2):
            if ((i == 0) or (j == 0) or
                (i == n + 1) or (j == n + 1)):

                # For border elements,
                # set value as INT_MIN
                A[i][j] = float('-inf')
            else:

                # For rest elements, just copy
                # it into new matrix
                A[i][j] = a[i - 1][j - 1]

    # Check for mountains in the modified matrix
    for i in range(n + 1):
        for j in range(n + 1):
            if ((A[i][j] > A[i - 1][j]) and
                (A[i][j] > A[i + 1][j]) and
                (A[i][j] > A[i][j - 1]) and
                (A[i][j] > A[i][j + 1]) and
                (A[i][j] > A[i - 1][j - 1]) and
                (A[i][j] > A[i + 1][j + 1]) and
                (A[i][j] > A[i - 1][j + 1]) and
                (A[i][j] > A[i + 1][j - 1])):
                count = count + 1

    return count

# Driver code
a = [ [ 1, 2, 3 ],
    [ 4, 5, 6 ],
    [ 7, 8, 9 ] ]

n = 3

print(countMountains(a, n))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program find the count of
// mountains in a given Matrix
using System;

class GFG{

    static int MAX = 100;

    // Function to count number of mountains
    // in a given matrix of size n
    static int countMountains(int [,]a, int n)
    {
        int [,]A = new int[n + 2,n + 2];
        int count = 0;

        // form another matrix with one extra
        // layer of border elements. Border
        // elements will contain Integer.MIN_VALUE value.
        for (int i = 0; i < n + 2; i++) {
            for (int j = 0; j < n + 2; j++) {

                if ((i == 0) || (j == 0)
                    || (i == n + 1)
                    || (j == n + 1)) {

                    // For border elements,
                    // set value as Integer.MIN_VALUE
                    A[i,j] = int.MinValue;
                }
                else {

                    // For rest elements, just copy
                    // it into new matrix
                    A[i,j] = a[i - 1,j - 1];
                }
            }
        }

        // Check for mountains in the modified matrix
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {

                // check for all directions
                if ((A[i,j] > A[i - 1,j])
                    && (A[i,j] > A[i + 1,j])
                    && (A[i,j] > A[i,j - 1])
                    && (A[i,j] > A[i,j + 1])
                    && (A[i,j] > A[i - 1,j - 1])
                    && (A[i,j] > A[i + 1,j + 1])
                    && (A[i,j] > A[i - 1,j + 1])
                    && (A[i,j] > A[i + 1,j - 1])) {
                    count++;
                }
            }
        }

        return count;
    }

    // Driver code
    public static void Main(string[] args)
    {
        int [,]a = { { 1, 2, 3 },
                        { 4, 5, 6 },
                        { 7, 8, 9 } };
        int n = 3;

        Console.WriteLine(countMountains(a, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
//Javascript program find the count of
// mountains in a given Matrix

// Function to count number of mountains
// in a given matrix of size n
function countMountains(a,  n)
{
    var A= new Array(n+2).fill(0).map(() => new Array(n+2).fill(0));
    var count = 0;

    // form another matrix with one extra
    // layer of border elements. Border
    // elements will contain INT_MIN value.
    for (var i = 0; i < n + 2; i++) {
        for (var j = 0; j < n + 2; j++) {

            if ((i == 0) || (j == 0)
                || (i == n + 1)
                || (j == n + 1)) {

                // For border elements,
                // set value as INT_MIN
                A[i][j] = Number.MIN_VALUE;
            }
            else {

                // For rest elements, just copy
                // it into new matrix
                A[i][j] = a[i - 1][j - 1];
            }
        }
    }

    // Check for mountains in the modified matrix
    for (var i = 1; i <= n; i++) {
        for (var j = 1; j <= n; j++) {

            // check for all directions
            if ((A[i][j] > A[i - 1][j])
                && (A[i][j] > A[i + 1][j])
                && (A[i][j] > A[i][j - 1])
                && (A[i][j] > A[i][j + 1])
                && (A[i][j] > A[i - 1][j - 1])
                && (A[i][j] > A[i + 1][j + 1])
                && (A[i][j] > A[i - 1][j + 1])
                && (A[i][j] > A[i + 1][j - 1])) {
                count++;
            }
        }
    }

    return count;
}

var a = [[ 1, 2, 3 ],
                     [ 4, 5, 6 ],
                     [ 7, 8, 9 ] ];
var n = 3;
  document.write( countMountains(a, n));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
1
```

**性能分析** s:

*   **时间复杂度**:在上面的方法中，我们做了两次迭代。首先是在 **(N + 2) X (N + 2)** 元素上创建辅助矩阵。第二个在 **N X N** 元素上寻找实际的山元素，所以时间复杂度为 **O(N X N)** 。

*   **辅助空间复杂度**:在上面的做法中，我们使用的是一个大小为 **(N + 2) X (N + 2)** 的辅助矩阵，所以辅助空间复杂度为 **O(N *N)** 。