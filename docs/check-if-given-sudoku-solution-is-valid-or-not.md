# 检查给定的数独解是否有效

> 原文:[https://www . geesforgeks . org/check-if-given-sudoku-solution-is-valid-or-not/](https://www.geeksforgeeks.org/check-if-given-sudoku-solution-is-valid-or-not/)

给定一个大小为 **9 × 9** 的 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)、**棋盘[][]** ，它代表了[数独谜题](https://www.geeksforgeeks.org/sudoku-backtracking-7/)的解，任务是检查给定的已解数独谜题的表示是否有效。

**示例:**

> **输入:**
> 
> ```
> board[][] = {{7, 9, 2, 1, 5, 4, 3, 8, 6}, 
>              {6, 4, 3, 8, 2, 7, 1, 5, 9},
>              {8, 5, 1, 3, 9, 6, 7, 2, 4},
>              {2, 6, 5, 9, 7, 3, 8, 4, 1},
>              {4, 8, 9, 5, 6, 1, 2, 7, 3},
>              {3, 1, 7, 4, 8, 2, 9, 6, 5},
>              {1, 3, 6, 7, 4, 8, 5, 9, 2},
>              {9, 7, 4, 2, 1, 5, 6, 3, 8},
>              {5, 2, 8, 6, 3, 9, 4, 1, 7}}
> ```
> 
> **输出:**有效
> 
> **输入:**
> 
> ```
> board[][] = {{5, 5, 5, 5, 5, 5, 5, 5, 5}, 
>              {5, 5, 5, 5, 5, 5, 5, 5, 5},
>              {5, 5, 5, 5, 5, 5, 5, 5, 5},
>              {5, 5, 5, 5, 5, 5, 5, 5, 5},
>              {5, 5, 5, 5, 5, 5, 5, 5, 5},
>              {5, 5, 5, 5, 5, 5, 5, 5, 5},
>              {5, 5, 5, 5, 5, 5, 5, 5, 5},
>              {5, 5, 5, 5, 5, 5, 5, 5, 5},
>              {5, 5, 5, 5, 5, 5, 5, 5, 5}}
> ```
> 
> **输出:**无效

**方法:**通过检查以下条件可以解决问题:

*   检查**板[][]** 阵列的每一行是否只存储范围[ **1** 、 **9** 中的唯一值。
*   检查**板[][]** 阵列的每一列是否存储范围[ **1** 、 **9** 的唯一值。
*   检查**板【】【】**阵列的所有可能的 **3 × 3 子矩阵**是否存储范围【 **1** 、 **9** 的唯一值。

按照以下步骤解决问题:

*   [遍历给定矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/) **棋盘[][]** 。
*   检查是否满足上述条件。
*   如果不满足上述任一条件，则打印“**无效**”。
*   否则，打印“**有效**”。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;
#define N 9

// Function to check if all elements
// of the board[][] array store
// value in the range[1, 9]
bool isinRange(int board[][N])
{

    // Traverse board[][] array
    for (int i = 0; i < N;
         i++) {
        for (int j = 0; j < N;
             j++) {

            // Check if board[i][j]
            // lies in the range
            if (board[i][j] <= 0 || board[i][j] > 9) {
                return false;
            }
        }
    }
    return true;
}

// Function to check if the solution
// of sudoku puzzle is valid or not
bool isValidSudoku(int board[][N])
{
    // Check if all elements of board[][]
    // stores value in the range[1, 9]
    if (isinRange(board)
        == false) {
        return false;
    }

    // Stores unique value
    // from 1 to N
    bool unique[N + 1];

    // Traverse each row of
    // the given array
    for (int i = 0; i < N; i++) {

        // Initialize unique[]
        // array to false
        memset(unique, false,
               sizeof(unique));

        // Traverse each column
        // of current row
        for (int j = 0; j < N;
             j++) {

            // Stores the value
            // of board[i][j]
            int Z = board[i][j];

            // Check if current row
            // stores duplicate value
            if (unique[Z]) {
                return false;
            }
            unique[Z] = true;
        }
    }

    // Traverse each column of
    // the given array
    for (int i = 0; i < N; i++) {

        // Initialize unique[]
        // array to false
        memset(unique, false,
               sizeof(unique));

        // Traverse each row
        // of current column
        for (int j = 0; j < N;
             j++) {

            // Stores the value
            // of board[j][i]
            int Z = board[j][i];

            // Check if current column
            // stores duplicate value
            if (unique[Z]) {
                return false;
            }
            unique[Z] = true;
        }
    }

    // Traverse each block of
    // size 3 * 3 in board[][] array
    for (int i = 0; i < N - 2;
         i += 3) {

        // j stores first column of
        // each 3 * 3 block
        for (int j = 0; j < N - 2;
             j += 3) {

            // Initialize unique[]
            // array to false
            memset(unique, false,
                   sizeof(unique));

            // Traverse current block
            for (int k = 0; k < 3;
                 k++) {

                for (int l = 0; l < 3;
                     l++) {

                    // Stores row number
                    // of current block
                    int X = i + k;

                    // Stores column number
                    // of current block
                    int Y = j + l;

                    // Stores the value
                    // of board[X][Y]
                    int Z = board[X][Y];

                    // Check if current block
                    // stores duplicate value
                    if (unique[Z]) {
                        return false;
                    }
                    unique[Z] = true;
                }
            }
        }
    }

    // If all conditions satisfied
    return true;
}

// Driver Code
int main()
{
    int board[N][N]
        = { { 7, 9, 2, 1, 5, 4, 3, 8, 6 },
            { 6, 4, 3, 8, 2, 7, 1, 5, 9 },
            { 8, 5, 1, 3, 9, 6, 7, 2, 4 },
            { 2, 6, 5, 9, 7, 3, 8, 4, 1 },
            { 4, 8, 9, 5, 6, 1, 2, 7, 3 },
            { 3, 1, 7, 4, 8, 2, 9, 6, 5 },
            { 1, 3, 6, 7, 4, 8, 5, 9, 2 },
            { 9, 7, 4, 2, 1, 5, 6, 3, 8 },
            { 5, 2, 8, 6, 3, 9, 4, 1, 7 } };

    if (isValidSudoku(board)) {
        cout << "Valid";
    }
    else {
        cout << "Not Valid";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

static int N = 9;

// Function to check if all elements
// of the board[][] array store
// value in the range[1, 9]
static boolean isinRange(int[][] board)
{

    // Traverse board[][] array
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Check if board[i][j]
            // lies in the range
            if (board[i][j] <= 0 ||
                board[i][j] > 9)
            {
                return false;
            }
        }
    }
    return true;
}

// Function to check if the solution
// of sudoku puzzle is valid or not
static boolean isValidSudoku(int board[][])
{

    // Check if all elements of board[][]
    // stores value in the range[1, 9]
    if (isinRange(board) == false)
    {
        return false;
    }

    // Stores unique value
    // from 1 to N
    boolean[] unique = new boolean[N + 1];

    // Traverse each row of
    // the given array
    for(int i = 0; i < N; i++)
    {

        // Initialize unique[]
        // array to false
        Arrays.fill(unique, false);

        // Traverse each column
        // of current row
        for(int j = 0; j < N; j++)
        {

            // Stores the value
            // of board[i][j]
            int Z = board[i][j];

            // Check if current row
            // stores duplicate value
            if (unique[Z])
            {
                return false;
            }
            unique[Z] = true;
        }
    }

    // Traverse each column of
    // the given array
    for(int i = 0; i < N; i++)
    {

        // Initialize unique[]
        // array to false
        Arrays.fill(unique, false);

        // Traverse each row
        // of current column
        for(int j = 0; j < N; j++)
        {

            // Stores the value
            // of board[j][i]
            int Z = board[j][i];

            // Check if current column
            // stores duplicate value
            if (unique[Z])
            {
                return false;
            }
            unique[Z] = true;
        }
    }

    // Traverse each block of
    // size 3 * 3 in board[][] array
    for(int i = 0; i < N - 2; i += 3)
    {

        // j stores first column of
        // each 3 * 3 block
        for(int j = 0; j < N - 2; j += 3)
        {

            // Initialize unique[]
            // array to false
            Arrays.fill(unique, false);

            // Traverse current block
            for(int k = 0; k < 3; k++)
            {
                for(int l = 0; l < 3; l++)
                {

                    // Stores row number
                    // of current block
                    int X = i + k;

                    // Stores column number
                    // of current block
                    int Y = j + l;

                    // Stores the value
                    // of board[X][Y]
                    int Z = board[X][Y];

                    // Check if current block
                    // stores duplicate value
                    if (unique[Z])
                    {
                        return false;
                    }
                    unique[Z] = true;
                }
            }
        }
    }

    // If all conditions satisfied
    return true;
}

// Driver Code
public static void main(String[] args)
{
    int[][] board = { { 7, 9, 2, 1, 5, 4, 3, 8, 6 },
                      { 6, 4, 3, 8, 2, 7, 1, 5, 9 },
                      { 8, 5, 1, 3, 9, 6, 7, 2, 4 },
                      { 2, 6, 5, 9, 7, 3, 8, 4, 1 },
                      { 4, 8, 9, 5, 6, 1, 2, 7, 3 },
                      { 3, 1, 7, 4, 8, 2, 9, 6, 5 },
                      { 1, 3, 6, 7, 4, 8, 5, 9, 2 },
                      { 9, 7, 4, 2, 1, 5, 6, 3, 8 },
                      { 5, 2, 8, 6, 3, 9, 4, 1, 7 } };

    if (isValidSudoku(board))
    {
        System.out.println("Valid");
    }
    else
    {
        System.out.println("Not Valid");
    }
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if all elements
# of the board[][] array store
# value in the range[1, 9]
def isinRange(board):

  N = 9

  # Traverse board[][] array
  for i in range(0, N):
    for j in range(0, N):

      # Check if board[i][j]
      # lies in the range
      if ((board[i][j] <= 0) or
          (board[i][j] > 9)):
        return False

  return True

# Function to check if the solution
# of sudoku puzzle is valid or not
def isValidSudoku(board):

  N = 9

  # Check if all elements of board[][]
  # stores value in the range[1, 9]
  if (isinRange(board) == False):
    return False

  # Stores unique value
  # from 1 to N
  unique = [False] * (N + 1)

  # Traverse each row of
  # the given array
  for i in range(0, N):

    # Initialize unique[]
    # array to false
    for m in range(0, N + 1):
      unique[m] = False

    # Traverse each column
    # of current row
    for j in range(0, N):

      # Stores the value
      # of board[i][j]
      Z = board[i][j]

      # Check if current row
      # stores duplicate value
      if (unique[Z] == True):
        return False

      unique[Z] = True

  # Traverse each column of
  # the given array
  for i in range(0, N):

    # Initialize unique[]
    # array to false
    for m in range(0, N + 1):
      unique[m] = False

    # Traverse each row
    # of current column
    for j in range(0, N):

      # Stores the value
      # of board[j][i]
      Z = board[j][i]

      # Check if current column
      # stores duplicate value
      if (unique[Z] == True):
        return False

      unique[Z] = True

  # Traverse each block of
  # size 3 * 3 in board[][] array
  for i in range(0, N - 2, 3):

    # j stores first column of
    # each 3 * 3 block
    for j in range(0, N - 2, 3):

      # Initialize unique[]
      # array to false
      for m in range(0, N + 1):
        unique[m] = False

      # Traverse current block
      for k in range(0, 3):
        for l in range(0, 3):

          # Stores row number
          # of current block
          X = i + k

          # Stores column number
          # of current block
          Y = j + l

          # Stores the value
          # of board[X][Y]
          Z = board[X][Y]

          # Check if current block
          # stores duplicate value
          if (unique[Z] == True):
            return False

          unique[Z] = True

  # If all conditions satisfied
  return True

# Driver Code
if __name__ == '__main__':

  board = [ [ 7, 9, 2, 1, 5, 4, 3, 8, 6 ],
            [ 6, 4, 3, 8, 2, 7, 1, 5, 9 ],
            [ 8, 5, 1, 3, 9, 6, 7, 2, 4 ],
            [ 2, 6, 5, 9, 7, 3, 8, 4, 1 ],
            [ 4, 8, 9, 5, 6, 1, 2, 7, 3 ],
            [ 3, 1, 7, 4, 8, 2, 9, 6, 5 ],
            [ 1, 3, 6, 7, 4, 8, 5, 9, 2 ],
            [ 9, 7, 4, 2, 1, 5, 6, 3, 8 ],
            [ 5, 2, 8, 6, 3, 9, 4, 1, 7 ] ]

  if (isValidSudoku(board)):
    print("Valid")
  else:
    print("Not Valid")

# This code is contributed by akhilsaini
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

static int N = 9;

// Function to check if all elements
// of the board[][] array store
// value in the range[1, 9]
static bool isinRange(int[, ] board)
{

    // Traverse board[][] array
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Check if board[i][j]
            // lies in the range
            if (board[i, j] <= 0 ||
                board[i, j] > 9)
            {
                return false;
            }
        }
    }
    return true;
}

// Function to check if the solution
// of sudoku puzzle is valid or not
static bool isValidSudoku(int[, ] board)
{

    // Check if all elements of board[][]
    // stores value in the range[1, 9]
    if (isinRange(board) == false)
    {
        return false;
    }

    // Stores unique value
    // from 1 to N
    bool[] unique = new bool[N + 1];

    // Traverse each row of
    // the given array
    for(int i = 0; i < N; i++)
    {

        // Initialize unique[]
        // array to false
        Array.Fill(unique, false);

        // Traverse each column
        // of current row
        for(int j = 0; j < N; j++)
        {

            // Stores the value
            // of board[i][j]
            int Z = board[i, j];

            // Check if current row
            // stores duplicate value
            if (unique[Z])
            {
                return false;
            }
            unique[Z] = true;
        }
    }

    // Traverse each column of
    // the given array
    for(int i = 0; i < N; i++)
    {

        // Initialize unique[]
        // array to false
        Array.Fill(unique, false);

        // Traverse each row
        // of current column
        for(int j = 0; j < N; j++)
        {

            // Stores the value
            // of board[j][i]
            int Z = board[j, i];

            // Check if current column
            // stores duplicate value
            if (unique[Z])
            {
                return false;
            }
            unique[Z] = true;
        }
    }

    // Traverse each block of
    // size 3 * 3 in board[][] array
    for(int i = 0; i < N - 2; i += 3)
    {

        // j stores first column of
        // each 3 * 3 block
        for(int j = 0; j < N - 2; j += 3)
        {

            // Initialize unique[]
            // array to false
            Array.Fill(unique, false);

            // Traverse current block
            for(int k = 0; k < 3; k++)
            {
                for(int l = 0; l < 3; l++)
                {

                    // Stores row number
                    // of current block
                    int X = i + k;

                    // Stores column number
                    // of current block
                    int Y = j + l;

                    // Stores the value
                    // of board[X][Y]
                    int Z = board[X, Y];

                    // Check if current block
                    // stores duplicate value
                    if (unique[Z])
                    {
                        return false;
                    }
                    unique[Z] = true;
                }
            }
        }
    }

    // If all conditions satisfied
    return true;
}

// Driver Code
public static void Main()
{
    int[,] board = { { 7, 9, 2, 1, 5, 4, 3, 8, 6 },
                      { 6, 4, 3, 8, 2, 7, 1, 5, 9 },
                      { 8, 5, 1, 3, 9, 6, 7, 2, 4 },
                      { 2, 6, 5, 9, 7, 3, 8, 4, 1 },
                      { 4, 8, 9, 5, 6, 1, 2, 7, 3 },
                      { 3, 1, 7, 4, 8, 2, 9, 6, 5 },
                      { 1, 3, 6, 7, 4, 8, 5, 9, 2 },
                      { 9, 7, 4, 2, 1, 5, 6, 3, 8 },
                      { 5, 2, 8, 6, 3, 9, 4, 1, 7 } };

    if (isValidSudoku(board))
    {
        Console.WriteLine("Valid");
    }
    else
    {
        Console.WriteLine("Not Valid");
    }
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

var N = 9;

// Function to check if all elements
// of the board[][] array store
// value in the range[1, 9]
function isinRange(board)
{

    // Traverse board[][] array
    for(var i = 0; i < N; i++)
    {
        for(var j = 0; j < N; j++)
        {

            // Check if board[i][j]
            // lies in the range
            if (board[i][j] <= 0 ||
                board[i][j] > 9)
            {
                return false;
            }
        }
    }
    return true;
}

// Function to check if the solution
// of sudoku puzzle is valid or not
function isValidSudoku(board)
{

    // Check if all elements of board[][]
    // stores value in the range[1, 9]
    if (isinRange(board) == false)
    {
        return false;
    }

    // Stores unique value
    // from 1 to N
    var unique = Array(N+1).fill(false);

    // Traverse each row of
    // the given array
    for(var i = 0; i < N; i++)
    {
        unique = Array(N+1).fill(false);

        // Traverse each column
        // of current row
        for(var j = 0; j < N; j++)
        {

            // Stores the value
            // of board[i][j]
            var Z = board[i][j];

            // Check if current row
            // stores duplicate value
            if (unique[Z])
            {
                return false;
            }
            unique[Z] = true;
        }
    }

    // Traverse each column of
    // the given array
    for(var i = 0; i < N; i++)
    {

        // Initialize unique[]
        // array to false
        unique = Array(N+1).fill(false);

        // Traverse each row
        // of current column
        for(var j = 0; j < N; j++)
        {

            // Stores the value
            // of board[j][i]
            var Z = board[j][i];

            // Check if current column
            // stores duplicate value
            if (unique[Z])
            {
                return false;
            }
            unique[Z] = true;
        }
    }

    // Traverse each block of
    // size 3 * 3 in board[][] array
    for(var i = 0; i < N - 2; i += 3)
    {

        // j stores first column of
        // each 3 * 3 block
        for(var j = 0; j < N - 2; j += 3)
        {

            // Initialize unique[]
            // array to false
            unique = Array(N+1).fill(false);

            // Traverse current block
            for(var k = 0; k < 3; k++)
            {
                for(var l = 0; l < 3; l++)
                {

                    // Stores row number
                    // of current block
                    var X = i + k;

                    // Stores column number
                    // of current block
                    var Y = j + l;

                    // Stores the value
                    // of board[X][Y]
                    var Z = board[X][Y];

                    // Check if current block
                    // stores duplicate value
                    if (unique[Z])
                    {
                        return false;
                    }
                    unique[Z] = true;
                }
            }
        }
    }

    // If all conditions satisfied
    return true;
}

// Driver Code
var board = [ [ 7, 9, 2, 1, 5, 4, 3, 8, 6 ],
                  [ 6, 4, 3, 8, 2, 7, 1, 5, 9 ],
                  [ 8, 5, 1, 3, 9, 6, 7, 2, 4 ],
                  [ 2, 6, 5, 9, 7, 3, 8, 4, 1 ],
                  [ 4, 8, 9, 5, 6, 1, 2, 7, 3 ],
                  [ 3, 1, 7, 4, 8, 2, 9, 6, 5 ],
                  [ 1, 3, 6, 7, 4, 8, 5, 9, 2 ],
                  [ 9, 7, 4, 2, 1, 5, 6, 3, 8 ],
                  [ 5, 2, 8, 6, 3, 9, 4, 1, 7 ] ];
if (isValidSudoku(board))
{
    document.write("Valid");
}
else
{
    document.write("Not Valid");
}

</script>
```

**Output:** 

```
Valid
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*