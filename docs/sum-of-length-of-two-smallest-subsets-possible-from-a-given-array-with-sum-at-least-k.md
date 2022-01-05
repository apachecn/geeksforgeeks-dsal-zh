# 给定数组中两个最小子集长度之和，和至少为 K

> 原文:[https://www . geeksforgeeks . org/两个最小子集的长度之和-从给定的数组中可能得到至少 k 的和/](https://www.geeksforgeeks.org/sum-of-length-of-two-smallest-subsets-possible-from-a-given-array-with-sum-at-least-k/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找出两个最小唯一[子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)的长度之和，这两个子集的元素之和**至少为 K** 。

**示例:**

> **输入:** arr[] = {2，4，5，6，7，8}，K = 16
> **输出:** 6
> **解释:**
> 子集{2，6，8}和{4，5，7}是和 K(= 16)最小的两个子集。
> 因此，这两个子集的长度之和= 3 + 3 = 6。
> 
> **输入:** arr[] = {14，3，7，8，9，7，12，15，10，6}，K = 40
> **输出:** 8

**方法:**给定的问题可以基于以下观察来解决:

*   [对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序将问题简化为在索引**【I，N】**的范围内选择一个总和至少为**K**的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，然后检查在索引**【I，N】**的范围内剩余数组元素的总和是否为 **K** 。
*   为了实现上述思想，使用了一个 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)，比如说 **dp[][]** ，使得 **dp[i][j]** 存储在索引**【I，N】**范围内的子集的最小和，该索引的值**至少为 j。**则过渡状态类似于 [0/1 背包](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)，可以定义为:
    *   如果 **arr[i]** 的值大于 **j** ，则更新 **dp[i][j]** 为 **arr[i]** 。
    *   否则，将 **dp[i][j]** 更新至最小 **dp[i + 1][j]** 和**(DP[I+1][j–arr[I]]+arr[I])**。

按照以下步骤解决问题:

*   [按升序排列数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   初始化一个数组，说出**后缀[]，**，将数组 **arr[]** 的[后缀和](https://www.geeksforgeeks.org/tag/suffix-sum/)存入其中。
*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/dynamically-allocate-2d-array-c/)，比如说 **dp[][]，**，使得 **dp[i][j]** 存储索引范围内子集的最小和**【I，N】**，其值**至少为 j** 。
*   将 **dp[N][0]** 初始化为 **0** ，将所有其他状态初始化为 [**INT_MAX**](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 。
*   [以相反的顺序遍历数组**arr【I】**](https://www.geeksforgeeks.org/iterating-arrays-java/)，并执行以下步骤:
    *   以相反的顺序迭代索引范围**【0，K】**，并执行以下操作:
        *   如果 **arr[i]** 的值至少为 **j** ，则将 **dp[i][j]** 的值更新为 **arr[i]** ，因为当前状态的总和**至少为 j** 。现在，[继续迭代](https://www.geeksforgeeks.org/continue-statement-cpp/)。
        *   如果下一状态，即**DP[I+1][j–arr[I]]**的值为 **INT_MAX** ，则更新 **dp[i][j]** 为 **INT_MAX** 。
        *   否则，更新 **dp[i][j]** 作为 **dp[i + 1][j]** 和**(DP[I+1][j–arr[I]+arr[I])**的最小值，以存储总和**至少为 j** 的所有值的总和。
*   现在，[以相反的顺序遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **后缀[]** ，如果**(后缀[I]–DP[I][K])**的值至少为**K**，则打印**(N–I)**作为形成的两个最小子集的大小之和，[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
const int MAX = 1e9;

// Function to calculate sum of lengths
// of two smallest subsets with sum >= K
int MinimumLength(int A[], int N, int K)
{
    // Sort the array in ascending order
    sort(A, A + N);

    // Stores suffix sum of the array
    int suffix[N + 1] = { 0 };

    // Update the suffix sum array
    for (int i = N - 1; i >= 0; i--)
        suffix[i] = suffix[i + 1] + A[i];

    // Stores all dp-states
    int dp[N + 1][K + 1];

    // Initialize all dp-states
    // with a maximum possible value
    for (int i = 0; i <= N; i++)
        for (int j = 0; j <= K; j++)
            dp[i][j] = MAX;

    // Base Case
    dp[N][0] = 0;

    // Traverse the array arr[]
    for (int i = N - 1; i >= 0; i--) {

        // Iterate over the range [0, K]
        for (int j = K; j >= 0; j--) {

            // If A[i] is equal to at
            // least the required sum
            // j for the current state
            if (j <= A[i]) {
                dp[i][j] = A[i];
                continue;
            }

            // If the next possible
            // state doesn't exist
            if (dp[i + 1][j - A[i]] == MAX)
                dp[i][j] = MAX;

            // Otherwise, update the current
            // state to the minimum of the
            // next state and state including
            // the current element A[i]
            else
                dp[i][j] = min(dp[i + 1][j],
                               dp[i + 1][j - A[i]] + A[i]);
        }
    }

    // Traverse the suffix sum array
    for (int i = N - 1; i >= 0; i--) {

        // If suffix[i] - dp[i][K] >= K
        if (suffix[i] - dp[i][K] >= K) {

            // Sum of lengths of the two
            // smallest subsets is obtained
            return N - i;
        }
    }

    // Return -1, if there doesn't
    // exist any subset of sum >= K
    return -1;
}

// Driver Code
int main()
{
    int arr[] = { 7, 4, 5, 6, 8 };
    int K = 13;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << MinimumLength(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

static int MAX = (int)(1e9);

// Function to calculate sum of lengths
// of two smallest subsets with sum >= K
static int MinimumLength(int A[], int N, int K)
{

    // Sort the array in ascending order
    Arrays.sort(A);

    // Stores suffix sum of the array
    int suffix[] = new int[N + 1];

    // Update the suffix sum array
    for(int i = N - 1; i >= 0; i--)
        suffix[i] = suffix[i + 1] + A[i];

    // Stores all dp-states
    int dp[][] = new int[N + 1][K + 1];

    // Initialize all dp-states
    // with a maximum possible value
    for(int i = 0; i <= N; i++)
        for(int j = 0; j <= K; j++)
            dp[i][j] = MAX;

    // Base Case
    dp[N][0] = 0;

    // Traverse the array arr[]
    for(int i = N - 1; i >= 0; i--)
    {

        // Iterate over the range [0, K]
        for(int j = K; j >= 0; j--)
        {

            // If A[i] is equal to at
            // least the required sum
            // j for the current state
            if (j <= A[i])
            {
                dp[i][j] = A[i];
                continue;
            }

            // If the next possible
            // state doesn't exist
            if (dp[i + 1][j - A[i]] == MAX)
                dp[i][j] = MAX;

            // Otherwise, update the current
            // state to the minimum of the
            // next state and state including
            // the current element A[i]
            else
                dp[i][j] = Math.min(dp[i + 1][j],
                                    dp[i + 1][j - A[i]]
                                         + A[i]);
        }
    }

    // Traverse the suffix sum array
    for(int i = N - 1; i >= 0; i--)
    {

        // If suffix[i] - dp[i][K] >= K
        if (suffix[i] - dp[i][K] >= K)
        {

            // Sum of lengths of the two
            // smallest subsets is obtained
            return N - i;
        }
    }

    // Return -1, if there doesn't
    // exist any subset of sum >= K
    return -1;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 7, 4, 5, 6, 8 };
    int K = 13;
    int N = arr.length;

    System.out.println(MinimumLength(arr, N, K));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach
MAX = 1e9

# Function to calculate sum of lengths
# of two smallest subsets with sum >= K
def MinimumLength(A, N, K):

    # Sort the array in ascending order
    A.sort()

    # Stores suffix sum of the array
    suffix = [0] * (N + 1)

    # Update the suffix sum array
    for i in range(N - 1, -1, -1):
        suffix[i] = suffix[i + 1] + A[i]

    # Stores all dp-states
    dp = [[0] * (K + 1)] * (N + 1)

    # Initialize all dp-states
    # with a maximum possible value
    for i in range(N + 1):
        for j in range(K + 1):
            dp[i][j] = MAX

    # Base Case
    dp[N][0] = 0

    # Traverse the array arr[]
    for i in range(N - 1, -1, -1):

        # Iterate over the range [0, K]
        for j in range(K, -1, -1):

            # If A[i] is equal to at
            # least the required sum
            # j for the current state
            if (j <= A[i]) :
                dp[i][j] = A[i]
                continue

            # If the next possible
            # state doesn't exist
            if (dp[i + 1][j - A[i]] == MAX):
                dp[i][j] = MAX

            # Otherwise, update the current
            # state to the minimum of the
            # next state and state including
            # the current element A[i]
            else :
                dp[i][j] = min(dp[i + 1][j],
                               dp[i + 1][j - A[i]] + A[i])

    # Traverse the suffix sum array
    for i in range(N - 1, -1, -1):

        # If suffix[i] - dp[i][K] >= K
        if (suffix[i] - dp[i][K] >= K):

            # Sum of lengths of the two
            # smallest subsets is obtained
            return N - i

    # Return -1, if there doesn't
    # exist any subset of sum >= K
    return -1

# Driver Code
arr = [ 7, 4, 5, 6, 8 ]
K = 13
N = len(arr)

print(MinimumLength(arr, N, K))

# This code is contributed by splevel62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int MAX = (int)(1e9);

// Function to calculate sum of lengths
// of two smallest subsets with sum >= K
static int MinimumLength(int[] A, int N, int K)
{

    // Sort the array in ascending order
    Array.Sort(A);

    // Stores suffix sum of the array
    int[] suffix = new int[N + 1];

    // Update the suffix sum array
    for(int i = N - 1; i >= 0; i--)
        suffix[i] = suffix[i + 1] + A[i];

    // Stores all dp-states
    int[,] dp = new int[N + 1, K + 1];

    // Initialize all dp-states
    // with a maximum possible value
    for(int i = 0; i <= N; i++)
        for(int j = 0; j <= K; j++)
            dp[i, j] = MAX;

    // Base Case
    dp[N, 0] = 0;

    // Traverse the array arr[]
    for(int i = N - 1; i >= 0; i--)
    {

        // Iterate over the range [0, K]
        for(int j = K; j >= 0; j--)
        {

            // If A[i] is equal to at
            // least the required sum
            // j for the current state
            if (j <= A[i])
            {
                dp[i, j] = A[i];
                continue;
            }

            // If the next possible
            // state doesn't exist
            if (dp[i + 1, j - A[i]] == MAX)
                dp[i, j] = MAX;

            // Otherwise, update the current
            // state to the minimum of the
            // next state and state including
            // the current element A[i]
            else
                dp[i, j] = Math.Min(dp[i + 1, j],
                                    dp[i + 1, j - A[i]]
                                         + A[i]);
        }
    }

    // Traverse the suffix sum array
    for(int i = N - 1; i >= 0; i--)
    {

        // If suffix[i] - dp[i][K] >= K
        if (suffix[i] - dp[i, K] >= K)
        {

            // Sum of lengths of the two
            // smallest subsets is obtained
            return N - i;
        }
    }

    // Return -1, if there doesn't
    // exist any subset of sum >= K
    return -1;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 7, 4, 5, 6, 8 };
    int K = 13;
    int N = arr.Length;

    Console.WriteLine(MinimumLength(arr, N, K));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// javascript program for the above approach
var max1 = 1000000000;

// Function to calculate sum of lengths
// of two smallest subsets with sum >= K
function MinimumLength(A, N, K)
{
0
    // Sort the array in ascending order
    A.sort();

    // Stores suffix sum of the array
    var suffix = Array(N + 1).fill(0);

    var i;
    // Update the suffix sum array
    for (i = N - 1; i >= 0; i--)
        suffix[i] = suffix[i + 1] + A[i];

    // Stores all dp-states
    var dp = new Array(N + 1);
    for (i = 0; i < N+1; i++)
       dp[i] = new Array(K + 1);

    // Initialize all dp-states
    // with a max1imum possible value
    var j;
    for (i = 0; i <= N; i++) {
        for (j = 0; j <= K; j++){
            dp[i][j] = max1;
        }
    };

    // Base Case
    dp[N][0] = 0;

    // Traverse the array arr[]
    for (i = N - 1; i >= 0; i--) {

        // Iterate over the range [0, K]
        for (j = K; j >= 0; j--) {

            // If A[i] is equal to at
            // least the required sum
            // j for the current state
            if (j <= A[i]) {
                dp[i][j] = A[i];
                continue;
            }

            // If the next possible
            // state doesn't exist
            if (dp[i + 1][j - A[i]] == max1)
                dp[i][j] = max1;

            // Otherwise, update the current
            // state to the minimum of the
            // next state and state including
            // the current element A[i]
            else
                dp[i][j] = Math.min(dp[i + 1][j],
                               dp[i + 1][j - A[i]] + A[i]);
        }
    }

    // Traverse the suffix sum array
    for (i = N - 1; i >= 0; i--) {

        // If suffix[i] - dp[i][K] >= K
        if (suffix[i] - dp[i][K] >= K) {

            // Sum of lengths of the two
            // smallest subsets is obtained
            return N - i;
        }
    }

    // Return -1, if there doesn't
    // exist any subset of sum >= K
    return -1;
}

// Driver Code

    var arr = [7, 4, 5, 6, 8];
    var K = 13;
    var N = arr.length;

    document.write(MinimumLength(arr, N, K));

// This code is contributed by SURENDRA_GANGWAR.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N * K)*
T5**辅助空间:** O(N * K)