# 构造一个二进制矩阵，其每一行和每一列的和是一个素数

> 原文:[https://www . geeksforgeeks . org/construct-a-binary-matrix-其每行每列的和是素数/](https://www.geeksforgeeks.org/construct-a-binary-matrix-whose-sum-of-each-row-and-column-is-a-prime-number/)

给定一个整数 **N** ，任务是构造一个大小为 **N * N** 的[二进制矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/)，使得矩阵的每行和每列之和为一个[素数](https://www.geeksforgeeks.org/prime-numbers/)。

**示例:**

> **输入:**N = 2
> T3】输出:
> 
> ```
> 1 1
> 1 1
> ```
> 
> **说明:**
> 0 之和<sup>第</sup>行= 1 + 1 = 2(质数)
> 1 之和<sup>第</sup>行= 1 + 1 = 2(质数)
> 0 之和<sup>第</sup>列= 1 + 1 = 2(质数)
> 1 之和<sup>第</sup>列= 1 + 1 = 2(质数)
> 
> **输入:**N = 4
> T3】输出:
> 
> ```
> 1 0 0 1 
> 0 1 1 0 
> 0 1 1 0 
> 1 0 0 1 
> ```

**方法:**按照以下步骤解决问题:

*   初始化一个[二进制矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-binary-matrix-or-not/)，比如说 **mat[][]** 大小 **N * N** 。
*   将 **mat[i][i]** 的所有可能值更新为 **1** 。
*   将**mat[I][N–I-1]**的所有可能值更新为 **1** 。
*   如果 **N** 是[奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则更新值**mat【N/2】【0】**和**mat【0】【N/2】**至 **1** 。

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to construct
// the required binary matrix
void constructBinaryMat(int N)
{
    // Stores binary value with row
    // and column sum as prime number
    int mat[N][N];

    // initialize the binary matrix mat[][]
    memset(mat, 0, sizeof(mat));

    // Update all possible values of
    // mat[i][i] to 1
    for (int i = 0; i < N; i++) {
        mat[i][i] = 1;
    }

    // Update all possible values of
    // mat[i][N - i -1]
    for (int i = 0; i < N; i++) {
        mat[i][N - i - 1] = 1;
    }

    // Check if N is an odd number
    if (N % 2 != 0) {

        // Update mat[N / 2][0] to 1
        mat[N / 2][0] = 1;

        // Update mat[0][N / 2] to 1
        mat[0][N / 2] = 1;
    }

    // Print required binary matrix
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            cout << mat[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    int N = 5;

    constructBinaryMat(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to construct
// the required binary matrix
static void constructBinaryMat(int N)
{
  // Stores binary value with row
  // and column sum as prime number
  int mat[][] = new int[N][N];

  // Update all possible values
  // of mat[i][i] to 1
  for (int i = 0; i < N; i++)
  {
    mat[i][i] = 1;
  }

  // Update all possible values
  // of mat[i][N - i -1]
  for (int i = 0; i < N; i++)
  {
    mat[i][N - i - 1] = 1;
  }

  // Check if N is an odd
  // number
  if (N % 2 != 0)
  {
    // Update mat[N / 2][0]
    // to 1
    mat[N / 2][0] = 1;

    // Update mat[0][N / 2]
    // to 1
    mat[0][N / 2] = 1;
  }

  // Print required binary matrix
  for (int i = 0; i < N; i++)
  {
    for (int j = 0; j < N; j++)
    {
      System.out.print(mat[i][j] + " ");
    }
    System.out.println();
  }
}

// Driver Code
public static void main(String[] args)
{
  int N = 5;
  constructBinaryMat(N);
}
}

// This code is contributed by Chitranayal
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to construct
# the required binary matrix
def constructBinaryMat(N):

    # Stores binary value with row
    # and column sum as prime number
    mat = [[0 for i in range(N)]
              for i in range(N)]

    # Initialize the binary matrix mat[][]
    # memset(mat, 0, sizeof(mat));

    # Update all possible values of
    # mat[i][i] to 1
    for i in range(N):
        mat[i][i] = 1

    # Update all possible values of
    # mat[i][N - i -1]
    for i in range(N):
        mat[i][N - i - 1] = 1

    # Check if N is an odd number
    if (N % 2 != 0):

        # Update mat[N / 2][0] to 1
        mat[N // 2][0] = 1

        # Update mat[0][N / 2] to 1
        mat[0][N // 2] = 1

    # Print required binary matrix
    for i in range(N):
        for j in range(N):
            print(mat[i][j], end = " ")

        print()

# Driver Code
if __name__ == '__main__':

    N = 5

    constructBinaryMat(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to construct
// the required binary matrix
static void constructBinaryMat(int N)
{
  // Stores binary value with row
  // and column sum as prime number
  int [,]mat = new int[N, N];

  // Update all possible values
  // of mat[i,i] to 1
  for (int i = 0; i < N; i++)
  {
    mat[i, i] = 1;
  }

  // Update all possible values
  // of mat[i,N - i -1]
  for (int i = 0; i < N; i++)
  {
    mat[i, N - i - 1] = 1;
  }

  // Check if N is an odd
  // number
  if (N % 2 != 0)
  {
    // Update mat[N / 2,0]
    // to 1
    mat[N / 2, 0] = 1;

    // Update mat[0,N / 2]
    // to 1
    mat[0, N / 2] = 1;
  }

  // Print required binary matrix
  for (int i = 0; i < N; i++)
  {
    for (int j = 0; j < N; j++)
    {
      Console.Write(mat[i, j] + " ");
    }
    Console.WriteLine();
  }
}

// Driver Code
public static void Main(String[] args)
{
  int N = 5;
  constructBinaryMat(N);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to construct
// the required binary matrix
function constructBinaryMat(N)
{

    // Stores binary value with row
    // and column sum as prime number
    var mat = Array.from(Array(N), () =>
                         Array(N).fill(0));

    // Update all possible values of
    // mat[i][i] to 1
    for(var i = 0; i < N; i++)
    {
        mat[i][i] = 1;
    }

    // Update all possible values of
    // mat[i][N - i -1]
    for(var i = 0; i < N; i++)
    {
        mat[i][N - i - 1] = 1;
    }

    // Check if N is an odd number
    if (N % 2 != 0)
    {

        // Update mat[N / 2][0] to 1
        mat[parseInt(N / 2)][0] = 1;

        // Update mat[0][N / 2] to 1
        mat[0][parseInt(N / 2)] = 1;
    }

    // Print required binary matrix
    for(var i = 0; i < N; i++)
    {
        for(var j = 0; j < N; j++)
        {
            document.write( mat[i][j] + " ");
        }
        document.write("<br>");
    }
}

// Driver Code
var N = 5;

constructBinaryMat(N);

// This code is contributed by rutvik_56

</script>
```

**Output:** 

```
1 0 1 0 1 
0 1 0 1 0 
1 0 1 0 0 
0 1 0 1 0 
1 0 0 0 1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*