# 检查矩阵的行是否可以重新排列，以使第一列的按位异或非零

> 原文:[https://www . geeksforgeeks . org/check-如果矩阵的行可以重新排列，则对第一列非零进行按位异或运算/](https://www.geeksforgeeks.org/check-if-rows-of-a-matrix-can-be-rearranged-to-make-bitwise-xor-of-first-column-non-zero/)

给定一个大小为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **mat[][]** ，任务是检查是否有可能重新排列矩阵的行元素，使得第一列元素的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)为非零。如果可能，则打印**“是”**否则打印**“否”**。

**示例:**

> **输入:** mat[][] = {{1，1，2}，{2，2，2}，{3，3，3}}
> 输出:是
> T6】解释:T8】将第一行重新排列为 2，1，1 后。
> 第一列的按位异或将是 3，即(2 ^ 2 ^ 3)。
> 
> **输入:** mat[][] = {{1，1，1}，{2，2，2}，{3，3，3}}
> **输出:** No
> **解释:**
> 由于所有重排给出相同的第一个元素，因此唯一的组合是等于零的(1 ^ 2 ^ 3)。
> 因此，不可能获得第一列的非零按位异或。

**方法:**按照以下步骤解决问题:

*   求矩阵第一列元素的按位异或，并将其存储在变量 **res** 中。
*   如果 **res** 为非零，则打印**“是”**。
*   否则，遍历所有行，并在一行中找到与该行第一个索引处的元素不相等的元素。
*   如果在上述步骤的任何一行中不存在这样的元素，则打印**“否”**，否则打印**“是”。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if there is any
// row where number of unique elements
// are greater than 1
string checkRearrangements(
    vector<vector<int> > mat, int N, int M)
{
    // Iterate over the matrix
    for (int i = 0; i < N; i++) {

        for (int j = 1; j < M; j++) {

            if (mat[i][0] != mat[i][j]) {

                return "Yes";
            }
        }
    }
    return "No";
}

// Function to check if it is possible
// to rearrange mat[][] such that XOR
// of its first column is non-zero
string nonZeroXor(vector<vector<int> > mat,
                  int N, int M)
{
    int res = 0;

    // Find bitwise XOR of the first
    // column of mat[][]
    for (int i = 0; i < N; i++) {

        res = res ^ mat[i][0];
    }

    // If bitwise XOR of the first
    // column of mat[][] is non-zero
    if (res != 0)
        return "Yes";

    // Otherwise check rearrangements
    else
        return checkRearrangements(mat, N, M);
}

