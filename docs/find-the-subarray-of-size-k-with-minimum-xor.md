# 用最小异或求 K 大小的子阵

> 原文:[https://www . geesforgeks . org/find-the-subarray-of-size-k-with-minimum-xor/](https://www.geeksforgeeks.org/find-the-subarray-of-size-k-with-minimum-xor/)

给定一个数组 **arr[]** 和整数 **K** ，任务是找到给定数组中任意大小的子数组 **K** 的最小按位异或和。
**举例:**

> **输入:** arr[] = {3，7，90，20，10，50，40}，K = 3
> **输出:** 16
> **解释:**
> 子阵列{10，50，40}具有最小 XOR
> **输入:** arr[] = {3，7，5，20，-10，0，12}，K = 2
> **输出:**

**天真方法:**一个简单的解决方案是将每个元素都视为大小为 k 的子阵列的开始，并从这个元素开始计算子阵列的 XOR。
**时间复杂度:** O(N * K)
**高效方法:**思路是使用大小为 **K** 的[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)，跟踪当前 **K** 元素的异或和。要计算当前窗口的异或，请对前一个窗口的第一个元素执行异或运算以丢弃该元素，并对当前元素执行异或运算以将该元素添加到窗口中。同样，滑动窗口，找到大小为 **K** 的子阵列的最小异或。
以下是上述方法的实施:

## C++

```
// C++ implementation to find the
// subarray with minimum XOR

#include <bits/stdc++.h>

using namespace std;

// Function to find the minimum
// XOR of the subarray of size K
void findMinXORSubarray(int arr[],
                     int n, int k)
{
    // K must be smaller
    // than or equal to n
    if (n < k)
        return;

    // Initialize beginning
    // index of result
    int res_index = 0;

    // Compute XOR sum of first
    // subarray of size K
    int curr_xor = 0;
    for (int i = 0; i < k; i++)
        curr_xor ^= arr[i];

    // Initialize minimum XOR
    // sum as current xor
    int min_xor = curr_xor;

    // Traverse from (k+1)'th
    // element to n'th element
    for (int i = k; i < n; i++) {

        // XOR with current item
        // and first item of
        // previous subarray
        curr_xor ^= (arr[i] ^ arr[i - k]);

        // Update result if needed
        if (curr_xor < min_xor) {
            min_xor = curr_xor;
            res_index = (i - k + 1);
        }
    }

    cout << min_xor << "\n";
}

// Driver Code
int main()
{
    int arr[] = { 3, 7, 90, 20, 10, 50, 40 };
    int k = 3; // Subarray size
    int n = sizeof arr / sizeof arr[0];

    // Function Call
    findMinXORSubarray(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// subarray with minimum XOR
class GFG{

// Function to find the minimum
// XOR of the subarray of size K
static void findMinXORSubarray(int arr[],
                               int n, int k)
{

    // K must be smaller
    // than or equal to n
    if (n < k)
        return;

    // Initialize beginning
    // index of result
    int res_index = 0;

    // Compute XOR sum of first
    // subarray of size K
    int curr_xor = 0;
    for(int i = 0; i < k; i++)
       curr_xor ^= arr[i];

    // Initialize minimum XOR
    // sum as current xor
    int min_xor = curr_xor;

    // Traverse from (k+1)'th
    // element to n'th element
    for(int i = k; i < n; i++)
    {

       // XOR with current item
       // and first item of
       // previous subarray
       curr_xor ^= (arr[i] ^ arr[i - k]);

       // Update result if needed
       if (curr_xor < min_xor)
       {
           min_xor = curr_xor;
           res_index = (i - k + 1);
       }
    }
    System.out.print(min_xor + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 7, 90, 20, 10, 50, 40 };

    // Subarray size
    int k = 3;
    int n = arr.length;

    // Function Call
    findMinXORSubarray(arr, n, k);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# subarray with minimum XOR

# Function to find the minimum
# XOR of the subarray of size K
def findMinXORSubarray(arr, n, k):

    # K must be smaller
    # than or equal to n
    if (n < k):
        return

    # Initialize beginning
    # index of result
    res_index = 0

    # Compute XOR sum of first
    # subarray of size K
    curr_xor = 0
    for i in range(0, k):
        curr_xor = curr_xor ^ arr[i]

    # Initialize minimum XOR
    # sum as current xor
    min_xor = curr_xor

    # Traverse from (k+1)'th
    # element to n'th element
    for i in range(k, n):

        # XOR with current item
        # and first item of
        # previous subarray
        curr_xor ^= (arr[i] ^ arr[i - k])

        # Update result if needed
        if (curr_xor < min_xor):
            min_xor = curr_xor
            res_index = (i - k + 1)

    print(min_xor, end = '\n')

# Driver Code
arr = [ 3, 7, 90, 20, 10, 50, 40 ]

# Subarray size
k = 3
n = len(arr)

# Function Call
findMinXORSubarray(arr, n, k)

# This code is contributed by PratikBasu   
```

## C#

```
// C# implementation to find the
// subarray with minimum XOR
using System;

class GFG{

// Function to find the minimum
// XOR of the subarray of size K
static void findMinXORSubarray(int []arr,
                               int n, int k)
{

    // K must be smaller
    // than or equal to n
    if (n < k)
        return;

    // Initialize beginning
    // index of result
    int res_index = 0;

    // Compute XOR sum of first
    // subarray of size K
    int curr_xor = 0;
    for(int i = 0; i < k; i++)
       curr_xor ^= arr[i];

    // Initialize minimum XOR
    // sum as current xor
    int min_xor = curr_xor;

    // Traverse from (k+1)'th
    // element to n'th element
    for(int i = k; i < n; i++)
    {

       // XOR with current item
       // and first item of
       // previous subarray
       curr_xor ^= (arr[i] ^ arr[i - k]);

       // Update result if needed
       if (curr_xor < min_xor)
       {
           min_xor = curr_xor;
           res_index = (i - k + 1);
       }
    }
    Console.Write(min_xor + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 3, 7, 90, 20, 10, 50, 40 };

    // Subarray size
    int k = 3;
    int n = arr.Length;

    // Function Call
    findMinXORSubarray(arr, n, k);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// subarray with minimum XOR

// Function to find the minimum
// XOR of the subarray of size K
function findMinXORSubarray(arr, n, k)
{
    // K must be smaller
    // than or equal to n
    if (n < k)
        return;

    // Initialize beginning
    // index of result
    let res_index = 0;

    // Compute XOR sum of first
    // subarray of size K
    let curr_xor = 0;
    for (let i = 0; i < k; i++)
        curr_xor ^= arr[i];

    // Initialize minimum XOR
    // sum as current xor
    let min_xor = curr_xor;

    // Traverse from (k+1)'th
    // element to n'th element
    for (let i = k; i < n; i++) {

        // XOR with current item
        // and first item of
        // previous subarray
        curr_xor ^= (arr[i] ^ arr[i - k]);

        // Update result if needed
        if (curr_xor < min_xor) {
            min_xor = curr_xor;
            res_index = (i - k + 1);
        }
    }

    document.write(min_xor + "<br>");
}

// Driver Code
    let arr = [ 3, 7, 90, 20, 10, 50, 40 ];
    let k = 3; // Subarray size
    let n = arr.length;

    // Function Call
    findMinXORSubarray(arr, n, k);

</script>
```

**Output:** 

```
16
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)