# 打印矩阵链乘法(一种空间优化解决方案)

> 原文:[https://www . geesforgeks . org/printing-matrix-chain-乘法-a-space-optimized-solution/](https://www.geeksforgeeks.org/printing-matrix-chain-multiplication-a-space-optimized-solution/)

先决条件:[动态规划|集合 8(矩阵链乘法)](https://www.geeksforgeeks.org/dynamic-programming-set-8-matrix-chain-multiplication/)
给定一个矩阵序列，找到将这些矩阵相乘的最有效方法。问题不在于实际执行乘法，而仅仅在于决定以何种顺序执行乘法。

我们有很多选择来乘矩阵链，因为矩阵乘法是关联的。换句话说，无论我们如何给产品加上括号，结果都是一样的。例如，如果我们有四个矩阵 A、B、C 和 D，我们会有:

```
    (ABC)D = (AB)(CD) = A(BCD) = ....

```

然而，我们给乘积加括号的顺序会影响计算乘积所需的简单算术运算的次数或效率。例如，假设 A 是 10 × 30 矩阵，B 是 30 × 5 矩阵，C 是 5 × 60 矩阵。然后，

```
    (AB)C = (10×30×5) + (10×5×60) = 1500 + 3000 = 4500 operations
    A(BC) = (30×5×60) + (10×30×60) = 9000 + 18000 = 27000 operations.

```

显然，第一个括号需要较少的操作次数。

*给定一个表示矩阵链的数组 p[]，使得矩阵 Ai 的维数为 p[i-1] x p[i]。我们需要编写一个 MatrixChainOrder()函数，该函数应该返回乘法链所需的最小乘法次数。*

```
  Input:  p[] = {40, 20, 30, 10, 30}  
  Output: Optimal parenthesization is  ((A(BC))D)
          Optimal cost of parenthesization is 26000
  There are 4 matrices of dimensions 40x20, 20x30, 30x10 and 10x30.
  Let the input 4 matrices be A, B, C, and D.  The minimum number of 
  multiplications are obtained by putting the parenthesis in the following way
  (A(BC))D --> 20*30*10 + 40*20*10 + 40*10*30

  Input: p[] = {10, 20, 30, 40, 30} 
  Output: Optimal parenthesization is (((AB)C)D)
          Optimal cost of parenthesization is 30000
  There are 4 matrices of dimensions 10x20, 20x30, 30x40 and 40x30\. 
  Let the input 4 matrices be A, B, C, and D.  The minimum number of 
  multiplications are obtained by putting the parenthesis in the following way
  ((AB)C)D --> 10*20*30 + 10*30*40 + 10*40*30

  Input: p[] = {10, 20, 30} 
  Output: Optimal parenthesization is (AB)
          Optimal cost of parenthesization is 6000
  There are only two matrices of dimensions 10x20 and 20x30\. So there 
  is only one way to multiply the matrices, the cost of which is 10*20*30

```

这个问题主要是[求矩阵链乘](https://www.geeksforgeeks.org/dynamic-programming-set-8-matrix-chain-multiplication/)最优成本的一个延伸。这里我们还需要打印括号。

我们在一篇帖子中讨论了一个使用两个矩阵的解决方案。在这篇文章中，讨论了一个使用单一矩阵的空间优化解决方案。
1)为了找到最优成本，我们创建了一个矩阵，该矩阵只有上三角被填充，其余的单元没有被使用。
2)思路是用同一个矩阵的下三角部分(不使用的部分)存放括号。
想法是在 m [ j ][ i ]存储每个子表达式(I，j)的最优断点，在 m [ i ] [ j ]存储最优成本。

下面是以上步骤的实现。

## C++

```
// A space optimized C++ program to print optimal
// parenthesization in matrix chain multiplication.
#include<bits/stdc++.h>
using namespace std;

// Function for printing the optimal
// parenthesization of a matrix chain product
void printParenthesis(int i, int j, int n,
                      int *bracket, char &name)
{
    // If only one matrix left in current segment
    if (i == j)
    {
        cout << name++;
        return;
    }

    cout << "(";

    // Recursively put brackets around subexpression
    // from i to bracket[j][i].
    // Note that "*((bracket+j*n)+i)" is similar to
    // bracket[j][i]
    printParenthesis(i, *((bracket+j*n)+i), n,
                     bracket, name);

    // Recursively put brackets around subexpression
    // from bracket[j][i] + 1 to i.
    printParenthesis(*((bracket+j*n)+i) + 1, j,
                     n, bracket, name);
    cout << ")";
}

// Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
// Please refer below article for details of this
// function
// https://goo.gl/k6EYKj
void matrixChainOrder(int p[], int n)
{
    /* For simplicity of the program, one extra
       row and one extra column are allocated in
        m[][]. 0th row and 0th column of m[][]
        are not used */
    int m[n][n];

    /* m[i,j] = Minimum number of scalar multiplications
    needed to compute the matrix A[i]A[i+1]...A[j] =
    A[i..j] where dimension of A[i] is p[i-1] x p[i] */

    // cost is zero when multiplying one matrix.
    for (int i=1; i<n; i++)
        m[i][i] = 0;

    // L is chain length.
    for (int L=2; L<n; L++)
    {
        for (int i=1; i<n-L+1; i++)
        {
            int j = i+L-1;
            m[i][j] = INT_MAX;
            for (int k=i; k<=j-1; k++)
            {
                // q = cost/scalar multiplications
                int q = m[i][k] + m[k+1][j] + p[i-1]*p[k]*p[j];
                if (q < m[i][j])
                {
                    m[i][j] = q;

                    // Each entry m[j,ji=k shows
                    // where to split the product arr
                    // i,i+1....j for the minimum cost.
                    m[j][i] = k;
                }
            }
        }
    }

    // The first matrix is printed as 'A', next as 'B',
    // and so on
    char name = 'A';

    cout << "Optimal Parenthesization is: ";
    printParenthesis(1, n-1, n, (int *)m, name);
    cout << "\nOptimal Cost is : " << m[1][n-1];
}

// Driver code
int main()
{
    int arr[] = {40, 20, 30, 10, 30};
    int n = sizeof(arr)/sizeof(arr[0]);
    matrixChainOrder(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A space optimized Java program to print optimal
// parenthesization in matrix chain multiplication.
import java.util.*;

class GFG
{

    static char name;

    // Function for printing the optimal
    // parenthesization of a matrix chain product
    static void printParenthesis(int i, int j, int n, int[][] bracket)
    {
        // If only one matrix left in current segment
        if (i == j)
        {
            System.out.print(name++);
            return;
        }

        System.out.print('(');

        // Recursively put brackets around subexpression
        // from i to bracket[j][i].
        // Note that "*((bracket+j*n)+i)" is similar to
        // bracket[i][j]
        printParenthesis(i, bracket[j][i], n, bracket);

        // Recursively put brackets around subexpression
        // from bracket[j][i] + 1 to i.
        printParenthesis(bracket[j][i] + 1, j, n, bracket);

        System.out.print(')');
    }

    // Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
    // Please refer below article for details of this
    // function
    // https://goo.gl/k6EYKj
    static void matrixChainOrder(int[] p, int n)
    {

        /*
        * For simplicity of the program, one extra row and one extra column are
        * allocated in m[][]. 0th row and 0th column of m[][] are not used
        */
        int[][] m = new int[n][n];

        /*
        * m[i,j] = Minimum number of scalar multiplications needed to compute the
        * matrix A[i]A[i+1]...A[j] = A[i..j] where dimension of A[i] is p[i-1] x p[i]
        */

        // cost is zero when multiplying one matrix.
        for (int L = 2; L < n; L++)
        {
            for (int i = 1; i < n - L + 1; i++)
            {
                int j = i + L - 1;
                m[i][j] = Integer.MAX_VALUE;
                for (int k = i; k <= j - 1; k++)
                {

                    // q = cost/scalar multiplications
                    int q = m[i][k] + m[k + 1][j] + p[i - 1] * p[k] * p[j];
                    if (q < m[i][j])
                    {
                        m[i][j] = q;

                        // Each entry m[j,ji=k shows
                        // where to split the product arr
                        // i,i+1....j for the minimum cost.
                        m[j][i] = k;
                    }
                }
            }
        }

        // The first matrix is printed as 'A', next as 'B',
        // and so on
        name = 'A';

        System.out.print("Optimal Parenthesization is: ");
        printParenthesis(1, n - 1, n, m);
        System.out.print("\nOptimal Cost is :" + m[1][n - 1]);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 40, 20, 30, 10, 30 };
        int n = arr.length;
        matrixChainOrder(arr, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# A space optimized python3 program to
# print optimal parenthesization in
# matrix chain multiplication.

def printParenthesis(m, j, i ):

    # Displaying the parenthesis.
    if j == i:

        # The first matrix is printed as
        # 'A', next as 'B', and so on
        print(chr(65 + j), end = "")
        return;
    else:
        print("(", end = "")

        # Passing (m, k, i) instead of (s, i, k)
        printParenthesis(m, m[j][i] - 1, i)

        # (m, j, k+1) instead of (s, k+1, j)
        printParenthesis(m, j, m[j][i])
        print (")", end = "" )

def matrixChainOrder(p, n):

    # Creating a matrix of order
    # n*n in the memory.
    m = [[0 for i in range(n)]
            for i in range (n)]

    for l in range (2, n + 1):
        for i in range (n - l + 1):
            j = i + l - 1

            # Initializing infinity value.
            m[i][j] = float('Inf')
            for k in range (i, j):
                q = (m[i][k] + m[k + 1][j] +
                    (p[i] * p[k + 1] * p[j + 1]));
                if (q < m[i][j]):
                    m[i][j] = q

                    # Storing k value in opposite index.
                    m[j][i] = k + 1
    return m;

# Driver Code
arr = [40, 20, 30, 10, 30]
n = len(arr) - 1

m = matrixChainOrder(arr, n) # Forming the matrix m

print("Optimal Parenthesization is: ", end = "")

# Passing the index of the bottom left
# corner of the 'm' matrix instead of
# passing the index of the top right
# corner of the 's' matrix as we used
# to do earlier. Everything is just opposite
# as we are using the bottom half of the
# matrix so assume everything opposite even
# the index, take m[j][i].
printParenthesis(m, n - 1, 0)
print("\nOptimal Cost is :", m[0][n - 1])

# This code is contributed by Akash Gupta.
```

## C#

```
// A space optimized C# program to print optimal
// parenthesization in matrix chain multiplication.
using System;

class GFG{

static char name;

// Function for printing the optimal
// parenthesization of a matrix chain product
static void printParenthesis(int i, int j,
                             int n, int[,] bracket)
{

    // If only one matrix left in current segment
    if (i == j)
    {
        Console.Write(name++);
        return;
    }

    Console.Write('(');

    // Recursively put brackets around subexpression
    // from i to bracket[j,i].
    // Note that "*((bracket+j*n)+i)" is similar to
    // bracket[i,j]
    printParenthesis(i, bracket[j, i], n, bracket);

    // Recursively put brackets around subexpression
    // from bracket[j,i] + 1 to i.
    printParenthesis(bracket[j, i] + 1, j, n, bracket);

    Console.Write(')');
}

// Matrix Ai has dimension p[i-1] x p[i] for i = 1..n
// Please refer below article for details of this
// function
// https://goo.gl/k6EYKj
static void matrixChainOrder(int[] p, int n)
{

    /*
    * For simplicity of the program, one extra
    * row and one extra column are
    * allocated in m[,]. 0th row and 0th
    * column of m[,] are not used
    */
    int[,] m = new int[n, n];

    /*
    * m[i,j] = Minimum number of scalar
    * multiplications needed to compute the
    * matrix A[i]A[i+1]...A[j] = A[i..j]
    * where dimension of A[i] is p[i-1] x p[i]
    */

    // Cost is zero when multiplying one matrix.
    for(int L = 2; L < n; L++)
    {
        for(int i = 1; i < n - L + 1; i++)
        {
            int j = i + L - 1;
            m[i, j] = int.MaxValue;

            for(int k = i; k <= j - 1; k++)
            {

                // q = cost/scalar multiplications
                int q = m[i, k] + m[k + 1, j] +
                        p[i - 1] * p[k] * p[j];

                if (q < m[i, j])
                {
                    m[i, j] = q;

                    // Each entry m[j,ji=k shows
                    // where to split the product arr
                    // i,i+1....j for the minimum cost.
                    m[j, i] = k;
                }
            }
        }
    }

    // The first matrix is printed as 'A', next as 'B',
    // and so on
    name = 'A';

    Console.Write("Optimal Parenthesization is: ");
    printParenthesis(1, n - 1, n, m);
    Console.Write("\nOptimal Cost is :" + m[1, n - 1]);
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 40, 20, 30, 10, 30 };
    int n = arr.Length;

    matrixChainOrder(arr, n);
}
}

// This code is contributed by Princi Singh
```

**Output:** 

```
Optimal Parenthesization is : ((A(BC))D)
Optimal Cost is : 26000

```

**时间复杂度:**o(n^3)
T3】辅助空间: O(n^2):这个渐近值保持不变，但是我们把辅助空间减少到一半。