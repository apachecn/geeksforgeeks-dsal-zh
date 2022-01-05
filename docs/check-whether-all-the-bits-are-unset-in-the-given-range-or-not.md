# 检查所有位在给定范围内是否未置位

> 原文:[https://www . geeksforgeeks . org/check-所有位是否在给定范围内未设置/](https://www.geeksforgeeks.org/check-whether-all-the-bits-are-unset-in-the-given-range-or-not/)

给定一个非负数 **n** 和两个值 **l** 和 **r** 。问题是检查在 **n** 的二进制表示中 **l** 到 **r** 的范围内是否所有的位都没有置位。
约束:1 < = l < = r < =二进制表示的位数 **n** 。
**举例:**

```
Input : n = 17, l = 2, r = 4
Output : Yes
(17)10 = (10001)2
The bits in the range 2 to 4 are all unset.

Input : n = 36, l = 3, r = 5
Output : No
(36)10 = (100100)2
The bits in the range 3 to 5 are all not unset.
```

**进场:**以下为步骤:

1.  计算**num**=((1<<r)–1)^((1<<(l-1))–1)。这将产生具有 **r** 比特数的数字编号，并且范围 **l** 到 **r** 中的比特是唯一设置的比特。
2.  计算**新 _ 数** = n &数。
3.  如果 new_num == 0，则返回“是”(在给定范围内，所有位都不设置)。
4.  否则返回“否”(在给定的范围内，所有的位不会被取消设置)。

## C++

```
// C++ implementation to check whether all
// the bits are unset in the given range
// or not
#include <bits/stdc++.h>
using namespace std;

// function to check whether all the bits
// are unset in the given range or not
string allBitsSetInTheGivenRange(unsigned int n,
                                unsigned int l,
                                unsigned int r)
{
    // calculating a number 'num' having 'r'
    // number of bits and bits in the range l
    // to r are the only set bits
    int num = ((1 << r) - 1) ^
            ((1 << (l - 1)) - 1);

    // new number which will only have
    // one or more set bits in the range
    // l to r and nowhere else
    int new_num = n & num;

    // if new num is 0, then all bits
    // are unset in the given range
    if (new_num == 0)
        return "Yes";

    // else all bits are not unset
    return "No";
}

// Driver program to test above
int main()
{
    unsigned int n = 17;
    unsigned int l = 2, r = 4;
    cout << allBitsSetInTheGivenRange(n, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// check whether all the
// bits are unset in the
// given range or not
import java.io.*;

class GFG
{

// function to check whether
// all the bits are unset in
// the given range or not
static String allBitsSetInTheGivenRange(int n,
                                        int l,
                                        int r)
{
    // calculating a number 'num'
    // having 'r' number of bits
    // and bits in the range l to
    // r are the only set bits
    int num = ((1 << r) - 1) ^
              ((1 << (l - 1)) - 1);

    // new number which will
    // only have one or more
    // set bits in the range
    // l to r and nowhere else
    int new_num = n & num;

    // if new num is 0, then
    // all bits are unset in
    // the given range
    if(new_num == 0)
        return "Yes";

    // else all bits
    // are not unset
    return "No";
}

// Driver Code
public static void main (String[] args)
{
    int n = 17;
    int l = 2;
    int r = 4;
    System.out.println(
           allBitsSetInTheGivenRange(n, l, r));
}
}

// This code is contributed by akt_mit
```

## 蟒蛇 3

```
# Python 3 implementation to check whether 
# all the bits are unset in the given range
# or not

# function to check whether all the bits
# are unset in the given range or not
def allBitsSetInTheGivenRange(n, l, r):

    # calculating a number 'num' having 'r'
    # number of bits and bits in the range l
    # to r are the only set bits
    num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1)

    # new number which will only have
    # one or more set bits in the
    # range l to r and nowhere else
    new_num = n & num

    # if new num is 0, then all bits
    # are unset in the given range
    if (new_num == 0):
        return "Yes"

    # else all bits are not unset
    return "No"

# Driver Code
if __name__ == "__main__":

    n = 17
    l = 2
    r = 4
    print(allBitsSetInTheGivenRange(n, l, r))

# This code is contributed by ita_c
```

## C#

```
// C#  implementation to
// check whether all the
// bits are unset in the
// given range or not
using System;

public class GFG{

// function to check whether
// all the bits are unset in
// the given range or not
static String allBitsSetInTheGivenRange(int n,
                                        int l,
                                        int r)
{
    // calculating a number 'num'
    // having 'r' number of bits
    // and bits in the range l to
    // r are the only set bits
    int num = ((1 << r) - 1) ^
            ((1 << (l - 1)) - 1);

    // new number which will
    // only have one or more
    // set bits in the range
    // l to r and nowhere else
    int new_num = n & num;

    // if new num is 0, then
    // all bits are unset in
    // the given range
    if(new_num == 0)
        return "Yes";

    // else all bits
    // are not unset
    return "No";
}

// Driver Code
    static public void Main (){
        int n = 17;
        int l = 2;
        int r = 4;
        Console.WriteLine(
            allBitsSetInTheGivenRange(n, l, r));
    }
}

// This code is contributed by k_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// whether all the bits are
// unset in the given range
// or not

// function to check whether
// all the bits are unset in
// the given range or not
function allBitsSetInTheGivenRange($n,
                                   $l, $r)
{
    // calculating a number 'num'
    // having 'r' number of bits
    // and bits in the range l
    // to r are the only set bits
    $num = ((1 << $r) - 1) ^
           ((1 << ($l - 1)) - 1);

    // new number which will
    // only have one or more
    // set bits in the range
    // l to r and nowhere else
    $new_num = $n & $num;

    // if new num is 0, then
    // all bits are unset in
    // the given range
    if ($new_num == 0)
        return "Yes";

    // else all bits
    // are not unset
    return "No";
}

// Driver Code
$n = 17;
$l = 2; $r = 4;
echo allBitsSetInTheGivenRange($n,
                               $l, $r);

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>

// Javascript implementation to check whether all
// the bits are unset in the given range
// or not

// function to check whether all the bits
// are unset in the given range or not
function allBitsSetInTheGivenRange(n, l, r)
{
    // calculating a number 'num' having 'r'
    // number of bits and bits in the range l
    // to r are the only set bits
    var num = ((1 << r) - 1) ^
            ((1 << (l - 1)) - 1);

    // new number which will only have
    // one or more set bits in the range
    // l to r and nowhere else
    var new_num = n & num;

    // if new num is 0, then all bits
    // are unset in the given range
    if (new_num == 0)
        return "Yes";

    // else all bits are not unset
    return "No";
}

// Driver program to test above
var n = 17;
var l = 2, r = 4;
document.write( allBitsSetInTheGivenRange(n, l, r));

</script>
```

**输出:**

```
Yes
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。