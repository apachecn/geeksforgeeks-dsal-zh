# 仅允许相邻交换时要排序的交换数量

> 原文:[https://www . geesforgeks . org/number-互换-排序-相邻-互换-允许/](https://www.geeksforgeeks.org/number-swaps-sort-adjacent-swapping-allowed/)

给定非负整数的数组 arr[]。我们可以对数组中任意两个相邻的元素执行交换操作。找到按升序排列数组所需的最小交换次数。

**示例:**

```
Input  : arr[] = {3, 2, 1}
Output : 3
We need to do following swaps
(3, 2), (3, 1) and (1, 2)

Input  : arr[] = {1, 20, 6, 4, 5}
Output : 5
```

这个问题有一个有趣的解决方案。可以利用需要的互换次数等于[反转](https://www.geeksforgeeks.org/counting-inversions/)次数的事实来解决。所以我们基本上需要[计算数组](https://www.geeksforgeeks.org/counting-inversions/)中的逆序。
事实可以通过以下观察来确定:
1)排序的数组没有反转。
2)相邻交换可以减少一次反转。执行 x 个相邻交换可以减少数组中的 x 个反转。

## C++

```
// C++ program to count number of swaps required
// to sort an array when only swapping of adjacent
// elements is allowed.
#include <bits/stdc++.h>

/* This function merges two sorted arrays and returns inversion
   count in the arrays.*/
int merge(int arr[], int temp[], int left, int mid, int right)
{
    int inv_count = 0;

    int i = left; /* i is index for left subarray*/
    int j = mid;  /* j is index for right subarray*/
    int k = left; /* k is index for resultant merged subarray*/
    while ((i <= mid - 1) && (j <= right))
    {
        if (arr[i] <= arr[j])
            temp[k++] = arr[i++];
        else
        {
            temp[k++] = arr[j++];

            /* this is tricky -- see above explanation/
              diagram for merge()*/
            inv_count = inv_count + (mid - i);
        }
    }

    /* Copy the remaining elements of left subarray
     (if there are any) to temp*/
    while (i <= mid - 1)
        temp[k++] = arr[i++];

    /* Copy the remaining elements of right subarray
     (if there are any) to temp*/
    while (j <= right)
        temp[k++] = arr[j++];

    /*Copy back the merged elements to original array*/
    for (i=left; i <= right; i++)
        arr[i] = temp[i];

    return inv_count;
}

/* An auxiliary recursive function that sorts the input
   array and returns the number of inversions in the
   array. */
int _mergeSort(int arr[], int temp[], int left, int right)
{
    int mid, inv_count = 0;
    if (right > left)
    {
        /* Divide the array into two parts and call
          _mergeSortAndCountInv() for each of the parts */
        mid = (right + left)/2;

        /* Inversion count will be sum of inversions in
           left-part, right-part and number of inversions
           in merging */
        inv_count  = _mergeSort(arr, temp, left, mid);
        inv_count += _mergeSort(arr, temp, mid+1, right);

        /*Merge the two parts*/
        inv_count += merge(arr, temp, left, mid+1, right);
    }

    return inv_count;
}

/* This function sorts the input array and returns the
   number of inversions in the array */
int countSwaps(int arr[], int n)
{
    int temp[n];
    return _mergeSort(arr, temp, 0, n - 1);
}

/* Driver progra to test above functions */
int main(int argv, char** args)
{
    int arr[] = {1, 20, 6, 4, 5};
    int n = sizeof(arr)/sizeof(arr[0]);
    printf("Number of swaps is %d \n", countSwaps(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of
// swaps required to sort an array
// when only swapping of adjacent
// elements is allowed.
import java.io.*;

class GFG {

// This function merges two sorted
// arrays and returns inversion
// count in the arrays.
static int merge(int arr[], int temp[],
            int left, int mid, int right)
{
    int inv_count = 0;

    /* i is index for left subarray*/
    int i = left;

    /* j is index for right subarray*/
    int j = mid;

    /* k is index for resultant merged subarray*/
    int k = left;

    while ((i <= mid - 1) && (j <= right))
    {
        if (arr[i] <= arr[j])
            temp[k++] = arr[i++];
        else
        {
            temp[k++] = arr[j++];

            /* this is tricky -- see above /
             explanation diagram for merge()*/
            inv_count = inv_count + (mid - i);
        }
    }

    /* Copy the remaining elements of left
    subarray (if there are any) to temp*/
    while (i <= mid - 1)
        temp[k++] = arr[i++];

    /* Copy the remaining elements of right
    subarray (if there are any) to temp*/
    while (j <= right)
        temp[k++] = arr[j++];

    /*Copy back the merged elements
    to original array*/
    for (i=left; i <= right; i++)
        arr[i] = temp[i];

    return inv_count;
}

// An auxiliary recursive function that
// sorts the input array and returns
// the number of inversions in the array.
static int _mergeSort(int arr[], int temp[],
                         int left, int right)
{
    int mid, inv_count = 0;
    if (right > left)
    {
        // Divide the array into two parts and
        // call _mergeSortAndCountInv() for
        // each of the parts
        mid = (right + left)/2;

        /* Inversion count will be sum of
        inversions in left-part, right-part
        and number of inversions in merging */
        inv_count = _mergeSort(arr, temp,
                                left, mid);

        inv_count += _mergeSort(arr, temp,
                                mid+1, right);

        /*Merge the two parts*/
        inv_count += merge(arr, temp,
                        left, mid+1, right);
    }

    return inv_count;
}

// This function sorts the input
// array and returns the number
// of inversions in the array
static int countSwaps(int arr[], int n)
{
    int temp[] = new int[n];
    return _mergeSort(arr, temp, 0, n - 1);
}

// Driver Code
public static void main (String[] args)
{

    int arr[] = {1, 20, 6, 4, 5};
    int n = arr.length;
        System.out.println("Number of swaps is "
                           + countSwaps(arr, n));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# python 3 program to count number of swaps required
# to sort an array when only swapping of adjacent
# elements is allowed.
#include <bits/stdc++.h>

#This function merges two sorted arrays and returns inversion count in the arrays.*/
def merge(arr, temp, left, mid, right):
    inv_count = 0

    i = left #i is index for left subarray*/
    j = mid #j is index for right subarray*/
    k = left #k is index for resultant merged subarray*/
    while ((i <= mid - 1) and (j <= right)):
        if (arr[i] <= arr[j]):
            temp[k] = arr[i]
            k += 1
            i += 1
        else:
            temp[k] = arr[j]
            k += 1
            j += 1

            #this is tricky -- see above explanation/
            # diagram for merge()*/
            inv_count = inv_count + (mid - i)

    #Copy the remaining elements of left subarray
    # (if there are any) to temp*/
    while (i <= mid - 1):
        temp[k] = arr[i]
        k += 1
        i += 1

    #Copy the remaining elements of right subarray
    # (if there are any) to temp*/
    while (j <= right):
        temp[k] = arr[j]
        k += 1
        j += 1

    # Copy back the merged elements to original array*/
    for i in range(left,right+1,1):
        arr[i] = temp[i]

    return inv_count

#An auxiliary recursive function that sorts the input
# array and returns the number of inversions in the
# array. */
def _mergeSort(arr, temp, left, right):
    inv_count = 0
    if (right > left):
        # Divide the array into two parts and call
        #_mergeSortAndCountInv()
        # for each of the parts */
        mid = int((right + left)/2)

        #Inversion count will be sum of inversions in
        # left-part, right-part and number of inversions
        # in merging */
        inv_count = _mergeSort(arr, temp, left, mid)
        inv_count += _mergeSort(arr, temp, mid+1, right)

        # Merge the two parts*/
        inv_count += merge(arr, temp, left, mid+1, right)

    return inv_count

#This function sorts the input array and returns the
#number of inversions in the array */
def countSwaps(arr, n):
    temp = [0 for i in range(n)]
    return _mergeSort(arr, temp, 0, n - 1)

# Driver progra to test above functions */
if __name__ == '__main__':
    arr = [1, 20, 6, 4, 5]
    n = len(arr)
    print("Number of swaps is",countSwaps(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to count number of
// swaps required to sort an array
// when only swapping of adjacent
// elements is allowed.
using System;

class GFG
{

// This function merges two
// sorted arrays and returns
// inversion count in the arrays.
static int merge(int []arr, int []temp,
                 int left, int mid,
                 int right)
{
    int inv_count = 0;

    /* i is index for
    left subarray*/
    int i = left;

    /* j is index for
    right subarray*/
    int j = mid;

    /* k is index for resultant
    merged subarray*/
    int k = left;

    while ((i <= mid - 1) &&
           (j <= right))
    {
        if (arr[i] <= arr[j])
            temp[k++] = arr[i++];
        else
        {
            temp[k++] = arr[j++];

            /* this is tricky -- see above /
            explanation diagram for merge()*/
            inv_count = inv_count + (mid - i);
        }
    }

    /* Copy the remaining elements
    of left subarray (if there are
    any) to temp*/
    while (i <= mid - 1)
        temp[k++] = arr[i++];

    /* Copy the remaining elements
    of right subarray (if there are
    any) to temp*/
    while (j <= right)
        temp[k++] = arr[j++];

    /*Copy back the merged
    elements to original array*/
    for (i=left; i <= right; i++)
        arr[i] = temp[i];

    return inv_count;
}

// An auxiliary recursive function
// that sorts the input array and
// returns the number of inversions
// in the array.
static int _mergeSort(int []arr, int []temp,
                      int left, int right)
{
    int mid, inv_count = 0;
    if (right > left)
    {
        // Divide the array into two parts
        // and call _mergeSortAndCountInv()
        // for each of the parts
        mid = (right + left) / 2;

        /* Inversion count will be sum of
        inversions in left-part, right-part
        and number of inversions in merging */
        inv_count = _mergeSort(arr, temp,
                               left, mid);

        inv_count += _mergeSort(arr, temp,
                                mid + 1, right);

        /*Merge the two parts*/
        inv_count += merge(arr, temp,
                           left, mid + 1, right);
    }

    return inv_count;
}

// This function sorts the input
// array and returns the number
// of inversions in the array
static int countSwaps(int []arr, int n)
{
    int []temp = new int[n];
    return _mergeSort(arr, temp, 0, n - 1);
}

// Driver Code
public static void Main ()
{

    int []arr = {1, 20, 6, 4, 5};
    int n = arr.Length;
        Console.Write("Number of swaps is " +
                         countSwaps(arr, n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of swaps required
// to sort an array when only swapping of adjacent
// elements is allowed.

/* This function merges two sorted arrays and returns inversion
   count in the arrays.*/
function merge(&$arr, &$temp, $left, $mid, $right)
{
    $inv_count = 0;

    $i = $left; /* i is index for left subarray*/
    $j = $mid;  /* j is index for right subarray*/
    $k = $left; /* k is index for resultant merged subarray*/
    while (($i <= $mid - 1) && ($j <= $right))
    {
        if ($arr[$i] <= $arr[$j])
            $temp[$k++] = $arr[$i++];
        else
        {
            $temp[$k++] = $arr[$j++];

            /* this is tricky -- see above explanation/
              diagram for merge()*/
            $inv_count = $inv_count + ($mid - $i);
        }
    }

    /* Copy the remaining elements of left subarray
     (if there are any) to temp*/
    while ($i <= $mid - 1)
        $temp[$k++] = $arr[$i++];

    /* Copy the remaining elements of right subarray
     (if there are any) to temp*/
    while ($j <= $right)
        $temp[$k++] = $arr[$j++];

    /*Copy back the merged elements to original array*/
    for ($i=$left; $i <= $right; $i++)
        $arr[$i] = $temp[$i];

    return $inv_count;
}

/* An auxiliary recursive function that sorts the input
   array and returns the number of inversions in the
   array. */
function _mergeSort(&$arr, &$temp, $left, $right)
{
    $inv_count = 0;
    if ($right > $left)
    {
        /* Divide the array into two parts and call
          _mergeSortAndCountInv() for each of the parts */
        $mid = intval(($right + $left)/2);

        /* Inversion count will be sum of inversions in
           left-part, right-part and number of inversions
           in merging */
        $inv_count  = _mergeSort($arr, $temp, $left, $mid);
        $inv_count += _mergeSort($arr, $temp, $mid+1, $right);

        /*Merge the two parts*/
        $inv_count += merge($arr, $temp, $left, $mid+1, $right);
    }

    return $inv_count;
}

/* This function sorts the input array and returns the
   number of inversions in the array */
function countSwaps(&$arr, $n)
{
    $temp = array_fill(0,$n,NULL);
    return _mergeSort($arr, $temp, 0, $n - 1);
}

/* Driver progra to test above functions */

$arr = array(1, 20, 6, 4, 5);
$n = sizeof($arr)/sizeof($arr[0]);
echo "Number of swaps is ". countSwaps($arr, $n);
return 0;
?>
```

