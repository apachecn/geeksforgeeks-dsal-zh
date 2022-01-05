# 找到最小移动，将所有元素放入矩阵的一个单元格中

> 原文:[https://www . geeksforgeeks . org/find-最小移动数-将所有元素纳入矩阵的一个单元/](https://www.geeksforgeeks.org/find-minimum-moves-to-bring-all-elements-in-one-cell-of-a-matrix/)

给定一个矩阵 **mat[][]** ，一对索引 **X** 和 **Y** ，任务是找出移动的次数，将矩阵的所有非零元素带到给定的单元格 **(X，Y)** 。

> 移动包括将任意单元格中的元素移动到其四个方向相邻的单元格，即左、右、上、下。

**例:**

> **输入:** mat[][] = {{1，0}，{1，0}}，X = 1，Y = 1
> **输出:** 3
> **解释:**
> 所需招式= >
> 对于指数(0，0) = > 2
> 对于指数(1，0) = > 1
> 所需总招式= 3
> **输入:** mat[][] = {{1，0，0}

**方法:**想法是遍历矩阵，对于矩阵的每个非零元素，找到当前像元(比如说 **(A，B)** )到矩阵的目标像元 **(X，Y)** 的距离为:

```
moves = abs(x - i) + abs(y - j)
```

上述公式对所有非零元素的所有距离的总和就是所需的结果。
以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum number of moves to
// bring all non-zero element
// in one cell of the matrix

#include <bits/stdc++.h>
using namespace std;

const int M = 4;
const int N = 5;

// Function to find the minimum
// number of moves to bring all
// elements in one cell of matrix
void no_of_moves(int Matrix[M][N],
                int x, int y)
{

    // Moves variable to store
    // the sum of number of moves
    int moves = 0;

    // Loop to count the number
    // of the moves
    for (int i = 0; i < M; i++) {

        for (int j = 0; j < N; j++) {

            // Condition to check that
            // the current cell is a
            // non-zero element
            if (Matrix[i][j] != 0) {
                moves += abs(x - i);

                moves += abs(y - j);
            }
        }
    }

    cout << moves << "\n";
}

// Driver Code
int main()
{
    // Coordinates of given cell
    int x = 3;
    int y = 2;

    // Given Matrix
    int Matrix[M][N] = { { 1, 0, 1, 1, 0 },
                        { 0, 1, 1, 0, 1 },
                        { 0, 0, 1, 1, 0 },
                        { 1, 1, 1, 0, 0 } };

    // Element to be moved
    int num = 1;

    // Function call
    no_of_moves(Matrix, x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum number of moves to
// bring all non-zero element
// in one cell of the matrix
class GFG{

static int M = 4;
static int N = 5;

// Function to find the minimum
// number of moves to bring all
// elements in one cell of matrix
public static void no_of_moves(int[][] Matrix,
                               int x, int y)
{

    // Moves variable to store
    // the sum of number of moves
    int moves = 0;

    // Loop to count the number
    // of the moves
    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Condition to check that
            // the current cell is a
            // non-zero element
            if (Matrix[i][j] != 0)
            {
                moves += Math.abs(x - i);
                moves += Math.abs(y - j);
            }
        }
    }
    System.out.println(moves);
}

// Driver code
public static void main(String[] args)
{

    // Coordinates of given cell
    int x = 3;
    int y = 2;

    // Given Matrix
    int[][] Matrix = { { 1, 0, 1, 1, 0 },
                       { 0, 1, 1, 0, 1 },
                       { 0, 0, 1, 1, 0 },
                       { 1, 1, 1, 0, 0 } };

    // Element to be moved
    int num = 1;

    // Function call
    no_of_moves(Matrix, x, y);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum number of moves to
# bring all non-zero element
# in one cell of the matrix
M = 4
N = 5

# Function to find the minimum
# number of moves to bring all
# elements in one cell of matrix
def no_of_moves(Matrix, x, y):

    # Moves variable to store
    # the sum of number of moves
    moves = 0

    # Loop to count the number
    # of the moves
    for i in range(M):
        for j in range(N):

            # Condition to check that
            # the current cell is a
            # non-zero element
            if (Matrix[i][j] != 0):
                moves += abs(x - i)
                moves += abs(y - j)

    print(moves)

# Driver Code
if __name__ == '__main__':

    # Coordinates of given cell
    x = 3
    y = 2

    # Given Matrix
    Matrix = [ [ 1, 0, 1, 1, 0 ],
               [ 0, 1, 1, 0, 1 ],
               [ 0, 0, 1, 1, 0 ],
               [ 1, 1, 1, 0, 0 ] ]

    # Element to be moved
    num = 1

    # Function call
    no_of_moves(Matrix, x, y)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the
// minimum number of moves to
// bring all non-zero element
// in one cell of the matrix
using System;

class GFG{

static int M = 4;
static int N = 5;

// Function to find the minimum
// number of moves to bring all
// elements in one cell of matrix
public static void no_of_moves(int[,] Matrix,
                               int x, int y)
{

    // Moves variable to store
    // the sum of number of moves
    int moves = 0;

    // Loop to count the number
    // of the moves
    for(int i = 0; i < M; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // Condition to check that
            // the current cell is a
            // non-zero element
            if (Matrix[i, j] != 0)
            {
                moves += Math.Abs(x - i);
                moves += Math.Abs(y - j);
            }
        }
    }
    Console.WriteLine(moves);
}

// Driver code
public static void Main(String[] args)
{

    // Coordinates of given cell
    int x = 3;
    int y = 2;

    // Given matrix
    int[,] Matrix = { { 1, 0, 1, 1, 0 },
                      { 0, 1, 1, 0, 1 },
                      { 0, 0, 1, 1, 0 },
                      { 1, 1, 1, 0, 0 } };

    // Function call
    no_of_moves(Matrix, x, y);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// minimum number of moves to
// bring all non-zero element
// in one cell of the matrix

let M = 4;
let N = 5;

// Function to find the minimum
// number of moves to bring all
// elements in one cell of matrix
function no_of_moves(Matrix, x, y)
{

    // Moves variable to store
    // the sum of number of moves
    let moves = 0;

    // Loop to count the number
    // of the moves
    for(let i = 0; i < M; i++)
    {
        for(let j = 0; j < N; j++)
        {

            // Condition to check that
            // the current cell is a
            // non-zero element
            if (Matrix[i][j] != 0)
            {
                moves += Math.abs(x - i);
                moves += Math.abs(y - j);
            }
        }
    }
   document.write(moves);
}

// Driver Code

    // Coordinates of given cell
    let x = 3;
    let y = 2;

    // Given Matrix
    let Matrix = [[ 1, 0, 1, 1, 0 ],
                  [ 0, 1, 1, 0, 1 ],
                  [ 0, 0, 1, 1, 0 ],
                  [ 1, 1, 1, 0, 0 ]];

    // Element to be moved
    let num = 1;

    // Function call
    no_of_moves(Matrix, x, y);

</script>
```

**Output:** 

```
27
```

**时间复杂度:***O(N<sup>2</sup>)*
**辅助空间:** *O(1)*