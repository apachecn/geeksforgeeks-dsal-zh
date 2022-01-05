# 仅由偶数或奇数组成的最长子阵列中的最大元素

> 原文:[https://www . geeksforgeeks . org/最长子数组中最大元素仅由偶数或奇数组成/](https://www.geeksforgeeks.org/largest-element-in-the-longest-subarray-consisting-of-only-even-or-only-odd-numbers/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是在最长的[子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)中找到最大的[元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)，该子阵列仅由[偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)或[奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)组成。

**示例:**

> **输入:** arr[] = { 2，4，6，9，10，11 }
> **输出:** 6
> **解释:**
> 仅由偶数或奇数组成的最长子阵是{ arr[0]，arr[1]，arr[2] }。
> 由于子阵最大的元素是 arr[2]，所以需要的输出是 6。
> 
> **输入:** arr[] = { 3，5，7，4，9，11，13 }
> **输出:** 13
> **解释:**
> 仅由偶数或奇数组成的最长子阵列为{ {3，5，7 }，{ 9，11，13 } }。
> 子阵中最大的元素分别为 7 个和 13 个。13 是最大的，是所需的输出。

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如 **maxLen** ，来存储最长的[子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的长度，直到 **i <sup>th</sup>** 索引，它只包含[偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)或者[奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。
*   初始化一个变量，比如 **Len** ，将当前子阵列的长度存储到第 **i <sup>第</sup>T5】个数组元素，只包含偶数或奇数。**
*   初始化一个变量，比如 **MaxElem** ，来存储最长子阵列的[最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)，直到 **i <sup>第</sup>** 个仅由偶数或奇数元素组成的索引。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。对于每个 **i <sup>第</sup>** 个数组元素，检查 **arr[i] % 2** 是否等于**arr[I–1]% 2**。如果发现为真，则增加 **Len** 的值。
*   否则，更新 **Len = 1** 的值。
*   如果 **Len > = maxLen** ，则更新 **MaxElem = max(MaxElem，arr[i])** 。
*   最后打印 **MaxElem** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <iostream>
using namespace std;

// Function to find the largest element
// of the longest subarray consisting
// only of odd or even elements only
int maxelementLongestSub(int arr[], int n)
{
    // Stores largest element of the
    // longest subarray till i-th index
    int MaxElem = arr[0];

    // Stores maximum length of the
    // longest subarray till i-th index
    int maxLen = 1;

    // Stores length of the current
    // subarray including the i-th element
    int Len = 1;

    // Stores largest element in
    // current subarray
    int Max = arr[0];

    // Traverse the array
    for (int i = 1; i < n; i++) {

        // If arr[i] and arr[i - 1]
        // are either even numbers
        // or odd numbers
        if (arr[i] % 2 == arr[i - 1] % 2) {

            // Update Len
            Len++;

            // Update Max
            if (arr[i] > Max)
                Max = arr[i];

            // If Len greater than
            // maxLen
            if (Len >= maxLen) {
                maxLen = Len;

                // Update MaxElem
                if (Max >= MaxElem)
                    MaxElem = Max;
            }
        }

        else {

            // Update Len
            Len = 1;

            // Update Max
            Max = arr[i];

            // If Len greater
            // than maxLen
            if (Len >= maxLen) {

                // Update maxLen
                maxLen = Len;

                // If Max greater
                // than MaxElem
                if (Max >= MaxElem) {

                    // Update MaxElem
                    MaxElem = Max;
                }
            }
        }
    }

    return MaxElem;
}

// Driver Code
int main()
{

    int arr[] = { 1, 3, 5, 7, 8, 12, 10 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxelementLongestSub(arr, n);

    return 0;
}
```

## C

```
// C program to implement
// the above approach
#include <stdio.h>

// Function to find the largest element
// of the longest subarray consisting
// only of odd or even elements only
int maxelementLongestSub(int arr[], int n)
{

    // Stores largest element of the
    // longest subarray till i-th index
    int MaxElem = arr[0];

    // Stores maximum length of the
    // longest subarray till i-th index
    int maxLen = 1;

    // Stores length of the current
    // subarray including the i-th element
    int Len = 1;

    // Stores largest element in
    // current subarray
    int Max = arr[0];

    // Traverse the array
    for(int i = 1; i < n; i++)
    {

        // If arr[i] and arr[i - 1]
        // are either even numbers
        // or odd numbers
        if (arr[i] % 2 == arr[i - 1] % 2)
        {

            // Update Len
            Len++;

            // Update Max
            if (arr[i] > Max)
                Max = arr[i];

            // If Len greater than
            // maxLen
            if (Len >= maxLen)
            {
                maxLen = Len;

                // Update MaxElem
                if (Max >= MaxElem)
                    MaxElem = Max;
            }
        }

        else
        {

            // Update Len
            Len = 1;

            // Update Max
            Max = arr[i];

            // If Len greater
            // than maxLen
            if (Len >= maxLen)
            {

                // Update maxLen
                maxLen = Len;

                // If Max greater
                // than MaxElem
                if (Max >= MaxElem)
                {

                    // Update MaxElem
                    MaxElem = Max;
                }
            }
        }
    }
    return MaxElem;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 5, 7, 8, 12, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("%d", maxelementLongestSub(arr, n));

    return 0;
}

// This code is contributed by sourav singh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to find the largest element
// of the longest subarray consisting
// only of odd or even elements only    
static int maxelementLongestSub(int arr[], int n)
{

    // Stores largest element of the
    // longest subarray till i-th index
    int MaxElem = arr[0];

    // Stores maximum length of the
    // longest subarray till i-th index
    int maxLen = 1;

    // Stores length of the current
    // subarray including the i-th element
    int Len = 1;

    // Stores largest element in
    // current subarray
    int Max = arr[0];

    // Traverse the array
    for(int i = 1; i < n; i++)
    {

        // If arr[i] and arr[i - 1]
        // are either even numbers
        // or odd numbers
        if (arr[i] % 2 == arr[i - 1] % 2)
        {

            // Update Len
            Len++;

            // Update Max
            if (arr[i] > Max)
                Max = arr[i];

            // If Len greater than
            // maxLen
            if (Len >= maxLen)
            {
                maxLen = Len;

                // Update MaxElem
                if (Max >= MaxElem)
                    MaxElem = Max;
            }
        }
        else
        {

            // Update Len
            Len = 1;

            // Update Max
            Max = arr[i];

            // If Len greater
            // than maxLen
            if (Len >= maxLen)
            {

                // Update maxLen
                maxLen = Len;

                // If Max greater
                // than MaxElem
                if (Max >= MaxElem)
                {

                    // Update MaxElem
                    MaxElem = Max;
                }
            }
        }
    }
    return MaxElem;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 3, 5, 7, 8, 12, 10 };
    int n = arr.length;

    System.out.print(maxelementLongestSub(arr, n));
}
}

// This code is contributed by sourav singh
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the largest element
# of the longest subarray consisting
# only of odd or even elements only
def maxelementLongestSub(arr, n):

    # Stores largest element of the
    # longest sub-array till i-th index
    MaxElem = arr[0]

    # Stores maximum length of the
    # longest sub-array till i-th index
    maxLen = 1

    # Stores length of the current
    # sub-array including the i-th element
    Len = 1

    # Stores largest element in
    # current sub-array
    Max = arr[0]

    for i in range(1, n):

        # If arr[i] and arr[i - 1]
        # are either even numbers
        # or odd numbers
        if arr[i] % 2 == arr[i - 1] % 2:

            # Update Len
            Len += 1

            # Update Max
            if arr[i] > Max:
                Max = arr[i]

            # If Len greater than
            # maxLen
            if Len >= maxLen:
                maxLen = Len

                # Update MaxElem
                if Max >= MaxElem:
                    MaxElem = Max
        else:

            # Update Len
            Len = 1

            # Update Max
            Max = arr[i]

            # If Len greater
            # than maxLen
            if Len >= maxLen:
                maxLen = Len

                # If Max greater
                #   than MaxElem
                if Max >= MaxElem:
                    MaxElem = Max

    return MaxElem

# Driver Code
arr = [ 1, 3, 5, 7, 8, 12, 10 ]
n = len(arr)

print(maxelementLongestSub(arr, n))

# This code is contributed by sourav singh
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the largest element
// of the longest subarray consisting
// only of odd or even elements only    
static int maxelementLongestSub(int[] arr,
                                int n)
{

    // Stores largest element of the
    // longest subarray till i-th index
    int MaxElem = arr[0];

    // Stores maximum length of the
    // longest subarray till i-th index
    int maxLen = 1;

    // Stores length of the current
    // subarray including the i-th element
    int Len = 1;

    // Stores largest element in
    // current subarray
    int Max = arr[0];

    // Traverse the array
    for(int i = 1; i < n; i++)
    {

        // If arr[i] and arr[i - 1]
        // are either even numbers
        // or odd numbers
        if (arr[i] % 2 == arr[i - 1] % 2)
        {

            // Update Len
            Len++;

            // Update Max
            if (arr[i] > Max)
                Max = arr[i];

            // If Len greater than
            // maxLen
            if (Len >= maxLen)
            {
                maxLen = Len;

                // Update MaxElem
                if (Max >= MaxElem)
                    MaxElem = Max;
            }
        }
        else
        {

            // Update Len
            Len = 1;

            // Update Max
            Max = arr[i];

            // If Len greater
            // than maxLen
            if (Len >= maxLen)
            {

                // Update maxLen
                maxLen = Len;

                // If Max greater
                // than MaxElem
                if (Max >= MaxElem)
                {

                    // Update MaxElem
                    MaxElem = Max;
                }
            }
        }
    }
    return MaxElem;
}

//  Driver Code
public static void Main(String[] args)
{
    int[] arr = { 1, 3, 5, 7, 8, 12, 10 };
    int n = arr.Length;

    // Function call
    Console.Write(maxelementLongestSub(arr, n));
}
}

// This code is contributed by sourav singh
```

## java 描述语言

```
<script>

      // JavaScript program to implement
      // the above approach

      // Function to find the largest element
      // of the longest subarray consisting
      // only of odd or even elements only
      function maxelementLongestSub(arr, n)
      {
        // Stores largest element of the
        // longest subarray till i-th index
        var MaxElem = arr[0];

        // Stores maximum length of the
        // longest subarray till i-th index
        var maxLen = 1;

        // Stores length of the current
        // subarray including the i-th element
        var Len = 1;

        // Stores largest element in
        // current subarray
        var Max = arr[0];

        // Traverse the array
        for (var i = 1; i < n; i++) {
          // If arr[i] and arr[i - 1]
          // are either even numbers
          // or odd numbers
          if (arr[i] % 2 == arr[i - 1] % 2) {
            // Update Len
            Len++;

            // Update Max
            if (arr[i] > Max) Max = arr[i];

            // If Len greater than
            // maxLen
            if (Len >= maxLen) {
              maxLen = Len;

              // Update MaxElem
              if (Max >= MaxElem) MaxElem = Max;
            }
          } else {
            // Update Len
            Len = 1;

            // Update Max
            Max = arr[i];

            // If Len greater
            // than maxLen
            if (Len >= maxLen) {
              // Update maxLen
              maxLen = Len;

              // If Max greater
              // than MaxElem
              if (Max >= MaxElem) {
                // Update MaxElem
                MaxElem = Max;
              }
            }
          }
        }

        return MaxElem;
      }

      // Driver Code
      var arr = [1, 3, 5, 7, 8, 12, 10];
      var n = arr.length;

      document.write(maxelementLongestSub(arr, n));

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)