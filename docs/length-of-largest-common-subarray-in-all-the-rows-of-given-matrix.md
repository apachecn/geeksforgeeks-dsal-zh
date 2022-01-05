# 给定矩阵所有行中最大公共子阵列的长度

> 原文:[https://www . geeksforgeeks . org/给定矩阵所有行中最大公共子阵列的长度/](https://www.geeksforgeeks.org/length-of-largest-common-subarray-in-all-the-rows-of-given-matrix/)

给定大小为 **N×M** 的[矩阵](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/) **mat[][]** ，其中[矩阵](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)的每一行是来自**【1，M】**的元素的[排列，任务是找到](https://www.geeksforgeeks.org/check-if-an-array-is-a-permutation-of-numbers-from-1-to-n/)[矩阵](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)的每一行中存在的子阵列的最大长度。

**示例:**

> **输入:** mat[][] = {{1，2，3，4，5}，{2，3，4，1，5}，{5，2，3，4，1}，{1，5，2，3，4} }
> T3】输出:3
> T6】解释:T8】每行中，{2，3，4 }是矩阵所有行中存在的最长的公共子数组。
> 
> **输入:** mat[][] = {{4，5，1，2，3，6，7}，{1，2，4，5，7，6，3}，{2，7，3，4，5，1，6}}
> **输出:** 2

**天真方法:**解决问题最简单的方法是[生成矩阵第一行](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)所有可能的子阵列，然后检查剩余行是否包含该子阵列。

***时间复杂度:**O(m×N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过创建一个[矩阵](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)，比如 **dp[][]** 来优化，该矩阵存储每行中元素的位置，然后检查每行中当前和以前的元素索引是否有 **1** 的差异。按照以下步骤解决问题:

*   初始化一个矩阵，比如说 **dp[][]** ，存储每行中每个元素的位置。
*   要填充矩阵 **dp[][]** ，[使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M-1】**中迭代，并将**DP[I][arr[I][j]】**的值修改为 **j** 。
*   初始化变量，比如说**和**存储所有行中最长的公共子阵列的长度，**透镜**存储所有行中公共子阵列的长度。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，M-1】**中迭代，并执行以下步骤:
    *   初始化一个布尔变量**检查**为 **1** ，检查每一行中 **a[i][0]** 是否在 **a[i-1][0]** 之后。
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N-1】**中迭代，并执行以下步骤:
        *   如果 **dp[j][arr[0][i-1]] + 1！= dp[j][arr[0][i]]** ，将校验值修改为 **0** 并终止循环。
    *   如果**检查**的值为 **1** ，则将 **len** 的值增加 **1** ，并将 **ans** 的值修改为 **max(ans，len)** 。
    *   如果**检查**的值为 **0** ，则将**透镜**的值修改为 **1** 。
*   完成以上步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find longest common subarray
// in all the rows of the matrix
int largestCommonSubarray(
    vector<vector<int> > arr,
    int n, int m)
{
    // Array to store the position
    // of element in every row
    int dp[n][m + 1];

    // Traverse the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            // Store the position of
            // every element in every row
            dp[i][arr[i][j]] = j;
        }
    }

    // Variable to store length of largest
    // common Subarray
    int ans = 1;
    int len = 1;

    // Traverse through the matrix column
    for (int i = 1; i < m; i++) {
        // Variable to check if every row has
        // arr[i][j] next to arr[i-1][j] or not
        bool check = true;

        // Traverse through the matrix rows
        for (int j = 1; j < n; j++) {
            // Check if arr[i][j] is next to
            // arr[i][j-1] in every row or not
            if (dp[j][arr[0][i - 1]] + 1
                != dp[j][arr[0][i]]) {
                check = false;
                break;
            }
        }

        // If every row has arr[0][j] next
        // to arr[0][j-1] increment len by 1
        // and update the value of ans
        if (check) {
            len++;
            ans = max(ans, len);
        }
        else {
            len = 1;
        }
    }
    return ans;
}

// Driver Code
int main()
{

    // Given Input
    int n = 4;
    int m = 5;
    vector<vector<int> > arr{ { 4, 5, 1, 2, 3, 6, 7 },
                              { 1, 2, 4, 5, 7, 6, 3 },
                              { 2, 7, 3, 4, 5, 1, 6 } };

    int N = arr.size();
    int M = arr[0].size();

    // Function Call
    cout << largestCommonSubarray(arr, N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to find longest common subarray
// in all the rows of the matrix
static int largestCommonSubarray(int[][] arr,
                                 int n, int m)
{

    // Array to store the position
    // of element in every row
    int dp[][] = new int[n][m + 1];

    // Traverse the matrix
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {

            // Store the position of
            // every element in every row
            dp[i][arr[i][j]] = j;
        }
    }

    // Variable to store length of largest
    // common Subarray
    int ans = 1;
    int len = 1;

    // Traverse through the matrix column
    for(int i = 1; i < m; i++)
    {

        // Variable to check if every row has
        // arr[i][j] next to arr[i-1][j] or not
        boolean check = true;

        // Traverse through the matrix rows
        for(int j = 1; j < n; j++)
        {

            // Check if arr[i][j] is next to
            // arr[i][j-1] in every row or not
            if (dp[j][arr[0][i - 1]] + 1 !=
                dp[j][arr[0][i]])
            {
                check = false;
                break;
            }
        }

        // If every row has arr[0][j] next
        // to arr[0][j-1] increment len by 1
        // and update the value of ans
        if (check)
        {
            len++;
            ans = Math.max(ans, len);
        }
        else
        {
            len = 1;
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{

    // Given Input
    int n = 4;
    int m = 5;
    int[][] arr = { { 4, 5, 1, 2, 3, 6, 7 },
                    { 1, 2, 4, 5, 7, 6, 3 },
                    { 2, 7, 3, 4, 5, 1, 6 } };

    int N = arr.length;
    int M = arr[0].length;

    // Function Call
    System.out.println(largestCommonSubarray(arr, N, M));
}
}

// This code is contributed by avijitmondal1998
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find longest common subarray
# in all the rows of the matrix
def largestCommonSubarray(arr, n, m):

    # Array to store the position
    # of element in every row
    dp = [[0 for i in range(m+1)] for j in range(n)]

    # Traverse the matrix
    for i in range(n):
        for j in range(m):

            # Store the position of
            # every element in every row
            dp[i][arr[i][j]] = j

    # Variable to store length of largest
    # common Subarray
    ans = 1
    len1 = 1

    # Traverse through the matrix column
    for i in range(1,m,1):
        # Variable to check if every row has
        # arr[i][j] next to arr[i-1][j] or not
        check = True

        # Traverse through the matrix rows
        for j in range(1,n,1):
            # Check if arr[i][j] is next to
            # arr[i][j-1] in every row or not
            if (dp[j][arr[0][i - 1]] + 1 != dp[j][arr[0][i]]):
                check = False
                break

        # If every row has arr[0][j] next
        # to arr[0][j-1] increment len by 1
        # and update the value of ans
        if (check):
            len1 += 1
            ans = max(ans, len1)

        else:
            len1 = 1

    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    n = 4
    m = 5
    arr = [[4, 5, 1, 2, 3, 6, 7],
           [1, 2, 4, 5, 7, 6, 3],
           [2, 7, 3, 4, 5, 1, 6]]

    N = len(arr)
    M = len(arr[0])

    # Function Call
    print(largestCommonSubarray(arr, N, M))

    # This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach

      // Function to find longest common subarray
      // in all the rows of the matrix
      function largestCommonSubarray(arr, n, m) {
          // Array to store the position
          // of element in every row
          let dp = Array(n).fill().map(() => Array(m + 1));

          // Traverse the matrix
          for (let i = 0; i < n; i++) {
              for (let j = 0; j < m; j++) {
                  // Store the position of
                  // every element in every row
                  dp[i][arr[i][j]] = j;
              }
          }

          // Variable to store length of largest
          // common Subarray
          let ans = 1;
          let len = 1;

          // Traverse through the matrix column
          for (let i = 1; i < m; i++) {
              // Variable to check if every row has
              // arr[i][j] next to arr[i-1][j] or not
              let check = true;

              // Traverse through the matrix rows
              for (let j = 1; j < n; j++) {
                  // Check if arr[i][j] is next to
                  // arr[i][j-1] in every row or not
                  if (dp[j][arr[0][i - 1]] + 1
                      != dp[j][arr[0][i]]) {
                      check = false;
                      break;
                  }
              }

              // If every row has arr[0][j] next
              // to arr[0][j-1] increment len by 1
              // and update the value of ans
              if (check) {
                  len++;
                  ans = Math.max(ans, len);
              }
              else {
                  len = 1;
              }
          }
          return ans;
      }

      // Driver Code

      // Given Input
      let n = 4;
      let m = 5;
      let arr = [[4, 5, 1, 2, 3, 6, 7],
      [1, 2, 4, 5, 7, 6, 3],
      [2, 7, 3, 4, 5, 1, 6]];

      let N = arr.length;
      let M = arr[0].length;

      // Function Call
      document.write(largestCommonSubarray(arr, N, M));

  // This code is contributed by Potta Lokesh

  </script>
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find longest common subarray
// in all the rows of the matrix
static int largestCommonSubarray(int [,]arr,
                                 int n, int m)
{

    // Array to store the position
    // of element in every row
    int [,]dp = new int[n,m + 1];

    // Traverse the matrix
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {

            // Store the position of
            // every element in every row
            dp[i,arr[i,j]] = j;
        }
    }

    // Variable to store length of largest
    // common Subarray
    int ans = 1;
    int len = 1;

    // Traverse through the matrix column
    for(int i = 1; i < m; i++)
    {

        // Variable to check if every row has
        // arr[i][j] next to arr[i-1][j] or not
        bool check = true;

        // Traverse through the matrix rows
        for(int j = 1; j < n; j++)
        {

            // Check if arr[i][j] is next to
            // arr[i][j-1] in every row or not
            if (dp[j,arr[0,i - 1]] + 1 !=
                dp[j,arr[0,i]])
            {
                check = false;
                break;
            }
        }

        // If every row has arr[0][j] next
        // to arr[0][j-1] increment len by 1
        // and update the value of ans
        if (check == true)
        {
            len++;
            ans = Math.Max(ans, len);
        }
        else
        {
            len = 1;
        }
    }
    return ans;
}

// Driver code
public static void Main()
{

    // Given Input
    int [,]arr = { { 4, 5, 1, 2, 3, 6, 7 },
                    { 1, 2, 4, 5, 7, 6, 3 },
                    { 2, 7, 3, 4, 5, 1, 6 } };

    int N = 3;
    int M = 7;

    // Function Call
    Console.Write(largestCommonSubarray(arr, N, M));
}
}

// This code is contributed by _saurabh_jaiswal.
```

**Output**

```
2
```

***时间复杂度:** O(N×M)*
***辅助空间:** O(N×M)*