# 选择 n 个元素，使其平均值最大

> 原文:[https://www . geesforgeks . org/choose-n-elements-so-它们的平均值是最大值/](https://www.geeksforgeeks.org/choose-n-elements-such-that-their-mean-is-maximum/)

给定一个由 **2 * n 个**元素组成的数组，任务是构造并打印一个由 **n 个**元素组成的数组，使得新数组的[均值](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)最大。这里 **n 是偶数**。

**示例:**

> **输入:** arr[] = {3，1，2，3，8，6}
> **输出:**3 6 8
> T6】输入: arr[] = {3，2，3，8}
> **输出:** 3 8

**方法:**数组的平均值是同一数组元素的平均值，即 **(∑arr[i]) / n** 。因此，为了使数组的平均值最大，从数组中选择最大的 **n** 元素，这可以通过首先对数组进行排序，然后从最大值开始选择元素来实现。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the contents
// of an array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to print the array with
// maximum mean
void printMaxMean(int arr[], int n)
{
    int newArr[n];

    // Sort the original array
    sort(arr, arr + 2 * n);

    // Construct new array
    for (int i = 0; i < n; i++)
        newArr[i] = arr[i + n];

    // Print the resultant array
    printArray(newArr, n);
}

// Driver code
int main()
{
    int arr[] = { 4, 8, 3, 1, 3, 7, 0, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printMaxMean(arr, n / 2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GfG{

    // Utility function to print the 
    // contents of an array
    static void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Function to print the array 
    // with maximum mean
    static void printMaxMean(int arr[], int n)
    {
        int newArr[] = new int[n];

        // Sort the original array
        Arrays.sort(arr, 0, 2 * n);

        // Construct new array
        for (int i = 0; i < n; i++)
            newArr[i] = arr[i + n];

        // Print the resultant array
        printArray(newArr, n);
    }

    // Driver code
    public static void main(String []args)
    {
        int arr[] = { 4, 8, 3, 1, 3, 7, 0, 4 };
        int n = arr.length;
        printMaxMean(arr, n / 2);
    }
}

// This code is contributed by
// Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to print the contents
# of an array
def printArray(arr, n) :
    for i in range(n) :
        print(arr[i], end = " ")

# Function to print the array with
# maximum mean
def printMaxMean(arr, n) :
    newArr = [0] * n

    # Sort the original array
    arr.sort()

    # Construct new array
    for i in range(n) :
        newArr[i] = arr[i + n]

    # Print the resultant array
    printArray(newArr, n)

# Driver code
if __name__ == "__main__" :

    arr = [ 4, 8, 3, 1, 3, 7, 0, 4 ]
    n = len(arr)
    printMaxMean(arr, n // 2)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Utility function to print the
    // contents of an array
    static void printArray(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Function to print the array
    // with maximum mean
    static void printMaxMean(int[] arr, int n)
    {
        int[] newArr = new int[n];

        // Sort the original array
        Array.Sort(arr, 0, 2 * n);

        // Construct new array
        for (int i = 0; i < n; i++)
            newArr[i] = arr[i + n];

        // Print the resultant array
        printArray(newArr, n);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 4, 8, 3, 1, 3, 7, 0, 4 };
        int n = arr.Length;
        printMaxMean(arr, n / 2);
    }
}

// This code is contributed by Ita_c.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Utility function to print the contents
// of an array
function printArray($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i] . " ";
}

// Function to print the array with
// maximum mean
function printMaxMean($arr, $n)
{
    $newArr[$n] = array();

    // Sort the original array
    sort($arr,0);

    // Construct new array
    for ($i = 0; $i < $n; $i++)
        $newArr[$i] = $arr[$i + $n];

    // Print the resultant array
    printArray($newArr, $n);
}

// Driver code
$arr = array(4, 8, 3, 1, 3, 7, 0, 4);
$n = sizeof($arr);
printMaxMean($arr, $n / 2);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Utility function to print the
    // contents of an array
    function printArray(arr , n) {
        for (i = 0; i < n; i++)
            document.write(arr[i] + " ");
    }

    // Function to print the array
    // with maximum mean
    function printMaxMean(arr , n) {
        var newArr = Array(n).fill(0);

        // Sort the original array
        arr.sort((a,b)=>a-b);

        // Construct new array
        for (i = 0; i < n; i++)
            newArr[i] = arr[i + n];

        // Print the resultant array
        printArray(newArr, n);
    }

    // Driver code

        var arr = [ 4, 8, 3, 1, 3, 7, 0, 4 ];
        var n = arr.length;
        printMaxMean(arr, n / 2);

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
4 4 7 8
```