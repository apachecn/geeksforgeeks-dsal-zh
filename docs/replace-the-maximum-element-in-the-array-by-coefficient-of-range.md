# 用范围系数

替换数组中的最大元素

> 原文:[https://www . geesforgeks . org/按范围系数替换数组中的最大元素/](https://www.geeksforgeeks.org/replace-the-maximum-element-in-the-array-by-coefficient-of-range/)

给定一个整数元素数组 **arr[]** ，任务是用同一个数组的[范围系数](https://www.geeksforgeeks.org/range-and-coefficient-of-range-of-array/)替换数组中的最大元素。
**范围系数:**(最大–最小)/(最大+最小)

**示例:**

> **输入:** arr[] = {15，16，10，9，6，7，17}
> **输出:** 15 16 10 9 6 7 0.478261
> Max = 17，Min = 6
> 范围系数=(Max–Min)/(Max+Min)= 11/23 = 0.478261
> 
> **输入:** arr[] = {5，10，15 }
> T3】输出: 5 10 0.5

**方法:**从给定数组中找到最大和最小元素，计算范围系数，**系数=(最大–最小)/(最大+最小)**然后用计算出的**系数**替换最大元素。更新数组后，打印更新数组的内容。

下面是上述方法的实现:

## C++

```
// C++ implementation to replace maximum element
// by coefficient of range
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the contents of the array
void printArr(float arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to replace the maximum element from the array
// with the coefficient of range of the array
void replaceMax(float arr[], int n)
{

    // Maximum element from the array
    float max = *std::max_element(arr, arr + n);

    // Minimum element from the array
    float min = *std::min_element(arr, arr + n);

    // Calculate the coefficient of range for the array
    float range = max - min;
    float coeffOfRange = range / (max + min);

    // Assuming all the array elements are distinc
    // Replace the maximum element with
    // the coefficient of range of the array
    for (int i = 0; i < n; i++) {
        if (arr[i] == max) {
            arr[i] = coeffOfRange;
            break;
        }
    }

    // Print the updated array
    printArr(arr, n);
}

// Driver code
int main()
{
    float arr[] = { 15, 16, 10, 9, 6, 7, 17 };
    int n = sizeof(arr) / sizeof(arr[0]);
    replaceMax(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to replace maximum element
// by coefficient of range
import java.util.*;

class GFG
{

// Utility function to print the
// contents of the array
static void printArr(float arr[], int n)
{
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Function to replace the maximum
// element from the array with the
// coefficient of range of the array
static void replaceMax(float arr[], int n)
{
    // Maximum element from the array
    float max = arr[0];
    for(int i = 0; i < n; i++)
    {
        if(arr[i] > max)
        max = arr[i];
    }
    // Minimum element from the array
    float min = arr[0];
    for(int i = 0; i < n; i++)
    {
        if(arr[i] < min)
        min = arr[i];
    }

    // Calculate the coefficient of
    // range for the array
    float range = max - min;
    float coeffOfRange = range / (max + min);

    // Assuming all the array elements are distinc
    // Replace the maximum element with
    // the coefficient of range of the array
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == max)
        {
            arr[i] = coeffOfRange;
            break;
        }
    }

    // Print the updated array
    printArr(arr, n);
}

// Driver code
public static void main(String args[])
{
    float arr[] = { 15, 16, 10, 9, 6, 7, 17 };
    int n = arr.length;
    replaceMax(arr, n);

}
}

// This code is contributed by
// Sahil_Shelangia
```

## 蟒蛇 3

```
# Python3 implementation to replace
# maximum element by coefficient of range

# Utility function to print the
# contents of the array
def printArr(arr, n) :

    for i in range(n) :
        print(arr[i], end = " ")

# Function to replace the maximum element
# from the array with the coefficient of
# range of the array
def replaceMax(arr, n) :

    # Maximum element from the array
    max_element = max(arr)

    # Minimum element from the array
    min_element = min(arr)

    # Calculate the coefficient of
    # range for the array
    ranges = max_element - min_element
    coeffOfRange = ranges / (max_element + min_element)

    # Assuming all the array elements are
    # distinct. Replace the maximum element
    # with the coefficient of range of the array
    for i in range(n) :
        if (arr[i] == max_element) :
            arr[i] = coeffOfRange
            break

    # Print the updated array
    printArr(arr, n)

# Driver code
if __name__ == "__main__" :

    arr = [ 15, 16, 10, 9, 6, 7, 17 ]
    n = len(arr)

    replaceMax(arr, n)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation to replace maximum element
// by coefficient of range
using System;

class GFG
{

// Utility function to print the
// contents of the array
static void printArr(float []arr, int n)
{
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}

// Function to replace the maximum
// element from the array with the
// coefficient of range of the array
static void replaceMax(float []arr, int n)
{
    // Maximum element from the array
    float max = arr[0];
    for(int i = 0; i < n; i++)
    {
        if(arr[i] > max)
        max = arr[i];
    }

    // Minimum element from the arra
    float min = arr[0];
    for(int i = 0; i < n; i++)
    {
        if(arr[i] < min)
        min = arr[i];
    }

    // Calculate the coefficient of
    // range for the array
    float range = max - min;
    float coeffOfRange = range / (max + min);

    // Assuming all the array elements are distinc
    // Replace the maximum element with
    // the coefficient of range of the array
    for (int i = 0; i < n; i++)
    {
        if (arr[i] == max)
        {
            arr[i] = coeffOfRange;
            break;
        }
    }

    // Print the updated array
    printArr(arr, n);
}

// Driver code
public static void Main()
{
    float []arr = { 15, 16, 10, 9, 6, 7, 17 };
    int n = arr.Length;
    replaceMax(arr, n);
}
}

// This code is contributed by
// shs..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to replace maximum
// element by coefficient of range

// Utility function to print the
// contents of the array
function printArr($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i] . " ";
}

// Function to replace the maximum element
// from the array with the coefficient of
// range of the array
function replaceMax($arr, $n)
{

    // Maximum element from the array
    $max = max($arr);

    // Minimum element from the array
    $min = min($arr);

    // Calculate the coefficient of
    // range for the array
    $range = $max - $min;
    $coeffOfRange = round($range /
                         ($max + $min), 6);

    // Assuming all the array elements
    // are distinct. Replace the maximum
    // element with the coefficient of
    // range of the array
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] == $max)
        {
            $arr[$i] = $coeffOfRange;
            break;
        }
    }

    // Print the updated array
    printArr($arr, $n);
}

// Driver code
$arr = array( 15, 16, 10, 9, 6, 7, 17 );
$n = count($arr);
replaceMax($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation to
    // replace maximum element
    // by coefficient of range

    // Utility function to print the
    // contents of the array
    function printArr(arr, n)
    {
        for (let i = 0; i < n - 1; i++)
            document.write(arr[i] + " ");

          document.write(arr[n - 1].toFixed(6));
    }

    // Function to replace the maximum
    // element from the array with the
    // coefficient of range of the array
    function replaceMax(arr, n)
    {
        // Maximum element from the array
        let max = arr[0];
        for(let i = 0; i < n; i++)
        {
            if(arr[i] > max)
                max = arr[i];
        }

        // Minimum element from the arra
        let min = arr[0];
        for(let i = 0; i < n; i++)
        {
            if(arr[i] < min)
                min = arr[i];
        }

        // Calculate the coefficient of
        // range for the array
        let range = max - min;
        let coeffOfRange = range / (max + min);

        // Assuming all the array elements are distinc
        // Replace the maximum element with
        // the coefficient of range of the array
        for (let i = 0; i < n; i++)
        {
            if (arr[i] == max)
            {
                arr[i] = coeffOfRange;
                break;
            }
        }

        // Print the updated array
        printArr(arr, n);
    }

    let arr = [ 15, 16, 10, 9, 6, 7, 17 ];
    let n = arr.length;
    replaceMax(arr, n);

</script>
```

**Output:** 

```
15 16 10 9 6 7 0.478261
```

**时间复杂度:**O(n)
T3】辅助空间 : O(1)。