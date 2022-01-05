# 检查给定范围内的位是否处于交替模式

> 原文:[https://www . geesforgeks . org/check-bit-in-alternate-pattern-in-给定范围/](https://www.geeksforgeeks.org/check-whether-bits-are-in-alternate-pattern-in-the-given-range/)

给定一个非负数 **n** 和两个值 **l** 和 **r** 。问题是检查 **n** 在 **l** 到 **r** 范围内的二进制表示中是否有交替模式。这里，交替模式意味着设置位和未设置位以交替顺序出现。这些位从右向左编号，即最低有效位被认为在第一个位置。
**约束:** 1 < = l < = r < =二进制表示中的位数 **n** 。
**举例:**

```
Input : n = 18, l = 1, r = 3
Output : Yes
(18)<sub>10</sub> = (10010)2
The bits in the range 1 to 3 in the
binary representation of 18 are in
alternate order.

Input : n = 22, l = 2, r = 4
Output : No
(22)<sub>10</sub> = (10110)2
The bits in the range 2 to 4 in the
binary representation of 22 are not in
alternate order.
```

**算法:**

```
bitsAreInAltPatrnInGivenTRange(n, l, r)

    // Shift bits of given number n by 
    // (l-1).
    num = n >> (l - 1)

    // Find first bit of range
    prev = num & 1

    // Traverse through remaining
    // bits. For every bit, check if
    // current bit is same as previous
    // or not.
    num = num >> 1    
    for i = 1 to (r - l)
        curr = num & 1

        if curr == prev then
            return false

        prev = curr
        num = num >> 1

    return true;
```

## C++

```
// C++ implementation to check whether bits are in
// alternate pattern in the given range
#include <bits/stdc++.h>

using namespace std;

// function to check whether bits are in
// alternate pattern in the given range
bool bitsAreInAltPatrnInGivenTRange(unsigned int n,
                                    unsigned int l,
                                    unsigned int r)
{
    unsigned int num, prev, curr;

    // right shift n by (l - 1) bits
    num = n >> (l - 1);

    // get the bit at the last position in 'num'
    prev = num & 1;

    // right shift 'num' by 1
    num = num >> 1;

    // loop until there are bits in the given range
    for (int i = 1; i <= (r - l); i++) {

        // get the bit at the last position in 'num'
        curr = num & 1;

        // if true, then bits are not in alternate
        // pattern
        if (curr == prev)
            return false;

        // update 'prev'
        prev = curr;

        // right shift 'num' by 1
        num = num >> 1;
    }

    // bits are in alternate pattern in the
    // given range
    return true;
}

// Driver program to test above
int main()
{
    unsigned int n = 18;
    unsigned int l = 1, r = 3;

    if (bitsAreInAltPatrnInGivenTRange(n, l, r))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check
// whether bits are in alternate
// pattern in the given range
class GFG
{

// function to check whether
// bits are in alternate
// pattern in the given range
static boolean bitsAreInAltPatrnInGivenTRange(int n,
                                       int l, int r)
{
    int num, prev, curr;

    // right shift n by (l - 1) bits
    num = n >> (l - 1);

    // get the bit at the
    // last position in 'num'
    prev = num & 1;

    // right shift 'num' by 1
    num = num >> 1;

    // loop until there are
    // bits in the given range
    for (int i = 1; i <= (r - l); i++)
    {

        // get the bit at the
        // last position in 'num'
        curr = num & 1;

        // if true, then bits are
        // not in alternate pattern
        if (curr == prev)
            return false;

        // update 'prev'
        prev = curr;

        // right shift 'num' by 1
        num = num >> 1;
    }

    // bits are in alternate
    // pattern in the given range
    return true;
}

// Driver Code
public static void main(String[] args)
{
    int n = 18;
    int l = 1, r = 3;

    if (bitsAreInAltPatrnInGivenTRange(n, l, r))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation to check
# whether bits are in alternate
# pattern in the given range

# function to check whether
# bits are in alternate
# pattern in the given range
def bitsAreInAltPatrnInGivenTRange(n, l, r):

    # right shift n by (l - 1) bits
    num = n >> (l - 1);

    # get the bit at the
    # last position in 'num'
    prev = num & 1;

    # right shift 'num' by 1
    num = num >> 1;

    # loop until there are
    # bits in the given range
    for i in range(1,(r - l)):

        # get the bit at the
        # last position in 'num'
        curr = num & 1;

        # if true, then bits are
        # not in alternate pattern
        if (curr == prev):
            return False;

        # update 'prev'
        prev = curr;

        # right shift 'num' by 1
        num = num >> 1;

    # bits are in alternate
    # pattern in the given range
    return True;

# Driver Code
if __name__ == "__main__":
    n = 18;
    l = 1;
    r = 3;

    if(bitsAreInAltPatrnInGivenTRange(n, l, r)):
        print("Yes");
    else:
        print("No");

# This Code is contributed by mits
```

## C#

```
// C# implementation to check
// whether bits are in alternate
// pattern in the given range
using System;

class GFG
{

// function to check whether
// bits are in alternate
// pattern in the given range
static bool bitsAreInAltPatrnInGivenTRange(int n,
                                    int l, int r)
{
    int num, prev, curr;

    // right shift n by (l - 1) bits
    num = n >> (l - 1);

    // get the bit at the
    // last position in 'num'
    prev = num & 1;

    // right shift 'num' by 1
    num = num >> 1;

    // loop until there are
    // bits in the given range
    for (int i = 1; i <= (r - l); i++)
    {

        // get the bit at the
        // last position in 'num'
        curr = num & 1;

        // if true, then bits are
        // not in alternate pattern
        if (curr == prev)
            return false;

        // update 'prev'
        prev = curr;

        // right shift 'num' by 1
        num = num >> 1;
    }

    // bits are in alternate
    // pattern in the given range
    return true;
}

// Driver Code
static void Main()
{
    int n = 18;
    int l = 1, r = 3;

    if (bitsAreInAltPatrnInGivenTRange(n, l, r))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// whether bits are in alternate
// pattern in the given range

// function to check whether
// bits are in alternate
// pattern in the given range
function bitsAreInAltPatrnInGivenTRange($n, $l, $r)
{

    // right shift n by (l - 1) bits
    $num = $n >> ($l - 1);

    // get the bit at the
    // last position in 'num'
    $prev = $num & 1;

    // right shift 'num' by 1
    $num = $num >> 1;

    // loop until there are
    // bits in the given range
    for ($i = 1; $i <= ($r - $l); $i++)
    {

        // get the bit at the
        // last position in 'num'
        $curr = $num & 1;

        // if true, then bits are
        // not in alternate pattern
        if ($curr == $prev)
            return false;

        // update 'prev'
        $prev = $curr;

        // right shift 'num' by 1
        $num = $num >> 1;
    }

    // bits are in alternate
    // pattern in the given range
    return true;
}

// Driver Code
$n = 18;
$l = 1;
$r = 3;

if (bitsAreInAltPatrnInGivenTRange($n, $l, $r))
    echo "Yes";
else
    echo "No";

// This Code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation to check whether bits are in
// alternate pattern in the given range

// function to check whether bits are in
// alternate pattern in the given range
function bitsAreInAltPatrnInGivenTRange(n, l, r)
{
    var num, prev, curr;

    // right shift n by (l - 1) bits
    num = n >> (l - 1);

    // get the bit at the last position in 'num'
    prev = num & 1;

    // right shift 'num' by 1
    num = num >> 1;

    // loop until there are bits in the given range
    for (var i = 1; i <= (r - l); i++) {

        // get the bit at the last position in 'num'
        curr = num & 1;

        // if true, then bits are not in alternate
        // pattern
        if (curr == prev)
            return false;

        // update 'prev'
        prev = curr;

        // right shift 'num' by 1
        num = num >> 1;
    }

    // bits are in alternate pattern in the
    // given range
    return true;
}

// Driver program to test above
var n = 18;
var l = 1, r = 3;
if (bitsAreInAltPatrnInGivenTRange(n, l, r))
    document.write( "Yes");
else
    document.write( "No");

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
Yes
```