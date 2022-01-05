# 使二进制矩阵的每对相邻单元不同所需的最小行或列交换

> 原文:[https://www . geeksforgeeks . org/最小行或列交换-二进制矩阵的每对相邻单元都需要进行区分/](https://www.geeksforgeeks.org/minimum-row-or-column-swaps-required-to-make-every-pair-of-adjacent-cell-of-a-binary-matrix-distinct/)

给定维度为 **N x N** 的二元[矩阵](https://www.geeksforgeeks.org/matrix/) **M[][]** ，任务是通过交换最小数量的行或列来使给定矩阵的同一行或列中的每对相邻单元格不同。

**示例**

> **输入:** M[][] = {{0，1，1，0}，{0，1，1，0}，{1，0，0，1}，{1，0，0，1}}，N = 4
> **输出:** 2
> **解释:**
> 第 1 步:交换第 2 行和第 3 行将矩阵修改为以下表示形式:
> M[]= { { 0，1，1，0}，
> { 1，0，0 1} }
> 步骤 1:交换第一列和第二列将矩阵修改为以下表示形式:
> M[][] = { { 1，0，1，0}，
> { 0，1，0，1}，
> { 1，0，1，0}，
> { 0，1，0，1} }
> 
> **输入:** M[][] = {{0，1，1}，{1，1，0}，{1，0，0}，{1，1，1}}，N = 3
> **输出:** -1

**方法:**给定的问题可以基于以下观察来解决:

*   在所需的矩阵中，从一个角开始的任何子矩阵必须使所有单元的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于 **0** 。
*   还可以观察到，在**行**或**列**中最多应该存在两种类型的序列，即{0，1，0，1}和{1，0，1，1}。因此，通过将一个序列的**异或**值与 **1** 进行交换，可以从另一个序列生成一个序列。
*   因此，通过根据所需格式仅制作第一**列**和第一**行**，所需的总互换将被最小化。

按照以下步骤解决问题:

1.  [遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/) **M[][]** ，检查所有元素 **M[i][0]** 、 **M[0][j]** 、 **M[0][0]** 、 **M[i][j]** 是否为 **1** ，然后返回 **-1** 。
2.  初始化变量 **rowSum** 、 **colSum** 、 **rowSwap** 和 **colSwap** 为 **0** 。
    1.  在范围**【0，N-1】**内进行导线测量，如果**M【I】【0】**等于 **i%2** 和 **colSwap** 的话，将 **rowSum** 增加**M【I】【0】**、 **colSum** 增加**M【0】【I】**并将 **rowSwap** 增加 **1**
    2.  如果**行总和**不等于 **N/2** 或 **(N+1)/2** 中的任何一个，则返回 **-1** 。
    3.  如果 **colSum** 不等于 **N/2 或(N+1)/2** 中的任何一个，则返回 **-1** 。
    4.  分配**colSwap = N–colSwap**if、 **N%2** 和 **colSwap%2** 都不等于 0 和**row swap = N–row swap**if、 **N%2** 和 **rowSwap%2** 都不等于 0。
    5.  分配 **colSwap** 等于 **colSwap** 和 **N-colSwap** 的最小值， **rowSwap** 等于 **rowSwap** 和 **N-rowSwap** 的最小值。
3.  最后将结果打印为 **(rowSum+colSum)/2** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return number of moves
// to convert matrix into chessboard
int minSwaps(vector<vector<int> >& b)
{
    // Size of the matrix
    int n = b.size();

    // Traverse the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (b[0][0] ^ b[0][j] ^ b[i][0] ^ b[i][j])
                return -1;
        }
    }

    // Initialize rowSum to count 1s in row
    int rowSum = 0;

    // Initialize colSum to count 1s in column
    int colSum = 0;

    // To store no. of rows to be corrected
    int rowSwap = 0;

    // To store no. of columns to be corrected
    int colSwap = 0;

    // Traverse in the range [0, N-1]
    for (int i = 0; i < n; i++) {
        rowSum += b[i][0];
        colSum += b[0][i];
        rowSwap += b[i][0] == i % 2;
        colSwap += b[0][i] == i % 2;
    }
    // Check if rows is either N/2 or
    // (N+1)/2 and return -1
    if (rowSum != n / 2 && rowSum != (n + 1) / 2)
        return -1;

    // Check if rows is either N/2
    // or (N+1)/2  and return -1
    if (colSum != n / 2 && colSum != (n + 1) / 2)
        return -1;

    // Check if N is odd
    if (n % 2 == 1) {

        // Check if column required to be
        // corrected is odd and then
        // assign N-colSwap to colSwap
        if (colSwap % 2)
            colSwap = n - colSwap;

        // Check if rows required to
        // be corrected is odd and then
        // assign N-rowSwap to rowSwap
        if (rowSwap % 2)
            rowSwap = n - rowSwap;
    }
    else {

        // Take min of colSwap and N-colSwap
        colSwap = min(colSwap, n - colSwap);

        // Take min of rowSwap and N-rowSwap
        rowSwap = min(rowSwap, n - rowSwap);
    }

    // Finally return answer
    return (rowSwap + colSwap) / 2;
}

