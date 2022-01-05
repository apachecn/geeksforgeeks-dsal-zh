# 居中七边形数

> 原文:[https://www.geeksforgeeks.org/centered-heptagonal-number/](https://www.geeksforgeeks.org/centered-heptagonal-number/)

给定一个数字 **n** ，任务是找到第 n 个<sup>中心七边形数。
居中七边形数是表示一个七边形的居中图形数，该七边形以点为中心，所有其他点以七边形形式环绕。N <sup>第</sup>个居中的七边数可用公式**(7n<sup>2</sup>–7n+2)/2**计算。
**示例:**</sup>

```
Input : n = 2
Output : 8

Input : n = 7
Output : 148
```

图示请参考[本](https://en.wikipedia.org/wiki/Centered_heptagonal_number#/media/File:Centered_heptagonal_number.svg)图。

下面是实现:

## C++

```
// CPP program to find n-th
// Centered heptagonal number
#include <bits/stdc++.h>

using namespace std;

// Function to find Centered
// heptagonal number
int centered_heptagonal_num(long int n)
{
    // Formula to calculate nth
    // Centered heptagonal number
    return (7 * n * n - 7 * n + 2) / 2;
}

// Driver Code
int main()
{
    long int n = 5;
    cout << n << "th Centered heptagonal number : ";
    cout << centered_heptagonal_num(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find n-th Centered
// heptagonal number
import java.io.*;

class GFG {

    // Function to find Centered heptagonal
    // number
    static long centered_heptagonal_num(long n)
    {

        // Formula to calculate nth
        // Centered heptagonal number
        return (7 * n * n - 7 * n + 2) / 2;
    }

    // Driver Code
    public static void main (String[] args)
    {
        long n = 5;
        System.out.println( n + "th Centered "
                      + "heptagonal number : "
                + centered_heptagonal_num(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python program to find nth
# Centered heptagonal number

# Function to find Centered
# heptagonal number
def centered_heptagonal_num(n):

    # Formula to calculate nth
    # Centered heptagonal number
    return (7 * n * n - 7 * n + 2) // 2

# Driver Code
n = 5
print("%sth Centered heptagonal number : " %n,
                    centered_heptagonal_num(n))
```

## C#

```
//C# program to find n-th Centered
// heptagonal number
using System;

class GFG {

    // Function to find Centered heptagonal
    // number
    static long centered_heptagonal_num(long n)
    {

        // Formula to calculate nth
        // Centered heptagonal number
        return (7 * n * n - 7 * n + 2) / 2;
    }

    // Driver Code
    public static void Main ()
    {
        long n = 5;
        Console.WriteLine( n + "th Centered "
                    + "heptagonal number : "
                + centered_heptagonal_num(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find n-th
// Centered heptagonal number

// Function to find Centered
// heptagonal number
function centered_heptagonal_num($n)
{
    // Formula to calculate nth
    // Centered heptagonal number
    return (7 * $n * $n - 7 *
                $n + 2) / 2;
}

// Driver Code
$n = 5;
echo $n ,"th Centered heptagonal number : ";
echo centered_heptagonal_num($n);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
// Javascript program to find n-th
// Centered heptagonal number

// Function to find Centered
// heptagonal number
function centered_heptagonal_num(n)
{
    // Formula to calculate nth
    // Centered heptagonal number
    return parseInt((7 * n * n - 7 * n + 2) / 2);
}

// Driver Code
let n = 5;
document.write(n + "th Centered heptagonal number : ");
document.write(centered_heptagonal_num(n));

// This code is contributed by rishavmahato348.
</script>
```

**输出:**

```
5th Centered heptagonal number : 71
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)