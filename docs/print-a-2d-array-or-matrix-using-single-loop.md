# 使用单循环打印 2D 阵列或矩阵

> 原文:[https://www . geesforgeks . org/print-a-2d-array-or-matrix-use-single-loop/](https://www.geeksforgeeks.org/print-a-2d-array-or-matrix-using-single-loop/)

给定一个 **N * M** 尺寸的[矩阵](https://www.geeksforgeeks.org/matrix/) **mat[][]** ，任务是使用单个[循环](https://www.geeksforgeeks.org/c-c-for-loop-with-examples/)打印矩阵的元素。

**示例:**

> **输入:** mat[][] = {{1，2，3}，{4，5，6}，{7，8，9 } }
> T3】输出: 1 2 3 4 5 6 7 8 9
> 
> **输入:** mat[][] = {{7，9}，{10，34}，{12，15 } }
> T3】输出: 7 9 10 34 12 15

**方法:**到[使用单个循环遍历给定矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)，观察只有 **N * M** 元素。因此，想法是使用模数和除法来切换行和列，同时在范围**【0，N * M】**上迭代单个循环。按照以下步骤解决给定的问题:

*   使用变量 **i** 在范围**【0，N * M】**内循环。
*   每次迭代时，求当前行和列的索引分别为**行= i / M** 和**列= i % M** 。
*   在上面的步骤中，打印**mat【row】【column】**的值，得到该索引处矩阵的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to print the element
// of 2D matrix using single loop
void print2DMatrix(int arr[][3],
                   int rows, int columns)
{

    // Iterate over the range
    // [0, rows*columns]

    for(int i = 0; i < rows * columns; i++)
    {

        // Find row and column index
        int row = i / columns;
        int col = i % columns;

        // Print the element at
        // current index
        cout << arr[row][col] << " ";
    }
}

// Driver Code
int main()
{

    // Given matrix mat[][]
    int mat[][3] = { { 1, 2, 3 },
                     { 4, 5, 6 },
                     { 7, 8, 9 } };

    // Dimensions of the matrix
    int N = sizeof(mat) / sizeof(mat[0]);
    int M = sizeof(mat[0]) / sizeof(mat[0][0]);

    // Function Call
    print2DMatrix(mat, N, M);
    return 0;
}

// This code is contributed by akhilsaini
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach

import java.io.*;

class GFG {

    // Function to print the element
    // of 2D matrix using single loop
    public static void print2DMatrix(
        int arr[][], int rows, int columns)
    {

        // Iterate over the range
        // [0, rows*columns]
        for (int i = 0;
             i < rows * columns; i++) {

            // Find row and column index
            int row = i / columns;
            int col = i % columns;

            // Print the element at
            // current index
            System.out.print(
                arr[row][col] + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given matrix mat[][]
        int[][] mat = { { 1, 2, 3 },
                        { 4, 5, 6 },
                        { 7, 8, 9 } };

        // Dimensions of the matrix
        int N = mat.length;
        int M = mat[0].length;

        // Function Call
        print2DMatrix(mat, N, M);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the element
# of 2D matrix using single loop
def print2DMatrix(arr, rows, columns):

  # Iterate over the range
  # [0, rows*columns]
  for i in range(0, rows * columns):

    # Find row and column index
    row = i // columns
    col = i % columns

    # Print the element at
    # current index
    print(arr[row][col], end = ' ')

# Driver Code
if __name__ == '__main__':

  # Given matrix mat[][]
  mat = [ [ 1, 2, 3 ],
          [ 4, 5, 6 ],
          [ 7, 8, 9 ] ]

  # Dimensions of the matrix
  N = len(mat)
  M = len(mat[0])

  # Function Call
  print2DMatrix(mat, N, M)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print the element
// of 2D matrix using single loop
public static void print2DMatrix(int[, ] arr, int rows,
                                 int columns)
{

    // Iterate over the range
    // [0, rows*columns]
    for(int i = 0; i < rows * columns; i++)
    {

        // Find row and column index
        int row = i / columns;
        int col = i % columns;

        // Print the element at
        // current index
        Console.Write(arr[row, col] + " ");
    }
}

// Driver Code
public static void Main()
{

    // Given matrix mat[][]
    int[, ] mat = { { 1, 2, 3 },
                    { 4, 5, 6 },
                    { 7, 8, 9 } };

    // Dimensions of the matrix
    int N = mat.GetLength(0);
    int M = mat.GetLength(1);

    // Function Call
    print2DMatrix(mat, N, M);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach
    // Function to print the element
    // of 2D matrix using single loop

    function print2DMatrix(arr,rows,columns)
    {

        // Iterate over the range
        // [0, rows*columns]

        for(let i = 0; i < rows * columns; i++)
        {

            // Find row and column index
            let row = parseInt(i / columns, 10);
            let col = i % columns;

            // Print the element at
            // current index
            document.write(arr[row][col] + " ");
        }
    }

    // Given matrix mat[][]
    let mat = [ [ 1, 2, 3 ],
                 [ 4, 5, 6 ],
                 [ 7, 8, 9 ] ];

    // Dimensions of the matrix
    let N = mat.length;
    let M = mat[0].length;

    // Function Call
    print2DMatrix(mat, N, M);

</script>
```

**Output:** 

```
1 2 3 4 5 6 7 8 9
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*