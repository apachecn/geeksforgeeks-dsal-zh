# 检查给定范围内是否所有位都没有置位

> 原文:[https://www . geeksforgeeks . org/check-所有位是否在给定范围内未设置/](https://www.geeksforgeeks.org/check-whether-all-the-bits-are-unset-in-the-given-range/)

给定一个非负数 **n** 和两个值 **l** 和 **r** 。问题是检查在 **n** 的二进制表示中 **l** 到 **r** 的范围内是否所有的位都没有置位。这些位从右向左编号，即最低有效位被认为在第一个位置。
**约束:** 1 < = l < = r < =二进制表示中的位数 **n** 。
**举例:**

```
Input : n = 17, l = 2, r = 4
Output : Yes
(17)10 = (10001)2
The bits in the range 2 to 4 are all unset.

Input : n = 39, l = 4, r = 6
Output : No
(39)10 = (100111)2
The bits in the range 4 to 6 are all not unset.
```

**进场:**以下为步骤:

1.  计算**num**=((1<<r)–1)^((1<<(l-1))–1)。这将产生一个数字**号**，其具有 **r** 数量的比特，并且范围 **l** 到 **r** 中的比特是唯一设置的比特。
2.  计算**新 _ 数** = n &数。
3.  如果 new_num == 0，则返回“是”(在给定范围内，所有位都不设置)。
4.  否则返回“否”(在给定的范围内，所有的位不会被取消设置)。

## C++

```
// C++ implementation to check whether all the bits
// are unset in the given range or not
#include <bits/stdc++.h>

using namespace std;

// function to check whether all the bits
// are unset in the given range or not
bool allBitsSetInTheGivenRange(unsigned int n,
                               unsigned int l, unsigned int r)
{
    // calculating a number 'num' having 'r'
    // number of bits and bits in the range l
    // to r are the only set bits
    int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

    // new number which could only have one or more
    // set bits in the range l to r and nowhere else
    int new_num = n & num;

    // if true, then all bits are unset
    // in the given range
    if (new_num == 0)
        return true;

    // else all bits are not unset
    // in the given range
    return false;
}

// Driver program to test above
int main()
{
    unsigned int n = 17;
    unsigned int l = 2, r = 4;
    if (allBitsSetInTheGivenRange(n, l, r))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// whether all the bits are
// unset in the given range or not
class GFG
{

// function to check whether
// all the bits are unset in
// the given range or not
static boolean allBitsSetInTheGivenRange(int n,
                                         int l,
                                         int r)
{
    // calculating a number 'num'
    // having 'r' number of bits
    // and bits in the range l
    // to r are the only set bits
    int num = ((1 << r) - 1) ^
              ((1 << (l - 1)) - 1);

    // new number which could only
    // have one or more set bits in
    // the range l to r and nowhere else
    int new_num = n & num;

    // if true, then all bits are
    // unset in the given range
    if (new_num == 0)
        return true;

    // else all bits are not
    // unset in the given range
    return false;
}

// Driver Code
public static void main(String[] args)
{
    int n = 17;
    int l = 2, r = 4;
    if (allBitsSetInTheGivenRange(n, l, r))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed
// by Smitha
```

## 蟒蛇 3

```
# Python3 implementation to
# check whether all the bits
# are unset in the given
# range or not

# function to check whether
# all the bits are unset in
# the given range or not
def allBitsSetInTheGivenRange(n, l, r):

    # calculating a number 'num'
    # having 'r' number of bits
    # and bits in the range l
    # to r are the only set bits
    num = (((1 << r) - 1) ^
           ((1 << (l - 1)) - 1))

    # new number which could only
    # have one or more set bits in
    # the range l to r and nowhere else
    new_num = n & num

    # if true, then all bits are
    # unset in the given range
    if (new_num == 0):
        return True

    # else all bits are not
    # unset in the given range
    return false

# Driver Code
n = 17
l = 2
r = 4
if (allBitsSetInTheGivenRange(n, l, r)):
    print("Yes")
else:
    print("No")

# This code is contributed
# by Smitha
```

## C#

```
// C# implementation to check
// whether all the bits are
// unset in the given range or not
using System;

class GFG
{

// function to check whether
// all the bits are unset in
// the given range or not
static bool allBitsSetInTheGivenRange(int n,
                                      int l,
                                      int r)
{
    // calculating a number 'num'
    // having 'r' number of bits
    // and bits in the range l
    // to r are the only set bits
    int num = ((1 << r) - 1) ^
              ((1 << (l - 1)) - 1);

    // new number which could 
    // only have one or more
    // set bits in the range
    // l to r and nowhere else
    int new_num = n & num;

    // if true, then all
    // bits are unset
    // in the given range
    if (new_num == 0)
        return true;

    // else all bits are not
    // unset in the given range
    return false;
}

// Driver Code
public static void Main()
{
    int n = 17;
    int l = 2, r = 4;
    if (allBitsSetInTheGivenRange(n, l, r))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed
// by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// whether all the bits are
// unset in the given range or not

// function to check whether
// all the bits are unset in
// the given range or not
function allBitsSetInTheGivenRange($n, $l, $r)
{
    // calculating a number 'num'
    // having 'r' number of bits
    // and bits in the range l
    // to r are the only set bits
    $num = ((1 << $r) - 1) ^
           ((1 << ($l - 1)) - 1);

    // new number which could only
    // have one or more set bits in
    // the range l to r and nowhere else
    $new_num = $n & $num;

    // if true, then all bits are
    // unset in the given range
    if ($new_num == 0)
        return true;

    // else all bits are not unset
    // in the given range
    return false;
}

// Driver Code
$n = 17;
$l = 2;
$r = 4;
if (allBitsSetInTheGivenRange($n, $l, $r))
    echo "Yes";
else
    echo "No";

// This code is contributed by Smitha
?>
```

## java 描述语言

```
<script>

// Javascript implementation to
// check whether all the bits
// are unset in the given range or not

// function to check whether all the bits
// are unset in the given range or not
function allBitsSetInTheGivenRange(n, l, r)
{
    // calculating a number 'num' having 'r'
    // number of bits and bits in the range l
    // to r are the only set bits
    let num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

    // new number which could only have one or more
    // set bits in the range l to r and nowhere else
    let new_num = n & num;

    // if true, then all bits are unset
    // in the given range
    if (new_num == 0)
        return true;

    // else all bits are not unset
    // in the given range
    return false;
}

// Driver program to test above
    let n = 17;
    let l = 2, r = 4;
    if (allBitsSetInTheGivenRange(n, l, r))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**输出:**

```
Yes
```