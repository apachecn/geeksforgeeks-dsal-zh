# 在几乎排序的数组中搜索

> 原文:[https://www.geeksforgeeks.org/search-almost-sorted-array/](https://www.geeksforgeeks.org/search-almost-sorted-array/)

给定一个已排序的数组，但是在排序之后，一些元素被移动到相邻的位置，即 arr[i]可能出现在 arr[i+1]或 arr[i-1]处。编写一个高效的函数来搜索这个数组中的元素。基本上，arr[i]元素只能与 arr[i+1]或 arr[i-1]交换。
例如，考虑阵列{2，3，10，4，40}，4 移动到下一个位置，10 移动到前一个位置。
**例:**

```
Input: arr[] =  {10, 3, 40, 20, 50, 80, 70}, key = 40
Output: 2 
Output is index of 40 in given array

Input: arr[] =  {10, 3, 40, 20, 50, 80, 70}, key = 90
Output: -1
-1 is returned to indicate element is not present
```

一个简单的解决方案是在给定的数组中线性搜索给定的键。这个解的时间复杂度是 O(n)。我们可以修改[二分搜索法](http://geeksquiz.com/binary-search/)在 O(Logn)时间内完成。
我们的想法是将关键字与中间 3 个元素进行比较，如果存在，则返回索引。如果不存在，那么将该键与中间元素进行比较，以决定是进入左半部分还是右半部分。与中间元素进行比较就足够了，因为 mid+2 之后的所有元素必须大于元素 mid，mid-2 之前的所有元素必须小于元素 mid。
以下是本办法的实施情况。

## C++

```
// C++ program to find an element
// in an almost sorted array
#include <stdio.h>

// A recursive binary search based function.
// It returns index of x in given array
// arr[l..r] is present, otherwise -1
int binarySearch(int arr[], int l, int r, int x)
{
if (r >= l)
{
        int mid = l + (r - l) / 2;

        // If the element is present at
        // one of the middle 3 positions
        if (arr[mid] == x)
            return mid;
        if (mid > l && arr[mid - 1] == x)
            return (mid - 1);
        if (mid < r && arr[mid + 1] == x)
            return (mid + 1);

        // If element is smaller than mid, then
        // it can only be present in left subarray
        if (arr[mid] > x)
            return binarySearch(arr, l, mid - 2, x);

        // Else the element can only be present
        // in right subarray
        return binarySearch(arr, mid + 2, r, x);
}

// We reach here when element is not present in array
return -1;
}

// Driver Code
int main(void)
{
int arr[] = {3, 2, 10, 4, 40};
int n = sizeof(arr) / sizeof(arr[0]);
int x = 4;
int result = binarySearch(arr, 0, n - 1, x);
(result == -1) ? printf("Element is not present in array")
               : printf("Element is present at index %d",
                         result);
return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find an element
// in an almost sorted array
class GFG
{
    // A recursive binary search based function.
    // It returns index of x in given array
    // arr[l..r] is present, otherwise -1
    int binarySearch(int arr[], int l, int r, int x)
    {
        if (r >= l)
        {
            int mid = l + (r - l) / 2;

            // If the element is present at
            // one of the middle 3 positions
            if (arr[mid] == x)
                return mid;
            if (mid > l && arr[mid - 1] == x)
                return (mid - 1);
            if (mid < r && arr[mid + 1] == x)
                return (mid + 1);

            // If element is smaller than mid, then
            // it can only be present in left subarray
            if (arr[mid] > x)
                return binarySearch(arr, l, mid - 2, x);

            // Else the element can only be present
            // in right subarray
            return binarySearch(arr, mid + 2, r, x);
        }

        // We reach here when element is
        // not present in array
        return -1;
    }

    // Driver code
    public static void main(String args[])
    {
        GFG ob = new GFG();
        int arr[] = {3, 2, 10, 4, 40};
        int n = arr.length;
        int x = 4;
        int result = ob.binarySearch(arr, 0, n - 1, x);
        if(result == -1)
            System.out.println("Element is not present in array");
        else
            System.out.println("Element is present at index " +
                                result);
    }
}

// This code is contributed by Rajat Mishra
```

## 蟒蛇 3

```
# Python 3 program to find an element
# in an almost sorted array

# A recursive binary search based function.
# It returns index of x in given array arr[l..r]
# is present, otherwise -1
def binarySearch(arr, l, r, x):

    if (r >= l):

        mid = int(l + (r - l) / 2)

        # If the element is present at one
        # of the middle 3 positions
        if (arr[mid] == x): return mid
        if (mid > l and arr[mid - 1] == x):
            return (mid - 1)
        if (mid < r and arr[mid + 1] == x):
            return (mid + 1)

        # If element is smaller than mid, then
        # it can only be present in left subarray
        if (arr[mid] > x):
            return binarySearch(arr, l, mid - 2, x)

        # Else the element can only
        # be present in right subarray
        return binarySearch(arr, mid + 2, r, x)

    # We reach here when element
    # is not present in array
    return -1

# Driver Code
arr = [3, 2, 10, 4, 40]
n = len(arr)
x = 4
result = binarySearch(arr, 0, n - 1, x)
if (result == -1):
    print("Element is not present in array")
else:
    print("Element is present at index", result)

# This code is contributed by Smitha Dinesh Semwal.
```

## C#

```
// C# program to find an element
// in an almost sorted array
using System;

class GFG
{
    // A recursive binary search based function.
    // It returns index of x in given array
    // arr[l..r] is present, otherwise -1
    int binarySearch(int []arr, int l, int r, int x)
    {
        if (r >= l)
        {
            int mid = l + (r - l) / 2;

            // If the element is present at
            // one of the middle 3 positions
            if (arr[mid] == x)
                return mid;
            if (mid > l && arr[mid - 1] == x)
                return (mid - 1);
            if (mid < r && arr[mid + 1] == x)
                return (mid + 1);

            // If element is smaller than mid, then
            // it can only be present in left subarray
            if (arr[mid] > x)
                return binarySearch(arr, l, mid - 2, x);

            // Else the element can only be present
            // in right subarray
            return binarySearch(arr, mid + 2, r, x);
        }

        // We reach here when element is
        // not present in array
        return -1;
    }

    // Driver code
    public static void Main()
    {
        GFG ob = new GFG();
        int []arr = {3, 2, 10, 4, 40};
        int n = arr.Length;
        int x = 4;
        int result = ob.binarySearch(arr, 0, n - 1, x);
        if(result == -1)
            Console.Write("Element is not present in array");
        else
            Console.Write("Element is present at index " +
                           result);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find an element
// in an almost sorted array

// A recursive binary search based function.
// It returns index of x in given array
// arr[l..r] is present, otherwise -1
function binarySearch($arr, $l, $r, $x)
{
    if ($r >= $l)
    {
        $mid = $l + ($r - $l) / 2;

        // If the element is present at
        // one of the middle 3 positions
        if ($arr[$mid] == $x)
            return $mid;
        if ($mid > $l && $arr[$mid - 1] == $x)
            return ($mid - 1);
        if ($mid < $r && $arr[$mid + 1] == $x)
            return ($mid + 1);

        // If element is smaller than mid, then
        // it can only be present in left subarray
        if ($arr[$mid] > $x)
            return binarySearch($arr, $l,
                           $mid - 2, $x);

        // Else the element can only be present
        // in right subarray
        return binarySearch($arr, $mid + 2,
                                    $r, $x);
}

// We reach here when element
// is not present in array
return -1;
}

// Driver Code
$arr = array(3, 2, 10, 4, 40);
$n = sizeof($arr);
$x = 4;
$result = binarySearch($arr, 0, $n - 1, $x);
if($result == -1)
    echo("Element is not present in array");
else
    echo("Element is present at index $result");

//This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// Javascript program to find an element
// in an almost sorted array

// A recursive binary search based function.
    // It returns index of x in given array
    // arr[l..r] is present, otherwise -1
function binarySearch(arr,l,r,x)
{
    if (r >= l)
        {
            let mid = l + Math.floor((r - l) / 2);

            // If the element is present at
            // one of the middle 3 positions
            if (arr[mid] == x)
                return mid;
            if (mid > l && arr[mid - 1] == x)
                return (mid - 1);
            if (mid < r && arr[mid + 1] == x)
                return (mid + 1);

            // If element is smaller than mid, then
            // it can only be present in left subarray
            if (arr[mid] > x)
                return binarySearch(arr, l, mid - 2, x);

            // Else the element can only be present
            // in right subarray
            return binarySearch(arr, mid + 2, r, x);
        }

        // We reach here when element is
        // not present in array
        return -1;
}

// Driver code
let arr=[3, 2, 10, 4, 40];
let n = arr.length;
let x = 4;
let result = binarySearch(arr, 0, n - 1, x);
if(result == -1)
    document.write("Element is not present in array<br>");
else
    document.write("Element is present at index " +
                   result+"<br>");

// This code is contributed by unknown2108
</script>
```

**输出:**

```
Element is present at index 3
```

上述函数的时间复杂度为 O(Logn)。

本文由 **Abhishek** 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息