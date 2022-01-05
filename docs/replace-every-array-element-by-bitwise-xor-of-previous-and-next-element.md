# 通过上一个和下一个元素的按位异或来替换每个数组元素

> 原文:[https://www . geeksforgeeks . org/通过对上一个和下一个元素进行逐位异或来替换每个数组元素/](https://www.geeksforgeeks.org/replace-every-array-element-by-bitwise-xor-of-previous-and-next-element/)

给定一个整数数组，用前一个和后一个元素的 xor 替换每个元素，但有以下例外。
a)第一个元素被第一个和第二个的和代替。
b)最后一个元素被最后一个和第二个最后一个的和所取代。

**示例:**

```
Input: arr[] = { 2, 3, 4, 5, 6}
Output: 1 6 6 2 3 

We get the following array as {2^3, 2^4, 3^5, 4^6, 5^6}

Input: arr[] = { 1, 2, 1, 5}
Output: 3, 0, 7, 4

We get the following array as {1^2, 1^1, 2^5, 1^5}

```

一个**简单的解决方案**就是创建一个辅助数组，将给定数组的内容复制到辅助数组中。最后遍历辅助数组，并使用复制的值更新给定数组。该解决方案的时间复杂度为 O(n)，但需要 O(n)个额外空间。

一个**高效解**可以解决 O(n)时间和 O(1)空间的问题。想法是跟踪循环中的前一个元素。使用额外的变量对前一个元素和下一个元素进行异或运算，得到每个元素。

下面是上述方法的实现:

## C++

```
// C++ program to update every array element with
// sum of previous and next numbers in array
#include <iostream>
using namespace std;

void ReplaceElements(int arr[], int n)
{
    // Nothing to do when array size is 1
    if (n <= 1)
        return;

    // store current value of arr[0] and update it
    int prev = arr[0];
    arr[0] = arr[0] ^ arr[1];

    // Update rest of the array elements
    for (int i = 1; i < n - 1; i++) {
        // Store current value of next interaction
        int curr = arr[i];

        // Update current value using previous value
        arr[i] = prev ^ arr[i + 1];

        // Update previous value
        prev = curr;
    }

    // Update last array element separately
    arr[n - 1] = prev ^ arr[n - 1];
}

// Driver program
int main()
{
    int arr[] = { 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    ReplaceElements(arr, n);

    // Print the modified array
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to update every array
// element with sum of previous and
// next numbers in array
import  java .io.*;

class GFG
{
static void ReplaceElements(int[] arr,
                            int n)
{
    // Nothing to do when array size is 1
    if (n <= 1)
        return;

    // store current value of arr[0]
    // and update it
    int prev = arr[0];
    arr[0] = arr[0] ^ arr[1];

    // Update rest of the array elements
    for (int i = 1; i < n - 1; i++)
    {
        // Store current value of
        // next interaction
        int curr = arr[i];

        // Update current value using
        // previous value
        arr[i] = prev ^ arr[i + 1];

        // Update previous value
        prev = curr;
    }

    // Update last array element separately
    arr[n - 1] = prev ^ arr[n - 1];
}

// Driver Code
public static void main(String[] args)

{
    int[] arr = { 2, 3, 4, 5, 6 };
    int n = arr.length;

    ReplaceElements(arr, n);

    // Print the modified array
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}
}

// This code is contributed
// by anuj_67..
```

## 蟒蛇 3

```
# Python3 program to update every
# array element with sum of previous
# and next numbers in array
def ReplaceElements(arr, n):

    # Nothing to do when array
    # size is 1
    if n <= 1:
        return

    # store current value of arr[0]
    # and update it
    prev = arr[0]
    arr[0] = arr[0] ^ arr[1]

    # Update rest of the array elements
    for i in range(1, n - 1):

        # Store current value of
        # next interaction
        curr = arr[i]

        # Update current value using
        # previous value
        arr[i] = prev ^ arr[i + 1]

        # Update previous value
        prev = curr

    # Update last array element separately
    arr[n - 1] = prev ^ arr[n - 1]

# Driver Code
arr = [2, 3, 4, 5, 6]
n = len(arr)
ReplaceElements(arr, n)
for i in range(n):
    print(arr[i], end = " ")

# This code is contributed
# by Shrikant13
```

## C#

```
// C# program to update every array
// element with sum of previous and
// next numbers in array
using System;

class GFG
{
static void ReplaceElements(int[] arr,
                            int n)
{
    // Nothing to do when array size is 1
    if (n <= 1)
        return;

    // store current value of arr[0]
    // and update it
    int prev = arr[0];
    arr[0] = arr[0] ^ arr[1];

    // Update rest of the array elements
    for (int i = 1; i < n - 1; i++)
    {
        // Store current value of
        // next interaction
        int curr = arr[i];

        // Update current value using
        // previous value
        arr[i] = prev ^ arr[i + 1];

        // Update previous value
        prev = curr;
    }

    // Update last array element separately
    arr[n - 1] = prev ^ arr[n - 1];
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 3, 4, 5, 6 };
    int n = arr.Length;

    ReplaceElements(arr, n);

    // Print the modified array
    for (int i = 0; i < n; i++)
        Console.Write(arr[i] + " ");
}
}

// This code is contributed
// by Akanskha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to update every array
// element with sum of previous and
// next numbers in array
function ReplaceElements(&$arr, $n)
{
    // Nothing to do when array size is 1
    if ($n <= 1)
        return;

    // store current value of arr[0]
    // and update it
    $prev = $arr[0];
    $arr[0] = $arr[0] ^ $arr[1];

    // Update rest of the array elements
    for ($i = 1; $i < $n - 1; $i++)
    {
        // Store current value of next
        // interaction
        $curr = $arr[$i];

        // Update current value using
        // previous value
        $arr[$i] = $prev ^ $arr[$i + 1];

        // Update previous value
        $prev = $curr;
    }

    // Update last array element separately
    $arr[$n - 1] = $prev ^ $arr[$n - 1];
}

// Driver Code
$arr = array( 2, 3, 4, 5, 6 );
$n = sizeof($arr);

ReplaceElements($arr, $n);

// Print the modified array
for ($i = 0; $i < $n; $i++)
    echo $arr[$i] . " ";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to update every array
// element with sum of previous and next
// numbers in array
function ReplaceElements(arr, n)
{

    // Nothing to do when array size is 1
    if (n <= 1)
        return;

    // Store current value of arr[0] and update it
    let prev = arr[0];
    arr[0] = arr[0] ^ arr[1];

    // Update rest of the array elements
    for(let i = 1; i < n - 1; i++)
    {

        // Store current value of next interaction
        let curr = arr[i];

        // Update current value using previous value
        arr[i] = prev ^ arr[i + 1];

        // Update previous value
        prev = curr;
    }

    // Update last array element separately
    arr[n - 1] = prev ^ arr[n - 1];
}

// Driver code
let arr = [ 2, 3, 4, 5, 6 ];
let n = arr.length;

ReplaceElements(arr, n);

// Print the modified array
for(let i = 0; i < n; i++)
    document.write(arr[i] + " ");

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
1 6 6 2 3
```