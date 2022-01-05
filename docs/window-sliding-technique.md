# 窗口滑动技术

> 原文:[https://www.geeksforgeeks.org/window-sliding-technique/](https://www.geeksforgeeks.org/window-sliding-technique/)

这项技术展示了如何将一些问题中的嵌套 for 循环转换为单个 for 循环，以降低时间复杂度。
让我们从一个问题开始，说明我们可以在哪里应用这种技术–

```
Given an array of integers of size ‘n’.
Our aim is to calculate the maximum sum of ‘k’ 
consecutive elements in the array.

Input  : arr[] = {100, 200, 300, 400}
         k = 2
Output : 700

Input  : arr[] = {1, 4, 2, 10, 23, 3, 1, 0, 20}
         k = 4 
Output : 39
We get maximum sum by adding subarray {4, 2, 10, 23}
of size 4.

Input  : arr[] = {2, 3}
         k = 3
Output : Invalid
There is no subarray of size 3 as size of whole
array is 2.
```

那么，我们来分析一下**蛮力进场**的问题。我们从第一个索引和求和开始，直到第 k 个元素。我们对 k 个元素的所有可能的连续块或组都这样做。这个方法需要嵌套 for 循环，外部 for 循环从 k 个元素的块的起始元素开始，内部或嵌套循环相加，直到第 k 个元素。

考虑以下实现:

## C++

```
// O(n*k) solution for finding maximum sum of
// a subarray of size k
#include <bits/stdc++.h>
using namespace std;

// Returns maximum sum in a subarray of size k.
int maxSum(int arr[], int n, int k)
{
    // Initialize result
    int max_sum = INT_MIN;

    // Consider all blocks starting with i.
    for (int i = 0; i < n - k + 1; i++) {
        int current_sum = 0;
        for (int j = 0; j < k; j++)
            current_sum = current_sum + arr[i + j];

        // Update result if required.
        max_sum = max(current_sum, max_sum);
    }

    return max_sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 4, 2, 10, 2, 3, 1, 0, 20 };
    int k = 4;
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxSum(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code here
// O(n*k) solution for finding
// maximum sum of a subarray
// of size k
class GFG {
    // Returns maximum sum in
    // a subarray of size k.
    static int maxSum(int arr[], int n, int k)
    {
        // Initialize result
        int max_sum = Integer.MIN_VALUE;

        // Consider all blocks starting with i.
        for (int i = 0; i < n - k + 1; i++) {
            int current_sum = 0;
            for (int j = 0; j < k; j++)
                current_sum = current_sum + arr[i + j];

            // Update result if required.
            max_sum = Math.max(current_sum, max_sum);
        }

        return max_sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 4, 2, 10, 2, 3, 1, 0, 20 };
        int k = 4;
        int n = arr.length;
        System.out.println(maxSum(arr, n, k));
    }
}

// This code is contributed
// by  prerna saini.
```

## 计算机编程语言

```
# code
import sys
print "GFG"
# O(n * k) solution for finding
# maximum sum of a subarray of size k
INT_MIN = -sys.maxsize - 1

# Returns maximum sum in a
# subarray of size k.

def maxSum(arr, n, k):

    # Initialize result
    max_sum = INT_MIN

    # Consider all blocks
    # starting with i.
    for i in range(n - k + 1):
        current_sum = 0
        for j in range(k):
            current_sum = current_sum + arr[i + j]

        # Update result if required.
        max_sum = max(current_sum, max_sum)

    return max_sum

# Driver code
arr = [1, 4, 2, 10, 2,
       3, 1, 0, 20]
k = 4
n = len(arr)
print(maxSum(arr, n, k))

# This code is contributed by mits
```

## C#

```
// C# code here O(n*k) solution for
// finding maximum sum of a subarray
// of size k
using System;

class GFG {

    // Returns maximum sum in a
    // subarray of size k.
    static int maxSum(int[] arr, int n, int k)
    {
        // Initialize result
        int max_sum = int.MinValue;

        // Consider all blocks starting
        // with i.
        for (int i = 0; i < n - k + 1; i++) {
            int current_sum = 0;
            for (int j = 0; j < k; j++)
                current_sum = current_sum + arr[i + j];

            // Update result if required.
            max_sum = Math.Max(current_sum, max_sum);
        }

        return max_sum;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 4, 2, 10, 2, 3, 1, 0, 20 };
        int k = 4;
        int n = arr.Length;
        Console.WriteLine(maxSum(arr, n, k));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
    // code
?>
<?php
// O(n*k) solution for finding maximum sum of
// a subarray of size k

// Returns maximum sum in a subarray of size k.
function maxSum($arr, $n, $k)
{

    // Initialize result
    $max_sum = PHP_INT_MIN ;

    // Consider all blocks
    // starting with i.
    for ( $i = 0; $i < $n - $k + 1; $i++)
    {
        $current_sum = 0;
        for ( $j = 0; $j < $k; $j++)
            $current_sum = $current_sum +
                            $arr[$i + $j];

        // Update result if required.
        $max_sum = max($current_sum, $max_sum );
    }

    return $max_sum;
}

    // Driver code
    $arr = array(1, 4, 2, 10, 2, 3, 1, 0, 20);
    $k = 4;
    $n = count($arr);
    echo maxSum($arr, $n, $k);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// O(n*k) solution for finding maximum sum of
// a subarray of size k

// Returns maximum sum in a subarray of size k.
function maxSum( arr, n, k){
    // Initialize result
    let max_sum = Number.MIN_VALUE;

    // Consider all blocks starting with i.
    for (let i = 0; i < n - k + 1; i++) {
        let current_sum = 0;
        for (let j = 0; j < k; j++)
            current_sum = current_sum + arr[i + j];

        // Update result if required.
        max_sum = Math.max(current_sum, max_sum);
    }

    return max_sum;
}

// Driver code
let arr = [ 1, 4, 2, 10, 2, 3, 1, 0, 20 ];
let k = 4;
let n = arr.length;
document.write(maxSum(arr, n, k));

</script>
```

**Output**

```
24
```