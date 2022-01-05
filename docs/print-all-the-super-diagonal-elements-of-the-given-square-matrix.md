# 打印给定方阵的所有超对角线元素

> 原文:[https://www . geeksforgeeks . org/print-给定方阵的所有超对角线元素/](https://www.geeksforgeeks.org/print-all-the-super-diagonal-elements-of-the-given-square-matrix/)

给定大小为 **n * n** 的正方形矩阵 **mat[][]** 。任务是打印位于给定矩阵的超对角线上的所有元素。
**例:**

> **输入:** mat[][] = {
> {1，2，3}，
> {3，3，4，}，
> {2，4，6}}
> **输出:**2 4
> T9】输入: mat[][] = {
> {1，2，3，4}，
> {3，3，4，4}，
> {2，4，6，3}，
> {1

**方法:**正方形矩阵的超对角线是位于构成主对角线的元素正上方的元素集。对于主对角线元素，它们的索引类似于(i = j)，对于超对角线元素，它们的索引为 j = i + 1 (i 表示行，j 表示列)。
因此元素 **arr[0][1]，arr[1][2]，arr[2][3]，arr[3][4]，…。**是超对角线的元素。
遍历矩阵的所有元素，只打印 j = i + 1 的元素，这需要 O(n <sup>2</sup> )的时间复杂度，或者只遍历从 1 到列 count–1 的列，并将元素打印为 arr[column–1][column]。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define R 4
#define C 4

// Function to print the super diagonal
// elements of the given matrix
void printSuperDiagonal(int arr[R][C])
{
    for (int i = 1; i < C; i++) {
        cout << arr[i - 1][i] << " ";
    }
}

// Driver code
int main()
{
    int arr[R][C] = { { 1, 2, 3, 4 },
                      { 5, 6, 7, 8 },
                      { 9, 10, 11, 12 },
                      { 13, 14, 15, 16 } };

    printSuperDiagonal(arr);

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
    for (int i = 1; i < C; i++)
    {
            System.out.print(arr[i-1][i] + " ");
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

// This code is contributed by mohit kumar 29
```

## 蟒蛇 3

```
# Python3 implementation of the approach

R = 4
C = 4

# Function to print the super diagonal
# elements of the given matrix
def printSuperDiagonal(arr) :

    for i in range(1, C) :
        print(arr[i - 1][i],end= " ");

# Driver code
if __name__ == "__main__" :

    arr = [ [ 1, 2, 3, 4 ],
            [5, 6, 7, 8 ],
            [ 9, 10, 11, 12 ],
            [ 13, 14, 15, 16 ]]
    printSuperDiagonal(arr);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

lass GFG
{

    static int R = 4;
    static int C = 4;

    // Function to print the sub diagonal
    // elements of the given matrix
    static void printSubDiagonal(int [,]arr)
    {
        for (int i = 1; i < C; i++)
        {
                Console.Write(arr[i-1,i] + " ");
        }
    }

    // Driver code
    public static void Main (String[] args)
    {

        int [,]arr = { { 1, 2, 3, 4 },
                        { 5, 6, 7, 8 },
                        { 9, 10, 11, 12 },
                        { 13, 14, 15, 16 } };

        printSubDiagonal(arr);
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var R = 4
var C = 4

// Function to print the super diagonal
// elements of the given matrix
function printSuperDiagonal( arr)
{
    for (var i = 1; i < C; i++) {
        document.write( arr[i - 1][i] + " ");
    }
}

// Driver code
var arr = [ [ 1, 2, 3, 4 ],
                  [ 5, 6, 7, 8 ],
                  [ 9, 10, 11, 12 ],
                  [ 13, 14, 15, 16 ] ];
printSuperDiagonal(arr);

</script>
```

**Output:** 

```
2 7 12
```