## java 描述语言

```
<script>
// Javascript program to count number of
// swaps required to sort an array
// when only swapping of adjacent
// elements is allowed.

    // This function merges two sorted
    // arrays and returns inversion
    // count in the arrays.
    function merge(arr,temp,left,mid,right)
    {
         let inv_count = 0;

        /* i is index for left subarray*/
        let i = left;

        /* j is index for right subarray*/
        let j = mid;

        /* k is index for resultant merged subarray*/
        let k = left;

        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] <= arr[j])
                temp[k++] = arr[i++];
            else
            {
                temp[k++] = arr[j++];

                /* this is tricky -- see above /
                 explanation diagram for merge()*/
                inv_count = inv_count + (mid - i);
            }
        }

        /* Copy the remaining elements of left
        subarray (if there are any) to temp*/
        while (i <= mid - 1)
            temp[k++] = arr[i++];

        /* Copy the remaining elements of right
        subarray (if there are any) to temp*/
        while (j <= right)
            temp[k++] = arr[j++];

        /*Copy back the merged elements
        to original array*/
        for (i=left; i <= right; i++)
            arr[i] = temp[i];

        return inv_count;
    }

    // An auxiliary recursive function that
    // sorts the input array and returns
    // the number of inversions in the array.
    function _mergeSort(arr,temp,left,right)
    {
        let mid, inv_count = 0;
        if (right > left)
        {
            // Divide the array into two parts and
            // call _mergeSortAndCountInv() for
            // each of the parts
            mid = Math.floor((right + left)/2);

            /* Inversion count will be sum of
            inversions in left-part, right-part
            and number of inversions in merging */
            inv_count = _mergeSort(arr, temp,
                                    left, mid);

            inv_count += _mergeSort(arr, temp,
                                    mid+1, right);

            /*Merge the two parts*/
            inv_count += merge(arr, temp,
                            left, mid+1, right);
        }

        return inv_count;
    }

    // This function sorts the input
    // array and returns the number
    // of inversions in the array
    function countSwaps(arr,n)
    {
        let temp = new Array(n);
        for(let i = 0; i < n; i++)
        {
            temp[i] = 0;
        }
        return _mergeSort(arr, temp, 0, n - 1);
    }

    // Driver Code
    let arr=[1, 20, 6, 4, 5];
    let n = arr.length;
    document.write("Number of swaps is "
                           + countSwaps(arr, n));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
Number of swaps is 5
```

**时间复杂度:** O(n Log n)
**相关帖子:**
[对数组进行排序所需的最小交换次数](https://www.geeksforgeeks.org/minimum-number-swaps-required-sort-array/)

**参考文献:**
[http://stackoverflow . com/questions/20990127/通过交换对相邻元素进行排序使用最小交换](http://stackoverflow.com/questions/20990127/sorting-a-sequence-by-swapping-adjacent-elements-using-minimum-swaps)

本文由**希瓦姆·古普塔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。