# 前一个较小的整数，少一个设置位

> 原文:[https://www . geesforgeks . org/previous-small-integer-one-less-number-set-bits/](https://www.geeksforgeeks.org/previous-smaller-integer-one-less-number-set-bits/)

给定一个正整数“n”，其二进制表示中有“x”个设置位。问题是找到先前的较小整数(小于 n 的最大整数)，在其二进制表示中具有(x-1)个设置位。
**注:**1<=**n**T5**例:**

```
Input : 8
Output : 0
(8)<sub>10</sub> = (1000)2
is having 1 set bit.

(0)<sub>10</sub> = (0)2
is having 0 set bit and is the previous smaller.

Input : 25
Output : 24
```

以下是步骤:

1.  在 **n** 的二进制表示中，找到最右边设置位的位置(考虑位置 1 的最后一位，位置 2 的第二个最后一位，以此类推)。让**位置代表**。参考[这篇](https://www.geeksforgeeks.org/position-of-rightmost-set-bit/)帖子。
2.  在**位置**关闭或解除钻头。参考[这篇](https://www.geeksforgeeks.org/how-to-turn-off-a-particular-bit-in-a-number/)帖子。

## C++

```
// C++ implementation to find the previous
// smaller integer with one less number of
// set bits
#include<bits/stdc++.h>
using namespace std;

// function to find the position of
// rightmost set bit.
int getFirstSetBitPos(int n)
{
    return log2(n & -n) + 1;
}

// function to find the previous smaller
// integer
int previousSmallerInteger(int n)
{
    // position of rightmost set bit of n
    int pos = getFirstSetBitPos(n);

    // turn off or unset the bit at
    // position 'pos'
    return (n & ~(1 << (pos - 1)));
}

// Driver program
int main()
{
    int n = 25;
    cout << previousSmallerInteger(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the previous
// smaller integer with one less number of
// set bits
class GFG {

    // function to find the position of
    // rightmost set bit.
    static int getFirstSetBitPos(int n)
    {
        return (int)(Math.log(n & -n) / Math.log(2)) + 1;
    }

    // function to find the previous smaller
    // integer
    static int previousSmallerInteger(int n)
    {

        // position of rightmost set bit of n
        int pos = getFirstSetBitPos(n);

        // turn off or unset the bit at
        // position 'pos'
        return (n & ~(1 << (pos - 1)));
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 25;
        System.out.print("Previous smaller Integer ="
                     + previousSmallerInteger(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 implementation to find
# the previous smaller integer with
# one less number of set bits
import math

# Function to find the position 
# of rightmost set bit.
def getFirstSetBitPos(n):

    return (int)(math.log(n & -n) /
                 math.log(2)) + 1

# Function to find the 
# previous smaller integer
def previousSmallerInteger(n):

    # position of rightmost set bit of n
    pos = getFirstSetBitPos(n)

    # turn off or unset the bit 
    # at position 'pos'
    return (n & ~(1 << (pos - 1)))

# Driver code
n = 25
print("Previous small Integer = ",
       previousSmallerInteger(n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# implementation to find the previous
// smaller integer with one less number of
// set bits
using System;

    class GFG {

    // function to find the position of
    // rightmost set bit.
    static int getFirstSetBitPos(int n)
    {
        return (int)(Math.Log(n & -n) /
                           Math.Log(2)) + 1;
    }

    // function to find the previous smaller
    // integer
    static int previousSmallerInteger(int n)
    {

        // position of rightmost set bit of n
        int pos = getFirstSetBitPos(n);

        // turn off or unset the bit at
        // position 'pos'
        return (n & ~(1 << (pos - 1)));
    }

    // Driver code
    public static void Main()
    {
        int n = 25;

        Console.WriteLine("Previous small Integer ="
                      + previousSmallerInteger(n));
    }
}

// This code is contributed by anant321.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the previous
// smaller integer with one less number of
// set bits

// function to find the position of
// rightmost set bit.

function getFirstSetBitPos($n)
{
    return log($n & -$n) + 1;
}

// function to find the previous
// smaller integer

function previousSmallerInteger($n)
{
    // position of rightmost set bit of n
    $pos = getFirstSetBitPos($n);

    // turn off or unset the bit at
    // position 'pos'
    return ($n & ~(1 << ($pos - 1)));
}

// Driver Code
$n = 25;
echo "Previous smaller Integer = ", previousSmallerInteger($n);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find the previous
// smaller integer with one less number of
// set bits

// function to find the position of
// rightmost set bit.
function getFirstSetBitPos(n)
{
    return parseInt(Math.log(n & -n)/Math.log(2)) + 1;
}

// function to find the previous smaller
// integer
function previousSmallerInteger(n)
{
    // position of rightmost set bit of n
    var pos = getFirstSetBitPos(n);

    // turn off or unset the bit at
    // position 'pos'
    return (n & ~(1 << (pos - 1)));
}

// Driver program
var n = 25;
document.write("Previous smaller Integer = " + previousSmallerInteger(n));

</script>
```

**输出:**

```
Previous smaller integer = 24
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。