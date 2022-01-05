# 生成给定总和的每行每列的矩阵

> 原文:[https://www . geeksforgeeks . org/生成给定总和的每行每列矩阵/](https://www.geeksforgeeks.org/generate-a-matrix-with-each-row-and-column-of-given-sum/)

给定两个尺寸分别为 **N** 和 **M** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **行【】**和**col【】**，任务是构建尺寸为 **N × M** 的[矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，使得每 i <sup>第</sup>行中矩阵元素的[和为**行【I】**中矩阵元素的](https://www.geeksforgeeks.org/program-to-find-the-sum-of-each-row-and-each-column-of-a-matrix/)[和](https://www.geeksforgeeks.org/program-to-find-the-sum-of-each-row-and-each-column-of-a-matrix/)

**示例:**

> **输入:**行[] = {5，7，10}，列[] = {8，6，8}
> **输出:** {{0，5，0}，{6，1，0}，{2，0，8}}
> **解释:**
> 行 1 的和等于 5，列 1 的和等于 8
> 行 2 的和等于 7，列 2 的和等于 6
> 行 3 的和等于 10，列
> 
> **输入:**行[] ={1，0}，列[] = {1}
> **输出:** {{1}，{0}}
> **解释:**
> 行 1 的和等于 1，列 1 的和等于 1
> 行 2 的和等于 0

**方法:**解决这个问题最简单的方法就是使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)。按照以下步骤解决此问题:

*   初始化一个具有尺寸 **N × M** 的[矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)。
*   按照以下方式开始填充矩阵的每个单元格 **(i，j)** :
    *   对于每个单元格 **(i，j)** ，选择**行【I】**、**列【j】**的最小值，并将其放在单元格 **(i，j)** 处。就这样吧。
    *   从**行【I】**和**列**中减去**min**。
*   完成上述步骤后，打印形成的[矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate a matrix with
// sum of each row equal to sum of r[]
// and sum of each column equal to sum of c[]
vector<vector<int> > restoreGem(
    vector<int>& r, vector<int>& c)
{
    // Initialize a matrix
    vector<vector<int> > dp(r.size(),
                            vector<int>(c.size(), 0));

    // Traverse each cell (i, j) of the matrix
    for (int i = 0; i < r.size(); i++) {
        for (int j = 0; j < c.size(); j++) {

            // Assign the minimum of the
            // row or column value
            int m = min(r[i], c[j]);
            dp[i][j] = m;

            // Subtract the minimum from
            // both row and column sum
            r[i] -= m;
            c[j] -= m;
        }
    }

    return dp;
}

void printMatrix(vector<vector<int> > ans,
                 int N, int M)
{

    // Print the matrix obtained
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            cout << ans[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    vector<int> rowSum = { 5, 7, 10 };
    vector<int> colSum = { 8, 6, 8 };

    vector<vector<int> > ans
        = restoreGem(rowSum, colSum);

    printMatrix(ans, rowSum.size(),
                colSum.size());
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

// Function to generate a matrix with
// sum of each row equal to sum of r[]
// and sum of each column equal to sum of c[]
static int[][] restoreGem(int[] r, int[] c)
{

    // Initialize a matrix
    int[][] dp = new int[r.length][c.length];

    // Traverse each cell (i, j) of the matrix
    for (int i = 0; i < r.length; i++)
    {
        for (int j = 0; j < c.length; j++)
        {

            // Assign the minimum of the
            // row or column value
            int m = Math.min(r[i], c[j]);
            dp[i][j] = m;

            // Subtract the minimum from
            // both row and column sum
            r[i] -= m;
            c[j] -= m;
        }
    }
    return dp;
}

static void printMatrix(int[][] ans,
                 int N, int M)
{

    // Print the matrix obtained
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {
            System.out.print(ans[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] rowSum = { 5, 7, 10 };
    int[] colSum = { 8, 6, 8 };

    int[][] ans
        = restoreGem(rowSum, colSum);

    printMatrix(ans, rowSum.length,
                colSum.length);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

// Function to generate a matrix with
// sum of each row equal to sum of r[]
// and sum of each column equal to sum of c[]
static int[,] restoreGem(int[] r, int[] c)
{

    // Initialize a matrix
    int[,] dp = new int[r.Length, c.Length];

    // Traverse each cell (i, j) of the matrix
    for (int i = 0; i < r.Length; i++)
    {
        for (int j = 0; j < c.Length; j++)
        {

            // Assign the minimum of the
            // row or column value
            int m = Math.Min(r[i], c[j]);
            dp[i,j] = m;

            // Subtract the minimum from
            // both row and column sum
            r[i] -= m;
            c[j] -= m;
        }
    }
    return dp;
}

static void printMatrix(int[,] ans,
                 int N, int M)
{

    // Print the matrix obtained
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {
            Console.Write(ans[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Driver Code
public static void Main(String[] args)
{
    int[] rowSum = { 5, 7, 10 };
    int[] colSum = { 8, 6, 8 };

    int[,] ans
        = restoreGem(rowSum, colSum);
    printMatrix(ans, rowSum.Length,
                colSum.Length);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program of the above approach

// Function to generate a matrix with
// sum of each row equal to sum of r[]
// and sum of each column equal to sum of c[]
function restoreGem(r, c)
{

    // Initialize a matrix
    let dp = new Array(r.length);

    // Loop to create 2D array using 1D array
    for (var i = 0; i < dp.length; i++) {
        dp[i] = new Array(2);
    }

    // Traverse each cell (i, j) of the matrix
    for (let i = 0; i < r.length; i++)
    {
        for (let j = 0; j < c.length; j++)
        {

            // Assign the minimum of the
            // row or column value
            let m = Math.min(r[i], c[j]);
            dp[i][j] = m;

            // Subtract the minimum from
            // both row and column sum
            r[i] -= m;
            c[j] -= m;
        }
    }
    return dp;
}

function prletMatrix(ans, N, M)
{

    // Prlet the matrix obtained
    for (let i = 0; i < N; i++)
    {
        for (let j = 0; j < M; j++)
        {
            document.write(ans[i][j] + " ");
        }
        document.write("<br/>");
    }
}

    // Driver Code

    let rowSum = [ 5, 7, 10 ];
    let colSum = [ 8, 6, 8 ];

    let ans
        = restoreGem(rowSum, colSum);

    prletMatrix(ans, rowSum.length,
                colSum.length);

</script>
```

**Output:** 

```
5 0 0 
3 4 0 
0 2 8
```

***时间复杂度:** O(N×M)*
***辅助空间:** O(N×M)*