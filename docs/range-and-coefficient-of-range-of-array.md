# 数组的范围和范围系数

> 原文:[https://www . geeksforgeeks . org/数组范围和范围系数/](https://www.geeksforgeeks.org/range-and-coefficient-of-range-of-array/)

给定一个整数元素的数组 **arr** ，任务是找出给定数组的范围和范围系数，其中:
**范围:**分布中最大值和最小值之差。
**范围系数:**(最大–最小)/(最大+最小)。
**举例:**

> **输入:** arr[] = {15，16，10，9，6，7，17}
> **输出:**范围:11
> 范围系数:0.478261
> 最大值= 17，最小值= 6
> 范围=最大值–最小值= 17–6 = 11
> 范围系数=(最大值–最小值)/(最大值+最小值)= 11/23 = 0.478261
> T10

**方法:**从给定的数组中找出最大和最小元素，计算范围和范围系数如下:

*   范围=最大–最小
*   范围系数=(最大–最小)/(最大+最小)

以下是上述方法的实现:

## C++

```
// C++ implementation to find
// Range and coefficient of range
#include <iostream>
#include <numeric>
using namespace std;

// Function to return the minimum element from the array
float getMin(float arr[], int n)
{
    float res = arr[0];
    for (int i = 1; i < n; i++)
        res = min(res, arr[i]);
    return res;
}

// Function to return the maximum element from the array
float getMax(float arr[], int n)
{
    float res = arr[0];
    for (int i = 1; i < n; i++)
        res = max(res, arr[i]);
    return res;
}

// Function to print the Range and
// Coefficient of Range in the given array
void findRangeAndCoefficient(float arr[], int n)
{
    float max = getMax(arr, n);
    float min = getMin(arr, n);
    float range = max - min;
    float coeffOfRange = range / (max + min);
    cout << "Range : " << range << endl;
    cout << "Coefficient of Range : " << coeffOfRange;
}

// Driver code
int main()
{
    float arr[] = { 5, 10, 15 };
    int n = sizeof(arr) / sizeof(arr[0]);
    findRangeAndCoefficient(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// Range and coefficient of range

import java.io.*;

class GFG {
    // Function to return the minimum element from the array
static float getMin(float arr[], int n)
{
    float res = arr[0];
    for (int i = 1; i < n; i++)
        res = Math.min(res, arr[i]);
    return res;
}

// Function to return the maximum element from the array
static float getMax(float arr[], int n)
{
    float res = arr[0];
    for (int i = 1; i < n; i++)
        res = Math.max(res, arr[i]);
    return res;
}

// Function to print the Range and
// Coefficient of Range in the given array
static void findRangeAndCoefficient(float arr[], int n)
{
    float max = getMax(arr, n);
    float min = getMin(arr, n);
    float range = max - min;
    float coeffOfRange = range / (max + min);
    System.out.println("Range : " + range );
    System.out.println("Coefficient of Range : " + coeffOfRange);
}

       // Driver code
    public static void main (String[] args) {

    float arr[] = { 5, 10, 15 };
    int n = arr.length;
    findRangeAndCoefficient(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation to find
# Range and coefficient of range

# Function to return the minimum
# element from the array
def getMin(arr, n):
    res = arr[0]
    for i in range(1, n, 1):
        res = min(res, arr[i])
    return res

# Function to return the maximum
# element from the array
def getMax(arr, n):
    res = arr[0]
    for i in range(1, n, 1):
        res = max(res, arr[i])
    return res

# Function to print the Range and
# Coefficient of Range in the given array
def findRangeAndCoefficient(arr, n):
    max = getMax(arr, n)
    min = getMin(arr, n)
    range = max - min
    coeffOfRange = range / (max + min)
    print("Range :", range)
    print("Coefficient of Range :", coeffOfRange)

# Driver code
if __name__ == '__main__':
    arr = [5, 10, 15]
    n = len(arr)
    findRangeAndCoefficient(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation to find
// Range and coefficient of range

using System;

public class GFG{
    // Function to return the minimum element from the array
static float getMin(float []arr, int n)
{
    float res = arr[0];
    for (int i = 1; i < n; i++)
        res = Math.Min(res, arr[i]);
    return res;
}

// Function to return the maximum element from the array
static float getMax(float []arr, int n)
{
    float res = arr[0];
    for (int i = 1; i < n; i++)
        res = Math.Max(res, arr[i]);
    return res;
}

// Function to print the Range and
// Coefficient of Range in the given array
static void findRangeAndCoefficient(float []arr, int n)
{
    float max = getMax(arr, n);
    float min = getMin(arr, n);
    float range = max - min;
    float coeffOfRange = range / (max + min);
    Console.WriteLine ("Range : " + range );
    Console.WriteLine ("Coefficient of Range : " + coeffOfRange);
}

// Driver code

    static public void Main (){

    float []arr = { 5, 10, 15 };
    int n = arr.Length;
    findRangeAndCoefficient(arr, n);
    }
//This code is contributed by akt_mit.   
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// Range and coefficient of range
// Function to return the minimum
// element from the array
function getMin($arr, $n)
{
    $res = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $res = min($res, $arr[$i]);
    return $res;
}

// Function to return the maximum
// element from the array
function getMax($arr, $n)
{
    $res = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $res = max($res, $arr[$i]);
    return $res;
}

// Function to print the Range and
// Coefficient of Range in the given array
function findRangeAndCoefficient($arr, $n)
{
    $max = getMax($arr, $n);
    $min = getMin($arr, $n);
    $range = $max - $min;
    $coeffOfRange = $range / ($max + $min);
    echo "Range : ", $range, "\n";
    echo "Coefficient of Range : ",
                     $coeffOfRange;
}

// Driver code
$arr = array( 5, 10, 15 );
$n = sizeof($arr);
findRangeAndCoefficient($arr, $n);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

    // Javascript implementation to find
    // Range and coefficient of range

    // Function to return the minimum
    // element from the array
    function getMin(arr, n)
    {
        let res = arr[0];
        for (let i = 1; i < n; i++)
            res = Math.min(res, arr[i]);
        return res;
    }

    // Function to return the maximum
    // element from the array
    function getMax(arr, n)
    {
        let res = arr[0];
        for (let i = 1; i < n; i++)
            res = Math.max(res, arr[i]);
        return res;
    }

    // Function to print the Range and
    // Coefficient of Range in the given array
    function findRangeAndCoefficient(arr, n)
    {
        let max = getMax(arr, n);
        let min = getMin(arr, n);
        let range = max - min;
        let coeffOfRange = range / (max + min);
        document.write("Range : " + range + "</br>");
        document.write("Coefficient of Range : " +
        coeffOfRange + "</br>");
    }

    let arr = [ 5, 10, 15 ];
    let n = arr.length;
    findRangeAndCoefficient(arr, n);

</script>
```

**Output:** 

```
Range : 10
Coefficient of Range : 0.5
```

**时间复杂度:** O(n)
***辅助空间** : O(1)*