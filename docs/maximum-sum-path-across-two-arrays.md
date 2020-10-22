# 两个数组中的最大和路径

> 原文： [https://www.geeksforgeeks.org/maximum-sum-path-across-two-arrays/](https://www.geeksforgeeks.org/maximum-sum-path-across-two-arrays/)

给定两个排序的数组，这样该数组可能具有一些公共元素。 查找从任何数组的开始到两个数组中的任何一个数组的结尾的最大和路径的和。 我们只能在公共元素处从一个数组切换到另一个数组。

**注意**：公用元素不必具有相同的索引。

**预期时间复杂度**：`O(m + n)`，其中`m`是`ar1[]`中的元素数，`n`是`ar2[]`中的元素数。

**示例**：

```
Input: ar1[] = {2, 3, 7, 10, 12}
       ar2[] = {1, 5, 7, 8}
Output: 35

Explanation: 35 is sum of 1 + 5 + 7 + 10 + 12.
We start from the first element of arr2 which is 1, then we
move to 5, then 7\.  From 7, we switch to ar1 (as 7 is common)
and traverse 10 and 12.

Input: ar1[] = {10, 12}
       ar2 = {5, 7, 9}
Output: 22

Explanation: 22 is the sum of 10 and 12.
Since there is no common element, we need to take all 
elements from the array with more sum.

Input: ar1[] = {2, 3, 7, 10, 12, 15, 30, 34}
        ar2[] = {1, 5, 7, 8, 10, 15, 16, 19}
Output: 122

Explanation: 122 is sum of 1, 5, 7, 8, 10, 12, 15, 30, 34

```



**有效方法**： 的想法是做类似于[归并排序](http://geeksquiz.com/merge-sort/)的合并过程的操作。 这涉及计算两个数组的所有公共点之间的元素之和。 只要有一个共同点，就比较两个和并将两个的最大值相加。

**算法**：

1.  创建一些变量，`result`，`sum1`，`sum2`。 将结果初始化为 0。还将两个变量`sum1`和`sum2`初始化为 0。这里，`sum1`和`sum2`用于分别将元素的和存储在`ar1[]`和`ar2[]`中。 这些总和在两个共同点之间。

2.  现在运行一个循环以遍历两个数组的元素。 遍历时，按以下顺序比较数组 1 和数组 2 的当前元素。

    1.  如果`ar1[]`的当前元素小于`ar2[]`的当前元素，则更新`sum1`，否则，如果`ar2[]`较小，然后更新`sum2`。

    2.  如果`ar1[]`和`ar2[]`的当前元素相同，则取`sum1`和`sum2`的最大值，并将其加到结果中。 还将公共元素添加到结果中。

    3.  可以将此步骤与合并两个**排序的**数组进行比较，如果处理了两个当前数组索引中的最小元素，则可以保证如果有任何公共元素，则将它们一起处理。 可以处理两个公共元素之间的元素总和。

**实现**：

## C++

```cpp
// C++ program to find maximum sum path
#include <iostream>
using namespace std;
 
// Utility function to find maximum of two integers
int max(int x, int y) { return (x > y) ? x : y; }
 
// This function returns the sum of elements on maximum path
// from beginning to end
int maxPathSum(int ar1[], int ar2[], int m, int n)
{
    // initialize indexes for ar1[] and ar2[]
    int i = 0, j = 0;
 
    // Initialize result and current sum through ar1[] and
    // ar2[].
    int result = 0, sum1 = 0, sum2 = 0;
 
    // Below 3 loops are similar to merge in merge sort
    while (i < m && j < n) 
    {
        // Add elements of ar1[] to sum1
        if (ar1[i] < ar2[j])
            sum1 += ar1[i++];
 
        // Add elements of ar2[] to sum2
        else if (ar1[i] > ar2[j])
            sum2 += ar2[j++];
 
        else // we reached a common point
        {
            // Take the maximum of two sums and add to
            // result
            result += max(sum1, sum2);
 
            // Update sum1 and sum2 for elements after this
            // intersection point
            sum1 = 0, sum2 = 0;
 
            // Keep updating result while there are more
            // common elements
            int temp = i;
            while (i < m && ar1[i] == ar2[j])
                sum1 += ar1[i++];
 
            while (j < n && ar1[temp] == ar2[j])
                sum2 += ar2[j++];
 
            result += max(sum1, sum2);
 
            sum1 = 0, sum2 = 0;
        }
    }
 
    // Add remaining elements of ar1[]
    while (i < m)
        sum1 += ar1[i++];
 
    // Add remaining elements of ar2[]
    while (j < n)
        sum2 += ar2[j++];
 
    // Add maximum of two sums of remaining elements
    result += max(sum1, sum2);
 
    return result;
}
 
// Driver code
int main()
{
    int ar1[] = { 2, 3, 7, 10, 12, 15, 30, 34 };
    int ar2[] = { 1, 5, 7, 8, 10, 15, 16, 19 };
    int m = sizeof(ar1) / sizeof(ar1[0]);
    int n = sizeof(ar2) / sizeof(ar2[0]);
   
    // Function call
    cout << "Maximum sum path is "
         << maxPathSum(ar1, ar2, m, n);
    return 0;
}
```

## Java

```java
// JAVA program to find maximum sum path
class MaximumSumPath 
{
    // Utility function to find maximum of two integers
    int max(int x, int y) { return (x > y) ? x : y; }
 
    // This function returns the sum of elements on maximum
    // path from beginning to end
    int maxPathSum(int ar1[], int ar2[], int m, int n)
    {
        // initialize indexes for ar1[] and ar2[]
        int i = 0, j = 0;
 
        // Initialize result and current sum through ar1[]
        // and ar2[].
        int result = 0, sum1 = 0, sum2 = 0;
 
        // Below 3 loops are similar to merge in merge sort
        while (i < m && j < n) 
        {
            // Add elements of ar1[] to sum1
            if (ar1[i] < ar2[j])
                sum1 += ar1[i++];
 
            // Add elements of ar2[] to sum2
            else if (ar1[i] > ar2[j])
                sum2 += ar2[j++];
 
            // we reached a common point
            else
            {
                // Take the maximum of two sums and add to
                // result
                result += max(sum1, sum2);
 
                // Update sum1 and sum2 for elements after
                // this intersection point
                sum1 = 0;
                sum2 = 0;
 
                // Keep updating result while there are more
                // common elements
                int temp = i;
                while (i < m && ar1[i] == ar2[j])
                    sum1 += ar1[i++];
 
                while (j < n && ar1[temp] == ar2[j])
                    sum2 += ar2[j++];
 
                result += max(sum1, sum2);
 
                sum1 = 0;
                sum2 = 0;
            }
        }
 
        // Add remaining elements of ar1[]
        while (i < m)
            sum1 += ar1[i++];
 
        // Add remaining elements of ar2[]
        while (j < n)
            sum2 += ar2[j++];
 
        // Add maximum of two sums of remaining elements
        result += max(sum1, sum2);
 
        return result;
    }
 
    // Driver code
    public static void main(String[] args)
    {
        MaximumSumPath sumpath = new MaximumSumPath();
        int ar1[] = { 2, 3, 7, 10, 12, 15, 30, 34 };
        int ar2[] = { 1, 5, 7, 8, 10, 15, 16, 19 };
        int m = ar1.length;
        int n = ar2.length;
       
        // Function call
        System.out.println(
            "Maximum sum path is :"
            + sumpath.maxPathSum(ar1, ar2, m, n));
    }
}
 
// This code has been contributed by Mayank Jaiswal
```

## Python

```py
# Python program to find maximum sum path
 
# This function returns the sum of elements on maximum path from
# beginning to end
 
 
def maxPathSum(ar1, ar2, m, n):
 
    # initialize indexes for ar1[] and ar2[]
    i, j = 0, 0
 
    # Initialize result and current sum through ar1[] and ar2[]
    result, sum1, sum2 = 0, 0, 0
 
    # Below 3 loops are similar to merge in merge sort
    while (i < m and j < n):
 
        # Add elements of ar1[] to sum1
        if ar1[i] < ar2[j]:
            sum1 += ar1[i]
            i += 1
 
        # Add elements of ar2[] to sum1
        elif ar1[i] > ar2[j]:
            sum2 += ar2[j]
            j += 1
 
        else:   # we reached a common point
 
            # Take the maximum of two sums and add to result
            result += max(sum1, sum2)
 
            # Update sum1 and sum2 for elements after this intersection point
            sum1, sum2 = 0, 0
 
            # Keep updating result while there are more common elements
            temp = i
            while i < m and ar1[i] == ar2[j]:
                sum1 += ar1[i];
                i += 1
            while j<n and ar1[temp] == ar2[j]:
                sum2 += ar2[j]
                j += 1
            result += max(sum1,sum2)
            sum1 = sum2 = 0;           
 
    # Add remaining elements of ar1[]
    while i < m:
        sum1 += ar1[i]
        i += 1
    # Add remaining elements of b[]
    while j < n:
        sum2 += ar2[j]
        j += 1
 
    # Add maximum of two sums of remaining elements
    result += max(sum1, sum2)
 
    return result
 
 
# Driver code
ar1 = [2, 3, 7, 10, 12, 15, 30, 34]
ar2 = [1, 5, 7, 8, 10, 15, 16, 19]
m = len(ar1)
n = len(ar2)
 
# Function call
print "Maximum sum path is", maxPathSum(ar1, ar2, m, n)
 
# This code is contributed by __Devesh Agrawal__
```

## C#

```cs
// C# program for Maximum Sum Path in
// Two Arrays
using System;
 
class GFG {
 
    // Utility function to find maximum
    // of two integers
    static int max(int x, int y) { return (x > y) ? x : y; }
 
    // This function returns the sum of
    // elements on maximum path from
    // beginning to end
    static int maxPathSum(int[] ar1, int[] ar2, int m,
                          int n)
    {
 
        // initialize indexes for ar1[]
        // and ar2[]
        int i = 0, j = 0;
 
        // Initialize result and current
        // sum through ar1[] and ar2[].
        int result = 0, sum1 = 0, sum2 = 0;
 
        // Below 3 loops are similar to
        // merge in merge sort
        while (i < m && j < n) {
            // Add elements of ar1[] to sum1
            if (ar1[i] < ar2[j])
                sum1 += ar1[i++];
 
            // Add elements of ar2[] to sum2
            else if (ar1[i] > ar2[j])
                sum2 += ar2[j++];
 
            // we reached a common point
            else {
 
                // Take the maximum of two
                // sums and add to result
                result += max(sum1, sum2);
 
                // Update sum1 and sum2 for
                // elements after this
                // intersection point
                sum1 = 0;
                sum2 = 0;
 
                // Keep updating result while
                // there are more common
                // elements
                int temp = i;
                while (i < m && ar1[i] == ar2[j])
                    sum1 += ar1[i++];
 
                while (j < n && ar1[temp] == ar2[j])
                    sum2 += ar2[j++];
 
                result += max(sum1, sum2);
 
                sum1 = 0;
                sum2 = 0;
            }
        }
 
        // Add remaining elements of ar1[]
        while (i < m)
            sum1 += ar1[i++];
 
        // Add remaining elements of ar2[]
        while (j < n)
            sum2 += ar2[j++];
 
        // Add maximum of two sums of
        // remaining elements
        result += max(sum1, sum2);
 
        return result;
    }
 
    // Driver code
    public static void Main()
    {
        int[] ar1 = { 2, 3, 7, 10, 12, 15, 30, 34 };
        int[] ar2 = { 1, 5, 7, 8, 10, 15, 16, 19 };
        int m = ar1.Length;
        int n = ar2.Length;
       
        // Function call
        Console.Write("Maximum sum path is :"
                      + maxPathSum(ar1, ar2, m, n));
    }
}
 
// This code is contributed by nitin mittal.
```

## PHP

```php
<?php
// PHP Program to find Maximum Sum 
// Path in Two Arrays
 
// This function returns the sum of
// elements on maximum path
// from beginning to end
function maxPathSum($ar1, $ar2, $m, $n)
{
     
    // initialize indexes for 
    // ar1[] and ar2[]
    $i = 0; 
    $j = 0;
 
    // Initialize result and 
    // current sum through ar1[] 
    // and ar2[].
    $result = 0;
    $sum1 = 0; 
    $sum2 = 0;
 
    // Below 3 loops are similar
    // to merge in merge sort
    while ($i < $m and $j < $n)
    {
         
        // Add elements of
        // ar1[] to sum1
        if ($ar1[$i] < $ar2[$j])
            $sum1 += $ar1[$i++];
 
        // Add elements of 
        // ar2[] to sum2
        else if ($ar1[$i] > $ar2[$j])
            $sum2 += $ar2[$j++];
 
        // we reached a 
        // common point
        else
        {
             
            // Take the maximum of two
            // sums and add to result
            $result += max($sum1, $sum2);
 
            // Update sum1 and sum2 for
            // elements after this
            // intersection point
            $sum1 = 0; 
            $sum2 = 0;
 
            // Keep updating result while
            // there are more common
            // elements
           $temp = $i;
           while ($i < $m && $ar1[$i] == $ar2[$j])
               $sum1 += $ar1[$i++];
 
           while ($j < $n && $ar1[$temp] == $ar2[$j])
               $sum2 += $ar2[$j++];
 
           $result += max($sum1, $sum2);
 
           $sum1 = 0;
           $sum2 = 0;
        }
    }
 
    // Add remaining elements of ar1[]
    while ($i < $m)
        $sum1 += $ar1[$i++];
 
    // Add remaining elements of ar2[]
    while ($j < $n)
        $sum2 += $ar2[$j++];
 
    // Add maximum of two sums 
    // of remaining elements
    $result += max($sum1, $sum2);
 
    return $result;
}
 
    // Driver Code
    $ar1 = array(2, 3, 7, 10, 12, 15, 30, 34);
    $ar2 = array(1, 5, 7, 8, 10, 15, 16, 19);
    $m = count($ar1);
    $n = count($ar2);
 
    // Function call
    echo "Maximum sum path is "
        , maxPathSum($ar1, $ar2, $m, $n);
         
// This code is contributed by anuj_67.
?>
```

输出：

```
Maximum sum path is 122
```

复杂度分析：

+   空间复杂度：`O(1)`。

    不需要任何额外的空间，因此空间复杂度是恒定的。
+   时间复杂度：`O(m + n)`。
    
    在`while`循环的每次迭代中，都会处理两个数组之一的元素。 总共有`m + n`个元素。 因此，时间复杂度为`O(m + n)`。