# 给定矩阵中大小为 K 的所有正方形子矩阵中的最小元素

> 原文:[https://www . geeksforgeeks . org/全正方形矩阵中的最小元素-给定矩阵中的 k 尺寸子矩阵/](https://www.geeksforgeeks.org/smallest-element-from-all-square-submatrices-of-size-k-from-a-given-matrix/)

给定一个矩阵 **arr[][]** 和一个整数 **K** ，任务是从给定矩阵的所有可能的正方形子矩阵 **K** 中找到最小元素。

**示例:**

> **输入:** K = 2，arr[][] ={ {1，2，3}，{4，5，6}，{7，8，9} }
> **输出:**
> 1 2
> 4 5
> T8】解释:
> 所有可能的大小为 2 的正方形子矩阵中的最小元素如下:
> { {1，2}，{4，5} } - > 1
> { {2，3}，{4
> 
> **输入:** K = 3，
> arr[][] = { {-1，5，4，1，-3}，
> {4，3，1，1，6}，
> {2，-2，5，3，1}，
> {8，5，1，9，-4}，
> {12，3，5，8，1} }
> **输出:**
> -2-2-3
> -2-4】

**天真方法:**解决问题最简单的方法是[从给定的矩阵中生成所有可能的大小为 **K**](https://www.geeksforgeeks.org/given-n-x-n-square-matrix-find-sum-sub-squares-size-k-x-k/) 的正方形子矩阵，并从每个这样的子矩阵中打印最小的元素。

***时间复杂度:**O(N * M * K<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤优化上述方法:

*   遍历矩阵的每一行，对于每一个***arr【I】【j】，*** 就地更新索引***arr【I】【j】***至***arr【I】【j+K–1】***(***0<= j<M–K+1)***。
*   同样，遍历矩阵的每一列，对于每一个***arr【I】【j】，*** 就地更新索引***arr【I】【j】***至***arr【I+K-1】【j】***(***0<= I<N–K+1)***。
*   执行上述操作后，矩阵 ***的左上角子矩阵***(N–K+1)*(M–K+1)***由给定矩阵的所有 **K x K** 子矩阵的所有最小元素组成。***
*   因此，打印大小为***(N–K+1)*(M–K+1)***的子矩阵作为所需输出。

下面是上述方法的实现:

## C++

```
// C++ Program for
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to returns a smallest
// elements of all KxK submatrices
// of a given NxM matrix
vector<vector<int> > matrixMinimum(
       vector<vector<int> > nums, int K)
{
  // Stores the dimensions
  // of the given matrix
  int N = nums.size();
  int M = nums[0].size();

  // Stores the required
  // smallest elements
  vector<vector<int> > res(N - K + 1,
                           vector<int>(M - K + 1));

  // Update the smallest elements row-wise
  for (int i = 0; i < N; i++)
  {
    for (int j = 0; j < M - K + 1; j++)
    {
      int mini = INT_MAX;
      for (int k = j; k < j + K; k++)
      {
        mini = min(mini, nums[i][k]);
      }
      nums[i][j] = mini;
    }
  }

  // Update the minimum column-wise
  for (int j = 0; j < M; j++)
  {
    for (int i = 0; i < N - K + 1; i++)
    {
      int mini = INT_MAX;
      for (int k = i; k < i + K; k++)
      {
        mini = min(mini, nums[k][j]);
      }
      nums[i][j] = mini;
    }
  }

  // Store the final submatrix with
  // required minimum values
  for (int i = 0; i < N - K + 1; i++)
    for (int j = 0; j < M - K + 1; j++)
      res[i][j] = nums[i][j];

  // Return the resultant matrix
  return res;
}

void smallestinKsubmatrices(vector<vector<int> > arr,
                            int K)
{
  // Function Call
  vector<vector<int> > res = matrixMinimum(arr, K);

  // Print resultant matrix with the
  // minimum values of KxK sub-matrix
  for (int i = 0; i < res.size(); i++)
  {
    for (int j = 0; j < res[0].size(); j++)
    {
      cout << res[i][j] << " ";
    }
    cout << endl;
  }
}

// Driver Code
int main()
{

  // Given matrix
  vector<vector<int> > arr = {{-1, 5, 4, 1, -3},
                              {4, 3, 1, 1, 6},
                              {2, -2, 5, 3, 1},
                              {8, 5, 1, 9, -4},
                              {12, 3, 5, 8, 1}};

  // Given K
  int K = 3;

  smallestinKsubmatrices(arr, K);
}

// This code is contributed by Chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to returns a smallest
    // elements of all KxK submatrices
    // of a given NxM matrix
    public static int[][] matrixMinimum(
        int[][] nums, int K)
    {
        // Stores the dimensions
        // of the given matrix
        int N = nums.length;
        int M = nums[0].length;

        // Stores the required
        // smallest elements
        int[][] res
            = new int[N - K + 1][M - K + 1];

        // Update the smallest elements row-wise
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M - K + 1; j++) {

                int min = Integer.MAX_VALUE;
                for (int k = j; k < j + K; k++) {
                    min = Math.min(min, nums[i][k]);
                }
                nums[i][j] = min;
            }
        }

        // Update the minimum column-wise
        for (int j = 0; j < M; j++) {
            for (int i = 0; i < N - K + 1; i++) {
                int min = Integer.MAX_VALUE;
                for (int k = i; k < i + K; k++) {
                    min = Math.min(min, nums[k][j]);
                }
                nums[i][j] = min;
            }
        }

        // Store the final submatrix with
        // required minimum values
        for (int i = 0; i < N - K + 1; i++)
            for (int j = 0; j < M - K + 1; j++)
                res[i][j] = nums[i][j];

        // Return the resultant matrix
        return res;
    }

    public static void smallestinKsubmatrices(
        int arr[][], int K)
    {
        // Function Call
        int[][] res = matrixMinimum(arr, K);

        // Print resultant matrix with the
        // minimum values of KxK sub-matrix
        for (int i = 0; i < res.length; i++) {
            for (int j = 0; j < res[0].length; j++) {
                System.out.print(res[i][j] + " ");
            }
            System.out.println();
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given matrix
        int[][] arr = { { -1, 5, 4, 1, -3 },
                        { 4, 3, 1, 1, 6 },
                        { 2, -2, 5, 3, 1 },
                        { 8, 5, 1, 9, -4 },
                        { 12, 3, 5, 8, 1 } };

        // Given K
        int K = 3;

        smallestinKsubmatrices(arr, K);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to returns a smallest
# elements of all KxK submatrices
# of a given NxM matrix
def matrixMinimum(nums, K):

    # Stores the dimensions
    # of the given matrix
    N = len(nums)
    M = len(nums[0])

    # Stores the required
    # smallest elements
    res = [[0 for x in range(M - K + 1)]
              for y in range(N - K + 1)]

    # Update the smallest elements row-wise
    for i in range(N):
        for j in range(M - K + 1):
            mn = sys.maxsize

            for k in range(j, j + K):
                mn = min(mn, nums[i][k])

            nums[i][j] = mn

    # Update the minimum column-wise
    for j in range(M):
        for i in range(N - K + 1):
            mn = sys.maxsize

            for k in range(i, i + K):
                mn = min(mn, nums[k][j])

            nums[i][j] = mn

    # Store the final submatrix with
    # required minimum values
    for i in range(N - K + 1):
        for j in range(M - K + 1):
            res[i][j] = nums[i][j]

    # Return the resultant matrix
    return res

def smallestinKsubmatrices(arr, K):

    # Function call
    res = matrixMinimum(arr, K)

    # Print resultant matrix with the
    # minimum values of KxK sub-matrix
    for i in range(len(res)):
        for j in range(len(res[0])):
            print(res[i][j], end = " ")

        print()

# Driver Code

# Given matrix
arr = [ [ -1, 5, 4, 1, -3 ],
        [ 4, 3, 1, 1, 6 ],
        [ 2, -2, 5, 3, 1 ],
        [ 8, 5, 1, 9, -4 ],
        [ 12, 3, 5, 8, 1 ] ]

# Given K
K = 3

# Function call
smallestinKsubmatrices(arr, K)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to returns a smallest
// elements of all KxK submatrices
// of a given NxM matrix
public static int[,] matrixMinimum(int[,] nums,
                                   int K)
{

    // Stores the dimensions
    // of the given matrix
    int N = nums.GetLength(0);
    int M = nums.GetLength(1);

    // Stores the required
    // smallest elements
    int[,] res = new int[N - K + 1,
                         M - K + 1];

    // Update the smallest elements row-wise
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M - K + 1; j++)
        {
            int min = int.MaxValue;
            for(int k = j; k < j + K; k++)
            {
                min = Math.Min(min, nums[i, k]);
            }
            nums[i, j] = min;
        }
    }

    // Update the minimum column-wise
    for(int j = 0; j < M; j++)
    {
        for(int i = 0; i < N - K + 1; i++)
        {
            int min = int.MaxValue;
            for(int k = i; k < i + K; k++)
            {
                min = Math.Min(min, nums[k, j]);
            }
            nums[i, j] = min;
        }
    }

    // Store the readonly submatrix with
    // required minimum values
    for(int i = 0; i < N - K + 1; i++)
        for(int j = 0; j < M - K + 1; j++)
            res[i, j] = nums[i, j];

    // Return the resultant matrix
    return res;
}

public static void smallestinKsubmatrices(int [,]arr,
                                          int K)
{

    // Function call
    int[,] res = matrixMinimum(arr, K);

    // Print resultant matrix with the
    // minimum values of KxK sub-matrix
    for(int i = 0; i < res.GetLength(0); i++)
    {
        for(int j = 0; j < res.GetLength(1); j++)
        {
            Console.Write(res[i, j] + " ");
        }
        Console.WriteLine();
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given matrix
    int[,] arr = { { -1, 5, 4, 1, -3 },
                   { 4, 3, 1, 1, 6 },
                   { 2, -2, 5, 3, 1 },
                   { 8, 5, 1, 9, -4 },
                   { 12, 3, 5, 8, 1 } };

    // Given K
    int K = 3;

    smallestinKsubmatrices(arr, K);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to returns a smallest
    // elements of all KxK submatrices
    // of a given NxM matrix
    function matrixMinimum(
        nums, K)
    {
        // Stores the dimensions
        // of the given matrix
        let N = nums.length;
        let M = nums[0].length;

        // Stores the required
        // smallest elements
        let res
            = new Array(N - K + 1);
        for (var i = 0; i < res.length; i++) {
            res[i] = new Array(2);
        }

        // Update the smallest elements row-wise
        for (let i = 0; i < N; i++) {
            for (let j = 0; j < M - K + 1; j++) {

                let min = Number.MAX_VALUE;
                for (let k = j; k < j + K; k++) {
                    min = Math.min(min, nums[i][k]);
                }
                nums[i][j] = min;
            }
        }

        // Update the minimum column-wise
        for (let j = 0; j < M; j++) {
            for (let i = 0; i < N - K + 1; i++) {
                let min = Number.MAX_VALUE;
                for (let k = i; k < i + K; k++) {
                    min = Math.min(min, nums[k][j]);
                }
                nums[i][j] = min;
            }
        }

        // Store the final submatrix with
        // required minimum values
        for (let i = 0; i < N - K + 1; i++)
            for (let j = 0; j < M - K + 1; j++)
                res[i][j] = nums[i][j];

        // Return the resultant matrix
        return res;
    }

    function smallestinKsubmatrices(arr, K)
    {
        // Function Call
        let res = matrixMinimum(arr, K);

        // Print resultant matrix with the
        // minimum values of KxK sub-matrix
        for (let i = 0; i < res.length; i++) {
            for (let j = 0; j < res[0].length; j++) {
                document.write(res[i][j] + " ");
            }
            document.write("<br/>");
        }
    }

// Driver Code

     // Given matrix
        let arr = [[ -1, 5, 4, 1, -3 ],
                        [ 4, 3, 1, 1, 6 ],
                        [ 2, -2, 5, 3, 1 ],
                        [ 8, 5, 1, 9, -4 ],
                        [ 12, 3, 5, 8, 1 ]];

        // Given K
        let K = 3;

        smallestinKsubmatrices(arr, K);

</script>
```

**Output:** 

```
-2 -2 -3 
-2 -2 -4 
-2 -2 -4
```

***时间复杂度:** O( max(N，M) <sup>3</sup> )*
***辅助空间:** O( (N-K+1)*(M-K+1) )*