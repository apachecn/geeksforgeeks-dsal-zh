# 通过操作位

将数字增加 1

> 原文:[https://www . geesforgeks . org/increment-number-one-operating-bits/](https://www.geeksforgeeks.org/increment-number-one-manipulating-bits/)

给定一个非负整数 **n** 。问题是通过操纵 **n** 的位将 **n** 增加 1。
**举例:**

```
Input : 6
Output : 7

Input : 15
Output : 16
```

**进场:**以下为步骤:

1.  [获取 **n** 最右侧未置位位](https://www.geeksforgeeks.org/get-position-rightmost-unset-bit/)的位置。让这个位置成为 **k** 。
2.  [设置 n 的第 k 位](https://www.geeksforgeeks.org/set-k-th-bit-given-number/)。
3.  [切换 **n** 的最后 k-1 位](https://www.geeksforgeeks.org/toggle-last-m-bits/)。
4.  最后，返回 **n** 。

## C++

```
// C++ implementation to increment a number
// by one by manipulating the bits
#include <bits/stdc++.h>
using namespace std;

// function to find the position
// of rightmost set bit
int getPosOfRightmostSetBit(int n)
{
    return log2(n & -n);
}

// function to toggle the last m bits
unsigned int toggleLastKBits(unsigned int n,
                             unsigned int k)
{
    // calculating a number 'num' having 'm' bits
    // and all are set
    unsigned int num = (1 << k) - 1;

    // toggle the last m bits and return the number
    return (n ^ num);
}

// function to increment a number by one
// by manipulating the bits
unsigned int incrementByOne(unsigned int n)
{
    // get position of rightmost unset bit
    // if all bits of 'n' are set, then the
    // bit left to the MSB is the rightmost
    // unset bit
    int k = getPosOfRightmostSetBit(~n);

    // kth bit of n is being set by this operation
    n = ((1 << k) | n);

    // from the right toggle all the bits before the
    // k-th bit
    if (k != 0)
        n = toggleLastKBits(n, k);

    // required number
    return n;
}

// Driver program to test above
int main()
{
    unsigned int n = 15;
    cout << incrementByOne(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to increment a number
// by one by manipulating the bits
import java.io.*;
import java.util.*;

class GFG {

    // function to find the position
    // of rightmost set bit
    static int getPosOfRightmostSetBit(int n)
    {
        return (int)(Math.log(n & -n) / Math.log(2));
    }

    // function to toggle the last m bits
    static int toggleLastKBits( int n, int k)
    {
        // calculating a number 'num' having
        // 'm' bits and all are set
        int num = (1 << k) - 1;

        // toggle the last m bits and return
        // the number
        return (n ^ num);
    }

    // function to increment a number by one
    // by manipulating the bits
    static int incrementByOne( int n)
    {
        // get position of rightmost unset bit
        // if all bits of 'n' are set, then the
        // bit left to the MSB is the rightmost
        // unset bit
        int k = getPosOfRightmostSetBit(~n);

        // kth bit of n is being set
        // by this operation
        n = ((1 << k) | n);

        // from the right toggle all
        // the bits before the k-th bit
        if (k != 0)
            n = toggleLastKBits(n, k);

        // required number
        return n;

    }

    // Driver Program   
    public static void main (String[] args)
    {
        int n = 15;
        System.out.println(incrementByOne(n));

    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# python 3 implementation
# to increment a number
# by one by manipulating
# the bits
import math

# function to find the
# position of rightmost
# set bit
def getPosOfRightmostSetBit(n) :
    return math.log2(n & -n)

# function to toggle the last m bits
def toggleLastKBits(n, k) :
    # calculating a number 
    # 'num' having 'm' bits
    # and all are set
    num = (1 << (int)(k)) - 1

    # toggle the last m bits and
    # return the number
    return (n ^ num)

# function to increment
# a number by one by
# manipulating the bits
def incrementByOne(n) :

    # get position of rightmost
    # unset bit if all bits of
    # 'n' are set, then the bit
    # left to the MSB is the
    # rightmost unset bit
    k = getPosOfRightmostSetBit(~n)

    # kth bit of n is being
    # set by this operation
    n = ((1 << (int)(k)) | n)

    # from the right toggle
    # all the bits before the
    # k-th bit
    if (k != 0) :
        n = toggleLastKBits(n, k)

    # required number
    return n

# Driver program
n = 15
print(incrementByOne(n))

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# implementation to increment a number
// by one by manipulating the bits
using System;

class GFG {

    // function to find the position
    // of rightmost set bit
    static int getPosOfRightmostSetBit(int n)
    {
        return (int)(Math.Log(n & -n) / Math.Log(2));
    }

    // function to toggle the last m bits
    static int toggleLastKBits( int n, int k)
    {

        // calculating a number 'num' having
        // 'm' bits and all are set
        int num = (1 << k) - 1;

        // toggle the last m bits and return
        // the number
        return (n ^ num);
    }

    // function to increment a number by one
    // by manipulating the bits
    static int incrementByOne( int n)
    {

        // get position of rightmost unset bit
        // if all bits of 'n' are set, then the
        // bit left to the MSB is the rightmost
        // unset bit
        int k = getPosOfRightmostSetBit(~n);

        // kth bit of n is being set
        // by this operation
        n = ((1 << k) | n);

        // from the right toggle all
        // the bits before the k-th bit
        if (k != 0)
            n = toggleLastKBits(n, k);

        // required number
        return n;

    }

    // Driver Program
    public static void Main ()
    {
        int n = 15;

        Console.WriteLine(incrementByOne(n));

    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to increment a number
// by one by manipulating the bits

// function to find the position
// of rightmost set bit
function getPosOfRightmostSetBit($n)
{
    $t = $n & -$n;
    return log($t, 2);
}

// function to toggle the last m bits
function toggleLastKBits($n, $k)
{
    // calculating a number 'num'
    // having 'm' bits and all are set
    $num = (1 << $k) - 1;

    // toggle the last m bits and
    // return the number
    return ($n ^ $num);
}

// function to increment a number by one
// by manipulating the bits
function incrementByOne($n)
{
    // get position of rightmost unset bit
    // if all bits of 'n' are set, then the
    // bit left to the MSB is the rightmost
    // unset bit
    $k = getPosOfRightmostSetBit(~$n);

    // kth bit of n is being set
    // by this operation
    $n = ((1 << $k) | $n);

    // from the right toggle all the
    // bits before the k-th
    if ($k != 0)
        $n = toggleLastKBits($n, $k);

    // required number
    return $n;
}

// Driver code
$n = 15;
echo incrementByOne($n);

// This code is contributed by Mithun Kumar
?>
```

## java 描述语言

```
<script>

// JavaScript program to increment a number
// by one by manipulating the bits

    // function to find the position
    // of rightmost set bit
    function getPosOfRightmostSetBit(n)
    {
        return (Math.log(n & -n) / Math.log(2));
    }

    // function to toggle the last m bits
    function toggleLastKBits(n, k)
    {
        // calculating a number 'num' having
        // 'm' bits and all are set
        let num = (1 << k) - 1;

        // toggle the last m bits and return
        // the number
        return (n ^ num);
    }

    // function to increment a number by one
    // by manipulating the bits
    function incrementByOne(n)
    {
        // get position of rightmost unset bit
        // if all bits of 'n' are set, then the
        // bit left to the MSB is the rightmost
        // unset bit
        let k = getPosOfRightmostSetBit(~n);

        // kth bit of n is being set
        // by this operation
        n = ((1 << k) | n);

        // from the right toggle all
        // the bits before the k-th bit
        if (k != 0)
            n = toggleLastKBits(n, k);

        // required number
        return n;

    }  

// Driver code

        let n = 15;
        document.write(incrementByOne(n));

</script>
```

**输出:**

```
16
```