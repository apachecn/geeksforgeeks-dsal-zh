# 检查两个数的 L 到 R 范围内的位是否互补

> 原文:[https://www . geeksforgeeks . org/check-in-range-l-r 范围内的两个数字是否都是互补的/](https://www.geeksforgeeks.org/check-if-all-the-bits-of-two-numbers-that-lies-within-range-l-to-r-are-complement-of-each-other-or-not/)

给定两个非负数 **a** 和 **b** 以及两个值 **l** 和 **r** 。问题是检查两个给定数目的 **l** 到 **r** 范围内对应位置的所有位是否互补。
位从右向左编号，即最低有效位被认为在第一位置。
**示例** :

```
Input: a = 10, b = 5
       l = 1, r = 3
Output: Yes
(10)10 = (1010)2
(5)10 = (101)2 = (0101)2
All the bits in the range 1 to 3 are complement of each other.

Input: a = 21, b = 13
       l = 2, r = 4
Output: No
(21)10 = (10101)2
(13)10 = (1101)2 = (1101)2
All the bits in the range 2 to 4 are not complement of each other.
```

**方法:**下面是解决问题的步骤

*   计算 **xor_value** = a ^ b。
*   在 **xor_value** 中检查所有位是否都设置在 **l** 到 **r** 的范围内。参考[这个](https://www.geeksforgeeks.org/check-whether-bits-set-given-range/)岗位。

下面是上述方法的实现。

## C++

```
// C++ implementation to check
// whether all the bits in the given range
// of two numbers are complement of each other
#include <bits/stdc++.h>
using namespace std;

// function to check whether all the bits
// are set in the given range or not
bool allBitsSetInTheGivenRange(unsigned int n,
                               unsigned int l,
                               unsigned int r)
{
    // calculating a number 'num' having 'r'
    // number of bits and bits in the range l
    // to r are the only set bits
    int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

    // new number which will only have one or more
    // set bits in the range l to r and nowhere else
    int new_num = n & num;

    // if both are equal, then all bits are set
    // in the given range
    if (num == new_num)
        return true;

    // else all bits are not set
    return false;
}

// function to check whether all the bits in the given range
// of two numbers are complement of each other
bool bitsAreComplement(unsigned int a, unsigned int b,
                       unsigned int l, unsigned int r)
{
    unsigned int xor_value = a ^ b;
    return allBitsSetInTheGivenRange(xor_value, l, r);
}

// Driver Code
int main()
{
    unsigned int a = 10, b = 5;
    unsigned int l = 1, r = 3;

    if (bitsAreComplement(a, b, l, r))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// whether all the bits in the
// given range of two numbers
// are complement of each other
class GFG
{
// function to check whether
// all the bits are set in
// the given range or not
static boolean allBitsSetInTheGivenRange(int n,
                                         int l, int r)
{
    // calculating a number 'num'
    // having 'r' number of bits
    // and bits in the range l
    // to r are the only set bits
    int num = ((1 << r) - 1) ^
              ((1 << (l - 1)) - 1);

    // new number which will only
    // have one or more set bits
    // in the range l to r and
    // nowhere else
    int new_num = n & num;

    // if both are equal,
    // then all bits are set
    // in the given range
    if (num == new_num)
        return true;

    // else all bits are not set
    return false;
}

// function to check whether all
// the bits in the given range
// of two numbers are complement
// of each other
static boolean bitsAreComplement(int a, int b,
                                 int l, int r)
{
    int xor_value = a ^ b;
    return allBitsSetInTheGivenRange(xor_value, l, r);
}

// Driver Code
public static void main(String []args)
{
    int a = 10, b = 5;
    int l = 1, r = 3;

    if (bitsAreComplement(a, b, l, r))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Smitha
```

## 蟒蛇 3

```
# Python 3 implementation to check whether
# all the bits in the given range of two
# numbers are complement of each other

# function to check whether all the bits
# are set in the given range or not
def allBitsSetInTheGivenRange(n, l, r):

    # calculating a number 'num' having 'r'
    # number of bits and bits in the range l
    # to r are the only set bits
    num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1)

    # new number which will only have one
    # or more set bits in the range l to r
    # and nowhere else
    new_num = n & num

    # if both are equal, then all bits
    # are set in the given range
    if (num == new_num):
        return True

    # else all bits are not set
    return False

# function to check whether all the bits
# in the given range of two numbers are
# complement of each other
def bitsAreComplement(a, b, l, r):
    xor_value = a ^ b
    return allBitsSetInTheGivenRange(xor_value, l, r)

# Driver Code
if __name__ == "__main__":

    a = 10
    b = 5
    l = 1
    r = 3

    if (bitsAreComplement(a, b, l, r)):
        print("Yes")
    else:
        print("No")

# This code is contributed by ita_c
```

## C#

```
// C# implementation to check
// whether all the bits in the
// given range of two numbers
// are complement of each other
using System;

class GFG
{
// function to check whether
// all the bits are set in
// the given range or not
static bool allBitsSetInTheGivenRange(int n, int l,
                                      int r)
{
    // calculating a number 'num'
    // having 'r' number of bits
    // and bits in the range l
    // to r are the only set bits
    int num = ((1 << r) - 1) ^
              ((1 << (l - 1)) - 1);

    // new number which will only
    // have one or more set bits
    // in the range l to r and
    // nowhere else
    int new_num = n & num;

    // if both are equal,
    // then all bits are set
    // in the given range
    if (num == new_num)
        return true;

    // else all bits are not set
    return false;
}

// function to check whether all
// the bits in the given range
// of two numbers are complement
// of each other
static bool bitsAreComplement(int a, int b,
                              int l, int r)
{
    int xor_value = a ^ b;
    return allBitsSetInTheGivenRange(xor_value, l, r);
}

// Driver Code
static public void Main ()
{
    int a = 10, b = 5;
    int l = 1, r = 3;

    if (bitsAreComplement(a, b, l, r))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed
// by Ajit Deshpal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// whether all the bits in the
// given range of two numbers
// are complement of each other

// function to check whether
// all the bits are set in
// the given range or not
function allBitsSetInTheGivenRange($n, $l ,$r)
{

    // calculating a number
    // 'num' having 'r' number
    // of bits and bits in
    // the range l to r are
    // the only set bits
    $num = ((1 << $r) - 1) ^
       ((1 << ($l - 1)) - 1);

    // new number which will
    // only have one or more
    // set bits in the range
    // l to r and nowhere else
    $new_num = ($n & $num);

    // if both are equal,
    // then all bits are set
    // in the given range
    if ($num == $new_num)
        return true;

    // else all bits
    // are not set
    return false;
}

// function to check whether
// all the bits in the given range
// of two numbers are complement
// of each other
function bitsAreComplement($a, $b,$l, $r)
{
    $xor_value = $a ^ $b;
    return allBitsSetInTheGivenRange($xor_value, $l, $r);
}

// Driver Code
$a = 10;
$b = 5;
$l = 1;
$r = 3;
if (bitsAreComplement($a, $b, $l, $r))
    echo "Yes";
else
    echo "No";

// This Code is Contributed by ajit
?>
```

## java 描述语言

```
<script>
// javascript implementation to check
// whether all the bits in the
// given range of two numbers
// are complement of each other

// function to check whether
// all the bits are set in
// the given range or not
function allBitsSetInTheGivenRange(n, l , r)
{
    // calculating a number 'num'
    // having 'r' number of bits
    // and bits in the range l
    // to r are the only set bits
    var num = ((1 << r) - 1) ^
              ((1 << (l - 1)) - 1);

    // new number which will only
    // have one or more set bits
    // in the range l to r and
    // nowhere else
    var new_num = n & num;

    // if both are equal,
    // then all bits are set
    // in the given range
    if (num == new_num)
        return true;

    // else all bits are not set
    return false;
}

// function to check whether all
// the bits in the given range
// of two numbers are complement
// of each other
function bitsAreComplement(a , b,l , r)
{
    var xor_value = a ^ b;
    return allBitsSetInTheGivenRange(xor_value, l, r);
}

// Driver Code
var a = 10, b = 5;
var l = 1, r = 3;

if (bitsAreComplement(a, b, l, r))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by Princi Singh
</script>
```

**Output:** 

```
Yes
```