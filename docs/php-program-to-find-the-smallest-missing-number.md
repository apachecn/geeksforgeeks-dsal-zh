# 寻找最小缺失数的 Php 程序

> 原文:[https://www . geeksforgeeks . org/PHP-程序查找最小缺失数/](https://www.geeksforgeeks.org/php-program-to-find-the-smallest-missing-number/)

给定一个由 n 个不同整数组成的排序的数组，其中每个整数都在 0 到 m-1 和 m > n 的范围内。找出数组中缺少的最小数字。

例子

```
Input: {0, 1, 2, 6, 9}, n = 5, m = 10 
Output: 3

Input: {4, 5, 10, 11}, n = 4, m = 12 
Output: 0

Input: {0, 1, 2, 3}, n = 4, m = 5 
Output: 4

Input: {0, 1, 2, 3, 4, 5, 6, 7, 10}, n = 9, m = 11 
Output: 8
```

感谢拉维钱德拉提出以下两种方法。

**法 1(用** [**【二分搜索法】**](https://www.geeksforgeeks.org/binary-search/) **)**
为 i = 0 至 m-1，在阵中做二分搜索法为 I。如果数组中没有 I，则返回 i.
时间复杂度:O(m log n)

**方法 2(**[](https://www.geeksforgeeks.org/linear-search/)****)**
如果 arr[0]不是 0，返回 0。否则，从索引 0 开始遍历输入数组，对于每对元素 a[i]和 a[i+1]，找出它们之间的区别。如果差值大于 1，则 a[i]+1 是缺失的数字。
时间复杂度:O(n)**

****方法三(使用改良二分搜索法)**
感谢亚辛和**杰姆**提出这个方法。
在标准二分搜索法过程中，将待搜索元素与中间元素进行比较，根据比较结果，我们决定是搜索结束，还是前往左半部分或右半部分。
在该方法中，我们修改了标准二分搜索法算法，将中间元素与其索引进行比较，并在此基础上进行决策。**

*   **如果第一个元素与其索引不同，则返回第一个索引**
*   **否则得到中间指数，比如说中间

    *   如果 arr[mid]大于 mid，则所需元素位于左半部分。
    *   否则所需元素位于右半部分。** 

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP program to find the
// smallest elements missing
// in a sorted array.

// function that returns 
// smallest elements missing
// in a sorted array.
function findFirstMissing($array, $start, $end)
{
    if ($start > $end)
        return $end + 1;

    if ($start != $array[$start])
        return $start;

    $mid = ($start + $end) / 2;

    // Left half has all 
    // elements from 0 to mid
    if ($array[$mid] == $mid)
        return findFirstMissing($array, 
                                $mid + 1, 
                                $end);

    return findFirstMissing($array, 
                            $start, 
                            $mid);
}

    // Driver Code
    $arr = array (0, 1, 2, 3, 4, 5, 6, 7, 10);
    $n = count($arr);
    echo "Smallest missing element is " ,
          findFirstMissing($arr, 2, $n - 1);

// This code Contributed by Ajit.
?>
```

 **Please refer complete article on [Find the smallest missing number](https://www.geeksforgeeks.org/find-the-first-missing-number/) for more details!**