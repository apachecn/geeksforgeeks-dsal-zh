# 检查数组是否可以分成两个子数组，使得它们的绝对差值为 K

> 原文:[https://www . geesforgeks . org/check-if-array-can-division-two-sub-array-so-它们的绝对差值是-k/](https://www.geeksforgeeks.org/check-if-array-can-be-divided-into-two-sub-arrays-such-that-their-absolute-difference-is-k/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是找出该数组是否可以分成两个子数组，使得两个子数组元素之和的绝对差为 **K** 。
**举例:**

> **输入:** arr[] = {2，4，5，1}，K = 0
> **输出:**是
> {2，4}和{5，1}是两个可能的子数组。
> |(2+4)–(5+1)| = | 6–6 | = 0
> **输入:** arr[] = {2，4，1，5}，K = 2
> **输出:**否

**进场:**

*   假设存在一个答案，让子阵的元素之和(和较小)为 **S** 。
*   第二个数组的元素之和将是 **S + K** 。
*   并且， **S + S + K** 必须等于数组中所有元素的和比如 **totalSum = 2 *S + K** 。
*   **S =(total sum–K)/2**
*   现在，遍历数组，直到我们从第一个元素开始得到 **S** 的总和，如果不可能，则打印 **No** 。
*   否则打印**是**。

以下是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function that return true if it is possible
// to divide the array into sub-arrays
// that satisfy the given condition
bool solve(int array[], int size, int k)
{
    // To store the sum of all the elements
    // of the array
    int totalSum = 0;
    for (int i = 0; i < size; i++)
        totalSum += array[i];

    // Sum of any sub-array cannot be
    // a floating point value
    if ((totalSum - k) % 2 == 1)
        return false;

    // Required sub-array sum
    int S = (totalSum - k) / 2;

    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum += array[i];
        if (sum == S)
            return true;
    }

    return false;
}

// Driver Code
int main()
{
    int array[] = { 2, 4, 1, 5 };
    int k = 2;
    int size = sizeof(array) / sizeof(array[0]);
    if (solve(array, size, k))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG
{

// Function that return true if it is possible
// to divide the array into sub-arrays
// that satisfy the given condition
static boolean solve(int array[], int size, int k)
{
    // To store the sum of all the elements
    // of the array
    int totalSum = 0;
    for (int i = 0; i < size; i++)
        totalSum += array[i];

    // Sum of any sub-array cannot be
    // a floating point value
    if ((totalSum - k) % 2 == 1)
        return false;

    // Required sub-array sum
    int S = (totalSum - k) / 2;

    int sum = 0;
    for (int i = 0; i < size; i++)
    {
        sum += array[i];
        if (sum == S)
            return true;
    }
    return false;
}

    // Driver Code
    public static void main (String[] args)
    {
        int array[] = { 2, 4, 1, 5 };
        int k = 2;
        int size = array.length;

        if (solve(array, size, k))
            System.out.println ("Yes");
        else
            System.out.println ("No" );
    }
}

// This Code is contributed by akt_mit
```

## 蟒蛇 3

```
# Function that return true if it is possible
# to divide the array into sub-arrays
# that satisfy the given condition
def solve(array,size,k):
    # To store the sum of all the elements
    # of the array
    totalSum = 0
    for i in range (0,size):
        totalSum += array[i]

    # Sum of any sub-array cannot be
    # a floating point value
    if ((totalSum - k) % 2 == 1):
        return False

    # Required sub-array sum
    S = (totalSum - k) / 2

    sum = 0;
    for i in range (0,size):
        sum += array[i]
        if (sum == S):
            return True

    return False

# Driver Code
array= [2, 4, 1, 5]
k = 2
n = 4
if (solve(array, n, k)):
    print("Yes")
else:
    print("No")

# This code is contributed by iAyushRaj.
```

## C#

```
using System;
class GFG
{

// Function that return true if it is possible
// to divide the array into sub-arrays
// that satisfy the given condition
public static bool solve(int[] array, int size, int k)
{
    // To store the sum of all the elements
    // of the array
    int totalSum = 0;
    for (int i = 0; i < size; i++)
        totalSum += array[i];

    // Sum of any sub-array cannot be
    // a floating point value
    if ((totalSum - k) % 2 == 1)
        return false;

    // Required sub-array sum
    int S = (totalSum - k) / 2;

    int sum = 0;
    for (int i = 0; i < size; i++)
    {
        sum += array[i];
        if (sum == S)
            return true;
    }

    return false;
}

// Driver Code
public static void Main()
{
    int[] array = { 2, 4, 1, 5 };
    int k = 2;
    int size = 4;

    if (solve(array, size, k))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by iAyushRaj.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function that return true if it is possible
// to divide the array into sub-arrays
// that satisfy the given condition
function solve($array, $size,$k)
{
    // To store the sum of all the elements
    // of the array
    $totalSum = 0;
    for ($i = 0; $i < $size; $i++)
        $totalSum += $array[$i];

    // Sum of any sub-array cannot be
    // a floating point value
    if (($totalSum - $k) % 2 == 1)
        return false;

    // Required sub-array sum
    $S = ($totalSum - $k) / 2;

    $sum = 0;
    for ($i = 0; $i < $size; $i++)
    {
        $sum += $array[$i];
        if ($sum == $S)
            return true;
    }

    return false;
}

// Driver Code
$array = array( 2, 4, 1, 5 );
$k = 2;
$size = sizeof($array);
if (solve($array, $size, $k))
    echo "Yes";
else
    echo "No";

// This code is contributed by iAyushRaj.
?>
```

## java 描述语言

```
<script>

// Javascript program to illustrate
// the above problem

// Function that return true if it is possible
// to divide the array into sub-arrays
// that satisfy the given condition
function solve(array, size, k)
{
    // To store the sum of all the elements
    // of the array
    let totalSum = 0;
    for (let i = 0; i < size; i++)
        totalSum += array[i];

    // Sum of any sub-array cannot be
    // a floating point value
    if ((totalSum - k) % 2 == 1)
        return false;

    // Required sub-array sum
    let S = (totalSum - k) / 2;

    let sum = 0;
    for (let i = 0; i < size; i++)
    {
        sum += array[i];
        if (sum == S)
            return true;
    }
    return false;
}

// Driver Code

        let array = [ 2, 4, 1, 5 ];
        let k = 2;
        let size = array.length;

        if (solve(array, size, k))
            document.write("Yes");
        else
            document.write ("No" );

</script>
```

**Output:** 

```
No
```