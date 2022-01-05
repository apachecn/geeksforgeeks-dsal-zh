# 求零的个数

> 原文:[https://www.geeksforgeeks.org/find-number-zeroes/](https://www.geeksforgeeks.org/find-number-zeroes/)

给定一个由 1 和 0 组成的数组，该数组首先包含所有的 1，然后包含所有的 0。求 0 的个数。计算给定数组中的零个数。
**例:**

```
Input: arr[] = {1, 1, 1, 1, 0, 0}
Output: 2

Input: arr[] = {1, 0, 0, 0, 0}
Output: 4

Input: arr[] = {0, 0, 0}
Output: 3

Input: arr[] = {1, 1, 1, 1}
Output: 0
```

一个**简单的解决方案**是遍历输入数组。一旦我们找到 0，我们就返回第一个 0 的 n-索引。这里 n 是输入数组中的元素个数。该解决方案的时间复杂度为 0(n)。
由于输入数组是排序的，所以我们可以使用 [**二分搜索法**来查找第一个出现的](https://www.geeksforgeeks.org/count-number-of-occurrences-in-a-sorted-array/)为 0。一旦我们有了第一个元素的索引，我们就可以将 count 作为第一个零的索引返回。

## C

```
// A divide and conquer solution to find count of zeroes in an array
// where all 1s are present before all 0s
#include <stdio.h>

/* if 0 is present in arr[] then returns the index of FIRST occurrence
of 0 in arr[low..high], otherwise returns -1 */
int firstZero(int arr[], int low, int high)
{
    if (high >= low)
    {
        // Check if mid element is first 0
        int mid = low + (high - low)/2;
        if (( mid == 0 || arr[mid-1] == 1) && arr[mid] == 0)
            return mid;

        if (arr[mid] == 1) // If mid element is not 0
            return firstZero(arr, (mid + 1), high);
        else // If mid element is 0, but not first 0
            return firstZero(arr, low, (mid -1));
    }
    return -1;
}

// A wrapper over recursive function firstZero()
int countZeroes(int arr[], int n)
{
    // Find index of first zero in given array
    int first = firstZero(arr, 0, n-1);

    // If 0 is not present at all, return 0
    if (first == -1)
        return 0;

    return (n - first);
}

/* Driver program to check above functions */
int main()
{
    int arr[] = {1, 1, 1, 0, 0, 0, 0, 0};
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("Count of zeroes is %d", countZeroes(arr, n));
    return 0;
}
```

## C++

```
// A divide and conquer solution to
// find count of zeroes in an array
// where all 1s are present before all 0s
#include <bits/stdc++.h>
using namespace std;

/* if 0 is present in arr[] then
returns the index of FIRST occurrence
of 0 in arr[low..high], otherwise returns -1 */
int firstZero(int arr[], int low, int high)
{
    if (high >= low)
    {
        // Check if mid element is first 0
        int mid = low + (high - low) / 2;
        if ((mid == 0 || arr[mid - 1] == 1) &&
                         arr[mid] == 0)
            return mid;

        // If mid element is not 0
        if (arr[mid] == 1)
            return firstZero(arr, (mid + 1), high);

        // If mid element is 0, but not first 0   
        else
            return firstZero(arr, low, (mid -1));
    }
    return -1;
}

// A wrapper over recursive function firstZero()
int countZeroes(int arr[], int n)
{
    // Find index of first zero in given array
    int first = firstZero(arr, 0, n - 1);

    // If 0 is not present at all, return 0
    if (first == -1)
        return 0;

    return (n - first);
}

// Driver Code
int main()
{
    int arr[] = {1, 1, 1, 0, 0, 0, 0, 0};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Count of zeroes is "
         << countZeroes(arr, n);
    return 0;
}

// This code is contributed by SoumikMondal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A divide and conquer solution to find count of zeroes in an array
// where all 1s are present before all 0s

class CountZeros
{
    /* if 0 is present in arr[] then returns the index of FIRST occurrence
       of 0 in arr[low..high], otherwise returns -1 */
    int firstZero(int arr[], int low, int high)
    {
        if (high >= low)
        {
            // Check if mid element is first 0
            int mid = low + (high - low) / 2;
            if ((mid == 0 || arr[mid - 1] == 1) && arr[mid] == 0)
                return mid;

            if (arr[mid] == 1) // If mid element is not 0
                return firstZero(arr, (mid + 1), high);
            else // If mid element is 0, but not first 0
                return firstZero(arr, low, (mid - 1));
        }
        return -1;
    }

    // A wrapper over recursive function firstZero()
    int countZeroes(int arr[], int n)
    {
        // Find index of first zero in given array
        int first = firstZero(arr, 0, n - 1);

        // If 0 is not present at all, return 0
        if (first == -1)
            return 0;

        return (n - first);
    }

    // Driver program to test above functions
    public static void main(String[] args)
    {
        CountZeros count = new CountZeros();
        int arr[] = {1, 1, 1, 0, 0, 0, 0, 0};
        int n = arr.length;
        System.out.println("Count of zeroes is " + count.countZeroes(arr, n));
    }
}
```

## 蟒蛇 3

```
# A divide and conquer solution to
# find count of zeroes in an array
# where all 1s are present before all 0s

# if 0 is present in arr[] then returns
# the index of FIRST occurrence of 0 in
# arr[low..high], otherwise returns -1
def firstZero(arr, low, high):

    if (high >= low):

        # Check if mid element is first 0
        mid = low + int((high - low) / 2)
        if (( mid == 0 or arr[mid-1] == 1)
                      and arr[mid] == 0):
            return mid

        # If mid element is not 0
        if (arr[mid] == 1):
            return firstZero(arr, (mid + 1), high)

        # If mid element is 0, but not first 0
        else:
            return firstZero(arr, low, (mid - 1))

    return -1

# A wrapper over recursive
# function firstZero()
def countZeroes(arr, n):

    # Find index of first zero in given array
    first = firstZero(arr, 0, n - 1)

    # If 0 is not present at all, return 0
    if (first == -1):
        return 0

    return (n - first)

# Driver Code
arr = [1, 1, 1, 0, 0, 0, 0, 0]
n = len(arr)
print("Count of zeroes is",
        countZeroes(arr, n))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// A divide and conquer solution to find
// count of zeroes in an array where all
// 1s are present before all 0s
using System;

class CountZeros
{
    /* if 0 is present in arr[] then returns
       the index of FIRST occurrence of 0 in
       arr[low..high], otherwise returns -1 */
    int firstZero(int []arr, int low, int high)
    {
        if (high >= low)
        {
            // Check if mid element is first 0
            int mid = low + (high - low) / 2;
            if ((mid == 0 || arr[mid - 1] == 1) &&
                                 arr[mid] == 0)
                return mid;

            if (arr[mid] == 1) // If mid element is not 0
                return firstZero(arr, (mid + 1), high);

            else // If mid element is 0, but not first 0
                return firstZero(arr, low, (mid - 1));
        }
        return -1;
    }

    // A wrapper over recursive function firstZero()
    int countZeroes(int []arr, int n)
    {
        // Find index of first zero in given array
        int first = firstZero(arr, 0, n - 1);

        // If 0 is not present at all, return 0
        if (first == -1)
            return 0;

        return (n - first);
    }

    // Driver program to test above functions
    public static void Main()
    {
        CountZeros count = new CountZeros();
        int []arr = {1, 1, 1, 0, 0, 0, 0, 0};
        int n = arr.Length;
        Console.Write("Count of zeroes is " +
                       count.countZeroes(arr, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A divide and conquer solution to
// find count of zeroes in an array
// where all 1s are present before all 0s

/* if 0 is present in arr[] then
   returns the index of FIRST
   occurrence of 0 in arr[low..high],
   otherwise returns -1 */
function firstZero($arr, $low, $high)
{
    if ($high >= $low)
    {

        // Check if mid element is first 0
        $mid = $low + floor(($high - $low)/2);

        if (( $mid == 0 || $arr[$mid-1] == 1) &&
                                 $arr[$mid] == 0)
            return $mid;

        // If mid element is not 0
        if ($arr[$mid] == 1)
            return firstZero($arr, ($mid + 1), $high);

        // If mid element is 0,
        // but not first 0   
        else
            return firstZero($arr, $low,
                            ($mid - 1));
    }
    return -1;
}

// A wrapper over recursive
// function firstZero()
function countZeroes($arr, $n)
{

    // Find index of first
    // zero in given array
    $first = firstZero($arr, 0, $n - 1);

    // If 0 is not present
    // at all, return 0
    if ($first == -1)
        return 0;

    return ($n - $first);
}

    // Driver Code
    $arr = array(1, 1, 1, 0, 0, 0, 0, 0);
    $n = sizeof($arr);
    echo("Count of zeroes is ");
    echo(countZeroes($arr, $n));

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// A divide and conquer solution to find count of zeroes in an array
// where all 1s are present before all 0s

    /*
     * if 0 is present in arr then returns the index of FIRST occurrence of 0 in
     * arr[low..high], otherwise returns -1
     */
    function firstZero(arr , low , high) {
        if (high >= low) {

            // Check if mid element is first 0
            var mid = low + parseInt((high - low) / 2);
            if ((mid == 0 || arr[mid - 1] == 1) && arr[mid] == 0)
                return mid;

            if (arr[mid] == 1) // If mid element is not 0
                return firstZero(arr, (mid + 1), high);
            else // If mid element is 0, but not first 0
                return firstZero(arr, low, (mid - 1));
        }
        return -1;
    }

    // A wrapper over recursive function firstZero()
    function countZeroes(arr , n)
    {

        // Find index of first zero in given array
        var first = firstZero(arr, 0, n - 1);

        // If 0 is not present at all, return 0
        if (first == -1)
            return 0;

        return (n - first);
    }

    // Driver program to test above functions

        var arr = [ 1, 1, 1, 0, 0, 0, 0, 0 ];
        var n = arr.length;
        document.write("Count of zeroes is " + countZeroes(arr, n));

// This code is contributed by gauravrajput1
</script>
```

输出:

```
Count of zeroes is 5 
```

时间复杂度:O(Logn)，其中 n 是 arr[]中的元素数量。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息