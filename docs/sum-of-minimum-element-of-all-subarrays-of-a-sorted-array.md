# 排序数组中所有子数组的最小元素之和

> 原文:[https://www . geeksforgeeks . org/排序数组的所有子数组的最小元素之和/](https://www.geeksforgeeks.org/sum-of-minimum-element-of-all-subarrays-of-a-sorted-array/)

给定一个排序数组**一个由 **n** 个整数组成的**。任务是求 **A** 所有可能子阵的最小值之和。

**示例:**

> **输入:** A = [ 1，2，4，5]
> **输出:** 23
> 子序列为[ 1]，[2]，[4]，[5]，[1，2]，[2，4]，[4，5] [1，2，4]，[2，4，5]，[1，2，4，5]
> 最小值为 1，2，4，5，1，2，4，1，2，1。
> 和为 23
> **输入:**A =【1，2，3】
> **输出:** 10

**方法:**天真的方法是生成所有可能的子阵列，找到它们的最小值，并将其添加到结果中。
**高效做法:**给定数组排序，那么观察最小元素出现 N 次，第二个最小出现 N-1 次，以此类推……举个例子:

> arr[] = {1，2，3}
> 子阵列是{1}、{2}、{3}、{1，2}、{2，3}、{1，2，3}
> 每个子阵列的最小值:{1}、{2}、{3}、{1}、{2}、{1}。
> 其中
> 1 出现 3 次，即 n = 3 时出现 n 次。
> 2 发生 2 次，即 n = 3 时 n-1 次。
> 3 发生 1 次，即 n = 3 时 n-2 次。

因此，遍历数组，将当前元素(即 arr[i]* n-i)加到和中。
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum
// of minimum of all subarrays
int findMinSum(int arr[], int n)
{

    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i] * (n - i);

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 3, 5, 7, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findMinSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GfG
{

// Function to find the sum
// of minimum of all subarrays
static int findMinSum(int arr[], int n)
{

    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i] * (n - i);

    return sum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 5, 7, 8 };
    int n = arr.length;

    System.out.println(findMinSum(arr, n));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to find the sum
# of minimum of all subarrays
def findMinSum(arr, n):
    sum = 0
    for i in range(0, n):
        sum += arr[i] * (n - i)
    return sum

# Driver code
arr = [3, 5, 7, 8 ]
n = len(arr)

print(findMinSum(arr, n))

# This code has been contributed
# by 29AjayKumar
```

## C#

```
// C# implementation of the above approach
using System;

class GfG
{

// Function to find the sum
// of minimum of all subarrays
static int findMinSum(int []arr, int n)
{

    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i] * (n - i);

    return sum;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 3, 5, 7, 8 };
    int n = arr.Length;

    Console.WriteLine(findMinSum(arr, n));
}
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// PHP implementation of the above approach
// Function to find the sum
// of minimum of all subarrays
function findMinSum($arr,$n)
{

    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i] * ($n - $i);

    return $sum;
}

// Driver code
$arr = array( 3, 5, 7, 8 );
$n = count($arr);

echo findMinSum($arr, $n);

// This code is contributed by Arnab Kundu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the sum
// of minimum of all subarrays
function findMinSum(arr, n)
{

    var sum = 0;
    for (var i = 0; i < n; i++)
        sum += arr[i] * (n - i);

    return sum;
}

// Driver code
var arr = [ 3, 5, 7, 8 ];
var n = arr.length;
document.write( findMinSum(arr, n));

</script>
```

**Output:** 

```
49
```

**注意:**要求排序数组中所有子数组最大元素的**和，只需反向遍历数组，并应用相同的求和公式即可。**