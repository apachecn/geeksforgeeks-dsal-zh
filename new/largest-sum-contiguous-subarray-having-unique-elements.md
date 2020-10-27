# 具有唯一元素的最大总和连续子数组

给定 **N** 个正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，任务是在所有具有唯一元素的子数组中找到具有最大和的子数组并打印其和。

> **输入** arr [] = {1、2、3、3、4、5、2、1}
> **输出：** 15
> **说明：[HTG7
> 具有最大和且具有不同元素的子数组是{3，4，5，2，1，1}。
> 因此，总和为= 3 + 4 + 5 + 2 + 1 = 15**
> 
> **输入：** arr [] = {1,2,3,1,5}
> **输出：** 11
> **说明：**
> 具有最大和且具有不同元素的子数组为{2，3，1，5}。
> 因此，总和为= 2 + 3 + 1 + 5 = 11。

**天真的方法：**解决该问题的最简单方法是[生成所有可能的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并为每个子数组检查其所有元素是否唯一。 在这些子数组中找到最大和并打印出来。
***时间复杂度：** O（N <sup>3</sup> ）*
***辅助空间：** O（N）*

**高效方法：**要优化上述方法，其思想是使用[两指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)。 请按照以下步骤解决该方法：

1.  将两个指针 **i** 和 **j** 分别初始化为 **0** 和 **1** ，以存储所得子数组的开始和结束索引。
2.  初始化 [**HashSet**](http://www.geeksforgeeks.org/hashset-in-java/) 以存储数组元素。
3.  从一个空子数组开始，其中 **i = 0** 和 **j = 0** 和[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，直到找到任何重复的元素，并将当前和更新为最大和 （例如说 **max_sum** ）是否大于当前的 **max_sum** 。
4.  如果找到重复元素，则递增 **j** 并更新变量，直到在当前子数组中仅剩下唯一元素为止，它们从索引 **j** 到 **i** 。
5.  对其余数组重复上述步骤，并继续更新 **max_sum** 。
6.  完成上述步骤后，打印获得的最大金额。

下面是上述方法的实现：

## C++

```cpp

// C++ program for 
// the above approach 
#include<bits/stdc++.h>
using namespace std;

// Function to calculate required
// maximum subarray sum
int maxSumSubarray(int arr[], int n)
{
  // Initialize two pointers
  int i = 0, j = 1;
  // Stores the unique elements
  set<int> set;

  // Insert the first element
  set.insert(arr[0]);

  // Current max sum
  int sum = arr[0];

  // Global maximum sum
  int maxsum = sum;

  while (i < n - 1 && j < n) 
  {
    // Update sum & increment j
    // auto pos = s.find(3); 
    const bool is_in = set.find(arr[j]) != 
                       set.end();
    if (!is_in) 
    {
      sum = sum + arr[j];
      maxsum = max(sum, maxsum);

      // Add the current element
      set.insert(arr[j++]);
    }

    // Update sum and increment i
    // and remove arr[i] from set
    else
    {
      sum -= arr[i];

      // Remove the element
      // from start position
      set.erase(arr[i++]);
    }
  }

  // Return the maximum sum
  return maxsum;
}

// Driver Code
int  main()
{
  // Given array arr[]
  int arr[] = {1, 2, 3, 1, 5};

  // Function Call
  int ans = maxSumSubarray(arr, 5);

  // Print the maximum sum
  cout << (ans);
}

// This code is contributed by gauravrajput1

```

## Java

```java

// Java program for the above approach

import java.io.*;
import java.lang.Math;
import java.util.*;
public class GFG {

    // Function to calculate required
    // maximum subarray sum
    public static int
    maxSumSubarray(int[] arr)
    {

        // Initialize two pointers
        int i = 0, j = 1;

        // Stores the unique elements
        HashSet<Integer> set
            = new HashSet<Integer>();

        // Insert the first element
        set.add(arr[0]);

        // Current max sum
        int sum = arr[0];

        // Global maximum sum
        int maxsum = sum;

        while (i < arr.length - 1
               && j < arr.length) {

            // Update sum & increment j
            if (!set.contains(arr[j])) {

                sum = sum + arr[j];
                maxsum = Math.max(sum,
                                  maxsum);

                // Add the current element
                set.add(arr[j++]);
            }

            // Update sum and increment i
            // and remove arr[i] from set
            else {

                sum -= arr[i];

                // Remove the element
                // from start position
                set.remove(arr[i++]);
            }
        }

        // Return the maximum sum
        return maxsum;
    }

    // Driver Code
    public static void
        main(String[] args)
    {
        // Given array arr[]
        int arr[] = new int[] { 1, 2, 3, 1, 5 };

        // Function Call
        int ans = maxSumSubarray(arr);

        // Print the maximum sum
        System.out.println(ans);
    }
}

```

## Python3

```py

# Python3 program for the above approach

# Function to calculate required
# maximum subarray sum
def maxSumSubarray(arr):

    # Initialize two pointers
    i = 0
    j = 1

    # Stores the unique elements
    set = {}

    # Insert the first element
    set[arr[0]] = 1

    # Current max sum
    sum = arr[0]

    # Global maximum sum
    maxsum = sum

    while (i < len(arr) - 1 and
           j < len(arr)):

        # Update sum & increment j
        if arr[j] not in set:
            sum = sum + arr[j]
            maxsum = max(sum, maxsum)

            # Add the current element
            set[arr[j]] = 1
            j += 1

        # Update sum and increment i
        # and remove arr[i] from set
        else:
            sum -= arr[i]

            # Remove the element
            # from start position
            del set[arr[i]]
            i += 1

    # Return the maximum sum
    return maxsum

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 2, 3, 1, 5 ]

    # Function call
    ans = maxSumSubarray(arr)

    # Print the maximum sum
    print(ans)

# This code is contributed by mohit kumar 29

```

## C#

```cs

// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

  // Function to calculate 
  // required maximum subarray sum
  public static int maxSumSubarray(int[] arr)
  {
    // Initialize two pointers
    int i = 0, j = 1;

    // Stores the unique elements
    HashSet<int> set = 
            new HashSet<int>();

    // Insert the first element
    set.Add(arr[0]);

    // Current max sum
    int sum = arr[0];

    // Global maximum sum
    int maxsum = sum;

    while (i < arr.Length - 1 && 
           j < arr.Length) 
    {
      // Update sum & increment j
      if (!set.Contains(arr[j])) 
      {
        sum = sum + arr[j];
        maxsum = Math.Max(sum,
                          maxsum);

        // Add the current element
        set.Add(arr[j++]);
      }

      // Update sum and increment i
      // and remove arr[i] from set
      else
      {
        sum -= arr[i];

        // Remove the element
        // from start position
        set.Remove(arr[i++]);
      }
    }

    // Return the maximum sum
    return maxsum;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    // Given array []arr
    int []arr = new int[] {1, 2, 
                           3, 1, 5};

    // Function Call
    int ans = maxSumSubarray(arr);

    // Print the maximum sum
    Console.WriteLine(ans);
  }
}

// This code is contributed by shikhasingrajput

```

**Output:** 

```
11

```

***时间复杂度：** O（N）*
***辅助空间：** O（N）*



* * *

* * *



