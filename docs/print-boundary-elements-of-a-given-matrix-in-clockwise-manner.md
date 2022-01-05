# 顺时针打印给定矩阵的边界元素

> 原文:[https://www . geeksforgeeks . org/print-给定矩阵的边界元素-顺时针方向/](https://www.geeksforgeeks.org/print-boundary-elements-of-a-given-matrix-in-clockwise-manner/)

给定一个尺寸为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **arr[][]** ，任务是以顺时针形式打印给定矩阵的边界元素。

**示例:**

> **输入:** arr[][] = {{1，2，3}，{4，5，6}，{7，8，9} }
> **输出:** 1 2 3 6 9 8 7 4
> **说明:**
> 矩阵的边界元素有:
> **1 2 3**
> T13】45**6**
> T18<强
> 
> **输入:** arr[][] = {{11，12，33}，{64，57，61}，{74，88，39}}
> **输出:** 11 12 33 61 39 88 74 64

**天真法:**解决这个问题最简单的方法是[遍历给定矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)[检查当前元素是否为边界元素](https://www.geeksforgeeks.org/java-program-to-print-boundary-elements-of-the-matrix/)。如果发现为真，则打印该元素。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是[遍历](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)只遍历矩阵的**首末行**和**首末列**。按照以下步骤解决问题:

*   打印矩阵的第一行。
*   打印矩阵除第一行以外的最后一列。
*   打印矩阵的最后一行，除了最后一列。
*   打印矩阵的第一列，第一行和最后一行除外。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the boundary elements
// of the matrix in clockwise
void boundaryTraversal(vector<vector<int> > arr, int N,
                       int M)
{

  // Print the first row
  for (int i = 0; i < M; i++)
  {
    cout << arr[0][i] << " ";
  }

  // Print the last column
  // except the first row
  for (int i = 1; i < N; i++)
  {
    cout << arr[i][M - 1] << " ";
  }

  // Print the last row
  // except the last column
  if (N > 1)
  {

    // Print the last row
    for (int i = M - 2; i >= 0; i--)
    {
      cout << arr[N - 1][i] << " ";
    }
  }

  // Print the first column except
  // the first and last row
  if (M > 1) {

    // Print the first column
    for (int i = N - 2; i > 0; i--) {
      cout << arr[i][0] << " ";
    }
  }
}

// Driver Code
int main()
{
  vector<vector<int> > arr{ { 1, 2, 3 },
                           { 4, 5, 6 },
                           { 7, 8, 9 } };
  int N = arr.size();
  int M = arr[0].size();

  // Function Call
  boundaryTraversal(arr, N, M);
  return 0;
}

// This code is contributed by Dharanendra L V
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG {

    // Function to print the boundary elements
    // of the matrix in clockwise
    public static void boundaryTraversal(
        int arr[][], int N, int M)
    {

        // Print the first row
        for (int i = 0; i < M; i++) {
            System.out.print(arr[0][i] + " ");
        }

        // Print the last column
        // except the first row
        for (int i = 1; i < N; i++) {
            System.out.print(arr[i][M - 1] + " ");
        }

        // Print the last row
        // except the last column
        if (N > 1) {

            // Print the last row
            for (int i = M - 2; i >= 0; i--) {
                System.out.print(arr[N - 1][i] + " ");
            }
        }

        // Print the first column except
        // the first and last row
        if (M > 1) {

            // Print the first column
            for (int i = N - 2; i > 0; i--) {
                System.out.print(arr[i][0] + " ");
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[][]
            = { { 1, 2, 3 },
                { 4, 5, 6 },
                { 7, 8, 9 } };
        int N = arr.length;
        int M = arr[0].length;

        // Function Call
        boundaryTraversal(arr, N, M);
    }
}
```

## 蟒蛇 3

```
# Python program of the above approach

# Function to print the boundary elements
# of the matrix in clockwise
def boundaryTraversal(arr, N, M):

    # Print the first row
    for i in range(M):
        print(arr[0][i], end = " ");

    # Print the last column
    # except the first row
    for i in range(1, N):
        print(arr[i][M - 1], end = " ");

    # Print the last row
    # except the last column
    if (N > 1):

        # Print the last row
        for i in range(M - 2, -1, -1):
            print(arr[N - 1][i], end = " ");

    # Print the first column except
    # the first and last row
    if (M > 1):

        # Print the first column
        for i in range(N - 2, 0, -1):
            print(arr[i][0], end = " ");

# Driver Code
if __name__ == '__main__':
    arr = [[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]];
    N = len(arr);
    M = len(arr[0]);

    # Function Call
    boundaryTraversal(arr, N, M);

    # This code is contributed by 29AjayKumar
```

## C#

```
// C# program of the above approach
using System;

class GFG{

// Function to print the boundary elements
// of the matrix in clockwise
static void boundaryTraversal(int[,] arr,
                              int N, int M)
{

    // Print the first row
    for(int i = 0; i < M; i++)
    {
        Console.Write(arr[0, i] + " ");
    }

    // Print the last column
    // except the first row
    for(int i = 1; i < N; i++)
    {
        Console.Write(arr[i, M - 1] + " ");
    }

    // Print the last row
    // except the last column
    if (N > 1)
    {

        // Print the last row
        for(int i = M - 2; i >= 0; i--)
        {
            Console.Write(arr[N - 1, i] + " ");
        }
    }

    // Print the first column except
    // the first and last row
    if (M > 1)
    {

        // Print the first column
        for(int i = N - 2; i > 0; i--)
        {
            Console.Write(arr[i, 0] + " ");
        }
    }
}

// Driver code   
static void Main()
{
    int[,] arr = { { 1, 2, 3 },
                   { 4, 5, 6 },
                   { 7, 8, 9 } };
    int N = 3;
    int M = 3;

    // Function Call
    boundaryTraversal(arr, N, M);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program of the above approach

// Function to print the boundary elements
// of the matrix in clockwise
function boundaryTraversal(arr, N, M)
{

  // Print the first row
  for (let i = 0; i < M; i++)
  {
    document.write(arr[0][i] + " ");
  }

  // Print the last column
  // except the first row
  for (let i = 1; i < N; i++)
  {
    document.write(arr[i][M - 1] + " ");
  }

  // Print the last row
  // except the last column
  if (N > 1)
  {

    // Print the last row
    for (let i = M - 2; i >= 0; i--)
    {
      document.write(arr[N - 1][i] + " ");
    }
  }

  // Print the first column except
  // the first and last row
  if (M > 1) {

    // Print the first column
    for (let i = N - 2; i > 0; i--) {
      document.write(arr[i][0] + " ");
    }
  }
}

// Driver Code
  let arr = [ [ 1, 2, 3 ],
                           [ 4, 5, 6 ],
                           [ 7, 8, 9 ] ];
  let N = arr.length;
  let M = arr[0].length;

  // Function Call
  boundaryTraversal(arr, N, M);

</script>
```

**Output:** 

```
1 2 3 6 9 8 7 4
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(1)*