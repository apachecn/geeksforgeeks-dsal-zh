# 生成一个矩阵，使得给定的矩阵元素等于所生成矩阵的所有相应行和列元素的按位或

> 原文:[https://www . geeksforgeeks . org/generate-a-matrix-so-给定矩阵元素等于生成矩阵的所有对应行和列元素的按位或/](https://www.geeksforgeeks.org/generate-a-matrix-such-that-given-matrix-elements-are-equal-to-bitwise-or-of-all-corresponding-row-and-column-elements-of-generated-matrix/)

给定尺寸为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **B[][]** ，任务是生成相同尺寸的矩阵 **A[][]** ，该矩阵可以被形成为使得对于任何元素 **B[i][j]** 等于 **i <sup>th</sup>** 行和 **j <sup>th</sup>** 列中所有元素的[按位 OR](https://www.geeksforgeeks.org/Bitwise-operators-in-c-cpp/) 如果不存在这样的矩阵，打印“**不可能**”。否则，打印矩阵 **A[][]** 。

**示例:**

> **输入:** B[][] = {{1，1，1}，{1，1，1}}
> **输出:**
> 1 1 1
> 1 1
> T8】说明:
> B[0][0]= 1 = A[][]第 0 行第 0 列所有元素的按位 OR。
> B[0][1]= 1 = A[][]第 0 行第 1 列所有元素的按位 OR。
> B[0][2]= 1 = A[][]第 0 行第 2 列所有元素的按位 OR。
> B[1][0]= 1 = A[][]第 1 行第 0 列所有元素的按位 OR。
> B[1][1]= 1 = A[][]第 1 行第 1 列所有元素的按位 OR。
> B[1][2]= 1 = A[][]第 1 行第 2 列所有元素的按位 OR。
> 
> **输入:** B[][] = {{1，0，0}，{0，0，0}}
> **输出:**不可能

**方法:**这个想法是基于这样的观察:如果任何元素 **B[i][j] = 0** ，那么矩阵 **A[][]** 的 **i <sup>第</sup>行和 **j <sup>第</sup>列中的所有元素都将是 0，因为只有 **0s** 的组合的**位“或”**才会产生 **0** 。按照以下步骤解决问题:****

*   创建一个大小为 **N*M** 的矩阵 **A[][]** ，并用 **1** 初始化其所有元素。
*   [使用变量 **i** 和 **j** 遍历矩阵 B[][]行](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，如果 **B[i][j] = 0** ，则将矩阵 **A[][]** 的 **i <sup>第</sup>行**和 **j <sup>第</sup>T15】列的所有元素设为 **0** 。**
*   [使用变量 **i** 和 **j** 遍历矩阵 A[][]行](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，对于每个索引 **(i，j)** ，找到矩阵 **A[][]** 的 **i <sup>第</sup>** 行和 **j <sup>第</sup>** 列中元素的按位 or，并将其存储在变量 **c** 中。如果 **c** 不等于**B【I】【j】**，则打印“不可能”并[断开](https://www.geeksforgeeks.org/break-statement-cc/)的循环。
*   完成上述步骤后，如果没有遇到 break 语句，则打印生成的矩阵 **A[][]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the matrix, A[][]
// satisfying the given conditions
void findOriginalMatrix(
    vector<vector<int> > B, int N, int M)
{
    // Store the final matrix
    int A[N][M];

    // Initialize all the elements of
    // the matrix A with 1
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < M; ++j) {
            A[i][j] = 1;
        }
    }

    // Traverse the matrix B[][] row-wise
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < M; ++j) {

            // If B[i][j] is equal to 0
            if (B[i][j] == 0) {

                // Mark all the elements of
                // ith row of A[][] as 0
                for (int k = 0; k < M; ++k) {
                    A[i][k] = 0;
                }

                // Mark all the elements of
                // jth column of A[][] as 0
                for (int k = 0; k < N; ++k) {
                    A[k][j] = 0;
                }
            }
        }
    }

    // Check if the matrix B[][] can
    // be made using matrix A[][]
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < M; ++j) {

            // Store the bitwise OR of
            // all elements of A[][] in
            // ith row and jth column
            int c = 0;

            // Traverse through ith row
            for (int k = 0; k < M; ++k) {
                if (c == 1)
                    break;
                c += A[i][k];
            }

            // Traverse through jth column
            for (int k = 0; k < N; ++k) {
                if (c == 1)
                    break;
                c += A[k][j];
            }

            // If B[i][j] is not equal to
            // c, print "Not Possible"
            if (c != B[i][j]) {
                cout << "Not Possible";
                return;
            }
        }
    }

    // Print the final matrix A[][]
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < M; ++j) {
            cout << A[i][j] << " ";
        }
        cout << "\n";
    }
}

