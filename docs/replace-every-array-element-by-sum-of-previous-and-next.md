# 用上一个和下一个的和替换每个数组元素

> 原文:[https://www . geeksforgeeks . org/按上一个和下一个的总和替换每个数组元素/](https://www.geeksforgeeks.org/replace-every-array-element-by-sum-of-previous-and-next/)

给定一个整数数组，用前一个和后一个元素的和更新每个元素，但有以下例外。
a)第一个元素被第一个和第二个的和代替。
b)最后一个元素被最后一个和第二个最后一个的和所取代。
**例:**

```
Input : arr[] = { 2, 3, 4, 5, 6}
Output : 5 6 8 10 11
Explanation: We get the following array as {2+3, 2+4, 3+5, 4+6, 5+6}

Input : arr[] = { 3, 2, 1}
Output : 5 4 3
```

一个**简单的解决方案**就是创建一个辅助数组，将给定数组的内容复制到辅助数组中。最后遍历辅助数组，并使用复制的值更新给定数组。该解决方案的时间复杂度为 O(n)，但需要 O(n)个额外空间。
一个**高效的解决方案**可以在 O(n)时间和 O(1)空间内解决问题。想法是跟踪循环中的前一个元素。使用额外的变量添加上一个元素，并使用下一个元素来获取每个元素。
下面是这个想法的实现。

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
    arr[0] = arr[0] + arr[1];

    // Update rest of the array elements
    for (int i = 1; i < n - 1; i++) {

        // Store current value of next iteration
        int curr = arr[i];

        // Update current value using previews value
        arr[i] = prev + arr[i + 1];

        // Update previous value
        prev = curr;
    }

    // Update last array element separately
    arr[n - 1] = prev + arr[n - 1];
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
// Java program to update every array element with
// sum of previous and next numbers in array

import java.io.*;

class GFG {
        static void ReplaceElements(int arr[], int n) {
        // Nothing to do when array size is 1
        if (n <= 1) {
            return;
        }

        // store current value of arr[0] and update it
        int prev = arr[0];
        arr[0] = arr[0] + arr[1];

        // Update rest of the array elements
        for (int i = 1; i < n - 1; i++) {

            // Store current value of next iteration
            int curr = arr[i];

            // Update current value using previews value
            arr[i] = prev + arr[i + 1];

            // Update previous value
            prev = curr;
        }

        // Update last array element separately
        arr[n - 1] = prev + arr[n - 1];
    }

// Driver program

    public static void main (String[] args) {

        int arr[] = {2, 3, 4, 5, 6};
        int n = arr.length;
        ReplaceElements(arr, n);
        // Print the modified array
        for (int i = 0; i < n; i++) {
            System.out.print(arr[i] + " ");
        }
    }
}
// This code is contributed by akt_mit
```

## 蟒蛇 3

```
# Python 3 program to update every array
# element with sum of previous and next
# numbers in array

def ReplaceElements(arr, n):

    # Nothing to do when array size is 1
    if (n <= 1):
        return

    # store current value of arr[0]
    # and update it
    prev = arr[0]
    arr[0] = arr[0] + arr[1]

    # Update rest of the array elements
    for i in range(1, n - 1):

        # Store current value of
        # next iteration
        curr = arr[i]

        # Update current value using
        # previews value
        arr[i] = prev + arr[i + 1]

        # Update previous value
        prev = curr

    # Update last array element separately
    arr[n - 1] = prev + arr[n - 1]

# Driver Code
if __name__ == "__main__":

    arr = [ 2, 3, 4, 5, 6 ]
    n = len(arr)

    ReplaceElements(arr, n)

    # Print the modified array
    for i in range(n):
        print (arr[i], end = " ")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to update every array element with
// sum of previous and next numbers in array
using System;
public class GFG {

    static void ReplaceElements(int []arr, int n) {
        // Nothing to do when array size is 1
        if (n <= 1) {
            return;
        }

        // store current value of arr[0] and update it
        int prev = arr[0];
        arr[0] = arr[0] + arr[1];

        // Update rest of the array elements
        for (int i = 1; i < n - 1; i++) {

            // Store current value of next iteration
            int curr = arr[i];

            // Update current value using previews value
            arr[i] = prev + arr[i + 1];

            // Update previous value
            prev = curr;
        }

        // Update last array element separately
        arr[n - 1] = prev + arr[n - 1];
    }

// Driver program
    public static void Main() {
        int []arr = {2, 3, 4, 5, 6};
        int n = arr.Length;

        ReplaceElements(arr, n);

        // Print the modified array
        for (int i = 0; i < n; i++) {
            Console.Write(arr[i] + " ");
        }
    }
}

// This code is contributed by Rajput-JI
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to update every array
// element with sum of previous and
// next numbers in array

function ReplaceElements($arr, $n)
{
    // Nothing to do when array
    // size is 1
    if ($n <= 1)
        return;

    // store current value of
    // arr[0] and update it
    $prev = $arr[0];
    $arr[0] = $arr[0] + $arr[1];

    // Update rest of the array elements
    for ($i = 1; $i < $n - 1; $i++)
    {

        // Store current value of
        // next iteration
        $curr = $arr[$i];

        // Update current value using
        // previews value
        $arr[$i] = $prev + $arr[$i + 1];

        // Update previous value
        $prev = $curr;
    }

    // Update last array element
    // separately
    $arr[$n - 1] = $prev + $arr[$n - 1];
    return $arr;
}

// Driver Code
$arr = array(2, 3, 4, 5, 6);
$n = sizeof($arr);

$arr1 = ReplaceElements($arr, $n);

// Print the modified array
for ($i = 0; $i < $n; $i++)
    echo $arr1[$i] . " ";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
    // Javascript program to update every array element with
    // sum of previous and next numbers in array

    function ReplaceElements(arr, n) {
        // Nothing to do when array size is 1
        if (n <= 1) {
            return;
        }

        // store current value of arr[0] and update it
        let prev = arr[0];
        arr[0] = arr[0] + arr[1];

        // Update rest of the array elements
        for (let i = 1; i < n - 1; i++) {

            // Store current value of next iteration
            let curr = arr[i];

            // Update current value using previews value
            arr[i] = prev + arr[i + 1];

            // Update previous value
            prev = curr;
        }

        // Update last array element separately
        arr[n - 1] = prev + arr[n - 1];
    }

    let arr = [2, 3, 4, 5, 6];
    let n = arr.length;

    ReplaceElements(arr, n);

    // Print the modified array
    for (let i = 0; i < n; i++) {
      document.write(arr[i] + " ");
    }

</script>
```

**Output:** 

```
5 6 8 10 11
```

**时间复杂度**–O(N)