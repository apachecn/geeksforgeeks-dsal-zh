# 在 1 到 N 的数组中向右旋转所有奇数，向左旋转所有偶数

> 原文:[https://www . geeksforgeeks . org/rotate-all-奇数-right-and-all-偶数-1 对 n 数组中的 left/](https://www.geeksforgeeks.org/rotate-all-odd-numbers-right-and-all-even-numbers-left-in-an-array-of-1-to-n/)

给定由范围**【1，N】**中的 **N** 个数字组成的排列数组 **A[]** ，任务是向左旋转排列的所有偶数，向右旋转排列的所有奇数，并打印更新的排列。
**注:** N 始终为偶数。
**示例:**

> **输入:** A = {1，2，3，4，5，6，7，8}
> **输出:** {7，4，1，6，3，8，5，2}
> **解释:**
> 偶数元素= {2，4，6，8}
> 奇数元素= {1，3，5，7}
> 偶数的左旋转= {4，6，8，2}
> 奇数的右旋转= {7
> **输入:** A = {1，2，3，4，5，6}
> **输出:** {5，4，1，6，3，2}

**进场:**

1.  很明显，奇数元素总是在偶数索引上，偶数元素总是在奇数索引上。
2.  为了做偶数的左旋转，我们只选择奇数索引。
3.  为了对奇数进行右旋转，我们只选择偶数索引。
4.  打印更新后的数组。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// function to left rotate
void left_rotate(int arr[])
{
    int last = arr[1];
    for (int i = 3; i < 6; i = i + 2)
    {
        arr[i - 2] = arr[i];
    }
    arr[6 - 1] = last;
}

// function to right rotate
void right_rotate(int arr[])
{
    int start = arr[6 - 2];
    for (int i = 6- 4; i >= 0; i = i - 2)
    {
        arr[i + 2] = arr[i];
    }
    arr[0] = start;
}

// Function to rotate the array
void rotate(int arr[])
{
    left_rotate(arr);
    right_rotate(arr);
    for (int i = 0; i < 6; i++)
    {
        cout << (arr[i]) << " ";
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6 };

    rotate(arr);
}

// This code is contributed by rock_cool
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;
import java.util.*;
import java.lang.*;

class GFG {

    // function to left rotate
    static void left_rotate(int[] arr)
    {
        int last = arr[1];
        for (int i = 3;
            i < arr.length;
            i = i + 2) {
            arr[i - 2] = arr[i];
        }
        arr[arr.length - 1] = last;
    }

    // function to right rotate
    static void right_rotate(int[] arr)
    {
        int start = arr[arr.length - 2];
        for (int i = arr.length - 4;
            i >= 0;
            i = i - 2) {
            arr[i + 2] = arr[i];
        }
        arr[0] = start;
    }

    // Function to rotate the array
    public static void rotate(int arr[])
    {
        left_rotate(arr);
        right_rotate(arr);
        for (int i = 0; i < arr.length; i++) {
            System.out.print(arr[i] + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5, 6 };

        rotate(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to left rotate
def left_rotate(arr):

    last = arr[1];
    for i in range(3, len(arr), 2):
        arr[i - 2] = arr[i]

    arr[len(arr) - 1] = last

# Function to right rotate
def right_rotate(arr):

    start = arr[len(arr) - 2]
    for i in range(len(arr) - 4, -1, -2):
        arr[i + 2] = arr[i]

    arr[0] = start

# Function to rotate the array
def rotate(arr):

    left_rotate(arr)
    right_rotate(arr)
    for i in range(len(arr)):
        print(arr[i], end = " ")

# Driver code
arr = [ 1, 2, 3, 4, 5, 6 ]

rotate(arr);

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to left rotate
static void left_rotate(int[] arr)
{
    int last = arr[1];
    for(int i = 3;
            i < arr.Length;
            i = i + 2)
    {
        arr[i - 2] = arr[i];
    }
    arr[arr.Length - 1] = last;
}

// Function to right rotate
static void right_rotate(int[] arr)
{
    int start = arr[arr.Length - 2];
    for(int i = arr.Length - 4;
            i >= 0; i = i - 2)
    {
        arr[i + 2] = arr[i];
    }
    arr[0] = start;
}

// Function to rotate the array
public static void rotate(int[] arr)
{
    left_rotate(arr);
    right_rotate(arr);

    for(int i = 0; i < arr.Length; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 2, 3, 4, 5, 6 };

    rotate(arr);
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

    // Javascript program to implement
    // the above approach

    // function to left rotate
    function left_rotate(arr)
    {
        let last = arr[1];
        for (let i = 3; i < 6; i = i + 2)
        {
            arr[i - 2] = arr[i];
        }
        arr[6 - 1] = last;
    }

    // function to right rotate
    function right_rotate(arr)
    {
        let start = arr[6 - 2];
        for (let i = 6- 4; i >= 0; i = i - 2)
        {
            arr[i + 2] = arr[i];
        }
        arr[0] = start;
    }

    // Function to rotate the array
    function rotate(arr)
    {
        left_rotate(arr);
        right_rotate(arr);
        for (let i = 0; i < 6; i++)
        {
            document.write(arr[i] + " ");
        }
    }

      let arr = [ 1, 2, 3, 4, 5, 6 ];

    rotate(arr);

</script>
```

**Output:**

```
5 4 1 6 3 2
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*