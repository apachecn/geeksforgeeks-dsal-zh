# 获取最右边未置位位的位置

> 原文:[https://www . geesforgeks . org/get-position-最右侧-unset-bit/](https://www.geeksforgeeks.org/get-position-rightmost-unset-bit/)

给定一个非负数 **n** 。在 **n** 的二进制表示中找到最右边未设置位的位置，考虑位置 1 的最后一位，位置 2 的第二个最后一位，以此类推。如果 **n** 的二进制表示中没有**0**。然后打印“-1”。
示例:

```
Input : n = 9
Output : 2
(9)<sub>10</sub> = (1001)2
The position of rightmost unset bit in the binary
representation of 9 is 2.

Input : n = 32
Output : 1
```

**进场:**以下为步骤:

1.  如果 **n** = 0，返回 1。
2.  如果 **n** 的所有位都被置位，返回-1。参考[这篇](https://www.geeksforgeeks.org/check-bits-number-set/)帖子。
3.  否则对给定的数字执行按位非运算(相当于 1 的补码的运算)。让它成为 **num** = ~n。
4.  获取**号**最右边设定位的[位置。这将是 **n** 最右边未置位的位置。](https://www.geeksforgeeks.org/position-of-rightmost-set-bit/)

## C++

```
// C++ implementation to get the position of rightmost unset bit
#include <bits/stdc++.h>

using namespace std;

// function to find the position
// of rightmost set bit
int getPosOfRightmostSetBit(int n)
{
    return log2(n&-n)+1;
}

// function to get the position of rightmost unset bit
int getPosOfRightMostUnsetBit(int n)
{
    // if n = 0, return 1
    if (n == 0)
        return 1;

    // if all bits of 'n' are set
    if ((n & (n + 1)) == 0)   
        return -1;

    // position of rightmost unset bit in 'n'
    // passing ~n as argument
    return getPosOfRightmostSetBit(~n);       
}

// Driver program to test above
int main()
{
    int n = 9;
    cout << getPosOfRightMostUnsetBit(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to get the
// position of rightmost unset bit

class GFG {

// function to find the position
// of rightmost set bit
static int getPosOfRightmostSetBit(int n)
{
    return (int)((Math.log10(n & -n)) / Math.log10(2)) + 1;
}

// function to get the position
// of rightmost unset bit
static int getPosOfRightMostUnsetBit(int n) {

    // if n = 0, return 1
    if (n == 0)
    return 1;

    // if all bits of 'n' are set
    if ((n & (n + 1)) == 0)
    return -1;

    // position of rightmost unset bit in 'n'
    // passing ~n as argument
    return getPosOfRightmostSetBit(~n);
}

// Driver code
public static void main(String arg[])
{
    int n = 9;
    System.out.print(getPosOfRightMostUnsetBit(n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 implementation to get the position
# of rightmost unset bit

# import library
import math as m

# function to find the position
# of rightmost set bit
def getPosOfRightmostSetBit(n):

    return (m.log(((n & - n) + 1),2))

# function to get the position ot rightmost unset bit
def getPosOfRightMostUnsetBit(n):

    # if n = 0, return 1
    if (n == 0):
        return 1

    # if all bits of 'n' are set
    if ((n & (n + 1)) == 0):
        return -1

    # position of rightmost unset bit in 'n'
    # passing ~n as argument
    return getPosOfRightmostSetBit(~n)   

# Driver program to test above
n = 13;
ans = getPosOfRightMostUnsetBit(n)

#rounding the final answer
print (round(ans))

# This code is contributed by Saloni Gupta.
```

## C#

```
// C# implementation to get the
// position of rightmost unset bit
using System;

class GFG
{
    // function to find the position
    // of rightmost set bit
    static int getPosOfRightmostSetBit(int n)
    {
        return (int)((Math.Log10(n & -n)) / Math.Log10(2)) + 1;
    }

    // function to get the position
    // of rightmost unset bit
    static int getPosOfRightMostUnsetBit(int n) {

        // if n = 0, return 1
        if (n == 0)
        return 1;

        // if all bits of 'n' are set
        if ((n & (n + 1)) == 0)
        return -1;

        // position of rightmost unset bit in 'n'
        // passing ~n as argument
        return getPosOfRightmostSetBit(~n);
    }

    // Driver code
    public static void Main()
    {
        int n = 9;
        Console.Write(getPosOfRightMostUnsetBit(n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to get the
// position of rightmost unset bit

// function to find the position
// of rightmost set bit
function getPosOfRightmostSetBit( $n)
{
    return ceil(log($n &- $n) + 1);
}

// function to get the position
// of rightmost unset bit
function getPosOfRightMostUnsetBit( $n)
{
    // if n = 0, return 1
    if ($n == 0)
        return 1;

    // if all bits of 'n' are set
    if (($n & ($n + 1)) == 0)
        return -1;

    // position of rightmost unset bit in 'n'
    // passing ~n as argument
    return getPosOfRightmostSetBit(~$n);    
}

    // Driver Code
    $n = 9;
    echo getPosOfRightMostUnsetBit($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// JavaScript implementation to get the position of rightmost unset bit

// function to find the position
// of rightmost set bit
function getPosOfRightmostSetBit(n)
{
    return Math.log2(n&-n)+1;
}

// function to get the position of rightmost unset bit
function getPosOfRightMostUnsetBit(n)
{

    // if n = 0, return 1
    if (n == 0)
        return 1;

    // if all bits of 'n' are set
    if ((n & (n + 1)) == 0)   
        return -1;

    // position of rightmost unset bit in 'n'
    // passing ~n as argument
    return getPosOfRightmostSetBit(~n);       
}

// Driver program to test above
    let n = 9;
    document.write(getPosOfRightMostUnsetBit(n));

// This code is contributed by Manoj.
</script>
```

输出:

```
2
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。