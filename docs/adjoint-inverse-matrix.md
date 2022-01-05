# 矩阵的伴随和逆

> 原文:[https://www.geeksforgeeks.org/adjoint-inverse-matrix/](https://www.geeksforgeeks.org/adjoint-inverse-matrix/)

给定一个方阵，求矩阵的伴随和逆。
我们强烈建议您将以下内容作为先决条件。
[【矩阵的行列式】](https://www.geeksforgeeks.org/determinant-of-a-matrix/)
**什么是伴随？**
矩阵的伴随(或称附属)是对给定方阵的辅因子矩阵进行转置得到的矩阵，称为它的伴随或附属矩阵。任何方阵‘A’(比如)的伴随都表示为 Adj(A)。
示例:

```
Below example and explanation are taken from here.
5  -2  2  7
1   0  0  3
-3  1  5  0
3  -1 -9  4

For instance, the cofactor of the top left corner '5' is
 + |0   0   3|
...|1   5   0| = 3(1 * -9 - (-1) * 5) = -12.
...|-1 -9   4|
(The minor matrix is formed by deleting the row 
 and column of the given entry.)

As another sample, the cofactor of the top row corner '-2' is
  -|1   0  3|
...|-3  5  0| = - [1 (20 - 0) - 0 + 3 (27 - 15)] = -56.
...|3  -9  4|

Proceeding like this, we obtain the matrix
[-12  -56   4   4]
[76   208   4   4]
[-60  -82  -2  20]
[-36  -58  -10 12]

Finally, to get the adjoint, just take the previous
matrix's transpose:
[-12   76 -60  -36]
[-56  208 -82  -58]
[4     4   -2  -10]
[4     4   20   12] 
```

**重要属性:**

*   正方形矩阵 A 与其伴随矩阵的乘积产生一个对角矩阵，其中每个对角条目等于 A 的行列式
    ，即

```
A.adj(A) = det(A).I 

I  => Identity matrix of same order as of A.
det(A) => Determinant value of A 
```

*   如果存在唯一的 n 阶方阵“B ”,那么 n 阶的非零方阵“A”被称为**可逆的**,

```
   A.B = B.A = I
The matrix 'B' is said to be inverse of 'A'.
i.e.,  B = A-1
```

**如何找到伴随？**
我们遵循上面给出的定义。

```
Let A[N][N] be input matrix.

1) Create a matrix adj[N][N] store the adjoint matrix.
2) For every entry A[i][j] in input matrix where 0 <= i < N
   and 0 <= j < N.
    a) Find cofactor of A[i][j]
    b) Find sign of entry.  Sign is + if (i+j) is even else
       sign is odd.
    c) Place the cofactor at adj[j][i]
```

**如何求逆？**
矩阵的逆只有在矩阵非奇异的情况下才存在，即行列式不应该为 0。
利用行列式和伴随式，我们可以很容易地用下面的公式求出方阵的逆矩阵，

```
  If det(A) != 0
    A-1 = adj(A)/det(A)
  Else
    "Inverse doesn't exist"  
```

逆是用来求线性方程组的解的。
下面是求矩阵的伴随和逆的实现。

## C++

```
// C++ program to find adjoint and inverse of a matrix
#include<bits/stdc++.h>
using namespace std;
#define N 4

// Function to get cofactor of A[p][q] in temp[][]. n is current
// dimension of A[][]
void getCofactor(int A[N][N], int temp[N][N], int p, int q, int n)
{
    int i = 0, j = 0;

    // Looping for each element of the matrix
    for (int row = 0; row < n; row++)
    {
        for (int col = 0; col < n; col++)
        {
            //  Copying into temporary matrix only those element
            //  which are not in given row and column
            if (row != p && col != q)
            {
                temp[i][j++] = A[row][col];

                // Row is filled, so increase row index and
                // reset col index
                if (j == n - 1)
                {
                    j = 0;
                    i++;
                }
            }
        }
    }
}

/* Recursive function for finding determinant of matrix.
   n is current dimension of A[][]. */
int determinant(int A[N][N], int n)
{
    int D = 0; // Initialize result

    //  Base case : if matrix contains single element
    if (n == 1)
        return A[0][0];

    int temp[N][N]; // To store cofactors

    int sign = 1;  // To store sign multiplier

     // Iterate for each element of first row
    for (int f = 0; f < n; f++)
    {
        // Getting Cofactor of A[0][f]
        getCofactor(A, temp, 0, f, n);
        D += sign * A[0][f] * determinant(temp, n - 1);

        // terms are to be added with alternate sign
        sign = -sign;
    }

    return D;
}

// Function to get adjoint of A[N][N] in adj[N][N].
void adjoint(int A[N][N],int adj[N][N])
{
    if (N == 1)
    {
        adj[0][0] = 1;
        return;
    }

    // temp is used to store cofactors of A[][]
    int sign = 1, temp[N][N];

    for (int i=0; i<N; i++)
    {
        for (int j=0; j<N; j++)
        {
            // Get cofactor of A[i][j]
            getCofactor(A, temp, i, j, N);

            // sign of adj[j][i] positive if sum of row
            // and column indexes is even.
            sign = ((i+j)%2==0)? 1: -1;

            // Interchanging rows and columns to get the
            // transpose of the cofactor matrix
            adj[j][i] = (sign)*(determinant(temp, N-1));
        }
    }
}

// Function to calculate and store inverse, returns false if
// matrix is singular
bool inverse(int A[N][N], float inverse[N][N])
{
    // Find determinant of A[][]
    int det = determinant(A, N);
    if (det == 0)
    {
        cout << "Singular matrix, can't find its inverse";
        return false;
    }

    // Find adjoint
    int adj[N][N];
    adjoint(A, adj);

    // Find Inverse using formula "inverse(A) = adj(A)/det(A)"
    for (int i=0; i<N; i++)
        for (int j=0; j<N; j++)
            inverse[i][j] = adj[i][j]/float(det);

    return true;
}

// Generic function to display the matrix.  We use it to display
// both adjoin and inverse. adjoin is integer matrix and inverse
// is a float.
template<class T>
void display(T A[N][N])
{
    for (int i=0; i<N; i++)
    {
        for (int j=0; j<N; j++)
            cout << A[i][j] << " ";
        cout << endl;
    }
}

// Driver program
int main()
{
    int A[N][N] = { {5, -2, 2, 7},
                    {1, 0, 0, 3},
                    {-3, 1, 5, 0},
                    {3, -1, -9, 4}};

    int adj[N][N];  // To store adjoint of A[][]

    float inv[N][N]; // To store inverse of A[][]

    cout << "Input matrix is :\n";
    display(A);

    cout << "\nThe Adjoint is :\n";
    adjoint(A, adj);
    display(adj);

    cout << "\nThe Inverse is :\n";
    if (inverse(A, inv))
        display(inv);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find adjoint and inverse of a matrix
class GFG
{

static final int N = 4;

// Function to get cofactor of A[p][q] in temp[][]. n is current
// dimension of A[][]
static void getCofactor(int A[][], int temp[][], int p, int q, int n)
{
    int i = 0, j = 0;

    // Looping for each element of the matrix
    for (int row = 0; row < n; row++)
    {
        for (int col = 0; col < n; col++)
        {
            // Copying into temporary matrix only those element
            // which are not in given row and column
            if (row != p && col != q)
            {
                temp[i][j++] = A[row][col];

                // Row is filled, so increase row index and
                // reset col index
                if (j == n - 1)
                {
                    j = 0;
                    i++;
                }
            }
        }
    }
}

/* Recursive function for finding determinant of matrix.
n is current dimension of A[][]. */
static int determinant(int A[][], int n)
{
    int D = 0; // Initialize result

    // Base case : if matrix contains single element
    if (n == 1)
        return A[0][0];

    int [][]temp = new int[N][N]; // To store cofactors

    int sign = 1; // To store sign multiplier

    // Iterate for each element of first row
    for (int f = 0; f < n; f++)
    {
        // Getting Cofactor of A[0][f]
        getCofactor(A, temp, 0, f, n);
        D += sign * A[0][f] * determinant(temp, n - 1);

        // terms are to be added with alternate sign
        sign = -sign;
    }

    return D;
}

// Function to get adjoint of A[N][N] in adj[N][N].
static void adjoint(int A[][],int [][]adj)
{
    if (N == 1)
    {
        adj[0][0] = 1;
        return;
    }

    // temp is used to store cofactors of A[][]
    int sign = 1;
    int [][]temp = new int[N][N];

    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {
            // Get cofactor of A[i][j]
            getCofactor(A, temp, i, j, N);

            // sign of adj[j][i] positive if sum of row
            // and column indexes is even.
            sign = ((i + j) % 2 == 0)? 1: -1;

            // Interchanging rows and columns to get the
            // transpose of the cofactor matrix
            adj[j][i] = (sign)*(determinant(temp, N-1));
        }
    }
}

// Function to calculate and store inverse, returns false if
// matrix is singular
static boolean inverse(int A[][], float [][]inverse)
{
    // Find determinant of A[][]
    int det = determinant(A, N);
    if (det == 0)
    {
        System.out.print("Singular matrix, can't find its inverse");
        return false;
    }

    // Find adjoint
    int [][]adj = new int[N][N];
    adjoint(A, adj);

    // Find Inverse using formula "inverse(A) = adj(A)/det(A)"
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            inverse[i][j] = adj[i][j]/(float)det;

    return true;
}

// Generic function to display the matrix. We use it to display
// both adjoin and inverse. adjoin is integer matrix and inverse
// is a float.

static void display(int A[][])
{
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
            System.out.print(A[i][j]+ " ");
        System.out.println();
    }
}
static void display(float A[][])
{
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
            System.out.printf("%.6f ",A[i][j]);
        System.out.println();
    }
}

// Driver program
public static void main(String[] args)
{
    int A[][] = { {5, -2, 2, 7},
                    {1, 0, 0, 3},
                    {-3, 1, 5, 0},
                    {3, -1, -9, 4}};

    int [][]adj = new int[N][N]; // To store adjoint of A[][]

    float [][]inv = new float[N][N]; // To store inverse of A[][]

    System.out.print("Input matrix is :\n");
    display(A);

    System.out.print("\nThe Adjoint is :\n");
    adjoint(A, adj);
    display(adj);

    System.out.print("\nThe Inverse is :\n");
    if (inverse(A, inv))
        display(inv);

}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# program to find adjoint and inverse of a matrix
using System;
using System.Collections.Generic;

class GFG
{

static readonly int N = 4;

// Function to get cofactor of A[p,q] in [,]temp. n is current
// dimension of [,]A
static void getCofactor(int [,]A, int [,]temp, int p, int q, int n)
{
    int i = 0, j = 0;

    // Looping for each element of the matrix
    for (int row = 0; row < n; row++)
    {
        for (int col = 0; col < n; col++)
        {
            // Copying into temporary matrix only those element
            // which are not in given row and column
            if (row != p && col != q)
            {
                temp[i, j++] = A[row, col];

                // Row is filled, so increase row index and
                // reset col index
                if (j == n - 1)
                {
                    j = 0;
                    i++;
                }
            }
        }
    }
}

/* Recursive function for finding determinant of matrix.
n is current dimension of [,]A. */
static int determinant(int [,]A, int n)
{
    int D = 0; // Initialize result

    // Base case : if matrix contains single element
    if (n == 1)
        return A[0, 0];

    int [,]temp = new int[N, N]; // To store cofactors

    int sign = 1; // To store sign multiplier

    // Iterate for each element of first row
    for (int f = 0; f < n; f++)
    {
        // Getting Cofactor of A[0,f]
        getCofactor(A, temp, 0, f, n);
        D += sign * A[0, f] * determinant(temp, n - 1);

        // terms are to be added with alternate sign
        sign = -sign;
    }
    return D;
}

// Function to get adjoint of A[N,N] in adj[N,N].
static void adjoint(int [,]A, int [,]adj)
{
    if (N == 1)
    {
        adj[0, 0] = 1;
        return;
    }

    // temp is used to store cofactors of [,]A
    int sign = 1;
    int [,]temp = new int[N, N];

    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
        {
            // Get cofactor of A[i,j]
            getCofactor(A, temp, i, j, N);

            // sign of adj[j,i] positive if sum of row
            // and column indexes is even.
            sign = ((i + j) % 2 == 0)? 1: -1;

            // Interchanging rows and columns to get the
            // transpose of the cofactor matrix
            adj[j, i] = (sign) * (determinant(temp, N - 1));
        }
    }
}

// Function to calculate and store inverse, returns false if
// matrix is singular
static bool inverse(int [,]A, float [,]inverse)
{
    // Find determinant of [,]A
    int det = determinant(A, N);
    if (det == 0)
    {
        Console.Write("Singular matrix, can't find its inverse");
        return false;
    }

    // Find adjoint
    int [,]adj = new int[N, N];
    adjoint(A, adj);

    // Find Inverse using formula "inverse(A) = adj(A)/det(A)"
    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            inverse[i, j] = adj[i, j]/(float)det;

    return true;
}

// Generic function to display the matrix. We use it to display
// both adjoin and inverse. adjoin is integer matrix and inverse
// is a float.
static void display(int [,]A)
{
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
            Console.Write(A[i, j]+ " ");
        Console.WriteLine();
    }
}
static void display(float [,]A)
{
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < N; j++)
            Console.Write("{0:F6} ", A[i, j]);
        Console.WriteLine();
    }
}

// Driver program
public static void Main(String[] args)
{
    int [,]A = { {5, -2, 2, 7},
                    {1, 0, 0, 3},
                    {-3, 1, 5, 0},
                    {3, -1, -9, 4}};

    int [,]adj = new int[N, N]; // To store adjoint of [,]A

    float [,]inv = new float[N, N]; // To store inverse of [,]A

    Console.Write("Input matrix is :\n");
    display(A);

    Console.Write("\nThe Adjoint is :\n");
    adjoint(A, adj);
    display(adj);

    Console.Write("\nThe Inverse is :\n");
    if (inverse(A, inv))
        display(inv);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find adjoint and
// inverse of a matrix

let N = 4;
// Function to get cofactor of
// A[p][q] in temp[][]. n is current
// dimension of A[][]
function getCofactor(A,temp,p,q,n)
{
    let i = 0, j = 0;

    // Looping for each element of the matrix
    for (let row = 0; row < n; row++)
    {
        for (let col = 0; col < n; col++)
        {
            // Copying into temporary matrix only those element
            // which are not in given row and column
            if (row != p && col != q)
            {
                temp[i][j++] = A[row][col];

                // Row is filled, so increase row index and
                // reset col index
                if (j == n - 1)
                {
                    j = 0;
                    i++;
                }
            }
        }
    }
}

/* Recursive function for finding determinant of matrix.
n is current dimension of A[][]. */
function determinant(A,n)
{
    let D = 0; // Initialize result

    // Base case : if matrix contains single element
    if (n == 1)
        return A[0][0];

    let temp = new Array(N);// To store cofactors
    for(let i=0;i<N;i++)
    {
        temp[i]=new Array(N);
    }

    let sign = 1; // To store sign multiplier

    // Iterate for each element of first row
    for (let f = 0; f < n; f++)
    {
        // Getting Cofactor of A[0][f]
        getCofactor(A, temp, 0, f, n);
        D += sign * A[0][f] * determinant(temp, n - 1);

        // terms are to be added with alternate sign
        sign = -sign;
    }

    return D;
}

// Function to get adjoint of A[N][N] in adj[N][N].
function  adjoint(A,adj)
{
    if (N == 1)
    {
        adj[0][0] = 1;
        return;
    }

    // temp is used to store cofactors of A[][]
    let sign = 1;
    let temp = new Array(N);
    for(let i=0;i<N;i++)
    {
        temp[i]=new Array(N);
    }

    for (let i = 0; i < N; i++)
    {
        for (let j = 0; j < N; j++)
        {
            // Get cofactor of A[i][j]
            getCofactor(A, temp, i, j, N);

            // sign of adj[j][i] positive if sum of row
            // and column indexes is even.
            sign = ((i + j) % 2 == 0)? 1: -1;

            // Interchanging rows and columns to get the
            // transpose of the cofactor matrix
            adj[j][i] = (sign)*(determinant(temp, N-1));
        }
    }
}

// Function to calculate and store inverse, returns false if
// matrix is singular
function inverse(A,inverse)
{
    // Find determinant of A[][]
    let det = determinant(A, N);
    if (det == 0)
    {
        document.write("Singular matrix, can't find its inverse");
        return false;
    }

    // Find adjoint
    let adj = new Array(N);
    for(let i=0;i<N;i++)
    {
        adj[i]=new Array(N);
    }
    adjoint(A, adj);

    // Find Inverse using formula "inverse(A) = adj(A)/det(A)"
    for (let i = 0; i < N; i++)
        for (let j = 0; j < N; j++)
            inverse[i][j] = adj[i][j]/det;

    return true;
}

// Generic function to display the
// matrix. We use it to display
// both adjoin and inverse. adjoin
// is integer matrix and inverse
// is a float.
function display(A)
{
    for (let i = 0; i < N; i++)
    {
        for (let j = 0; j < N; j++)
            document.write(A[i][j]+ " ");
        document.write("<br>");
    }
}

function displays(A)
{
    for (let i = 0; i < N; i++)
    {
        for (let j = 0; j < N; j++)
            document.write(A[i][j].toFixed(6)+" ");
        document.write("<br>");
    }
}

// Driver program
let A=[[5, -2, 2, 7],
                    [1, 0, 0, 3],
                    [-3, 1, 5, 0],
                    [3, -1, -9, 4]];
let adj = new Array(N);
let inv = new Array(N);

for(let i=0;i<N;i++)
{
    adj[i]=new Array(N);
    inv[i]=new Array(N);
}

document.write("Input matrix is :<br>");
display(A);

document.write("<br>The Adjoint is :<br>");
adjoint(A, adj);
display(adj);

document.write("<br>The Inverse is :<br>");
if (inverse(A, inv))
    displays(inv);

// This code is contributed by rag2127

</script>
```

**输出:**

```
The Adjoint is :
-12 76 -60 -36 
-56 208 -82 -58 
4 4 -2 -10 
4 4 20 12 

The Inverse is :
-0.136364 0.863636 -0.681818 -0.409091 
-0.636364 2.36364 -0.931818 -0.659091 
0.0454545 0.0454545 -0.0227273 -0.113636 
0.0454545 0.0454545 0.227273 0.136364
```

getCofactor()和行列式()的详细内容请参考[https://www.geeksforgeeks.org/determinant-of-a-matrix/](https://www.geeksforgeeks.org/determinant-of-a-matrix/)。
参考文献:
[https://www.geeksforgeeks.org/determinant-of-a-matrix/](https://www.geeksforgeeks.org/determinant-of-a-matrix/)
[https://en.wikipedia.org/wiki/Adjugate_matrix](https://en.wikipedia.org/wiki/Adjugate_matrix)
本文由**阿舒托什·库马尔**供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息