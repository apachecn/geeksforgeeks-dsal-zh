# 给定和的计数对的 Php 程序

> 原文:[https://www . geeksforgeeks . org/PHP-计数对给定总和的程序/](https://www.geeksforgeeks.org/php-program-for-count-pairs-with-given-sum/)

给定一个整数数组和一个数“和”，求数组中和等于“和”的整数对的个数。

**示例:**

```
Input  :  arr[] = {1, 5, 7, -1}, 
          sum = 6
Output :  2
Pairs with sum 6 are (1, 5) and (7, -1)

Input  :  arr[] = {1, 5, 7, -1, 5}, 
          sum = 6
Output :  3
Pairs with sum 6 are (1, 5), (7, -1) &
                     (1, 5)         

Input  :  arr[] = {1, 1, 1, 1}, 
          sum = 2
Output :  6
There are 3! pairs with sum 2.

Input  :  arr[] = {10, 12, 10, 15, -1, 7, 6, 
                   5, 4, 2, 1, 1, 1}, 
          sum = 11
Output :  9
```

预期时间复杂度 O(n)

**天真的解决方案–**一个**简单的解决方案**是遍历每个元素，检查数组中是否有另一个数字可以添加到其中以给出总和。

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of simple 
// method to find count of
// pairs with given sum.

// Returns number of pairs in 
// arr[0..n-1] with sum equal
// to 'sum'
function getPairsCount($arr, $n, $sum)
{
    // Initialize result
    $count = 0; 

    // Consider all possible pairs 
    // and check their sums
    for ($i = 0; $i < $n; $i++)
        for ($j = $i + 1; $j < $n; $j++)
            if ($arr[$i] + $arr[$j] == $sum)
                $count++;

    return $count;
}

    // Driver Code
    $arr = array(1, 5, 7, -1, 5) ;
    $n = sizeof($arr);
    $sum = 6;
    echo "Count of pairs is "
         , getPairsCount($arr, $n, $sum);

// This code is contributed by nitin mittal.
?>
```

**Output**

```
Count of pairs is 3
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(1)