// Driver Code
int main()
{

    // Given matrix
    vector<vector<int> > M = { { 0, 1, 1, 0 },
                               { 0, 1, 1, 0 },
                               { 1, 0, 0, 1 },
                               { 1, 0, 0, 1 } };

    // Function Call
    int ans = minSwaps(M);

    // Print answer
    cout << ans;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*; 
class GFG
{

  // Function to return number of moves
  // to convert matrix into chessboard
  public static int minSwaps(int[][] b)
  {

    // Size of the matrix
    int n = b.length;

    // Traverse the matrix
    for (int i = 0; i < n; i++)
    {
      for (int j = 0; j < n; j++)
      {

        if ((b[0][0] ^ b[0][j] ^ b[i][0] ^ b[i][j]) == 1)
        {
          return -1;
        }
      }
    }

    // Initialize rowSum to count 1s in row
    int rowSum = 0;

    // Initialize colSum to count 1s in column
    int colSum = 0;

    // To store no. of rows to be corrected
    int rowSwap = 0;

    // To store no. of columns to be corrected
    int colSwap = 0;

    // Traverse in the range [0, N-1]
    for (int i = 0; i < n; i++)
    {
      rowSum += b[i][0];
      colSum += b[0][i];
      int cond1 = 0;
      int cond2 = 0;
      if(b[i][0] == i % 2)
        cond1 = 1;
      if(b[0][i] == i % 2)
        cond2 = 1;
      rowSwap += cond1;
      colSwap += cond2;
    }

    // Check if rows is either N/2 or
    // (N+1)/2 and return -1
    if (rowSum != n / 2 && rowSum != (n + 1) / 2)
      return -1;

    // Check if rows is either N/2
    // or (N+1)/2  and return -1
    if (colSum != n / 2 && colSum != (n + 1) / 2)
      return -1;

    // Check if N is odd
    if (n % 2 == 1)
    {

      // Check if column required to be
      // corrected is odd and then
      // assign N-colSwap to colSwap
      if ((colSwap % 2) == 1)
        colSwap = n - colSwap;

      // Check if rows required to
      // be corrected is odd and then
      // assign N-rowSwap to rowSwap
      if ((rowSwap % 2) == 1)
        rowSwap = n - rowSwap;
    }
    else
    {

      // Take min of colSwap and N-colSwap
      colSwap = Math.min(colSwap, n - colSwap);

      // Take min of rowSwap and N-rowSwap
      rowSwap = Math.min(rowSwap, n - rowSwap);
    }

    // Finally return answer
    return (rowSwap + colSwap) / 2;
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given matrix
    int[][] M = { { 0, 1, 1, 0 },
                 { 0, 1, 1, 0 },
                 { 1, 0, 0, 1 },
                 { 1, 0, 0, 1 } };

    // Function Call
    int ans = minSwaps(M);

    // Print answer
    System.out.println(ans);
  }
}

// This code is contributed by rohitsingh07052
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return number of moves
# to convert matrix into chessboard
def minSwaps(b):

    # Size of the matrix
    n = len(b)

    # Traverse the matrix
    for i in range(n):
        for j in range(n):
            if (b[0][0] ^ b[0][j] ^
                b[i][0] ^ b[i][j]):
                return -1

    # Initialize rowSum to count 1s in row
    rowSum = 0

    # Initialize colSum to count 1s in column
    colSum = 0

    # To store no. of rows to be corrected
    rowSwap = 0

    # To store no. of columns to be corrected
    colSwap = 0

    # Traverse in the range [0, N-1]
    for i in range(n):
        rowSum += b[i][0]
        colSum += b[0][i]
        rowSwap += b[i][0] == i % 2
        colSwap += b[0][i] == i % 2

    # Check if rows is either N/2 or
    # (N+1)/2 and return -1
    if (rowSum != n // 2 and
        rowSum != (n + 1) // 2):
        return -1

    # Check if rows is either N/2
    # or (N+1)/2  and return -1
    if (colSum != n // 2 and
        colSum != (n + 1) // 2):
        return -1

    # Check if N is odd
    if (n % 2 == 1):

        # Check if column required to be
        # corrected is odd and then
        # assign N-colSwap to colSwap
        if (colSwap % 2):
            colSwap = n - colSwap

        # Check if rows required to
        # be corrected is odd and then
        # assign N-rowSwap to rowSwap
        if (rowSwap % 2):
            rowSwap = n - rowSwap

    else:

        # Take min of colSwap and N-colSwap
        colSwap = min(colSwap, n - colSwap)

        # Take min of rowSwap and N-rowSwap
        rowSwap = min(rowSwap, n - rowSwap)

    # Finally return answer
    return (rowSwap + colSwap) // 2

# Driver Code
if __name__ == "__main__":

    # Given matrix
    M = [ [ 0, 1, 1, 0 ],
          [ 0, 1, 1, 0 ],
          [ 1, 0, 0, 1 ],
          [ 1, 0, 0, 1 ] ]

    # Function Call
    ans = minSwaps(M)

    # Print answer
    print(ans)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to return number of moves
  // to convert matrix into chessboard
  public static int minSwaps(int[,] b)
  {

    // Size of the matrix
    int n = b.GetLength(0);

    // Traverse the matrix
    for (int i = 0; i < n; i++)
    {
      for (int j = 0; j < n; j++)
      {

        if ((b[0, 0] ^ b[0, j] ^ b[i, 0] ^ b[i, j]) == 1)
        {
          return -1;
        }
      }
    }

    // Initialize rowSum to count 1s in row
    int rowSum = 0;

    // Initialize colSum to count 1s in column
    int colSum = 0;

    // To store no. of rows to be corrected
    int rowSwap = 0;

    // To store no. of columns to be corrected
    int colSwap = 0;

    // Traverse in the range [0, N-1]
    for (int i = 0; i < n; i++)
    {
      rowSum += b[i, 0];
      colSum += b[0, i];
      int cond1 = 0;
      int cond2 = 0;
      if(b[i, 0] == i % 2)
        cond1 = 1;
      if(b[0, i] == i % 2)
        cond2 = 1;
      rowSwap += cond1;
      colSwap += cond2;
    }

    // Check if rows is either N/2 or
    // (N+1)/2 and return -1
    if (rowSum != n / 2 && rowSum != (n + 1) / 2)
      return -1;

    // Check if rows is either N/2
    // or (N+1)/2  and return -1
    if (colSum != n / 2 && colSum != (n + 1) / 2)
      return -1;

    // Check if N is odd
    if (n % 2 == 1)
    {

      // Check if column required to be
      // corrected is odd and then
      // assign N-colSwap to colSwap
      if ((colSwap % 2) == 1)
        colSwap = n - colSwap;

      // Check if rows required to
      // be corrected is odd and then
      // assign N-rowSwap to rowSwap
      if ((rowSwap % 2) == 1)
        rowSwap = n - rowSwap;
    }
    else
    {

      // Take min of colSwap and N-colSwap
      colSwap = Math.Min(colSwap, n - colSwap);

      // Take min of rowSwap and N-rowSwap
      rowSwap = Math.Min(rowSwap, n - rowSwap);
    }

    // Finally return answer
    return (rowSwap + colSwap) / 2;
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given matrix
    int[,] M = { { 0, 1, 1, 0 },
                 { 0, 1, 1, 0 },
                 { 1, 0, 0, 1 },
                 { 1, 0, 0, 1 } };

    // Function Call
    int ans = minSwaps(M);

    // Print answer
    Console.WriteLine(ans);
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// javascript program for the above approach

  // Function to return number of moves
  // to convert matrix into chessboard
  function minSwaps(b)
  {

    // Size of the matrix
    var n = b.length;

    // Traverse the matrix
    for (i = 0; i < n; i++)
    {
      for (j = 0; j < n; j++)
      {

        if ((b[0][0] ^ b[0][j] ^ b[i][0] ^ b[i][j]) == 1)
        {
          return -1;
        }
      }
    }

    // Initialize rowSum to count 1s in row
    var rowSum = 0;

    // Initialize colSum to count 1s in column
    var colSum = 0;

    // To store no. of rows to be corrected
    var rowSwap = 0;

    // To store no. of columns to be corrected
    var colSwap = 0;

    // Traverse in the range [0, N-1]
    for (i = 0; i < n; i++)
    {
      rowSum += b[i][0];
      colSum += b[0][i];
      var cond1 = 0;
      var cond2 = 0;
      if(b[i][0] == i % 2)
        cond1 = 1;
      if(b[0][i] == i % 2)
        cond2 = 1;
      rowSwap += cond1;
      colSwap += cond2;
    }

    // Check if rows is either N/2 or
    // (N+1)/2 and return -1
    if (rowSum != n / 2 && rowSum != (n + 1) / 2)
      return -1;

    // Check if rows is either N/2
    // or (N+1)/2  and return -1
    if (colSum != n / 2 && colSum != (n + 1) / 2)
      return -1;

    // Check if N is odd
    if (n % 2 == 1)
    {

      // Check if column required to be
      // corrected is odd and then
      // assign N-colSwap to colSwap
      if ((colSwap % 2) == 1)
        colSwap = n - colSwap;

      // Check if rows required to
      // be corrected is odd and then
      // assign N-rowSwap to rowSwap
      if ((rowSwap % 2) == 1)
        rowSwap = n - rowSwap;
    }
    else
    {

      // Take min of colSwap and N-colSwap
      colSwap = Math.min(colSwap, n - colSwap);

      // Take min of rowSwap and N-rowSwap
      rowSwap = Math.min(rowSwap, n - rowSwap);
    }

    // Finally return answer
    return (rowSwap + colSwap) / 2;
  }

  // Driver Code

var M = [[ 0, 1, 1, 0 ],
             [ 0, 1, 1, 0 ],
             [ 1, 0, 0, 1 ],
             [ 1, 0, 0, 1 ] ];

// Function Call
var ans = minSwaps(M);

// Print answer
document.write(ans);

// This code contributed by Princi Singh

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*