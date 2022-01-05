# 所需的最小移除量，使得剩余数组模 M 的总和为 X

> 原文:[https://www . geeksforgeeks . org/minimum-removes-required-so-sum-of-remain-array-modal-m-is-x/](https://www.geeksforgeeks.org/minimum-removals-required-such-that-sum-of-remaining-array-modulo-m-is-x/)

给定一个由 **N** 正整数和整数 **X** 和 **M** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，其中 **0 < = X < M** ，任务是找到需要移除的元素的最小数量，使得剩余数组的[和模 **M** 等于 **X** 。如果不可能，打印 **-1** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {3，2，1，2}，M = 4，X = 2
> **输出:** 1
> **说明:**可以删除索引(从 0 开始)1 或 3 处的元素之一。如果 arr[1]被删除，那么 arr[]修改为{3，1，2}，和% M = 6 % 4 = 2，等于 X = 2。
> 
> **输入:** arr[] = {3，2，1，3}，M = 4，X = 3
> **输出:** 1
> **解释:**移除元素 arr[1]( = 2)。因此，arr[]修改为{3，1，3}，总和% M = 7 % 4 = 3，等于 X = 3。

**朴素方法:**最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)的所有可能子集，对于每个子集，检查去除子集后数组的[和模 **M**](https://www.geeksforgeeks.org/sum-of-two-numbers-modulo-m/) 是否等于 **X** 。如果发现是真的，存储它的大小。打印获得的所有此类子集的最小尺寸。

***时间复杂度:** O(2 <sup>N</sup> )其中 **N** 是给定数组的长度。*
***辅助空间:** O(N)*

**高效方法:**优化上述方法，思路是基于以下观察使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/):

*   如果 **S % M > X** ，则必须从数组中移除具有和**S % M–X**的元素的最小数量，以使和模 **M** 等于 **X** 。
*   否则，必须移除具有总和**S % M+M–X**的元素的最小数量，以使总和模 **M** 等于 **X** 。

按照以下步骤解决问题:

*   初始化一个 **dp[]** 表、**表【N+1】【X+1】**其中**表【I】【j】**表示要移除的元素的最小数量，其索引在**【0，I】**范围内，使得它们的和为 **j** ，其中 **X** 为要移除的和。
*   为范围**【1，X】**中的每个 **i** 初始化**DP【0】【I】**和一些大值。
*   dp 转换如下:

> **dp[i][j] = min(dp[i-1][j]，dp[i][j-arr[i-1]]+1)**
> 其中， **i** 在范围**【1，N】**内， **j** 在范围**【1，X】**内。

*   打印 **dp[N][X]** 作为要移除的最小元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// elements having sum x
int findSum(vector<int> S, int n, int x)
{

    // Initialize dp table
    vector<vector<int> > table(n + 1,
                               vector<int>(
                                   x + 1, 0));

    for (int i = 1; i <= x; i++) {
        table[0][i] = INT_MAX - 1;
    }

    // Pre-compute subproblems
    for (int i = 1; i <= n; i++) {

        for (int j = 1; j <= x; j++) {

            // If mod is smaller than element
            if (S[i - 1] > j) {
                table[i][j] = table[i - 1][j];
            }
            else {

                // Minimum elements with sum
                // j upto index i
                table[i][j]
                    = min(table[i - 1][j],
                          table[i][j
                                   - S[i - 1]]
                              + 1);
            }
        }
    }

    // Return answer
    return (table[n][x] > n)
               ? -1
               : table[n][x];
}

// Function to find minimum number
// of removals to make sum % M in
// remaining array is equal to X
void minRemovals(vector<int> arr,
                 int n, int m, int x)
{

    // Sum of all elements
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i];
    }

    // Sum to be removed
    int requied_Sum = 0;

    if (sum % m < x)
        requied_Sum
            = m + sum % m - x;
    else
        requied_Sum
            = sum % m - x;

    // Print answer
    cout << findSum(arr, n,
                    requied_Sum);
}

// Driver Code
int main()
{

    // Given array
    vector<int> arr = { 3, 2, 1, 2 };

    // Given size
    int n = arr.size();

    // Given mod and x
    int m = 4, x = 2;

    // Function call
    minRemovals(arr, n, m, x % m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum
// elements having sum x
static int findSum(int[] S, int n, int x)
{

    // Initialize dp table
    int [][]table = new int[n + 1][x + 1];

    for(int i = 1; i <= x; i++)
    {
        table[0][i] = Integer.MAX_VALUE - 1;
    }

    // Pre-compute subproblems
    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= x; j++)
        {

            // If mod is smaller than element
            if (S[i - 1] > j)
            {
                table[i][j] = table[i - 1][j];
            }
            else
            {

                // Minimum elements with sum
                // j upto index i
                table[i][j] = Math.min(table[i - 1][j],
                                       table[i][j - S[i - 1]] + 1);
            }
        }
    }

    // Return answer
    return (table[n][x] > n) ? -1 : table[n][x];
}

