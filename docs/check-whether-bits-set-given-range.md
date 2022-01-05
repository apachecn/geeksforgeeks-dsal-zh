# 检查是否所有的位都设置在给定的范围内

> 原文:[https://www . geesforgeks . org/check-when-bits-set-给定-range/](https://www.geeksforgeeks.org/check-whether-bits-set-given-range/)

给定一个非负数 **n** 和两个值 **l** 和 **r** 。问题是在 **n** 的二进制表示中，检查是否所有的位都设置在 **l** 到 **r** 的范围内。
**约束:** 1 < = l < = r < =二进制表示中的位数 **n** 。
示例:

```
Input : n = 22, l = 2, r = 3
Output : Yes
(22)10 = (10110)2
The bits in the range 2 to 3 are all set.

Input : n = 47, l = 2, r = 5 
Output : No
(47)10 = (101111)2
The bits in the range 2 to 5 are all not set.
```

**进场:**以下为步骤:

1.  计算**num**=((1<<r)–1)^((1<<(l-1))–1)。这将产生一个数字**号**，其具有 **r** 数量的比特，并且范围 **l** 到 **r** 中的比特是唯一设置的比特。
2.  计算**新 _ 数** = n &数。
3.  如果 num == new_num，返回“是”(所有位都设置在给定范围内)。
4.  否则返回“否”(并非所有位都设置在给定范围内)。

## C++

```
// C++ implementation to check whether all the bits
// are set in the given range or not
#include <bits/stdc++.h>

using namespace std;

// function to check whether all the bits
// are set in the given range or not
string allBitsSetInTheGivenRange(unsigned int n,
                                 unsigned int l, unsigned int r)
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
        return "Yes";

    // else all bits are not set   
    return "No";   
}

// Driver program to test above
int main()
{
    unsigned int n = 22;
    unsigned int l = 2, r = 3;
    cout << allBitsSetInTheGivenRange(n, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether all
// the bits are set in the given range or not
class GFG {

    // function to check whether all the bits
    // are set in the given range or not
    static String allBitsSetInTheGivenRange(int n,
                                    int l,int r)
    {

        // calculating a number 'num' having 'r'
        // number of bits and bits in the range
        // l to r are the only set bits
        int num = ((1 << r) - 1) ^ ((1 <<
                                  (l - 1)) - 1);

        // new number which will only have one
        // or more set bits in the range l to r
        // and nowhere else
        int new_num = n & num;

        // if both are equal, then all bits are
        // set in the given range
        if (num == new_num)
            return "Yes";

        // else all bits are not set
        return "No";
    }

    //Driver code
    public static void main (String[] args)
    {
        int n = 22;
        int l = 2, r = 3;

        System.out.print(allBitsSetInTheGivenRange(
                                           n, l, r));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 implementation to check
# whether all the bits are set in
# the given range or not

# Function to check whether all the bits
# are set in the given range or not
def allBitsSetInTheGivenRange(n, l, r):

    # calculating a number 'num' having 'r'
    # number of bits and bits in the range l
    # to r are the only set bits
    num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1)

    # new number which will only have
    # one or more set bits in the range
    # l to r and nowhere else
    new_num = n & num

    # if both are equal, then all bits
    # are set in the given range
    if (num == new_num):
        return "Yes"

    # else all bits are not set
    return "No"

# Driver code
n, l, r = 22, 2, 3
print(allBitsSetInTheGivenRange(n, l, r))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# implementation to check whether all the bits
// are set in the given range or not
using System;

class GFG
{
    // function to check whether all the bits
    // are set in the given range or not
    static String allBitsSetInTheGivenRange(int n,
                                       int l,int r)
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
            return "Yes";

        // else all bits are not set   
        return "No";   
    }

    //Driver code
    public static void Main ()
    {
        int n = 22;
        int l = 2, r = 3;
        Console.Write(allBitsSetInTheGivenRange(n, l, r));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// whether all the bits are set
// in the given range or not

// function to check whether
// all the bits are set in
// the given range or not
function allBitsSetInTheGivenRange($n, $l, $r)
{

    // Calculating a number
    // 'num' having 'r'
    // number of bits and
    // bits in the range l
    // to r are the only
    // set bits
    $num = ((1 << $r) - 1) ^
           ((1 << ($l - 1)) - 1);

    // new number which will
    // only have one or more
    // set bits in the range
    // l to r and nowhere else
    $new_num = $n & $num;

    // if both are equal,
    // then all bits are set
    // in the given range
    if ($num == $new_num)
        return "Yes";

    // else all bits
    // are not set
    return "No";
}

    // Driver Code
    $n = 22;
    $l = 2;
    $r = 3;
    echo allBitsSetInTheGivenRange($n, $l, $r);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// javascript implementation to check whether all
// the bits are set in the given range or not

// function to check whether all the bits
// are set in the given range or not
function allBitsSetInTheGivenRange(n,l,r)
{

    // calculating a number 'num' having 'r'
    // number of bits and bits in the range
    // l to r are the only set bits
    var num = ((1 << r) - 1) ^ ((1 <<
                              (l - 1)) - 1);

    // new number which will only have one
    // or more set bits in the range l to r
    // and nowhere else
    var new_num = n & num;

    // if both are equal, then all bits are
    // set in the given range
    if (num == new_num)
        return "Yes";

    // else all bits are not set
    return "No";
}

// Driver code
var n = 22;
var l = 2, r = 3;

document.write(allBitsSetInTheGivenRange(
                                   n, l, r));

// This code contributed by Princi Singh

</script>
```

输出:

```
Yes
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。