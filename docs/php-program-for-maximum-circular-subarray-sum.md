# 最大圆子阵和的 Php 程序

> 原文:[https://www . geesforgeks . org/PHP-program-for-maximum-circular-subarray-sum/](https://www.geeksforgeeks.org/php-program-for-maximum-circular-subarray-sum/)

给定 n 个数字(都是+ve 和-ve)，排列成一个圆，求连续数字的最大和。

**示例:**

```
Input: a[] = {8, -8, 9, -9, 10, -11, 12}
Output: 22 (12 + 8 - 8 + 9 - 9 + 10)

Input: a[] = {10, -3, -4, 7, 6, 5, -4, -1} 
Output:  23 (7 + 6 + 5 - 4 -1 + 10) 

Input: a[] = {-1, 40, -14, 7, 6, 5, -4, -1}
Output: 52 (7 + 6 + 5 - 4 - 1 - 1 + 40)
```

**MApproach:** 最大和可以有两种情况:

*   **情况 1:** 对最大和有贡献的元素被排列成没有缠绕。示例:{-10，2，-1，5}，{-2，4，-1，4，-1}。在这种情况下，[卡丹的算法](https://www.geeksforgeeks.org/archives/576)会产生结果。
*   **情况 2:** 对最大和有贡献的元素被布置成使得包裹在那里。示例:{10，-12，11}，{12，-5，4，-8，11}。在这种情况下，我们将包装改为非包装。让我们看看如何。贡献元素的包装意味着非贡献元素的不包装，所以找出非贡献元素的总和，并从总和中减去这个总和。为了找出非贡献的总和，反转每个元素的符号，然后运行卡丹的算法。
    我们的数组就像一个环，我们必须消除最大连续负数，这意味着在倒排数组中最大连续正数。最后，我们比较两种情况下得到的和，并返回两个和的最大值。

以下是上述方法的实现。

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP program for maximum 
// contiguous circular sum problem 

// The function returns maximum 
// circular contiguous sum $a[] 
function maxCircularSum($a, $n) 
{ 
    // Case 1: get the maximum sum 
    // using standard kadane' s algorithm 
    $max_kadane = kadane($a, $n); 

    // Case 2: Now find the maximum  
    // sum that includes corner elements. 
    $max_wrap = 0;
    for ($i = 0; $i < $n; $i++) 
    { 
            $max_wrap += $a[$i]; // Calculate array-sum 
            $a[$i] = -$a[$i]; // invert the array (change sign) 
    } 

    // max sum with corner elements will be: 
    // array-sum - (-max subarray sum of inverted array) 
    $max_wrap = $max_wrap + kadane($a, $n); 

    // The maximum circular sum will be maximum of two sums 
    return ($max_wrap > $max_kadane)? $max_wrap: $max_kadane; 
} 

// Standard Kadane's algorithm to 
// find maximum subarray sum 
// See https://www.geeksforgeeks.org/archives/576 for details 
function kadane($a, $n) 
{ 
    $max_so_far = 0;
    $max_ending_here = 0; 
    for ($i = 0; $i < $n; $i++) 
    { 
        $max_ending_here = $max_ending_here +$a[$i]; 
        if ($max_ending_here < 0) 
            $max_ending_here = 0; 
        if ($max_so_far < $max_ending_here) 
            $max_so_far = $max_ending_here; 
    } 
    return $max_so_far; 
} 

    /* Driver code */
    $a = array(11, 10, -20, 5, -3, -5, 8, -13, 10); 
    $n = count($a);
    echo "Maximum circular sum is ". maxCircularSum($a, $n); 

// This code is contributed by rathbhupendra
?>
```

**输出:**

```
Maximum circular sum is 31
```

**复杂度分析:**

*   **时间复杂度:** O(n)，其中 n 为输入数组中的元素个数。
    因为只需要数组的线性遍历。
*   **辅助空间:** O(1)。
    因为不需要额外的空间。

**注意**如果所有数字都是负数，例如{-1，-2，-3}，上述算法就不起作用了。在这种情况下，它返回 0。这种情况可以通过在运行上述算法之前添加一个预检查来查看是否所有数字都是负数来处理。

详见[最大圆子阵和](https://www.geeksforgeeks.org/maximum-contiguous-circular-sum/)整篇文章！