# Javascript 程序寻找平均值最小的子阵

> 原文:[https://www . geesforgeks . org/JavaScript-program-to-find-the-subarray-with-average/](https://www.geeksforgeeks.org/javascript-program-to-find-the-subarray-with-least-average/)

给定大小为 n 且整数为 k 的数组 arr[,使得 k <= n。

**示例:**

```
Input:  arr[] = {3, 7, 90, 20, 10, 50, 40}, k = 3
Output: Subarray between indexes 3 and 5
The subarray {20, 10, 50} has the least average 
among all subarrays of size 3.

Input:  arr[] = {3, 7, 5, 20, -10, 0, 12}, k = 2
Output: Subarray between [4, 5] has minimum average
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/subarray-with-least-average5031/1)

一个**简单的解决方案**是把每个元素看作大小为 k 的子阵列的开始，并从这个元素开始计算子阵列的和。这个解决方案的时间复杂度是 O(nk)。

一个**高效的解决方案**就是在 O(n)个时间和 O(1)个额外空间内解决上述问题。想法是使用大小为 k 的滑动窗口。跟踪当前 k 个元素的总和。要计算当前窗口的总和，请移除前一个窗口的第一个元素并添加当前元素(当前窗口的最后一个元素)。

```
1) Initialize res_index = 0 // Beginning of result index
2) Find sum of first k elements. Let this sum be 'curr_sum'
3) Initialize min_sum = sum
4) Iterate from (k+1)'th to n'th element, do following
   for every element arr[i]
      a) curr_sum = curr_sum + arr[i] - arr[i-k]
      b) If curr_sum < min_sum
           res_index = (i-k+1)
5) Print res_index and res_index+k-1 as beginning and ending
   indexes of resultant subarray.
```

下面是上述算法的实现。

## java 描述语言

```
<script>

// A Simple JavaScript program to find
// minimum average subarray

// Prints beginning and ending indexes
// of subarray of size k with minimum average
function findMinAvgSubarray(arr, n, k)
{

    // k must be smaller than or equal to n
    if (n < k)
        return;

    // Initialize beginning index of result
    let res_index = 0;

    // Compute sum of first subarray of size k
    let curr_sum = 0;
    for(let i = 0; i < k; i++)
        curr_sum += arr[i];

    // Initialize minimum sum as current sum
    let min_sum = curr_sum;

    // Traverse from (k+1)'th element
    // to n'th element
    for(let i = k; i < n; i++) 
    {

        // Add current item and remove first
        // item of previous subarray
        curr_sum += arr[i] - arr[i - k];

        // Update result if needed
        if (curr_sum < min_sum)
        {
            min_sum = curr_sum;
            res_index = (i - k + 1);
        }
    }
    document.write("Subarray between [" + res_index + 
                   ", " + (res_index + k - 1) + 
                   "] has minimum average");
}

// Driver code
let arr = [ 3, 7, 90, 20, 10, 50, 40 ];

// Subarray size
let k = 3; 
let n = arr.length;

findMinAvgSubarray(arr, n, k);

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
Subarray between [3, 5] has minimum average
```

时间复杂度:O(n)
辅助空间:O(1)

详情请参考[整篇文章找到平均值最小的子阵](https://www.geeksforgeeks.org/find-subarray-least-average/)！

=>