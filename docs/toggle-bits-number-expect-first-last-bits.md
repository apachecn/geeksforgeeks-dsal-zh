# 切换除第一位和最后一位以外的数字位

> 原文:[https://www . geesforgeks . org/toggle-bits-number-expect-first-last-bits/](https://www.geeksforgeeks.org/toggle-bits-number-expect-first-last-bits/)

给定一个数字，任务是切换除第一位和最后一位之外的数字位。
示例:

```
Input : 10
Output : 12
Binary representation:- 1 0 1 0
After toggling first and last : 1 1 0 0

Input : 9
Output : 15
Binary representation : 1 0 0 1
After toggling first and last : 1 1 1 1
```

先决条件:[找到一个数的最高有效集合位](https://www.geeksforgeeks.org/find-significant-set-bit-number/)
1)生成一个包含中间位的数作为集合。我们需要将所有中间位更改为 1，并将边角位保留为 0。
2)答案是生成数与原数的异或。请注意，1 与数字的异或会切换数字。

## C++

```
// C++ Program to toggle bits
// except first and last bit
#include<iostream>
using namespace std;

// return set middle bits
int setmiddlebits(int n)
{

    // set all bit
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // return middle set bits
    // shift by 1 and xor with 1
    return (n >> 1) ^ 1;
}

int togglemiddlebits(int n)
{

    // if number is 1 then
    // simply return
    if (n == 1)
        return 1;

    // xor with
    // middle bits
    return n ^ setmiddlebits(n);
}

// Driver Code
int main()
{

    // Given number
    int n = 9;

    // print toggle bits
    cout<<togglemiddlebits(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for toggle bits
// expect first and last bit
import java.io.*;

class GFG {

    // return set middle bits
    static int setmiddlebits(int n)
    {

        // set all bit
        n |= n >> 1;
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        // return middle set bits
        // shift by 1 and xor with 1
        return (n >> 1) ^ 1;
    }

    static int togglemiddlebits(int n)
    {
        // if number is 1 then
        // simply return
        if (n == 1)
            return 1;

        // XOR with middle bits
        return n ^ setmiddlebits(n);
    }

    // Driver Code
    public static void main (String[] args)
    {

        // Given number
        int n = 9;

        // print toggle bits
        System.out.println(togglemiddlebits(n));
    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python3 program for toggle bits
# expect first and last bit

# return set middle bits
def setmiddlebits(n):

    # set all bit
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    # return middle set bits
    # shift by 1 and xor with 1
    return (n >> 1) ^ 1

def togglemiddlebits(n):

    # if number is 1 then simply return
    if (n == 1):
        return 1

    # xor with middle bits
    return n ^ setmiddlebits(n)

# Driver code
n = 9
print(togglemiddlebits(n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program for toggle bits
// expect first and last bit
using System;

class GFG {

    // return set middle bits
    static int setmiddlebits(int n)
    {

        // set all bit
        n |= n >> 1;
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        // return middle set bits
        // shift by 1 and xor with 1
        return (n >> 1) ^ 1;
    }

    static int togglemiddlebits(int n)
    {

        // if number is 1 then
        // simply return
        if (n == 1)
            return 1;

        // XOR with middle bits
        return n ^ setmiddlebits(n);
    }

    // Driver Code
    public static void Main ()
    {

        // Given number
        int n = 9;

        // print toggle bits
        Console.WriteLine(togglemiddlebits(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php Program to toggle bits
// except first and last bit

// return set middle bits
function setmiddlebits($n)
{

    // set all bit
    $n |= $n >> 1;
    $n |= $n >> 2;
    $n |= $n >> 4;
    $n |= $n >> 8;
    $n |= $n >> 16;

    // return middle set bits
    // shift by 1 and xor with 1
    return ($n >> 1) ^ 1;
}

function togglemiddlebits($n)
{

    // if number is 1 then
    // simply return
    if ($n == 1)
        return 1;

    // xor with
    // middle bits
    return $n ^ setmiddlebits($n);
}

    // Driver Code
    $n = 9;

    // print toggle bits
    echo togglemiddlebits($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript Program to toggle bits
// except first and last bit

// return set middle bits
function setmiddlebits(n)
{

    // set all bit
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // return middle set bits
    // shift by 1 and xor with 1
    return (n >> 1) ^ 1;
}

function togglemiddlebits(n)
{

    // if number is 1 then
    // simply return
    if (n == 1)
        return 1;

    // xor with
    // middle bits
    return n ^ setmiddlebits(n);
}

// Driver Code

// Given number
var n = 9;
// print toggle bits
document.write(togglemiddlebits(n));

</script>
```

时间复杂度:- O(1)
**输出:**

```
15
```