# 排列给定数字形成最大数字的 Php 程序

> 原文:[https://www . geesforgeks . org/PHP-程序-排列-给定数字-形成最大数字/](https://www.geeksforgeeks.org/php-program-to-arrange-given-numbers-to-form-the-biggest-number/)

给定一组数字，以产生最大值的方式排列它们。例如，如果给定的数字是{54，546，548，60}，则排列 6054854654 给出最大值。如果给定的数字是{1，34，3，98，9，76，45，4}，那么排列 998764543431 给出最大值。

我们想到的一个**简单的解决方法**就是把所有的数字按照降序排序，但是单纯的排序是行不通的。例如，548 大于 60，但在输出中 60 在 548 之前。作为第二个例子，98 大于 9，但是在输出中 9 在 98 之前。

那我们该怎么做呢？想法是使用任何基于[比较的排序](https://www.geeksforgeeks.org/analysis-of-different-sorting-techniques/)算法。
在使用的排序算法中，不使用默认的比较，而是编写一个比较函数 **myCompare()** 并用它来排序数字。

给定两个数字 **X** 和 **Y** ，那么 **myCompare()** 应该如何决定先放哪个数字——我们比较两个数字 XY (Y 附加在 X 的末尾)和 YX (X 附加在 Y 的末尾)。如果 **XY** 比较大，那么输出中 X 应该在 Y 之前，否则 Y 应该在之前。例如，让 X 和 Y 分别为 542 和 60。为了比较 X 和 Y，我们比较了 54260 和 60542。因为 60542 大于 54260，所以我们把 Y 放在第一位。

下面是上述方法的实现。
为了保持代码简单，数字被视为字符串，使用向量代替普通数组。

下面是上述方法的实现:

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Given an array of numbers, program 
// to arrange the numbers to form the
// largest number 

// A comparison function which is used
// by sort() in printLargest() 
function myCompare($X, $Y) 
{ 
    // First append Y at the end of X 
    $XY = $Y.$X; 

    // Then append X at the end of Y 
    $YX = $X.$Y; 

    // Now see which of the two formed
    // numbers is greater 
    return strcmp($XY, $YX) > 0 ? 1: 0; 
} 

// The main function that prints the
// arrangement with the largest value. 
// The function accepts a vector of strings 
function printLargest($arr) 
{ 
    // Sort the numbers using library sort 
    // function. The function uses our 
    // comparison function myCompare() to 
    // compare two strings. 
    usort($arr, "myCompare"); 

    for ($i = 0; $i < count($arr) ; $i++ ) 
        echo $arr[$i]; 
} 

// Driver Code
$arr = array("54", "546", "548", "60"); 
printLargest($arr); 

// This code is contributed by rathbhupendra
?>
```

**输出:**

```
6054854654
```

**时间复杂度:**O(nlogn)**排序**被认为运行时间复杂度为 O(nlogn)，for 循环在 O(n)时间内运行。
**辅助空间:** O(1)。

更多详情请参考[整篇文章排列给定数字形成最大数字|集合 1](https://www.geeksforgeeks.org/given-an-array-of-numbers-arrange-the-numbers-to-form-the-biggest-number/) ！