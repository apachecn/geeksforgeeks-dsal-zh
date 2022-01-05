# 只允许给定数组旋转的情况下，寻找 Sum( i*arr[i])最大值的 Php 程序

> 原文:[https://www . geesforgeks . org/PHP-for-program-for-find-sum-value-iarri-仅允许给定数组上的旋转/](https://www.geeksforgeeks.org/php-program-for-find-maximum-value-of-sum-iarri-with-only-rotations-on-given-array-allowed/)

给定一个数组，只允许对数组进行旋转操作。我们可以随意旋转阵列多次。返回 i*arr[i]的最大可能总和。

**示例:**

```
Input: arr[] = {1, 20, 2, 10}
Output: 72
We can get 72 by rotating array twice.
{2, 10, 1, 20}
20*3 + 1*2 + 10*1 + 2*0 = 72

Input: arr[] = {10, 1, 2, 3, 4, 5, 6, 7, 8, 9}
Output: 330
We can get 330 by rotating array 9 times.
{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
0*1 + 1*2 + 2*3 ... 9*10 = 330
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
A **简单解**就是逐个找到所有的旋转，检查每个旋转的和，返回最大和。这个解的时间复杂度为 O(n <sup>2</sup> )。

我们可以使用**高效解决方案**在 O(n)时间内解决这个问题。
设 R <sub>j</sub> 为 i*arr[i]的值，j 旋转。其思路是由前一次旋转计算下一次旋转值，即由 R <sub>j-1</sub> 计算出 R <sub>j</sub> 。我们可以将结果的初始值计算为 R <sub>0</sub> ，然后继续计算下一个旋转值。

**如何从 R <sub>j-1</sub> 高效计算 R <sub>j</sub> ？**
这可以在 O(1)时间内完成。以下是细节。

```
Let us calculate initial value of i*arr[i] with no rotation
R0 = 0*arr[0] + 1*arr[1] +...+ (n-1)*arr[n-1]

After 1 rotation arr[n-1], becomes first element of array, 
arr[0] becomes second element, arr[1] becomes third element
and so on.
R1 = 0*arr[n-1] + 1*arr[0] +...+ (n-1)*arr[n-2]

R1 - R0 = arr[0] + arr[1] + ... + arr[n-2] - (n-1)*arr[n-1]

After 2 rotations arr[n-2], becomes first element of array, 
arr[n-1] becomes second element, arr[0] becomes third element
and so on.
R2 = 0*arr[n-2] + 1*arr[n-1] +...+ (n-1)*arr[n-3]

R2 - R1 = arr[0] + arr[1] + ... + arr[n-3] - (n-1)*arr[n-2] + arr[n-1]

If we take a closer look at above values, we can observe 
below pattern

Rj - Rj-1 = arrSum - n * arr[n-j]

Where arrSum is sum of all array elements, i.e., 

arrSum = ∑ arr[i]
        0<=i<=n-1 < pre>下面是完整的算法:

```
1) Compute sum of all array elements. Let this sum be 'arrSum'.

2) Compute R0 by doing i*arr[i] for given array. 
   Let this value be currVal.

3) Initialize result: maxVal = currVal // maxVal is result.

// This loop computes Rj from  Rj-1 
4) Do following for j = 1 to n-1
......a) currVal = currVal + arrSum-n*arr[n-j];
......b) If (currVal > maxVal)
            maxVal = currVal   

5) Return maxVal
```

以下是上述想法的实现:

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find max 
// value of i*arr[i] 

// Returns max possible 
// value of i*arr[i]
function maxSum($arr, $n)
{
    // Find array sum and
    // i*arr[i] with no rotation

    // Stores sum of arr[i]
    $arrSum = 0; 

    // Stores sum of i*arr[i]
    $currVal = 0; 
    for ($i = 0; $i < $n; $i++)
    {
        $arrSum = $arrSum + $arr[$i];
        $currVal = $currVal + 
                  ($i * $arr[$i]);
    }

    // Initialize result as
    // 0 rotation sum
    $maxVal = $currVal;

    // Try all rotations one 
    // by one and find the 
    // maximum rotation sum.
    for ($j = 1; $j < $n; $j++)
    {
        $currVal = $currVal + $arrSum - 
                   $n * $arr[$n - $j];
        if ($currVal > $maxVal)
            $maxVal = $currVal;
    }

    // Return result
    return $maxVal;
}

// Driver Code
$arr = array (10, 1, 2, 3, 4,
              5, 6, 7, 8, 9);
$n = sizeof($arr);
echo "Max sum is " ,
     maxSum($arr, $n);

// This code is contributed by m_kit
?>
```

**输出:**

```
Max sum is 330
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)更多细节，请参考完整的文章[只允许给定数组旋转的情况下求 Sum( i*arr[i])的最大值](https://www.geeksforgeeks.org/find-maximum-value-of-sum-iarri-with-only-rotations-on-given-array-allowed/)！

=i<=n-1>
```