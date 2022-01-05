# 至少有 k 个数的最大和子阵

> 原文:[https://www . geesforgeks . org/maximum-sum-subarray-minist-k-numbers/](https://www.geeksforgeeks.org/largest-sum-subarray-least-k-numbers/)

给定一个数组，找出和最大的子数组(至少包含 k 个数)。
示例:

```
Input : arr[] = {-4, -2, 1, -3} 
            k = 2
Output : -1
The sub array is {-2, 1}

Input : arr[] = {1, 1, 1, 1, 1, 1} 
            k = 2
Output : 6 
The sub array is {1, 1, 1, 1, 1, 1}
```

问于:脸书

这个问题是[最大和子阵问题](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)的扩展。
1)我们首先计算每个索引前的最大和，并将其存储在一个数组 maxSum[]中。
2)填充数组后，我们使用大小为 k 的[滑动窗口概念](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)，跟踪当前 k 个元素的总和。要计算当前窗口的总和，请移除前一个窗口的第一个元素并添加当前元素。在得到当前窗口的总和之后，我们加上前一个窗口的最大总和，如果它大于当前最大值，则更新它，否则不更新。
以下是上述方法的实施:

## C++

```
// C++ program to find largest subarray sum with
// at-least k elements in it.
#include<bits/stdc++.h>
using namespace std;

// Returns maximum sum of a subarray with at-least
// k elements.
int maxSumWithK(int a[], int n, int k)
{
    // maxSum[i] is going to store maximum sum
    // till index i such that a[i] is part of the
    // sum.
    int maxSum[n];
    maxSum[0] = a[0];

    // We use Kadane's algorithm to fill maxSum[]
    // Below code is taken from method 3 of
    // https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/
    int curr_max = a[0];
    for (int i = 1; i < n; i++)
    {
        curr_max = max(a[i], curr_max+a[i]);
        maxSum[i] = curr_max;
    }

    // Sum of first k elements
    int sum = 0;
    for (int i = 0; i < k; i++)
        sum += a[i];

    // Use the concept of sliding window
    int result = sum;
    for (int i = k; i < n; i++)
    {
        // Compute sum of k elements ending
        // with a[i].
        sum = sum + a[i] - a[i-k];

        // Update result if required
        result = max(result, sum);

        // Include maximum sum till [i-k] also
        // if it increases overall max.
        result = max(result, sum + maxSum[i-k]);
    }
    return result;
}

// Driver code
int main()
{
    int a[] = {1, 2, 3, -10, -3};
    int k = 4;
    int n = sizeof(a)/sizeof(a[0]);
    cout << maxSumWithK(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest subarray sum with
// at-least k elements in it.
class Test
{
    // Returns maximum sum of a subarray with at-least
    // k elements.
    static int maxSumWithK(int a[], int n, int k)
    {
        // maxSum[i] is going to store maximum sum
        // till index i such that a[i] is part of the
        // sum.
        int maxSum[] = new int [n];
        maxSum[0] = a[0];

        // We use Kadane's algorithm to fill maxSum[]
        // Below code is taken from method 3 of
        // https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/
        int curr_max = a[0];
        for (int i = 1; i < n; i++)
        {
            curr_max = Math.max(a[i], curr_max+a[i]);
            maxSum[i] = curr_max;
        }

        // Sum of first k elements
        int sum = 0;
        for (int i = 0; i < k; i++)
            sum += a[i];

        // Use the concept of sliding window
        int result = sum;
        for (int i = k; i < n; i++)
        {
            // Compute sum of k elements ending
            // with a[i].
            sum = sum + a[i] - a[i-k];

            // Update result if required
            result = Math.max(result, sum);

            // Include maximum sum till [i-k] also
            // if it increases overall max.
            result = Math.max(result, sum + maxSum[i-k]);
        }
        return result;
    }

    // Driver method
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 3, -10, -3};
        int k = 4;
        System.out.println(maxSumWithK(arr, arr.length, k));;
    }
}
```

## 蟒蛇 3

