# 求几何级数中缺失的数

> 原文:[https://www . geesforgeks . org/find-missing-number-geometric-progression/](https://www.geeksforgeeks.org/find-missing-number-geometric-progression/)

给定一个按顺序表示几何级数元素的数组。级数中缺少一个元素，找出缺少的数字。可以假设总是缺少一个项，并且缺少的项不是系列的第一个或最后一个。
**例:**

```
Input : arr[] = {1, 3 , 27, 81}
Output : 9

Input : arr[] = {4, 16, 64, 1024};
Output : 256
```

一个**简单的解决方法**就是线性遍历数组，找到缺失的数字。这个解的时间复杂度是 O(n)。
一个**高效的解决方案**使用二分搜索法在 O(Log n)时间内解决了这个问题。想法是去中间元素。检查中间和次中间的比率是否等于公比，如果不是，则缺少的元素位于中间和中间+1 之间。如果中间元素等于几何级数中的第 n/2 项(设 n 为输入数组中的元素个数)，则缺失元素位于右半部分。否则元素位于左半部分。

## C++

```
// C++ program to find missing number in
// geometric progression
#include <bits/stdc++.h>
using namespace std;

// It returns INT_MAX in case of error
int findMissingRec(int arr[], int low,
                   int high, int ratio)
{
    if (low >= high)
        return INT_MAX;
    int mid = low + (high - low)/2;

    // If element next to mid is missing
    if (arr[mid+1]/arr[mid] != ratio)
        return (arr[mid] * ratio);

    // If element previous to mid is missing
    if ((mid > 0) && (arr[mid]/arr[mid-1]) != ratio)
        return (arr[mid-1] * ratio);

    // If missing element is in right half
    if (arr[mid] == arr[0] * (pow(ratio, mid)) )
        return findMissingRec(arr, mid+1, high, ratio);

    return findMissingRec(arr, low, mid-1, ratio);
}

// Find ration and calls findMissingRec
int findMissing(int arr[], int n)
{
    // Finding ration assuming that the missing term is
    // not first or last term of series.
    int ratio = (float) pow(arr[n-1]/arr[0], 1.0/n);

    return findMissingRec(arr, 0, n-1, ratio);
}

// Driver code
int main(void)
{
    int arr[] = {2, 4, 8, 32};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << findMissing(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Find the missing number
// in Geometric Progression
class GFG {

    // It returns INT_MAX in case of error
    public static int findMissingRec(int arr[], int low,
                       int high, int ratio)
    {
        if (low >= high)
            return Integer.MAX_VALUE;
        int mid = low + (high - low)/2;

        // If element next to mid is missing
        if (arr[mid+1]/arr[mid] != ratio)
            return (arr[mid] * ratio);

        // If element previous to mid is missing
        if ((mid > 0) && (arr[mid]/arr[mid-1]) != ratio)
            return (arr[mid-1] * ratio);

        // If missing element is in right half
        if (arr[mid] == arr[0] * (Math.pow(ratio, mid)) )
            return findMissingRec(arr, mid+1, high, ratio);

        return findMissingRec(arr, low, mid-1, ratio);
    }

    // Find ration and calls findMissingRec
    public static int findMissing(int arr[], int n)
    {
        // Finding ration assuming that the missing
        // term is not first or last term of series.
        int ratio =(int) Math.pow(arr[n-1]/arr[0], 1.0/n);

        return findMissingRec(arr, 0, n-1, ratio);
    }   

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {2, 4, 8, 32};
        int n = arr.length;

        System.out.print(findMissing(arr, n));
    }
  }
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to find missing
# number in geometric progression

# It returns INT_MAX in case of error
def findMissingRec(arr, low, high, ratio):

    if (low >= high):
        return 2147483647
    mid = low + (high - low) // 2

    # If element next to mid is missing
    if (arr[mid + 1] // arr[mid] != ratio):
        return (arr[mid] * ratio)

    # If element previous to mid is missing
    if ((mid > 0) and (arr[mid] / arr[mid-1]) != ratio):
        return (arr[mid - 1] * ratio)

    # If missing element is in right half
    if (arr[mid] == arr[0] * (pow(ratio, mid)) ):
        return findMissingRec(arr, mid+1, high, ratio)

    return findMissingRec(arr, low, mid-1, ratio)

# Find ration and calls findMissingRec
def findMissing(arr, n):

    # Finding ration assuming that
    # the missing term is not first
    # or last term of series.
    ratio = int(pow(arr[n-1] / arr[0], 1.0 / n))

    return findMissingRec(arr, 0, n-1, ratio)

# Driver code
arr = [2, 4, 8, 32]
n = len(arr)
print(findMissing(arr, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# Code for Find the missing number
// in Geometric Progression
using System;

class GFG {

    // It returns INT_MAX in case of error
    public static int findMissingRec(int []arr, int low,
                                    int high, int ratio)
    {
        if (low >= high)
            return int.MaxValue;

        int mid = low + (high - low)/2;

        // If element next to mid is missing
        if (arr[mid+1]/arr[mid] != ratio)
            return (arr[mid] * ratio);

        // If element previous to mid is missing
        if ((mid > 0) && (arr[mid]/arr[mid-1]) != ratio)
            return (arr[mid-1] * ratio);

        // If missing element is in right half
        if (arr[mid] == arr[0] * (Math.Pow(ratio, mid)) )
            return findMissingRec(arr, mid+1, high, ratio);

        return findMissingRec(arr, low, mid-1, ratio);
    }

    // Find ration and calls findMissingRec
    public static int findMissing(int []arr, int n)
    {

        // Finding ration assuming that the missing
        // term is not first or last term of series.
        int ratio =(int) Math.Pow(arr[n-1]/arr[0], 1.0/n);

        return findMissingRec(arr, 0, n-1, ratio);
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int []arr = {2, 4, 8, 32};
        int n = arr.Length;

        Console.Write(findMissing(arr, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find missing number
// in geometric progression

// It returns INT_MAX in case of error
function findMissingRec(&$arr, $low,
                         $high, $ratio)
{
    if ($low >= $high)
        return PHP_INT_MAX;
    $mid = $low + intval(($high - $low) / 2);

    // If element next to mid is missing
    if ($arr[$mid+1]/$arr[$mid] != $ratio)
        return ($arr[$mid] * $ratio);

    // If element previous to mid is missing
    if (($mid > 0) && ($arr[$mid] /
                       $arr[$mid - 1]) != $ratio)
        return ($arr[$mid - 1] * $ratio);

    // If missing element is in right half
    if ($arr[$mid] == $arr[0] * (pow($ratio, $mid)))
        return findMissingRec($arr, $mid + 1,
                              $high, $ratio);

    return findMissingRec($arr, $low,
                          $mid - 1, $ratio);
}

// Find ration and calls findMissingRec
function findMissing(&$arr, $n)
{
    // Finding ration assuming that the missing
    // term is not first or last term of series.
    $ratio = (float) pow($arr[$n - 1] /
                         $arr[0], 1.0 / $n);

    return findMissingRec($arr, 0, $n - 1, $ratio);
}

// Driver code
$arr = array(2, 4, 8, 32);
$n = sizeof($arr);
echo findMissing($arr, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript Code for Find the missing number
// in Geometric Progression

    // It returns INT_MAX in case of error
    function findMissingRec(arr,low,high,ratio)
    {
        if (low >= high)
            return Integer.MAX_VALUE;
        let mid = Math.floor(low + (high - low)/2);

        // If element next to mid is missing
        if (arr[mid+1]/arr[mid] != ratio)
            return (arr[mid] * ratio);

        // If element previous to mid is missing
        if ((mid > 0) && (arr[mid]/arr[mid-1]) != ratio)
            return (arr[mid-1] * ratio);

        // If missing element is in right half
        if (arr[mid] == arr[0] * (Math.pow(ratio, mid)) )
            return findMissingRec(arr, mid+1, high, ratio);

        return findMissingRec(arr, low, mid-1, ratio);
    }

     // Find ration and calls findMissingRec
    function findMissing(arr,n)
    {
        // Finding ration assuming that the missing
        // term is not first or last term of series.
        let ratio =Math.floor( Math.pow(arr[n-1]/arr[0], 1.0/n));

        return findMissingRec(arr, 0, n-1, ratio);
    }

    /* Driver program to test above function */
    let arr=[2, 4, 8, 32];
    let n = arr.length;
    document.write(findMissing(arr, n));

    // This code is contributed by rag2127

</script>
```

**输出:**

```
16
```

注意:此解决方案的缺点是:对于较大的值或较大的数组，它可能会导致溢出和/或可能需要更多的时间来为计算机供电。
本文由**亚辛·扎法尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。