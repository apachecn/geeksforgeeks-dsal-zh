# 最长递增圆形子阵列的长度

> 原文:[https://www . geesforgeks . org/length-最长-递增-圆形-subarray/](https://www.geeksforgeeks.org/length-longest-increasing-circular-subarray/)

给定一个包含 **n 个**数字的数组。问题是以循环的方式找到最长的连续子阵列的长度，使得子阵列中的每个元素都严格大于它在同一子阵列中的前一个元素。时间复杂度应为 0(n)。

**示例:**

```
Input : arr[] = {2, 3, 4, 5, 1}
Output : 5
{2, 3, 4, 5, 1} is the subarray if we circularly
start from the last element and then take the
first four elements. This will give us an increasing
subarray {1, 2, 3, 4, 5} in a circular manner.

Input : arr[] = {2, 3, 8, 4, 6, 7, 10, 12, 9, 1}
Output : 5
```

**方法 1(使用额外空间):**制作一个大小为 2*n 的 temp[]数组，在 temp[]中复制 arr[]的元素两次。现在，在温度[]中找到[最长递增子阵列](https://www.geeksforgeeks.org/longest-increasing-subarray/)的长度。

**方法 2(不使用额外空间):**以下是步骤:

1.  如果 n == 1，返回 1。
2.  从 arr[]的第一个元素开始查找最长递增子阵列的长度。让它的长度为 **startLen** 。
3.  从第一个递增子阵结束的下一个元素开始，求最长递增子阵的[长度。让它成为**最大**。](https://www.geeksforgeeks.org/longest-increasing-subarray/)
4.  考虑以 arr[]的最后一个元素结束的递增子阵列的长度。让它成为 **endLen** 。
5.  如果 arr[n-1] < arr[0], then **继续** =继续+开始。
6.  最后，返回最大值(max，endLen，startLen)。

## C++

```
// C++ implementation to find length of longest
// increasing circular subarray
#include <bits/stdc++.h>
using namespace std;

// function to find length of longest
// increasing circular subarray
int longlenCircularSubarr(int arr[], int n)
{
    // if there is only one element
    if (n == 1)
        return 1;

    // 'startLen' stores the length of the longest
    // increasing subarray which starts from
    // first element
    int startLen = 1, i;
    int len = 1, max = 0;

    // finding the length of the longest
    // increasing subarray starting from
    // first element
    for (i = 1; i < n; i++) {
        if (arr[i - 1] < arr[i])
            startLen++;
        else
            break;
    }

    if (max < startLen)
        max = startLen;

    // traverse the array index (i+1)
    for (int j = i + 1; j < n; j++) {

        // if current element if greater than previous
        // element, then this element helps in building
        // up the previous increasing subarray encountered
        // so far
        if (arr[j - 1] < arr[j])
            len++;
        else {

            // check if 'max' length is less than the length
            // of the current increasing subarray. If true,
            // then update 'max'
            if (max < len)
                max = len;

            // reset 'len' to 1 as from this element
            // again the length of the new increasing
            // subarray is being calculated
            len = 1;
        }
    }

    // if true, then add length of the increasing
    // subarray ending at last element with the
    // length of the increasing subarray starting
    // from first element - This is done for
    // circular rotation
    if (arr[n - 1] < arr[0])
        len += startLen;

    // check if 'max' length is less than the length
    // of the current increasing subarray. If true,
    // then update 'max'
    if (max < len)
        max = len;

    return max;
}

// Driver program to test above
int main()
{
    int arr[] = { 2, 3, 4, 5, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Length = "
         << longlenCircularSubarr(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find length
// of longest increasing circular subarray

class Circular
{
    // function to find length of longest
    // increasing circular subarray
    public static int longlenCircularSubarr(int arr[],
                                               int n)
    {
        // if there is only one element
        if (n == 1)
            return 1;

        // 'startLen' stores the length of the
        // longest increasing subarray which
        // starts from first element
        int startLen = 1, i;
        int len = 1, max = 0;

        // finding the length of the longest
        // increasing subarray starting from
        // first element
        for (i = 1; i < n; i++) {
            if (arr[i - 1] < arr[i])
                startLen++;
            else
                break;
        }

        if (max < startLen)
            max = startLen;

        // traverse the array index (i+1)
        for (int j = i + 1; j < n; j++) {

            // if current element if greater than
            // previous element, then this element
            // helps in building up the previous
            // increasing subarray encountered so far
            if (arr[j - 1] < arr[j])
                len++;
            else {

                // check if 'max' length is less than
                // the length of the current increasing
                // subarray. If true, then update 'max'
                if (max < len)
                    max = len;

                // reset 'len' to 1 as from this element
                // again the length of the new increasing
                // subarray is being calculated
                len = 1;
            }
        }

        // if true, then add length of the increasing
        // subarray ending at last element with the
        // length of the increasing subarray starting
        // from first element - This is done for
        // circular rotation
        if (arr[n - 1] < arr[0])
            len += startLen;

        // check if 'max' length is less than the
        // length of the current increasing subarray.
        // If true, then update 'max'
        if (max < len)
            max = len;

        return max;
    }

    // driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 4, 5, 1 };
        int n = 5;
        System.out.print("Length = "+
                      longlenCircularSubarr(arr, n));
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 implementation to find length
# of longest increasing circular subarray

# function to find length of longest
# increasing circular subarray
def longlenCircularSubarr (arr, n):

    # if there is only one element
    if n == 1:
        return 1

    # 'startLen' stores the length of the
    # longest increasing subarray which
    # starts from first element
    startLen = 1

    len = 1
    max = 0

    # finding the length of the longest
    # increasing subarray starting from
    # first element
    for i in range(1, n):
        if arr[i - 1] < arr[i]:
            startLen+=1
        else:
            break

    if max < startLen:
        max = startLen

    # traverse the array index (i+1)
    for j in range(i + 1, n):

        # if current element if greater than
        # previous element, then this element
        # helps in building up the previous
        # increasing subarray encountered
        # so far
        if arr[j - 1] < arr[j]:
            len+=1
        else:
            # check if 'max' length is less
            # than the length of the current
            # increasing subarray. If true,
            # then update 'max'
            if max < len:
                max = len

            # reset 'len' to 1 as from this
            # element again the length of the
            # new increasing subarray is
            # being calculated
            len = 1

    # if true, then add length of the increasing
    # subarray ending at last element with the
    # length of the increasing subarray starting
    # from first element - This is done for
    # circular rotation
    if arr[n - 1] < arr[0]:
        len += startLen

    # check if 'max' length is less than the
    # length of the current increasing subarray.
    # If true, then update 'max'
    if max < len:
        max = len

    return max

# Driver code to test above
arr = [ 2, 3, 4, 5, 1 ]
n = len(arr)
print("Length = ",longlenCircularSubarr(arr, n))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# implementation to find length
// of longest increasing circular subarray
using System;

public class GFG {

    // function to find length of longest
    // increasing circular subarray
    static int longlenCircularSubarr(int[] arr, int n)
    {
        // if there is only one element
        if (n == 1)
            return 1;

        // 'startLen' stores the length of the longest
        // increasing subarray which starts from
        // first element
        int startLen = 1, i;
        int len = 1, max = 0;

        // finding the length of the longest
        // increasing subarray starting from
        // first element
        for (i = 1; i < n; i++) {
            if (arr[i - 1] < arr[i])
                startLen++;
            else
                break;
        }

        if (max < startLen)
            max = startLen;

        // traverse the array index (i+1)
        for (int j = i + 1; j < n; j++) {

            // if current element if greater than previous
            // element, then this element helps in building
            // up the previous increasing subarray encountered
            // so far
            if (arr[j - 1] < arr[j])
                len++;
            else {

                // check if 'max' length is less than the length
                // of the current increasing subarray. If true,
                // then update 'max'
                if (max < len)
                    max = len;

                // reset 'len' to 1 as from this element
                // again the length of the new increasing
                // subarray is being calculated
                len = 1;
            }
        }

        // if true, then add length of the increasing
        // subarray ending at last element with the
        // length of the increasing subarray starting
        // from first element - This is done for
        // circular rotation
        if (arr[n - 1] < arr[0])
            len += startLen;

        // check if 'max' length is less than the length
        // of the current increasing subarray. If true,
        // then update 'max'
        if (max < len)
            max = len;

        return max;
    }

    // Driver program to test above
    static public void Main()
    {
        int[] arr = { 2, 3, 4, 5, 1 };
        int n = arr.Length;
        Console.WriteLine("Length = " +
                           longlenCircularSubarr(arr, n));
        // Code
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find length of longest
// increasing circular subarray

// function to find length of longest
// increasing circular subarray
function longlenCircularSubarr(&$arr, $n)
{
    // if there is only one element
    if ($n == 1)
        return 1;

    // 'startLen' stores the length of the longest
    // increasing subarray which starts from
    // first element
    $startLen = 1;
    $len = 1;
    $max = 0;

    // finding the length of the longest
    // increasing subarray starting from
    // first element
    for ($i = 1; $i < $n; $i++)
    {
        if ($arr[$i - 1] < $arr[$i])
            $startLen++;
        else
            break;
    }

    if ($max < $startLen)
        $max = $startLen;

    // traverse the array index (i+1)
    for ($j = $i + 1; $j < $n; $j++)
    {

        // if current element if greater than
        // previous element, then this element
        // helps in building up the previous
        // increasing subarray encountered
        // so far
        if ($arr[$j - 1] < $arr[$j])
            $len++;
        else
        {

            // check if 'max' length is less than
            // the length of the current increasing
            // subarray. If true, then update 'max'
            if ($max < $len)
                $max = $len;

            // reset 'len' to 1 as from this element
            // again the length of the new increasing
            // subarray is being calculated
            $len = 1;
        }
    }

    // if true, then add length of the increasing
    // subarray ending at last element with the
    // length of the increasing subarray starting
    // from first element - This is done for
    // circular rotation
    if ($arr[$n - 1] < $arr[0])
        $len += $startLen;

    // check if 'max' length is less than the length
    // of the current increasing subarray. If true,
    // then update 'max'
    if ($max < $len)
        $max = $len;

    return $max;
}

// Driver Code
$arr = array( 2, 3, 4, 5, 1 );
$n = sizeof($arr);
echo "Length = " . longlenCircularSubarr($arr, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find length
// of longest increasing circular subarray

     // function to find length of longest
    // increasing circular subarray
    function longlenCircularSubarr(arr,n)
    {
        // if there is only one element
        if (n == 1)
            return 1;

        // 'startLen' stores the length of the
        // longest increasing subarray which
        // starts from first element
        let startLen = 1, i;
        let len = 1, max = 0;

        // finding the length of the longest
        // increasing subarray starting from
        // first element
        for (i = 1; i < n; i++) {
            if (arr[i - 1] < arr[i])
                startLen++;
            else
                break;
        }

        if (max < startLen)
            max = startLen;

        // traverse the array index (i+1)
        for (let j = i + 1; j < n; j++) {

            // if current element if greater than
            // previous element, then this element
            // helps in building up the previous
            // increasing subarray encountered so far
            if (arr[j - 1] < arr[j])
                len++;
            else {

                // check if 'max' length is less than
                // the length of the current increasing
                // subarray. If true, then update 'max'
                if (max < len)
                    max = len;

                // reset 'len' to 1 as from this element
                // again the length of the new increasing
                // subarray is being calculated
                len = 1;
            }
        }

        // if true, then add length of the increasing
        // subarray ending at last element with the
        // length of the increasing subarray starting
        // from first element - This is done for
        // circular rotation
        if (arr[n - 1] < arr[0])
            len += startLen;

        // check if 'max' length is less than the
        // length of the current increasing subarray.
        // If true, then update 'max'
        if (max < len)
            max = len;

        return max;
    }

     // driver code
    let arr=[2, 3, 4, 5, 1 ];
    let n = 5;
    document.write("Length = "+
                      longlenCircularSubarr(arr, n));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Length = 5
```

**时间复杂度:** O(n)。