# 对排序旋转数组中小于或等于给定值的元素进行计数

> 原文:[https://www . geesforgeks . org/count-elements-less-equal-给定值-sorted-rotated-array/](https://www.geeksforgeeks.org/count-elements-less-equal-given-value-sorted-rotated-array/)

给定在某个点旋转的不同整数的排序数组。给定值 **x** 。问题是计算数组中所有小于或等于 **x** 的元素。
**举例:**

```
Input : arr[] = {4, 5, 8, 1, 3}, 
            x = 6
Output : 4

Input : arr[] = {6, 10, 12, 15, 2, 4, 5}, 
            x = 14
Output : 6
```

**天真方法:**逐个遍历数组的所有元素，统计小于或等于 **x** 的元素。时间复杂度为 0(n)。
**有效途径:**一个**修改的二分搜索法**的先决条件，它可以返回在**arr【l…h】**的排序范围内小于或等于给定值的最大元素的索引。
所需修改的二分搜索法参见[本](https://www.geeksforgeeks.org/element-1st-array-count-elements-less-equal-2nd-array/)帖:
**步骤:**

1.  查找旋转排序数组中最小元素的索引。参考[本](https://www.geeksforgeeks.org/find-minimum-element-in-a-sorted-and-rotated-array/)岗位。就这样吧 **min_index** 。
2.  如果 **x < = arr[n-1]** ，借助修改后的二分搜索法，在排序范围 **arr[min_index…n-1]** 中找到小于或等于 **x** 的最大元素的索引。
    让它成为**索引 1** 。现在，**计数**= index 1+1–min _ index。
3.  如果**0<=(min _ index-1)&&x<= arr【min _ index–1】**，借助修改后的二分搜索法，在排序范围**arr【0…min _ index-1】**中找到小于或等于 **x** 的最大元素的索引。让它成为**索引 2** 。现在，**计数**= n–min _ index+index 2+1。
4.  否则**计数** = n.

## C++

```
// C++ implementation to count elements less than or
// equal to a given value in a sorted rotated array
#include <bits/stdc++.h>

using namespace std;

// function to find the minimum element's index
int findMinIndex(int arr[], int low, int high)
{
    // This condition is needed to handle the case when
    // array is not rotated at all
    if (high < low)  return 0;

    // If there is only one element left
    if (high == low) return low;

    // Find mid
    int mid = (low + high) / 2;

    // Check if element (mid+1) is minimum element. Consider
    // the cases like {3, 4, 5, 1, 2}
    if (mid < high && arr[mid+1] < arr[mid])
       return (mid + 1);

    // Check if mid itself is minimum element
    if (mid > low && arr[mid] < arr[mid - 1])
       return mid;

    // Decide whether we need to go to left half or right half
    if (arr[high] > arr[mid])
       return findMinIndex(arr, low, mid-1);
    return findMinIndex(arr, mid+1, high);
}

// function returns the index of largest element
// smaller than equal to 'x' in 'arr[l...h]'.
// If no such element exits in the given range,
// then it returns l-1.
int binary_search(int arr[], int l, int h, int x)
{
    while (l <= h)
    {
        int mid = (l+h) / 2;

        // if 'x' is less than or equal to arr[mid],
        // then search in arr[mid+1...h]
        if (arr[mid] <= x)
            l = mid + 1;

        // else search in arr[l...mid-1]   
        else
            h = mid - 1;   
    }

    // required index
    return h;
}

// function to count elements less than
// or equal to a given value
int countEleLessThanOrEqual(int arr[], int n, int x)
{
    // index of the smallest element in the array
    int min_index = findMinIndex(arr, 0, n-1);

    // if largest element smaller than or equal to 'x' lies
    // in the sorted range arr[min_index...n-1]
    if (x <= arr[n-1])
        return (binary_search(arr, min_index, n-1, x) + 1 - min_index);

    // if largest element smaller than or equal to 'x' lies
    // in the sorted range arr[0...min_index-1]
    if ((min_index - 1) >= 0 && x <= arr[min_index - 1])
        return (n - min_index + binary_search(arr, 0, min_index-1, x) + 1);

    // else all the elements of the array
    // are less than 'x'   
    return n;               
}

// Driver program to test above
int main()
{
    int arr[] = {6, 10, 12, 15, 2, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    int x = 14;
    cout << "Count = "
         << countEleLessThanOrEqual(arr, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count elements
// less than or equal to a given
// value in a sorted rotated array

class GFG {

// function to find the minimum
// element's index
static int findMinIndex(int arr[], int low, int high)
{
    // This condition is needed to handle
    // the case when array is not rotated at all
    if (high < low)
    return 0;

    // If there is only one element left
    if (high == low)
    return low;

    // Find mid
    int mid = (low + high) / 2;

    // Check if element (mid+1) is
    // minimum element. Consider
    // the cases like {3, 4, 5, 1, 2}
    if (mid < high && arr[mid + 1] < arr[mid])
    return (mid + 1);

    // Check if mid itself is minimum element
    if (mid > low && arr[mid] < arr[mid - 1])
    return mid;

    // Decide whether we need to go to
    // left half or right half
    if (arr[high] > arr[mid])
    return findMinIndex(arr, low, mid - 1);
    return findMinIndex(arr, mid + 1, high);
}

// function returns the index of largest element
// smaller than equal to 'x' in 'arr[l...h]'.
// If no such element exits in the given range,
// then it returns l-1.
static int binary_search(int arr[], int l, int h, int x)
{
    while (l <= h) {
    int mid = (l + h) / 2;

    // if 'x' is less than or equal to arr[mid],
    // then search in arr[mid+1...h]
    if (arr[mid] <= x)
        l = mid + 1;

    // else search in arr[l...mid-1]
    else
        h = mid - 1;
    }

    // required index
    return h;
}

// function to count elements less than
// or equal to a given value
static int countEleLessThanOrEqual(int arr[], int n, int x)
{
    // index of the smallest element in the array
    int min_index = findMinIndex(arr, 0, n - 1);

    // if largest element smaller than or
    // equal to 'x' lies in the sorted
    // range arr[min_index...n-1]
    if (x <= arr[n - 1])
    return (binary_search(arr, min_index, n - 1, x) + 1 - min_index);

    // if largest element smaller than or
    // equal to 'x' lies in the sorted
    // range arr[0...min_index-1]
    if ((min_index - 1) >= 0 && x <= arr[min_index - 1])
    return (n - min_index + binary_search(arr, 0, min_index - 1, x) + 1);

    // else all the elements of the array
    // are less than 'x'
    return n;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {6, 10, 12, 15, 2, 4, 5};
    int n = arr.length;
    int x = 14;
    System.out.print("Count = " +
                      countEleLessThanOrEqual(arr, n, x));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python implementation to
# count elements less than or
# equal to a given value
# in a sorted rotated array

# function to find the
# minimum element's index
def findMinIndex(arr,low,high):

    # This condition is needed
    # to handle the case when
    # array is not rotated at all
    if (high < low):
        return 0

    # If there is only one element left
    if (high == low):
        return low

    # Find mid
    mid = (low + high) // 2

    # Check if element (mid+1) is
    # minimum element. Consider
    # the cases like {3, 4, 5, 1, 2}
    if (mid < high and arr[mid+1] < arr[mid]):
       return (mid + 1)

    # Check if mid itself
    # is minimum element
    if (mid > low and arr[mid] < arr[mid - 1]):
       return mid

    # Decide whether we need to
    # go to left half or right half
    if (arr[high] > arr[mid]):
       return findMinIndex(arr, low, mid-1)
    return findMinIndex(arr, mid+1, high)

# function returns the
# index of largest element
# smaller than equal to
# 'x' in 'arr[l...h]'.
# If no such element exits
# in the given range,
# then it returns l-1.
def binary_search(arr,l,h,x):

    while (l <= h):

        mid = (l+h) // 2

        # if 'x' is less than
        # or equal to arr[mid],
        # then search in arr[mid+1...h]
        if (arr[mid] <= x):
            l = mid + 1

        # else search in arr[l...mid-1]   
        else:
            h = mid - 1   

    # required index
    return h

# function to count
# elements less than
# or equal to a given value
def countEleLessThanOrEqual(arr,n,x):

    # index of the smallest
    # element in the array
    min_index = findMinIndex(arr, 0, n-1)

    # if largest element smaller
    # than or equal to 'x' lies
    # in the sorted range arr[min_index...n-1]
    if (x <= arr[n-1]):
        return (binary_search(arr, min_index, n-1, x) + 1 - min_index)

    # if largest element smaller
    # than or equal to 'x' lies
    # in the sorted range arr[0...min_index-1]
    if ((min_index - 1) >= 0 and x <= arr[min_index - 1]):
        return (n - min_index + binary_search(arr, 0, min_index-1, x) + 1)

    # else all the elements of the array
    # are less than 'x'   
    return n               

# driver code
arr = [6, 10, 12, 15, 2, 4, 5]
n = len(arr)
x = 14

print("Count = ",end="")
print(countEleLessThanOrEqual(arr, n, x))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# implementation to count elements
// less than or equal to a given
// value in a sorted rotated array
using System;

public class GFG {

    // function to find the minimum
    // element's index
    static int findMinIndex(int []arr, int low,
                                      int high)
    {

        // This condition is needed to handle
        // the case when array is not rotated
        // at all
        if (high < low)
            return 0;

        // If there is only one element left
        if (high == low)
            return low;

        // Find mid
        int mid = (low + high) / 2;

        // Check if element (mid+1) is
        // minimum element. Consider
        // the cases like {3, 4, 5, 1, 2}
        if (mid < high && arr[mid + 1] < arr[mid])
            return (mid + 1);

        // Check if mid itself is minimum element
        if (mid > low && arr[mid] < arr[mid - 1])
            return mid;

        // Decide whether we need to go to
        // left half or right half
        if (arr[high] > arr[mid])
            return findMinIndex(arr, low, mid - 1);

        return findMinIndex(arr, mid + 1, high);
    }

    // function returns the index of largest element
    // smaller than equal to 'x' in 'arr[l...h]'.
    // If no such element exits in the given range,
    // then it returns l-1.
    static int binary_search(int []arr, int l,
                                       int h, int x)
    {
        while (l <= h)
        {
            int mid = (l + h) / 2;

            // if 'x' is less than or equal to
            // arr[mid], then search in
            // arr[mid+1...h]
            if (arr[mid] <= x)
                l = mid + 1;

            // else search in arr[l...mid-1]
            else
                h = mid - 1;
        }

        // required index
        return h;
    }

    // function to count elements less than
    // or equal to a given value
    static int countEleLessThanOrEqual(int []arr,
                                      int n, int x)
    {

        // index of the smallest element in
        // the array
        int min_index = findMinIndex(arr, 0, n - 1);

        // if largest element smaller than or
        // equal to 'x' lies in the sorted
        // range arr[min_index...n-1]
        if (x <= arr[n - 1])
            return (binary_search(arr, min_index,
                          n - 1, x) + 1 - min_index);

        // if largest element smaller than or
        // equal to 'x' lies in the sorted
        // range arr[0...min_index-1]
        if ((min_index - 1) >= 0 &&
                             x <= arr[min_index - 1])
            return (n - min_index + binary_search(arr,
                             0, min_index - 1, x) + 1);

        // else all the elements of the array
        // are less than 'x'
        return n;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {6, 10, 12, 15, 2, 4, 5};
        int n = arr.Length;
        int x = 14;

        Console.Write("Count = " +
                countEleLessThanOrEqual(arr, n, x));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to count elements
// less than or equal to a given value
// in a sorted rotated array

// function to find the minimum
// element's index
function findMinIndex(&$arr, $low, $high)
{
    // This condition is needed to
    // handle the case when array
    // is not rotated at all
    if ($high < $low) return 0;

    // If there is only one element left
    if ($high == $low) return $low;

    // Find mid
    $mid = intval(($low + $high) / 2);

    // Check if element (mid+1) is
    // minimum element. Consider
    // the cases like {3, 4, 5, 1, 2}
    if ($mid < $high &&
        $arr[$mid + 1] < $arr[$mid])
    return ($mid + 1);

    // Check if mid itself is minimum element
    if ($mid > $low &&
        $arr[$mid] < $arr[$mid - 1])
    return $mid;

    // Decide whether we need to go
    // to left half or right half
    if ($arr[$high] > $arr[$mid])
    return findMinIndex($arr, $low, $mid - 1);
    return findMinIndex($arr, $mid + 1, $high);
}

// function returns the index of largest
// element smaller than equal to 'x' in 
// 'arr[l...h]'. If no such element exits
// in the given range, then it returns l-1.
function binary_search(&$arr, $l, $h, $x)
{
    while ($l <= $h)
    {
        $mid = intval(($l + $h) / 2);

        // if 'x' is less than or equal
        // to arr[mid], then search in
        // arr[mid+1...h]
        if ($arr[$mid] <= $x)
            $l = $mid + 1;

        // else search in arr[l...mid-1]
        else
            $h = $mid - 1;
    }

    // required index
    return $h;
}

// function to count elements less
// than or equal to a given value
function countEleLessThanOrEqual(&$arr, $n, $x)
{
    // index of the smallest element
    // in the array
    $min_index = findMinIndex($arr, 0, $n - 1);

    // if largest element smaller than
    // or equal to 'x' lies in the sorted
    // range arr[min_index...n-1]
    if ($x <= $arr[$n - 1])
        return (binary_search($arr, $min_index,
                              $n - 1, $x) + 1 - $min_index);

    // if largest element smaller than or
    // equal to 'x' lies in the sorted
    // range arr[0...min_index-1]
    if (($min_index - 1) >= 0 &&
         $x <= $arr[$min_index - 1])
        return ($n - $min_index +
                binary_search($arr, 0,
                              $min_index - 1, $x) + 1);

    // else all the elements of
    // the array are less than 'x'
    return $n;            
}

// Driver Code
$arr = array(6, 10, 12, 15, 2, 4, 5);
$n = sizeof($arr);
$x = 14;
echo "Count = " . countEleLessThanOrEqual($arr, $n, $x);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript implementation to count elements
// less than or equal to a given
// value in a sorted rotated array

    // function to find the minimum
    // element's index
    function findMinIndex(arr,low,high)
    {
        // This condition is needed to handle
    // the case when array is not rotated at all
    if (high < low)
        return 0;

    // If there is only one element left
    if (high == low)
        return low;

    // Find mid
    let mid = Math.floor((low + high) / 2);

    // Check if element (mid+1) is
    // minimum element. Consider
    // the cases like {3, 4, 5, 1, 2}
    if (mid < high && arr[mid + 1] < arr[mid])
        return (mid + 1);

    // Check if mid itself is minimum element
    if (mid > low && arr[mid] < arr[mid - 1])
        return mid;

    // Decide whether we need to go to
    // left half or right half
    if (arr[high] > arr[mid])
        return findMinIndex(arr, low, mid - 1);
    return findMinIndex(arr, mid + 1, high);
    }

    // function returns the index of largest element
// smaller than equal to 'x' in 'arr[l...h]'.
// If no such element exits in the given range,
// then it returns l-1.
    function binary_search(arr,l,h,x)
    {
        while (l <= h) {
    let mid = Math.floor((l + h) / 2);

    // if 'x' is less than or equal to arr[mid],
    // then search in arr[mid+1...h]
    if (arr[mid] <= x)
        l = mid + 1;

    // else search in arr[l...mid-1]
    else
        h = mid - 1;
    }

    // required index
    return h;
    }

    // function to count elements less than
// or equal to a given value
    function countEleLessThanOrEqual(arr,n,x)
    {
        // index of the smallest element in the array
    let min_index = findMinIndex(arr, 0, n - 1);

    // if largest element smaller than or
    // equal to 'x' lies in the sorted
    // range arr[min_index...n-1]
    if (x <= arr[n - 1])
    return (binary_search(arr, min_index, n - 1, x) + 1 - min_index);

    // if largest element smaller than or
    // equal to 'x' lies in the sorted
    // range arr[0...min_index-1]
    if ((min_index - 1) >= 0 && x <= arr[min_index - 1])
        return (n - min_index + binary_search(arr, 0, min_index - 1, x) + 1);

    // else all the elements of the array
    // are less than 'x'
    return n;
    }

    // Driver code
    let arr=[6, 10, 12, 15, 2, 4, 5];
    let n = arr.length;
    let x = 14;
    document.write("Count = " +
                      countEleLessThanOrEqual(arr, n, x));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
Count = 6
```

**时间复杂度:** O(logn)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。