# 未排序数组中的第 k 个缺失元素

> 原文:[https://www . geesforgeks . org/k-th-未排序数组中缺少元素/](https://www.geeksforgeeks.org/k-th-missing-element-in-an-unsorted-array/)

给定一个未排序的序列 a[]，任务是在数组元素的递增序列中找到第 K 个缺失的连续元素，即按排序顺序考虑数组并找到第 K 个缺失的数字。如果没有第 k 个缺失元素，则输出-1。
**注:**待考虑的最小和最大元素范围内只存在元素。
**示例:**

```
Input: arr[] = {2, 4, 10, 7}, k = 5
Output: 9
Missing elements in the given array: 3, 5, 6, 8, 9
5th missing is 9.

Input: arr[] = {1, 3, 4}, k = 5
Output: -1
```

**方法-1:** 对数组进行排序，并使用排序数组中第 [k 个缺失元素所使用的方法。
**方法-2:**](https://www.geeksforgeeks.org/k-th-missing-element-in-sorted-array/) 

1.  在无序集中插入所有元素。
2.  找到数组的最小和最大元素。
3.  从最小到最大遍历元素。
    *   检查集合中是否存在当前元素。
    *   如果没有，那么通过计算丢失的元素来检查这是否是第 k 个丢失的。
    *   如果当前缺少当前元素，则返回当前元素。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum
// of minimum of all subarrays
int findKth(int arr[], int n, int k)
{

    unordered_set<int> missing;
    int count = 0;

    // Insert all the elements in a set
    for (int i = 0; i < n; i++)
        missing.insert(arr[i]);

    // Find the maximum and minimum element
    int maxm = *max_element(arr, arr + n);
    int minm = *min_element(arr, arr + n);

    // Traverse from the minimum to maximum element
    for (int i = minm + 1; i < maxm; i++) {
        // Check if "i" is missing
        if (missing.find(i) == missing.end())
            count++;

        // Check if it is kth missing
        if (count == k)
            return i;
    }

    // If no kth element is missing
    return -1;
}

// Driver code
int main()
{
    int arr[] = { 2, 10, 9, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 5;
    cout << findKth(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    // Function to find the sum
    // of minimum of all subarrays
    static int findKth(int arr[], int n, int k)
    {

        HashSet<Integer> missing = new HashSet<>();
        int count = 0;

        // Insert all the elements in a set
        for (int i = 0; i < n; i++)
        {
            missing.add(arr[i]);
        }

        // Find the maximum and minimum element
        int maxm = Arrays.stream(arr).max().getAsInt();
        int minm = Arrays.stream(arr).min().getAsInt();

        // Traverse from the minimum to maximum element
        for (int i = minm+1; i < maxm; i++)
        {
            // Check if "i" is missing
            if (!missing.contains(i))
            {
                count++;
            }

            // Check if it is kth missing
            if (count == k)
            {
                return i;
            }
        }

        // If no kth element is missing
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {2, 10, 9, 4};
        int n = arr.length;
        int k = 5;
        System.out.println(findKth(arr, n, k));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 计算机编程语言

```
# Python3 implementation of the above approach

# Function to find the sum
# of minimum of all subarrays
def findKth( arr, n, k):

    missing = dict()
    count = 0

    # Insert all the elements in a set
    for i in range(n):
        missing[arr[i]] = 1

    # Find the maximum and minimum element
    maxm = max(arr)
    minm = min(arr)

    # Traverse from the minimum to maximum element
    for i in range(minm + 1, maxm):

        # Check if "i" is missing
        if (i not in missing.keys()):
            count += 1

        # Check if it is kth missing
        if (count == k):
            return i

    # If no kth element is missing
    return -1

# Driver code
arr = [2, 10, 9, 4 ]
n = len(arr)
k = 5
print(findKth(arr, n, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{

    // Function to find the sum
    // of minimum of all subarrays
    static int findKth(int []arr, int n, int k)
    {

        HashSet<int> missing = new HashSet<int>();
        int count = 0;

        // Insert all the elements in a set
        for (int i = 0; i < n; i++)
        {
            missing.Add(arr[i]);
        }

        // Find the maximum and minimum element
        int maxm = arr.Max();
        int minm = arr.Min();

        // Traverse from the minimum to maximum element
        for (int i = minm + 1; i < maxm; i++)
        {
            // Check if "i" is missing
            if (!missing.Contains(i))
            {
                count++;
            }

            // Check if it is kth missing
            if (count == k)
            {
                return i;
            }
        }

        // If no kth element is missing
        return -1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {2, 10, 9, 4};
        int n = arr.Length;
        int k = 5;
        Console.WriteLine(findKth(arr, n, k));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find the sum
// of minimum of all subarrays
function findKth($arr, $n, $k)
{

    $missing = array();
    $count = 0;

    // Insert all the elements in a set
    for ($i = 0; $i < $n; $i++)
        array_push($missing, $arr[$i]);

    $missing = array_unique($missing);

    // Find the maximum and minimum element
    $maxm = max($arr);
    $minm = min($arr);

    // Traverse from the minimum to
    // maximum element
    for ($i = $minm + 1; $i < $maxm; $i++)
    {
        // Check if "i" is missing
        if (!in_array($i, $missing, false))
            $count += 1;

        // Check if it is kth missing
        if ($count == $k)
            return $i;
    }

    // If no kth element is missing
    return -1;
}

// Driver code
$arr = array(2, 10, 9, 4);
$n = sizeof($arr);
$k = 5;

echo findKth($arr, $n, $k);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// javascript implementation of the above approach

// Function to find the sum
// of minimum of all subarrays
function findKth(arr, n, k)
{

    var missing = new Set();
    var count = 0;

    // Insert all the elements in a set
    for (var i = 0; i < n; i++)
        missing.add(arr[i]);

    // Find the maximum and minimum element
    var maxm = arr.reduce((a,b)=>Math.max(a,b));
    var minm = arr.reduce((a,b)=>Math.min(a,b));

    // Traverse from the minimum to maximum element
    for (var i = minm + 1; i < maxm; i++) {
        // Check if "i" is missing
        if (!missing.has(i))
            count++;

        // Check if it is kth missing
        if (count == k)
            return i;
    }

    // If no kth element is missing
    return -1;
}

// Driver code
var arr = [ 2, 10, 9, 4 ];
var n = arr.length;
var k = 5;
document.write( findKth(arr, n, k));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
8
```