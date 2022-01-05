# 求一个方阵两条对角线之和的乘积

> 原文:[https://www . geeksforgeeks . org/find-方阵两对角线之和的乘积/](https://www.geeksforgeeks.org/find-the-product-of-sum-of-two-diagonals-of-a-square-matrix/)

给定一个由大小为 **NxN** 的整数组成的正方形矩阵 **mat** ，任务是计算其对角线之和之间的乘积。
**例:**

```
Input: mat[][] = {{5, 8, 1}, 
                   {5, 10, 3}, 
                   {-6, 17, -9}}
Output: 30
Sum of primary diagonal = 5 + 10 + (-9) = 6.
Sum of secondary diagonal = 1 + 10 + (-6) = 5.
Product = 6 * 5 = 30.

Input: mat[][] = {{22, -8, 11}, 
                   {55, 87, -1}, 
                   {-61, 69, 19}}
Output: 4736
```

**天真的做法:** [遍历整个矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)[找到对角元素](https://www.geeksforgeeks.org/program-to-print-the-diagonals-of-a-matrix/)。[计算正方形矩阵两条对角线的和](https://www.geeksforgeeks.org/efficiently-compute-sums-of-diagonals-of-a-matrix/)。然后，取两个和的乘积。
***时间复杂度:**O(N<sup>2</sup>)*
**朴素方法:**通过观察对角元素索引中的模式，只遍历对角元素，而不是整个矩阵。
以下是本办法的实施情况:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find the product
// of the sum of diagonals.

#include <bits/stdc++.h>
using namespace std;

// Function to find the product
// of the sum of diagonals.
long long product(vector<vector<int>> &mat, int n)
{
    // Initialize sums of diagonals
    long long d1 = 0, d2 = 0;

    for (int i = 0; i < n; i++)
    {
        d1 += mat[i][i];
        d2 += mat[i][n - i - 1];
    }

    // Return the answer
    return 1LL * d1 * d2;
}

// Driven code
int main()
{
    vector<vector<int>> mat = {{ 5, 8, 1},
                               { 5, 10, 3},
                               { -6, 17, -9}};

    int n = mat.size();

    // Function call
    cout << product(mat, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the product
// of the sum of diagonals.

class GFG{

// Function to find the product
// of the sum of diagonals.
static long product(int [][]mat, int n)
{
    // Initialize sums of diagonals
    long d1 = 0, d2 = 0;

    for (int i = 0; i < n; i++)
    {
        d1 += mat[i][i];
        d2 += mat[i][n - i - 1];
    }

    // Return the answer
    return 1L * d1 * d2;
}

// Driven code
public static void main(String[] args)
{
    int [][]mat = {{ 5, 8, 1},
                               { 5, 10, 3},
                               { -6, 17, -9}};

    int n = mat.length;

    // Function call
    System.out.print(product(mat, n));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the product
# of the sum of diagonals.

# Function to find the product
# of the sum of diagonals.
def product(mat,n):

    # Initialize sums of diagonals
    d1 = 0
    d2 = 0

    for i in range(n):

        d1 += mat[i][i]
        d2 += mat[i][n - i - 1]

    # Return the answer
    return d1 * d2

# Driven code
if __name__ == '__main__':
    mat = [[5, 8, 1],
        [5, 10, 3],
        [-6, 17, -9]]

    n = len(mat)

    # Function call
    print(product(mat, n))

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program to find the product
// of the sum of diagonals.
using System;

class GFG{

// Function to find the product
// of the sum of diagonals.
static long product(int [,]mat, int n)
{
    // Initialize sums of diagonals
    long d1 = 0, d2 = 0;

    for (int i = 0; i < n; i++)
    {
        d1 += mat[i, i];
        d2 += mat[i, n - i - 1];
    }

    // Return the answer
    return 1L * d1 * d2;
}

// Driven code
public static void Main(String[] args)
{
    int [,]mat = {{ 5, 8, 1},
                    { 5, 10, 3},
                    { -6, 17, -9}};

    int n = mat.GetLength(0);

    // Function call
    Console.Write(product(mat, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to find the product
// of the sum of diagonals.

// Function to find the product
// of the sum of diagonals.
function product(mat, n)
{
    // Initialize sums of diagonals
    let d1 = 0, d2 = 0;

    for (let i = 0; i < n; i++)
    {
        d1 += mat[i][i];
        d2 += mat[i][n - i - 1];
    }

    // Return the answer
    return d1 * d2;
}

// Driven code
    let mat = [[ 5, 8, 1],
                               [ 5, 10, 3],
                               [ -6, 17, -9]];

    let n = mat.length;

    // Function call
    document.write(product(mat, n));

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
30
```

***时间复杂度:**O(N)*T4】