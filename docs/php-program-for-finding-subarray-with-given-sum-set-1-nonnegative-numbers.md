# 寻找给定和的子阵的 Php 程序–集合 1(非负数)

> 原文:[https://www . geeksforgeeks . org/PHP-用于查找给定和集 1 的子数组的程序-非负数/](https://www.geeksforgeeks.org/php-program-for-finding-subarray-with-given-sum-set-1-nonnegative-numbers/)

给定一个非负整数的未排序数组，找到一个与给定数字相加的连续子数组。
**例:**

```
Input: arr[] = {1, 4, 20, 3, 10, 5}, sum = 33
Output: Sum found between indexes 2 and 4
Sum of elements between indices
2 and 4 is 20 + 3 + 10 = 33

Input: arr[] = {1, 4, 0, 0, 3, 10, 5}, sum = 7
Output: Sum found between indexes 1 and 4
Sum of elements between indices
1 and 4 is 4 + 0 + 0 + 3 = 7

Input: arr[] = {1, 4}, sum = 0
Output: No subarray found
There is no subarray with 0 sum
```

可能有多个以和作为给定和的子阵列。以下解决方案首先打印这样的子阵列。

**<u>简单方法:</u>** 一个简单的解决方法是逐个考虑所有子阵列，检查每个子阵列的和。下面的程序实现了简单的解决方案。运行两个循环:外环选择一个起点 I，内环尝试从 I 开始的所有子阵列。
**算法:**

1.  从头到尾遍历数组。
2.  从每个索引开始另一个循环，从 *i* 到数组结束，从 I 开始获取所有子数组，保持一个变量和来计算和。
3.  对于内部循环中的每个索引，更新 *sum = sum + array[j]*
4.  如果总和等于给定的总和，则打印子阵列。

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple program to print subarray
// with sum as given sum 

/* Returns true if the there is a 
   subarray of arr[] with sum equal 
   to 'sum' otherwise returns false. 
   Also, prints the result */
function subArraySum($arr, $n, $sum)
{
    $curr_sum; $i; $j;

    // Pick a starting point
    for ($i = 0; $i < $n; $i++)
    {
        $curr_sum = $arr[$i];

        // Try all subarrays starting 
        // with 'i'
        for ($j = $i + 1; $j <= $n; $j++)
        {
            if ($curr_sum == $sum)
            {
                echo "Sum found between indexes ", 
                      $i, " and ", $j-1 ;
                return 1;
            }
            if ($curr_sum > $sum || $j == $n)
                break;
        $curr_sum = $curr_sum + $arr[$j];
        }
    }

    echo "No subarray found";
    return 0;
}

// Driver Code
$arr= array(15, 2, 4, 8, 9, 5, 10, 23);
$n = sizeof($arr);
$sum = 23;
subArraySum($arr, $n, $sum);
return 0;
// This code is contributed by AJit
?>
```

**输出:**

```
Sum found between indexes 1 and 4
```

**复杂度分析:**

*   **时间复杂度:**最坏情况下的 O(n^2)。
    嵌套循环用于遍历数组，因此时间复杂度为 O(n^2)
*   **空间复杂度:** O(1)。
    因为需要恒定的额外空间。

**<u>高效方法:</u>** 有一个想法，如果数组的所有元素都是正的。如果一个子阵列的总和大于给定的总和，那么向当前子阵列添加元素的总和不可能是 *x* (给定的总和)。想法是使用类似的方法来滑动窗口。从一个空的子阵列开始，向子阵列添加元素，直到总和小于 *x* 。如果总和大于 *x* ，则从当前子阵列的开始处移除元素。
**算法:**

1.  创建三个变量， *l=0，sum = 0*
2.  从头到尾遍历数组。
3.  通过添加当前元素更新变量和，*和=和+数组[i]*
4.  如果和大于给定的和，将变量和更新为*和=和–数组[l]* ，将 l 更新为，l++。
5.  如果总和等于给定总和，打印子阵列并中断循环。

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
/* An efficient program to print 
   subarray with sum as given sum */

/* Returns true if the there is a 
   subarray of arr[] with sum equal 
   to 'sum' otherwise returns false. 
   Also, prints the result */
function subArraySum($arr, $n, $sum)
{
    /* Initialize curr_sum as value 
       of first element and starting 
       point as 0 */
    $curr_sum = $arr[0]; 
    $start = 0; $i;

    /* Add elements one by one to curr_sum 
       and if the curr_sum exceeds the sum, 
       then remove starting element */
    for ($i = 1; $i <= $n; $i++)
    {
        // If curr_sum exceeds the sum, 
        // then remove the starting elements
        while ($curr_sum > $sum and 
               $start < $i - 1)
        {
            $curr_sum = $curr_sum - 
                        $arr[$start];
            $start++;
        }

        // If curr_sum becomes equal to 
        // sum, then return true
        if ($curr_sum == $sum)
        {
            echo "Sum found between indexes",
                 " ", $start, " ", "and ", 
                 " ", $i - 1;
            return 1;
        }

        // Add this element to curr_sum
        if ($i < $n)
        $curr_sum = $curr_sum + $arr[$i];
    }

    // If we reach here, then no subarray
    echo "No subarray found";
    return 0;
}

// Driver Code
$arr = array(15, 2, 4, 8, 
             9, 5, 10, 23);
$n = count($arr);
$sum = 23;
subArraySum($arr, $n, $sum);
// This code is contributed by anuj_67.
?>
```

**输出:**

```
Sum found between indexes 1 and 4
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    只需要遍历一次数组。所以时间复杂度是 O(n)。
*   **空间复杂度:** O(1)。
    因为需要恒定的额外空间。

详情请参考[求给定和的子阵|集合 1(非负数)](https://www.geeksforgeeks.org/find-subarray-with-given-sum/)整篇文章！