// Function to find minimum number
// of removals to make sum % M in
// remaining array is equal to X
static void minRemovals(int[] arr, int n,
                        int m, int x)
{

    // Sum of all elements
    int sum = 0;
    for(int i = 0; i < n; i++)
    {
        sum += arr[i];
    }

    // Sum to be removed
    int requied_Sum = 0;

    if (sum % m < x)
        requied_Sum = m + sum % m - x;
    else
        requied_Sum = sum % m - x;

    // Print answer
    System.out.print(findSum(arr, n,
                             requied_Sum));
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int[] arr = { 3, 2, 1, 2 };

    // Given size
    int n = arr.length;

    // Given mod and x
    int m = 4, x = 2;

    // Function call
    minRemovals(arr, n, m, x % m);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the minimum
# elements having sum x
def findSum(S, n, x):

    # Initialize dp table
    table = [[0 for x in range(x + 1)]
                for y in range(n + 1)]

    for i in range(1, x + 1):
        table[0][i] = sys.maxsize - 1

    # Pre-compute subproblems
    for i in range(1, n + 1):
        for j in range(1, x + 1):

            # If mod is smaller than element
            if (S[i - 1] > j):
                table[i][j] = table[i - 1][j]

            else:

                # Minimum elements with sum
                # j upto index i
                table[i][j] = min(table[i - 1][j],
                                  table[i][j - S[i - 1]] + 1)

    # Return answer
    if (table[n][x] > n):
        return -1

    return table[n][x]

# Function to find minimum number
# of removals to make sum % M in
# remaining array is equal to X
def minRemovals(arr, n, m, x):

    # Sum of all elements
    sum = 0
    for i in range(n):
        sum += arr[i]

    # Sum to be removed
    requied_Sum = 0

    if (sum % m < x):
        requied_Sum = m + sum % m - x
    else:
        requied_Sum = sum % m - x

    # Print answer
    print(findSum(arr, n,
                  requied_Sum))

# Driver Code
if __name__ == "__main__":

    # Given array
    arr = [ 3, 2, 1, 2 ]

    # Given size
    n = len(arr)

    # Given mod and x
    m = 4
    x = 2

    # Function call
    minRemovals(arr, n, m, x % m)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find the minimum
// elements having sum x
static int findSum(int[] S,
                   int n, int x)
{   
  // Initialize dp table
  int [,]table = new int[n + 1,
                         x + 1];

  for(int i = 1; i <= x; i++)
  {
    table[0, i] = int.MaxValue - 1;
  }

  // Pre-compute subproblems
  for(int i = 1; i <= n; i++)
  {
    for(int j = 1; j <= x; j++)
    {

      // If mod is smaller than
      // element
      if (S[i - 1] > j)
      {
        table[i, j] = table[i - 1, j];
      }
      else
      {

        // Minimum elements with sum
        // j upto index i
        table[i, j] = Math.Min(table[i - 1, j],
                              table[i, j -
                              S[i - 1]] + 1);
      }
    }
  }

  // Return answer
  return (table[n, x] > n) ? -1 :
          table[n, x];
}

// Function to find minimum number
// of removals to make sum % M in
// remaining array is equal to X
static void minRemovals(int[] arr, int n,
                        int m, int x)
{   
  // Sum of all elements
  int sum = 0;
  for(int i = 0; i < n; i++)
  {
    sum += arr[i];
  }

  // Sum to be removed
  int requied_Sum = 0;

  if (sum % m < x)
    requied_Sum = m + sum %
                  m - x;
  else
    requied_Sum = sum % m - x;

  // Print answer
  Console.Write(findSum(arr, n,
                        requied_Sum));
}

// Driver Code
public static void Main(String[] args)
{   
  // Given array
  int[] arr = {3, 2, 1, 2};

  // Given size
  int n = arr.Length;

  // Given mod and x
  int m = 4, x = 2;

  // Function call
  minRemovals(arr, n, m, x % m);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the minimum
// elements having sum x
function findSum(S, n, x)
{

    // Initialize dp table
    let table = new Array(n + 1);

    // Loop to create 2D array using 1D array
    for (var i = 0; i < table.length; i++) {
        table[i] = new Array(2);
    }

    for (var i = 0; i < table.length; i++) {
        for (var j = 0; j < table.length; j++) {
        table[i][j] = 0;
    }
    }

    for(let i = 1; i <= x; i++)
    {
        table[0][i] = Number.MAX_VALUE - 1;
    }

    // Pre-compute subproblems
    for(let i = 1; i <= n; i++)
    {
        for(let j = 1; j <= x; j++)
        {

            // If mod is smaller than element
            if (S[i - 1] > j)
            {
                table[i][j] = table[i - 1][j];
            }
            else
            {

                // Minimum elements with sum
                // j upto index i
                table[i][j] = Math.min(table[i - 1][j],
                              table[i][j - S[i - 1]] + 1);
            }
        }
    }

    // Return answer
    return (table[n][x] > n) ? -1 : table[n][x];
}

// Function to find minimum number
// of removals to make sum % M in
// remaining array is equal to X
function minRemovals(arr, n, m, x)
{

    // Sum of all elements
    let sum = 0;
    for(let i = 0; i < n; i++)
    {
        sum += arr[i];
    }

    // Sum to be removed
    let requied_Sum = 0;

    if (sum % m < x)
        requied_Sum = m + sum % m - x;
    else
        requied_Sum = sum % m - x;

    // Print answer
   document.write(findSum(arr, n,
                          requied_Sum));
}

// Driver Code

      // Given array
    let arr = [ 3, 2, 1, 2 ];

    // Given size
    let n = arr.length;

    // Given mod and x
    let m = 4, x = 2;

    // Function call
    minRemovals(arr, n, m, x % m);

</script>
```

**Output**

```
1
```

***时间复杂度:** O(N*X)，其中 N 为给定数组的长度，X 为给定整数。*
***辅助空间:** O(N*X)*