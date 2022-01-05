# 将一个矩阵转换成另一个给定维度的矩阵

> 原文:[https://www . geeksforgeeks . org/convert-a-matrix-to-另一个给定维度的矩阵/](https://www.geeksforgeeks.org/convert-a-matrix-into-another-matrix-of-given-dimensions/)

给定一个大小为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix-introduction/)、 **mat[][]** 和两个正整数 **A** 和 **B** ，任务是根据给定的矩阵元素构造一个大小为 **A * B** 的矩阵。如果存在多个解决方案，则打印其中任何一个。否则，打印 **-1** 。

> **输入:** mat[][] = { { 1，2，3，4，5，6 } }，A = 2，B = 3
> **输出:** { { 1，2，3 }，{ 4，5，6 } }
> **解释** :
> 由于矩阵的大小{ { 1，2，3 }，{ 4，5，6 } }是 A * B(2 * 3)。
> 因此，需要的输出是{ { 1，2，3 }，{ 4，5，6 } }。
> 
> **输入:** mat[][] = { {1，2}，{ 3，4 }，{ 5，6 } }，A = 1，B = 6
> **输出:** { { 1，2，3，4，5，6 } }

**方法:**按照以下步骤解决问题:

*   初始化一个大小为 **A * B** 的矩阵，比如说 **res[][]** 。
*   遍历矩阵， **mat[][]** 并将矩阵的每个元素插入矩阵， **res[][]** 。
*   最后，打印矩阵 **res[][]** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to construct a matrix of size
// A * B from the given matrix elements
void ConstMatrix(int* mat, int N, int M,
                 int A, int B)
{
    if (N * M != A * B)
        return;

    int idx = 0;

    // Initialize a new matrix
    int res[A][B];

    // Traverse the matrix, mat[][]
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            res[idx / B][idx % B] = *((mat + i * M) + j);

            // Update idx
            idx++;
        }
    }

    // Print the resultant matrix
    for(int i = 0; i < A; i++)
    {
        for(int j = 0; j < B; j++)
            cout << res[i][j] << " ";

        cout << "\n";
    }
}

// Driver Code
int main()
{
    int mat[][6] = { { 1, 2, 3, 4, 5, 6 } };
    int A = 2;
    int B = 3;

    int N = sizeof(mat) / sizeof(mat[0]);
    int M = sizeof(mat[0]) / sizeof(int);

    ConstMatrix((int*)mat, N, M, A, B);

    return 0;
}

// This code is contributed by subhammahato348
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to cona matrix of size
// A * B from the given matrix elements
static void ConstMatrix(int[][] mat, int N, int M,
                 int A, int B)
{
    if (N * M != A * B)
        return;

    int idx = 0;

    // Initialize a new matrix
    int [][]res = new int[A][B];

    // Traverse the matrix, mat[][]
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            res[idx / B][idx % B] = mat[i][j];

            // Update idx
            idx++;
        }
    }

    // Print the resultant matrix
    for(int i = 0; i < A; i++)
    {
        for(int j = 0; j < B; j++)
            System.out.print(res[i][j] + " ");           
        System.out.print("\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int mat[][] = { { 1, 2, 3, 4, 5, 6 } };
    int A = 2;
    int B = 3;   
    int N = mat.length;
    int M = mat[0].length;   
    ConstMatrix(mat, N, M, A, B);   
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to construct a matrix of size A * B
# from the given matrix elements
def ConstMatrix(mat, N, M, A, B):
    if (N * M != A * B):
        return -1
    idx = 0;

    # Initialize a new matrix
    res = [[0 for i in range(B)] for i in range(A)]

    # Traverse the matrix, mat[][]
    for i in range(N):
        for j in range(M):
            res[idx//B][idx % B] = mat[i][j];

            # Update idx
            idx += 1

    # Print the resultant matrix
    for i in range(A):
        for j in range(B):
            print(res[i][j], end = " ")
        print()

# Driver Code
if __name__ == '__main__':

    mat = [ [ 1, 2, 3, 4, 5, 6 ] ]
    A = 2
    B = 3
    N = len(mat)
    M = len(mat[0])
    ConstMatrix(mat, N, M, A, B)
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

// Function to cona matrix of size
// A * B from the given matrix elements
static void ConstMatrix(int[,] mat, int N, int M,
                 int A, int B)
{
    if (N * M != A * B)
        return;       
    int idx = 0;

    // Initialize a new matrix
    int [,]res = new int[A,B];

    // Traverse the matrix, [,]mat
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            res[idx / B, idx % B] = mat[i, j];

            // Update idx
            idx++;
        }
    }

    // Print the resultant matrix
    for(int i = 0; i < A; i++)
    {
        for(int j = 0; j < B; j++)
            Console.Write(res[i, j] + " ");           
        Console.Write("\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int [,]mat = {{ 1, 2, 3, 4, 5, 6 }};
    int A = 2;
    int B = 3;   
    int N = mat.GetLength(0);
    int M = mat.GetLength(1);   
    ConstMatrix(mat, N, M, A, B);   
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program of the above approach

// Function to cona matrix of size
// A * B from the given matrix elements
function ConstMatrix(mat, N, M,
                 A, B)
{
    if (N * M != A * B)
        return;

    let idx = 0;

    // Initialize a new matrix
    let res = new Array(A);
    // Loop to create 2D array using 1D array
    for (var i = 0; i < res.length; i++) {
        res[i] = new Array(2);
    }

    // Traverse the matrix, mat[][]
    for(let i = 0; i < N; i++)
    {
        for(let j = 0; j < M; j++)
        {
            res[Math.floor(idx / B)][idx % B] = mat[i][j];

            // Update idx
            idx++;
        }
    }

    // Prlet the resultant matrix
    for(let i = 0; i < A; i++)
    {
        for(let j = 0; j < B; j++)
            document.write(res[i][j] + " ");          
        document.write("<br/>");
    }
}

    // Driver Code

    let mat = [[ 1, 2, 3, 4, 5, 6 ]];
    let A = 2;
    let B = 3;  
    let N = mat.length;
    let M = mat[0].length;  
    ConstMatrix(mat, N, M, A, B);

 // This code is contributed by chinmoy1997pal.
</script>
```

**Output:** 

```
1 2 3 
4 5 6
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*