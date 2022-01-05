# 通过最小化每个子阵列中重复元素的数量，以最小的成本将阵列分成子阵列

> 原文:[https://www . geeksforgeeks . org/通过最小化每个子阵列中重复元素的数量以最小的成本将阵列分成子阵列/](https://www.geeksforgeeks.org/split-array-into-subarrays-at-minimum-cost-by-minimizing-count-of-repeating-elements-in-each-subarray/)

给定范围为**【1，N】**和整数 **K** 的具有 **N** 个整数的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到最小可能成本，将阵列分割成非空子阵列，这可以基于以下条件实现:

*   如果子阵列中不存在唯一元素，则成本为 **K** 。
*   否则，成本为 **K** +每个重复元素的[频率之和。](https://www.geeksforgeeks.org/find-the-frequencies-of-all-duplicates-elements-in-the-array/)

**示例:**

> ***输入:** arr[] = {1，2，3，1，2，3}，K = 2*
> ***输出:** 4*
> **解释:**
> 将阵列拆分为子阵列{1，2，3}和{1，2，3}会产生最小的成本，因为子阵列都不包含任何重复元素。
> 由于一个子阵列将包含至少一个重复元素，因此所有其他拆分的成本都会更高。
> 因此，最小可能成本为 4。
> 
> ***输入:** arr[] = {1，2，1，1，1}，K = 2*
> ***输出:** 6*

**天真的做法:**解决问题最简单的思路就是[生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)来预计算并存储各自的成本。然后，计算可以在阵列上执行的每个可能拆分的成本。最后，打印所有拆分的最小成本。
按照以下步骤解决问题:

1.  根据上述条件预先计算每个子阵列的成本。
2.  生成可以在阵列上执行的所有可能的拆分。
3.  对于每个拆分，计算每个拆分子阵列的总成本。
4.  保持生成的总成本最小，最后，打印最小的总和。

***时间复杂度:** O(N！)*
***辅助空间:** O(N)*

**高效途径:**思路是利用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)对上述途径进行优化。按照以下步骤解决问题:

1.  在所有索引处用 [INT_MAX](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 初始化一个长度为 **N** 的数组 **dp[]** 。
2.  用**零**初始化数组的第一个元素。
3.  对于任何索引 **i** ，数组**DP【I】**代表将数组分成从 **0 到 i** 的子数组的最小成本。
4.  对于每个指数 **i** ，计算从 **i 到 N** 的所有指数的最小成本。
5.  对数组的所有元素重复这个过程
6.  返回 **dp[]** 的最后一个元素，得到拆分数组的最小代价。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define ll long long
using namespace std;

// Function to find the minimum cost
// of splitting the array into subarrays
int findMinCost(vector<int>& a, int k)
{
    // Size of the array
    int n = (int)a.size();

    // Get the maximum element
    int max_ele = *max_element(a.begin(),
                               a.end());

    // dp[] will store the minimum cost
    // upto index i
    ll dp[n + 1];

    // Initialize the result array
    for (int i = 1; i <= n; ++i)
        dp[i] = INT_MAX;

    // Initialise the first element
    dp[0] = 0;

    for (int i = 0; i < n; ++i) {

        // Create the frequency array
        int freq[max_ele + 1];

        // Initialize frequency array
        memset(freq, 0, sizeof freq);

        for (int j = i; j < n; ++j) {

            // Update the frequency
            freq[a[j]]++;
            int cost = 0;

            // Counting the cost of
            // the duplicate element
            for (int x = 0;
                 x <= max_ele; ++x) {
                cost += (freq[x] == 1)
                            ? 0
                            : freq[x];
            }

            // Minimum cost of operation
            // from 0 to j
            dp[j + 1] = min(dp[i] + cost + k,
                            dp[j + 1]);
        }
    }

    // Total cost of the array
    return dp[n];
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 1, 1, 1 };

    // Given cost K
    int K = 2;

    // Function Call
    cout << findMinCost(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG {

// Function to find the
// minimum cost of splitting
// the array into subarrays
static long findMinCost(int[] a,
                        int k, int n)
{
  // Get the maximum element
  int max_ele = Arrays.stream(a).max().getAsInt();

  // dp[] will store the minimum cost
  // upto index i
  long[] dp = new long[n + 1];

  // Initialize the result array
  for (int i = 1; i <= n; ++i)
    dp[i] = Integer.MAX_VALUE;

  // Initialise the first element
  dp[0] = 0;

  for (int i = 0; i < n; ++i)
  {
    // Create the frequency array
    int[] freq = new int[max_ele + 1];

    for (int j = i; j < n; ++j)
    {
      // Update the frequency
      freq[a[j]]++;
      int cost = 0;

      // Counting the cost of
      // the duplicate element
      for (int x = 0; x <= max_ele; ++x)
      {
        cost += (freq[x] == 1) ? 0 :
                 freq[x];
      }

      // Minimum cost of operation
      // from 0 to j
      dp[j + 1] = Math.min(dp[i] + cost + k,
                           dp[j + 1]);
    }
  }

  // Total cost of the array
  return dp[n];
}

// Driver Code
public static void main(String[] args)
{
  int[] arr = {1, 2, 1, 1, 1};

  // Given cost K
  int K = 2;
  int n = arr.length;

  // Function Call
  System.out.print(findMinCost(arr,
                               K, n));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the
# minimum cost of splitting
# the array into subarrays
def findMinCost(a, k, n):

    # Get the maximum element
    max_ele = max(a)

    # dp will store the minimum cost
    # upto index i
    dp = [0] * (n + 1)

    # Initialize the result array
    for i in range(1, n + 1):
        dp[i] = sys.maxsize

    # Initialise the first element
    dp[0] = 0

    for i in range(0, n):

        # Create the frequency array
        freq = [0] * (max_ele + 1)

        for j in range(i, n):

            # Update the frequency
            freq[a[j]] += 1
            cost = 0

            # Counting the cost of
            # the duplicate element
            for x in range(0, max_ele + 1):
                cost += (0 if (freq[x] == 1) else
                               freq[x])

            # Minimum cost of operation
            # from 0 to j
            dp[j + 1] = min(dp[i] + cost + k,
                            dp[j + 1])

    # Total cost of the array
    return dp[n]

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 1, 1, 1 ];

    # Given cost K
    K = 2;
    n = len(arr);

    # Function call
    print(findMinCost(arr, K, n));

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;
class GFG{

// Function to find the
// minimum cost of splitting
// the array into subarrays
static long findMinCost(int[] a,
                        int k, int n)
{
  // Get the maximum element
  int max_ele = a.Max();

  // []dp will store the minimum cost
  // upto index i
  long[] dp = new long[n + 1];

  // Initialize the result array
  for (int i = 1; i <= n; ++i)
    dp[i] = int.MaxValue;

  // Initialise the first element
  dp[0] = 0;

  for (int i = 0; i < n; ++i)
  {
    // Create the frequency array
    int[] freq = new int[max_ele + 1];

    for (int j = i; j < n; ++j)
    {
      // Update the frequency
      freq[a[j]]++;
      int cost = 0;

      // Counting the cost of
      // the duplicate element
      for (int x = 0; x <= max_ele; ++x)
      {
        cost += (freq[x] == 1) ? 0 :
                 freq[x];
      }

      // Minimum cost of operation
      // from 0 to j
      dp[j + 1] = Math.Min(dp[i] + cost + k,
                           dp[j + 1]);
    }
  }

  // Total cost of the array
  return dp[n];
}

// Driver Code
public static void Main(String[] args)
{
  int[] arr = {1, 2, 1, 1, 1};

  // Given cost K
  int K = 2;
  int n = arr.Length;

  // Function Call
  Console.Write(findMinCost(arr,
                               K, n));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum cost
// of splitting the array into subarrays
function findMinCost(a, k)
{

    // Size of the array
    var n = a.length;

    // Get the maximum element
    var max_ele = a.reduce((a, b) => Math.max(a, b))

    // dp[] will store the minimum cost
    // upto index i
    var dp = Array(n + 1).fill(1000000000);

    // Initialise the first element
    dp[0] = 0;

    for(var i = 0; i < n; ++i)
    {

        // Create the frequency array
        var freq = Array(max_ele + 1).fill(0);

        for(var j = i; j < n; ++j)
        {

            // Update the frequency
            freq[a[j]]++;
            var cost = 0;

            // Counting the cost of
            // the duplicate element
            for(var x = 0; x <= max_ele; ++x)
            {
                cost += (freq[x] == 1) ? 0 : freq[x];
            }

            // Minimum cost of operation
            // from 0 to j
            dp[j + 1] = Math.min(dp[i] + cost + k,
                                 dp[j + 1]);
        }
    }

    // Total cost of the array
    return dp[n];
}

// Driver Code
var arr = [ 1, 2, 1, 1, 1 ];

// Given cost K
var K = 2;

// Function Call
document.write(findMinCost(arr, K));

// This code is contributed by itsok

</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N <sup>3</sup> ，其中 N 为给定数组的大小。*
***辅助空间:** O(N)*