// Driver Code
int main()
{
    // Given Matrix mat[][]
    vector<vector<int> > mat
        = { { 1, 1, 2 },
            { 2, 2, 2 },
            { 3, 3, 3 } };

    int N = mat.size();
    int M = mat[0].size();

    // Function Call
    cout << nonZeroXor(mat, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to check if there is any
// row where number of unique elements
// are greater than 1
static String checkRearrangements(int[][] mat,
                                  int N, int M)
{
  // Iterate over the matrix
  for (int i = 0; i < N; i++)
  {
    for (int j = 1; j < M; j++)
    {
      if (mat[i][0] != mat[i][j])
      {
        return "Yes";
      }
    }
  }
  return "No";
}

// Function to check if it is possible
// to rearrange mat[][] such that XOR
// of its first column is non-zero
static String nonZeroXor(int[][] mat,
                         int N, int M)
{
  int res = 0;

  // Find bitwise XOR of the
  // first column of mat[][]
  for (int i = 0; i < N; i++)
  {
    res = res ^ mat[i][0];
  }

  // If bitwise XOR of the first
  // column of mat[][] is non-zero
  if (res != 0)
    return "Yes";

  // Otherwise check
  // rearrangements
  else
    return checkRearrangements(mat,
                               N, M);
}

// Driver Code
public static void main(String[] args)
{
  // Given Matrix mat[][]
  int[][] mat = {{1, 1, 2},
                 {2, 2, 2},
                 {3, 3, 3}};

  int N = mat.length;
  int M = mat[0].length;

  // Function Call
  System.out.print(nonZeroXor(mat,
                              N, M));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if there is any
# row where number of unique elements
# are greater than 1
def checkRearrangements(mat, N, M):

    # Iterate over the matrix
    for i in range(N):
        for j in range(1, M):
            if (mat[i][0] != mat[i][j]):
                return "Yes"

    return "No"

# Function to check if it is possible
# to rearrange mat[][] such that XOR
# of its first column is non-zero
def nonZeroXor(mat, N, M):

    res = 0

    # Find bitwise XOR of the first
    # column of mat[][]
    for i in range(N):
        res = res ^ mat[i][0]

    # If bitwise XOR of the first
    # column of mat[][] is non-zero
    if (res != 0):
        return "Yes"

    # Otherwise check rearrangements
    else:
        return checkRearrangements(mat, N, M)

# Driver Code
if __name__ == "__main__":

    # Given Matrix mat[][]
    mat = [ [ 1, 1, 2 ],
            [ 2, 2, 2 ],
            [ 3, 3, 3 ] ]

    N = len(mat)
    M = len(mat[0])

    # Function Call
    print(nonZeroXor(mat, N, M))

# This code is contributed by chitranayal
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Function to check if there is any
// row where number of unique elements
// are greater than 1
static String checkRearrangements(int[,] mat,
                                  int N, int M)
{

  // Iterate over the matrix
  for(int i = 0; i < N; i++)
  {
    for(int j = 1; j < M; j++)
    {
      if (mat[i, 0] != mat[i, j])
      {
        return "Yes";
      }
    }
  }
  return "No";
}

// Function to check if it is possible
// to rearrange [,]mat such that XOR
// of its first column is non-zero
static String nonZeroXor(int[,] mat,
                         int N, int M)
{
  int res = 0;

  // Find bitwise XOR of the
  // first column of [,]mat
  for(int i = 0; i < N; i++)
  {
    res = res ^ mat[i, 0];
  }

  // If bitwise XOR of the first
  // column of [,]mat is non-zero
  if (res != 0)
    return "Yes";

  // Otherwise check
  // rearrangements
  else
    return checkRearrangements(mat,
                               N, M);
}

// Driver Code
public static void Main(String[] args)
{

  // Given Matrix [,]mat
  int[,] mat = { { 1, 1, 2 },
                 { 2, 2, 2 },
                 { 3, 3, 3 } };

  int N = mat.GetLength(0);
  int M = mat.GetLength(1);

  // Function Call
  Console.Write(nonZeroXor(mat,
                           N, M));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to check if there is any
// row where number of unique elements
// are greater than 1
function checkRearrangements(mat, N, M)
{
  // Iterate over the matrix
  for (let i = 0; i < N; i++)
  {
    for (let j = 1; j < M; j++)
    {
      if (mat[i][0] != mat[i][j])
      {
        return "Yes";
      }
    }
  }
  return "No";
}

// Function to check if it is possible
// to rearrange mat[][] such that XOR
// of its first column is non-zero
function nonZeroXor(mat, N, M)
{
  let res = 0;

  // Find bitwise XOR of the
  // first column of mat[][]
  for (let i = 0; i < N; i++)
  {
    res = res ^ mat[i][0];
  }

  // If bitwise XOR of the first
  // column of mat[][] is non-zero
  if (res != 0)
    return "Yes";

  // Otherwise check
  // rearrangements
  else
    return checkRearrangements(mat,
                               N, M);
}

// Driver Code

    // Given Matrix mat[][]
  let mat = [[1, 1, 2],
             [2, 2, 2],
             [3, 3, 3]];

  let N = mat.length;
  let M = mat[0].length;

  // Function Call
  document.write(nonZeroXor(mat,
                              N, M));

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*