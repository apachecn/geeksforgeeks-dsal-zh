# 用左侧最大的元素替换每个元素

> 原文:[https://www . geesforgeks . org/用左侧最大元素替换每个元素/](https://www.geeksforgeeks.org/replace-every-element-with-the-greatest-element-on-its-left-side/)

给定一个整数数组，任务是用左边最大的元素替换每个元素。
**注意:**将第一个元素替换为-1，因为它的左边没有元素。
**示例:**

```
Input: arr[] = {4, 5, 2, 1, 7, 6}
Output: -1 4 5 5 5 7
Since, 4 has no element in its left, so replace it by -1.
For 5, 4 is the greatest element in its left.
For 2, 5 is the greatest element in its left.
For 1, 5 is the greatest element in its left.
For 7, 5 is the greatest element in its left.
For 6, 7 is the greatest element in its left.

Input: arr[] = {3, 2, 5, 7, 1}
Output: -1 3 3 5 7
```

**进场:**

1.  保持一个变量 max_ele，它将存储最大的元素。
2.  最初，max_ele 将等于第 0 个索引处的元素。
3.  首先用-1 替换 arr[0]，然后遍历数组
4.  然后用 max_ele 值替换元素，如果元素大于 max_ele，则更新 max_ele。
5.  打印修改后的数组。

以下是上述方法的实现:

## C++

```
// C++ program to Replace every
// element with the greater element
// on its left side
#include <bits/stdc++.h>
using namespace std;

// Function to replace the elements
void ReplaceElements(int arr[], int n)
{
    // Max value initialised
    // to element at 0th index
    int max_ele = arr[0];
    arr[0] = -1;

    for (int i = 1; i < n; ++i) {

        // If max_ele is greater than arr[i]
        // then just replace arr[i] with max_ele
        if (max_ele > arr[i])
            arr[i] = max_ele;

        // Else if update the max_ele also
        else if (max_ele <= arr[i]) {
            int temp = arr[i];
            arr[i] = max_ele;
            max_ele = temp;
        }
    }
}

// Driver code
int main()
{
    int arr[] = { 4, 5, 2, 1, 7, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Replace the elements
    // with the smaller element
    // on its left side
    ReplaceElements(arr, n);

    // Print the modified array
    for (int i = 0; i < n; ++i)
        cout << arr[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Replace every
// element with the greater element
// on its left side
import java.util.*;

class Geeks {

// Function to replace the elements
static void ReplaceElements(int arr[], int n)
{
    // Max value initialised
    // to element at 0th index
    int max_ele = arr[0];
    arr[0] = -1;

    for (int i = 1; i < n; ++i) {

        // If max_ele is greater than arr[i]
        // then just replace arr[i] with max_ele
        if (max_ele > arr[i])
            arr[i] = max_ele;

        // Else if update the max_ele also
        else if (max_ele <= arr[i]) {
            int temp = arr[i];
            arr[i] = max_ele;
            max_ele = temp;
        }
    }
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 4, 5, 2, 1, 7, 6 };
    int n = arr.length;

    // Replace the elements
    // with the smaller element
    // on its left side
    ReplaceElements(arr, n);

    // Print the modified array
    for (int i = 0; i < n; ++i)
        System.out.println(arr[i]);
}
}

// This code is contributed by ankita_saini
```

## 蟒蛇 3

```
# Python3 program to Replace every
# element with the greater element
# on its left side

# Function to replace the elements
def ReplaceElements(arr, n):

    # Max value initialised
    # to element at 0th index
    max_ele = arr[0]
    arr[0] = -1

    for i in range(1, n):

        # If max_ele is greater than arr[i]
        # then just replace arr[i] with max_ele
        if (max_ele > arr[i]):
            arr[i] = max_ele

        # Else if update the max_ele also
        elif (max_ele <= arr[i]):
            temp = arr[i]
            arr[i] = max_ele
            max_ele = temp

# Driver code
if __name__ == "__main__":

    arr = [4, 5, 2, 1, 7, 6 ]
    n = len(arr)

    # Replace the elements
    # with the smaller element
    # on its left side
    ReplaceElements(arr, n)

    # Print the modified array
    for i in range (n):
        print( arr[i], end = " ")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to Replace every
// element with the greater element
// on its left side
using System;
public class GFG {

// Function to replace the elements
static void ReplaceElements(int []arr, int n)
{
    // Max value initialised
    // to element at 0th index
    int max_ele = arr[0];
    arr[0] = -1;

    for (int i = 1; i < n; ++i) {

        // If max_ele is greater than arr[i]
        // then just replace arr[i] with max_ele
        if (max_ele > arr[i])
            arr[i] = max_ele;

        // Else if update the max_ele also
        else if (max_ele <= arr[i]) {
            int temp = arr[i];
            arr[i] = max_ele;
            max_ele = temp;
        }
    }
}

// Driver code
public static void Main()
{
    int []arr = { 4, 5, 2, 1, 7, 6 };
    int n = arr.Length;

    // Replace the elements
    // with the smaller element
    // on its left side
    ReplaceElements(arr, n);

    // Print the modified array
    for (int i = 0; i < n; ++i) {
        Console.Write(arr[i]+" ");
    }
}
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Replace every
// element with the greater element
// on its left side

// Function to replace the elements
function ReplaceElements($arr, $n)
{
    // Max value initialised
    // to element at 0th index
    $max_ele = $arr[0];
    $arr[0] = -1;

    for ($i = 1; $i < $n; ++$i)
    {

        // If max_ele is greater than arr[i]
        // then just replace arr[i] with max_ele
        if ($max_ele > $arr[$i])
            $arr[$i] = $max_ele;

        // Else if update the max_ele also
        else if ($max_ele <= $arr[$i])
        {
            $temp = $arr[$i];
            $arr[$i] = $max_ele;
            $max_ele = $temp;
        }
    }
    return $arr;
}

// Driver code
$arr = array(4, 5, 2, 1, 7, 6);
$n = sizeof($arr);

// Replace the elements
// with the smaller element
// on its left side
$arr1 = ReplaceElements($arr, $n);

// Print the modified array
for ($i = 0; $i < $n; ++$i)
    echo $arr1[$i] . " ";

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
// Java script program to Replace every
// element with the greater element
// on its left side

// Function to replace the elements
function ReplaceElements(arr,n)
{

    // Max value initialised
    // to element at 0th index
    let max_ele = arr[0];
    arr[0] = -1;

    for (let i = 1; i < n; ++i) {

        // If max_ele is greater than arr[i]
        // then just replace arr[i] with max_ele
        if (max_ele > arr[i])
            arr[i] = max_ele;

        // Else if update the max_ele also
        else if (max_ele <= arr[i]) {
            let temp = arr[i];
            arr[i] = max_ele;
            max_ele = temp;
        }
    }
}

// Driver code
    let arr = [ 4, 5, 2, 1, 7, 6 ];
    let n = arr.length;

    // Replace the elements
    // with the smaller element
    // on its left side
    ReplaceElements(arr, n);

    // Print the modified array
    for (let i = 0; i < n; ++i)
        document.write(arr[i]+" ");

// This code is contributed by sravan kumar G
</script>
```

**Output:** 

```
-1 4 5 5 5 7
```

**时间复杂度:** O(N)