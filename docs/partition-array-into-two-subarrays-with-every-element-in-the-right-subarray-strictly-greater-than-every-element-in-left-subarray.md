# 将阵列划分为两个子阵列，右子阵列中的每个元素严格大于左子阵列中的每个元素

> 原文:[https://www . geesforgeks . org/partition-array-分成两个子阵列-右子阵列中的每个元素-严格大于左子阵列中的每个元素/](https://www.geeksforgeeks.org/partition-array-into-two-subarrays-with-every-element-in-the-right-subarray-strictly-greater-than-every-element-in-left-subarray/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是将该数组划分为两个非空的[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，使得右子数组中的每个元素严格大于左子数组中的每个元素。如果可以，则打印两个结果[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。否则，打印**“不可能”。**

**示例:**

> **输入:** arr[] = {5，3，2，7，9}
> **输出:**
> 5 3 2
> 7 9
> **解释:**
> 可能的分区之一是{5，3，2}和{7，9}。
> 第二个<sup>子阵列{7}的最小值大于第一个子阵列(5)的最大值。</sup>
> 
> **输入:** arr[] = {1，1，1，1，1}
> **输出:**不可能
> **说明:**
> 这个数组没有分区可能。

**天真方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个索引，检查第一个子数组的最大值是否小于第二个子数组的最小值。如果发现是真的，那么打印两个子阵列。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间** : O(N)*

**高效方法:**上述方法可以通过计算**前缀最大数组**和**后缀最小数组**来优化，这导致第一个子数组的最大值和 2 个<sup>和</sup>子数组的最小值的时间计算是恒定的。按照以下步骤解决问题:

*   初始化一个[数组，](https://www.geeksforgeeks.org/array-data-structure/)说 **min[，**存储**最小后缀数组。**
*   初始化 3 个变量，比如 **ind** 、 **mini** 和 **maxi、**分别存储分区索引、后缀最小值和前缀最大值。
*   [反向遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将 **mini** 更新为 **mini = min (mini，arr[i])** 。将 **mini** 分配给**min【I】。**
*   现在，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并执行以下操作:
    *   更新**最大**为**最大=最大(最大，arr[i])。**
    *   如果 **i+1 < N** 以及**maxi<min【I+1】**，则打印索引 **i** 和[断开时制作的分区。](https://www.geeksforgeeks.org/break-statement-cc/)
*   完成以上步骤后，如果以上情况都不满足，则打印“**不可能”。**

以下是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to partition the array
// into two non-empty subarrays
// which satisfies the given condition
void partitionArray(int *a, int n)
{

  // Stores the suffix Min array
  int *Min = new int[n];

  // Stores the Minimum of a suffix
  int Mini = INT_MAX;

  // Traverse the array in reverse
  for (int i = n - 1; i >= 0; i--) {

    // Update Minimum
    Mini = min(Mini, a[i]);

    // Store the Minimum
    Min[i] = Mini;
  }

  // Stores the Maximum value of a prefix
  int Maxi = INT_MIN;

  // Stores the index of the partition
  int ind = -1;

  for (int i = 0; i < n - 1; i++) {

    // Update Max
    Maxi = max(Maxi, a[i]);

    // If Max is less than Min[i+1]
    if (Maxi < Min[i + 1]) {

      // Store the index
      // of partition
      ind = i;

      // break
      break;
    }
  }

  // If ind is not -1
  if (ind != -1) {

    // Print the first subarray
    for (int i = 0; i <= ind; i++)
      cout << a[i] << " ";

    cout << endl;

    // Print the second subarray
    for (int i = ind + 1; i < n; i++)
      cout << a[i] << " ";
  }

  // Otherwise
  else
    cout << "Impossible";
}

// Driver Code
int main()
{
  int arr[] = { 5, 3, 2, 7, 9 };
  int N = 5;
  partitionArray(arr, N);
  return 0;
}

// This code is contributed by Shubhamsingh10
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach

import java.util.*;

class GFG {

    // Function to partition the array
    // into two non-empty subarrays
    // which satisfies the given condition
    static void partitionArray(int a[], int n)
    {
        // Stores the suffix min array
        int min[] = new int[n];

        // Stores the minimum of a suffix
        int mini = Integer.MAX_VALUE;

        // Traverse the array in reverse
        for (int i = n - 1; i >= 0; i--) {

            // Update minimum
            mini = Math.min(mini, a[i]);

            // Store the minimum
            min[i] = mini;
        }

        // Stores the maximum value of a prefix
        int maxi = Integer.MIN_VALUE;

        // Stores the index of the partition
        int ind = -1;

        for (int i = 0; i < n - 1; i++) {

            // Update max
            maxi = Math.max(maxi, a[i]);

            // If max is less than min[i+1]
            if (maxi < min[i + 1]) {

                // Store the index
                // of partition
                ind = i;

                // break
                break;
            }
        }

        // If ind is not -1
        if (ind != -1) {

            // Print the first subarray
            for (int i = 0; i <= ind; i++)
                System.out.print(a[i] + " ");

            System.out.println();

            // Print the second subarray
            for (int i = ind + 1; i < n; i++)
                System.out.print(a[i] + " ");
        }

        // Otherwise
        else
            System.out.println("Impossible");
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 5, 3, 2, 7, 9 };
        int N = arr.length;
        partitionArray(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to partition the array
# into two non-empty subarrays
# which satisfies the given condition
def partitionArray(a, n) :

  # Stores the suffix Min array
  Min = [0] * n

  # Stores the Minimum of a suffix
  Mini = sys.maxsize

  # Traverse the array in reverse
  for i in range(n - 1, -1, -1):

    # Update Minimum
    Mini = min(Mini, a[i])

    # Store the Minimum
    Min[i] = Mini

  # Stores the Maximum value of a prefix
  Maxi = -sys.maxsize - 1

  # Stores the index of the partition
  ind = -1
  for i in range(n - 1):

    # Update Max
    Maxi = max(Maxi, a[i])

    # If Max is less than Min[i+1]
    if (Maxi < Min[i + 1]) :

      # Store the index
      # of partition
      ind = i

      # break
      break

  # If ind is not -1
  if (ind != -1) :

    # Print first subarray
    for i in range(ind + 1):
      print(a[i], end = " ")
    print()

    # Print second subarray
    for i in range(ind + 1 , n , 1):
      print(a[i], end = " ")

  # Otherwise
  else :
    print("Impossible")

# Driver Code
arr = [ 5, 3, 2, 7, 9 ]
N = 5
partitionArray(arr, N)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program of the above approach
using System;

class GFG {

  // Function to partition the array
  // into two non-empty subarrays
  // which satisfies the given condition
  static void partitionArray(int[] a, int n)
  {
    // Stores the suffix min array
    int[] min = new int[n];

    // Stores the minimum of a suffix
    int mini = Int32.MaxValue;

    // Traverse the array in reverse
    for (int i = n - 1; i >= 0; i--) {

      // Update minimum
      mini = Math.Min(mini, a[i]);

      // Store the minimum
      min[i] = mini;
    }

    // Stores the maximum value of a prefix
    int maxi = Int32.MinValue;

    // Stores the index of the partition
    int ind = -1;

    for (int i = 0; i < n - 1; i++) {

      // Update max
      maxi = Math.Max(maxi, a[i]);

      // If max is less than min[i+1]
      if (maxi < min[i + 1]) {

        // Store the index
        // of partition
        ind = i;

        // break
        break;
      }
    }

    // If ind is not -1
    if (ind != -1) {

      // Print the first subarray
      for (int i = 0; i <= ind; i++)
        Console.Write(a[i] + " ");

      Console.WriteLine();

      // Print the second subarray
      for (int i = ind + 1; i < n; i++)
        Console.Write(a[i] + " ");
    }

    // Otherwise
    else
      Console.Write("Impossible");
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[] arr = { 5, 3, 2, 7, 9 };
    int N = arr.Length;
    partitionArray(arr, N);
  }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// javascript program of the above approach   

// Function to partition the array
// into two non-empty subarrays
// which satisfies the given condition
    function partitionArray(a , n)
    {
        // Stores the suffix min array
        var min = Array(n).fill(0);

        // Stores the minimum of a suffix
        var mini = Number.MAX_VALUE;

        // Traverse the array in reverse
        for (i = n - 1; i >= 0; i--) {

            // Update minimum
            mini = Math.min(mini, a[i]);

            // Store the minimum
            min[i] = mini;
        }

        // Stores the maximum value of a prefix
        var maxi = Number.MIN_VALUE;

        // Stores the index of the partition
        var ind = -1;

        for (i = 0; i < n - 1; i++) {

            // Update max
            maxi = Math.max(maxi, a[i]);

            // If max is less than min[i+1]
            if (maxi < min[i + 1]) {

                // Store the index
                // of partition
                ind = i;

                // break
                break;
            }
        }

        // If ind is not -1
        if (ind != -1) {

            // Print the first subarray
            for (i = 0; i <= ind; i++)
                document.write(a[i] + " ");

            document.write("<br/>");

            // Print the second subarray
            for (i = ind + 1; i < n; i++)
                document.write(a[i] + " ");
        }

        // Otherwise
        else
            document.write("Impossible");
    }

    // Driver Code

        var arr = [ 5, 3, 2, 7, 9 ];
        var N = arr.length;
        partitionArray(arr, N);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
5 3 2 
7 9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)