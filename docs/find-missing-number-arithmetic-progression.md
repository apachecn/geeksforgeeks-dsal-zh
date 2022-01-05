# 求算术级数中缺失的数

> 原文:[https://www . geesforgeks . org/find-missing-number-算术-progression/](https://www.geeksforgeeks.org/find-missing-number-arithmetic-progression/)

给定一个按顺序表示算术级数元素的数组。级数中缺少一个元素，找出缺少的数字。

**示例:**

```
Input: arr[]  = {2, 4, 8, 10, 12, 14}
Output: 6

Input: arr[]  = {1, 6, 11, 16, 21, 31};
Output: 26
```

一个简单的解决方案是线性遍历数组并找到丢失的数字。这个解的时间复杂度是 O(n)。我们可以利用二分搜索法在 0(Logn)时间内解决这个问题。想法是去中间元素。检查中间和下一个中间之间的差是否等于 diff，如果不是，则缺少的元素位于中间和中间+1 之间。如果中间元素等于算术级数中的第 n/2 项(设 n 为输入数组中的元素个数)，则缺失的元素位于右半部分。否则元素位于左半部分。

以下是上述想法的实现。

## C++

```
// C++ program to find the missing number
// in a given arithmetic progression
#include<iostream>
using namespace std;
#define INT_MAX 2147483647;
class GFG
{

// A binary search based recursive function that returns
// the missing element in arithmetic progression
public:int findMissingUtil(int arr[], int low,
                        int high, int diff)
{
    // There must be two elements to find the missing
    if (high <= low)
        return INT_MAX;

    // Find index of middle element
    int mid = low + (high - low) / 2;

    // The element just after the middle element is missing.
    // The arr[mid+1] must exist, because we return when
    // (low == high) and take floor of (high-low)/2
    if (arr[mid + 1] - arr[mid] != diff)
        return (arr[mid] + diff);

    // The element just before mid is missing
    if (mid > 0 && arr[mid] - arr[mid - 1] != diff)
        return (arr[mid - 1] + diff);

    // If the elements till mid follow AP, then recur
    // for right half
    if (arr[mid] == arr[0] + mid * diff)
        return findMissingUtil(arr, mid + 1,
                            high, diff);

    // Else recur for left half
    return findMissingUtil(arr, low, mid - 1, diff);
}

// The function uses findMissingUtil() to
// find the missing element in AP.
// It assumes that there is exactly one
// missing element and may give incorrect result
// when there is no missing element or
// more than one missing elements. This function
// also assumes that the difference in AP is an
// integer.
int findMissing(int arr[], int n)
{
    // If exactly one element is missing, then we can find
    // difference of arithmetic progression using following
    // formula. Example, 2, 4, 6, 10, diff = (10-2)/4 = 2.
    // The assumption in formula is that the difference is
    // an integer.
    int diff = (arr[n - 1] - arr[0]) / n;

    // Binary search for the missing
    // number using above calculated diff
    return findMissingUtil(arr, 0, n - 1, diff);
}
};

// Driver Code
int main()
{
    GFG g;
    int arr[] = {2, 4, 8, 10, 12, 14};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "The missing element is "
        << g.findMissing(arr, n);
    return 0;
}

// This code is contributed by Soumik
```

## C

```
// A C program to find the missing number in a given
// arithmetic progression
#include <stdio.h>
#include <limits.h>

// A binary search based recursive function that returns
// the missing element in arithmetic progression
int findMissingUtil(int arr[], int low, int high, int diff)
{
    // There must be two elements to find the missing
    if (high <= low)
        return INT_MAX;

    // Find index of middle element
    int mid = low + (high - low)/2;

    // The element just after the middle element is missing.
    // The arr[mid+1] must exist, because we return when
    // (low == high) and take floor of (high-low)/2
    if (arr[mid+1] - arr[mid] != diff)
        return (arr[mid] + diff);

    // The element just before mid is missing
    if (mid > 0 && arr[mid] - arr[mid-1] != diff)
        return (arr[mid-1] + diff);

    // If the elements till mid follow AP, then recur
    // for right half
    if (arr[mid] == arr[0] + mid*diff)
        return findMissingUtil(arr, mid+1, high, diff);

    // Else recur for left half
    return findMissingUtil(arr, low, mid-1, diff);
}

// The function uses findMissingUtil() to find the missing
// element in AP. It assumes that there is exactly one missing
// element and may give incorrect result when there is no missing
// element or more than one missing elements.
// This function also assumes that the difference in AP is an
// integer.
int findMissing(int arr[], int n)
{
    // If exactly one element is missing, then we can find
    // difference of arithmetic progression using following
    // formula. Example, 2, 4, 6, 10, diff = (10-2)/4 = 2.
    // The assumption in formula is that the difference is
    // an integer.
    int diff = (arr[n-1] - arr[0])/n;

    // Binary search for the missing number using above
    // calculated diff
    return findMissingUtil(arr, 0, n-1, diff);
}

/* Driver program to check above functions */
int main()
{
    int arr[] = {2, 4, 8, 10, 12, 14};
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("The missing element is %d", findMissing(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find
// the missing number in
// a given arithmetic
// progression
import java.io.*;

class GFG
{

// A binary search based
// recursive function that
// returns the missing
// element in arithmetic
// progression
static int findMissingUtil(int arr[], int low,
                        int high, int diff)
{
    // There must be two elements
    // to find the missing
    if (high <= low)
        return Integer.MAX_VALUE;

    // Find index of
    // middle element
    int mid = low + (high - low) / 2;

    // The element just after the
    // middle element is missing.
    // The arr[mid+1] must exist,
    // because we return when
    // (low == high) and take
    // floor of (high-low)/2
    if (arr[mid + 1] - arr[mid] != diff)
        return (arr[mid] + diff);

    // The element just
    // before mid is missing
    if (mid > 0 && arr[mid] -
                arr[mid - 1] != diff)
        return (arr[mid - 1] + diff);

    // If the elements till mid follow
    // AP, then recur for right half
    if (arr[mid] == arr[0] + mid * diff)
        return findMissingUtil(arr, mid + 1,
                            high, diff);

    // Else recur for left half
    return findMissingUtil(arr, low, mid - 1, diff);
}

// The function uses findMissingUtil()
// to find the missing element in AP.
// It assumes that there is exactly
// one missing element and may give
// incorrect result when there is no
// missing element or more than one
// missing elements. This function also
// assumes that the difference in AP is
// an integer.
static int findMissing(int arr[], int n)
{
    // If exactly one element is missing,
    // then we can find difference of
    // arithmetic progression using
    // following formula. Example, 2, 4,
    // 6, 10, diff = (10-2)/4 = 2.
    // The assumption in formula is that
    // the difference is an integer.
    int diff = (arr[n - 1] - arr[0]) / n;

    // Binary search for the missing
    // number using above calculated diff
    return findMissingUtil(arr, 0, n - 1, diff);
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = {2, 4, 8, 10, 12, 14};
    int n = arr.length;
    System.out.println("The missing element is "+
                            findMissing(arr, n));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# A Python3 program to find the missing
# number in a given arithmetic progression
import sys

# A binary search based recursive function
# that returns the missing element in
# arithmetic progression
def findMissingUtil(arr, low, high, diff):

    # There must be two elements to
    # find the missing
    if (high <= low):
        return sys.maxsize;

    # Find index of middle element
    mid = int(low + (high - low) / 2);

    # The element just after the middle
    # element is missing. The arr[mid+1]
    # must exist, because we return when
    # (low == high) and take floor of
    # (high-low)/2
    if (arr[mid + 1] - arr[mid] != diff):
        return (arr[mid] + diff);

    # The element just before mid is missing
    if (mid > 0 and arr[mid] -
                    arr[mid - 1] != diff):
        return (arr[mid - 1] + diff);

    # If the elements till mid follow AP,
    # then recur for right half
    if (arr[mid] == arr[0] + mid * diff):
        return findMissingUtil(arr, mid + 1,
                                high, diff);

    # Else recur for left half
    return findMissingUtil(arr, low,
                        mid - 1, diff);

# The function uses findMissingUtil() to find
# the missing element in AP. It assumes that
# there is exactly one missing element and may
# give incorrect result when there is no missing
# element or more than one missing elements.
# This function also assumes that the difference
# in AP is an integer.
def findMissing(arr, n):

    # If exactly one element is missing, then
    # we can find difference of arithmetic
    # progression using following formula.
    # Example, 2, 4, 6, 10, diff = (10-2)/4 = 2.
    # The assumption in formula is that the
    # difference is an integer.
    diff = int((arr[n - 1] - arr[0]) / n);

    # Binary search for the missing number
    # using above calculated diff
    return findMissingUtil(arr, 0, n - 1, diff);

# Driver Code
arr = [2, 4, 8, 10, 12, 14];
n = len(arr);
print("The missing element is",
        findMissing(arr, n));

# This code is contributed by chandan_jnu
```

## C#

```
// A C# program to find
// the missing number in
// a given arithmetic
// progression
using System;

class GFG
{

// A binary search based
// recursive function that
// returns the missing
// element in arithmetic
// progression
static int findMissingUtil(int []arr, int low,
                        int high, int diff)
{
    // There must be two elements
    // to find the missing
    if (high <= low)
        return int.MaxValue;

    // Find index of
    // middle element
    int mid = low + (high -
                    low) / 2;

    // The element just after the
    // middle element is missing.
    // The arr[mid+1] must exist,
    // because we return when
    // (low == high) and take
    // floor of (high-low)/2
    if (arr[mid + 1] -
        arr[mid] != diff)
        return (arr[mid] + diff);

    // The element just
    // before mid is missing
    if (mid > 0 && arr[mid] -
                arr[mid - 1] != diff)
        return (arr[mid - 1] + diff);

    // If the elements till mid follow
    // AP, then recur for right half
    if (arr[mid] == arr[0] +
            mid * diff)
        return findMissingUtil(arr, mid + 1,
                            high, diff);

    // Else recur for left half
    return findMissingUtil(arr, low,
                        mid - 1, diff);
}

// The function uses findMissingUtil()
// to find the missing element
// in AP. It assumes that there
// is exactly one missing element
// and may give incorrect result
// when there is no missing element
// or more than one missing elements.
// This function also assumes that
// the difference in AP is an integer.
static int findMissing(int []arr, int n)
{
    // If exactly one element
    // is missing, then we can
    // find difference of arithmetic
    // progression using following
    // formula. Example, 2, 4, 6, 10,
    // diff = (10-2)/4 = 2.The assumption
    // in formula is that the difference
    // is an integer.
    int diff = (arr[n - 1] -
                arr[0]) / n;

    // Binary search for the
    // missing number using
    // above calculated diff
    return findMissingUtil(arr, 0,
                        n - 1, diff);
}

// Driver Code
public static void Main ()
{
    int []arr = {2, 4, 8,
                10, 12, 14};
    int n = arr.Length;
    Console.WriteLine("The missing element is "+
                        findMissing(arr, n));
}
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find the missing
// number in a given arithmetic progression

// A binary search based recursive function
// that returns the missing element in
// arithmetic progression

function findMissingUtil($arr, $low, $high, $diff)
{
    // There must be two elements to
    // find the missing
    if ($high <= $low)
        return PHP_INT_MAX;

    // Find index of middle element
    $mid = $low + ($high - $low) / 2;

    // The element just after the middle
    // element is missing. The arr[mid+1]
    // must exist, because we return when
    // (low == high) and take floor of (high-low)/2
    if ($arr[$mid + 1] - $arr[$mid] != $diff)
        return ($arr[$mid] + $diff);

    // The element just before mid is missing
    if ($mid > 0 && $arr[$mid] - $arr[$mid - 1] != $diff)
        return ($arr[$mid - 1] + $diff);

    // If the elements till mid follow AP,
    // then recur for right half
    if ($arr[$mid] == $arr[0] + $mid * $diff)
        return findMissingUtil($arr, $mid + 1,
                            $high, $diff);

    // Else recur for left half
    return findMissingUtil($arr, $low, $mid - 1, $diff);
}

// The function uses findMissingUtil() to find
// the missing element in AP. It assumes that
// there is exactly one missing element and may
// give incorrect result when there is no missing
// element or more than one missing elements.
// This function also assumes that the difference
// in AP is an integer.
function findMissing($arr, $n)
{
    // If exactly one element is missing, then
    // we can find difference of arithmetic
    // progression using following formula.
    // Example, 2, 4, 6, 10, diff = (10-2)/4 = 2.
    // The assumption in formula is that the
    // difference is an integer.
    $diff = ($arr[$n - 1] - $arr[0]) / $n;

    // Binary search for the missing number
    // using above calculated diff
    return findMissingUtil($arr, 0, $n - 1, $diff);
}

// Driver Code
$arr = array(2, 4, 8, 10, 12, 14);
$n = sizeof($arr);
echo "The missing element is ",
        findMissing($arr, $n);

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>

    // A JavaScript program to find
    // the missing number in
    // a given arithmetic
    // progression

    // A binary search based
    // recursive function that
    // returns the missing
    // element in arithmetic
    // progression
    function findMissingUtil(arr, low, high, diff)
    {
        // There must be two elements
        // to find the missing
        if (high <= low)
            return Number.MAX_VALUE;

        // Find index of
        // middle element
        let mid = low + parseInt((high - low) / 2, 10);

        // The element just after the
        // middle element is missing.
        // The arr[mid+1] must exist,
        // because we return when
        // (low == high) and take
        // floor of (high-low)/2
        if (arr[mid + 1] - arr[mid] != diff)
            return (arr[mid] + diff);

        // The element just
        // before mid is missing
        if (mid > 0 && arr[mid] -
                    arr[mid - 1] != diff)
            return (arr[mid - 1] + diff);

        // If the elements till mid follow
        // AP, then recur for right half
        if (arr[mid] == arr[0] + mid * diff)
            return findMissingUtil(arr, mid + 1, high, diff);

        // Else recur for left half
        return findMissingUtil(arr, low, mid - 1, diff);
    }

    // The function uses findMissingUtil()
    // to find the missing element in AP.
    // It assumes that there is exactly
    // one missing element and may give
    // incorrect result when there is no
    // missing element or more than one
    // missing elements. This function also
    // assumes that the difference in AP is
    // an integer.
    function findMissing(arr, n)
    {
        // If exactly one element is missing,
        // then we can find difference of
        // arithmetic progression using
        // following formula. Example, 2, 4,
        // 6, 10, diff = (10-2)/4 = 2.
        // The assumption in formula is that
        // the difference is an integer.
        let diff = parseInt((arr[n - 1] - arr[0]) / n, 10);

        // Binary search for the missing
        // number using above calculated diff
        return findMissingUtil(arr, 0, n - 1, diff);
    }

    let arr = [2, 4, 8, 10, 12, 14];
    let n = arr.length;
    document.write("The missing element is "+
                            findMissing(arr, n));

</script>
```

**Output**

```
The missing element is 6
```

时间复杂度:0(对数 n)

辅助空间:0(1)

**迭代:**

想法是去中间元素。检查中间元素的索引是否等于(AP 中中间元素的第 n 个位置)–1，那么丢失的元素位于右半部分；如果不是，那么丢失的元素位于左半部分(这个想法类似于[在大小为 n 的排序数组中找到唯一的重复元素](https://www.geeksforgeeks.org/find-repeating-element-sorted-array-size-n/))。打破二分搜索法循环后，丢失的元素将位于高和低之间。我们可以通过在索引高的元素上加上一个公共差或在索引低的元素上减去一个公共差来找到丢失的元素。

以下是上述想法的实现。

## C++

```
// C++ program to find the missing number
// in a given arithmetic progression
#include<iostream>
using namespace std;
#define INT_MAX 2147483647;
class GFG
{

// A binary search based function that returns
// the missing element in arithmetic progression
public:int findMissingUtil(int arr[], int low,
                           int high, int diff)
{   
    // Find index of middle element
    int mid;
    while (low <= high)
    {   
          // find index of middle element
        mid = (low + high) / 2;
          // if mid == (nth position of element in AP)-1
          // the missing element will exist in right half
        if ((arr[mid] - arr[0]) / diff == mid)
            low = mid + 1;
        else
        // the missing element will exist in left half
            high = mid - 1;
    }
      // after breaking out of binary search loop
      // our missing element will exist between high and low
      // our missing element will be a[high] + commom difference
      // or a[low] - commom difference
    return arr[high] + diff;
}

// The function uses findMissingUtil() to
// find the missing element in AP.
// It assumes that there is exactly one
// missing element and may give incorrect result
// when there is no missing element or
// more than one missing elements. This function
// also assumes that the difference in AP is an
// integer.
int findMissing(int arr[], int n)
{
    // If exactly one element is missing, then we can find
    // difference of arithmetic progression using following
    // formula. Example, 2, 4, 6, 10, diff = (10-2)/4 = 2.
    // The assumption in formula is that the difference is
    // an integer.
    int diff = (arr[n - 1] - arr[0]) / n;

    // Binary search for the missing
    // number using above calculated diff
    return findMissingUtil(arr, 0, n - 1, diff);
}
};

// Driver Code
int main()
{
    GFG g;
    int arr[] = {2, 4, 8, 10, 12, 14};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "The missing element is "
         << g.findMissing(arr, n);
    return 0;
}

// This code is contributed by gurudev620gs
```

## C

```
// A C program to find the missing number in a given
// arithmetic progression
#include <stdio.h>
#include <limits.h>

// A binary search based function that returns
// the missing element in arithmetic progression
int findMissingUtil(int arr[], int low, int high, int diff)
{
    // Find index of middle element
    int mid;
    while (low <= high)
    {   
          // find index of middle element
        mid = (low + high) / 2;
          // if mid == (nth position of element in AP)-1
          // the missing element will exist in right half
        if ((arr[mid] - arr[0]) / diff == mid)
            low = mid + 1;
        else
        // the missing element will exist in left half
            high = mid - 1;
    }
      // after breaking out of binary search loop
      // our missing element will exist between high and low
      // our missing element will be a[high] + commom difference
      // or a[low] - commom difference
    return arr[high] + diff;
}

// The function uses findMissingUtil() to find the missing
// element in AP.  It assumes that there is exactly one missing
// element and may give incorrect result when there is no missing
// element or more than one missing elements.
// This function also assumes that the difference in AP is an
// integer.
int findMissing(int arr[], int n)
{
    // If exactly one element is missing, then we can find
    // difference of arithmetic progression using following
    // formula.  Example, 2, 4, 6, 10, diff = (10-2)/4 = 2.
    // The assumption in formula is that the difference is
    // an integer.
    int diff = (arr[n-1] - arr[0])/n;

    // Binary search for the missing number using above
    // calculated diff
    return findMissingUtil(arr, 0, n-1, diff);
}

/* Driver program to check above functions */
int main()
{
    int arr[] = {2, 4, 8, 10, 12, 14};
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("The missing element is %d", findMissing(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to find
// the missing number in
// a given arithmetic
// progression
import java.io.*;

class GFG
{

// A binary search function that
// returns the missing
// element in arithmetic
// progression
static int findMissingUtil(int arr[], int low,
                           int high, int diff)
{   
      // Find index of middle element
    int mid;
    while (low <= high)
    {   
          // find index of middle element
        mid = (low + high) / 2;
          // if mid == (nth position of element in AP)-1
          // the missing element will exist in right half
        if ((arr[mid] - arr[0]) / diff == mid)
            low = mid + 1;
        else
        // the missing element will exist in left half
            high = mid - 1;
    }
      // after breaking out of binary search loop
      // our missing element will exist between high and low
      // our missing element will be a[high] + commom difference
      // or a[low] - commom difference
    return arr[high] + diff;
}

// The function uses findMissingUtil()
// to find the missing element in AP.
// It assumes that there is exactly
// one missing element and may give
// incorrect result when there is no
// missing element or more than one
// missing elements. This function also
// assumes that the difference in AP is
// an integer.
static int findMissing(int arr[], int n)
{
    // If exactly one element is missing,
    // then we can find difference of
    // arithmetic progression using
    // following formula. Example, 2, 4,
    // 6, 10, diff = (10-2)/4 = 2.
    // The assumption in formula is that
    // the difference is an integer.
    int diff = (arr[n - 1] - arr[0]) / n;

    // Binary search for the missing
    // number using above calculated diff
    return findMissingUtil(arr, 0, n - 1, diff);
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = {2, 4, 8, 10, 12, 14};
    int n = arr.length;
    System.out.println("The missing element is "+  
                            findMissing(arr, n));
}
}

// This code is contributed by gurudev620gs.
```

## 蟒蛇 3

```
# A Python3 program to find the missing
# number in a given arithmetic progression
import sys

# A binary search based function
# that returns the missing element in
# arithmetic progression
def findMissingUtil(arr, low, high, diff):

    while low <= high:
          # find index of middle element
        mid = (low + high)//2
          # if mid == (nth position of element in AP)-1
          # the missing element will exist in right half
        if (arr[mid] - arr[0])//diff == mid:
            low = mid + 1
        else:
        # the missing element will exist in left half
            high = mid - 1
    # after breaking out of binary search loop
      # our missing element will exist between high and low
      # our missing element will be a[high] + commom difference
      # or a[low] - commom difference
    return arr[high] + diff

# The function uses findMissingUtil() to find
# the missing element in AP. It assumes that
# there is exactly one missing element and may
# give incorrect result when there is no missing
# element or more than one missing elements.
# This function also assumes that the difference
# in AP is an integer.
def findMissing(arr, n):

    # If exactly one element is missing, then
    # we can find difference of arithmetic
    # progression using following formula.
    # Example, 2, 4, 6, 10, diff = (10-2)/4 = 2.
    # The assumption in formula is that the
    # difference is an integer.
    diff = int((arr[n - 1] - arr[0]) / n);

    # Binary search for the missing number
    # using above calculated diff
    return findMissingUtil(arr, 0, n - 1, diff);

# Driver Code
arr = [2, 4, 8, 10, 12, 14];
n = len(arr);
print("The missing element is",
          findMissing(arr, n));

# This code is contributed by gurudev620gs
```

## C#

```
// A C# program to find
// the missing number in
// a given arithmetic
// progression
using System;

class GFG
{

// A binary search function that
// returns the missing
// element in arithmetic
// progression
static int findMissingUtil(int []arr, int low,
                           int high, int diff)
{
    // Find index of middle element
    int mid;
    while (low <= high)
    {   
          // find index of middle element
        mid = (low + high) / 2;
          // if mid == (nth position of element in AP)-1
          // the missing element will exist in right half
        if ((arr[mid] - arr[0]) / diff == mid)
            low = mid + 1;
        else
        // the missing element will exist in left half
            high = mid - 1;
    }
      // after breaking out of binary search loop
      // our missing element will exist between high and low
      // our missing element will be a[high] + commom difference
      // or a[low] - commom difference
    return arr[high] + diff;
}

// The function uses findMissingUtil()
// to find the missing element
// in AP. It assumes that there
// is exactly one missing element
// and may give incorrect result
// when there is no missing element
// or more than one missing elements.
// This function also assumes that
// the difference in AP is an integer.
static int findMissing(int []arr, int n)
{
    // If exactly one element
    // is missing, then we can
    // find difference of arithmetic
    // progression using following
    // formula. Example, 2, 4, 6, 10,
    // diff = (10-2)/4 = 2.The assumption
    // in formula is that the difference
    // is an integer.
    int diff = (arr[n - 1] -
                arr[0]) / n;

    // Binary search for the
    // missing number using
    // above calculated diff
    return findMissingUtil(arr, 0,
                           n - 1, diff);
}

// Driver Code
public static void Main ()
{
    int []arr = {2, 4, 8,
                 10, 12, 14};
    int n = arr.Length;
    Console.WriteLine("The missing element is "+
                           findMissing(arr, n));
}
}

// This code is contributed by gurudev620gs.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find the missing
// number in a given arithmetic progression

// A binary search based function
// that returns the missing element in
// arithmetic progression

function findMissingUtil($arr, $low, $high, $diff)
{
    while ($low <= $high)
    {   
          // find index of middle element
        $mid = ($low + $high) / 2;
          // if mid == (nth position of element in AP)-1
          // the missing element will exist in right half
        if (($arr[$mid] - $arr[0]) / $diff == $mid)
            $low = $mid + 1;
        else
        // the missing element will exist in left half
            $high = $mid - 1;
    }
      // after breaking out of binary search loop
      // our missing element will exist between high and low
      // our missing element will be a[high] + commom difference
      // or a[low] - commom difference
    return $arr[$high] + $diff;
}

// The function uses findMissingUtil() to find
// the missing element in AP. It assumes that
// there is exactly one missing element and may
// give incorrect result when there is no missing
// element or more than one missing elements.
// This function also assumes that the difference
// in AP is an integer.
function findMissing($arr, $n)
{
    // If exactly one element is missing, then
    // we can find difference of arithmetic
    // progression using following formula.
    // Example, 2, 4, 6, 10, diff = (10-2)/4 = 2.
    // The assumption in formula is that the
    // difference is an integer.
    $diff = ($arr[$n - 1] - $arr[0]) / $n;

    // Binary search for the missing number
    //  using above calculated diff
    return findMissingUtil($arr, 0, $n - 1, $diff);
}

// Driver Code
$arr = array(2, 4, 8, 10, 12, 14);
$n = sizeof($arr);
echo "The missing element is ",
         findMissing($arr, $n);

// This code is contributed by gurudev620.gs
?>
```

## java 描述语言

```
<script>

    // A JavaScript program to find
    // the missing number in
    // a given arithmetic
    // progression

    // A binary search function that
    // returns the missing
    // element in arithmetic
    // progression
    function findMissingUtil(arr, low, high, diff)
    {
        // Find index of middle element
        int mid;
        while (low <= high)
        {   
            // find index of middle element
            mid = (low + high) / 2;
            // if mid == (nth position of element in AP)-1
            // the missing element will exist in right half
            if ((arr[mid] - arr[0]) / diff == mid)
                low = mid + 1;
            else
            // the missing element will exist in left half
                high = mid - 1;
        }
        // after breaking out of binary search loop
        // our missing element will exist between high and low
        // our missing element will be a[high] + commom difference
        // or a[low] - commom difference
        return arr[high] + diff;
    }

    // The function uses findMissingUtil()
    // to find the missing element in AP.
    // It assumes that there is exactly
    // one missing element and may give
    // incorrect result when there is no
    // missing element or more than one
    // missing elements. This function also
    // assumes that the difference in AP is
    // an integer.
    function findMissing(arr, n)
    {
        // If exactly one element is missing,
        // then we can find difference of
        // arithmetic progression using
        // following formula. Example, 2, 4,
        // 6, 10, diff = (10-2)/4 = 2.
        // The assumption in formula is that
        // the difference is an integer.
        let diff = parseInt((arr[n - 1] - arr[0]) / n, 10);

        // Binary search for the missing
        // number using above calculated diff
        return findMissingUtil(arr, 0, n - 1, diff);
    }

    let arr = [2, 4, 8, 10, 12, 14];
    let n = arr.length;
    document.write("The missing element is "+  
                            findMissing(arr, n));

</script>
```

**Output**

```
The missing element is 6
```

时间复杂度:0(对数 n)

辅助空间:0(1)

感谢 [gurudev620gs](https://auth.geeksforgeeks.org/user/gurudev620gs/profile) 提出上述解决方案。

**练习:**
为几何级数解同样的问题。您的解决方案的时间复杂度是多少？斐波那契数列呢？
本文由**哈什特·阿格沃尔**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。