# 最小和连续子阵列|集合-2

> 原文:[https://www . geesforgeks . org/minist-sum-continuous-subarray-set-2/](https://www.geeksforgeeks.org/smallest-sum-contiguous-subarray-set-2/)

给定一个包含 N 个整数的数组。任务是找到具有最小(最小)和的相邻子阵列的元素的和。
**例** :

```
Input: arr[] = {3, -4, 2, -3, -1, 7, -5}
Output:-6

Input: arr = {2, 6, 8, 1, 4}
Output: 1
```

在之前的[帖子](https://www.geeksforgeeks.org/smallest-sum-contiguous-subarray/)中已经讨论了一种方法。本文讨论了使用[最大和邻接子阵](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)方法的解决方案。这是基于这样一个事实，为了找到最小连续和，我们可以首先使原始数组的元素为负。将每个 ar[i]替换为-ar[i]，然后应用[卡丹算法](http://Largest Sum Contiguous Subarray)。显然，如果这是形成的最大和，那么最小和就是这个和的负数。
以下是上述方法的实施:

## C++

```
// C++ program for
// Smallest sum contiguous subarray | Set 2
#include <bits/stdc++.h>

using namespace std;

// function to find the smallest sum contiguous subarray
int smallestSumSubarr(int arr[], int n)
{
    // First invert the sign of the elements
    for (int i = 0; i < n; i++)
        arr[i] = -arr[i];

    // Apply the normal Kadane algorithm But on the elements
    // Of the array having inverted sign
    int sum_here = arr[0], max_sum = arr[0];

    for (int i = 1; i < n; i++) {

        sum_here = max(sum_here + arr[i], arr[i]);
        max_sum = max(max_sum, sum_here);
    }

    // Invert  the answer to get minimum val
    return (-1) * max_sum;
}

// Driver Code
int main()
{
    int arr[] = { 3, -4, 2, -3, -1, 7, -5 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Smallest sum: "
         << smallestSumSubarr(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Smallest
// sum contiguous subarray | Set 2
import java.io.*;

class GFG
{

// function to find the
// smallest sum contiguous
// subarray
static int smallestSumSubarr(int arr[],
                             int n)
{
    // First invert the
    // sign of the elements
    for (int i = 0; i < n; i++)
        arr[i] = -arr[i];

    // Apply the normal Kadane
    // algorithm But on the
    // elements Of the array
    // having inverted sign
    int sum_here = arr[0],
        max_sum = arr[0];

    for (int i = 1; i < n; i++)
    {
        sum_here = Math.max(sum_here +
                            arr[i], arr[i]);
        max_sum = Math.max(max_sum,
                           sum_here);
    }

    // Invert the answer
    // to get minimum val
    return (-1) * max_sum;
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = {3, -4, 2, -3,
                -1, 7, -5};

    int n = arr.length;

    System.out.print("Smallest sum: " +
            smallestSumSubarr(arr, n));
}
}

// This code is contributed
// by inder_verma.
```

## 蟒蛇 3

```
# Python3 program for
# Smallest sum contiguous subarray | Set 2

# function to find the smallest
# sum contiguous subarray
def smallestSumSubarr(arr, n):

    # First invert the sign of the elements
    for i in range(n):
        arr[i] = -arr[i]

    # Apply the normal Kadane algorithm but
    # on the elements of the array having inverted sign
    sum_here = arr[0]
    max_sum = arr[0]

    for i in range(1, n):

        sum_here = max(sum_here + arr[i], arr[i])
        max_sum = max(max_sum, sum_here)

    # Invert the answer to get minimum val
    return (-1) * max_sum

# Driver Code
arr = [3, -4, 2, -3, -1, 7, -5]

n = len(arr)

print("Smallest sum:",
       smallestSumSubarr(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for Smallest
// sum contiguous subarray | Set 2
using System;
class GFG
{

// function to find the
// smallest sum contiguous
// subarray
static int smallestSumSubarr(int []arr,
                             int n)
{
    // First invert the
    // sign of the elements
    for (int i = 0; i < n; i++)
        arr[i] = -arr[i];

    // Apply the normal Kadane
    // algorithm But on the
    // elements Of the array
    // having inverted sign
    int sum_here = arr[0],
        max_sum = arr[0];

    for (int i = 1; i < n; i++)
    {
        sum_here = Math.Max(sum_here +
                            arr[i], arr[i]);
        max_sum = Math.Max(max_sum,
                           sum_here);
    }

    // Invert the answer
    // to get minimum val
    return (-1) * max_sum;
}

// Driver Code
public static void Main ()
{
    int []arr = {3, -4, 2, -3,
                -1, 7, -5};

    int n = arr.Length;

    Console.WriteLine("Smallest sum: " +
             smallestSumSubarr(arr, n));
}
}

// This code is contributed
// by inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Smallest sum
// contiguous subarray | Set 2

// Function to find the smallest
// sum contiguous subarray
function smallestSumSubarr($arr, $n)
{
    // First invert the sign
    // of the elements
    for ( $i = 0; $i < $n; $i++)
        $arr[$i] = -$arr[$i];

    // Apply the normal Kadane algorithm
    // but on the elements of the array
    // having inverted sign
    $sum_here = $arr[0];
    $max_sum = $arr[0];

    for ($i = 1; $i < $n; $i++)
    {
        $sum_here = max($sum_here +
                        $arr[$i], $arr[$i]);
        $max_sum = max($max_sum, $sum_here);
    }

    // Invert the answer to
    // get minimum val
    return (-1) * $max_sum;
}

// Driver Code
$arr = array( 3, -4, 2, -3, -1, 7, -5 );

$n = sizeof($arr);

echo "Smallest sum: ",
    smallestSumSubarr($arr, $n);

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// JavaScript program for Smallest
// sum contiguous subarray | Set 2

// function to find the
// smallest sum contiguous
// subarray
function smallestSumSubarr(arr, n)
{
    // First invert the
    // sign of the elements
    for (let i = 0; i < n; i++)
        arr[i] = -arr[i];

    // Apply the normal Kadane
    // algorithm But on the
    // elements Of the array
    // having inverted sign
    let sum_here = arr[0],
        max_sum = arr[0];

    for (let i = 1; i < n; i++)
    {
        sum_here = Math.max(sum_here +
                            arr[i], arr[i]);
        max_sum = Math.max(max_sum,
                           sum_here);
    }

    // Invert the answer
    // to get minimum val
    return (-1) * max_sum;
}

// driver code

     let arr = [3, -4, 2, -3,
                -1, 7, -5];

    let n = arr.length;

    document.write("Smallest sum: " +
            smallestSumSubarr(arr, n));

</script>
```

**Output:** 

```
Smallest sum: -6
```

**时间复杂度:** O(n)