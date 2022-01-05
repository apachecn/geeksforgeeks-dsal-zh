# 从给定数组中找到最大交替子序列和

> 原文:[https://www . geesforgeks . org/find-the-max-alternate-subsequence-sum-from-a-给定数组/](https://www.geeksforgeeks.org/find-the-maximum-alternate-subsequence-sum-from-a-given-array/)

给定大小为 n 的**数组 arr[]** ，该数组具有除零之外的正整数和负整数。求给定序列的最大大小交替子序列的最大和，也就是说，在子序列中，每个相邻元素的符号是相反的，例如，如果第一个元素是正的，那么第二个元素必须是负的，然后是另一个正整数，以此类推。

**示例:**

> **输入:** arr[] = {1，2，3，4，-1，-2}
> **输出:** 3
> **解释:**
> 这里，最大大小的子序列是[1，-1] [1，-2] [2，-1] [2，-2] [3，-1]【T9]【3，-2] [4，-1] [4，-2]，但是具有最大和的子序列是[4，-1]
> ，这个子序列的和是 3。因此，输出为 3。
> 
> **输入:** arr[] = {-1，-6，12，-4，-5}
> **输出:** 7
> **解释:**
> 这里，最大尺寸子序列是[-1，12，-4] [-1，12，-5] [-6，-12，-4]
> [-6，12，-5]但是具有最大和的子序列是[-1，12，-4]
> 因此，输出为 7。

**天真方法:**
解决上述问题的简单方法是找到所有交替的子序列及其和，并返回其中的最大和。

**高效法:**
解决上述问题的高效法是每次从连续的正元素和连续的负元素中挑出最大的元素，加到目前为止的最大和上。存储最大和的变量将保存最终答案。

以下是上述方法的实施情况:

## C++14

```
// C++ program to find the maximum
// alternating subsequence sum for
// a given array
#include <iostream>
using namespace std;

// Function to find maximum
// alternating subsequence sum
int maxAlternatingSum(int arr[], int n)
{

    // Initialize sum to 0
    int max_sum = 0;
    int i = 0;

    while (i < n)
    {
        int current_max = arr[i];
        int k = i;

         while (k < n &&
              ((arr[i] > 0 && arr[k] > 0) ||
               (arr[i] < 0 && arr[k] < 0)))
        {
            current_max = max(current_max, arr[k]);
            k += 1;
        }

        // Calculate the sum
        max_sum += current_max;

        i = k;
    }

    // Return the final result
    return max_sum;   
}

// Driver Code
int main()
{

    // Array initialization
    int arr[] = { 1, 2, 3, 4, -1, -2 };

    // Length of array
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxAlternatingSum(arr, n);
    return 0;
}

// This code is contributed by avanitrachhadiya2155
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// alternating subsequence sum for
// a given array
import java.io.*;
import java.util.*;

class GFG{

// Function to find maximum
// alternating subsequence sum
static int maxAlternatingSum(int[] arr, int n)
{

    // Initialize sum to 0
    int max_sum = 0;

    int i = 0;

    while (i < n)
    {
        int current_max = arr[i];
        int k = i;

         while (k < n &&
              ((arr[i] > 0 && arr[k] > 0) ||
               (arr[i] < 0 && arr[k] < 0)))
         {
            current_max = Math.max(current_max, arr[k]);
            k += 1;
        }

        // Calculate the sum
        max_sum += current_max;

        i = k;
    }

    // Return the final result
    return max_sum;
}

// Driver Code
public static void main(String args[])
{

    // Array initialization
    int[] arr = { 1, 2, 3, 4, -1, -2 };

    // Length of array
    int n = arr.length;

    System.out.println(maxAlternatingSum(arr, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the maximum alternating
# subsequence sum for a given array

# Function to find maximum
# alternating subsequence sum
def maxAlternatingSum(arr, n):

    # initialize sum to 0
    max_sum = 0

    i = 0

    while i<n:
        current_max = arr[i]
        k = i

        while k<n and ((arr[i]>0 and arr[k]>0)
        or (arr[i]<0 and arr[k]<0)):

            current_max = max(current_max, arr[k])

            k+= 1

        # calculate the sum
        max_sum+= current_max

        i = k

    # return the final result
    return max_sum

# Driver code

# array initiaisation
arr = [1, 2, 3, 4, -1, -2]

# length of array
n = len(arr)

print(maxAlternatingSum(arr, n))
```

## C#

```
// C# program to find the maximum
// alternating subsequence sum for
// a given array
using System;
class GFG{

// Function to find maximum
// alternating subsequence sum
static int maxAlternatingSum(int[] arr,
                             int n)
{
  // Initialize sum to 0
  int max_sum = 0;

  int i = 0;

  while (i < n)
  {
    int current_max = arr[i];
    int k = i;

    while (k < n &&
          ((arr[i] > 0 && arr[k] > 0) ||
           (arr[i] < 0 && arr[k] < 0)))
    {
      current_max = Math.Max(current_max,
                             arr[k]);
      k += 1;
    }

    // Calculate the sum
    max_sum += current_max;

    i = k;
  }

  // Return the final result
  return max_sum;
}

// Driver Code
public static void Main()
{    
  // Array initialization
  int[] arr = {1, 2, 3, 4,
               -1, -2};

  // Length of array
  int n = arr.Length;

  Console.Write(maxAlternatingSum(arr, n));
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
// JS program to find the maximum
// alternating subsequence sum for
// a given array

// Function to find maximum
// alternating subsequence sum
function maxAlternatingSum( arr, n)
{

    // Initialize sum to 0
    var max_sum = 0;

    var i = 0;

    while (i < n)
    {
        var current_max = arr[i];
        var k = i;

        while (k < n &&
            ((arr[i] > 0 && arr[k] > 0) ||
            (arr[i] < 0 && arr[k] < 0)))
        {
            current_max = Math.max(current_max, arr[k]);
            k += 1;
        }

        // Calculate the sum
        max_sum += current_max;

        i = k;
    }

    // Return the final result
    return max_sum;
}

// Driver Code

    // Array initialization
    var arr = [ 1, 2, 3, 4, -1, -2 ];

    // Length of array
    var n = arr.length;

    document.write(maxAlternatingSum(arr, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n)