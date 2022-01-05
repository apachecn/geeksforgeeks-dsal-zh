# 对矩阵的主对角线进行排序

> 原文:[https://www . geeksforgeeks . org/matrix 的主对角线排序/](https://www.geeksforgeeks.org/sort-the-major-diagonal-of-the-matrix/)

给定一个矩阵 **mat[][]** ，任务是将矩阵的[主对角元素](https://en.wikipedia.org/wiki/Main_diagonal)按照递增的顺序排序。
**主对角线:**矩阵的主对角线或主对角线是元素集合 mat <sub>i，j</sub> ，其中 **i == j** 。
**举例:**

```
Input: mat[][] = {{4, 2}, {3, 1}}
Output: 
1 2
3 4
Explanation:
In the given matrix, the diagonal elements are -
=> {mat[0][0], mat[1][1]}
=> {4, 1}
=> Sorted Order = {1, 4}

Input: mat[][] = {{9, 4}, {3, 4}}     
Output: 
4 4
3 9
Explanation:
In the given matrix, the diagonal elements are -
=> {mat[0][0], mat[1][1]}
=> {9, 4}
=> Sorted Order = {4, 9}
```

**方法 1 :-**
**方法:**思路是修改[选择排序](http://www.geeksforgeeks.org/selection-sort/)对矩阵的对角元素进行排序。矩阵 M*N 的二次元素个数为 **min(M，N)** 。正如我们所知，矩阵的主对角线元素是 mat <sub>i，j</sub> ，其中 i == j。因此，矩阵的[主对角线](https://en.wikipedia.org/wiki/Main_diagonal)的 i <sup>第</sup>个元素将是 mat【I】【I】。因此，从矩阵的主对角线上反复寻找最小元素，并将其放在开始处。
以下是上述方法的实施:

## C++

```
// C++ implementation to sort the
// major diagonal of the matrix

#include <bits/stdc++.h>

using namespace std;

// Function to sort the major
// diagonal of the matrix
void sortDiagonal(int a[2][2], int M, int N)
{
    // Loop to find the ith minimum
    // element from the major diagonal
    for (int i = 0; i < M; i++) {
        int sm = a[i][i];
        int pos = i;

        // Loop to find the minimum
        // element from the unsorted matrix
        for (int j = i + 1; j < N; j++) {
            if (sm > a[j][j]) {
                sm = a[j][j];
                pos = j;
            }
        }

        // Swap to put the minimum
        // element at the beginning of
        // the major diagonal of matrix
        swap(a[i][i], a[pos][pos]);
    }

    // Loop to print the matrix
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++)
            cout << a[i][j] << " ";
        cout << endl;
    }
}

// Driven Code
int main()
{
    int a[2][2] = { { 4, 2 },
                    { 3, 1 } };

    // Sort the major Diagonal
    sortDiagonal(a, 2, 2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to sort the
// major diagonal of the matrix
class GFG{

// Function to sort the major
// diagonal of the matrix
static void sortDiagonal(int a[][], int M, int N)
{
    // Loop to find the ith minimum
    // element from the major diagonal
    for (int i = 0; i < M; i++) {
        int sm = a[i][i];
        int pos = i;

        // Loop to find the minimum
        // element from the unsorted matrix
        for (int j = i + 1; j < N; j++) {
            if (sm > a[j][j]) {
                sm = a[j][j];
                pos = j;
            }
        }

        // Swap to put the minimum
        // element at the beginning of
        // the major diagonal of matrix
        swap(a, i, i, pos, pos);
    }

    // Loop to print the matrix
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++)
            System.out.print(a[i][j]+ " ");
        System.out.println();
    }
}

static void swap(int[][] a, int i, int i2, int pos, int pos2) {
    int temp = a[i][i2];
    a[i][i2] = a[pos][pos2];
    a[pos][pos2] = temp;   
}

// Driven Code
public static void main(String[] args)
{
    int a[][] = { { 4, 2 },
                    { 3, 1 } };

    // Sort the major Diagonal
    sortDiagonal(a, 2, 2);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to sort the
# major diagonal of the matrix

# Function to sort the major
# diagonal of the matrix
def sortDiagonal(a, M, N):

    # Loop to find the ith minimum
    # element from the major diagonal
    for i in range(M):
        sm = a[i][i]
        pos = i

        # Loop to find the minimum
        # element from the unsorted matrix
        for j in range(i + 1 , N):
            if (sm > a[j][j]):
                sm = a[j][j]
                pos = j

        # Swap to put the minimum
        # element at the beginning of
        # the major diagonal of matrix
        a[i][i], a[pos][pos] = a[pos][pos] , a[i][i]

    # Loop to print the matrix
    for i in range(M):
        for j in range(N):
            print(a[i][j],end=" ")
        print()

# Driven Code
a = [[4, 2],[3, 1]]

# Sort the major Diagonal
sortDiagonal(a, 2, 2)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to sort the
// major diagonal of the matrix
using System;

class GFG{

// Function to sort the major
// diagonal of the matrix
static void sortDiagonal(int[,]a, int M, int N)
{
    // Loop to find the ith minimum
    // element from the major diagonal
    for (int i = 0; i < M; i++) {
        int sm = a[i, i];
        int pos = i;

        // Loop to find the minimum
        // element from the unsorted matrix
        for (int j = i + 1; j < N; j++) {
            if (sm > a[j, j]) {
                sm = a[j, j];
                pos = j;
            }
        }

        // Swap to put the minimum
        // element at the beginning of
        // the major diagonal of matrix
        swap(a, i, i, pos, pos);
    }

    // Loop to print the matrix
    for (int i = 0; i < M; i++) {
        for (int j = 0; j < N; j++)
            Console.Write(a[i, j]+ " ");
        Console.WriteLine();
    }
}

static void swap(int[,] a, int i, int i2, int pos, int pos2) {
    int temp = a[i, i2];
    a[i, i2] = a[pos, pos2];
    a[pos, pos2] = temp;   
}

// Driven Code
public static void Main(String[] args)
{
    int[,]a = { { 4, 2 },
                    { 3, 1 } };

    // Sort the major Diagonal
    sortDiagonal(a, 2, 2);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to sort the
// major diagonal of the matrix

// Function to sort the major
// diagonal of the matrix
function sortDiagonal(a, M, N)
{
    // Loop to find the ith minimum
    // element from the major diagonal
    for (var i = 0; i < M; i++) {
        var sm = a[i][i];
        var pos = i;

        // Loop to find the minimum
        // element from the unsorted matrix
        for (var j = i + 1; j < N; j++) {
            if (sm > a[j][j]) {
                sm = a[j][j];
                pos = j;
            }
        }

        // Swap to put the minimum
        // element at the beginning of
        // the major diagonal of matrix
        temp = a[i][i]
        a[i][i] = a[pos][pos]
        a[pos][pos] = temp
    }

    // Loop to print the matrix
    for (var i = 0; i < M; i++) {
        for (var j = 0; j < N; j++)
            document.write( a[i][j] + " ");
        document.write("<br>");
    }
}

// Driven Code
var a = [ [ 4, 2 ],
                [ 3, 1 ] ];
// Sort the major Diagonal
sortDiagonal(a, 2, 2);

// This code is contributed by noob2000.
</script>
```

**Output**

```
1 2 
3 4 

```