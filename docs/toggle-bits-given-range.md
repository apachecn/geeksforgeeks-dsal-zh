# 在给定范围内切换位

> 原文:[https://www.geeksforgeeks.org/toggle-bits-given-range/](https://www.geeksforgeeks.org/toggle-bits-given-range/)

给定一个非负数 **n** 和两个值 **l** 和 **r** 。问题是在 **n** 的二进制表示中切换 **l** 到 **r** 范围内的位，即从最右边的 **lth** 位切换到最右边的 **rth** 位。拨动操作将一位 **0** 翻转至 **1** ，一位 **1** 翻转至 **0** 。
**约束:** 1 < = l < = r < =在 **n** 的二进制表示中的位数。
示例:

```
Input : n = 17, l = 2, r = 3
Output : 23
(17)<sub>10</sub> = (10001)2
(23)<sub>10</sub> = (10111)2
The bits in the range 2 to 3 in the binary
representation of 17 are toggled.

Input : n = 50, l = 2, r = 5
Output : 44
```

**进场:**以下为步骤:

1.  将 **num 计算为**=((1<<r)–1)^((1<<(l-1))–1)或 as ((1 < < r)-l)。这将产生一个数字**号**，其具有 **r** 数量的比特，并且范围 **l** 到 **r** 中的比特是唯一设置的比特。
2.  现在，执行 **n = n ^数**。这将切换 **l** 到 **r** 到 **n** 范围内的位。

C/C++

```
 // C++ implementation to toggle bits in
// the given range
#include <bits/stdc++.h>
using namespace std;

// function to toggle bits in the given range
unsigned int toggleBitsFromLToR(unsigned int n,
                                unsigned int l, unsigned int r)
{
    // calculating a number 'num' having 'r'
    // number of bits and bits in the range l
    // to r are the only set bits
    int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

    // toggle bits in the range l to r in 'n'
    // and return the number
//Besides this, we can calculate num as: num=(1<<r)-l .
    return (n ^ num);
}

// Driver program to test above
int main()
{
    unsigned int n = 50;
    unsigned int l = 2, r = 5;
    cout << toggleBitsFromLToR(n, l, r);
    return 0;
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to toggle bits in
// the given range
import java.io.*;

class GFG
{
    // Function to toggle bits in the given range
    static int toggleBitsFromLToR(int n, int l, int r)
    {
        // calculating a number 'num' having 'r'
        // number of bits and bits in the range l
        // to r are the only set bits
        int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

        // toggle bits in the range l to r in 'n'
        // and return the number
        //Besides this, we can calculate num as: num=(1<<r)-l .
        return (n ^ num);
    }

    // driver program
    public static void main (String[] args)
    {
        int n = 50;
        int l = 2, r = 5;
        System.out.println(toggleBitsFromLToR(n, l, r));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python implementation
# to toggle bits in
# the given range

# function to toggle bits
# in the given range
def toggleBitsFromLToR(n,l,r):

    # calculating a number
    # 'num' having 'r'
    # number of bits and
    # bits in the range l
    # to r are the only set bits
    num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1)

    # toggle bits in the
    # range l to r in 'n'
    # Besides this, we can calculate num as: num=(1<<r)-l .

    # and return the number
    return (n ^ num)

# Driver code

n = 50
l = 2
r = 5

print(toggleBitsFromLToR(n, l, r))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# implementation to toggle bits
// in the given range
using System;

namespace Toggle
{
    public class GFG
    {    

    // Function to toggle bits in the given range
    static int toggleBitsFromLToR(int n, int l, int r)
    {
        // calculating a number 'num' having 'r'
        // number of bits and bits in the range l
        // to r are the only set bits
        int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

        // toggle bits in the range l to r in 'n'
        //Besides this, we can calculate num as: num=(1<<r)-l .
        // and return the number
        return (n ^ num);
    }

    // Driver Code
    public static void Main ()
    {
        int n = 50;
        int l = 2, r = 5;
        Console.Write(toggleBitsFromLToR(n, l, r));
    }
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation
// to toggle bits in
// the given range

// function to toggle bits
// in the given range
function toggleBitsFromLToR($n, $l, $r)
{

    // calculating a number
    // 'num' having 'r'
    // number of bits and
    // bits in the range l
    // to r are the only
    // set bits
    $num = ((1 << $r) - 1) ^
           ((1 << ($l - 1)) - 1);

    // toggle bits in the
    // range l to r in 'n'
    //Besides this, we can calculate num as: $num=(1<<$r)-$l .
    // and return the number

    return ($n ^ $num);
}

    // Driver Code
    $n = 50;
    $l = 2; $r = 5;
    echo toggleBitsFromLToR($n, $l, $r);

// This code is contributed by anuj_67
?>
```

## java 描述语言

```
<script>

// Javascript implementation to toggle bits in
// the given range

// function to toggle bits in the given range
function toggleBitsFromLToR(n, l, r)
{
    // calculating a number 'num' having 'r'
    // number of bits and bits in the range l
    // to r are the only set bits
    var num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

    // toggle bits in the range l to r in 'n'
    // and return the number
//Besides this, we can calculate num as: num=(1<<r)-l .
    return (n ^ num);
}

// Driver program to test above
var n = 50;
var l = 2, r = 5;
document.write( toggleBitsFromLToR(n, l, r));

</script>
```

输出:

```
44
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。