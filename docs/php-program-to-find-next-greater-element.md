# 寻找下一个更大元素的 Php 程序

> 原文:[https://www . geesforgeks . org/PHP-program-to-find-next-greater-element/](https://www.geeksforgeeks.org/php-program-to-find-next-greater-element/)

给定一个数组，为每个元素打印下一个更大的元素(NGE)。元素 x 的下一个较大元素是数组中 x 右侧的第一个较大元素。不存在更大元素的元素，将下一个更大的元素视为-1。

**示例:**

1.  对于数组，最右边的元素总是将下一个较大的元素作为-1。
2.  对于按降序排序的数组，所有元素的下一个较大元素为-1。
3.  对于输入数组[4，5，2，25]，每个元素的下一个较大元素如下。

```
Element       NGE
   4      -->   5
   5      -->   25
   2      -->   25
   25     -->   -1
```

**d)** 对于输入数组[13，7，6，12]，每个元素的下一个较大元素如下。

```
  Element        NGE
   13      -->    -1
   7       -->     12
   6       -->     12
   12      -->     -1
```

**方法 1(简单)**
使用两个循环:外循环逐个拾取所有元素。内环为外环拾取的元素寻找第一个较大的元素。如果找到更大的元素，则该元素被打印为下一个，否则，打印-1。

下面是上述方法的实现:

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Simple PHP program to print next
// greater elements in a given array

/* prints element and NGE pair for 
   all elements of arr[] of size n */
function printNGE($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
    {
        $next = -1;
        for ($j = $i + 1; $j < $n; $j++)
        {
            if ($arr[$i] < $arr[$j])
            {
                $next = $arr[$j];
                break;
            }
        }
        echo $arr[$i]." -- ". $next."
";

    }
}

    // Driver Code
    $arr= array(11, 13, 21, 3);
    $n = count($arr);
    printNGE($arr, $n);

// This code is contributed by Sam007
?>
```

**Output**

```
11 -- 13
13 -- 21
21 -- -1
3 -- -1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

更多详情请参考[下一个更大元素](https://www.geeksforgeeks.org/next-greater-element/)的完整文章！