```
# Python3 program to find largest subarray
# sum with at-least k elements in it.

# Returns maximum sum of a subarray
#  with at-least k elements.
def maxSumWithK(a, n, k):

    # maxSum[i] is going to store
    # maximum sum till index i such
    # that a[i] is part of the sum.
    maxSum = [0 for i in range(n)]
    maxSum[0] = a[0]

    # We use Kadane's algorithm to fill maxSum[]
    # Below code is taken from method3 of
    # https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/
    curr_max = a[0]
    for i in range(1, n):

        curr_max = max(a[i], curr_max + a[i])
        maxSum[i] = curr_max

    # Sum of first k elements
    sum = 0
    for i in range(k):
        sum += a[i]

    # Use the concept of sliding window
    result = sum
    for i in range(k, n):

        # Compute sum of k elements
        # ending with a[i].
        sum = sum + a[i] - a[i-k]

        # Update result if required
        result = max(result, sum)

        # Include maximum sum till [i-k] also
        # if it increases overall max.
        result = max(result, sum + maxSum[i-k])

    return result

# Driver code
a = [1, 2, 3, -10, -3]
k = 4
n = len(a)
print(maxSumWithK(a, n, k))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find largest subarray sum with
// at-least k elements in it.

using System;
class Test
{
    // Returns maximum sum of a subarray with at-least
    // k elements.
    static int maxSumWithK(int[] a, int n, int k)
    {
        // maxSum[i] is going to store maximum sum
        // till index i such that a[i] is part of the
        // sum.
        int[] maxSum = new int [n];
        maxSum[0] = a[0];

        // We use Kadane's algorithm to fill maxSum[]
        // Below code is taken from method 3 of
        // https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/
        int curr_max = a[0];
        for (int i = 1; i < n; i++)
        {
            curr_max = Math.Max(a[i], curr_max+a[i]);
            maxSum[i] = curr_max;
        }

        // Sum of first k elements
        int sum = 0;
        for (int i = 0; i < k; i++)
            sum += a[i];

        // Use the concept of sliding window
        int result = sum;
        for (int i = k; i < n; i++)
        {
            // Compute sum of k elements ending
            // with a[i].
            sum = sum + a[i] - a[i-k];

            // Update result if required
            result = Math.Max(result, sum);

            // Include maximum sum till [i-k] also
            // if it increases overall max.
            result = Math.Max(result, sum + maxSum[i-k]);
        }
        return result;
    }

    // Driver method
    public static void Main()
    {
        int[] arr = {1, 2, 3, -10, -3};
        int k = 4;
        Console.Write(maxSumWithK(arr, arr.Length, k));;
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find largest subarray
// sum with at-least k elements in it.

// Returns maximum sum of a subarray
// with at-least k elements.
function maxSumWithK($a, $n, $k)
{

    // maxSum[i] is going to
    // store maximum sum till
    // index i such that a[i]
    // is part of the sum.
    $maxSum[0] = $a[0];

    // We use Kadane's algorithm
    // to fill maxSum[]
    $curr_max = $a[0];
    for ($i = 1; $i < $n; $i++)
    {
        $curr_max = max($a[$i], $curr_max+$a[$i]);
        $maxSum[$i] = $curr_max;
    }

    // Sum of first k elements
    $sum = 0;
    for ($i = 0; $i < $k; $i++)
        $sum += $a[$i];

    // Use the concept of
    // sliding window
    $result = $sum;
    for ($i = $k; $i < $n; $i++)
    {
        // Compute sum of k
        // elements ending
        // with a[i].
        $sum = $sum + $a[$i] - $a[$i - $k];

        // Update result if required
        $result = max($result, $sum);

        // Include maximum sum till [i-k] also
        // if it increases overall max.
        $result = max($result, $sum +
                    $maxSum[$i - $k]);
    }
    return $result;
}

    // Driver code
    $a= array (1, 2, 3, -10, -3);
    $k = 4;
    $n = sizeof($a);
    echo maxSumWithK($a, $n, $k);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
    // Javascript program to find largest subarray sum with
    // at-least k elements in it.

    // Returns maximum sum of a subarray with at-least
    // k elements.
    function maxSumWithK(a, n, k)
    {
        // maxSum[i] is going to store maximum sum
        // till index i such that a[i] is part of the
        // sum.
        let maxSum = new Array(n);
        maxSum[0] = a[0];

        // We use Kadane's algorithm to fill maxSum[]
        // Below code is taken from method 3 of
        // https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/
        let curr_max = a[0];
        for (let i = 1; i < n; i++)
        {
            curr_max = Math.max(a[i], curr_max+a[i]);
            maxSum[i] = curr_max;
        }

        // Sum of first k elements
        let sum = 0;
        for (let i = 0; i < k; i++)
            sum += a[i];

        // Use the concept of sliding window
        let result = sum;
        for (let i = k; i < n; i++)
        {
            // Compute sum of k elements ending
            // with a[i].
            sum = sum + a[i] - a[i-k];

            // Update result if required
            result = Math.max(result, sum);

            // Include maximum sum till [i-k] also
            // if it increases overall max.
            result = Math.max(result, sum + maxSum[i-k]);
        }
        return result;
    }

    let arr = [1, 2, 3, -10, -3];
    let k = 4;
    document.write(maxSumWithK(arr, arr.length, k));

    // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
-4
```

这里有另一种方法:

1)我们将首先计算 k 个数字的总和，并将其存储在总和中。

2)然后我们取另一个变量“last”，用零初始化。这个“最后”变量将存储以前数字的总和。

3)现在循环 i = k 到 i

## C++

```
long long int maxSumWithK(long long int a[], long long int n, long long int k)
{
    long long int sum = 0;
    for(long long int i = 0; i<k; i++){
        sum += a[i];
    }

    long long int last = 0;
    long long int j = 0;
    long long int ans = LLONG_MIN;
    ans = max(ans,sum);
    for(long long int i = k; i<n; i++){
        sum = sum + a[i];
        last = last + a[j++];
        ans = max(ans,sum);
        if(last<0){
            sum = sum-last;
            ans = max(ans,sum);
            last = 0;
        }
    }
    return ans;
}
```

**时间复杂度:** O(n)
本文由**拉克什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。