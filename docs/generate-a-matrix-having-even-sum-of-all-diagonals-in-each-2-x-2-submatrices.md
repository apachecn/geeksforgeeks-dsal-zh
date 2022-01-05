# 生成每个 2×2 子矩阵中所有对角线之和为偶数的矩阵

> 原文:[https://www . geesforgeks . org/generate-a-matrix-having-all-sum-in-2-x-2-submetrics/](https://www.geeksforgeeks.org/generate-a-matrix-having-even-sum-of-all-diagonals-in-each-2-x-2-submatrices/)

给定一个正整数 **N** ，任务是构造一个大小为 **N * N** 的[矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，使得所有矩阵元素都与范围**【1，N<sup>2</sup>**不同，并且每个 **2 * 2** 子矩阵的两条对角线上的元素之和是偶数。

**示例:**

> **输入:** N = 3
> **输出:**
> 1 2 3
> 4 5 6
> 7 8 9
> **说明:**
> 输出矩阵中每 2 * 2 个矩阵的对角元素为{ {1，5}、{2，4}、{2，6}、{3，5}、{4，8}、{5，7}、{5，9}、{6，8} }。可以观察到，每条对角线的和都是偶数。
> 
> **输入:** N = 4
> **输出:**
> 1 2 3 4
> 6 5 8 7
> 9 10 11 12
> 14 13 16 15

**方法:**按照以下步骤解决问题:

*   初始化一个矩阵，比如说 **mat[][]** ，来存储矩阵元素，使得所有的矩阵元素都与范围**【1，N】<sup>2</sup>**不同，并且每个 **2 * 2** 子矩阵的两条对角线上的矩阵元素之和是偶数。
*   初始化一个变量，比如说**奇数= 1** ，来存储奇数。
*   初始化一个变量，比如**偶数= 2** ，存储偶数。
*   通过检查以下条件，填充所有矩阵元素， **mat[i][j]** :
    *   如果 **(i + j) % 2 = 0** ，则设置**mat【I】【j】=奇数**并更新**奇数+= 2** 。
    *   否则，设置 **mat[i][j] =偶数**并更新**偶数+= 2** 。
*   最后打印矩阵 **mat[][]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to construct a matrix such that
// the sum elements in both diagonals of
// every 2 * 2 matrices is even
void generateMatrix(int N)
{
    // Stores odd numbers
    int odd = 1;

    // Stores even numbers
    int even = 2;

    // Store matrix elements such that
    // sum of elements in both diagonals
    // of every 2 * 2 submatrices is even
    int mat[N + 1][N + 1];

    // Fill all the values of
    // matrix elements
    for (int i = 1; i <= N; i++) {

        for (int j = 1; j <= N; j++) {

            if ((i + j) % 2 == 0) {

                mat[i][j] = odd;

                // Update odd
                odd += 2;
            }

            else {

                mat[i][j] = even;

                // Update even
                even += 2;
            }
        }
    }

    // Print the matrix
    for (int i = 1; i <= N; i++) {

        for (int j = 1; j <= N; j++) {

            cout << mat[i][j] << " ";
        }

        cout << endl;
    }
}

// Driver Code
int main()
{
    int N = 4;
    generateMatrix(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to construct a matrix such that
// the sum elements in both diagonals of
// every 2 * 2 matrices is even
static void generateMatrix(int N)
{

    // Stores odd numbers
    int odd = 1;

    // Stores even numbers
    int even = 2;

    // Store matrix elements such that
    // sum of elements in both diagonals
    // of every 2 * 2 submatrices is even
    int[][] mat = new int[N + 1][N + 1];

    // Fill all the values of
    // matrix elements
    for(int i = 1; i <= N; i++)
    {
        for(int j = 1; j <= N; j++)
        {
            if ((i + j) % 2 == 0)
            {
                mat[i][j] = odd;

                // Update odd
                odd += 2;
            }

            else
            {
                mat[i][j] = even;

                // Update even
                even += 2;
            }
        }
    }

    // Print the matrix
    for(int i = 1; i <= N; i++)
    {
        for(int j = 1; j <= N; j++)
        {
            System.out.print(mat[i][j] + " ");
        }

        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 4;

    generateMatrix(N);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to construct a matrix such that
# the sum elements in both diagonals of
# every 2 * 2 matrices is even
def generateMatrix(N):

    # Stores odd numbers
    odd = 1;

    # Stores even numbers
    even = 2;

    # Store matrix elements such that
    # sum of elements in both diagonals
    # of every 2 * 2 submatrices is even
    mat = [[0 for i in range(N + 1)] for j in range(N + 1)] ;

    # Fill all the values of
    # matrix elements
    for i in range(1, N + 1):
        for j in range(1, N + 1):
            if ((i + j) % 2 == 0):
                mat[i][j] = odd;

                # Update odd
                odd += 2;
            else:
                mat[i][j] = even;

                # Update even
                even += 2;

    # Print the matrix
    for i in range(1, N + 1):
        for j in range(1, N + 1):
            print(mat[i][j], end = " ");
        print();

# Driver Code
if __name__ == '__main__':
    N = 4;
    generateMatrix(N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to construct a matrix such that
// the sum elements in both diagonals of
// every 2 * 2 matrices is even
static void generateMatrix(int N)
{

    // Stores odd numbers
    int odd = 1;

    // Stores even numbers
    int even = 2;

    // Store matrix elements such that
    // sum of elements in both diagonals
    // of every 2 * 2 submatrices is even
    int[,] mat = new int[N + 1, N + 1];

    // Fill all the values of
    // matrix elements
    for(int i = 1; i <= N; i++)
    {
        for(int j = 1; j <= N; j++)
        {
            if ((i + j) % 2 == 0)
            {
                mat[i, j] = odd;

                // Update odd
                odd += 2;
            }

            else
            {
                mat[i, j] = even;

                // Update even
                even += 2;
            }
        }
    }

    // Print the matrix
    for(int i = 1; i <= N; i++)
    {
        for(int j = 1; j <= N; j++)
        {
            Console.Write(mat[i, j] + " ");
        }

        Console.WriteLine();
    }
}

// Driver Code
static public void Main()
{
    int N = 4;

    generateMatrix(N);
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to construct a matrix such that
// the sum elements in both diagonals of
// every 2 * 2 matrices is even
function generateMatrix(N)
{

    // Stores odd numbers
    let odd = 1;

    // Stores even numbers
    let even = 2;

    // Store matrix elements such that
    // sum of elements in both diagonals
    // of every 2 * 2 submatrices is even
    let mat = new Array(N + 1);

    // Loop to create 2D array using 1D array
    for (var i = 0; i < mat.length; i++) {
        mat[i] = new Array(2);
    }

    // Fill all the values of
    // matrix elements
    for(let i = 1; i <= N; i++)
    {
        for(let j = 1; j <= N; j++)
        {
            if ((i + j) % 2 == 0)
            {
                mat[i][j] = odd;

                // Update odd
                odd += 2;
            }

            else
            {
                mat[i][j] = even;

                // Update even
                even += 2;
            }
        }
    }

    // Prlet the matrix
    for(let i = 1; i <= N; i++)
    {
        for(let j = 1; j <= N; j++)
        {
            document.write(mat[i][j] + " ");
        }

        document.write("<br/>");
    }
}

    // Driver Code

    let N = 4;

    generateMatrix(N);

</script>
```

**Output:** 

```
1 2 3 4 
6 5 8 7 
9 10 11 12 
14 13 16 15
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*