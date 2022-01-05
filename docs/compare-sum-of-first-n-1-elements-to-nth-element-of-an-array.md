# 比较数组的第 N-1 个元素和第 N 个元素的和

> 原文:[https://www . geeksforgeeks . org/compare-first-n-1 元素之和与第 n 个数组元素之比/](https://www.geeksforgeeks.org/compare-sum-of-first-n-1-elements-to-nth-element-of-an-array/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是检查数组的第一个**N–1**元素的和是否等于最后一个元素。
**举例:**

> **输入:** arr[] = {1，2，3，4，10}
> **输出:**是
> **输入:** arr[] = {1，2，3，4，12}
> **输出:**否

**方法:**求数组中第一个**N–1**元素的和，即**arr[0]+arr[1]+…+arr[N–2]**并与**arr[N–1]**进行比较。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function that returns true if sum of
// first n-1 elements of the array is
// equal to the last element
bool isSumEqual(int ar[], int n)
{
    int sum = 0;

    // Find the sum of first n-1
    // elements of the array
    for (int i = 0; i < n - 1; i++)
        sum += ar[i];

    // If sum equals to the last element
    if (sum == ar[n - 1])
        return true;

    return false;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (isSumEqual(arr, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;

class GFG {

    // Function that returns true if sum of
    // first n-1 elements of the array is
    // equal to the last element
    static boolean isSumEqual(int ar[], int n)
    {
        int sum = 0;

        // Find the sum of first n-1
        // elements of the array
        for (int i = 0; i < n - 1; i++)
            sum += ar[i];

        // If sum equals to the last element
        if (sum == ar[n - 1])
            return true;

        return false;
    }

    // Driver code
    public static void main(String[] args)
    {

        int arr[] = { 1, 2, 3, 4, 10 };
        int n = arr.length;

        if (isSumEqual(arr, n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by jit_t.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if sum of
# first n-1 elements of the array is
# equal to the last element
def isSumEqual(ar, n):
    sum = 0

    # Find the sum of first n-1
    # elements of the array
    for i in range(n - 1):
        sum += ar[i]

    # If sum equals to the last element
    if (sum == ar[n - 1]):
        return True

    return False

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 10]
    n = len(arr)

    if (isSumEqual(arr, n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function that returns true if sum of
    // first n-1 elements of the array is
    // equal to the last element
    static bool isSumEqual(int[] ar, int n)
    {
        int sum = 0;

        // Find the sum of first n-1
        // elements of the array
        for (int i = 0; i < n - 1; i++)
            sum += ar[i];

        // If sum equals to the last element
        if (sum == ar[n - 1])
            return true;

        return false;
    }

    // Driver code
    static public void Main()
    {
        int[] arr = { 1, 2, 3, 4, 10 };
        int n = arr.Length;

        if (isSumEqual(arr, n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if sum of
// first n-1 elements of the array is
// equal to the last element
function isSumEqual($ar, $n)
{
    $sum = 0;

    // Find the sum of first n-1
    // elements of the array
    for ($i = 0; $i < $n - 1; $i++)
        $sum += $ar[$i];

    // If sum equals to the last element
    if ($sum == $ar[$n - 1])
        return true;

    return false;
}

// Driver code
$arr = array( 1, 2, 3, 4, 10 );
$n = count($arr);

if (isSumEqual($arr, $n))
    echo "Yes";
else
    echo "No";

// This code is contributed by AnkitRai01

?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function that returns true if sum of
    // first n-1 elements of the array is
    // equal to the last element
    function isSumEqual(ar, n)
    {
        let sum = 0;

        // Find the sum of first n-1
        // elements of the array
        for (let i = 0; i < n - 1; i++)
            sum += ar[i];

        // If sum equals to the last element
        if (sum == ar[n - 1])
            return true;

        return false;
    }

    let arr = [ 1, 2, 3, 4, 10 ];
    let n = arr.length;

    if (isSumEqual(arr, n))
      document.write("Yes");
    else
      document.write("No");

</script>
```

**Output:** 

```
Yes
```