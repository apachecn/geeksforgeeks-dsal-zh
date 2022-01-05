# 用所有其他元素的按位异或替换数组的每个元素

> 原文:[https://www . geeksforgeeks . org/将数组中的每个元素替换为所有其他元素的按位异或/](https://www.geeksforgeeks.org/replace-every-element-of-the-array-with-bitwise-xor-of-all-other/)

给定一个整数数组。任务是用数组中所有其他元素的按位异或来替换每个元素。
**例:**

```
Input: arr[] = { 2, 3, 3, 5, 5 }
Output: 0 1 1 7 7
Bitwise Xor of 3, 3, 5, 5 = 0
Bitwise Xor of 2, 3, 5, 5 = 1
Bitwise Xor of 2, 3, 5, 5 = 1
Bitwise Xor of 2, 3, 3, 5 = 7
Bitwise Xor of 2, 3, 3, 5 = 7

Input : arr[] = { 1, 2, 3 }
Output : 1 2 3
```

**进场:**

1.  首先，对数组的所有元素进行按位异或运算，并将其存储在一个变量中。
2.  现在用 X 和那个元素的异或替换每个元素，因为异或同一个元素会抵消掉所有其他元素的异或。
3.  打印修改后的数组。

以下是上述方法的实现:

## C++

```
// C++ program to Replace every element
// by the bitwise xor of all other elements
#include <bits/stdc++.h>
using namespace std;

// Function to replace the elements
void ReplaceElements(int arr[], int n)
{
    int X = 0;

    // Calculate the xor of all the elements
    for (int i = 0; i < n; ++i) {
        X ^= arr[i];
    }

    // Replace every element by the
    // xor of all other elements
    for (int i = 0; i < n; ++i) {
        arr[i] = X ^ arr[i];
    }
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 3, 5, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    ReplaceElements(arr, n);

    // Print the modified array.
    for (int i = 0; i < n; ++i) {
        cout << arr[i] << " ";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to Replace every element
// by the bitwise xor of all other elements

import java.io.*;

class GFG {

// Function to replace the elements
static void ReplaceElements(int arr[], int n)
{
    int X = 0;

    // Calculate the xor of all the elements
    for (int i = 0; i < n; ++i) {
        X ^= arr[i];
    }

    // Replace every element by the
    // xor of all other elements
    for (int i = 0; i < n; ++i) {
        arr[i] = X ^ arr[i];
    }
}

// Driver code
 public static void main (String[] args) {

    int arr[] = { 2, 3, 3, 5, 5 };
    int n = arr.length;

    ReplaceElements(arr, n);

    // Print the modified array.
    for (int i = 0; i < n; ++i) {
        System.out.print(arr[i] +" ");

        }
    }
}
```

## 蟒蛇 3

```
# Python 3 program to Replace every element
# by the bitwise xor of all other elements

# Function to replace the elements
def ReplaceElements(arr, n):

    X = 0

    # Calculate the xor of all the elements
    for i in range(n):
        X ^= arr[i]

    # Replace every element by the
    # xor of all other elements
    for i in range(n):
        arr[i] = X ^ arr[i]

# Driver code
if __name__ == "__main__":
    arr = [ 2, 3, 3, 5, 5 ]
    n = len(arr)

    ReplaceElements(arr, n)

    # Print the modified array.
    for i in range(n):
        print(arr[i], end = " ")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C#  program to Replace every element
// by the bitwise xor of all other elements
using System;

public class GFG{
    // Function to replace the elements
static void ReplaceElements(int []arr, int n)
{
    int X = 0;

    // Calculate the xor of all the elements
    for (int i = 0; i < n; ++i) {
        X ^= arr[i];
    }

    // Replace every element by the
    // xor of all other elements
    for (int i = 0; i < n; ++i) {
        arr[i] = X ^ arr[i];
    }
}

// Driver code

    static public void Main (){

    int []arr = { 2, 3, 3, 5, 5 };
    int n = arr.Length;

    ReplaceElements(arr, n);

    // Print the modified array.
    for (int i = 0; i < n; ++i) {
        Console.Write(arr[i] +" ");

        }
    }
//This code is contributed by ajit   
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Replace every element
// by the bitwise xor of all other elements

// Function to replace the elements
function ReplaceElements($arr, $n)
{
    $X = 0;

    // Calculate the xor of all the elements
    for ($i = 0; $i < $n; ++$i)
    {
        $X ^= $arr[$i];
    }

    // Replace every element by the
    // xor of all other elements
    for ($i = 0; $i < $n; ++$i)
    {
        $arr[$i] = $X ^ $arr[$i];
    }
    return $arr;
}

// Driver code
$arr = array( 2, 3, 3, 5, 5 );
$n = sizeof($arr);

$arr1 = ReplaceElements($arr, $n);

// Print the modified array.
for ($i = 0; $i < $n; ++$i)
{
    echo($arr1[$i] . " ");

}

// This code is contributed
// by Mukul singh
?>
```

## java 描述语言

```
<script>

// Javascript program to Replace every element
// by the bitwise xor of all other elements

// Function to replace the elements
function ReplaceElements(arr, n)
{
    let X = 0;

    // Calculate the xor of all the elements
    for (let i = 0; i < n; ++i) {
        X ^= arr[i];
    }

    // Replace every element by the
    // xor of all other elements
    for (let i = 0; i < n; ++i) {
        arr[i] = X ^ arr[i];
    }
}

// Driver code
    let arr = [ 2, 3, 3, 5, 5 ];
    let n = arr.length;

    ReplaceElements(arr, n);

    // Print the modified array.
    for (let i = 0; i < n; ++i) {
        document.write(arr[i] + " ");
    }

</script>
```

**Output:** 

```
0 1 1 7 7
```

**时间复杂度** : O(N)