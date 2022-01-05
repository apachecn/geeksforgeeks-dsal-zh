# 具有多一个设定位的下一个较大整数

> 原文:[https://www . geesforgeks . org/next-greater-integer-one-number-set-bits/](https://www.geeksforgeeks.org/next-greater-integer-one-number-set-bits/)

给定一个正整数“n”，其二进制表示中有“x”个设置位。问题是找到下一个更大的整数(大于 n 的最小整数)，在其二进制表示中有(x+1)个设置位。
**例:**

```
Input : 10
Output : 11
(10)<sub>10</sub> = (1010)2
is having 2 set bits.

(11)<sub>10</sub> = (1011)2
is having 3 set bits and is the next greater.

Input : 39
Output : 47
```

**进场:**以下是步骤:

1.  在 **n** 的二进制表示中找到最右边未设置位的位置(考虑位置 0 的最后一位、位置 1 的第二个最后一位等等)。
2.  让位置用**位置**表示。
3.  将钻头设置在**位置**。参考[这篇](https://www.geeksforgeeks.org/set-k-th-bit-given-number/)帖子。
4.  如果二进制表示中没有未设置的位，则对给定的数字执行按位左移 1，然后再加 1。

**如何获取最右边未置位位的位置？**

1.  对给定的数字执行按位非运算(相当于 1 的补码的运算)。让它成为 **num** = ~n。
2.  获取**号**最右边设定位的[位置。](https://www.geeksforgeeks.org/position-of-rightmost-set-bit/)

## C++

```
// C++ implementation to find the next greater integer
// with one more number of set bits
#include <bits/stdc++.h>

using namespace std;

// function to find the position of rightmost
// set bit. Returns -1 if there are no set bits
int getFirstSetBitPos(int n)
{
    return (log2(n&-n)+1) - 1;
}

// function to find the next greater integer
int nextGreaterWithOneMoreSetBit(int n)
{
    // position of rightmost unset bit of n
    // by passing ~n as argument
    int pos = getFirstSetBitPos(~n);

    // if n consists of unset bits, then
    // set the rightmost unset bit
    if (pos > -1)
        return (1 << pos) | n;

    //n does not consists of unset bits   
    return ((n << 1) + 1);   
}

// Driver program to test above
int main()
{
    int n = 10;
    cout << "Next greater integer = "
          << nextGreaterWithOneMoreSetBit(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the next greater integer
// with one more number of set bits
class GFG {

    // function to find the position of rightmost
    // set bit. Returns -1 if there are no set bits
    static int getFirstSetBitPos(int n)
    {
        return ((int)(Math.log(n & -n) / Math.log(2)) + 1) - 1;
    }

    // function to find the next greater integer
    static int nextGreaterWithOneMoreSetBit(int n)
    {

        // position of rightmost unset bit of n
        // by passing ~n as argument
        int pos = getFirstSetBitPos(~n);

        // if n consists of unset bits, then
        // set the rightmost unset bit
        if (pos > -1)
            return (1 << pos) | n;

        // n does not consists of unset bits
        return ((n << 1) + 1);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 10;
        System.out.print("Next greater integer = "
                + nextGreaterWithOneMoreSetBit(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 implementation to find
# the next greater integer with
# one more number of set bits
import math

# Function to find the position
# of rightmost set bit. Returns -1
# if there are no set bits
def getFirstSetBitPos(n):

    return ((int)(math.log(n & -n) /
                  math.log(2)) + 1) - 1

# Function to find the next greater integer
def nextGreaterWithOneMoreSetBit(n):

    # position of rightmost unset bit of
    # n by passing ~n as argument
    pos = getFirstSetBitPos(~n)

    # if n consists of unset bits, then
    # set the rightmost unset bit
    if (pos > -1):
        return (1 << pos) | n

    # n does not consists of unset bits
    return ((n << 1) + 1)

# Driver code
n = 10
print("Next greater integer = ",
       nextGreaterWithOneMoreSetBit(n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# implementation to find the next greater
// integer with one more number of set bits
using System;

class GFG {

    // function to find the position of rightmost
    // set bit. Returns -1 if there are no set bits
    static int getFirstSetBitPos(int n)
    {
        return ((int)(Math.Log(n & -n) / Math.Log(2))
                                            + 1) - 1;
    }

    // function to find the next greater integer
    static int nextGreaterWithOneMoreSetBit(int n)
    {

        // position of rightmost unset bit of n
        // by passing ~n as argument
        int pos = getFirstSetBitPos(~n);

        // if n consists of unset bits, then
        // set the rightmost unset bit
        if (pos > -1)
            return (1 << pos) | n;

        // n does not consists of unset bits   
        return ((n << 1) + 1);   
    }

    // Driver code
    public static void Main()
    {
        int n = 10;

        Console.Write("Next greater integer = "
              + nextGreaterWithOneMoreSetBit(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the
// next greater integer with
// one more number of set bits

// function to find the position
// of rightmost set bit. Returns
// -1 if there are no set bits

function getFirstSetBitPos($n)
{
    return (log($n & -$n + 1)) - 1;
}

// function to find the
// next greater integer

function nextGreaterWithOneMoreSetBit($n)
{
    // position of rightmost unset bit of n
    // by passing ~n as argument

    $pos = getFirstSetBitPos(~$n);

    // if n consists of unset bits, then
    // set the rightmost unset bit
    if ($pos > -1)
        return (1 << $pos) | $n;

    //n does not consists of unset bits
    return (($n << 1) + 1);
}

// Driver Code
$n = 10;
echo "Next greater integer = ",
    nextGreaterWithOneMoreSetBit($n);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the next greater integer
// with one more number of set bits

// function to find the position of rightmost
// set bit. Returns -1 if there are no set bits
function getFirstSetBitPos(n)
{
    return (parseInt(Math.log(n&-n)/Math.log(2))+1) - 1;
}

// function to find the next greater integer
function nextGreaterWithOneMoreSetBit(n)
{
    // position of rightmost unset bit of n
    // by passing ~n as argument
    var pos = getFirstSetBitPos(~n);

    // if n consists of unset bits, then
    // set the rightmost unset bit
    if (pos > -1)
        return (1 << pos) | n;

    //n does not consists of unset bits    
    return ((n << 1) + 1);    
}

// Driver program to test above
var n = 10;
document.write("Next greater integer = " + nextGreaterWithOneMoreSetBit(n));

</script>
```

**输出:**

```
Next greater integer = 11
```

***时间复杂度:** O(log(log N))*
***辅助空间:** O(1)*

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。