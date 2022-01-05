# 不使用 GCD 查找 2 个数字的 LCM 的程序

> 原文:[https://www . geesforgeks . org/program-to-find-LCM-of-2-numbers-not-use-gcd/](https://www.geeksforgeeks.org/program-to-find-lcm-of-2-numbers-without-using-gcd/)

使用 GCD 查找 LCM 在这里[解释](https://www.geeksforgeeks.org/c-program-find-lcm-two-numbers/)但是这里的任务是在不先计算 GCD 的情况下查找 LCM。
**例:**

```
Input: 7, 5
Output: 35

Input: 2, 6
Output: 6
```

方法是从 2 个数字中最大的一个开始，不断递增最大的数字，直到较小的数字完美地除以结果。

## C++

```
// C++ program to find LCM of 2 numbers
// without using GCD
#include <bits/stdc++.h>
using namespace std;

// Function to return LCM of two numbers
int findLCM(int a, int b)
{
    int lar = max(a, b);
    int small = min(a, b);
    for (int i = lar; ; i += lar) {
        if (i % small == 0)
            return i;
    }
}

// Driver program to test above function
int main()
{
    int a = 5, b = 7;
    cout << "LCM of " << a << " and "
         << b << " is " << findLCM(a, b);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find LCM of 2 numbers
// without using GCD
import java.io.*;
import java.lang.*;

class GfG {

    // Function to return LCM of two numbers
    public static int findLCM(int a, int b)
    {
        int lar = Math.max(a, b);
        int small = Math.min(a, b);
        for (int i = lar; ; i += lar) {
            if (i % small == 0)
                return i;
        }
    }

    // Driver program to test above function
    public static void main(String [] argc)
    {
        int a = 5, b = 7;
        System.out.println( "LCM of " + a + " and "
            + b + " is " + findLCM(a, b));

    }
}

// This dose is contributed by Sagar Shukla.
```

## 蟒蛇 3

```
# Python 3 program to find
# LCM of 2 numbers without
# using GCD
import sys

# Function to return
# LCM of two numbers
def findLCM(a, b):

    lar = max(a, b)
    small = min(a, b)
    i = lar
    while(1) :
        if (i % small == 0):
            return i
        i += lar

# Driver Code
a = 5
b = 7
print("LCM of " , a , " and ",
                  b , " is " ,
      findLCM(a, b), sep = "")

# This code is contributed
# by Smitha
```

## C#

```
// C# program to find
// LCM of 2 numbers
// without using GCD
using System;

class GfG
{

    // Function to return
    // LCM of two numbers
    public static int findLCM(int a,
                              int b)
    {
        int lar = Math.Max(a, b);
        int small = Math.Min(a, b);
        for (int i = lar; ; i += lar)
        {
            if (i % small == 0)
                return i;
        }
    }

    // Driver Code
    public static void Main()
    {
        int a = 5, b = 7;
        Console.WriteLine("LCM of " + a +
                            " and " + b +
                                 " is " +
                          findLCM(a, b));

    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// LCM of 2 numbers
// without using GCD

// Function to return
// LCM of two numbers
function findLCM($a, $b)
{
    $lar = max($a, $b);
    $small = min($a, $b);
    for ($i = $lar; ; $i += $lar)
    {
        if ($i % $small == 0)
            return $i;
    }
}

// Driver Code
$a = 5;
$b = 7;
echo "LCM of " , $a , " and ",
                 $b , " is " ,
                 findLCM($a, $b);

// This code is contributed
// by Smitha
?>
```

## java 描述语言

```
<script>
// javascript program to find LCM of 2 numbers
// without using GCD

    // Function to return LCM of two numbers
    function findLCM(a , b) {
        var lar = Math.max(a, b);
        var small = Math.min(a, b);
        for (i = lar;; i += lar) {
            if (i % small == 0)
                return i;
        }
    }

    // Driver program to test above function
    var a = 5, b = 7;
        document.write("LCM of " + a + " and " + b + " is " + findLCM(a, b));

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
LCM of 5 and 7 is 35
```