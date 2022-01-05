# 使用递归遍历给定矩阵

> 原文:[https://www . geeksforgeeks . org/traverse-a-给定矩阵-使用递归/](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)

给定一个大小为 **N x M** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **arr** ，任务是使用递归遍历这个矩阵[。
**示例:**](https://www.geeksforgeeks.org/recursion/)

```
Input: arr[][] = {{1, 2, 3}, 
                  {4, 5, 6},
                  {7, 8, 9}} 
Output: 1, 2, 3, 4, 5, 6, 7, 8, 9

Input: M[][] = {{11, 12, 13}, 
                  {14, 15, 16}, 
                  {17, 18, 19}}
Output: 11, 12, 13, 14, 15, 16, 17, 18, 19
```

**方法:**下面是递归遍历矩阵的步骤:

*   **基本情况:**如果当前行或列分别超过大小 N 或 M，则递归停止。
    *   如果当前列超过列总数 M，则开始下一行。

```
if (current_col >= M)
    This row ends.
    Start for next row
```

*   如果当前行超过了总行数 N，那么整个遍历将停止。

```
if (current_row >= N)
    Matrix has been
    traversed completely
```

*   **递归情况:**在每次递归调用中，
    1.  将打印矩阵的当前元素。
    2.  进行两次递归调用:
        *   一个遍历下一行，并且
        *   另一个遍历下一列。

下面是上述方法的实现:

## C++

```
// C++ program to traverse the matrix recursively

#include <iostream>
using namespace std;

#define N 2
#define M 3

// Function to traverse the matrix recursively
int traverseMatrix(int arr[N][M], int current_row,
                   int current_col)
{
    // If the entire column is traversed
    if (current_col >= M)
        return 0;

    // If the entire row is traversed
    if (current_row >= N)
        return 1;

    // Print the value of the current
    // cell of the matrix
    cout << arr[current_row][current_col] << ", ";

    // Recursive call to traverse the matrix
    // in the Horizontal direction
    if (traverseMatrix(arr, current_row,
                       current_col + 1)
        == 1)
        return 1;

    // Recursive call for changing the
    // Row of the matrix
    return traverseMatrix(arr,
                          current_row + 1,
                          0);
}

// Driver code
int main()
{
    int arr[N][M] = { { 1, 2, 3 },
                      { 4, 5, 6 } };

    traverseMatrix(arr, 0, 0);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to traverse the matrix recursively
class GFG {

    final static int N = 2;
    final static int  M = 3;

    // Function to traverse the matrix recursively
    static int traverseMatrix(int arr[][], int current_row,
                       int current_col)
    {
        // If the entire column is traversed
        if (current_col >= M)
            return 0;

        // If the entire row is traversed
        if (current_row >= N)
            return 1;

        // Print the value of the current
        // cell of the matrix
        System.out.print(arr[current_row][current_col] + ", ");

        // Recursive call to traverse the matrix
        // in the Horizontal direction
        if (traverseMatrix(arr, current_row,
                           current_col + 1)
            == 1)
            return 1;

        // Recursive call for changing the
        // Row of the matrix
        return traverseMatrix(arr,
                              current_row + 1,
                              0);
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[][] = { { 1, 2, 3 },
                          { 4, 5, 6 } };

        traverseMatrix(arr, 0, 0);
    }
}

// This code is contributed by AnkitRai01
```

## C#

```
// C# program to traverse the matrix recursively

using System;

public class GFG {

    static int N = 2;
    static int  M = 3;

    // Function to traverse the matrix recursively
    static int traverseMatrix(int [,]arr, int current_row,
                       int current_col)
    {
        // If the entire column is traversed
        if (current_col >= M)
            return 0;

        // If the entire row is traversed
        if (current_row >= N)
            return 1;

        // Print the value of the current
        // cell of the matrix
        Console.Write(arr[current_row,current_col] + ", ");

        // Recursive call to traverse the matrix
        // in the Horizontal direction
        if (traverseMatrix(arr, current_row,
                           current_col + 1)
            == 1)
            return 1;

        // Recursive call for changing the
        // Row of the matrix
        return traverseMatrix(arr,
                              current_row + 1,
                              0);
    }

    // Driver code
    public static void Main (string[] args)
    {
        int [,]arr = { { 1, 2, 3 },
                          { 4, 5, 6 } };

        traverseMatrix(arr, 0, 0);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to traverse the matrix recursively
N = 2
M = 3

# Function to traverse the matrix recursively
def traverseMatrix(arr, current_row, current_col) :

    # If the entire column is traversed
    if (current_col >= M) :
        return 0;

    # If the entire row is traversed
    if (current_row >= N) :
        return 1;

    # Print the value of the current
    # cell of the matrix
    print(arr[current_row][current_col],end= ", ");

    # Recursive call to traverse the matrix
    # in the Horizontal direction
    if (traverseMatrix(arr, current_row, current_col + 1 ) == 1) :
        return 1;

    # Recursive call for changing the
    # Row of the matrix
    return traverseMatrix(arr, current_row + 1, 0);

# Driver code
if __name__ == "__main__" :
    arr = [ [ 1, 2, 3 ],
            [ 4, 5, 6 ] ];

    traverseMatrix(arr, 0, 0);

# This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript program to traverse the matrix recursively

let N = 2
let M = 3

// Function to traverse the matrix recursively
function traverseMatrix(arr, current_row, current_col)
{
    // If the entire column is traversed
    if (current_col >= M)
        return 0;

    // If the entire row is traversed
    if (current_row >= N)
        return 1;

    // Print the value of the current
    // cell of the matrix
    document.write(arr[current_row][current_col] + ", ");

    // Recursive call to traverse the matrix
    // in the Horizontal direction
    if (traverseMatrix(arr, current_row,
                    current_col + 1)
        == 1)
        return 1;

    // Recursive call for changing the
    // Row of the matrix
    return traverseMatrix(arr,
                        current_row + 1,
                        0);
}

// Driver code

let arr = [ [ 1, 2, 3 ],
            [ 4, 5, 6 ] ];

traverseMatrix(arr, 0, 0);
</script>
```

**Output:** 

```
1, 2, 3, 4, 5, 6,
```

***时间复杂度:** O(N * M)*

***辅助空间:** O(M)，因为递归调用*