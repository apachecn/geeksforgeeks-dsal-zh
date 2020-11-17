# 不相邻的数组元素的不超过`K`的最大可能总和

> 原文：[https://www.geeksforgeeks.org/maximum-possible-sum-of-non-adjacent-array-elements-not-exceeding-k/](https://www.geeksforgeeks.org/maximum-possible-sum-of-non-adjacent-array-elements-not-exceeding-k/)

给定[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)`arr[]`，该数组由`N`个整数和一个整数`K`组成，任务是选择一些**总和最大不超过`K`的相邻数组元素**。

**示例**：

> **输入**：`arr[] = {50, 10, 20, 30, 40}, K = 100`
>
> **输出**：90
>
> **说明**：要使不超过`K = 100`的总和最大化，请选择元素 50 和 40。
>
> 因此，最大可能的总和为 90。
> 
> **输入**：`arr[] = {20, 10, 17, 12, 8, 9}, K = 64`
>
> **输出**：46
>
> **说明**：
>
> 为使不超过`K = 64`的总和最大化，请选择元素 20、17 和 9。
>
> 因此，最大可能的总和为 46。

**朴素的方法**：最简单的方法是[递归](https://www.geeksforgeeks.org/recursion/)[生成给定数组的所有可能子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)，对于每个子集，检查是否不包含相邻元素并且和不超过`K`。 在满足上述条件的所有子集中，打印出任何子集获得的最大和。

下面是上述方法的实现：

## Java

```java

// Java program for the above approach

import java.io.*;

class GFG {

    // Function to find the maximum sum
    // not exceeding K possible by selecting
    // a subset of non-adjacent elements
    public static int maxSum(
        int a[], int n, int k)
    {
        // Base Case
        if (n <= 0)
            return 0;

        // Not selecting current element
        int option = maxSum(a, n - 1, k);

        // If selecting current element
        // is possible
        if (k >= a[n - 1])
            option = Math.max(
                option,
                a[n - 1]
                    + maxSum(a, n - 2,
                             k - a[n - 1]));

        // Return answer
        return option;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array arr[]
        int arr[] = { 50, 10, 20, 30, 40 };

        int N = arr.length;

        // Given K
        int K = 100;

        // Function Call
        System.out.println(maxSum(arr, N, K));
    }
}

```

## Python3

```py

# Python3 program for the above approach

# Function to find the maximum sum
# not exceeding K possible by selecting
# a subset of non-adjacent elements
def maxSum(a, n, k):

    # Base Case
    if (n <= 0):
        return 0

    # Not selecting current element
    option = maxSum(a, n - 1, k)

    # If selecting current element
    # is possible
    if (k >= a[n - 1]):
        option = max(option, a[n - 1] +
        maxSum(a, n - 2, k - a[n - 1]))

    # Return answer
    return option

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 50, 10, 20, 30, 40 ]

    N = len(arr)

    # Given K
    K = 100

    # Function Call
    print(maxSum(arr, N, K))

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program for the 
// above approach
using System;
class GFG{

// Function to find the maximum
// sum not exceeding K possible 
// by selecting a subset of 
// non-adjacent elements
public static int maxSum(int []a, 
                         int n, int k)
{
  // Base Case
  if (n <= 0)
    return 0;

  // Not selecting current element
  int option = maxSum(a, n - 1, k);

  // If selecting current 
  // element is possible
  if (k >= a[n - 1])
    option = Math.Max(option, a[n - 1] + 
                      maxSum(a, n - 2, 
                             k - a[n - 1]));

  // Return answer
  return option;
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int []arr = {50, 10, 20, 30, 40};

  int N = arr.Length;

  // Given K
  int K = 100;

  // Function Call
  Console.WriteLine(maxSum(arr, N, K));
}
}

// This code is contributed by Rajput-Ji

```

**输出**： 

```
90

```

**时间复杂度**：`O（2 ^ N)`。

**辅助空间**：`O(n)`。

**有效方法**：为了优化上述方法，其想法是使用[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)。 每个数组元素都有两个可能的选项：

1.  仅当当前元素小于或等于`K`时，才选择它。

1.  否则跳过当前元素，然后继续下一个元素。

请按照以下步骤解决问题：

1.  使用`-1`初始化数组`dp[N][K + 1]`，其中`dp[i][j]`将存储使用直到索引`i`的元素求和`j`的最大和。

2.  从上面的转换中，找到当前元素的最大和，如果不选择，则递归。

3.  存储当前状态的最小答案。

4.  此外，添加一个基本条件，即如果已经访问了当前状态`(i, j)`，即`dp[i][j] != -1`返回`dp[i][j]`。

5.  将`dp[N][K]`打印为最大可能和。

下面是上述方法的实现：

## Java

```java

// Java program for the above approach

import java.util.*;

class GFG {

    // Function find the maximum sum that
    // doesn't exceeds K by choosing elements
    public static int maxSum(int a[], int n,
                             int k, int[][] dp)
    {
        // Base Case
        if (n <= 0)
            return 0;

        // Return the memoized state
        if (dp[n][k] != -1)
            return dp[n][k];

        // Dont pick the current element
        int option = maxSum(a, n - 1,
                            k, dp);

        // Pick the current element
        if (k >= a[n - 1])
            option = Math.max(
                option,
                a[n - 1]
                    + maxSum(a, n - 2,
                             k - a[n - 1],
                             dp));

        // Return and store the result
        return dp[n][k] = option;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 50, 10, 20, 30, 40 };

        int N = arr.length;

        int K = 100;

        // Initialize dp
        int dp[][] = new int[N + 1][K + 1];

        for (int i[] : dp) {
            Arrays.fill(i, -1);
        }
        // Print answer
        System.out.println(maxSum(arr, N, K, dp));
    }
}

```

**输出**： 

```
90

```

**时间复杂度**：`O(N * K)`，其中`N`是给定数组的大小，`K`是极限。

**辅助空间**：`O(n)`。



* * *

* * *



