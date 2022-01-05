# 要插入的具有相等和的最小整数

> 原文:[https://www . geeksforgeeks . org/最小待插入整数等于和/](https://www.geeksforgeeks.org/smallest-integer-to-be-inserted-to-have-equal-sums/)

给定一个正整数数组，找到最小的非负整数(即大于或等于零)，该整数可以放在数组的任意两个元素之间，这样子数组中出现在它之前的元素之和等于它之后的子数组中出现的元素之和，新放置的整数包含在两个子数组中的任何一个中。
**例:**

> **输入** : arr = {3，2，1，5，7，8}
> **输出** : 4
> **解释**:我们可以插入的最小可能数是 4，在位置 5(即 5 和 7 之间)作为第一个子阵列的一部分，这样两个子阵列的和就等于，3+2+1+5+4=15 和 7+8=15。
> **输入** : arr = {3，2，2，3}
> **输出** : 0
> **说明**:前两个元素和后两个元素作为单独的子阵相加，不插入任何多余的数，得到 5 的等份和。因此，要插入的最小整数在位置 3 是 0。

为了以这样的方式分割阵列，即它给出两个子阵列，它们各自元素的和相等，一种非常简单和直接的方法是从阵列的开始处开始一个接一个地添加元素，并找到它们的和与其余元素的和之间的差异。我们使用迭代循环来实现这一点。对于数组索引 0 到 N-1，我们不断从左到右添加元素，并找到它与剩余总和的差异。在第一次迭代中，所获得的差异被认为是最小的，以便进行进一步的比较。对于剩余的迭代，如果获得的差值小于前面考虑的最小值，我们就更新最小值。直到循环结束，我们终于得到了可以相加的最小数。
以下是上述方法的实现:

## C++

```
// C++ program to find the smallest
// number to be added to make the
// sum of left and right subarrays equal
#include<bits/stdc++.h>
using namespace std;

// Function to find the minimum
// value to be added
int findMinEqualSums(int a[], int N)
{
    // Variable to store entire
    // array sum
    int sum = 0;
    for (int i = 0; i < N; i++)
    {
        sum += a[i];
    }

    // Variables to store sum of
    // subarray1 and subarray 2
    int sum1 = 0, sum2 = 0;

    // minimum value to be added
    int min = INT_MAX;

    // Traverse through the array
    for (int i = 0; i < N; i++)
    {
        // Sum of both halves
        sum1 += a[i];
        sum2 = sum - sum1;

        // Calculate minimum number
        // to be added
        if (abs(sum1 - sum2) < min)
        {
            min = abs(sum1 - sum2);
        }

        if (min == 0)
        {
            break;
        }
    }

    return min;
}

// Driver code
int main()
{
    int a[] = { 3, 2, 1, 5, 7, 8 };

    // Length of array
    int N = sizeof(a) / sizeof(a[0]);

    cout << (findMinEqualSums(a, N));
}

// This code is contributed
// by ChitraNayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest
// number to be added to make the
// sum of left and right subarrays equal
import java.io.*;
import java.util.*;

class GFG
{

// Function to find the minimum
// value to be added
static int findMinEqualSums(int[] a, int N)
{
    // Variable to store
    // entire array sum
    int sum = 0;
    for (int i = 0; i < N; i++)
    {
        sum += a[i];
    }

    // Variables to store sum of
    // subarray1 and subarray 2
    int sum1 = 0, sum2 = 0;

    // minimum value to be added
    int min = Integer.MAX_VALUE;

    // Traverse through the array
    for (int i = 0; i < N; i++)
    {
        // Sum of both halves
        sum1 += a[i];
        sum2 = sum - sum1;

        // Calculate minimum number
        // to be added
        if (Math.abs(sum1 - sum2) < min)
        {
            min = Math.abs(sum1 - sum2);
        }

        if (min == 0)
        {
            break;
        }
    }

    return min;
}

// Driver code
public static void main(String args[])
{
    int[] a = { 3, 2, 1, 5, 7, 8 };

    // Length of array
    int N = a.length;

    System.out.println(findMinEqualSums(a, N));
}
}
```

## 蟒蛇 3

```
import sys
# Python3 program to find the smallest
# number to be added to make the
# sum of left and right subarrays equal

# Function to find the minimum
# value to be added
def findMinEqualSums(a, N):

    # Variable to store entire
    # array sum
    sum = 0
    for i in range(0,N):

        sum = sum+a[i]

    # Variables to store sum of
    # subarray1 and subarray 2
    sum1 = 0
    sum2 = 0

    # minimum value to be added
    min = sys.maxsize

    # Traverse through the array
    for i in range(0, N-1):

        # Sum of both halves
        sum1 += a[i]
        sum2 = sum - sum1

        # Calculate minimum number
        # to be added
        if (abs(sum1 - sum2) < min):
            min = abs(sum1 - sum2)

        if (min == 0) :

            break
    return min

# Driver code
if __name__=='__main__':
    a = [3, 2, 1, 5, 7, 8]

    # Length of array
    N = len(a)

    print(findMinEqualSums(a, N))

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# program to find the smallest
// number to be added to make the
// sum of left and right subarrays equal
using System;
class GFG
{

// Function to find the minimum
// value to be added
static int findMinEqualSums(int[] a, int N)
{
    // Variable to store
    // entire array sum
    int sum = 0;
    for (int i = 0; i < N; i++)
    {
        sum += a[i];
    }

    // Variables to store sum of
    // subarray1 and subarray 2
    int sum1 = 0, sum2 = 0;

    // minimum value to be added
    int min = int.MaxValue;

    // Traverse through the array
    for (int i = 0; i < N; i++)
    {
        // Sum of both halves
        sum1 += a[i];
        sum2 = sum - sum1;

        // Calculate minimum number
        // to be added
        if (Math.Abs(sum1 - sum2) < min)
        {
            min = Math.Abs(sum1 - sum2);
        }

        if (min == 0)
        {
            break;
        }
    }

    return min;
}

// Driver code
public static void Main()
{
    int[] a = { 3, 2, 1, 5, 7, 8 };

    // Length of array
    int N = a.Length;

    Console.WriteLine(findMinEqualSums(a, N));
}
}
// This code is contributed by shs
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the smallest
// number to be added to make the
// sum of left and right subarrays equal

// Function to find the minimum
// value to be added
function findMinEqualSums($a, $N)
{
    // Variable to store entire
    // array sum
    $sum = 0;
    for ($i = 0; $i < $N; $i++)
    {
        $sum += $a[$i];
    }

    // Variables to store sum of
    // subarray1 and subarray 2
    $sum1 = 0; $sum2 = 0;

    // minimum value to be added
    $min = PHP_INT_MAX;

    // Traverse through the array
    for ($i = 0; $i < $N; $i++)
    {
        // Sum of both halves
        $sum1 += $a[$i];
        $sum2 = $sum - $sum1;

        // Calculate minimum number
        // to be added
        if (abs($sum1 - $sum2) < $min)
        {
            $min = abs($sum1 - $sum2);
        }

        if ($min == 0)
        {
            break;
        }
    }

    return $min;
}

// Driver code
$a = array( 3, 2, 1, 5, 7, 8 );

// Length of array
$N = count($a);

echo (findMinEqualSums($a, $N));

// This code is contributed
// shs
?>
```

## java 描述语言

```
<script>
// Javascript program to find the smallest
// number to be added to make the
// sum of left and right subarrays equal

// Function to find the minimum
// value to be added
function findMinEqualSums(a,N)
{
    // Variable to store
    // entire array sum
    let sum = 0;
    for (let i = 0; i < N; i++)
    {
        sum += a[i];
    }

    // Variables to store sum of
    // subarray1 and subarray 2
    let sum1 = 0, sum2 = 0;

    // minimum value to be added
    let min = Number.MAX_VALUE;

    // Traverse through the array
    for (let i = 0; i < N; i++)
    {
        // Sum of both halves
        sum1 += a[i];
        sum2 = sum - sum1;

        // Calculate minimum number
        // to be added
        if (Math.abs(sum1 - sum2) < min)
        {
            min = Math.abs(sum1 - sum2);
        }

        if (min == 0)
        {
            break;
        }
    }

    return min;
}

// Driver code
let a=[3, 2, 1, 5, 7, 8];
// Length of array
let N = a.length;
document.write(findMinEqualSums(a, N));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
4
```