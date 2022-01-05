# 在给定范围内取消设置位

> 原文:[https://www.geeksforgeeks.org/unset-bits-given-range/](https://www.geeksforgeeks.org/unset-bits-given-range/)

给定一个非负数 **n** 和两个值 **l** 和 **r** 。问题是在 **n** 的二进制表示中 **l** 到 **r** 范围内的位不设置，即从最右边的 **lth** 位到最右边的 **rth** 位不设置位。
**约束:** 1 < = l < = r < =二进制表示的位数 **n** 。
示例:

```
Input : n = 42, l = 2, r = 5
Output : 32
(42)<sub>10</sub> = (101010)2
(32)<sub>10</sub> = (100000)2
The bits in the range 2 to 5 in the binary
representation of 42 have been unset.

Input : n = 63, l = 1, r = 4
Output : 48
```

**进场:**以下为步骤:

1.  计算**数**=(1<<(sizeof(int)* 8–1))–1。这将产生最高正整数**数**。 **num** 中的所有位都将被设置。
2.  在**编号**中的 **l** 至 **r** 范围内切换钻头。参考[这个](https://www.geeksforgeeks.org/toggle-bits-given-range/)岗位。
3.  现在，执行 **n = n & num** 。这将解除 **l** 至 **r** 范围内 **n** 的位。
4.  返回 **n** 。

**注意:****大小为(int)** 已被用作输入为 **int** 数据类型。对于大输入，您可以使用**长 int** 或**长 int** 数据类型来代替 **int** 。

## C++

```
// C++ implementation to unset bits in the given range
#include<bits/stdc++.h>
using namespace std;

// Function to toggle bits in the given range
int toggleBitsFromLToR(int n, int l, int r)
{
    // calculating a number 'num' having 'r' number of bits
    // and bits in the range l to r are the only set bits
    int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

    // toggle the bits in the range l to r in 'n'
    // and return the number
    return (n ^ num);
}

// Function to unset bits in the given range
int unsetBitsInGivenRange(int n, int l, int r)
{
    // 'num' is the highest positive integer number
    // all the bits of 'num' are set
    long num = (1ll << (4 * 8 - 1)) - 1;

    // toggle the bits in the range l to r in 'num'
    num = toggleBitsFromLToR(num, l, r);

    // unset the bits in the range l to r in 'n'
    // and return the number
    return (n & num);
}

// driver program
int main()
{
    int n = 42;
    int l = 2, r = 5;
    cout<< unsetBitsInGivenRange(n, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to unset bits in the given range
import java.io.*;

class GFG
{
    // Function to toggle bits in the given range
    static int toggleBitsFromLToR(int n, int l, int r)
    {
        // calculating a number 'num' having 'r' number of bits
        // and bits in the range l to r are the only set bits
        int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

        // toggle the bits in the range l to r in 'n'
        // and return the number
        return (n ^ num);
    }

    // Function to unset bits in the given range
    static int unsetBitsInGivenRange(int n, int l, int r)
    {
        // 'num' is the highest positive integer number
        // all the bits of 'num' are set
        int num = (1 << (4 * 8 - 1)) - 1;

        // toggle the bits in the range l to r in 'num'
        num = toggleBitsFromLToR(num, l, r);

        // unset the bits in the range l to r in 'n'
        // and return the number
        return (n & num);
    }

    // driver program
    public static void main (String[] args)
    {
        int n = 42;
        int l = 2, r = 5;
        System.out.println(unsetBitsInGivenRange(n, l, r));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# python implementation to unset bits
# in the given range

# Function to toggle bits in the
# given range
def toggleBitsFromLToR(n, l, r):

    # calculating a number 'num'
    # having 'r' number of bits
    # and bits in the range l to
    # r are the only set bits
    num = (((1 << r) - 1) ^
           ((1 << (l - 1)) - 1))

    # toggle the bits in the range
    # l to r in 'n' and return the
    # number
    return (n ^ num)

# Function to unset bits in the
# given range
def unsetBitsInGivenRange(n, l, r):

    # 'num' is the highest positive
    # integer number all the bits
    # of 'num' are set
    num = (1 << (4 * 8 - 1)) - 1

    # toggle the bits in the range
    # l to r in 'num'
    num = toggleBitsFromLToR(num, l, r)

    # unset the bits in the range
    # l to r in 'n' and return the
    # number
    return (n & num)

# Driver code   
n = 42
l = 2
r = 5
print(unsetBitsInGivenRange(n, l, r))

# This code is contributed by Sam007.
```

## C#

```
// C#  implementation to unset
// bits in the given range
using System;

class GFG {

    // Function to toggle bits in the given range
    static int toggleBitsFromLToR(int n, int l, int r)
    {
        // calculating a number 'num'
        // having 'r' number of bits
        // and bits in the range l
        // to r are the only set bits
        int num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

        // toggle the bits in the
        // range l to r in 'n'
        // and return the number
        return (n ^ num);
    }

    // Function to unset bits in the given range
    static int unsetBitsInGivenRange(int n, int l, int r)
    {
        // 'num' is the highest
        // positive integer number
        // all the bits of 'num'
        // are set
        int num = (1 << (2 * 8 - 1)) - 1;

        // toggle the bits in
        // the range l to r in 'num'
        num = toggleBitsFromLToR(num, l, r);

        // unset the bits in
        // the range l to r in 'n'
        // and return the number
        return (n & num);
    }

// Driver Code
static public void Main() {

    int n = 42;
    int l = 2, r = 5;
    Console.WriteLine(unsetBitsInGivenRange(n, l, r));
}
}

// This Code is  Contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to unset
// bits in the given range

    // Function to toggle bits
    // in the given range
    function toggleBitsFromLToR($n, $l, $r)
    {

        // calculating a number 'num'
        // having 'r' number of bits
        // and bits in the range l to
        // r are the only set bits
        $num = ((1 << $r) - 1) ^
               ((1 << ($l - 1)) - 1);

        // toggle the bits in the
        // range l to r in 'n'
        // and return the number
        return ($n ^ $num);
    }

    // Function to unset bits
    // in the given range
    function unsetBitsInGivenRange($n,$l,$r)
    {

        // 'num' is the highest
        // positive integer number
        // all the bits of 'num' are set
        $num = (1 << (4 * 8 - 1)) - 1;

        // toggle the bits in the
        // range l to r in 'num'
        $num = toggleBitsFromLToR($num, $l, $r);

        // unset the bits in the
        // range l to r in 'n'
        // and return the number
        return ($n & $num);
    }

        // Driver Code
        $n = 42;
        $l = 2;
        $r = 5;
        echo unsetBitsInGivenRange($n, $l, $r);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript implementation to unset bits in the given range

    // Function to toggle bits in the given range
    function toggleBitsFromLToR(n, l, r)
    {
        // calculating a number 'num'
        // having 'r' number of bits
        // and bits in the range l
        // to r are the only set bits
        let num = ((1 << r) - 1) ^ ((1 << (l - 1)) - 1);

        // toggle the bits in the
        // range l to r in 'n'
        // and return the number
        return (n ^ num);
    }

    // Function to unset bits in the given range
    function unsetBitsInGivenRange(n, l, r)
    {
        // 'num' is the highest
        // positive integer number
        // all the bits of 'num'
        // are set
        let num = (1 << (2 * 8 - 1)) - 1;

        // toggle the bits in
        // the range l to r in 'num'
        num = toggleBitsFromLToR(num, l, r);

        // unset the bits in
        // the range l to r in 'n'
        // and return the number
        return (n & num);
    }

    let n = 42;
    let l = 2, r = 5;
    document.write(unsetBitsInGivenRange(n, l, r));

</script>
```

输出:

```
32
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。