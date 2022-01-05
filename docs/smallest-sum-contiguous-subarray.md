# 最小和连续子阵列

> 原文:[https://www . geesforgeks . org/minist-sum-continuous-subarray/](https://www.geeksforgeeks.org/smallest-sum-contiguous-subarray/)

给定一个包含 **n** 个整数的数组。问题是找到具有最小和的相邻子阵列的元素的和。
示例:

```
Input : arr[] = {3, -4, 2, -3, -1, 7, -5}
Output : -6
Subarray is {-4, 2, -3, -1} = -6

Input : arr = {2, 6, 8, 1, 4}
Output : 1
```

**天真方法:**考虑所有大小不同的邻接子阵，求其和。具有最小(最小)和的子阵列是必需的答案。
**高效方法:**它是基于卡丹算法思想的[最大和邻接子阵](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)问题的变种。
**算法:**

```
smallestSumSubarr(arr, n)
    Initialize min_ending_here = INT_MAX
    Initialize min_so_far = INT_MAX

    for i = 0 to n-1
        if min_ending_here > 0
            min_ending_here = arr[i]        
        else
            min_ending_here += arr[i]
        min_so_far = min(min_so_far, min_ending_here)

    return min_so_far
```

## C++

```
// C++ implementation to find the smallest sum
// contiguous subarray
#include <bits/stdc++.h>

using namespace std;

// function to find the smallest sum contiguous subarray
int smallestSumSubarr(int arr[], int n)
{
    // to store the minimum value that is ending
    // up to the current index
    int min_ending_here = INT_MAX;

    // to store the minimum value encountered so far
    int min_so_far = INT_MAX;

    // traverse the array elements
    for (int i=0; i<n; i++)
    {
        // if min_ending_here > 0, then it could not possibly
        // contribute to the minimum sum further
        if (min_ending_here > 0)
            min_ending_here = arr[i];

        // else add the value arr[i] to min_ending_here   
        else
            min_ending_here += arr[i];

        // update min_so_far
        min_so_far = min(min_so_far, min_ending_here);           
    }

    // required smallest sum contiguous subarray value
    return min_so_far;
}

// Driver program to test above
int main()
{
    int arr[] = {3, -4, 2, -3, -1, 7, -5};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Smallest sum: "
         << smallestSumSubarr(arr, n);
    return 0;    
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the smallest sum
// contiguous subarray
class GFG {

    // function to find the smallest sum contiguous
    // subarray
    static int smallestSumSubarr(int arr[], int n)
    {

        // to store the minimum value that is
        // ending up to the current index
        int min_ending_here = 2147483647;

        // to store the minimum value encountered
        // so far
        int min_so_far = 2147483647;

        // traverse the array elements
        for (int i = 0; i < n; i++)
        {

            // if min_ending_here > 0, then it could
            // not possibly contribute to the
            // minimum sum further
            if (min_ending_here > 0)
                min_ending_here = arr[i];

            // else add the value arr[i] to
            // min_ending_here
            else
                min_ending_here += arr[i];

            // update min_so_far
            min_so_far = Math.min(min_so_far,
                                   min_ending_here);        
        }

        // required smallest sum contiguous
        // subarray value
        return min_so_far;
    }

    // Driver method
    public static void main(String[] args)
    {

        int arr[] = {3, -4, 2, -3, -1, 7, -5};
        int n = arr.length;

        System.out.print("Smallest sum: "
                + smallestSumSubarr(arr, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to find the smallest sum
# contiguous subarray
import sys

# function to find the smallest sum
# contiguous subarray
def smallestSumSubarr(arr, n):
    # to store the minimum value that is ending
    # up to the current index
    min_ending_here = sys.maxsize

    # to store the minimum value encountered so far
    min_so_far = sys.maxsize

    # traverse the array elements
    for i in range(n):
        # if min_ending_here > 0, then it could not possibly
        # contribute to the minimum sum further
        if (min_ending_here > 0):
            min_ending_here = arr[i]

        # else add the value arr[i] to min_ending_here
        else:
            min_ending_here += arr[i]

        # update min_so_far
        min_so_far = min(min_so_far, min_ending_here)

    # required smallest sum contiguous subarray value
    return min_so_far

# Driver code
arr = [3, -4, 2, -3, -1, 7, -5]
n = len(arr)
print "Smallest sum: ", smallestSumSubarr(arr, n)

# This code is contributed by Sachin Bisht
```

## C#

```
// C# implementation to find the
// smallest sum contiguous subarray
using System;

class GFG {

    // function to find the smallest sum
    // contiguous subarray
    static int smallestSumSubarr(int[] arr, int n)
    {
        // to store the minimum value that is
        // ending up to the current index
        int min_ending_here = 2147483647;

        // to store the minimum value encountered
        // so far
        int min_so_far = 2147483647;

        // traverse the array elements
        for (int i = 0; i < n; i++) {

            // if min_ending_here > 0, then it could
            // not possibly contribute to the
            // minimum sum further
            if (min_ending_here > 0)
                min_ending_here = arr[i];

            // else add the value arr[i] to
            // min_ending_here
            else
                min_ending_here += arr[i];

            // update min_so_far
            min_so_far = Math.Min(min_so_far,
                                min_ending_here);
        }

        // required smallest sum contiguous
        // subarray value
        return min_so_far;
    }

    // Driver method
    public static void Main()
    {

        int[] arr = { 3, -4, 2, -3, -1, 7, -5 };
        int n = arr.Length;

        Console.Write("Smallest sum: " +
             smallestSumSubarr(arr, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the
// smallest sum contiguous subarray

// function to find the smallest
// sum contiguous subarray
function smallestSumSubarr($arr, $n)
{

    // to store the minimum
    // value that is ending
    // up to the current index
    $min_ending_here = 999999;

    // to store the minimum value
    // encountered so far
    $min_so_far = 999999;

    // traverse the array elements
    for($i = 0; $i < $n; $i++)
    {

        // if min_ending_here > 0,
        // then it could not possibly
        // contribute to the minimum
        // sum further
        if ($min_ending_here > 0)
            $min_ending_here = $arr[$i];

        // else add the value arr[i]
        // to min_ending_here
        else
            $min_ending_here += $arr[$i];

        // update min_so_far
        $min_so_far = min($min_so_far,
                     $min_ending_here);        
    }

    // required smallest sum
    // contiguous subarray value
    return $min_so_far;
}

    // Driver Code
    $arr = array(3, -4, 2, -3, -1, 7, -5);
    $n = count($arr) ;
    echo "Smallest sum: "
         .smallestSumSubarr($arr, $n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation to find the
    // smallest sum contiguous subarray

    // function to find the smallest sum
    // contiguous subarray
    function smallestSumSubarr(arr, n)
    {
        // to store the minimum value that is
        // ending up to the current index
        let min_ending_here = 2147483647;

        // to store the minimum value encountered
        // so far
        let min_so_far = 2147483647;

        // traverse the array elements
        for (let i = 0; i < n; i++) {

            // if min_ending_here > 0, then it could
            // not possibly contribute to the
            // minimum sum further
            if (min_ending_here > 0)
                min_ending_here = arr[i];

            // else add the value arr[i] to
            // min_ending_here
            else
                min_ending_here += arr[i];

            // update min_so_far
            min_so_far = Math.min(min_so_far,
                                min_ending_here);
        }

        // required smallest sum contiguous
        // subarray value
        return min_so_far;
    }

    let arr = [ 3, -4, 2, -3, -1, 7, -5 ];
    let n = arr.length;

    document.write("Smallest sum: " +
                  smallestSumSubarr(arr, n));

</script>
```

**输出:**

```
Smallest sum: -6
```

时间复杂度:O(n)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。