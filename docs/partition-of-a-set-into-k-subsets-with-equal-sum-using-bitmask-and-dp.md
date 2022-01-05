# 使用位掩码和 DP 将一个集合划分为等和的 K 个子集

> 原文:[https://www . geeksforgeeks . org/使用位掩码和-dp 将集合划分为 k 个等份子集/](https://www.geeksforgeeks.org/partition-of-a-set-into-k-subsets-with-equal-sum-using-bitmask-and-dp/)

给定一个由 **N** 个整数组成的整数数组 **arr[]** ，任务是检查是否有可能将给定的数组分成相等和的 **K** 个非空子集，使得每个数组元素都是单个子集的一部分。
**举例:**

> **输入:** arr[] = {2，1，4，5，6}，K = 3
> **输出:**是
> **解释:**
> 给定数组的可能子集是{2，4}、(1，5}和{6}
> **输入:** arr[] = {2，1，5，5，6}，K = 3
> **输出:**否

对于递归方法，参考[将一个集合划分为具有相等和的 K 个子集](https://www.geeksforgeeks.org/partition-set-k-subsets-equal-sum/)。
**进场:**
按照以下步骤解决问题:

*   想法是用**屏蔽**确定当前状态。当前状态将告诉我们已经形成的子集(已经选择了哪些数字)。
    **例如:** arr[] = [2，1，4，3，5，6，2]，**遮罩** = (1100101)，这意味着当前遮罩中已经选择了{ 2，1，5，2 }。
*   对于任何当前状态**遮罩**，将基于以下两个条件向其添加 **j <sup>第</sup>T5】元素:** 

> 1.  **Bit [T2】 T5] of J <sup>is not set in the mask ( **Mask & (1 < < J) = = 0** )</sup>**
> 2.  [T0】 Sum (mask)+arr [j] < = target (where target = (sum of array elements)/K)

*   维护一个表 **dp[]** ，这样 **dp[i]** 会存储蒙版 **i** 中元素的总和。因此，差压转换将为:

> DP[I |(1)<< j)] = (dp[i] + arr[j]) % target 
> **图解:**
> arr [ ] = [4，3，2，3，5，2，1]，K = 4，tar = 5
> DP[“1100101”]暗示选择了{ 4，3，5，1 }
> 因此，Sum = 4 + 3 + 5 + 1 = 13，13 % 5 = 3。
> 因此，DP[“1100101”]= 3
> 如果 DP[“11111…1111”]= = 0，那么这意味着我们可以找到解决方案。

以下是上述方法的实现:

## C++

```
// C++ program to check if the
// given array can be partitioned
// into K subsets with equal sum
#include <bits/stdc++.h>
using namespace std;

// Function to check whether
// K required partitions
// are possible or not
bool isKPartitionPossible(int arr[],
                          int N, int K)
{
    if (K == 1)
        // Return true as the
        // entire array is the
        // answer
        return true;

    // If total number of
    // partitions exceeds
    // size of the array
    if (N < K)
        return false;

    int sum = 0;
    for (int i = 0; i < N; i++)
        sum += arr[i];
    // If the array sum is not
    // divisible by K
    if (sum % K != 0)
        // No such partitions are
        // possible
        return false;

    // Required sum of
    // each subset
    int target = sum / K;

    // Initialize dp array with -1
    int dp[(1 << 15)];
    for (int i = 0; i < (1 << N); i++)
        dp[i] = -1;

    // Sum of empty subset
    // is zero
    dp[0] = 0;

    // Iterate over all subsets/masks
    for (int mask = 0; mask < (1 << N); mask++) {
        // if current mask is invalid, continue
        if (dp[mask] == -1)
            continue;

        // Iterate over all array elements
        for (int i = 0; i < N; i++) {
            // Check if the current element
            // can be added to the current
            // subset/mask
            if (!(mask & (1 << i))
                && dp[mask]
                           + arr[i]
                       <= target) {
                // transition
                dp[mask | (1 << i)]
                    = (dp[mask]
                       + arr[i])
                      % target;
            }
        }
    }

    if (dp[(1 << N) - 1] == 0)
        return true;
    else
        return false;
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 4, 5, 3, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    if (isKPartitionPossible(arr, N, K)) {
        cout << "Partitions into equal ";
        cout << "sum is possible.\n";
    }
    else {
        cout << "Partitions into equal ";
        cout << "sum is not possible.\n";
    }
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if the
// given array can be partitioned
// into K subsets with equal sum
import java.util.*;

class GFG{

// Function to check whether
// K required partitions
// are possible or not
static boolean isKPartitionPossible(int arr[],
                                    int N, int K)
{
    if (K == 1)

        // Return true as the
        // entire array is the
        // answer
        return true;

    // If total number of
    // partitions exceeds
    // size of the array
    if (N < K)
        return false;

    int sum = 0;
    for(int i = 0; i < N; i++)
       sum += arr[i];

    // If the array sum is not
    // divisible by K
    if (sum % K != 0)

        // No such partitions are
        // possible
        return false;

    // Required sum of
    // each subset
    int target = sum / K;

    // Initialize dp array with -1
    int []dp = new int[(1 << 15)];
    for(int i = 0; i < (1 << N); i++)
       dp[i] = -1;

    // Sum of empty subset
    // is zero
    dp[0] = 0;

    // Iterate over all subsets/masks
    for(int mask = 0; mask < (1 << N); mask++)
    {

       // if current mask is invalid, continue
       if (dp[mask] == -1)
           continue;

       // Iterate over all array elements
       for(int i = 0; i < N; i++)
       {

          // Check if the current element
          // can be added to the current
          // subset/mask
          if (((mask & (1 << i)) == 0) &&
             dp[mask] + arr[i] <= target)
          {

              // Transition
              dp[mask | (1 << i)] = (dp[mask] +
                                      arr[i]) %
                                      target;
          }
       }
    }

    if (dp[(1 << N) - 1] == 0)
        return true;
    else
        return false;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 1, 4, 5, 3, 3 };
    int N = arr.length;
    int K = 3;

    if (isKPartitionPossible(arr, N, K))
    {
        System.out.print("Partitions into equal ");
        System.out.print("sum is possible.\n");
    }
    else
    {
        System.out.print("Partitions into equal ");
        System.out.print("sum is not possible.\n");
    }
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to check if the
# given array can be partitioned
# into K subsets with equal sum

# Function to check whether
# K required partitions
# are possible or not
def isKPartitionPossible(arr, N, K):

    if (K == 1):

        # Return true as the
        # entire array is the
        # answer
        return True

    # If total number of
    # partitions exceeds
    # size of the array
    if (N < K):
        return False

    sum = 0
    for i in range(N):
        sum += arr[i]

    # If the array sum is not
    # divisible by K
    if (sum % K != 0):

        # No such partitions are
        # possible
        return False

    # Required sum of
    # each subset
    target = sum / K

    # Initialize dp array with -1
    dp = [0 for i in range(1 << 15)]
    for i in range((1 << N)):
        dp[i] = -1

    # Sum of empty subset
    # is zero
    dp[0] = 0

    # Iterate over all subsets/masks
    for mask in range((1 << N)):

        # If current mask is invalid,
        # continue
        if (dp[mask] == -1):
            continue

        # Iterate over all array elements
        for i in range(N):

            # Check if the current element
            # can be added to the current
            # subset/mask
            if ((mask & (1 << i) == 0) and
              dp[mask] + arr[i] <= target):

                # Transition
                dp[mask | (1 << i)] = ((dp[mask] +
                                        arr[i]) %
                                        target)

    if (dp[(1 << N) - 1] == 0):
        return True
    else:
        return False

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 1, 4, 5, 3, 3 ]
    N = len(arr)
    K = 3

    if (isKPartitionPossible(arr, N, K)):
        print("Partitions into equal "\
              "sum is possible.")
    else:
        print("Partitions into equal sum "\
              "is not possible.")

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to check if the
// given array can be partitioned
// into K subsets with equal sum
using System;

class GFG{

// Function to check whether
// K required partitions
// are possible or not
static bool isKPartitionPossible(int []arr,
                                 int N, int K)
{
    if (K == 1)

        // Return true as the
        // entire array is the
        // answer
        return true;

    // If total number of
    // partitions exceeds
    // size of the array
    if (N < K)
        return false;

    int sum = 0;
    for(int i = 0; i < N; i++)
       sum += arr[i];

    // If the array sum is not
    // divisible by K
    if (sum % K != 0)

        // No such partitions are
        // possible
        return false;

    // Required sum of
    // each subset
    int target = sum / K;

    // Initialize dp array with -1
    int []dp = new int[(1 << 15)];
    for(int i = 0; i < (1 << N); i++)
       dp[i] = -1;

    // Sum of empty subset
    // is zero
    dp[0] = 0;

    // Iterate over all subsets/masks
    for(int mask = 0; mask < (1 << N); mask++)
    {

       // If current mask is invalid, continue
       if (dp[mask] == -1)
           continue;

       // Iterate over all array elements
       for(int i = 0; i < N; i++)
       {

          // Check if the current element
          // can be added to the current
          // subset/mask
          if (((mask & (1 << i)) == 0) &&
             dp[mask] + arr[i] <= target)
          {

              // Transition
              dp[mask | (1 << i)] = (dp[mask] +
                                      arr[i]) %
                                      target;
          }
       }
    }

    if (dp[(1 << N) - 1] == 0)
        return true;
    else
        return false;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 1, 4, 5, 3, 3 };
    int N = arr.Length;
    int K = 3;

    if (isKPartitionPossible(arr, N, K))
    {
        Console.Write("Partitions into equal ");
        Console.Write("sum is possible.\n");
    }
    else
    {
        Console.Write("Partitions into equal ");
        Console.Write("sum is not possible.\n");
    }
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program to check if the
// given array can be partitioned
// into K subsets with equal sum

// Function to check whether
// K required partitions
// are possible or not
function isKPartitionPossible(arr, N, K)
{
    if (K == 1)

        // Return true as the
        // entire array is the
        // answer
        return true;

    // If total number of
    // partitions exceeds
    // size of the array
    if (N < K)
        return false;

    let sum = 0;
    for(let i = 0; i < N; i++)
       sum += arr[i];

    // If the array sum is not
    // divisible by K
    if (sum % K != 0)

        // No such partitions are
        // possible
        return false;

    // Required sum of
    // each subset
    let target = sum / K;

    // Initialize dp array with -1
    let dp = Array.from({length: (1 << 15)}, (_, i) => 0);
    for(let i = 0; i < (1 << N); i++)
       dp[i] = -1;

    // Sum of empty subset
    // is zero
    dp[0] = 0;

    // Iterate over all subsets/masks
    for(let mask = 0; mask < (1 << N); mask++)
    {

       // if current mask is invalid, continue
       if (dp[mask] == -1)
           continue;

       // Iterate over all array elements
       for(let i = 0; i < N; i++)
       {

          // Check if the current element
          // can be added to the current
          // subset/mask
          if (((mask & (1 << i)) == 0) &&
             dp[mask] + arr[i] <= target)
          {

              // Transition
              dp[mask | (1 << i)] = (dp[mask] +
                                      arr[i]) %
                                      target;
          }
       }
    }

    if (dp[(1 << N) - 1] == 0)
        return true;
    else
        return false;
}

// Driver Code

    let arr = [ 2, 1, 4, 5, 3, 3 ];
    let N = arr.length;
    let K = 3;

    if (isKPartitionPossible(arr, N, K))
    {
        document.write("Partitions into equal ");
        document.write("sum is possible.\n");
    }
    else
    {
        document.write("Partitions into equal ");
        document.write("sum is not possible.\n");
    }

</script>
```

**输出:**

```
Partitions into equal sum is possible.
```

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O (2 <sup>N</sup> )*