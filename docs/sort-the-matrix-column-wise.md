# 按列对矩阵排序

> 原文:[https://www.geeksforgeeks.org/sort-the-matrix-column-wise/](https://www.geeksforgeeks.org/sort-the-matrix-column-wise/)

给定维度为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**mat【】【】**，任务是按升序对矩阵的每一列进行排序，[打印更新后的矩阵。](https://www.geeksforgeeks.org/print-matrix-after-multiplying-matrix-elements-n-times/)

**示例:**

> **输入:** mat[][] = { {1，6，10}，{8，5，9}，{9，4，15}，{7，3，60} }
> **输出:**
> 1 3 9
> 7 4 10
> 8 5 15
> 9 6 60
> **说明:**
> 输入矩阵按列排序，
> 1 < 7 <
> 
> **输入:** arr[][] = { {1，6}，{8，4}，{9，7} }
> **输出:**
> 1 4
> 8 6
> 9 7

**方法:**按照以下步骤解决问题:

*   [遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)
*   [求给定矩阵的转置](https://www.geeksforgeeks.org/program-to-find-transpose-of-a-matrix/) **mat[][]** 。
*   将 **mat[][]** 的转置存储在 [2D 向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/)、 **tr[][]** 中
*   [遍历矩阵 tr[][]](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/) 的行
*   [使用](https://www.geeksforgeeks.org/row-wise-sorting-2d-array/)[排序功能](https://www.geeksforgeeks.org/sort-c-stl/)对矩阵的每一行进行排序。
*   将 **tr[][]** 的转置存储在 **mat[][]** 中
*   [打印矩阵](https://www.geeksforgeeks.org/print-2-d-array-matrix-java/)、 **mat[][]**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the transpose
// of the matrix mat[]
vector<vector<int> > transpose(
    vector<vector<int> > mat,
    int row, int col)
{

    // Stores the transpose
    // of matrix mat[][]
    vector<vector<int> > tr(
        col, vector<int>(row));

    // Traverse each row of the matrix
    for (int i = 0; i < row; i++) {

        // Traverse each column of the matrix
        for (int j = 0; j < col; j++) {

            // Transpose matrix elements
            tr[j][i] = mat[i][j];
        }
    }

    return tr;
}

// Function to sort the given
// matrix in row wise manner
void RowWiseSort(vector<vector<int> >& B)
{
    // Traverse the row
    for (int i = 0; i < (int)B.size(); i++) {

        // Row - Wise Sorting
        sort(B[i].begin(), B[i].end());
    }
}

// Function to print the matrix
// in column wise sorted manner
void sortCol(vector<vector<int> > mat,
             int N, int M)
{
    // Function call to find transpose
    // of the the matrix mat[][]
    vector<vector<int> > B
        = transpose(mat, N, M);

    // Sorting the matrix row-wise
    RowWiseSort(B);

    // Calculate transpose of B[][]
    mat = transpose(B, M, N);

    // Print the matrix mat[][]
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {

            cout << mat[i][j] << " ";
        }
        cout << '\n';
    }
}

// Driver Code
int main()
{
    // Input
    vector<vector<int> > mat = { { 1, 6, 10 },
                                 { 8, 5, 9 },
                                 { 9, 4, 15 },
                                 { 7, 3, 60 } };

    int N = mat.size();
    int M = mat[0].size();

    // Function call to print the matrix
    // in column wise sorted manner
    sortCol(mat, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.util.Arrays;

class GFG{

// Function to find the transpose
// of the matrix mat[]
static int[][] transpose(int[][] mat, int row,
                         int col)
{

    // Stores the transpose
    // of matrix mat[][]
    int[][] tr = new int[col][row];

    // Traverse each row of the matrix
    for(int i = 0; i < row; i++)
    {

        // Traverse each column of the matrix
        for(int j = 0; j < col; j++)
        {

            // Transpose matrix elements
            tr[j][i] = mat[i][j];
        }
    }
    return tr;
}

// Function to sort the given
// matrix in row wise manner
static void RowWiseSort(int[][] B)
{

    // Traverse the row
    for(int i = 0; i < (int)B.length; i++)
    {

        // Row - Wise Sorting
        Arrays.sort(B[i]);
    }
}

// Function to print the matrix
// in column wise sorted manner
static void sortCol(int[][] mat, int N, int M)
{

    // Function call to find transpose
    // of the the matrix mat[][]
    int[][] B = transpose(mat, N, M);

    // Sorting the matrix row-wise
    RowWiseSort(B);

    // Calculate transpose of B[][]
    mat = transpose(B, M, N);

    // Print the matrix mat[][]
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {
            System.out.print(mat[i][j] + " ");
        }
        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int[][] mat = { { 1, 6, 10 },
                    { 8, 5, 9 },
                    { 9, 4, 15 },
                    { 7, 3, 60 } };

    int N = mat.length;
    int M = mat[0].length;

    // Function call to print the matrix
    // in column wise sorted manner
    sortCol(mat, N, M);
}
}

// This code is contributed by ukasp
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the transpose
# of the matrix mat[]
def transpose(mat, row, col):

    # Stores the transpose
    # of matrix mat[][]
    tr = [[0 for i in range(row)] for i in range(col)]

    # Traverse each row of the matrix
    for i in range(row):

        # Traverse each column of the matrix
        for j in range(col):

            # Transpose matrix elements
            tr[j][i] = mat[i][j]
    return tr

# Function to sort the given
# matrix in row wise manner
def RowWiseSort(B):

    # Traverse the row
    for i in range(len(B)):

        # Row - Wise Sorting
        B[i] = sorted(B[i])
    return B

# Function to print the matrix
# in column wise sorted manner
def sortCol(mat, N, M):

    # Function call to find transpose
    # of the the matrix mat[][]
    B = transpose(mat, N, M)

    # Sorting the matrix row-wise
    B = RowWiseSort(B)

    # Calculate transpose of B[][]
    mat = transpose(B, M, N)

    # Print the matrix mat[][]
    for i in range(N):
        for j in range(M):
            print(mat[i][j], end = " ")
        print()

# Driver Code
if __name__ == '__main__':

    # Input
    mat =[ [1, 6, 10 ],
            [ 8, 5, 9 ],
            [ 9, 4, 15 ],
            [ 7, 3, 60 ] ]

    N = len(mat)
    M = len(mat[0])

    # Function call to print the matrix
    # in column wise sorted manner
    sortCol(mat, N, M)

# This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the transpose
// of the matrix mat[]
function transpose(mat,row,col)
{
    // Stores the transpose
    // of matrix mat[][]
    let tr = new Array(col);
    for(let i=0;i<col;i++)
    {
        tr[i]=new Array(row);
    }

    // Traverse each row of the matrix
    for(let i = 0; i < row; i++)
    {

        // Traverse each column of the matrix
        for(let j = 0; j < col; j++)
        {

            // Transpose matrix elements
            tr[j][i] = mat[i][j];
        }
    }
    return tr;
}

// Function to sort the given
// matrix in row wise manner
function RowWiseSort(B)
{
    // Traverse the row
    for(let i = 0; i < B.length; i++)
    {

        // Row - Wise Sorting
        (B[i]).sort(function(a,b){return a-b;});
    }
}

// Function to print the matrix
// in column wise sorted manner
function sortCol(mat,n,M)
{
    // Function call to find transpose
    // of the the matrix mat[][]
    let B = transpose(mat, N, M);

    // Sorting the matrix row-wise
    RowWiseSort(B);

    // Calculate transpose of B[][]
    mat = transpose(B, M, N);

    // Print the matrix mat[][]
    for(let i = 0; i < N; i++)
    {
        for(let j = 0; j < M; j++)
        {
            document.write(mat[i][j] + " ");
        }
        document.write("<br>");
    }
}

// Driver Code
let mat = [[ 1, 6, 10 ],
                    [ 8, 5, 9 ],
                    [ 9, 4, 15 ],
                    [ 7, 3, 60 ] ];

let N = mat.length;
let M = mat[0].length;

// Function call to print the matrix
// in column wise sorted manner
sortCol(mat, N, M);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
1 3 9 
7 4 10 
8 5 15 
9 6 60
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*