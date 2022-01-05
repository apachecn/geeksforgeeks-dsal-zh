# 平均绝对偏差程序

> 原文:[https://www . geesforgeks . org/program-mean-绝对值偏差/](https://www.geeksforgeeks.org/program-mean-absolute-deviation/)

给定大小为 n 的数组，求平均绝对偏差。
先决条件:[均值、方差和标准差](https://www.geeksforgeeks.org/mathematics-mean-variance-and-standard-deviation/)
**示例:**

```
Input : arr[] = {10, 15, 15, 17, 18, 21}
Output : 2.66667

Input : arr[] = {23.54, 56, 34.56, 67, 45.34,  
                              56.78, 78, 21}
Output : 16.6675
```

> 数据集的平均绝对偏差或平均绝对偏差是与平均值或中心点的绝对差异的平均值。平均绝对偏差可以用下面给出的方法计算。
> 设 arr[n]为 n 大小的数组，任务是求平均绝对偏差。
> 平均绝对偏差=(绝对值(arr[0]–平均值)+绝对值(arr[1]–平均值)+。。。+ABS(arr[n-1]–平均值)/n；
> 其中 i = 0，1，2，。。。n-1 和“abs”是绝对的区别。
> 均值= (arr[0] + arr[1] + arr[2] +。。。+arr[n-1])/n；

## C++

```
// C++ Program to find mean absolute
// deviation of given array.
#include <bits/stdc++.h>
using namespace std;

// Function to find mean
// of the array elements.
float Mean(float arr[], int n)
{  
    // Calculate sum of all elements.
    float sum = 0;
    for (int i = 0; i < n; i++)
        sum = sum + arr[i];
    return sum / n;
}

// Function to find mean absolute
// deviation of given elements.
float meanAbsoluteDeviation(float arr[], int n)
{  
    // Calculate the sum of absolute
    // deviation about mean.
    float absSum = 0;
    for (int i = 0; i < n; i++)
        absSum = absSum + abs(arr[i] - Mean(arr, n));

    // Return mean absolute deviation about mean.
    return absSum / n;
}

// Driver function.
int main()
{
    float arr[] = { 10, 15, 15, 17, 18, 21 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << meanAbsoluteDeviation(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java Program to find mean absolute
// deviation of given array
import java.io.*;

class GFG {

    // Function to find mean
    // of the array elements.
    static float Mean(float arr[], int n)
    {
        // Calculate sum of all elements.
        float sum = 0;

        for (int i = 0; i < n; i++)
            sum = sum + arr[i];

        return sum / n;
    }

    // Function to find mean absolute
    // deviation of given elements.
    static float meanAbsDevtion(float arr[],
                                       int n)
    {
        // Calculate the sum of absolute
        // deviation about mean.
        float absSum = 0;

        for (int i = 0; i < n; i++)
            absSum = absSum + Math.abs(arr[i]
                                - Mean(arr, n));

        // Return mean absolute
        // deviation about mean.
        return absSum / n;
    }

        // Driver function.
        public static void main (String[] args) {

        float arr[] = { 10, 15, 15, 17, 18, 21 };
        int n = arr.length;

            System.out.println(meanAbsDevtion(arr, n));
        }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 Program to find
# mean absolute deviation
# of given array.

# Function to find mean
# of the array elements.
def Mean(arr, n) :

    # Calculate sum of all
    # elements.
    sm = 0

    for i in range(0, n) :
        sm = sm + arr[i]
    return sm // n

# Function to find mean
# absolute deviation of
# given elements.
def meanAbsoluteDeviation(arr, n) :

    # Calculate the sum of
    # absolute deviation
    # about mean.
    absSum = 0
    for i in range(0, n ):
        absSum = absSum + abs(arr[i] -
                         Mean(arr, n))

    # Return mean absolute
    # deviation about mean.
    return absSum / n

# Driver function.
arr = [ 10, 15, 15, 17, 18, 21 ]
n = len(arr)

print(meanAbsoluteDeviation(arr, n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# Program to find mean absolute
// deviation of given array
using System;

class GFG {

    // Function to find mean
    // of the array elements.
    static float Mean(float []arr, int n)
    {
        // Calculate sum of all elements.
        float sum = 0;

        for (int i = 0; i < n; i++)
            sum = sum + arr[i];

        return sum / n;
    }

    // Function to find mean absolute
    // deviation of given elements.
    static float meanAbsDevtion(float []arr,
                                    int n)
    {
        // Calculate the sum of absolute
        // deviation about mean.
        float absSum = 0;

        for (int i = 0; i < n; i++)
            absSum = absSum + Math.Abs(arr[i]
                                - Mean(arr, n));

        // Return mean absolute
        // deviation about mean.
        return absSum / n;
    }

        // Driver function.
        public static void Main ()
        {

            float []arr = { 10, 15, 15, 17, 18, 21 };
            int n = arr.Length;

            Console.WriteLine(meanAbsDevtion(arr, n));
        }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find mean absolute
// deviation of given array.

// Function to find mean
// of the array elements.
function Mean($arr, $n)
{

    // Calculate sum of
    // all elements.
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum = $sum + $arr[$i];
    return $sum / $n;
}

// Function to find mean absolute
// deviation of given elements.
function meanAbsoluteDeviation($arr, $n)
{

    // Calculate the sum of absolute
    // deviation about mean.
    $absSum = 0;
    for ($i = 0; $i < $n; $i++)
        $absSum = $absSum + abs($arr[$i] -
                         Mean($arr, $n));

    // Return mean absolute
    // deviation about mean.
    return $absSum / $n;
}

    // Driver Code
    $arr = array(10, 15, 15, 17, 18, 21);
    $n = sizeof($arr);
    echo meanAbsoluteDeviation($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find mean absolute
// deviation of given array

    // Function to find mean
    // of the array elements.
    function Mean(arr, n)
    {
        // Calculate sum of all elements.
        let sum = 0;

        for (let i = 0; i < n; i++)
            sum = sum + arr[i];

        return sum / n;
    }

    // Function to find mean absolute
    // deviation of given elements.
    function meanAbsDevtion(arr, n)
    {
        // Calculate the sum of absolute
        // deviation about mean.
        let absSum = 0;

        for (let i = 0; i < n; i++)
            absSum = absSum + Math.abs(arr[i]
                                - Mean(arr, n));

        // Return mean absolute
        // deviation about mean.
        return absSum / n;
    }

// Driver code
        let arr = [ 10, 15, 15, 17, 18, 21];
        let n = arr.length;

        document.write(meanAbsDevtion(arr, n));

 // This code is contributed by sanjoy_62.
</script>
```

输出:

```
2.66667
```