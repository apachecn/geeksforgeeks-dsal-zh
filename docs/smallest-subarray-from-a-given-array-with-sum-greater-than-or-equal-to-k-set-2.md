# 给定阵列中最小的子阵列，其和大于或等于 K |集合 2

> 原文:[https://www . geeksforgeeks . org/给定数组中最小子数组的和大于或等于 k-set-2/](https://www.geeksforgeeks.org/smallest-subarray-from-a-given-array-with-sum-greater-than-or-equal-to-k-set-2/)

给定一个由 **N** 正整数和一个整数 **K** 组成的数组 **A[]** ，任务是找出和大于等于 **K** 的最小子阵的长度。如果没有这样的子阵列，打印 **-1** 。

**示例:**

> **输入:** arr[] = {3，1，7，1，2}，K = 11
> **输出:** 3
> **解释:**
> 和≥ K(= 11)的最小子阵为{3，1，7}。
> 
> **输入:** arr[] = {2，3，5，4，1}，K = 11
> **输出:** 3
> **解释:**
> 最小可能的子阵是{3，5，4}。

**天真和二分搜索法方法:**参考给定阵列中的[最小子阵列，其和大于或等于 K](https://www.geeksforgeeks.org/smallest-subarray-from-a-given-array-with-sum-greater-than-or-equal-to-k/) 以获得最简单的方法和基于[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的方法来解决问题。

**递归法:**解决问题最简单的方法就是使用[递归](https://www.geeksforgeeks.org/recursion/)。按照以下步骤解决问题:

*   **如果 K ≤ 0:** 打印 **-1** ，因为无法获得这样的子阵列。
*   如果数组的和等于 **K** ，打印数组的长度作为所需答案。
*   如果数组中的第一个元素大于 **K** ，则打印 1 作为所需答案。
*   否则，通过考虑子阵列中的当前元素以及不包括它，继续寻找最小的子阵列。
*   对遍历的每个元素重复上述步骤。

下面是上述方法的实现:

## C++14

```
// C++14 program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest subarray
// sum greater than or equal to target
int smallSumSubset(vector<int> data,
                   int target, int maxVal)
{
    int sum = 0;

    for(int i : data)
        sum += i;

    // Base Case
    if (target <= 0)
        return 0;

    // If sum of the array
    // is less than target
    else if (sum < target)
        return maxVal;

    // If target is equal to
    // the sum of the array
    else if (sum == target)
        return data.size();

    // Required condition
    else if (data[0] >= target)
        return 1;

    else if (data[0] < target)
    {
        vector<int> temp;
        for(int i = 1; i < data.size(); i++)
            temp.push_back(data[i]);

        return min(smallSumSubset(temp, target,
                                  maxVal),
               1 + smallSumSubset(temp, target -
                               data[0], maxVal));
    }
}

// Driver Code
int main()
{
    vector<int> data = { 3, 1, 7, 1, 2 };
    int target = 11;

    int val = smallSumSubset(data, target,
                             data.size() + 1);

    if (val > data.size())
        cout << -1;
    else
        cout << val;
}    

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to find the smallest subarray
// sum greater than or equal to target
static int smallSumSubset(List<Integer> data,
                          int target, int maxVal)
{
    int sum = 0;

    for(Integer i : data)
        sum += i;

    // Base Case
    if (target <= 0)
        return 0;

    // If sum of the array
    // is less than target
    else if (sum < target)
        return maxVal;

    // If target is equal to
    // the sum of the array
    else if (sum == target)
        return data.size();

    // Required condition
    else if (data.get(0) >= target)
        return 1;

    else if (data.get(0) < target)
    {
        List<Integer> temp = new ArrayList<>();
        for(int i = 1; i < data.size(); i++)
            temp.add(data.get(i));

        return Math.min(smallSumSubset(temp, target,
                                             maxVal),
                    1 + smallSumSubset(temp, target -
                                data.get(0), maxVal));
    }
    return -1;
}

// Driver Code
public static void main (String[] args)
{
    List<Integer> data = Arrays.asList(3, 1, 7, 1, 2);
    int target = 11;

    int val = smallSumSubset(data, target,
                             data.size() + 1);

    if (val > data.size())
        System.out.println(-1);
    else
        System.out.println(val);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the smallest subarray
# sum greater than or equal to target
def smallSumSubset(data, target, maxVal):
    # base condition

    # Base Case
    if target <= 0:
        return 0

    # If sum of the array
    # is less than target
    elif sum(data) < target:
        return maxVal

    # If target is equal to
    # the sum of the array
    elif sum(data) == target:
        return len(data)

    # Required condition
    elif data[0] >= target:
        return 1

    elif data[0] < target:
        return min(smallSumSubset(data[1:], \
        target, maxVal),
                1 + smallSumSubset(data[1:], \
                target-data[0], maxVal))

# Driver Code
data = [3, 1, 7, 1, 2]
target = 11

val = smallSumSubset(data, target, len(data)+1)

if val > len(data):
    print(-1)
else:
    print(val)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the smallest subarray
// sum greater than or equal to target
static int smallSumSubset(List<int> data,
                   int target, int maxVal)
{
    int sum = 0;

    foreach(int i in data)
        sum += i;

    // Base Case
    if (target <= 0)
        return 0;

    // If sum of the array
    // is less than target
    else if (sum < target)
        return maxVal;

    // If target is equal to
    // the sum of the array
    else if (sum == target)
        return data.Count;

    // Required condition
    else if (data[0] >= target)
        return 1;

    else if (data[0] < target)
    {
        List<int> temp = new List<int>();
        for(int i = 1; i < data.Count; i++)
            temp.Add(data[i]); 

        return Math.Min(smallSumSubset(temp, target, 
                                       maxVal), 
                    1 + smallSumSubset(temp, target - 
                                    data[0], maxVal));
    }
    return 0;
}

// Driver code
static void Main()
{
    List<int> data = new List<int>();
    data.Add(3);
    data.Add(1);
    data.Add(7);
    data.Add(1);
    data.Add(2);

    int target = 11;

    int val = smallSumSubset(data, target,
                             data.Count + 1);

    if (val > data.Count)
        Console.Write(-1);
    else
        Console.Write(val);
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// js program for the above approach

// Function to find the smallest subarray
// sum greater than or equal to target
function smallSumSubset(data, target, maxVal)
{
    let sum = 0;

    for(let i=0;i< data.length;i++)
        sum += data[i];

    // Base Case
    if (target <= 0)
        return 0;

    // If sum of the array
    // is less than target
    else if (sum < target)
        return maxVal;

    // If target is equal to
    // the sum of the array
    else if (sum == target)
        return data.length;

    // Required condition
    else if (data[0] >= target)
        return 1;

    else if (data[0] < target)
    {
        let temp = [];
        for(let i = 1; i < data.length; i++)
            temp.push(data[i]);

        return Math.min(smallSumSubset(temp, target,
                                  maxVal),
               1 + smallSumSubset(temp, target -
                               data[0], maxVal));
    }
}

// Driver Code
let data = [ 3, 1, 7, 1, 2 ];
let target = 11;
let val = smallSumSubset(data, target,
                             data.length + 1);

    if (val > data.length)
        document.write( -1);
    else
        document.write(val);

</script>
```

**Output**

```
3
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过记忆子问题来使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)进行优化，以避免重复计算。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the smallest subarray
// with sum greater than or equal target
int minlt(vector<int> arr, int target, int n)
{

    // DP table to store the
    // computed subproblems
    vector<vector<int>> dp(arr.size() + 1 ,
           vector<int> (target + 1, -1));

    for(int i = 0; i < arr.size() + 1; i++)

        // Initialize first
        // column with 0
        dp[i][0] = 0;

    for(int j = 0; j < target + 1; j++)

        // Initialize first
        // row with 0
        dp[0][j] = INT_MAX;

    for(int i = 1; i <= arr.size(); i++)
    {
        for(int j = 1; j <= target; j++)
        {

            // Check for invalid condition
            if (arr[i - 1] > j)
            {
                dp[i][j] = dp[i - 1][j];
            }
            else
            {

                // Fill up the dp table
                dp[i][j] = min(dp[i - 1][j],
                   (dp[i][j - arr[i - 1]]) !=
                   INT_MAX ?
                   (dp[i][j - arr[i - 1]] + 1) :
                   INT_MAX);
            }
        }
    }

    // Print the minimum length
    if (dp[arr.size()][target] == INT_MAX)
    {
        return -1;
    }
    else
    {
        return dp[arr.size()][target];
    }
}

// Driver code
int main()
{
    vector<int> arr = { 2, 3, 5, 4, 1 };
    int target = 11;
    int n = arr.size();

    cout << minlt(arr, target, n);
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the smallest subarray
// with sum greater than or equal target
static int minlt(int[] arr, int target, int n)
{

    // DP table to store the
    // computed subproblems
    int[][] dp = new int[arr.length + 1][target + 1];

    for(int[] row : dp)
        Arrays.fill(row, -1);

    for(int i = 0; i < arr.length + 1; i++)

        // Initialize first
        // column with 0
        dp[i][0] = 0;

    for(int j = 0; j < target + 1; j++)

        // Initialize first
        // row with 0
        dp[0][j] = Integer.MAX_VALUE;

    for(int i = 1; i <= arr.length; i++)
    {
        for(int j = 1; j <= target; j++)
        {

            // Check for invalid condition
            if (arr[i - 1] > j)
            {
                dp[i][j] = dp[i - 1][j];
            }
            else
            {

                // Fill up the dp table
                dp[i][j] = Math.min(dp[i - 1][j],
                        (dp[i][j - arr[i - 1]]) !=
                        Integer.MAX_VALUE ?
                        (dp[i][j - arr[i - 1]] + 1) :
                        Integer.MAX_VALUE);
            }
        }
    }

    // Print the minimum length
    if (dp[arr.length][target] == Integer.MAX_VALUE)
    {
        return -1;
    }
    else
    {
        return dp[arr.length][target];
    }
}

// Driver code
public static void main (String[] args)
{
    int[] arr = { 2, 3, 5, 4, 1 };
    int target = 11;
    int n = arr.length;

    System.out.print(minlt(arr, target, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

import sys

# Function to find the smallest subarray
# with sum greater than or equal target
def minlt(arr, target, n):

    # DP table to store the
    # computed subproblems
    dp = [[-1 for _ in range(target + 1)]\
    for _ in range(len(arr)+1)]

    for i in range(len(arr)+1):

        # Initialize first
        # column with 0
        dp[i][0] = 0

    for j in range(target + 1):

        # Initialize first
        # row with 0
        dp[0][j] = sys.maxsize

    for i in range(1, len(arr)+1):
        for j in range(1, target + 1):

            # Check for invalid condition
            if arr[i-1] > j:
                dp[i][j] = dp[i-1][j]

            else:
                # Fill up the dp table
                dp[i][j] = min(dp[i-1][j], \
                1 + dp[i][j-arr[i-1]])

    return dp[-1][-1]

    # Print the minimum length
    if dp[-1][-1] == sys.maxsize:
        return(-1)
    else:
        return dp[-1][-1]

# Driver Code
arr = [2, 3, 5, 4, 1]
target = 11
n = len(arr)

print(minlt(arr, target, n))
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find the
// smallest subarray with
// sum greater than or equal
// target
static int minlt(int[] arr,
                 int target,
                 int n)
{   
  // DP table to store the
  // computed subproblems
  int[,] dp = new int[arr.Length + 1,
                      target + 1];

  for(int i = 0;
          i < arr.Length + 1; i++)
  {
    for (int j = 0;
             j < target + 1; j++)
    {
      dp[i, j] = -1;
    }
  }

  for(int i = 0;
          i < arr.Length + 1; i++)

    // Initialize first
    // column with 0
    dp[i, 0] = 0;

  for(int j = 0;
          j < target + 1; j++)

    // Initialize first
    // row with 0
    dp[0, j] = int.MaxValue;

  for(int i = 1;
          i <= arr.Length; i++)
  {
    for(int j = 1;
            j <= target; j++)
    {
      // Check for invalid
      // condition
      if (arr[i - 1] > j)
      {
        dp[i, j] = dp[i - 1, j];
      }
      else
      {
        // Fill up the dp table
        dp[i, j] = Math.Min(dp[i - 1, j],
                           (dp[i, j -
                            arr[i - 1]]) !=
                           int.MaxValue ?
                           (dp[i, j -
                            arr[i - 1]] + 1) :
                           int.MaxValue);
      }
    }
  }

  // Print the minimum
  // length
  if (dp[arr.Length,
         target] == int.MaxValue)
  {
    return -1;
  }
  else
  {
    return dp[arr.Length,
              target];
  }
}

// Driver code
public static void Main(String[] args)
{
  int[] arr = {2, 3, 5, 4, 1};
  int target = 11;
  int n = arr.Length;
  Console.Write(
  minlt(arr, target, n));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the smallest subarray
// with sum greater than or equal target
function minlt(arr, target, n)
{

    // DP table to store the
    // computed subproblems
    var dp = Array.from(Array(arr.length+1),
    ()=>Array(target+1).fill(-1));

    for(var i = 0; i < arr.length + 1; i++)

        // Initialize first
        // column with 0
        dp[i][0] = 0;

    for(var j = 0; j < target + 1; j++)

        // Initialize first
        // row with 0
        dp[0][j] = 1000000000;

    for(var i = 1; i <= arr.length; i++)
    {
        for(var j = 1; j <= target; j++)
        {

            // Check for invalid condition
            if (arr[i - 1] > j)
            {
                dp[i][j] = dp[i - 1][j];
            }
            else
            {

                // Fill up the dp table
                dp[i][j] = Math.min(dp[i - 1][j],
                   (dp[i][j - arr[i - 1]]) !=
                   1000000000 ?
                   (dp[i][j - arr[i - 1]] + 1) :
                   1000000000);
            }
        }
    }

    // Print the minimum length
    if (dp[arr.length][target] == 1000000000)
    {
        return -1;
    }
    else
    {
        return dp[arr.length][target];
    }
}

// Driver code

var arr = [2, 3, 5, 4, 1];
var target = 11;
var n = arr.length;

document.write( minlt(arr, target, n));

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*