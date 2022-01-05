# 找出数组第一和第二部分的最大元素

> 原文:[https://www . geeksforgeeks . org/在数组的第一个和第二个半部分中找到最大元素/](https://www.geeksforgeeks.org/find-the-maximum-elements-in-the-first-and-the-second-halves-of-the-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** 。任务是在数组的前半部分和后半部分找到最大的元素。**注意**如果数组的大小是奇数，那么中间的元素将包含在两半中。
**示例:**

> **输入:** arr[] = {1，12，14，5}
> 输出: 12，14
> 前半部分为{1，12}，后半部分为{14，5}。
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 3，5

**方法:**计算数组的中间索引为 **mid = N / 2** 。现在，如果 **N 为偶数**，第一半元素将出现在子阵列**arr[0…中间-1]** 和**arr[中间…N-1]** 中。
如果 **N 为奇数**，则两半为**arr【0…中间】**和 **arr【中间…N-1】**
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print largest element in
// first half and second half of an array
void findMax(int arr[], int n)
{

    // To store the maximum element
    // in the first half
    int maxFirst = INT_MIN;

    // Middle index of the array
    int mid = n / 2;

    // Calculate the maximum element
    // in the first half
    for (int i = 0; i < mid; i++)
        maxFirst = max(maxFirst, arr[i]);

    // If the size of array is odd then
    // the middle element will be included
    // in both the halves
    if (n % 2 == 1)
        maxFirst = max(maxFirst, arr[mid]);

    // To store the maximum element
    // in the second half
    int maxSecond = INT_MIN;

    // Calculate the maximum element
    // int the second half
    for (int i = mid; i < n; i++)
        maxSecond = max(maxSecond, arr[i]);

    // Print the found maximums
    cout << maxFirst << ", " << maxSecond;
}

// Driver code
int main()
{
    int arr[] = { 1, 12, 14, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    findMax(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{
    static void findMax(int []arr, int n)
    {

        // To store the maximum element
        // in the first half
        int maxFirst = Integer.MIN_VALUE;

        // Middle index of the array
        int mid = n / 2;

        // Calculate the maximum element
        // in the first half
        for (int i = 0; i < mid; i++)
        {
            maxFirst = Math.max(maxFirst, arr[i]);
        }

        // If the size of array is odd then
        // the middle element will be included
        // in both the halves
        if (n % 2 == 1)
        {
            maxFirst = Math.max(maxFirst, arr[mid]);
        }

        // To store the maximum element
        // in the second half
        int maxSecond = Integer.MIN_VALUE;

        // Calculate the maximum element
        // int the second half
        for (int i = mid; i < n; i++)
        {
            maxSecond = Math.max(maxSecond, arr[i]);
        }

        // Print the found maximums
        System.out.print(maxFirst + ", " + maxSecond);
        // cout << maxFirst << ", " << maxSecond;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int []arr = { 1, 12, 14, 5 };
        int n = arr.length;

        findMax(arr, n);
    }
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function to print largest element in
# first half and second half of an array
def findMax(arr, n) :

    # To store the maximum element
    # in the first half
    maxFirst = -sys.maxsize - 1

    # Middle index of the array
    mid = n // 2;

    # Calculate the maximum element
    # in the first half
    for i in range(0, mid):
        maxFirst = max(maxFirst, arr[i])

    # If the size of array is odd then
    # the middle element will be included
    # in both the halves
    if (n % 2 == 1):
        maxFirst = max(maxFirst, arr[mid])

    # To store the maximum element
    # in the second half
    maxSecond = -sys.maxsize - 1

    # Calculate the maximum element
    # int the second half
    for i in range(mid, n):
        maxSecond = max(maxSecond, arr[i])

    # Print the found maximums
    print(maxFirst, ",", maxSecond)

# Driver code
arr = [1, 12, 14, 5 ]
n = len(arr)

findMax(arr, n)

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static void findMax(int []arr, int n)
    {

        // To store the maximum element
        // in the first half
        int maxFirst = int.MinValue;

        // Middle index of the array
        int mid = n / 2;

        // Calculate the maximum element
        // in the first half
        for (int i = 0; i < mid; i++)
        {
            maxFirst = Math.Max(maxFirst, arr[i]);
        }

        // If the size of array is odd then
        // the middle element will be included
        // in both the halves
        if (n % 2 == 1)
        {
            maxFirst = Math.Max(maxFirst, arr[mid]);
        }

        // To store the maximum element
        // in the second half
        int maxSecond = int.MinValue;

        // Calculate the maximum element
        // int the second half
        for (int i = mid; i < n; i++)
        {
            maxSecond = Math.Max(maxSecond, arr[i]);
        }

        // Print the found maximums
        Console.WriteLine(maxFirst + ", " + maxSecond);
        // cout << maxFirst << ", " << maxSecond;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = { 1, 12, 14, 5 };
        int n = arr.Length;

        findMax(arr, n);
    }
}

// This code is contributed by nidhiva
```

## java 描述语言

```
// javascript implementation of the approach
    function findMax(arr, n)
    {

        // To store the maximum element
        // in the first half

        var maxFirst = Number.MIN_VALUE

        // Middle index of the array
        var mid = n / 2;

        // Calculate the maximum element
        // in the first half
        for (var i = 0; i < mid; i++)
        {
            maxFirst = Math.max(maxFirst, arr[i]);
        }

        // If the size of array is odd then
        // the middle element will be included
        // in both the halves
        if (n % 2 == 1)
        {
            maxFirst = Math.max(maxFirst, arr[mid]);
        }

        // To store the maximum element
        // in the second half
        var maxSecond = Number.MIN_VALUE

        // Calculate the maximum element
        // int the second half
        for (var i = mid; i < n; i++)
        {
            maxSecond = Math.max(maxSecond, arr[i]);
        }

        // Print the found maximums
        document.write(maxFirst + ", " + maxSecond);
    }

    // Driver Code
        var arr = [ 1, 12, 14, 5 ];
        var n = arr.length;

        findMax(arr, n);

 // This code is contributed by bunnyram19.
```

**Output:** 

```
12, 14
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*