// Driver Code
int main()
{
    vector<vector<int> > B{ { 1, 1, 1 }, { 1, 1, 1 } };

    int N = B.size();
    int M = B[0].size();

    // Function Call
    findOriginalMatrix(B, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the matrix, A[][]
// satisfying the given conditions
static void findOriginalMatrix(int[][] B, int N,
                               int M)
{

    // Store the final matrix
    int[][] A = new int[N][M];

    // Initialize all the elements of
    // the matrix A with 1
    for(int i = 0; i < N; ++i)
    {
        for(int j = 0; j < M; ++j)
        {
            A[i][j] = 1;
        }
    }

    // Traverse the matrix B[][] row-wise
    for(int i = 0; i < N; ++i)
    {
        for(int j = 0; j < M; ++j)
        {

            // If B[i][j] is equal to 0
            if (B[i][j] == 0)
            {

                // Mark all the elements of
                // ith row of A[][] as 0
                for(int k = 0; k < M; ++k)
                {
                    A[i][k] = 0;
                }

                // Mark all the elements of
                // jth column of A[][] as 0
                for(int k = 0; k < N; ++k)
                {
                    A[k][j] = 0;
                }
            }
        }
    }

    // Check if the matrix B[][] can
    // be made using matrix A[][]
    for(int i = 0; i < N; ++i)
    {
        for(int j = 0; j < M; ++j)
        {

            // Store the bitwise OR of
            // all elements of A[][] in
            // ith row and jth column
            int c = 0;

            // Traverse through ith row
            for(int k = 0; k < M; ++k)
            {
                if (c == 1)
                    break;

                c += A[i][k];
            }

            // Traverse through jth column
            for(int k = 0; k < N; ++k)
            {
                if (c == 1)
                    break;

                c += A[k][j];
            }

            // If B[i][j] is not equal to
            // c, print "Not Possible"
            if (c != B[i][j])
            {
                System.out.println("Not Possible");
                return;
            }
        }
    }

    // Print the final matrix A[][]
    for(int i = 0; i < N; ++i)
    {
        for(int j = 0; j < M; ++j)
        {
            System.out.print(A[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{
    int[][] B = new int[][]{ { 1, 1, 1 },
                             { 1, 1, 1 } };

    int N = B.length;
    int M = B[0].length;

    // Function Call
    findOriginalMatrix(B, N, M);
}
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the matrix, A[][]
# satisfying the given conditions
def findOriginalMatrix(B, N, M) :

    # Store the final matrix
    A = [[0]*M]*N

    # Initialize all the elements of
    # the matrix A with 1
    for i in range(N) :
        for j in range(M):
            A[i][j] = 1

    # Traverse the matrix B[][] row-wise
    for i in range(N) :
        for j in range(M):

            # If B[i][j] is equal to 0
            if (B[i][j] == 0) :

                # Mark all the elements of
                # ith row of A[][] as 0
                for k in range(M):
                    A[i][k] = 0

                # Mark all the elements of
                # jth column of A[][] as 0
                for k in range(N):
                    A[k][j] = 0

    # Check if the matrix B[][] can
    # be made using matrix A[][]
    for i in range(N) :
        for j in range(M):

            # Store the bitwise OR of
            # all elements of A[][] in
            # ith row and jth column
            c = 0

            # Traverse through ith row
            for k in range(M):
                if (c == 1) :
                    break
                c += A[i][k]

            # Traverse through jth column
            for k in range(N):
                if (c == 1) :
                    break
                c += A[k][j]

            # If B[i][j] is not equal to
            # c, pr"Not Possible"
            if (c != B[i][j]) :
                print("Not Possible")
                return

    # Print the final matrix A[][]
    for i in range(N) :
        for j in range(M):
            print(A[i][j], end = " ")

        print()

# Driver Code
B = [[ 1, 1, 1 ], [ 1, 1, 1 ]]

N = len(B)
M = len(B[0])

# Function Call
findOriginalMatrix(B, N, M)

# This code is contributed by splevel62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the matrix, A[][]
// satisfying the given conditions
static void findOriginalMatrix(int[,] B, int N,
                               int M)
{

    // Store the final matrix
    int[,] A = new int[N, M];

    // Initialize all the elements of
    // the matrix A with 1
    for(int i = 0; i < N; ++i)
    {
        for(int j = 0; j < M; ++j)
        {
            A[i, j] = 1;
        }
    }

    // Traverse the matrix B[][] row-wise
    for(int i = 0; i < N; ++i)
    {
        for(int j = 0; j < M; ++j)
        {

            // If B[i][j] is equal to 0
            if (B[i, j] == 0)
            {

                // Mark all the elements of
                // ith row of A[][] as 0
                for(int k = 0; k < M; ++k)
                {
                    A[i, k] = 0;
                }

                // Mark all the elements of
                // jth column of A[][] as 0
                for(int k = 0; k < N; ++k)
                {
                    A[k, j] = 0;
                }
            }
        }
    }

    // Check if the matrix B[][] can
    // be made using matrix A[][]
    for(int i = 0; i < N; ++i)
    {
        for(int j = 0; j < M; ++j)
        {

            // Store the bitwise OR of
            // all elements of A[][] in
            // ith row and jth column
            int c = 0;

            // Traverse through ith row
            for(int k = 0; k < M; ++k)
            {
                if (c == 1)
                    break;

                c += A[i, k];
            }

            // Traverse through jth column
            for(int k = 0; k < N; ++k)
            {
                if (c == 1)
                    break;

                c += A[k, j];
            }

            // If B[i][j] is not equal to
            // c, print "Not Possible"
            if (c != B[i, j])
            {
                Console.WriteLine("Not Possible");
                return;
            }
        }
    }

    // Print the final matrix A[][]
    for(int i = 0; i < N; ++i)
    {
        for(int j = 0; j < M; ++j)
        {
            Console.Write(A[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Driver Code
static public void Main()
{
    int[,] B = new int[,]{ { 1, 1, 1 },
                           { 1, 1, 1 } };

    int N = B.GetLength(0);
    int M = B.GetLength(1);

    // Function Call
    findOriginalMatrix(B, N, M);
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to find the matrix, A
    // satisfying the given conditions
    function findOriginalMatrix(B , N , M)
    {

        // Store the final matrix
        var A = Array(N);
        for(var i = 0;i<N;i++)
        A[i] = Array(M).fill(0);

        // Initialize all the elements of
        // the matrix A with 1
        for (i = 0; i < N; ++i) {
            for (j = 0; j < M; ++j) {
                A[i][j] = 1;
            }
        }

        // Traverse the matrix B row-wise
        for (i = 0; i < N; ++i) {
            for (j = 0; j < M; ++j) {

                // If B[i][j] is equal to 0
                if (B[i][j] == 0) {

                    // Mark all the elements of
                    // ith row of A as 0
                    for (k = 0; k < M; ++k) {
                        A[i][k] = 0;
                    }

                    // Mark all the elements of
                    // jth column of A as 0
                    for (k = 0; k < N; ++k) {
                        A[k][j] = 0;
                    }
                }
            }
        }

        // Check if the matrix B can
        // be made using matrix A
        for (i = 0; i < N; ++i) {
            for (j = 0; j < M; ++j) {

                // Store the bitwise OR of
                // all elements of A in
                // ith row and jth column
                var c = 0;

                // Traverse through ith row
                for (k = 0; k < M; ++k) {
                    if (c == 1)
                        break;

                    c += A[i][k];
                }

                // Traverse through jth column
                for (k = 0; k < N; ++k) {
                    if (c == 1)
                        break;

                    c += A[k][j];
                }

                // If B[i][j] is not equal to
                // c, print "Not Possible"
                if (c != B[i][j]) {
                    document.write("Not Possible");
                    return;
                }
            }
        }

        // Print the final matrix A
        for (i = 0; i < N; ++i) {
            for (j = 0; j < M; ++j) {
                document.write(A[i][j] + " ");
            }
            document.write("<br/>");
        }
    }

    // Driver Code

        var B =[[ 1, 1, 1 ], [ 1, 1, 1 ] ];

        var N = B.length;
        var M = B[0].length;

        // Function Call
        findOriginalMatrix(B, N, M);

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
1 1 1 
1 1 1
```

***时间复杂度:**O(N * M<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*