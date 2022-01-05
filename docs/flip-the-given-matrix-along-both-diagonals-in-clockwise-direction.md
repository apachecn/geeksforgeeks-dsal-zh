# 顺时针方向沿两条对角线翻转给定矩阵

> 原文:[https://www . geeksforgeeks . org/顺时针方向沿两条对角线翻转给定矩阵/](https://www.geeksforgeeks.org/flip-the-given-matrix-along-both-diagonals-in-clockwise-direction/)

给定一个大小为 **M*N** 的矩阵 **arr[][]** ，其中 **M** 是**行**的数量， **N** 是**列**的数量。任务是通过**和**两条对角线**翻转**矩阵。翻转矩阵意味着**顺时针**方向，沿着**对角线**旋转矩阵的所有元素。

**示例**:

> **输入** : arr[][] = { {1，2，3}，{4，5，6}，{7，8，9} }
> **输出:** { {9，8，7}，{6，5，4}，{3，2，1} }
> **解释**:沿主对角线翻转矩阵后的结果矩阵:{ {1，4，7}，{2，5，8}，{3，6，9} }
> 翻转后的结果矩阵
> 
> **输入** : arr[][] = { {1，2，3，4}，{5，6，7，8}，{9，10，11，12}，{13，14，15，16} }
> **输出:** { {16，15，14，13}，{12，11，10，9}，{8，7，6，5}，{4，3，2，1} }

**接近**:使用**观察**可以轻松解决任务。人们可以观察到，结果矩阵将包含**反向行**在**反向顺序**。按照以下步骤解决问题:

*   遍历矩阵的行，以相反的顺序交换第一行和最后一行的元素，类似地交换第二行和第二最后一行的元素，以此类推。

下面是上述代码的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

const int m = 4, n = 4;

// Function to flip the matrix along
// both the diagonals
void flip(int matrix[m][n])
{
    int i, j, temp;

      // Swapping elements
    for (i = 0; i < m / 2; i++) {
        for (j = 0; j < n; j++) {
            temp = matrix[i][j];
            matrix[i][j] = matrix[m - 1 - i][n - 1 - j];
            matrix[m - 1 - i][n - 1 - j] = temp;
        }
    }
}

// Function to print the matrix
void show(int matrix[m][n])
{
    int i, j;
    for (i = 0; i < m; i++) {
        for (j = 0; j < n; j++) {
            cout << matrix[i][j] << "  ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{

    int matrix[4][4] = { { 1, 2, 3, 4 },
                         { 5, 6, 7, 8 },
                         { 9, 10, 11, 12 },
                         { 13, 14, 15, 16 } };

    flip(matrix);
    show(matrix);
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
m = 4
n = 4

# Function to flip the matrix along
# both the diagonals
def flip(matrix):

    i = None
    j = None
    temp = None

    # Swapping elements
    for i in range(m // 2):
        for j in range(n):
            temp = matrix[i][j]
            matrix[i][j] = matrix[m - 1 - i][n - 1 - j]
            matrix[m - 1 - i][n - 1 - j] = temp

# Function to print the matrix
def show(matrix):

    i = None
    j = None
    for i in range(m):
        for j in range(n):
            print(matrix[i][j], end = "  ")

        print("")

# Driver Code
matrix = [ [ 1, 2, 3, 4 ],
           [ 5, 6, 7, 8 ],
           [ 9, 10, 11, 12 ],
           [ 13, 14, 15, 16 ] ]

flip(matrix)
show(matrix)

# This code is contributed by gfgking
```

## java 描述语言

```
<script>
        // JavaScript code for the above approach
        let m = 4, n = 4;

        // Function to flip the matrix along
        // both the diagonals
        function flip(matrix) {
            let i, j, temp;

            // Swapping elements
            for (i = 0; i < Math.floor(m / 2); i++) {
                for (j = 0; j < n; j++) {
                    temp = matrix[i][j];
                    matrix[i][j] = matrix[m - 1 - i][n - 1 - j];
                    matrix[m - 1 - i][n - 1 - j] = temp;
                }
            }
        }

        // Function to print the matrix
        function show(matrix) {
            let i, j;
            for (i = 0; i < m; i++) {
                for (j = 0; j < n; j++) {
                    document.write(matrix[i][j] + "  ");
                }
                document.write('<br>')
            }
        }

        // Driver Code
        let matrix = [[1, 2, 3, 4],
        [5, 6, 7, 8],
        [9, 10, 11, 12],
        [13, 14, 15, 16]];

        flip(matrix);
        show(matrix);

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
16  15  14  13  
12  11  10  9  
8  7  6  5  
4  3  2  1  
```

***时间复杂度*** : O(M*N)
***辅助空间*** : O(1)