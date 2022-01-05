# 最长递增子序列的数量

> 原文:[https://www . geeksforgeeks . org/最长递增子序列数/](https://www.geeksforgeeks.org/number-of-longest-increasing-subsequences/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算给定数组中存在的[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence-dp-3/)的数量。

**示例:**

> **输入:** arr[] = {2，2，2，2，2}
> **输出:** 5
> **说明:**最长递增子序列的长度为 1，即{2}。因此，长度为 1 的最长递增子序列的计数是 5。
> 
> **输入:** arr[] = {1，3，5，4，7}
> **输出:** 2
> **说明:**最长递增子序列的长度为 4，有 2 个长度为 4 的最长递增子序列，即{1，3，4，7}和{1，3，5，7}。

**天真方法:**最简单的方法是[生成给定数组中存在的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/) **arr[]** 并计算最大长度的递增子序列。检查所有子序列后打印计数。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**优化上述方法，思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)，因为上述问题有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)需要计算多次，减少计算使用[制表或记忆](https://www.geeksforgeeks.org/tabulation-vs-memoization/)。按照以下步骤解决问题:

*   初始化两个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **dp_l[]** 和 **dp_c[]** ，分别存储每个索引处最长递增子序列的长度和最长递增子序列的计数。
*   使用变量 **i** 迭代范围**【1，N–1】**:
    *   使用变量 **j** 迭代范围**【0，I–1】**:
        *   如果 **arr[i] > arr[j]** 则检查以下情况:
            **~** 如果( **dp_l[j]+1)** 大于 **dp_l[i]** ，则更新 **dp_l[i]** 为 **dp_l[j] + 1** ， **dp_c[i]** 为 **dp_c[j]**
*   [找到数组中的最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) **dp_l[]** ，并将其存储在变量 **max_length** 中，该变量将给出 LIS 的长度。
*   用 0 初始化一个变量**计数**，以存储最长递增子序列的数量。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**DP _ l【】**如果在任何索引 **idx** 、**DP _ l【idx】**与 **max_length** 相同，那么将**计数**增加**DP _ c【idx】**。
*   完成上述步骤后，打印**计数**的值，即给定数组中最长递增子序列的数量。

下面是上述方法的实现:

## C++

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

//Function to count the number
// of LIS in the array nums[]
int findNumberOfLIS(vector<int> nums)
{
  //Base Case
  if (nums.size() == 0)
    return 0;

  int n = nums.size();

  //Initialize dp_l array with
  // 1s
  vector<int> dp_l(n, 1);

  //Initialize dp_c array with
  // 1s
  vector<int> dp_c(n, 1);

  for (int i = 0; i < n; i++)
  {
    for (int j = 0; j < i; j++)
    {
      //If current element is
      // smaller
      if (nums[i] <= nums[j])
        continue;

      if  (dp_l[j] + 1 > dp_l[i])
      {
        dp_l[i] = dp_l[j] + 1;
        dp_c[i] = dp_c[j];
      }
      else if (dp_l[j] + 1 == dp_l[i])
        dp_c[i] += dp_c[j];
    }
  }

  //Store the maximum element
  // from dp_l
  int max_length = 0;

  for (int i : dp_l)
    max_length = max(i,max_length);

  //Stores the count of LIS
  int count = 0;

  //Traverse dp_l and dp_c
  // simultaneously
  for(int i = 0; i < n; i++)
  {
    //Update the count
    if (dp_l[i] == max_length)
      count += dp_c[i];
  }

  //Return the count of LIS
  return count;
}

//Driver code
int main()
{
  //Given array arr[]
  vector<int> arr = {1, 3, 5, 4, 7};

  //Function Call
  cout << findNumberOfLIS(arr) << endl;
}

// This code is contributed by Mohit Kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;

class GFG{

// Function to count the number
// of LIS in the array nums[]
static int findNumberOfLIS(int[] nums)
{

  // Base Case
  if (nums.length == 0)
      return 0;

  int n = nums.length;

  // Initialize dp_l array with
  // 1s
  int[] dp_l = new int[n];
  Arrays.fill(dp_l, 1);

  // Initialize dp_c array with
  // 1s
  int[] dp_c = new int[n];
  Arrays.fill(dp_c, 1);

  for(int i = 0; i < n; i++)
  {
    for(int j = 0; j < i; j++)
    {

      // If current element is
      // smaller
      if (nums[i] <= nums[j])
        continue;

      if (dp_l[j] + 1 > dp_l[i])
      {
        dp_l[i] = dp_l[j] + 1;
        dp_c[i] = dp_c[j];
      }
      else if (dp_l[j] + 1 == dp_l[i])
        dp_c[i] += dp_c[j];
    }
  }

  // Store the maximum element
  // from dp_l
  int max_length = 0;

  for(int i : dp_l)
    max_length = Math.max(i, max_length);

  // Stores the count of LIS
  int count = 0;

  // Traverse dp_l and dp_c
  // simultaneously
  for(int i = 0; i < n; i++)
  {

    // Update the count
    if (dp_l[i] == max_length)
      count += dp_c[i];
  }

  // Return the count of LIS
  return count;
}

// Driver code
public static void main(String[] args)
{

  // Given array arr[]
  int[] arr = { 1, 3, 5, 4, 7 };

  // Function Call
  System.out.print(findNumberOfLIS(arr) + "\n");
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of LIS
# in the array nums[]
def findNumberOfLIS(nums):

    # Base Case
    if not nums:
        return 0

    n = len(nums)

    # Initialize dp_l array with 1s
    dp_l = [1] * n

    # Initialize dp_c array with 1s
    dp_c = [1] * n

    for i, num in enumerate(nums):
        for j in range(i):

            # If current element is smaller
            if nums[i] <= nums[j]:
                continue

            # Otherwise
            if dp_l[j] + 1 > dp_l[i]:
                dp_l[i] = dp_l[j] + 1
                dp_c[i] = dp_c[j]

            elif dp_l[j] + 1 == dp_l[i]:
                dp_c[i] += dp_c[j]

    # Store the maximum element from dp_l
    max_length = max(x for x in dp_l)

    # Stores the count of LIS
    count = 0

    # Traverse dp_l and dp_c simultaneously
    for l, c in zip(dp_l, dp_c):

        # Update the count
        if l == max_length:
            count += c

    # Return the count of LIS
    return count

# Driver Code

# Given array arr[]
arr = [1, 3, 5, 4, 7]

# Function Call
print(findNumberOfLIS(arr))
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to count the number
    // of LIS in the array nums[]
    static int findNumberOfLIS(int[] nums)
    {

      // Base Case
      if (nums.Length == 0)
          return 0;

      int n = nums.Length;

      // Initialize dp_l array with
      // 1s
      int[] dp_l = new int[n];
      Array.Fill(dp_l, 1);

      // Initialize dp_c array with
      // 1s
      int[] dp_c = new int[n];
      Array.Fill(dp_c, 1);

      for(int i = 0; i < n; i++)
      {
        for(int j = 0; j < i; j++)
        {

          // If current element is
          // smaller
          if (nums[i] <= nums[j])
            continue;

          if (dp_l[j] + 1 > dp_l[i])
          {
            dp_l[i] = dp_l[j] + 1;
            dp_c[i] = dp_c[j];
          }
          else if (dp_l[j] + 1 == dp_l[i])
            dp_c[i] += dp_c[j];
        }
      }

      // Store the maximum element
      // from dp_l
      int max_length = 0;

      foreach(int i in dp_l)
        max_length = Math.Max(i, max_length);

      // Stores the count of LIS
      int count = 0;

      // Traverse dp_l and dp_c
      // simultaneously
      for(int i = 0; i < n; i++)
      {

        // Update the count
        if (dp_l[i] == max_length)
          count += dp_c[i];
      }

      // Return the count of LIS
      return count;
    }

  // Driver code
  static void Main() {

      // Given array arr[]
      int[] arr = { 1, 3, 5, 4, 7 };

      // Function Call
      Console.WriteLine(findNumberOfLIS(arr));
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the
// above approach

// Function to count the number
// of LIS in the array nums[]
function findNumberOfLIS(nums)
{
  //Base Case
  if (nums.length == 0)
    return 0;

  var n = nums.length;

  // Initialize dp_l array with
  // 1s
  var dp_l = Array(n).fill(1);

  // Initialize dp_c array with
  // 1s
  var dp_c = Array(n).fill(1);

  for (var i = 0; i < n; i++)
  {
    for (var j = 0; j < i; j++)
    {
      // If current element is
      // smaller
      if (nums[i] <= nums[j])
        continue;

      if  (dp_l[j] + 1 > dp_l[i])
      {
        dp_l[i] = dp_l[j] + 1;
        dp_c[i] = dp_c[j];
      }
      else if (dp_l[j] + 1 == dp_l[i])
        dp_c[i] += dp_c[j];
    }
  }

  // Store the maximum element
  // from dp_l
  var max_length = 0;

  dp_l.forEach(i => {

    max_length = Math.max(i,max_length);
  });

  // Stores the count of LIS
  var count = 0;

  //Traverse dp_l and dp_c
  // simultaneously
  for(var i = 0; i < n; i++)
  {
    // Update the count
    if (dp_l[i] == max_length)
      count += dp_c[i];
  }

  // Return the count of LIS
  return count;
}

// Driver code
// Given array arr[]
var arr = [1, 3, 5, 4, 7];

// Function Call
document.write( findNumberOfLIS(arr));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*