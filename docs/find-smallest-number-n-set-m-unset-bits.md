# 用 n 个置位和 m 个未置位的位找到最小的数

> 原文:[https://www . geesforgeks . org/find-minist-number-n-set-m-unset-bits/](https://www.geeksforgeeks.org/find-smallest-number-n-set-m-unset-bits/)

给定两个非负数 **n** 和 **m** 。问题是找到最小的数，在其二进制表示中具有 **n** 个设置位和 **m** 个未设置位。
**约束:** 1 < = n，0 < = m，(m+n) < = 31
**注:**二进制表示中前导 1(或最左边 1)前的 0 位计数

示例:

```
Input : n = 2, m = 2
Output : 9
(9)<sub>10</sub> = (1001)2
We can see that in the binary representation of 9 
there are 2 set and 2 unsets bits and it is the
smallest number. 

Input : n = 4, m = 1
Output : 23
```

**进场:**以下是步骤:

1.  计算**数**=(1<<(n+m))–1。这将产生具有 **(n + m)** 比特数的数字**数**，并且所有比特都被设置。
2.  现在，在**编号**中从 **n** 到 **(n+m-1)** 的范围内切换位，即从最右边的第**n**位切换位到最右边的第 **(n+m-1)个**位，然后返回切换后的编号。参考[这个](https://www.geeksforgeeks.org/toggle-bits-given-range/)岗位。

## C++

```
// C++ implementation to find the smallest number
// with n set and m unset bits
#include <bits/stdc++.h>

using namespace std;

// function to toggle bits in the given range
unsigned int toggleBitsFromLToR(unsigned int n,
                                unsigned int l,
                                unsigned int r)
{
    // for invalid range
    if (r < l)
        return n;

    // calculating a number 'num' having 'r'
    // number of bits and bits in the range l
    // to r are the only set bits
    int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

    // toggle bits in the range l to r in 'n'
    // and return the number
    return (n ^ num);
}

// function to find the smallest number
// with n set and m unset bits
unsigned int smallNumWithNSetAndMUnsetBits(unsigned int n,
                                           unsigned int m)
{
    // calculating a number 'num' having '(n+m)' bits
    // and all are set
    unsigned int num = (1 << (n + m)) - 1;

    // required smallest number
    return toggleBitsFromLToR(num, n, n + m - 1);
}

// Driver program to test above
int main()
{
    unsigned int n = 2, m = 2;
    cout << smallNumWithNSetAndMUnsetBits(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the smallest number
// with n set and m unset bits

class GFG
{
    // Function to toggle bits in the given range
    static int toggleBitsFromLToR(int n, int l, int r)
    {
        // for invalid range
        if (r < l)
            return n;

        // calculating a number 'num' having 'r'
        // number of bits and bits in the range l
        // to r are the only set bits
        int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

        // toggle bits in the range l to r in 'n'
        // and return the number
        return (n ^ num);
    }

    // Function to find the smallest number
    // with n set and m unset bits
    static int smallNumWithNSetAndMUnsetBits(int n, int m)
    {
        // calculating a number 'num' having '(n+m)' bits
        // and all are set
        int num = (1 << (n + m)) - 1;

        // required smallest number
        return toggleBitsFromLToR(num, n, n + m - 1);
    }

    // driver program
    public static void main (String[] args)
    {
        int n = 2, m = 2;
        System.out.println(smallNumWithNSetAndMUnsetBits(n, m));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 implementation to find
# the smallest number with n set
# and m unset bits

# function to toggle bits in the
# given range
def toggleBitsFromLToR(n, l, r):

    # for invalid range
    if (r < l):
        return n

    # calculating a number 'num'
    # having 'r' number of bits
    # and bits in the range l
    # to r are the only set bits
    num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1)

    # toggle bits in the range
    # l to r in 'n' and return the number
    return (n ^ num)

# function to find the smallest number
# with n set and m unset bits
def smallNumWithNSetAndMUnsetBits(n, m):

    # calculating a number 'num' having
    # '(n+m)' bits and all are set
    num = (1 << (n + m)) - 1

    # required smallest number
    return toggleBitsFromLToR(num, n, n + m - 1);

# Driver program to test above
n = 2
m = 2

ans = smallNumWithNSetAndMUnsetBits(n, m)
print (ans)

# This code is contributed by Saloni Gupta
```

## C#

```
// C# implementation to find the smallest number
// with n set and m unset bits
using System;

class GFG
{
    // Function to toggle bits in the given range
    static int toggleBitsFromLToR(int n, int l, int r)
    {
        // for invalid range
        if (r < l)
            return n;

        // calculating a number 'num' having 'r'
        // number of bits and bits in the range l
        // to r are the only set bits
        int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

        // toggle bits in the range l to r in 'n'
        // and return the number
        return (n ^ num);
    }

    // Function to find the smallest number
    // with n set and m unset bits
    static int smallNumWithNSetAndMUnsetBits(int n, int m)
    {
        // calculating a number 'num' having '(n+m)' bits
        // and all are set
        int num = (1 << (n + m)) - 1;

        // required smallest number
        return toggleBitsFromLToR(num, n, n + m - 1);
    }

    // Driver program
    public static void Main ()
    {
        int n = 2, m = 2;
        Console.Write(smallNumWithNSetAndMUnsetBits(n, m));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP  implementation to find the smallest number
// with n set and m unset bits

// function to toggle bits in the given range

function toggleBitsFromLToR($n,$l,$r)
{
    // for invalid range
    if ($r < $l)
        return $n;

    // calculating a number 'num' having 'r'
    // number of bits and bits in the range l
    // to r are the only set bits
    $num = ((1 << $r) - 1) ^ ((1 << ($l - 1)) - 1);

    // toggle bits in the range l to r in 'n'
    // and return the number
    return ($n ^ $num);
}

// function to find the smallest number
// with n set and m unset bits
function smallNumWithNSetAndMUnsetBits($n, $m)
{
    // calculating a number 'num' having '(n+m)' bits
    // and all are set
    $num = (1 << ($n + $m)) - 1;

    // required smallest number
    return toggleBitsFromLToR($num, $n, $n + $m - 1);
}

// Driver program to test above
     $n = 2; $m = 2;
     echo  smallNumWithNSetAndMUnsetBits($n, $m);

// This Code is Contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find
// the smallest number with n set and
// m unset bits

// Function to toggle bits in the given range
function toggleBitsFromLToR(n, l, r)
{

    // For invalid range
    if (r < l)
        return n;

    // Calculating a number 'num' having 'r'
    // number of bits and bits in the range l
    // to r are the only set bits
    let num = ((1 << r) - 1) ^
              ((1 << (l - 1)) - 1);

    // Toggle bits in the range l to r in 'n'
    // and return the number
    return (n ^ num);
}

// Function to find the smallest number
// with n set and m unset bits
function smallNumWithNSetAndMUnsetBits(n, m)
{

    // Calculating a number 'num' having
    // '(n+m)' bits and all are set
    let num = (1 << (n + m)) - 1;

    // Required smallest number
    return toggleBitsFromLToR(num, n, n + m - 1);
}

// Driver code
let n = 2, m = 2;

document.write(smallNumWithNSetAndMUnsetBits(n, m));

// This code is contributed by suresh07

</script>
```

**输出:**

```
9
```

对于 **n** 和 **m** 的较大值，可以使用**长 int** 和**长 int** 数据类型来生成所需的数字。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。