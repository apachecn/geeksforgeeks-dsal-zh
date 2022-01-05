# 以增量修改矩阵，使得没有一对相邻元素相等

> 原文:[https://www . geeksforgeeks . org/按增量修改矩阵，使得相邻元素对不相等/](https://www.geeksforgeeks.org/modify-matrix-by-increments-such-that-no-pair-of-adjacent-elements-are-equal/)

给定大小为 **N * N** 的正方形[矩阵](https://www.geeksforgeeks.org/matrix/) **mat[][]** ，任务是在递增矩阵元素后打印矩阵，使得矩阵的两个相邻元素不相等。

**示例:**

> **输入:** mat[][] = { { 1，2，2 }，{ 3，2，2 }，{ 2，2，2 } }
> **输出:** { { 2，3，2 }，{ 3，2，3 }，{ 2，3，2 } }
> **解释:**
> 将{ mat[0][0]、mat[0][1]、mat[1][2]、mat[2][1]的值递增 1 将矩阵修改为{ { 2，2 }
> 因此，需要的输出是{ { 2，3，2 }，{ 3，2，3 }，{ 2，3，2 } }。
> 
> **输入:** mat[][] = { { 1，2 }，{ 1，2 } }
> **输出:** { { 2，3 }，{ 1，2 } }

**方法:**按照以下步骤解决问题:

*   使用变量 **(i，j)** 遍历矩阵，并检查以下条件。
    *   如果 **i % 2 == 0 和 j % 2 == 0 和 mat[i][j] % 2 == 1** ，那么将 **mat[i][j]** 的值增加 **1** 。
    *   如果 **i % 2 == 0，j % 2 == 1，mat[i][j] % 2 == 0** ，则 **mat[i][j]** 的值增加 **1** 。
    *   如果 **i % 2 == 1，j % 2 == 0，mat[i][j] % 2 == 0** ，则 **mat[i][j]** 的值增加 **1** 。
    *   如果 **i % 2 == 1，j % 2 == 1，mat[i][j] % 2 == 1** ，则 **mat[i][j]** 的值增加 **1** 。
*   最后打印矩阵 **mat[][]** 。

下面是上述方法的实现:

## C++14

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the  matrix
void printMatrix(vector<vector<int> >& mat, int N)
{
    // Print the leftmost parenthesis
    // of the matrix
    cout << "{ ";

    // Traverse the matrix
    for (int i = 0; i < N; i++) {

        cout << "{ ";

        // Traverse each column
        // of the matrix
        for (int j = 0; j < N; j++) {

            // If current column is last
            // column of the matrix
            if (j == N - 1) {

                // Print current element
                // of the matrix
                cout << mat[i][j];
            }

            // If current column is not
            // last column of the matrix
            else {
                cout << mat[i][j] << ", ";
            }
        }
        cout << " } ";
    }

    // Print the leftmost parenthesis
    // of the matrix
    cout << "}";
}

// Function to find the matrix with no two
// adjacent elements equal by increment operation
void MatNoAdjacentElemEq(vector<vector<int> >& mat,
                         int N)
{
    // Traverse the matrix
    for (int i = 0; i < N; i++) {

        // Traverse column of the matrix
        for (int j = 0; j < N; j++) {

            // If i is an even number
            if (i % 2 == 0) {

                // If j is an even number and current
                // matrix element is an odd number
                if (j % 2 == 0 && mat[i][j] % 2 != 0) {

                    // Increment the value of
                    // matrix element
                    mat[i][j]++;
                }

                // If j is an odd number and current
                // matrix element is an even number
                else if (j % 2 != 0 && mat[i][j] % 2 == 0) {

                    // Increment the value of
                    // matrix element
                    mat[i][j]++;
                }
            }

            // If i is an odd number
            else {

                // If j is an even number and current
                // matrix element is an even number
                if (j % 2 == 0 && mat[i][j] % 2 == 0) {

                    // Increment the value of
                    // matrix element
                    mat[i][j]++;
                }

                // If j is an odd number and current
                // matrix element is an odd number
                else if (j % 2 != 0 && mat[i][j] % 2 != 0) {

                    // Increment the value of
                    // matrix element
                    mat[i][j]++;
                }
            }
        }
    }

    // Print the matrix
    printMatrix(mat, N);
}

// Driver Code
int main()
{
    vector<vector<int> > mat = { { 1, 2, 2 },
                                 { 3, 2, 2 },
                                 { 2, 2, 2 } };
    int N = mat.size();
    MatNoAdjacentElemEq(mat, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to print the  matrix
static void printMatrix(int[][] mat, int N)
{

    // Print the leftmost parenthesis
    // of the matrix
    System.out.print("{ ");

    // Traverse the matrix
    for(int i = 0; i < N; i++)
    {
        System.out.print("{ ");

        // Traverse each column
        // of the matrix
        for(int j = 0; j < N; j++)
        {

            // If current column is last
            // column of the matrix
            if (j == N - 1)
            {

                // Print current element
                // of the matrix
                System.out.print(mat[i][j]);
            }

            // If current column is not
            // last column of the matrix
            else
            {
                System.out.print(mat[i][j] + ", ");
            }
        }
        System.out.print(" } ");
    }

    // Print the leftmost parenthesis
    // of the matrix
    System.out.print("}");
}

// Function to find the matrix with no two
// adjacent elements equal by increment operation
static void MatNoAdjacentElemEq(int[][] mat,
                                int N)
{

    // Traverse the matrix
    for(int i = 0; i < N; i++)
    {

        // Traverse column of the matrix
        for(int j = 0; j < N; j++)
        {

            // If i is an even number
            if (i % 2 == 0)
            {

                // If j is an even number and current
                // matrix element is an odd number
                if (j % 2 == 0 &&
                    mat[i][j] % 2 != 0)
                {

                    // Increment the value of
                    // matrix element
                    mat[i][j]++;
                }

                // If j is an odd number and current
                // matrix element is an even number
                else if (j % 2 != 0 &&
                         mat[i][j] % 2 == 0)
                {

                    // Increment the value of
                    // matrix element
                    mat[i][j]++;
                }
            }

            // If i is an odd number
            else
            {

                // If j is an even number and current
                // matrix element is an even number
                if (j % 2 == 0 &&
                    mat[i][j] % 2 == 0)
                {

                    // Increment the value of
                    // matrix element
                    mat[i][j]++;
                }

                // If j is an odd number and current
                // matrix element is an odd number
                else if (j % 2 != 0 &&
                         mat[i][j] % 2 != 0)
                {

                    // Increment the value of
                    // matrix element
                    mat[i][j]++;
                }
            }
        }
    }

    // Print the matrix
    printMatrix(mat, N);
}

// Driver Code
public static void main(String[] args)
{
    int[][] mat = { { 1, 2, 2 },
                    { 3, 2, 2 },
                    { 2, 2, 2 } };
    int N = mat.length;

    MatNoAdjacentElemEq(mat, N);
}
}

// This code is contributed by aashish1995
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print the  matrix
def printMatrix(mat, N):

    # Print the leftmost parenthesis
    # of the matrix
    print("{ ",end = "")

    # Traverse the matrix
    for i in range(N):

        print("{ ",end = "")

        # Traverse each column
        # of the matrix
        for j in range(N):

            # If current column is last
            # column of the matrix
            if (j == N - 1):

                # Prcurrent element
                # of the matrix
                print(mat[i][j], end = "")

            # If current column is not
            # last column of the matrix
            else:
                print(mat[i][j], end = ", ")
        print(" } ",end = "")

    # Print the leftmost parenthesis
    # of the matrix
    print("}",end="")

# Function to find the matrix with no two
# adjacent elements equal by increment operation
def MatNoAdjacentElemEq(mat,N):

    # Traverse the matrix
    for i in range(N):

        # Traverse column of the matrix
        for j in range(N):

            # If i is an even number
            if (i % 2 == 0):

                # If j is an even number and current
                # matrix element is an odd number
                if (j % 2 == 0 and mat[i][j] % 2 != 0):

                    # Increment the value of
                    # matrix element
                    mat[i][j] += 1

                # If j is an odd number and current
                # matrix element is an even number
                elif (j % 2 != 0 and mat[i][j] % 2 == 0):

                    # Increment the value of
                    # matrix element
                    mat[i][j] += 1

            # If i is an odd number
            else:
                # If j is an even number and current
                # matrix element is an even number
                if (j % 2 == 0 and mat[i][j] % 2 == 0):

                    #Increment the value of
                    #matrix element
                    mat[i][j] += 1

                # If j is an odd number and current
                # matrix element is an odd number
                elif (j % 2 != 0 and mat[i][j] % 2 != 0):

                    # Increment the value of
                    # matrix element
                    mat[i][j] += 1

    # Print the matrix
    printMatrix(mat, N)

# Driver Code
if __name__ == '__main__':
    mat =[[1, 2, 2],
          [ 3, 2, 2],
          [ 2, 2, 2]]
    N = len(mat)
    MatNoAdjacentElemEq(mat, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to print the  matrix
static void printMatrix(int[,] mat, int N)
{

    // Print the leftmost parenthesis
    // of the matrix
    Console.Write("{ ");

    // Traverse the matrix
    for(int i = 0; i < N; i++)
    {
        Console.Write("{ ");

        // Traverse each column
        // of the matrix
        for(int j = 0; j < N; j++)
        {

            // If current column is last
            // column of the matrix
            if (j == N - 1)
            {

                // Print current element
                // of the matrix
                Console.Write(mat[i, j]);
            }

            // If current column is not
            // last column of the matrix
            else
            {
                Console.Write(mat[i, j] + ", ");
            }
        }
        Console.Write(" } ");
    }

    // Print the leftmost parenthesis
    // of the matrix
    Console.Write("}");
}

// Function to find the matrix with no two
// adjacent elements equal by increment operation
static void MatNoAdjacentElemEq(int[,] mat,
                                int N)
{

    // Traverse the matrix
    for(int i = 0; i < N; i++)
    {

        // Traverse column of the matrix
        for(int j = 0; j < N; j++)
        {

            // If i is an even number
            if (i % 2 == 0)
            {

                // If j is an even number and current
                // matrix element is an odd number
                if (j % 2 == 0 &&
                    mat[i, j] % 2 != 0)
                {

                    // Increment the value of
                    // matrix element
                    mat[i, j]++;
                }

                // If j is an odd number and current
                // matrix element is an even number
                else if (j % 2 != 0 &&
                         mat[i, j] % 2 == 0)
                {

                    // Increment the value of
                    // matrix element
                    mat[i, j]++;
                }
            }

            // If i is an odd number
            else
            {

                // If j is an even number and current
                // matrix element is an even number
                if (j % 2 == 0 &&
                    mat[i, j] % 2 == 0)
                {

                    // Increment the value of
                    // matrix element
                    mat[i, j]++;
                }

                // If j is an odd number and current
                // matrix element is an odd number
                else if (j % 2 != 0 &&
                         mat[i, j] % 2 != 0)
                {

                    // Increment the value of
                    // matrix element
                    mat[i, j]++;
                }
            }
        }
    }

    // Print the matrix
    printMatrix(mat, N);
}

// Driver Code
public static void Main(String[] args)
{
    int[,] mat = { { 1, 2, 2 },
                   { 3, 2, 2 },
                   { 2, 2, 2 } };
    int N = mat.GetLength(0);

    MatNoAdjacentElemEq(mat, N);
}
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to print the  matrix
function printMatrix(mat,N)
{
    // Print the leftmost parenthesis
    // of the matrix
    document.write("{ ");

    // Traverse the matrix
    for(let i = 0; i < N; i++)
    {
        document.write("{ ");

        // Traverse each column
        // of the matrix
        for(let j = 0; j < N; j++)
        {

            // If current column is last
            // column of the matrix
            if (j == N - 1)
            {

                // Print current element
                // of the matrix
                document.write(mat[i][j]);
            }

            // If current column is not
            // last column of the matrix
            else
            {
                document.write(mat[i][j] + ", ");
            }
        }
        document.write(" } ");
    }

    // Print the leftmost parenthesis
    // of the matrix
    document.write("}");
}

// Function to find the matrix with no two
// adjacent elements equal by increment operation
function MatNoAdjacentElemEq(mat, N)
{

    // Traverse the matrix
    for(let i = 0; i < N; i++)
    {

        // Traverse column of the matrix
        for(let j = 0; j < N; j++)
        {

            // If i is an even number
            if (i % 2 == 0)
            {

                // If j is an even number and current
                // matrix element is an odd number
                if (j % 2 == 0 &&
                    mat[i][j] % 2 != 0)
                {

                    // Increment the value of
                    // matrix element
                    mat[i][j]++;
                }

                // If j is an odd number and current
                // matrix element is an even number
                else if (j % 2 != 0 &&
                         mat[i][j] % 2 == 0)
                {

                    // Increment the value of
                    // matrix element
                    mat[i][j]++;
                }
            }

            // If i is an odd number
            else
            {

                // If j is an even number and current
                // matrix element is an even number
                if (j % 2 == 0 &&
                    mat[i][j] % 2 == 0)
                {

                    // Increment the value of
                    // matrix element
                    mat[i][j]++;
                }

                // If j is an odd number and current
                // matrix element is an odd number
                else if (j % 2 != 0 &&
                         mat[i][j] % 2 != 0)
                {

                    // Increment the value of
                    // matrix element
                    mat[i][j]++;
                }
            }
        }
    }

    // Print the matrix
    printMatrix(mat, N);
}

// Driver Code
let mat = [[ 1, 2, 2 ],
    [ 3, 2, 2 ],
    [ 2, 2, 2 ]];
let N = mat.length;

MatNoAdjacentElemEq(mat, N);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
{ { 2, 3, 2 } { 3, 2, 3 } { 2, 3, 2 } }
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*