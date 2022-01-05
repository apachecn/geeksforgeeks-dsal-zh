# 从具有至少 K 个相等元素对的两个阵列中选择相等大小的子阵列的方法数量

> 原文:[https://www . geesforgeks . org/从具有至少 k 个相等元素对的两个阵列中选择相等大小的子阵列的方式数/](https://www.geeksforgeeks.org/number-of-ways-to-select-equal-sized-subarrays-from-two-arrays-having-atleast-k-equal-pairs-of-elements/)

给定两个阵列 **A[]** 和 **B[]** ，以及一个整数 **K** ，任务是找到选择两个相同大小的子阵列的方法数量，一个来自 A，另一个来自 B，使得子阵列具有至少 K 个相等的元素对。(即两个选定子阵列中的对(A[i]，B[j])的数量，使得 A[i] = B[j] > = K)。

**示例:**

> **输入:** A[] = {1，2}，B[] = {1，2，3}，K = 1
> **输出:** 4
> 选择两个子阵的方式有:
> 
> 1.  [1], [1]
> 2.  [2], [2]
> 3.  [1, 2], [1, 2]
> 4.  [1, 2], [2, 3]
> 
> **输入:** A[] = {3，2，5，21，15，2，6}，B[] = {2，1，4，3，6，7，9}，K = 2
> **输出:** 7

**进场:**

*   我们不要分别处理这两个数组，而是将它们组合成一个二进制矩阵，这样:

```
mat[i][j] = 0, if A[i] != B[j]
          = 1, if A[i] = B[j]
```

*   现在，如果我们考虑这个矩阵的任何子矩阵，比如大小为 P × Q 的子矩阵，它基本上是来自大小为 P 的 A 的子矩阵和来自大小为 Q 的 B 的子矩阵的组合。由于我们只想检查大小相等的子矩阵，所以我们将只考虑正方形子矩阵。
*   让我们考虑一个正方形子矩阵，左上角为(I，j)，右下角为(i + size，，j + size)。这相当于考虑子阵列 A[i: i +大小]和 B[j: j +大小]。可以观察到，如果这两个子矩阵将有 x 对相等的元素，那么子矩阵将有 x 1。
*   所以遍历矩阵(I，j)的所有元素，并认为它们是正方形的右下角。现在，一种方法是遍历所有可能的子矩阵大小，并找到总和> = k 的大小，但这效率较低。可以观察到，假设一个以(I，j)为右下角的 S×S 子矩阵的和> = k，那么所有以> = S 和(I，j)为右下角的正方形子矩阵都将遵循这个性质。
*   因此，我们将在正方形子矩阵的大小上应用二分搜索法，找到最小的大小 S，使它的和> = K，然后简单地添加边长更大的矩阵，而不是在每个(I，j)迭代所有的大小。
    [这篇](https://www.geeksforgeeks.org/submatrix-sum-queries/)文章可以参考，看看如何使用 2D 前缀和在恒定时间内计算子矩阵和。

下面是上述方法的实现:

## C++

```
// C++ implementation to count the
// number of ways to select equal
// sized subarrays such that they
// have atleast K common elements

#include <bits/stdc++.h>

using namespace std;

// 2D prefix sum for submatrix
// sum query for matrix
int prefix_2D[2005][2005];

// Function to find the prefix sum
// of the matrix from i and j
int subMatrixSum(int i, int j, int len)
{
    return prefix_2D[i][j] -
           prefix_2D[i][j - len] -
           prefix_2D[i - len][j] +
           prefix_2D[i - len][j - len];
}

// Function to count the number of ways
// to select equal sized subarrays such
// that they have atleast K common elements
int numberOfWays(int a[], int b[], int n,
                            int m, int k)
{

    // Combining the two arrays
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            if (a[i - 1] == b[j - 1])
                prefix_2D[i][j] = 1;

            else
                prefix_2D[i][j] = 0;
        }
    }

    // Calculating the 2D prefix sum
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            prefix_2D[i][j] += prefix_2D[i][j - 1];
        }
    }

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            prefix_2D[i][j] += prefix_2D[i - 1][j];
        }
    }

    int answer = 0;

    // iterating through all
    // the elements of matrix
    // and considering them to
    // be the bottom right
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {

            // applying binary search
            // over side length
            int low = 1;
            int high = min(i, j);

            while (low < high) {
                int mid = (low + high) >> 1;

                // if sum of this submatrix >=k then
                // new search space will be [low, mid]
                if (subMatrixSum(i, j, mid) >= k) {
                    high = mid;
                }
                // else new search space
                // will be [mid+1, high]
                else {
                    low = mid + 1;
                }
            }

            // Adding the total submatrices
            if (subMatrixSum(i, j, low) >= k) {
                answer += (min(i, j) - low + 1);
            }
        }
    }
    return answer;
}

// Driver Code
int main()
{
    int N = 2, M = 3;
    int A[N] = { 1, 2 };
    int B[M] = { 1, 2, 3 };

    int K = 1;

    cout << numberOfWays(A, B, N, M, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// number of ways to select equal
// sized subarrays such that they
// have atleast K common elements
class GFG{

// 2D prefix sum for submatrix
// sum query for matrix
static int [][]prefix_2D = new int[2005][2005];

// Function to find the prefix sum
// of the matrix from i and j
static int subMatrixSum(int i, int j, int len)
{
    return prefix_2D[i][j] -
           prefix_2D[i][j - len] -
           prefix_2D[i - len][j] +
           prefix_2D[i - len][j - len];
}

// Function to count the number of ways
// to select equal sized subarrays such
// that they have atleast K common elements
static int numberOfWays(int a[], int b[], int n,
                        int m, int k)
{

    // Combining the two arrays
    for(int i = 1; i <= n; i++)
    {
       for(int j = 1; j <= m; j++)
       {
          if (a[i - 1] == b[j - 1])
              prefix_2D[i][j] = 1;
          else
              prefix_2D[i][j] = 0;
       }
    }

    // Calculating the 2D prefix sum
    for(int i = 1; i <= n; i++)
    {
       for(int j = 1; j <= m; j++)
       {
          prefix_2D[i][j] += prefix_2D[i][j - 1];
       }
    }

    for(int i = 1; i <= n; i++)
    {
       for(int j = 1; j <= m; j++)
       {
          prefix_2D[i][j] += prefix_2D[i - 1][j];
       }
    }

    int answer = 0;

    // Iterating through all
    // the elements of matrix
    // and considering them to
    // be the bottom right
    for(int i = 1; i <= n; i++)
    {
       for(int j = 1; j <= m; j++)
       {

          // Applying binary search
          // over side length
          int low = 1;
          int high = Math.min(i, j);

          while (low < high)
          {
              int mid = (low + high) >> 1;

              // If sum of this submatrix >=k then
              // new search space will be [low, mid]
              if (subMatrixSum(i, j, mid) >= k)
              {
                  high = mid;
              }

              // Else new search space
              // will be [mid+1, high]
              else
              {
                  low = mid + 1;
              }
          }

          // Adding the total submatrices
          if (subMatrixSum(i, j, low) >= k)
          {
              answer += (Math.min(i, j) - low + 1);
          }
       }
    }
    return answer;
}

// Driver Code
public static void main(String[] args)
{
    int N = 2, M = 3;
    int A[] = { 1, 2 };
    int B[] = { 1, 2, 3 };

    int K = 1;

    System.out.print(numberOfWays(A, B, N, M, K));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to count the
# number of ways to select equal
# sized subarrays such that they
# have atleast K common element

# 2D prefix sum for submatrix
# sum query for matrix
prefix_2D = [[0 for x in range (2005)]
                for y in range (2005)]

# Function to find the prefix sum
# of the matrix from i and j
def subMatrixSum(i, j, length):

    return (prefix_2D[i][j] -
            prefix_2D[i][j - length] -
            prefix_2D[i - length][j] +
            prefix_2D[i - length][j - length])

# Function to count the number of ways
# to select equal sized subarrays such
# that they have atleast K common elements
def numberOfWays(a, b, n, m, k):

    # Combining the two arrays
    for i in range (1, n + 1):
        for j in range (1, m + 1):
            if (a[i - 1] == b[j - 1]):
                prefix_2D[i][j] = 1
            else:
                prefix_2D[i][j] = 0

    # Calculating the 2D prefix sum
    for i in range (1, n + 1):
        for j in range (1, m + 1):
            prefix_2D[i][j] += prefix_2D[i][j - 1]

    for i in range (1, n + 1):
        for j in range (1, m + 1):
            prefix_2D[i][j] += prefix_2D[i - 1][j]
    answer = 0

    # iterating through all
    # the elements of matrix
    # and considering them to
    # be the bottom right
    for i in range (1, n +1):
        for j in range (1, m + 1):

            # applying binary search
            # over side length
            low = 1
            high = min(i, j)

            while (low < high):
                mid = (low + high) >> 1

                # if sum of this submatrix >=k then
                # new search space will be [low, mid]
                if (subMatrixSum(i, j, mid) >= k):
                    high = mid

                # else new search space
                # will be [mid+1, high]
                else:
                    low = mid + 1

            # Adding the total submatrices
            if (subMatrixSum(i, j, low) >= k):
                answer += (min(i, j) - low + 1)

    return answer

# Driver Code
if __name__ == "__main__":

    N = 2
    M = 3
    A = [1, 2]
    B = [1, 2, 3]
    K = 1
    print (numberOfWays(A, B, N, M, K))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation to count the
// number of ways to select equal
// sized subarrays such that they
// have atleast K common elements
using System;

class GFG{

// 2D prefix sum for submatrix
// sum query for matrix
static int [,]prefix_2D = new int[2005, 2005];

// Function to find the prefix sum
// of the matrix from i and j
static int subMatrixSum(int i, int j, int len)
{
    return prefix_2D[i, j] -
           prefix_2D[i, j - len] -
           prefix_2D[i - len, j] +
           prefix_2D[i - len, j - len];
}

// Function to count the number of ways
// to select equal sized subarrays such
// that they have atleast K common elements
static int numberOfWays(int []a, int []b, int n,
                        int m, int k)
{

    // Combining the two arrays
    for(int i = 1; i <= n; i++)
    {
       for(int j = 1; j <= m; j++)
       {
          if (a[i - 1] == b[j - 1])
              prefix_2D[i, j] = 1;
          else
              prefix_2D[i, j] = 0;
       }
    }

    // Calculating the 2D prefix sum
    for(int i = 1; i <= n; i++)
    {
       for(int j = 1; j <= m; j++)
       {
          prefix_2D[i, j] += prefix_2D[i, j - 1];

       }
    }

    for(int i = 1; i <= n; i++)
    {
       for(int j = 1; j <= m; j++)
       {
          prefix_2D[i, j] += prefix_2D[i - 1, j];
       }
    }

    int answer = 0;

    // Iterating through all
    // the elements of matrix
    // and considering them to
    // be the bottom right
    for(int i = 1; i <= n; i++)
    {
       for(int j = 1; j <= m; j++)
       {

          // Applying binary search
          // over side length
          int low = 1;
          int high = Math.Min(i, j);
          while (low < high)
          {
              int mid = (low + high) >> 1;

              // If sum of this submatrix >=k then
              // new search space will be [low, mid]
              if (subMatrixSum(i, j, mid) >= k)
              {
                  high = mid;
              }

              // Else new search space
              // will be [mid+1, high]
              else
              {
                  low = mid + 1;
              }
          }

          // Adding the total submatrices
          if (subMatrixSum(i, j, low) >= k)
          {
              answer += (Math.Min(i, j) - low + 1);
          }
       }
    }
    return answer;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 2, M = 3;
    int []A = { 1, 2 };
    int []B = { 1, 2, 3 };

    int K = 1;

    Console.Write(numberOfWays(A, B, N, M, K));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// javascript implementation to count the
// number of ways to select equal
// sized subarrays such that they
// have atleast K common elements   
// 2D prefix sum for submatrix
    // sum query for matrix
    var prefix_2D = Array(2005);

    // Function to find the prefix sum
    // of the matrix from i and j
    function subMatrixSum(i , j , len) {
        return prefix_2D[i][j] - prefix_2D[i][j - len] - prefix_2D[i - len][j] + prefix_2D[i - len][j - len];
    }

    // Function to count the number of ways
    // to select equal sized subarrays such
    // that they have atleast K common elements
    function numberOfWays(a , b , n , m , k) {

        // Combining the two arrays
        for (i = 1; i <= n; i++) {
            for (j = 1; j <= m; j++) {
                if (a[i - 1] == b[j - 1])
                    prefix_2D[i][j] = 1;
                else
                    prefix_2D[i][j] = 0;
            }
        }

        // Calculating the 2D prefix sum
        for (i = 1; i <= n; i++) {
            for (j = 1; j <= m; j++) {
                prefix_2D[i][j] += prefix_2D[i][j - 1];
            }
        }

        for (i = 1; i <= n; i++) {
            for (j = 1; j <= m; j++) {
                prefix_2D[i][j] += prefix_2D[i - 1][j];
            }
        }

        var answer = 0;

        // Iterating through all
        // the elements of matrix
        // and considering them to
        // be the bottom right
        for (i = 1; i <= n; i++) {
            for (j = 1; j <= m; j++) {

                // Applying binary search
                // over side length
                var low = 1;
                var high = Math.min(i, j);

                while (low < high) {
                    var mid = (low + high) >> 1;

                    // If sum of this submatrix >=k then
                    // new search space will be [low, mid]
                    if (subMatrixSum(i, j, mid) >= k) {
                        high = mid;
                    }

                    // Else new search space
                    // will be [mid+1, high]
                    else {
                        low = mid + 1;
                    }
                }

                // Adding the total submatrices
                if (subMatrixSum(i, j, low) >= k) {
                    answer += (Math.min(i, j) - low + 1);
                }
            }
        }
        return answer;
    }

    // Driver Code

        var N = 2, M = 3;
        var A = [ 1, 2 ];
        var B = [ 1, 2, 3 ];
        for(i = 0;i<205;i++)
        prefix_2D[i] = Array(205).fill(0);
        var K = 1;

        document.write(numberOfWays(A, B, N, M, K));

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
4
```

**时间复杂度:** *O(N * M * log(max(N，M)))*