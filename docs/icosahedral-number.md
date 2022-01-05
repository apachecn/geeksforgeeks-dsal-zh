# 二十面体数

> 原文:[https://www.geeksforgeeks.org/icosahedral-number/](https://www.geeksforgeeks.org/icosahedral-number/)

给定一个数 n，求第 n 个二十面体数。**二十面体数**是一类表示二十面体(有 20 个面的多面体)的比喻数。
前几个二十面体数字是 1，12，48，124，255，456，742，1128，1629……..

**示例:**

```
Input : 5
Output :255

Input :10
Output :2260
```

**二十面体数的第 n**项由下式给出:

上述思想的基本实现:

## C++

```
// Icosahedral number to find
// n-th term in C++
#include <bits/stdc++.h>
using namespace std;

// Function to find
// Icosahedral number
int icosahedralnum(int n)
{
    // Formula to calculate nth
    // Icosahedral number &
    // return it into main function.
    return (n * (5 * n * n - 5 * n + 2)) / 2;
}

// Driver Code
int main()
{
    int n = 7;

    cout << icosahedralnum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Icosahedral number to find
// n-th term in Java
import java.io.*;

class GFG {

    // Function to find
    // Icosahedral number
    static int icosahedralnum(int n)
    {
        // Formula to calculate nth
        // Icosahedral number &
        // return it into main function.

        return (n * (5 * n * n - 5 *
                            n + 2)) / 2;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 7;
        System.out.println(
                        icosahedralnum(n));
    }
}

// This code is contributed by aj_36.
```

## 蟒蛇 3

```
# Python 3 Program to find
# nth Icosahedral number

# Icosahedral number
# number function
def icosahedralnum(n) :

    # Formula to calculate nth
    # Icosahedral number
    # return it into main function.
    return (n * (5 * n * n -
                 5 * n + 2)) // 2

# Driver Code
if __name__ == '__main__' :

    n = 7
    print(icosahedralnum(n))

# This code is contributed aj_36
```

## C#

```
// Icosahedral number to
// find n-th term in C#
using System;

class GFG
{

    // Function to find
    // Icosahedral number
    static int icosahedralnum(int n)
    {
        // Formula to calculate
        // nth Icosahedral number
        // & return it into main
        // function.
        return (n * (5 * n * n -
                     5 * n + 2)) / 2;
    }

    // Driver Code
    static public void Main ()
    {
        int n = 7;
        Console.WriteLine(icosahedralnum(n));
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Icosahedral number to
// find n-th term in PHP

// Function to find
// Icosahedral number
function icosahedralnum($n)
{
    // Formula to calculate nth
    // Icosahedral number &
    // return it into main function.
    return ($n * (5 * $n * $n -
                  5 * $n + 2)) / 2;
}

// Driver Code
$n = 7;

echo icosahedralnum($n);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
    // Icosahedral number to
    // find n-th term in Javascript

    // Function to find
    // Icosahedral number
    function icosahedralnum(n)
    {
        // Formula to calculate
        // nth Icosahedral number
        // & return it into main
        // function.
        return (n * (5 * n * n - 5 * n + 2)) / 2;
    }

    let n = 7;
      document.write(icosahedralnum(n));

</script>
```

**输出:**

```
742
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)