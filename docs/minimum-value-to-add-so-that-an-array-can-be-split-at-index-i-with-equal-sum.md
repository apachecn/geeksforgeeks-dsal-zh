# 加到 arr[i]上的最小值，这样一个数组就可以在索引 I 处以相等的和进行拆分

> 原文:[https://www . geeksforgeeks . org/最小值相加，这样数组就可以在索引 I 处以相等的总和进行拆分/](https://www.geeksforgeeks.org/minimum-value-to-add-so-that-an-array-can-be-split-at-index-i-with-equal-sum/)

给定整数数组 **arr[]** ，任务是找到最小非负整数 **k** ，使得在给定数组中存在索引 **j** ，使得当 **arr[j]** 被更新为 **arr[j] + k** 时，从索引 **arr[0]** 到 **arr[j]** 的数组元素之和等于从 **arr 的元素之和**

> arr[0]+arr[1]+…+arr[j]= arr[j+1]+arr[j+2]+…+arr[n–1]

。
如果不存在这样的 **k** ，则打印 **-1** 。
**例:**

> **输入:** arr[] = {6，7，1，3，8，2，4}
> **输出:** 3
> 如果将 3 加到 1，则从索引 0 到 2 和 3 到 6 的元素总和将等于 17。
> **输入:** arr[] = {7，3}
> **输出:** -1

一种简单的方法是运行两个循环。对于每个元素，找出左边和右边元素总和之间的差异。最后，返回两个和之间的最小差。
一种**有效方法:**是首先计算前缀和并存储在数组 **pre[]** 中，其中 **pre[i]** 存储从 **arr[0]** 到 **arr[i]** 的数组元素的和。对于每个索引，如果留给它的元素之和(包括元素本身，即 pre[i])小于或等于右元素之和(pre[n–1]–pre[I])，则将 **k** 的值更新为 **min(k，(pre[n–1]–pre[I])–pre[I])**
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum value k to be added
int FindMinNum(int arr[], int n)
{

    // Array to store prefix sum
    int pre[n];

    // Initialize the prefix value for first index
    // as the first element of the array
    pre[0] = arr[0];

    // Compute the prefix sum for rest of the indices
    for (int i = 1; i < n; i++)
        pre[i] = pre[i - 1] + arr[i];

    int k = INT_MAX;

    for (int i = 0; i < n - 1; i++) {

        // Sum of elements from arr[i + 1] to arr[n - 1]
        int rightSum = pre[n - 1] - pre[i];

        // If sum on the right side of the ith element
        // is greater than or equal to the sum on the
        // left side then update the value of k
        if (rightSum >= pre[i])
            k = min(k, rightSum - pre[i]);
    }

    if (k != INT_MAX)
        return k;

    return -1;
}

// Driver code
int main()
{
    int arr[] = { 6, 7, 1, 3, 8, 2, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << FindMinNum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GfG
{

// Function to return the minimum value k to be added
static int FindMinNum(int arr[], int n)
{

    // Array to store prefix sum
    int pre[] = new int[n];

    // Initialize the prefix value for first index
    // as the first element of the array
    pre[0] = arr[0];

    // Compute the prefix sum for rest of the indices
    for (int i = 1; i < n; i++)
        pre[i] = pre[i - 1] + arr[i];

    int k = Integer.MAX_VALUE;

    for (int i = 0; i < n - 1; i++)
    {

        // Sum of elements from arr[i + 1] to arr[n - 1]
        int rightSum = pre[n - 1] - pre[i];

        // If sum on the right side of the ith element
        // is greater than or equal to the sum on the
        // left side then update the value of k
        if (rightSum >= pre[i])
            k = Math.min(k, rightSum - pre[i]);
    }

    if (k != Integer.MAX_VALUE)
        return k;

    return -1;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 6, 7, 1, 3, 8, 2, 4 };
    int n = arr.length;
    System.out.println(FindMinNum(arr, n));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
import sys

# Function to return the minimum
# value k to be added
def FindMinNum(arr, n):

    # Array to store prefix sum
    pre = [0 for i in range(n)]

    # Initialize the prefix value for first
    # index as the first element of the array
    pre[0] = arr[0]

    # Compute the prefix sum for rest
    # of the indices
    for i in range(1, n, 1):
        pre[i] = pre[i - 1] + arr[i]

    k = sys.maxsize

    for i in range(n - 1):

        # Sum of elements from arr[i + 1] to arr[n - 1]
        rightSum = pre[n - 1] - pre[i]

        # If sum on the right side of the ith element
        # is greater than or equal to the sum on the
        # left side then update the value of k
        if (rightSum >= pre[i]):
            k = min(k, rightSum - pre[i])

    if (k != sys.maxsize):
        return k

    return -1

# Driver code
if __name__ == '__main__':
    arr = [6, 7, 1, 3, 8, 2, 4]
    n = len(arr)
    print(FindMinNum(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Function to return the minimum value k to be added
    static int FindMinNum(int []arr, int n)
    {

        // Array to store prefix sum
        int []pre = new int[n];

        // Initialize the prefix value for first index
        // as the first element of the array
        pre[0] = arr[0];

        // Compute the prefix sum for rest of the indices
        for (int i = 1; i < n; i++)
            pre[i] = pre[i - 1] + arr[i];

        int k = int.MaxValue;

        for (int i = 0; i < n - 1; i++)
        {

            // Sum of elements from arr[i + 1] to arr[n - 1]
            int rightSum = pre[n - 1] - pre[i];

            // If sum on the right side of the ith element
            // is greater than or equal to the sum on the
            // left side then update the value of k
            if (rightSum >= pre[i])
                k = Math.Min(k, rightSum - pre[i]);
        }

        if (k != int.MaxValue)
            return k;

        return -1;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 6, 7, 1, 3, 8, 2, 4 };
        int n = arr.Length;

        Console.WriteLine(FindMinNum(arr, n));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// value k to be added
function FindMinNum($arr, $n)
{

    // Array to store prefix sum
    $pre = array();

    // Initialize the prefix value for first index
    // as the first element of the array
    $pre[0] = $arr[0];

    // Compute the prefix sum for
    // rest of the indices
    for ($i = 1; $i < $n; $i++)
        $pre[$i] = $pre[$i - 1] + $arr[$i];

    $k = PHP_INT_MAX;

    for ($i = 0; $i < $n - 1; $i++)
    {

        // Sum of elements from arr[i + 1] to arr[n - 1]
        $rightSum = $pre[$n - 1] - $pre[$i];

        // If sum on the right side of the ith element
        // is greater than or equal to the sum on the
        // left side then update the value of k
        if ($rightSum >= $pre[$i])
            $k = min($k, $rightSum - $pre[$i]);
    }

    if ($k != PHP_INT_MAX)
        return $k;

    return -1;
}

// Driver code
$arr = array(6, 7, 1, 3, 8, 2, 4);
$n = sizeof($arr);
echo FindMinNum($arr, $n);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
//Javascript Implementation

// Function to return the minimum value k to be added
function FindMinNum(arr, n)
{

    // Array to store prefix sum
    var pre = new Array(n);

    // Initialize the prefix value for first index
    // as the first element of the array
    pre[0] = arr[0];

    // Compute the prefix sum for rest of the indices
    for (var i = 1; i < n; i++)
        pre[i] = pre[i - 1] + arr[i];

    var k = Number.MAX_VALUE;

    for (var i = 0; i < n - 1; i++) {

        // Sum of elements from arr[i + 1] to arr[n - 1]
        var rightSum = pre[n - 1] - pre[i];

        // If sum on the right side of the ith element
        // is greater than or equal to the sum on the
        // left side then update the value of k
        if (rightSum >= pre[i])
            k = Math.min(k, rightSum - pre[i]);
    }

    if (k != Number.MAX_VALUE)
        return k;

    return -1;
}

/* Driver code*/
var arr = [6, 7, 1, 3, 8, 2, 4];
var n = arr.length;
document.write(FindMinNum(arr, n))
// This code is contributed by shubhamsingh10
</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(n)
T3】辅助空间:O(n)
T6】进一步优化:我们可以利用下面的步骤避免使用额外的空间。
1)计算所有元素的总和。
2)不断加左和右和可以从总和中减去左和得到。
思路类似于[均衡指标问题](https://www.geeksforgeeks.org/equilibrium-index-of-an-array/)的优化解。
**时间复杂度:** O(n)
**辅助空间:** O(1)