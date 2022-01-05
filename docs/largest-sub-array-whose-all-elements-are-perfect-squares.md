# 所有元素都是完美正方形的最大子阵列

> 原文:[https://www . geeksforgeeks . org/最大子数组-其所有元素都是完美的正方形/](https://www.geeksforgeeks.org/largest-sub-array-whose-all-elements-are-perfect-squares/)

给定整数元素的数组![arr ](img/30cc397b6188b98ce45d51c03c5400b3.png "Rendered by QuickLaTeX.com")，任务是找到![arr ](img/30cc397b6188b98ce45d51c03c5400b3.png "Rendered by QuickLaTeX.com")的最大子数组的长度，使得子数组的所有元素都是完美的正方形。
**例:**

> **输入:** arr[] = {1，7，36，4，49，2，4}
> **输出:** 3
> 所有元素均为完美正方形的最大长度子数组为{36，4，49}
> **输入:** arr[] = {25，100，2，3，9，1}
> **输出:** 2
> 可能的子数组为{25，100 }【T11

**进场:**

*   [从左到右遍历数组](https://www.geeksforgeeks.org/loops-in-c-sharp/)。用 **0** 初始化一个**最大长度**和**当前长度**变量。
*   取一个整数和一个浮点变量，对于数组存储的每个元素，它都是这两个变量的平方根。
*   如果两个变量相等，即当前元素是一个完美的正方形，那么增加 **current_length** 变量并继续。否则，设置**电流 _ 长度= 0** 。
*   在每一步，将最大长度指定为**最大长度=最大(当前长度，最大长度)**。
*   最后打印**最大 _ 长度**的值。

以下是上述方法的实现:

## C++

```
// C++ program to find the length of the
// largest sub-array of an array every
// element of whose is a perfect square
#include <bits/stdc++.h>
using namespace std;

// function to return the length of the
// largest sub-array of an array every
// element of whose is a perfect square
int contiguousPerfectSquare(int arr[], int n)
{
    int a;
    float b;

    int current_length = 0;
    int max_length = 0;

    for (int i = 0; i < n; i++) {
        b = sqrt(arr[i]);
        a = b;

        // if both a and b are equal then
        // arr[i] is a perfect square
        if (a == b)
            current_length++;
        else
            current_length = 0;

        max_length = max(max_length, current_length);
    }
    return max_length;
}

// Driver code
int main()
{
    int arr[] = { 9, 75, 4, 64, 121, 25 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << contiguousPerfectSquare(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of the
// largest sub-array of an array every
// element of whose is a perfect square
import java.io.*;

class GFG {

// function to return the length of the
// largest sub-array of an array every
// element of whose is a perfect square
 static int contiguousPerfectSquare(int []arr, int n)
{
    int a;
    float b;

    int current_length = 0;
    int max_length = 0;

    for (int i = 0; i < n; i++) {
        b = (float)Math.sqrt(arr[i]);
        a = (int)b;

        // if both a and b are equal then
        // arr[i] is a perfect square
        if (a == b)
            current_length++;
        else
            current_length = 0;

        max_length = Math.max(max_length, current_length);
    }
    return max_length;
}

// Driver code

    public static void main (String[] args) {
            int arr[] = { 9, 75, 4, 64, 121, 25 };
    int n = arr.length;

    System.out.print(contiguousPerfectSquare(arr, n));
    }
}
// This code is contributed by inder_verma..
```

## 蟒蛇 3

```
# Python 3 program to find the length of
# the largest sub-array of an array every
# element of whose is a perfect square
from math import sqrt

# function to return the length of the
# largest sub-array of an array every
# element of whose is a perfect square
def contiguousPerfectSquare(arr, n):
    current_length = 0
    max_length = 0

    for i in range(0, n, 1):
        b = sqrt(arr[i])
        a = int(b)

        # if both a and b are equal then
        # arr[i] is a perfect square
        if (a == b):
            current_length += 1
        else:
            current_length = 0

        max_length = max(max_length,
                         current_length)

    return max_length

# Driver code
if __name__ == '__main__':
    arr = [9, 75, 4, 64, 121, 25]
    n = len(arr)

    print(contiguousPerfectSquare(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the length of the
// largest sub-array of an array every
// element of whose is a perfect square
using System;

class GFG {

// function to return the length of the
// largest sub-array of an array every
// element of whose is a perfect square
static int contiguousPerfectSquare(int []arr, int n)
{
    int a;
    float b;

    int current_length = 0;
    int max_length = 0;

    for (int i = 0; i < n; i++) {
        b = (float)Math.Sqrt(arr[i]);
        a = (int)b;

        // if both a and b are equal then
        // arr[i] is a perfect square
        if (a == b)
            current_length++;
        else
            current_length = 0;

        max_length = Math.Max(max_length, current_length);
    }
    return max_length;
}

// Driver code

    public static void Main () {
            int []arr = { 9, 75, 4, 64, 121, 25 };
    int n = arr.Length;

  Console.WriteLine(contiguousPerfectSquare(arr, n));
    }
}
// This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the length of the
// largest sub-array of an array every
// element of whose is a perfect square

// function to return the length of the
// largest sub-array of an array every
// element of whose is a perfect square
function contiguousPerfectSquare($arr, $n)
{
    $current_length = 0;
    $max_length = 0;

    for ($i = 0; $i < $n; $i++)
    {
        $b = (float)sqrt($arr[$i]);
        $a = (int)$b;

        // if both a and b are equal then
        // arr[i] is a perfect square
        if ($a == $b)
            $current_length = $current_length + 1;
        else
            $current_length = 0;

        $max_length = max($max_length,
                          $current_length);
    }
    return $max_length;
}

// Driver code
$arr = array(9, 75, 4, 64, 121, 25);
$n = sizeof($arr);

echo contiguousPerfectSquare($arr, $n);

// This code os contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to find the length of the
// largest sub-array of an array every
// element of whose is a perfect square

// function to return the length of the
// largest sub-array of an array every
// element of whose is a perfect square
function contiguousPerfectSquare(arr, n)
{
    var a;
    var b;

    var current_length = 0;
    var max_length = 0;

    for (var i = 0; i < n; i++) {
        b = (Math.sqrt(arr[i]));
        a = parseInt(b);

        // if both a and b are equal then
        // arr[i] is a perfect square
        if (a == b)
            current_length++;
        else
            current_length = 0;

        max_length = Math.max(max_length, current_length);
    }
    return max_length;
}

// Driver code
var arr = [9, 75, 4, 64, 121, 25 ];
var n = arr.length;
document.write( contiguousPerfectSquare(arr, n));

</script>
```

**Output:** 

```
4
```