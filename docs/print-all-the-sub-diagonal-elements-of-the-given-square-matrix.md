# 打印给定方阵的所有次对角线元素

> 原文:[https://www . geeksforgeeks . org/print-给定方阵的所有次对角线元素/](https://www.geeksforgeeks.org/print-all-the-sub-diagonal-elements-of-the-given-square-matrix/)

给定大小为 **n * n** 的正方形矩阵 **mat[][]** 。任务是打印位于给定矩阵的次对角线上的所有元素。
**例:**

> **输入:** mat[][] = {
> {1，2，3}，
> {3，3，4，}，
> {2，4，6}}
> **输出:**3 4
> T9】输入: mat[][] = {
> {1，2，3，4}，
> {3，3，4，4}，
> {2，4，6，3}，
> {1

**方法:**正方形矩阵的次对角线是位于构成主对角线的元素正下方的元素集。对于主对角线元素，它们的索引类似于(i = j)，对于次对角线元素，它们的索引类似于 i = j + 1 (i 表示行，j 表示列)。
因此元素 **arr[1][0]，arr[2][1]，arr[3][2]，arr[4][3]，…。**是亚对角线的元素。
要么遍历矩阵的所有元素，只打印 i = j + 1 的那些需要 O(n <sup>2</sup> )时间复杂度的元素，要么只打印从 1 到 row count–1 的遍历行，并将元素打印为 arr[row][row–1]。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define R 4
#define C 4

// Function to print the sub diagonal
// elements of the given matrix
void printSubDiagonal(int arr[R][C])
{
    for (int i = 1; i < R; i++) {
        cout << arr[i][i - 1] << " ";
    }
}

// Driver code
int main()
{
    int arr[R][C] = { { 1, 2, 3, 4 },
                      { 5, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 } };

    printSubDiagonal(arr);

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

// Function to print the sub diagonal
// elements of the given matrix
static void printSubDiagonal(int arr[][])
{
    for (int i = 1; i < R; i++)
    {
            System.out.print(arr[i][i - 1] + " ");
    }
}

// Driver code
public static void main (String[] args)
{

    int arr[][] = { { 1, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 10, 11, 12 },
                    { 13, 14, 15, 16 } };

    printSubDiagonal(arr);

}
}

// This code is contributed by ajit.
```

## 蟒蛇 3

```
# Python3 implementation of the approach
R = 4
C = 4

# Function to print the sub diagonal
# elements of the given matrix
def printSubDiagonal(arr):

    for i in range(1, R):
        print(arr[i][i - 1], end = " ")

# Driver code
arr = [[ 1, 2, 3, 4 ],
       [ 5, 6, 7, 8 ],
       [ 9, 10, 11, 12 ],
       [ 13, 14, 15, 16 ]]

printSubDiagonal(arr);

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{
    static int R = 4;
    static int C = 4;

    // Function to print the sub diagonal
    // elements of the given matrix
    static void printSubDiagonal(int[,] arr)
    {
        for (int i = 1; i < R; i++)
        {
                Console.Write(arr[i, i - 1] + " ");
        }
    }

    // Driver code
    public static void Main ()
    {
        int [,]arr = {{ 1, 2, 3, 4 },
                      { 5, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 }};

        printSubDiagonal(arr);
    }
}

// This code is contributed by CodeMech.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var R = 4
var C = 4

// Function to print the sub diagonal
// elements of the given matrix
function printSubDiagonal(arr)
{
    for (var i = 1; i < R; i++) {
        document.write( arr[i][i - 1] + " ");
    }
}

// Driver code
var arr = [ [ 1, 2, 3, 4 ],
                  [ 5, 6, 7, 8 ],
                  [ 9, 10, 11, 12 ],
                  [ 13, 14, 15, 16 ] ];
printSubDiagonal(arr);

</script>
```

**Output:** 

```
5 10 15
```