# 使数组和为奇数的最小移除次数

> 原文:[https://www . geesforgeks . org/minimum-removes-to-make-array-sum-odd/](https://www.geeksforgeeks.org/minimum-removals-to-make-array-sum-odd/)

给定一个由 N 个整数组成的数组 Arr[]。任务是找到需要从数组中移除的最小元素数量，以便剩余元素的总和为奇数。考虑到至少有一个奇数。

**示例:**

```
Input:  arr[] = {1, 2, 3, 4}
Output: 1
Remove 1 to make array sum odd.

Input: arr[] =  {4, 2, 3, 4}
Output: 0
Sum is already odd.
```

**方法:**解决这个问题的思路是先回忆一下 ODDs 和 EVENs 的以下性质:

*   奇数+奇数=偶数
*   奇数+偶数=奇数
*   偶数+偶数=偶数
*   奇数*偶数=偶数
*   偶数*偶数=偶数
*   奇数*奇数=奇数

因为任何偶数的和都是偶数。所以偶数的计数不重要。
奇数的奇数之和总是奇数。所以要使数组和为奇数，奇数的计数必须为奇数。
因此，计算奇数的数量，并检查计数是否为奇数，然后不需要移除。否则计数为偶数，则需要删除 1 个奇数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <iostream>
using namespace std;

// Function to find minimum removals
int findCount(int arr[], int n)
{
    // Count odd numbers
    int countOdd = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] % 2 == 1)
            countOdd++;

    // If the counter is odd return 0
    // otherwise return 1
    if (countOdd % 2 == 0)
        return 1;
    else
        return 0;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 5, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findCount(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GfG
{

// Function to find minimum removals
static int findCount(int arr[], int n)
{
    // Count odd numbers
    int countOdd = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] % 2 == 1)
            countOdd++;

    // If the counter is odd return 0
    // otherwise return 1
    if (countOdd % 2 == 0)
        return 1;
    else
        return 0;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 5, 1 };
    int n = arr.length;

    System.out.println(findCount(arr, n));
}
}

// This code is contributed by
// Prerna Saini
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to find minimum removals
def findCount(arr, n) :

    # Count odd numbers
    countOdd = 0;
    for i in range(n) :
        if (arr[i] % 2 == 1) :
            countOdd += 1;

    # If the counter is odd return 0
    # otherwise return 1
    if (countOdd % 2 == 0) :
        return 1;
    else :
        return 0;

# Driver Code
if __name__ == "__main__" :
    arr = [ 1, 2, 3, 5, 1 ];
    n = len(arr) ;

    print(findCount(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

// Function to find minimum removals
static int findCount(int []arr, int n)
{
    // Count odd numbers
    int countOdd = 0;
    for (int i = 0; i < n; i++)
        if (arr[i] % 2 == 1)
            countOdd++;

    // If the counter is odd return 0
    // otherwise return 1
    if (countOdd % 2 == 0)
        return 1;
    else
        return 0;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 5, 1 };
    int n = arr.Length;

    Console.WriteLine(findCount(arr, n));
}
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find minimum removals
function findCount($arr, $n)
{
    // Count odd numbers
    $countOdd = 0;
    for ($i = 0; $i < $n; $i++)
    if ($arr[$i] % 2 == 1)
        $countOdd++;

    // If the counter is odd return 0
    // otherwise return 1
    if ($countOdd % 2 == 0)
        return 1;
    else
        return 0;
}

// Driver Code
$arr = array(1, 2, 3, 5, 1);
$n = sizeof($arr);

echo(findCount($arr, $n));

// This code is contributed by
// Code_Mech.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find minimum removals
function findCount(arr, n)
{
    // Count odd numbers
    var countOdd = 0;
    for (var i = 0; i < n; i++)
        if (arr[i] % 2 == 1)
            countOdd++;

    // If the counter is odd return 0
    // otherwise return 1
    if (countOdd % 2 == 0)
        return 1;
    else
        return 0;
}

// Driver Code
var arr = [ 1, 2, 3, 5, 1 ];
var n = arr.length;
document.write( findCount(arr, n));

</script>
```

**Output:** 

```
1
```