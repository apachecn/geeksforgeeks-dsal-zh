# 找出 O(Log n)时间内出现的奇数元素

> 原文:[https://www . geeksforgeeks . org/find-the-element-the-奇数-in-olog-n-time/](https://www.geeksforgeeks.org/find-the-element-that-odd-number-of-times-in-olog-n-time/)

给定一个数组，其中除一个元素外，所有元素出现偶数次。元素的所有重复出现都成对出现，并且这些对不相邻(任何元素的连续出现不能超过两次)。找出出现次数为奇数的元素。
请注意，像{2，2，1，2，2，1，1}这样的输入是有效的，因为所有重复出现都成对出现，并且这些对不相邻。像{2，1，2}这样的输入无效，因为重复元素不会成对出现。另外，像{1，2，2，2，2}这样的输入是无效的，因为两对 2 是相邻的。像{2，2，2，1}这样的输入也是无效的，因为连续出现了三次 2。
**例:**

```
Input: arr[] = {1, 1, 2, 2, 1, 1, 2, 2, 13, 1, 1, 40, 40, 13, 13}
Output: 13

Input: arr[] = {1, 1, 2, 2, 3, 3, 4, 4, 3, 600, 600, 4, 4}
Output: 3
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
一个**简单解决方案** n 是对数组进行排序，然后从左到右遍历数组。由于数组是排序的，我们可以很容易地计算出所需的元素。这个解的时间复杂度是 O(n Log n)
A **更好的解**是对所有元素进行异或，异或的结果会给出奇数出现的元素。这个解的时间复杂度是 O(n)。详见[出现](https://www.geeksforgeeks.org/find-the-number-occurring-odd-number-of-times/)增加的基于异或的解决方案。
一个**高效解**可以在 O(Log n)时间内找到需要的元素。这个想法是利用二分搜索法。下面是输入数组中的一个观察值。
由于元素出现的次数是奇数，所以元素必须出现一次。例如，在{2，1，1，2，2 }中，前 2 是奇数。所以这个想法是用[二分搜索法](http://geeksquiz.com/binary-search/)来发现这个奇怪的现象。
奇数出现之前的所有元素在偶数索引(0，2，..)和奇数索引(1，3，…)下一次出现。之后所有元素第一次出现在奇数索引处，下一次出现在偶数索引处。
1)找到中间指标，说‘中间’。
2)如果‘mid’为偶数，则比较 arr[mid]和 arr[mid + 1]。如果两者相同，那么在“mid”之后或 mid 之前会出现一个奇怪的元素。
3)如果‘中间’是奇数，则比较 arr[中间]和 arr[中间–1]。如果两者相同，那么在“mid”之后或 mid 之前会出现一个奇怪的事件。
以下是基于上述思路的实现。
T22】

## C++

```
// C program to find the element that appears odd number of time
#include<stdio.h>

// A Binary Search based function to find the element
// that appears odd times
void search(int *arr, int low, int high)
{
    // Base cases
    if (low > high)
    return;
    if (low==high)
    {
        printf("The required element is %d ", arr[low]);
        return;
    }

    // Find the middle point
    int mid = (low+high)/2;

    // If mid is even and element next to mid is
    // same as mid, then output element lies on
    // right side, else on left side
    if (mid%2 == 0)
    {
        if (arr[mid] == arr[mid+1])
            search(arr, mid+2, high);
        else
            search(arr, low, mid);
    }
    else // If mid is odd
    {
        if (arr[mid] == arr[mid-1])
            search(arr, mid+1, high);
        else
            search(arr, low, mid-1);
    }
}

// Driver program
int main()
{
    int arr[] = {1, 1, 2, 2, 1, 1, 2, 2, 13, 1, 1, 40, 40};
    int len = sizeof(arr)/sizeof(arr[0]);
    search(arr, 0, len-1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the element
// that appears odd number of time

class GFG
{
    // A Binary Search based function to find
    // the element that appears odd times
    static void search(int arr[], int low, int high)
    {
        // Base cases
        if (low > high)
        return;
        if (low == high)
        {
            System.out.printf("The required element is %d "
                              , arr[low]);
            return;
        }

        // Find the middle point
        int mid = (low + high)/2;

        // If mid is even and element next to mid is
        // same as mid, then output element lies on
        // right side, else on left side
        if (mid % 2 == 0)
        {
            if (arr[mid] == arr[mid + 1])
                search(arr, mid + 2, high);
            else
                search(arr, low, mid);
        }

        // If mid is odd
        else
        {
            if (arr[mid] == arr[mid - 1])
                search(arr, mid + 1, high);
            else
                search(arr, low, mid - 1);
        }
    }

    // Driver program
    public static void main(String[] args)
    {
        int arr[] = {1, 1, 2, 2, 1, 1, 2, 2, 13,
                                    1, 1, 40, 40};
        int len = arr.length;
        search(arr, 0, len-1);
    }
}
// This code is contributed by
// Smitha DInesh Semwal
```

## 计算机编程语言

```
# Python program to find the element that appears odd number of times
# O(log n) approach

# Binary search based function
# Returns the element that appears odd number of times
def search(arr, low, high):

    # Base case
    if low > high:
        return None
    if low == high:
        return arr[low]

    # Find the middle point
    mid = (low + high)/2;

    # If mid is even
    if mid%2 == 0:

        # If the element next to mid is same as mid,
        # then output element lies on right side,
        # else on left side
        if arr[mid] == arr[mid+1]:
            return search(arr, mid+2, high)
        else:
            return search(arr, low, mid)

    else:
        # else if mid is odd

        if arr[mid] == arr[mid-1]:
            return search(arr, mid+1, high)
        else:
            # (mid-1) because target element can only exist at even place
            return search(arr, low, mid-1)

# Test array
arr = [ 1, 1, 2, 2, 1, 1, 2, 2, 13, 1, 1, 40, 40 ]

result = search(arr, 0, len(arr)-1 )

if result is not None:
    print "The required element is %d " % result
else:
    print "Invalid array"
```

## C#

```
// C# program to find the element
// that appears odd number of time
using System;

class GFG  {

    // A Binary Search based function to find
    // the element that appears odd times
    static void search(int []arr, int low, int high)
    {
        // Base cases
        if (low > high)
        return;
        if (low == high)
        {
            Console.WriteLine("The required element is "+
                                               arr[low]);
            return;
        }

        // Find the middle point
        int mid = (low + high)/2;

        // If mid is even and element next to mid is
        // same as mid, then output element lies on
        // right side, else on left side
        if (mid % 2 == 0)
        {
            if (arr[mid] == arr[mid + 1])
                search(arr, mid + 2, high);
            else
                search(arr, low, mid);
        }

        // If mid is odd
        else
        {
            if (arr[mid] == arr[mid - 1])
                search(arr, mid + 1, high);
            else
                search(arr, low, mid - 1);
        }
    }

    // Driver program
    public static void Main()
    {
        int []arr = {1, 1, 2, 2, 1, 1, 2, 2, 13,
                                  1, 1, 40, 40};
        int len = arr.Length;
        search(arr, 0, len-1);
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// element that appears odd
// number of times

// A Binary Search based
// function to find the
// element that appears odd times
function search($arr, $low, $high)
{
    // Base cases
    if ($low > $high)
    return;
    if ($low == $high)
    {
        echo "The required element is ",
                             $arr[$low];
        return;
    }

    // Find the middle point
    $mid = ($low + $high) / 2;

    // If mid is even and element
    // next to mid is same as mid,
    // then output element lies on
    // right side, else on left side
    if ($mid % 2 == 0)
    {
        if ($arr[$mid] == $arr[$mid + 1])
            search($arr, $mid + 2, $high);
        else
            search($arr, $low, $mid);
    }

    // If mid is odd
    else
    {
        if ($arr[$mid] == $arr[$mid - 1])
            search($arr, $mid + 1, $high);
        else
            search($arr, $low, $mid - 1);
    }
}

// Driver Code
$arr = array(1, 1, 2, 2, 1, 1, 2,
             2, 13, 1, 1, 40, 40);
$len = count($arr);;
search($arr, 0, $len - 1);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find the element that appears odd number of time

// A Binary Search based function to find the element
// that appears odd times
function search(arr, low, high)
{
    // Base cases
    if (low > high)
    return;
    if (low == high)
    {
        document.write("The required element is "+
                                               arr[low]);
        return;
    }

    // Find the middle point
    let mid = Math.floor((low + high) / 2);

    // If mid is even and element next to mid is
    // same as mid, then output element lies on
    // right side, else on left side
    if (mid % 2 == 0)
    {
        if (arr[mid] == arr[mid + 1])
            search(arr, mid + 2, high);
        else
            search(arr, low, mid);
    }
    else // If mid is odd
    {
        if (arr[mid] == arr[mid-1])
            search(arr, mid + 1, high);
        else
            search(arr, low, mid - 1);
    }
}

    // Driver program
    let arr = [ 1, 1, 2, 2, 1, 1, 2, 2, 13, 1, 1, 40, 40 ];
    let len = arr.length;
    search(arr, 0, len-1);

    // This code is contribute by jana_sayantan.
</script>
```

**输出:**

```
The required element is 13
```

**时间复杂度:** O(Log n)

本文由 Mehboob Elahi 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息