# 检查矩阵是否为单数的程序

> 原文:[https://www . geesforgeks . org/program-check-matrix-单数-not/](https://www.geeksforgeeks.org/program-check-matrix-singular-not/)

如果矩阵的行列式为 0，则称该矩阵为奇异矩阵，否则称该矩阵为非奇异矩阵。
示例:

```
Input :  0 0 0
         4 5 6
         1 2 3
Output : Yes
Determinant value of the matrix is
0 (Note first row is 0)

Input :  1 0 0
         4 5 6
         1 2 3
Output : No
Determinant value of the matrix is 3
(which is non-zero).
```

首先求出矩阵的[行列式，检查行列式是否为 0，如果为 0，则矩阵为奇异矩阵，否则为非奇异矩阵。](https://www.geeksforgeeks.org/determinant-of-a-matrix/) 

## C++

```
// C++ program check if a matrix is
// singular or not.
#include <bits/stdc++.h>
using namespace std;
#define N 4

// Function to get cofactor of mat[p][q] in temp[][].
// n is current dimension of mat[][]
void getCofactor(int mat[N][N], int temp[N][N], int p,
                                         int q, int n)
{
    int i = 0, j = 0;

    // Looping for each element of the matrix
    for (int row = 0; row < n; row++) {
        for (int col = 0; col < n; col++) {

            // Copying into temporary matrix only
            // those element which are not in given
            // row and column
            if (row != p && col != q) {
                temp[i][j++] = mat[row][col];

                // Row is filled, so increase row
                // index and reset col index
                if (j == n - 1) {
                    j = 0;
                    i++;
                }
            }
        }
    }
}

/* Recursive function to check if mat[][] is
   singular or not. */
bool isSingular(int mat[N][N], int n)
{
    int D = 0; // Initialize result

    // Base case : if matrix contains single element
    if (n == 1)
        return mat[0][0];

    int temp[N][N]; // To store cofactors

    int sign = 1; // To store sign multiplier

    // Iterate for each element of first row
    for (int f = 0; f < n; f++) {

        // Getting Cofactor of mat[0][f]
        getCofactor(mat, temp, 0, f, n);
        D += sign * mat[0][f] * isSingular(temp, n - 1);

        // terms are to be added with alternate sign
        sign = -sign;
    }

    return D;
}

// Driver program to test above functions
int main()
{
    int mat[N][N] = { { 4, 10, 1 },
                      { 0, 0, 0 },
                      { 1, 4, -3 } };
    if (isSingular(mat, N))
        cout << "Matrix is Singular" << endl;
    else
        cout << "Matrix is non-singular" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program check if a matrix is
// singular or not.
class GFG
{

    static final int N = 3;

    // Function to get cofactor of mat[p][q] in temp[][].
    // n is current dimension of mat[][]
    static void getCofactor(int mat[][], int temp[][], int p,
                                              int q, int n)
    {
        int i = 0, j = 0;

        // Looping for each element of the matrix
        for (int row = 0; row < n; row++)
        {
            for (int col = 0; col < n; col++)
            {

                // Copying into temporary matrix only
                // those element which are not in given
                // row and column
                if (row != p && col != q)
                {
                    temp[i][j++] = mat[row][col];

                    // Row is filled, so increase row
                    // index and reset col index
                    if (j == n - 1)
                    {
                        j = 0;
                        i++;
                    }
                }
            }
        }
    }

    /* Recursive function to check if mat[][] is
    singular or not. */
    static int isSingular(int mat[][], int n)
    {
        int D = 0; // Initialize result

        // Base case : if matrix contains single element
        if (n == 1)
        {
            return mat[0][0];
        }

        int temp[][] = new int[N][N]; // To store cofactors

        int sign = 1; // To store sign multiplier

        // Iterate for each element of first row
        for (int f = 0; f < n; f++)
        {

            // Getting Cofactor of mat[0][f]
            getCofactor(mat, temp, 0, f, n);
            D += sign * mat[0][f] * isSingular(temp, n - 1);

            // terms are to be added with alternate sign
            sign = -sign;
        }

        return D;
    }

    // Driver code
    public static void main(String[] args)
    {
        int mat[][] = {{4, 10, 1},
                        {0, 0, 0},
                        {1, 4, -3}};
        if (isSingular(mat, N) == 1)
        {
            System.out.println("Matrix is Singular");
        }
        else
        {
            System.out.println("Matrix is non-singular");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# python 3 program check if a matrix is
# singular or not.
global N
N = 3

# Function to get cofactor of mat[p][q] in temp[][].
# n is current dimension of mat[][]
def getCofactor(mat,temp,p,q,n):
    i = 0
    j = 0

    # Looping for each element of the matrix
    for row in range(n):
        for col in range(n):

            # Copying into temporary matrix only
            # those element which are not in given
            # row and column
            if (row != p and col != q):
                temp[i][j] = mat[row][col]
                j += 1

                # Row is filled, so increase row
                # index and reset col index
                if (j == n - 1):
                    j = 0
                    i += 1

# Recursive function to check if mat[][] is
# singular or not. */
def isSingular(mat,n):
    D = 0 # Initialize result

    # Base case : if matrix contains single element
    if (n == 1):
        return mat[0][0]

    temp = [[0 for i in range(N + 1)] for i in range(N + 1)]# To store cofactors

    sign = 1 # To store sign multiplier

    # Iterate for each element of first row
    for f in range(n):

        # Getting Cofactor of mat[0][f]
        getCofactor(mat, temp, 0, f, n)
        D += sign * mat[0][f] * isSingular(temp, n - 1)

        # terms are to be added with alternate sign
        sign = -sign
    return D

# Driver program to test above functions
if __name__ == '__main__':
    mat = [[4, 10, 1],[0, 0, 0],[1, 4, -3]]
    if (isSingular(mat, N)):
        print("Matrix is Singular")
    else:
        print("Matrix is non-singular")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program check if a matrix is
// singular or not.
using System;

class GFG
{

    static readonly int N = 3;

    // Function to get cofactor of mat[p,q] in temp[,].
    // n is current dimension of mat[,]
    static void getCofactor(int [,]mat, int [,]temp, int p,
                                            int q, int n)
    {
        int i = 0, j = 0;

        // Looping for each element of the matrix
        for (int row = 0; row < n; row++)
        {
            for (int col = 0; col < n; col++)
            {

                // Copying into temporary matrix only
                // those element which are not in given
                // row and column
                if (row != p && col != q)
                {
                    temp[i, j++] = mat[row, col];

                    // Row is filled, so increase row
                    // index and reset col index
                    if (j == n - 1)
                    {
                        j = 0;
                        i++;
                    }
                }
            }
        }
    }

    /* Recursive function to check if mat[,] is
    singular or not. */
    static int isSingular(int [,]mat, int n)
    {
        int D = 0; // Initialize result

        // Base case : if matrix contains single element
        if (n == 1)
        {
            return mat[0, 0];
        }

        int [,]temp = new int[N, N]; // To store cofactors

        int sign = 1; // To store sign multiplier

        // Iterate for each element of first row
        for (int f = 0; f < n; f++)
        {

            // Getting Cofactor of mat[0,f]
            getCofactor(mat, temp, 0, f, n);
            D += sign * mat[0, f] * isSingular(temp, n - 1);

            // terms are to be added with alternate sign
            sign = -sign;
        }

        return D;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int [,]mat = {{4, 10, 1},
                        {0, 0, 0},
                        {1, 4, -3}};
        if (isSingular(mat, N) == 1)
        {
            Console.WriteLine("Matrix is Singular");
        }
        else
        {
            Console.WriteLine("Matrix is non-singular");
        }
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program check if a matrix is
// singular or not.
var N = 3;
// Function to get cofactor of mat[p,q] in temp[,].
// n is current dimension of mat[,]
function getCofactor(mat, temp, p, q, n)
{
    var i = 0, j = 0;
    // Looping for each element of the matrix
    for (var row = 0; row < n; row++)
    {
        for (var col = 0; col < n; col++)
        {
            // Copying into temporary matrix only
            // those element which are not in given
            // row and column
            if (row != p && col != q)
            {
                temp[i][j++] = mat[row][col];
                // Row is filled, so increase row
                // index and reset col index
                if (j == n - 1)
                {
                    j = 0;
                    i++;
                }
            }
        }
    }
}
/* Recursive function to check if mat[,] is
singular or not. */
function isSingular(mat, n)
{
    var D = 0; // Initialize result
    // Base case : if matrix contains single element
    if (n == 1)
    {
        return mat[0][0];
    }
    var temp = Array.from(Array(N), ()=>Array(N));// To store cofactors
    var sign = 1; // To store sign multiplier
    // Iterate for each element of first row
    for(var f = 0; f < n; f++)
    {
        // Getting Cofactor of mat[0,f]
        getCofactor(mat, temp, 0, f, n);
        D += sign * mat[0][f] * isSingular(temp, n - 1);
        // terms are to be added with alternate sign
        sign = -sign;
    }
    return D;
}
// Driver code
var mat = [[4, 10, 1],
                [0, 0, 0],
                [1, 4, -3]];
if (isSingular(mat, N) == 1)
{
    document.write("Matrix is Singular");
}
else
{
    document.write("Matrix is non-singular");
}

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
Matrix is non-singular
```