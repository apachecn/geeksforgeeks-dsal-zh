# 将阵列分成两个子阵列，使它们的和之差最小

> 原文:[https://www . geeksforgeeks . org/将数组拆分为两个子数组，这样它们的和之差就是最小值/](https://www.geeksforgeeks.org/split-array-into-two-subarrays-such-that-difference-of-their-sum-is-minimum/)

给定一个整数[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是将给定的阵列分成两个[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得它们之和的差值最小。

**示例:**

> **输入:** arr[] = {7，9，5，10}
> **输出:** 1
> **解释:**子阵{7，9}和{5，10}之和的差等于[16–15]= 1，这是最小可能。
> 
> **输入:** arr[] = {6，6，6}
> 输出 : 6

**天真方法:**思路是使用[前缀后缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)数组技术。生成给定数组的前缀和数组以及后缀和数组。现在，对数组中的任何索引**I**(0<= I<= N–1)迭代数组并打印 ***前缀 _sum[i]*** 和 ***后缀 _sum[i+1]*** 之间的最小差异。
***时间复杂度:** O(N)*
***辅助空间:** O(N)*

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return minimum difference
// between two subarray sums
int minDiffSubArray(int arr[], int n)
{

    // To store prefix sums
    int prefix_sum[n];

    // Generate prefix sum array
    prefix_sum[0] = arr[0];

    for(int i = 1; i < n; i++)
        prefix_sum[i] = prefix_sum[i - 1] +
                               arr[i];

    // To store suffix sums
    int suffix_sum[n];

    // Generate suffix sum array
    suffix_sum[n - 1] = arr[n - 1];

    for(int i = n - 2; i >= 0; i--)
        suffix_sum[i] = suffix_sum[i + 1] +
                               arr[i];

    // Stores the minimum difference
    int minDiff = INT_MAX;

    // Traverse the given array
    for(int i = 0; i < n - 1; i++)
    {

        // Calculate the difference
        int diff = abs(prefix_sum[i] -
                       suffix_sum[i + 1]);

        // Update minDiff
        if (diff < minDiff)
            minDiff = diff;
    }

    // Return minDiff
    return minDiff;
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 7, 9, 5, 10 };

    // Length of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minDiffSubArray(arr, n);
}

// This code is contributed by code_hunt
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
import java.util.*;
import java.lang.*;

class GFG {

    // Function to return minimum difference
    // between two subarray sums
    static int minDiffSubArray(int arr[], int n)
    {

        // To store prefix sums
        int[] prefix_sum = new int[n];

        // Generate prefix sum array
        prefix_sum[0] = arr[0];

        for (int i = 1; i < n; i++)
            prefix_sum[i]
                = prefix_sum[i - 1] + arr[i];

        // To store suffix sums
        int[] suffix_sum = new int[n];

        // Generate suffix sum array
        suffix_sum[n - 1] = arr[n - 1];

        for (int i = n - 2; i >= 0; i--)
            suffix_sum[i]
                = suffix_sum[i + 1] + arr[i];

        // Stores the minimum difference
        int minDiff = Integer.MAX_VALUE;

        // Traverse the given array
        for (int i = 0; i < n - 1; i++) {

            // Calculate the difference
            int diff
                = Math.abs(prefix_sum[i]
                           - suffix_sum[i + 1]);

            // Update minDiff
            if (diff < minDiff)
                minDiff = diff;
        }

        // Return minDiff
        return minDiff;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int[] arr = { 7, 9, 5, 10 };

        // Length of the array
        int n = arr.length;

        System.out.println(
            minDiffSubArray(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to return minimum difference
# between two subarray sums
def minDiffSubArray(arr, n):

    # To store prefix sums
    prefix_sum = [0] * n

    # Generate prefix sum array
    prefix_sum[0] = arr[0]

    for i in range(1, n):
        prefix_sum[i] = (prefix_sum[i - 1] +
                                arr[i])

    # To store suffix sums
    suffix_sum = [0] * n

    # Generate suffix sum array
    suffix_sum[n - 1] = arr[n - 1]

    for i in range(n - 2, -1, -1):
        suffix_sum[i] = (suffix_sum[i + 1] +
                                arr[i])

    # Stores the minimum difference
    minDiff = sys.maxsize

    # Traverse the given array
    for i in range(n - 1):

        # Calculate the difference
        diff = abs(prefix_sum[i] -
                   suffix_sum[i + 1])

        # Update minDiff
        if (diff < minDiff):
            minDiff = diff

    # Return minDiff
    return minDiff

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 7, 9, 5, 10 ]

    # Length of the array
    n = len(arr)

    print(minDiffSubArray(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to return minimum difference
// between two subarray sums
static int minDiffSubArray(int []arr,
                           int n)
{   
  // To store prefix sums
  int[] prefix_sum = new int[n];

  // Generate prefix sum array
  prefix_sum[0] = arr[0];

  for(int i = 1; i < n; i++)
    prefix_sum[i] = prefix_sum[i - 1] +
                    arr[i];

  // To store suffix sums
  int[] suffix_sum = new int[n];

  // Generate suffix sum array
  suffix_sum[n - 1] = arr[n - 1];

  for(int i = n - 2; i >= 0; i--)
    suffix_sum[i] = suffix_sum[i + 1] +
                    arr[i];

  // Stores the minimum difference
  int minDiff = int.MaxValue;

  // Traverse the given array
  for(int i = 0; i < n - 1; i++)
  {
    // Calculate the difference
    int diff = Math.Abs(prefix_sum[i] -
                        suffix_sum[i + 1]);

    // Update minDiff
    if (diff < minDiff)
      minDiff = diff;
    }

    // Return minDiff
    return minDiff;
}

// Driver Code
public static void Main(String[] args)
{   
    // Given array
    int[] arr = {7, 9, 5, 10};

    // Length of the array
    int n = arr.Length;

    Console.WriteLine(minDiffSubArray(arr, n));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to return minimum difference
    // between two subarray sums
    function minDiffSubArray(arr, n)
    {  
      // To store prefix sums
      let prefix_sum = new Array(n);

      // Generate prefix sum array
      prefix_sum[0] = arr[0];

      for(let i = 1; i < n; i++)
        prefix_sum[i] = prefix_sum[i - 1] + arr[i];

      // To store suffix sums
      let suffix_sum = new Array(n);

      // Generate suffix sum array
      suffix_sum[n - 1] = arr[n - 1];

      for(let i = n - 2; i >= 0; i--)
        suffix_sum[i] = suffix_sum[i + 1] + arr[i];

      // Stores the minimum difference
      let minDiff = Number.MAX_VALUE;

      // Traverse the given array
      for(let i = 0; i < n - 1; i++)
      {
        // Calculate the difference
        let diff = Math.abs(prefix_sum[i] - suffix_sum[i + 1]);

        // Update minDiff
        if (diff < minDiff)
          minDiff = diff;
        }

        // Return minDiff
        return minDiff;
    }

    // Given array
    let arr = [7, 9, 5, 10];

    // Length of the array
    let n = arr.length;

    document.write(minDiffSubArray(arr, n));

// This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
1
```

**高效方法:**优化上述方法的思路是计算数组元素的总和。现在，迭代数组并计算数组的前缀和，并为数组的任何索引找到前缀和之间的最小差以及总和和前缀和之间的差，即，

> 子阵列总和之间的最大差值=(前缀 _ 总和–(total _ sum–prefix _ sum))

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return minimum difference
// between sum of two subarrays
int minDiffSubArray(int arr[], int n)
{

    // To store total sum of array
    int total_sum = 0;

    // Calculate the total sum
    // of the array
    for(int i = 0; i < n; i++)
        total_sum += arr[i];

    // Stores the prefix sum
    int prefix_sum = 0;

    // Stores the minimum difference
    int minDiff = INT_MAX;

    // Traverse the given array
    for(int i = 0; i < n - 1; i++)
    {
        prefix_sum += arr[i];

        // To store minimum difference
        int diff = abs((total_sum -
                       prefix_sum) -
                       prefix_sum);

        // Update minDiff
        if (diff < minDiff)
            minDiff = diff;
    }

    // Return minDiff
    return minDiff;
}

// Driver code
int main()
{

    // Given array
    int arr[] = { 7, 9, 5, 10 };

    // Length of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minDiffSubArray(arr, n) << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
import java.util.*;
import java.lang.*;

class GFG {

    // Function to return minimum difference
    // between sum of two subarrays
    static int minDiffSubArray(int arr[], int n)
    {
        // To store total sum of array
        int total_sum = 0;

        // Calculate the total sum
        // of the array
        for (int i = 0; i < n; i++)
            total_sum += arr[i];

        // Stores the prefix sum
        int prefix_sum = 0;

        // Stores the minimum difference
        int minDiff = Integer.MAX_VALUE;

        // Traverse the given array
        for (int i = 0; i < n - 1; i++) {

            prefix_sum += arr[i];

            // To store minimum difference
            int diff
                = Math.abs((total_sum
                            - prefix_sum)
                           - prefix_sum);

            // Update minDiff
            if (diff < minDiff)
                minDiff = diff;
        }

        // Return minDiff
        return minDiff;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int[] arr = { 7, 9, 5, 10 };

        // Length of the array
        int n = arr.length;

        System.out.println(
            minDiffSubArray(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to return minimum difference
# between sum of two subarrays
def minDiffSubArray(arr, n):

    # To store total sum of array
    total_sum = 0

    # Calculate the total sum
    # of the array
    for i in range(n):
        total_sum += arr[i]

    # Stores the prefix sum
    prefix_sum = 0

    # Stores the minimum difference
    minDiff = sys.maxsize

    # Traverse the given array
    for i in range(n - 1):
        prefix_sum += arr[i]

        # To store minimum difference
        diff = abs((total_sum -
                   prefix_sum) -
                   prefix_sum)

        # Update minDiff
        if (diff < minDiff):
            minDiff = diff

    # Return minDiff
    return minDiff

# Driver code

# Given array
arr = [ 7, 9, 5, 10 ]

# Length of the array
n = len(arr)

print(minDiffSubArray(arr, n))

# This code is contributed by code_hunt
```

## C#

```
// C# Program for above approach
using System;
class GFG{

// Function to return minimum difference
// between sum of two subarrays
static int minDiffSubArray(int []arr,
                           int n)
{
  // To store total sum of array
  int total_sum = 0;

  // Calculate the total sum
  // of the array
  for (int i = 0; i < n; i++)
    total_sum += arr[i];

  // Stores the prefix sum
  int prefix_sum = 0;

  // Stores the minimum difference
  int minDiff = int.MaxValue;

  // Traverse the given array
  for (int i = 0; i < n - 1; i++)
  {
    prefix_sum += arr[i];

    // To store minimum difference
    int diff = Math.Abs((total_sum -
                         prefix_sum) -
                         prefix_sum);

    // Update minDiff
    if (diff < minDiff)
      minDiff = diff;
  }

  // Return minDiff
  return minDiff;
}

// Driver Code
public static void Main(String[] args)
{
  // Given array
  int[] arr = {7, 9, 5, 10};

  // Length of the array
  int n = arr.Length;

  Console.WriteLine(
          minDiffSubArray(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for above approach

// Function to return minimum difference
// between sum of two subarrays
function minDiffSubArray(arr, n)
{

    // To store total sum of array
    var total_sum = 0;

    // Calculate the total sum
    // of the array
    for(var i = 0; i < n; i++)
        total_sum += arr[i];

    // Stores the prefix sum
    var prefix_sum = 0;

    // Stores the minimum difference
    var minDiff = 1000000000;

    // Traverse the given array
    for(var i = 0; i < n - 1; i++)
    {
        prefix_sum += arr[i];

        // To store minimum difference
        var diff = Math.abs((total_sum -
                       prefix_sum) -
                       prefix_sum);

        // Update minDiff
        if (diff < minDiff)
            minDiff = diff;
    }

    // Return minDiff
    return minDiff;
}

// Driver code
// Given array
var arr = [7, 9, 5, 10];

// Length of the array
var n = arr.length;
document.write( minDiffSubArray(arr, n));

// This code is contributed by importantly.
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)