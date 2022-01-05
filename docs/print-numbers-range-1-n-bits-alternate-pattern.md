# 打印 1 到 n 范围内的数字，并以交替模式排列位

> 原文:[https://www . geesforgeks . org/print-numbers-range-1-n-bit-alternate-pattern/](https://www.geeksforgeeks.org/print-numbers-range-1-n-bits-alternate-pattern/)

给定正整数 **n** 。问题是打印 1 到 n 范围内的数字，这些数字具有交替模式的位。这里，交替模式意味着数字中的设置位和未设置位以交替顺序出现。例如- 5 具有交替模式，即 101。
示例:

```
Input : n = 10
Output : 1 2 5 10

Input : n = 50
Output : 1 2 5 10 21 42
```

**方法 1(天真方法):**生成 1 到 n 范围内的所有数字，对于每个生成的数字[检查它是否有交替模式的位](https://www.geeksforgeeks.org/check-number-bits-alternate-pattern-set-2-o1-approach/)。时间复杂度为 0(n)。
**方法 2(有效方法):**算法:

```
printNumHavingAltBitPatrn(n)
    Initialize curr_num = 1
    print curr_num    
    while (1)
        curr_num <<= 1
    if n < curr_num then
        break
    print curr_num
    curr_num = ((curr_num) << 1) ^ 1    
    if n < curr_num then
        break
    print curr_num    
```

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to print numbers in the range
// 1 to n having bits in alternate pattern
#include <bits/stdc++.h>

using namespace std;

// function to print numbers in the range 1 to n
// having bits in alternate pattern
void printNumHavingAltBitPatrn(int n)
{
    // first number having bits in alternate pattern
    int curr_num = 1;

    // display
    cout << curr_num << " ";

    // loop until n < curr_num
    while (1) {

        // generate next number having alternate
        // bit pattern
        curr_num <<= 1;

        // if true then break
        if (n < curr_num)
            break;

        // display
        cout << curr_num << " ";

        // generate next number having alternate
        // bit pattern
        curr_num = ((curr_num) << 1) ^ 1;

        // if true then break
        if (n < curr_num)
            break;

        // display
        cout << curr_num << " ";
    }
}

// Driver program to test above
int main()
{
    int n = 50;
    printNumHavingAltBitPatrn(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print numbers in the range
// 1 to n having bits in alternate pattern

import java.io.*;
import java.util.*;

class GFG
{
    public static void printNumHavingAltBitPatrn(int n)
    {
        // first number having bits in alternate pattern
        int curr_num = 1, i = 1;

        // display
        System.out.print(curr_num + " ");

        // loop until n < curr_num
        while (i!=0)
        {
            i++;
            // generate next number having alternate
            // bit pattern
            curr_num <<= 1;

            // if true then break
            if (n < curr_num)
                break;

            // display
            System.out.print(curr_num + " ");

            // generate next number having alternate
            // bit pattern
            curr_num = ((curr_num) << 1) ^ 1;

            // if true then break
            if (n < curr_num)
                break;

            // display
            System.out.print(curr_num + " ");
        }
    }
    public static void main (String[] args)
    {
        int n = 50;
        printNumHavingAltBitPatrn(n);
    }
}

// Code Contributed by Mohit Gupta_OMG <(0_o)>
```

## 蟒蛇 3

```
# Python3 program for count total
# zero in product of array

# function to print numbers in the range
# 1 to nhaving bits in alternate pattern
def printNumHavingAltBitPatrn(n):

    # first number having bits in
    # alternate pattern
    curr_num = 1

    # display
    print (curr_num)

    # loop until n < curr_num
    while (1) :

        # generate next number having
        # alternate bit pattern
        curr_num = curr_num << 1;

        # if true then break
        if (n < curr_num):
            break;

        # display
        print( curr_num )

        # generate next number having
        # alternate bit pattern
        curr_num = ((curr_num) << 1) ^ 1;

        # if true then break
        if (n < curr_num):
            break

        # display
        print( curr_num )

# Driven code
n = 50
printNumHavingAltBitPatrn(n)

# This code is contributed by "rishabh_jain".
```

## C#

```
// C# implementation to print numbers in the range
// 1 to n having bits in alternate pattern
using System;

class GFG {

    // function to print numbers in the range 1 to n
    // having bits in alternate pattern
    public static void printNumHavingAltBitPatrn(int n)
    {

        // first number having bits in alternate pattern
        int curr_num = 1, i = 1;

        // display
        Console.Write(curr_num + " ");

        // loop until n < curr_num
        while (i!=0)
        {

            // generate next number having alternate
            // bit pattern
            curr_num <<= 1;

            // if true then break
            if (n < curr_num)
                break;

            // display
            Console.Write(curr_num + " ");

            // generate next number having alternate
            // bit pattern
            curr_num = ((curr_num) << 1) ^ 1;

            // if true then break
            if (n < curr_num)
                break;

            // display
            Console.Write(curr_num + " ");
        }
    }

    // Driver code
    public static void Main ()
    {
        int n = 50;

        printNumHavingAltBitPatrn(n);
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php implementation to print
// numbers in the range
// 1 to n having bits in
// alternate pattern

// function to print numbers
// in the range 1 to n
// having bits in alternate
// pattern
function printNumHavingAltBitPatrn($n)
{

    // first number having bits
    // in alternate pattern
    $curr_num = 1;

    // display
    echo $curr_num." ";

    // loop until n < curr_num
    while (1)
    {

        // generate next number
        // having alternate
        // bit pattern
        $curr_num <<= 1;

        // if true then break
        if ($n < $curr_num)
            break;

        // display
        echo $curr_num." ";

        // generate next number
        // having alternate
        // bit pattern
        $curr_num = (($curr_num) << 1) ^ 1;

        // if true then break
        if ($n < $curr_num)
            break;

        // display
        echo $curr_num." ";
    }
}

    // Driver code
    $n = 50;
    printNumHavingAltBitPatrn($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation to print numbers in the range
// 1 to n having bits in alternate pattern

// function to print numbers in the range 1 to n
// having bits in alternate pattern
function printNumHavingAltBitPatrn(n)
{
    // first number having bits in alternate pattern
    var curr_num = 1;

    // display
    document.write(curr_num + " ");

    // loop until n < curr_num
    while (true) {

        // generate next number having alternate
        // bit pattern
        curr_num <<= 1;

        // if true then break
        if (n < curr_num)
            break;

        // display
        document.write(curr_num + " ");

        // generate next number having alternate
        // bit pattern
        curr_num = ((curr_num) << 1) ^ 1;

        // if true then break
        if (n < curr_num)
            break;

        // display
        document.write(curr_num + " ");
    }
}

// Driver program to test above
var n = 50;
printNumHavingAltBitPatrn(n);

</script>
```

**输出:**

```
1 2 5 10 21 42
```