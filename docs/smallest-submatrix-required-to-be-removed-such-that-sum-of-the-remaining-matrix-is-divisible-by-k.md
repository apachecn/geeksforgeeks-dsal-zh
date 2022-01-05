# 需要移除的最小子矩阵，使得剩余矩阵的和可被 K 整除

> 原文:[https://www . geesforgeks . org/minist-submatrix-需要移除-这样剩余矩阵的和才能被 k 整除/](https://www.geeksforgeeks.org/smallest-submatrix-required-to-be-removed-such-that-sum-of-the-remaining-matrix-is-divisible-by-k/)

给定一个大小为 **N * M** 的 [2D 矩阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**mat【】【】**和一个正整数 **K** ，任务是找到需要移除的最小矩形子矩阵的面积，使得矩阵中剩余元素的和可被 **K** 整除。

**示例:**

> **输入:** mat[][] = { {6，2，6}，{3，2，8}，{2，5，3} }，K = 3
> **输出:** 2
> **解释:**
> 从给定矩阵中移除子矩阵{ mat[1][1]，mat[2][1] }。
> 因为剩余矩阵的和等于 30，可以被 K(=3)整除。因此，所需的输出为 1 * 2 = 2。
> 
> **输入:** mat[][] = { {16，2，6，13}，{33，21，8，8}，{31，5，3，11} }，K = 15
> **输出:** 3

**方法:**按照下面给出的步骤解决问题:

*   初始化一个变量，比如 **S** 来存储给定矩阵所有元素的和。
*   初始化一个变量，比如说 **min_area** 来存储需要移除的最小区域，这样剩余矩阵元素的总和就可以被 **K** 整除。
*   初始化两个变量，说**左**和**右**分别存储每个子矩阵的**最左边一列**和**最右边一列**。
*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如说**前缀行总和【N】**，其中**前缀行总和【I】**存储子矩阵的所有元素的和，子矩阵的最左边的元素是 **(0，左)**，最右边的元素是 **(i，右)**超过了**左**和**右**的所有可能值。
*   迭代**左**和**右**的所有可能值，找到需要删除的最小子阵列的[长度，使 PrefixRowSum[]剩余元素之和等于(S % K)](https://www.geeksforgeeks.org/length-of-smallest-subarray-to-be-removed-to-make-sum-of-remaining-elements-divisible-by-k/) 并更新 **min_area**
*   最后，打印 **min_area** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the length of the
// smallest subarray to be removed such
// that sum of elements is equal to S % K
int removeSmallestSubarray(int arr[], int S,
                              int n, int k)
{

    // Remainder when total_sum
    // is divided by K
    int target_remainder
        = S % k;

    // Stores curr_remainder and the
    // most recent index at which
    // curr_remainder has occured
    unordered_map<int, int> map1;
    map1[0] = -1;

    int curr_remainder = 0;

    // Stores required answer
    int res = INT_MAX;

    for (int i = 0; i < n; i++) {

        // Add current element to
        // curr_sum and take mod
        curr_remainder = (curr_remainder
                          + arr[i] + k)
                         % k;

        // Update current
        // remainder index
        map1[curr_remainder] = i;

        int mod
            = (curr_remainder
               - target_remainder
               + k)
              % k;

        // If mod already exists in map
        // the subarray exists
        if (map1.find(mod) !=
                        map1.end()) {

            // Update res
            res = min(res, i - map1[mod]);
        }
    }

    // If not possible
    if (res == INT_MAX || res == n) {
        res = -1;
    }

    // Return the result
    return res;
}

// Function to find the smallest submatrix
// rqured to be deleted to make the sum
// of the matrix divisible by K
int smstSubmatDeleted(vector<vector<int> > &mat,
                        int N, int M, int K)
{

    // Stores the sum of
    // element of the matrix
    int S = 0;

    // Traverse the matrix mat[][]
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++)

        // Update S
        S += mat[i][j];
    }

    // Stores smallest area need to be
    // deleted to get sum divisible by K
    int min_area = N * M;

    // Stores leftmost column
    // of each matrix
    int left = 0;

    // Stores rightmost column
    // of each matrix
    int right = 0;

    // Stores number of coulmns
    // deleted of a matrix
    int width;

    // Store area of the deleted matrix
    int area;

    // prefixRowSum[i]: Store sum of sub matrix
    // whose topmost left and bottommost right
    // position is (0, left) (i, right)
    int prefixRowSum[N];

    // Iterate over all possible values
    // of (left, right)
    for (left = 0; left < M; left++) {

        // Initialize all possible values
        // of prefixRowSum[] to 0
        memset(prefixRowSum, 0,
                   sizeof(prefixRowSum));

        for (right = left; right < M; right++) {

            // Traverse each row from
            // left to right column
            for (int i = 0; i < N; i++) {

                // Update row_sum[i];
                prefixRowSum[i]
                      += mat[i][right];

            }

            // Update width
            width = removeSmallestSubarray(
                     prefixRowSum, S, N, K);

            // If no submatrix of the length
            // (right  - left + 1) found to get
            // the required output
            if (width != -1) {

                // Update area
                area = (right - left + 1)
                                  * (width);

                // If area is less than min_area
                if (area < min_area) {

                    // Update min_area
                    min_area = area;
                }
            }
        }
    }
    return min_area;

}

// Driver Code  
int main()
{

    vector<vector<int> > mat
                        = { { 6, 2, 6 },
                            { 3, 2, 8 },
                            { 2, 5, 3 } };

    int K = 3;

    // Stores number of rows
    // in the matrix
    int N = mat.size();

    // Stores number of column
    // in the matrix
    int M = mat[0].size();

    cout<< smstSubmatDeleted(mat, N, M, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the length of the
// smallest subarray to be removed such
// that sum of elements is equal to S % K
static int removeSmallestSubarray(int arr[], int S,
                                  int n, int k)
{   
  // Remainder when total_sum
  // is divided by K
  int target_remainder = S % k;

  // Stores curr_remainder and the
  // most recent index at which
  // curr_remainder has occured
  HashMap<Integer,
          Integer> map1 =
          new HashMap<>();

  map1.put(0, -1);
  int curr_remainder = 0;

  // Stores required answer
  int res = Integer.MAX_VALUE;

  for (int i = 0; i < n; i++)
  {
    // Add current element to
    // curr_sum and take mod
    curr_remainder = (curr_remainder +
                      arr[i] + k) % k;

    // Update current
    // remainder index
    map1.put(curr_remainder, i);

    int mod = (curr_remainder -
               target_remainder +
               k) % k;

    // If mod already exists in map
    // the subarray exists
    if (map1.containsKey(mod))
    {
      // Update res
      res = Math.min(res, i -
                     map1.get(mod));
    }
  }

  // If not possible
  if (res == Integer.MAX_VALUE ||
      res == n)
  {
    res = -1;
  }

  // Return the result
  return res;
}

// Function to find the smallest submatrix
// rqured to be deleted to make the sum
// of the matrix divisible by K
static int smstSubmatDeleted(int[][]mat,
                             int N, int M,
                             int K)
{
  // Stores the sum of
  // element of the matrix
  int S = 0;

  // Traverse the matrix mat[][]
  for (int i = 0; i < N; i++)
  {
    for (int j = 0; j < M; j++)

      // Update S
      S += mat[i][j];
  }

  // Stores smallest area need
  // to be deleted to get sum
  // divisible by K
  int min_area = N * M;

  // Stores leftmost column
  // of each matrix
  int left = 0;

  // Stores rightmost column
  // of each matrix
  int right = 0;

  // Stores number of coulmns
  // deleted of a matrix
  int width;

  // Store area of the deleted
  // matrix
  int area;

  // prefixRowSum[i]: Store sum
  // of sub matrix whose topmost
  // left and bottommost right
  // position is (0, left) (i, right)
  int []prefixRowSum = new int[N];

  // Iterate over all possible
  // values of (left, right)
  for (left = 0; left < M; left++)
  {
    // Initialize all possible
    // values of prefixRowSum[]
    // to 0
    Arrays.fill(prefixRowSum, 0);

    for (right = left;
         right < M; right++)
    {
      // Traverse each row from
      // left to right column
      for (int i = 0; i < N; i++)
      {
        // Update row_sum[i];
        prefixRowSum[i] +=
        mat[i][right];
      }

      // Update width
      width = removeSmallestSubarray(
              prefixRowSum, S, N, K);

      // If no submatrix of the
      // length (right  - left + 1)
      // found to get the required
      // output
      if (width != -1)
      {
        // Update area
        area = (right - left + 1) *
               (width);

        // If area is less than
        // min_area
        if (area < min_area)
        {
          // Update min_area
          min_area = area;
        }
      }
    }
  }
  return min_area;
}

// Driver Code  
public static void main(String[] args)
{
  int[][] mat = {{6, 2, 6},
                 {3, 2, 8},
                 {2, 5, 3}};

  int K = 3;

  // Stores number of rows
  // in the matrix
  int N = mat.length;

  // Stores number of column
  // in the matrix
  int M = mat[0].length;

  System.out.print(
  smstSubmatDeleted(mat, N,
                    M, K));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import sys

# Function to find the length of the
# smallest subarray to be removed such
# that sum of elements is equal to S % K
def removeSmallestSubarray(arr, S, n, k):

    # Remainder when total_sum
    # is divided by K
    target_remainder = S % k

    # Stores curr_remainder and the
    # most recent index at which
    # curr_remainder has occured
    map1 = {}
    map1[0] = -1

    curr_remainder = 0

    # Stores required answer
    res = sys.maxsize

    for i in range(n):

        # Add current element to
        # curr_sum and take mod
        curr_remainder = (curr_remainder +
                          arr[i] + k) % k

        # Update current
        # remainder index
        map1[curr_remainder] = i

        mod = (curr_remainder -
             target_remainder + k) % k

        # If mod already exists in map
        # the subarray exists
        if (mod in map1):

            # Update res
            res = min(res, i - map1[mod])

    # If not possible
    if (res == sys.maxsize or res == n):
        res = -1

    # Return the result
    return res

# Function to find the smallest submatrix
# rqured to be deleted to make the sum
# of the matrix divisible by K
def smstSubmatDeleted(mat, N, M, K):

    # Stores the sum of
    # element of the matrix
    S = 0

    # Traverse the matrix mat[][]
    for i in range(N):
        for j in range(M):

        # Update S
            S += mat[i][j]

    # Stores smallest area need to be
    # deleted to get sum divisible by K
    min_area = N * M

    # Stores leftmost column
    # of each matrix
    left = 0

    # Stores rightmost column
    # of each matrix
    right = 0

    # Stores number of coulmns
    # deleted of a matrix
    width = 0

    # Store area of the deleted matrix
    area = 0

    # prefixRowSum[i]: Store sum of sub matrix
    # whose topmost left and bottommost right
    # position is (0, left) (i, right)
    prefixRowSm = [0] * N

    # Iterate over all possible values
    # of (left, right)
    for left in range(M):

        # Initialize all possible values
        # of prefixRowSum[] to 0
        prefixRowSum = [0] * N

        for right in range(left, M):

            # Traverse each row from
            # left to right column
            for i in range(N):

                # Update row_sum[i]
                prefixRowSum[i] += mat[i][right]

            # Update width
            width = removeSmallestSubarray(
                prefixRowSum, S, N, K)

            # If no submatrix of the length
            # (right  - left + 1) found to get
            # the required output
            if (width != -1):

                # Update area
                area = (right - left + 1) * (width)

                # If area is less than min_area
                if (area < min_area):

                    # Update min_area
                    min_area = area

    return min_area

# Driver Code
if __name__ == '__main__':

    mat = [ [ 6, 2, 6 ],
            [ 3, 2, 8 ],
            [ 2, 5, 3 ] ]

    K = 3

    # Stores number of rows
    # in the matrix
    N = len(mat)

    # Stores number of column
    # in the matrix
    M = len(mat[0])

    print(smstSubmatDeleted(mat, N, M, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the length of the
// smallest subarray to be removed such
// that sum of elements is equal to S % K
static int removeSmallestSubarray(int []arr, int S,
                                  int n, int k)
{

  // Remainder when total_sum
  // is divided by K
  int target_remainder = S % k;

  // Stores curr_remainder and the
  // most recent index at which
  // curr_remainder has occured
  Dictionary<int,
             int> map1 = new Dictionary<int,
                                        int>();

  map1.Add(0, -1);
  int curr_remainder = 0;

  // Stores required answer
  int res = int.MaxValue;

  for(int i = 0; i < n; i++)
  {

    // Add current element to
    // curr_sum and take mod
    curr_remainder = (curr_remainder +
                      arr[i] + k) % k;

    // Update current
    // remainder index
    map1[curr_remainder]=  i;

    int mod = (curr_remainder -
               target_remainder +
               k) % k;

    // If mod already exists in map
    // the subarray exists
    if (map1.ContainsKey(mod))
    {

      // Update res
      res = Math.Min(res, i -
                     map1[mod]);
    }
  }

  // If not possible
  if (res == int.MaxValue ||
      res == n)
  {
    res = -1;
  }

  // Return the result
  return res;
}

// Function to find the smallest submatrix
// rqured to be deleted to make the sum
// of the matrix divisible by K
static int smstSubmatDeleted(int[,]mat,
                             int N, int M,
                             int K)
{

  // Stores the sum of
  // element of the matrix
  int S = 0;

  // Traverse the matrix [,]mat
  for(int i = 0; i < N; i++)
  {
    for(int j = 0; j < M; j++)

      // Update S
      S += mat[i,j];
  }

  // Stores smallest area need
  // to be deleted to get sum
  // divisible by K
  int min_area = N * M;

  // Stores leftmost column
  // of each matrix
  int left = 0;

  // Stores rightmost column
  // of each matrix
  int right = 0;

  // Stores number of coulmns
  // deleted of a matrix
  int width;

  // Store area of the deleted
  // matrix
  int area;

  // prefixRowSum[i]: Store sum
  // of sub matrix whose topmost
  // left and bottommost right
  // position is (0, left) (i, right)
  int []prefixRowSum = new int[N];

  // Iterate over all possible
  // values of (left, right)
  for(left = 0; left < M; left++)
  {

    // Initialize all possible
    // values of prefixRowSum[]
    // to 0
    for(int i = 0; i < prefixRowSum.Length; i++)
      prefixRowSum[i] = 0;

    for(right = left;
        right < M; right++)
    {

      // Traverse each row from
      // left to right column
      for(int i = 0; i < N; i++)
      {

        // Update row_sum[i];
        prefixRowSum[i] += mat[i, right];
      }

      // Update width
      width = removeSmallestSubarray(
              prefixRowSum, S, N, K);

      // If no submatrix of the
      // length (right  - left + 1)
      // found to get the required
      // output
      if (width != -1)
      {

        // Update area
        area = (right - left + 1) *
               (width);

        // If area is less than
        // min_area
        if (area < min_area)
        {

          // Update min_area
          min_area = area;
        }
      }
    }
  }
  return min_area;
}

// Driver Code  
public static void Main(String[] args)
{
  int[,] mat = { { 6, 2, 6 },
                 { 3, 2, 8 },
                 { 2, 5, 3 } };

  int K = 3;

  // Stores number of rows
  // in the matrix
  int N = mat.GetLength(0);

  // Stores number of column
  // in the matrix
  int M = mat.GetLength(1);
  Console.Write(
  smstSubmatDeleted(mat, N,
                    M, K));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the length of the
// smallest subarray to be removed such
// that sum of elements is equal to S % K
function removeSmallestSubarray(arr, S, n, k)
{

    // Remainder when total_sum
    // is divided by K
    var target_remainder
        = S % k;

    // Stores curr_remainder and the
    // most recent index at which
    // curr_remainder has occured
    var map1 = new Map();
    map1.set(0, -1);

    var curr_remainder = 0;

    // Stores required answer
    var res = 1000000000;

    for (var i = 0; i < n; i++) {

        // Add current element to
        // curr_sum and take mod
        curr_remainder = (curr_remainder
                          + arr[i] + k)
                         % k;

        // Update current
        // remainder index
        map1.set(curr_remainder, i);

        var mod
            = (curr_remainder
               - target_remainder
               + k)
              % k;

        // If mod already exists in map
        // the subarray exists
        if (map1.has(mod)) {

            // Update res
            res = Math.min(res, i - map1.get(mod));
        }
    }

    // If not possible
    if (res == 1000000000 || res == n) {
        res = -1;
    }

    // Return the result
    return res;
}

// Function to find the smallest submatrix
// rqured to be deleted to make the sum
// of the matrix divisible by K
function smstSubmatDeleted(mat, N, M, K)
{

    // Stores the sum of
    // element of the matrix
    var S = 0;

    // Traverse the matrix mat[][]
    for (var i = 0; i < N; i++) {
        for (var j = 0; j < M; j++)

        // Update S
        S += mat[i][j];
    }

    // Stores smallest area need to be
    // deleted to get sum divisible by K
    var min_area = N * M;

    // Stores leftmost column
    // of each matrix
    var left = 0;

    // Stores rightmost column
    // of each matrix
    var right = 0;

    // Stores number of coulmns
    // deleted of a matrix
    var width;

    // Store area of the deleted matrix
    var area;

    // prefixRowSum[i]: Store sum of sub matrix
    // whose topmost left and bottommost right
    // position is (0, left) (i, right)
    var prefixRowSum = Array(N);

    // Iterate over all possible values
    // of (left, right)
    for (left = 0; left < M; left++) {

        // Initialize all possible values
        // of prefixRowSum[] to 0
        prefixRowSum = Array(N).fill(0);

        for (right = left; right < M; right++) {

            // Traverse each row from
            // left to right column
            for (var i = 0; i < N; i++) {

                // Update row_sum[i];
                prefixRowSum[i]
                      += mat[i][right];

            }

            // Update width
            width = removeSmallestSubarray(
                     prefixRowSum, S, N, K);

            // If no submatrix of the length
            // (right  - left + 1) found to get
            // the required output
            if (width != -1) {

                // Update area
                area = (right - left + 1)
                                  * (width);

                // If area is less than min_area
                if (area < min_area) {

                    // Update min_area
                    min_area = area;
                }
            }
        }
    }
    return min_area;

}

// Driver Code  
var mat  = [ [ 6, 2, 6 ],
             [ 3, 2, 8 ],
             [ 2, 5, 3 ] ];

var K = 3;

// Stores number of rows
// in the matrix
var N = mat.length;

// Stores number of column
// in the matrix
var M = mat[0].length;

document.write( smstSubmatDeleted(mat, N, M, K));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(M<sup>2</sup>* N)*
***辅助空间:** O(N)*