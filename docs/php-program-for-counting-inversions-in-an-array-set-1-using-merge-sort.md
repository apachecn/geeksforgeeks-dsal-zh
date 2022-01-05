# 用于计算数组中反转的 Php 程序–集合 1(使用合并排序)

> 原文:[https://www . geesforgeks . org/PHP-用于计数的程序-数组中的反转-集合-1-使用-合并-排序/](https://www.geeksforgeeks.org/php-program-for-counting-inversions-in-an-array-set-1-using-merge-sort/)

*数组的反转计数*表示数组离排序有多远(或多近)。如果数组已经排序，则反转计数为 0，但是如果数组以相反的顺序排序，则反转计数为最大值。
形式上讲，如果 a[I]>a[j]I<j
**例:**

```
Input: arr[] = {8, 4, 2, 1}
Output: 6
Explanation: Given array has six inversions:
(8, 4), (4, 2), (8, 2), (8, 1), (4, 1), (2, 1).

Input: arr[] = {3, 1, 2}
Output: 2
Explanation: Given array has two inversions:
(3, 1), (3, 2) 
```

**<u>方法(简单):</u>**

**方法:**遍历数组，对于每个索引，找到数组右侧较小元素的数量。这可以使用嵌套循环来完成。合计数组中所有索引的计数，并打印总和。

**算法:**

1.  从头到尾遍历数组
2.  对于每个元素，使用另一个循环查找小于当前数字的元素计数，直到该索引。
3.  合计每个索引的反转计数。
4.  打印倒计数。

**实施:**

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php 
// PHP program to Count Inversions
// in an array
function getInvCount(&$arr, $n)
{
    $inv_count = 0;
    for ($i = 0; $i < $n - 1; $i++)
        for ($j = $i + 1; $j < $n; $j++)
            if ($arr[$i] > $arr[$j])
                $inv_count++;

    return $inv_count;
}

// Driver Code
$arr = array(1, 20, 6, 4, 5 );
$n = sizeof($arr);
echo "Number of inversions are ", 
           getInvCount($arr, $n);
// This code is contributed by ita_c
?>
```

**输出:**

```
 Number of inversions are 5
```

**复杂度分析:**

*   **时间复杂度:** O(n^2)，需要两个嵌套循环从头到尾遍历数组，所以时间复杂度为 O(n^2)
*   **空间**复杂度 **:** O(1)，不需要额外空间。

更多详细信息，请参考完整的文章[计算数组中的逆序|集合 1(使用合并排序)](https://www.geeksforgeeks.org/counting-inversions/)！