# 排序数组所有子序列的最小元素之和

> 原文:[https://www . geeksforgeeks . org/排序数组的所有子序列的最小元素之和/](https://www.geeksforgeeks.org/sum-of-minimum-element-of-all-sub-sequences-of-a-sorted-array/)

给定一个排序数组**一个 **n** 整数的**。任务是找到 **A** 所有可能子序列的最小值之和。
**注意:**考虑到不会有数字溢出。

**示例:**

> **输入:** A = [1，2，4，5]
> **输出:** 29
> 子序列为[1]，[2]，[4]，[5]，[1，2]，[1，4]，[1，5]，[2，4]，[2，5]，[4，5] [1，2，4]，[1，2，5]，[1，4，5]，[2，4，5]，[1，2，4，4，5]
> 和为 29
> **输入:**A =【1，2，3】
> **输出:** 11

**方法:**天真的方法是生成所有可能的子序列，找到它们的最小值，并将其添加到结果中。
**高效进场:**给定数组排序，观察最小元素出现 2 <sup>n-1</sup> 次，第二个最小元素出现 2 <sup>n-2</sup> 次，以此类推……举个例子:

> arr[] = {1，2，3}
> 子序列是{1}、{2}、{3}、{1，2}、{1，3}、{2，3}、{1，2，3}
> 每个子序列的最小值:{1}、{2}、{3}、{1}、{1}、{2}、{1}。
> 其中
> 1 出现 4 次，即 2 <sup>n-1</sup> 其中 n = 3。
> 2 出现 2 次，即 2 <sup>n-2</sup> ，其中 n = 3。
> 3 出现 1 次，即 2 <sup>n-3</sup> ，其中 n = 3。

因此，遍历数组，将当前元素，即 arr[I]* power(2，n-1-i)加到和中。
以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum
// of minimum of all subsequence
int findMinSum(int arr[], int n)
{

    int occ = n - 1, sum = 0;
    for (int i = 0; i < n; i++) {
        sum += arr[i] * pow(2, occ);
        occ--;
    }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4, 5 };
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
// of minimum of all subsequence
static int findMinSum(int arr[], int n)
{

    int occ = n - 1, sum = 0;
    for (int i = 0; i < n; i++)
    {
        sum += arr[i] * (int)Math.pow(2, occ);
        occ--;
    }

    return sum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 4, 5 };
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
# of minimum of all subsequence
def findMinSum(arr, n):

    occ = n - 1
    Sum = 0
    for i in range(n):
        Sum += arr[i] * pow(2, occ)
        occ -= 1

    return Sum

# Driver code
arr = [1, 2, 4, 5]
n = len(arr)

print(findMinSum(arr, n))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to find the sum
// of minimum of all subsequence
static int findMinSum(int []arr, int n)
{

    int occ = n - 1, sum = 0;
    for (int i = 0; i < n; i++)
    {
        sum += arr[i] *(int) Math.Pow(2, occ);
        occ--;
    }

    return sum;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 2, 4, 5 };
    int n = arr.Length;

    Console.WriteLine( findMinSum(arr, n));
}
}
// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Function to find the sum
// of minimum of all subsequence
function findMinSum($arr, $n)
{
    $occ1 = ($n);
    $occ = $occ1 - 1;
    $Sum = 0;
    for ($i = 0; $i < $n; $i++)
    {
        $Sum += $arr[$i] * pow(2, $occ);
        $occ -= 1;
    }
    return $Sum;
}

// Driver code
$arr = array(1, 2, 4, 5);
$n = count($arr);

echo findMinSum($arr, $n);

// This code is contributed
// by Srathore
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the sum
// of minimum of all subsequence
function findMinSum(arr, n)
{

    var occ = n - 1, sum = 0;
    for (var i = 0; i < n; i++) {
        sum += arr[i] * Math.pow(2, occ);
        occ--;
    }

    return sum;
}

// Driver code
var arr = [ 1, 2, 4, 5 ];
var n = arr.length;
document.write( findMinSum(arr, n));

</script>
```

**Output:** 

```
29
```

**注意:**要找到排序数组中所有子序列的 **最大元素的**和，只需按相反的顺序遍历数组，并对和应用相同的公式。****