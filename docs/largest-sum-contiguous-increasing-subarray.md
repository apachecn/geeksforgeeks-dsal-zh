# 最大和连续递增子阵列

> 原文:[https://www . geesforgeks . org/maximum-sum-continuous-递增-subarray/](https://www.geeksforgeeks.org/largest-sum-contiguous-increasing-subarray/)

给定 n 个不同正整数的数组。问题是在 O(n)时间复杂度中寻找连续递增子阵的最大和。
**例:**

```
Input : arr[] = {2, 1, 4, 7, 3, 6}
Output : 12
Contiguous Increasing subarray {1, 4, 7} = 12

Input : arr[] = {38, 7, 8, 10, 12}
Output : 38
```

一个**简单的解决方案**是[生成所有子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)并计算它们的和。最后返回和最大的子阵。该方案的时间复杂度为 O(n <sup>2</sup> )。
一个**高效的解决方案**是基于所有元素都是正的事实。所以我们考虑最长递增子阵，并比较它们的和。为了增加子阵不能重叠，所以我们的时间复杂度变成了 O(n)。
**算法:**

```
Let arr be the array of size n
Let result be the required sum

int largestSum(arr, n) 
    result = INT_MIN  // Initialize result

    i = 0
    while i < n

        // Find sum of longest increasing subarray
        // starting with i
        curr_sum = arr[i];
    while i+1 < n && arr[i] < arr[i+1]
              curr_sum += arr[i+1];
          i++; 

        // If current sum is greater than current
        // result.
        if result < curr_sum
            result = curr_sum; 

        i++;
    return result
```

下面是上述算法的实现。

## C++

```
// C++ implementation of largest sum
// contiguous increasing subarray
#include <bits/stdc++.h>
using namespace std;

// Returns sum of longest
// increasing subarray.
int largestSum(int arr[], int n)
{
    // Initialize result
    int result = INT_MIN;

    // Note that i is incremented
    // by inner loop also, so overall
    // time complexity is O(n)
    for (int i = 0; i < n; i++)
    {
        // Find sum of longest
        // increasing subarray
        // starting from arr[i]
        int curr_sum = arr[i];
        while (i + 1 < n &&
               arr[i + 1] > arr[i])
        {
            curr_sum += arr[i + 1];
            i++;
        }

        // Update result if required
        if (curr_sum > result)
            result = curr_sum;
    }

    // required largest sum
    return result;
}

// Driver Code
int main()
{
    int arr[] = {1, 1, 4, 7, 3, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Largest sum = "
         << largestSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of largest sum
// contiguous increasing subarray

class GFG
{
    // Returns sum of longest
    // increasing subarray.
    static int largestSum(int arr[], int n)
    {
        // Initialize result
        int result = -9999999;

        // Note that i is incremented
        // by inner loop also, so overall
        // time complexity is O(n)
        for (int i = 0; i < n; i++)
        {
            // Find sum of longest
            // increasing subarray
            // starting from arr[i]
            int curr_sum = arr[i];
            while (i + 1 < n &&
                   arr[i + 1] > arr[i])
            {
                curr_sum += arr[i + 1];
                i++;
            }

            // Update result if required
            if (curr_sum > result)
                result = curr_sum;
        }

        // required largest sum
        return result;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = {1, 1, 4, 7, 3, 6};
        int n = arr.length;
        System.out.println("Largest sum = " +
                         largestSum(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of largest
# sum contiguous increasing subarray

# Returns sum of longest
# increasing subarray.
def largestSum(arr, n):

    # Initialize result
    result = -2147483648

    # Note that i is incremented
    # by inner loop also, so overall
    # time complexity is O(n)
    for i in range(n):

        # Find sum of longest increasing
        # subarray starting from arr[i]
        curr_sum = arr[i]
        while (i + 1 < n and
               arr[i + 1] > arr[i]):

            curr_sum += arr[i + 1]
            i += 1

        # Update result if required
        if (curr_sum > result):
            result = curr_sum

    # required largest sum
    return result

# Driver Code
arr = [1, 1, 4, 7, 3, 6]
n = len(arr)
print("Largest sum = ", largestSum(arr, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# implementation of largest sum
// contiguous increasing subarray
using System;

class GFG
{

    // Returns sum of longest
    // increasing subarray.
    static int largestSum(int []arr,
                          int n)
    {

        // Initialize result
        int result = -9999999;

        // Note that i is incremented by
        // inner loop also, so overall
        // time complexity is O(n)
        for (int i = 0; i < n; i++)
        {

            // Find sum of longest increasing
            // subarray starting from arr[i]
            int curr_sum = arr[i];
            while (i + 1 < n &&
                   arr[i + 1] > arr[i])
            {
                curr_sum += arr[i + 1];
                i++;
            }

            // Update result if required
            if (curr_sum > result)
                result = curr_sum;
        }

        // required largest sum
        return result;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {1, 1, 4, 7, 3, 6};
        int n = arr.Length;
        Console.Write("Largest sum = " +
                    largestSum(arr, n));
    }
}

// This code is contributed
// by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of largest sum
// contiguous increasing subarray

// Returns sum of longest
// increasing subarray.
function largestSum($arr, $n)
{
    $INT_MIN = 0;

    // Initialize result
    $result = $INT_MIN;

    // Note that i is incremented
    // by inner loop also, so overall
    // time complexity is O(n)
    for ($i = 0; $i < $n; $i++)
    {
        // Find sum of longest
        // increasing subarray
        // starting from arr[i]
        $curr_sum = $arr[$i];
        while ($i + 1 < $n &&
               $arr[$i + 1] > $arr[$i])
        {
            $curr_sum += $arr[$i + 1];
            $i++;
        }

        // Update result if required
        if ($curr_sum > $result)
            $result = $curr_sum;
    }

    // required largest sum
    return $result;
}

// Driver Code
{
    $arr = array(1, 1, 4, 7, 3, 6);
    $n = sizeof($arr) / sizeof($arr[0]);
    echo "Largest sum = " ,
          largestSum($arr, $n);
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of largest sum
// contiguous increasing subarray

// Returns sum of longest
// increasing subarray.
function largestSum(arr, n)
{
    // Initialize result
    var result = -1000000000;

    // Note that i is incremented
    // by inner loop also, so overall
    // time complexity is O(n)
    for (var i = 0; i < n; i++)
    {
        // Find sum of longest
        // increasing subarray
        // starting from arr[i]
        var curr_sum = arr[i];
        while (i + 1 < n &&
               arr[i + 1] > arr[i])
        {
            curr_sum += arr[i + 1];
            i++;
        }

        // Update result if required
        if (curr_sum > result)
            result = curr_sum;
    }

    // required largest sum
    return result;
}

// Driver Code
var arr = [1, 1, 4, 7, 3, 6];
var n = arr.length;
document.write( "Largest sum = "
      + largestSum(arr, n));

// This code is contributed by itsok.
</script>
```

**输出:**

```
Largest sum = 12
```

**时间复杂度:** O(n)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。