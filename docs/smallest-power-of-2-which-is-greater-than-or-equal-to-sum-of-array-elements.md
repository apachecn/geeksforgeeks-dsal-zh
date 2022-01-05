# 大于或等于数组元素之和的 2 的最小幂

> 原文:[https://www . geesforgeks . org/2 的最小二乘方大于或等于数组元素的和/](https://www.geeksforgeeks.org/smallest-power-of-2-which-is-greater-than-or-equal-to-sum-of-array-elements/)

给定一个由 N 个数字组成的数组，其中数组的值代表内存大小。系统所需的内存只能用 2 的幂来表示。任务是返回系统所需的内存大小。
**例:**

```
Input: a[] = {2, 1, 4, 5}
Output: 16
The sum of memory required is 12, 
hence the nearest power of 2 is 16\. 

Input: a[] = {1, 2, 3, 2}
Output: 8
```

**来源:** [微软采访](https://www.geeksforgeeks.org/microsoft-interview-experience-set-133-campus-internship/)

**方法:**问题是数组元素的[求和与](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)[大于等于 N 的 2 的最小幂](https://www.geeksforgeeks.org/smallest-power-of-2-greater-than-or-equal-to-n/)的组合。求数组元素的和，然后求大于等于 n 的 2 的最小幂
下面是上面方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the nearest power of 2
int nextPowerOf2(int n)
{

    // The number
    int p = 1;

    // If already a power of 2
    if (n && !(n & (n - 1)))
        return n;

    // Find the next power of 2
    while (p < n)
        p <<= 1;

    return p;
}

// Function to find the memory used
int memoryUsed(int arr[], int n)
{
    // Sum of array
    int sum = 0;

    // Traverse and find the sum of array
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // Function call to find the nearest power of 2
    int nearest = nextPowerOf2(sum);

    return nearest;
}
// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << memoryUsed(arr, n);

    // getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{
    // Function to find the nearest power of 2
    static int nextPowerOf2(int n)
    {

        // The number
        int p = 1;

        // If already a power of 2
        if(n!=0 && ((n&(n-1)) == 0))
            return n;

        // Find the next power of 2
        while (p < n)
            p <<= 1;

        return p;
    }

    // Function to find the memory used
    static int memoryUsed(int arr[], int n)
    {
        // Sum of array
        int sum = 0;

        // Traverse and find the sum of array
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // Function call to find the nearest power of 2
        int nearest = nextPowerOf2(sum);

        return nearest;
    }
    // Driver Code
    public static void main(String []args)
    {
        int arr[] = { 1, 2, 3, 2 };
        int n = arr.length;

        System.out.println(memoryUsed(arr, n));

    }
}

// This code is contributed
// by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the nearest power of 2
def nextPowerOf2(n):

    # The number
    p = 1

    # If already a power of 2
    if (n and not(n & (n - 1))):
        return n

    # Find the next power of 2
    while (p < n):
        p <<= 1
    return p

# Function to find the memory used
def memoryUsed(arr, n):

    # Sum of array
    sum = 0

    # Traverse and find the sum of array
    for i in range(n):
        sum += arr[i]

    # Function call to find the nearest
    # power of 2
    nearest = nextPowerOf2(sum)

    return nearest

# Driver Code
arr = [1, 2, 3, 2]
n = len(arr)
print(memoryUsed(arr, n))

# This code is contributed by sahishelangia
```

## C#

```
// C# implementation of the above approach

using System;
class GFG
{
    // Function to find the nearest power of 2
    static int nextPowerOf2(int n)
    {

        // The number
        int p = 1;

        // If already a power of 2
        if(n!=0 && ((n&(n-1)) == 0))
            return n;

        // Find the next power of 2
        while (p < n)
            p <<= 1;

        return p;
    }

    // Function to find the memory used
    static int memoryUsed(int []arr, int n)
    {
        // Sum of array
        int sum = 0;

        // Traverse and find the sum of array
        for (int i = 0; i < n; i++)
            sum += arr[i];

        // Function call to find the nearest power of 2
        int nearest = nextPowerOf2(sum);

        return nearest;
    }
    // Driver Code
    public static void Main()
    {
        int []arr = { 1, 2, 3, 2 };
        int n = arr.Length;

        Console.WriteLine(memoryUsed(arr, n));

    }
}

// This code is contributed
// by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to find the nearest power of 2
function nextPowerOf2($n)
{

    // The number
    $p = 1;

    // If already a power of 2
    if ($n && !($n & ($n - 1)))
        return $n;

    // Find the next power of 2
    while ($p < $n)
        $p <<= 1;

    return $p;
}

// Function to find the memory used
function memoryUsed(&$arr, $n)
{
    // Sum of array
    $sum = 0;

    // Traverse and find the sum of array
    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    // Function call to find the
    // nearest power of 2
    $nearest = nextPowerOf2($sum);

    return $nearest;
}

// Driver Code
$arr = array(1, 2, 3, 2);
$n = sizeof($arr);

echo(memoryUsed($arr, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to find the nearest power of 2
function nextPowerOf2(n)
{

    // The number
    let p = 1;

    // If already a power of 2
    if (n && !(n & (n - 1)))
        return n;

    // Find the next power of 2
    while (p < n)
        p <<= 1;

    return p;
}

// Function to find the memory used
function memoryUsed(arr, n)
{
    // Sum of array
    let sum = 0;

    // Traverse and find the sum of array
    for (let i = 0; i < n; i++)
        sum += arr[i];

    // Function call to find the nearest power of 2
    let nearest = nextPowerOf2(sum);

    return nearest;
}
// Driver Code
let arr = [ 1, 2, 3, 2 ];
let n = arr.length;

document.write(memoryUsed(arr, n));

</script>
```

**Output:** 

```
8
```