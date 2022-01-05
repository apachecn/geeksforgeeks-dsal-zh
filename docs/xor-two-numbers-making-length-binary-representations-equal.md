# 两个数的二进制表示长度相等后的异或运算

> 原文:[https://www . geesforgeks . org/xor-二进制-数字-制作-长度-二进制-表示-相等/](https://www.geeksforgeeks.org/xor-two-numbers-making-length-binary-representations-equal/)

给定两个数字，比如 a 和 b。通过在较小的二进制表示中添加尾随零，使二进制表示的长度相等后，打印它们的异或。
**例:**

```
Input : a = 13, b = 5 
Output : 7
Explanation : Binary representation of 13 is 1101 and 
of 5 is 101\. As the length of "101" is smaller,
so add a '0' to it making it "1010', to make 
the length of binary representations equal. 
XOR of 1010 and 1101 gives 0111 which is 7.

Input : a = 7, b = 5 
Output : 2
Explanation : Since the length of binary representations
of 7 i.e, 111 and 5 i.e, 101 are same, hence simply
print XOR of a and b.
```

**方法:**计算 a 和 b 中较小数字的二进制表示的位数，如果较小数字(比如 a)的位数超过较大数字(比如 b)的位数，则向较小数字左移超出的位数，即 a = a < <(超出的位数)。应用左移位后，尾随零将被添加到较小数字的二进制表示的末尾，以使两个数字的二进制表示中的位数相等。对两个二进制表示进行异或运算，得到最终结果。
以下是上述方法的实施:

## C++

```
// C++ implementation to return
// XOR of two numbers after making
// length of their binary representation same
#include <bits/stdc++.h>
using namespace std;

// function to count the number
// of bits in binary representation
// of an integer
int count(int n)
{
    // initialize count
    int c = 0;

    // count till n is non zero
    while (n)
    {
        c++;

        // right shift by 1
        // i.e, divide by 2
        n = n>>1;
    }
    return c;
}

// function to calculate the xor of
// two numbers by adding trailing
// zeros to the number having less number
// of bits in its binary representation.
int XOR(int a, int b)
{
    // stores the minimum and maximum
    int c = min(a,b);
    int d = max(a,b);

    // left shift if the number of bits
    // are less in binary representation
    if (count(c) < count(d))
       c = c << ( count(d) - count(c) );

    return (c^d);
}

// driver code to check the above function
int main()
{  
    int a = 13, b = 5;
    cout << XOR(a,b);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to return
// XOR of two numbers after making
// length of their binary representation same
import java.io.*;

class GFG {

    // function to count the number
    // of bits in binary representation
    // of an integer
    static int count(int n)
    {
        // initialize count
        int c = 0;

        // count till n is non zero
        while (n != 0)
        {
            c++;

            // right shift by 1
            // i.e, divide by 2
            n = n >> 1;
        }
        return c;
    }

    // function to calculate the xor of
    // two numbers by adding trailing
    // zeros to the number having less number
    // of bits in its binary representation.
    static int XOR(int a, int b)
    {
        // stores the minimum and maximum
        int c = Math.min(a, b);
        int d = Math.max(a, b);

        // left shift if the number of bits
        // are less in binary representation
        if (count(c) < count(d))
        c = c << ( count(d) - count(c) );

        return (c ^ d);
    }

    // driver code to check the above function
    public static void main(String args[])
    {
        int a = 13, b = 5;
        System.out.println(XOR(a, b));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python 3 implementation to return XOR
# of two numbers after making length
# of their binary representation same

# Function to count the number of bits
# in binary representation of an integer
def count(n) :

    # initialize count
    c = 0

    # count till n is non zero
    while (n != 0) :
        c += 1

        # right shift by 1
        # i.e, divide by 2
        n = n >> 1

    return c

# Function to calculate the xor of
# two numbers by adding trailing
# zeros to the number having less number
# of bits in its binary representation.
def XOR(a, b) :

    # stores the minimum and maximum
    c = min(a, b)
    d = max(a, b)

    # left shift if the number of bits
    # are less in binary representation
    if (count(c) < count(d)) :
        c = c << ( count(d) - count(c) )

    return (c^d)

# Driver Code
a = 13; b = 5
print(XOR(a, b))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# implementation to return XOR of two
// numbers after making length of their
// binary representation same
using System;

class GFG {

    // function to count the number
    // of bits in binary representation
    // of an integer
    static int count(int n)
    {

        // initialize count
        int c = 0;

        // count till n is non zero
        while (n != 0)
        {

            c++;

            // right shift by 1
            // i.e, divide by 2
            n = n >> 1;
        }

        return c;
    }

    // function to calculate the xor of
    // two numbers by adding trailing
    // zeros to the number having less number
    // of bits in its binary representation.
    static int XOR(int a, int b)
    {

        // stores the minimum and maximum
        int c = Math.Min(a, b);
        int d = Math.Max(a, b);

        // left shift if the number of bits
        // are less in binary representation
        if (count(c) < count(d))
        c = c << ( count(d) - count(c) );

        return (c ^ d);
    }

    // driver code to check the above function
    public static void Main()
    {
        int a = 13, b = 5;

        Console.WriteLine(XOR(a, b));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php implementation to return XOR
// of two numbers after making
// length of their binary
// representation same

// function to count the number
// of bits in binary representation
// of an integer
function count1($n)
{

    // initialize count
    $c = 0;

    // count till n is
    // non zero
    while ($n)
    {
        $c++;

        // right shift by 1
        // i.e, divide by 2
        $n = $n>>1;
    }
    return $c;
}

// function to calculate the xor of
// two numbers by adding trailing
// zeros to the number having less number
// of bits in its binary representation.
function XOR1($a, $b)
{

    // stores the minimum
    // and maximum
    $c = min($a,$b);
    $d = max($a,$b);

    // left shift if the number of bits
    // are less in binary representation
    if (count1($c) < count1($d))
    $c = $c << ( count1($d) - count1($c) );

    return ($c^$d);
}

    // Driver Code
    $a = 13;
    $b = 5;
    echo XOR1($a, $b);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to return
// XOR of two numbers after making
// length of their binary representation same

    // function to count the number
    // of bits in binary representation
    // of an integer
    function count(n)
    {
        // initialize count
        let c = 0;

        // count till n is non zero
        while (n != 0)
        {
            c++;

            // right shift by 1
            // i.e, divide by 2
            n = n >> 1;
        }
        return c;
    }

    // function to calculate the xor of
    // two numbers by adding trailing
    // zeros to the number having less number
    // of bits in its binary representation.
    function XOR(a, b)
    {
        // stores the minimum and maximum
        let c = Math.min(a, b);
        let d = Math.max(a, b);

        // left shift if the number of bits
        // are less in binary representation
        if (count(c) < count(d))
        c = c << ( count(d) - count(c) );

        return (c ^ d);
    }

// Driver code

        let a = 13, b = 5;
        document.write(XOR(a, b));

</script>
```

**输出:**

```
7 
```