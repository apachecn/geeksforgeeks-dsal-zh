# 设置最右边的未设置位

> 原文:[https://www.geeksforgeeks.org/set-rightmost-unset-bit/](https://www.geeksforgeeks.org/set-rightmost-unset-bit/)

给定一个非负数 **n** 。问题是设置 **n** 的二进制表示中最右边的未设置位。如果没有未设置的位，那么就保持数字不变。

**示例:**

```
Input : 21
Output : 23
(21)<sub>10</sub> = (10101)2
Rightmost unset bit is at position 2(from right) as 
highlighted in the binary representation of 21.
(23)10 = (10111)2
The bit at position 2 has been set.

Input : 15
Output : 15
```

**进场:**以下是步骤:

1.  如果 **n** = 0，返回 1。
2.  如果 **n** 位全部置位，返回 n，参见[本](https://www.geeksforgeeks.org/check-bits-number-set/)帖。
3.  否则对给定的数字执行按位非运算(相当于 1 的补码的运算)。让它成为 **num** = ~n。
4.  获取**号**最右边设定位的[位置。让位置为**位置**。](https://www.geeksforgeeks.org/position-of-rightmost-set-bit/)
5.  返回 **(1 < <(位置–1))| n**。

## C++

```
// C++ implementation to set the rightmost unset bit
#include <bits/stdc++.h>
using namespace std;

// function to find the position
// of rightmost set bit
int getPosOfRightmostSetBit(int n)
{
    return log2(n&-n)+1;
}

int setRightmostUnsetBit(int n)
{
    // if n = 0, return 1
    if (n == 0)
        return 1;

    // if all bits of 'n' are set
    if ((n & (n + 1)) == 0)   
        return n;

    // position of rightmost unset bit in 'n'
    // passing ~n as argument
    int pos = getPosOfRightmostSetBit(~n);   

    // set the bit at position 'pos'
    return ((1 << (pos - 1)) | n);
}

// Driver program to test above
int main()
{
    int n = 21;
    cout << setRightmostUnsetBit(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to set
// the rightmost unset bit

class GFG {

// function to find the position
// of rightmost set bit
static int getPosOfRightmostSetBit(int n)
{
    return (int)((Math.log10(n & -n)) / (Math.log10(2))) + 1;
}

static int setRightmostUnsetBit(int n)
{
    // if n = 0, return 1
    if (n == 0)
    return 1;

    // if all bits of 'n' are set
    if ((n & (n + 1)) == 0)
    return n;

    // position of rightmost unset bit in 'n'
    // passing ~n as argument
    int pos = getPosOfRightmostSetBit(~n);

    // set the bit at position 'pos'
    return ((1 << (pos - 1)) | n);
}

// Driver code
public static void main(String arg[]) {
    int n = 21;
    System.out.print(setRightmostUnsetBit(n));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 implementation to
# set the rightmost unset bit
import math

# function to find the position
# of rightmost set bit
def getPosOfRightmostSetBit(n):

    return int(math.log2(n&-n)+1)

def setRightmostUnsetBit(n):

    # if n = 0, return 1
    if (n == 0):
        return 1

    # if all bits of 'n' are set
    if ((n & (n + 1)) == 0):   
        return n

    # position of rightmost unset bit in 'n'
    # passing ~n as argument
    pos = getPosOfRightmostSetBit(~n)   

    # set the bit at position 'pos'
    return ((1 << (pos - 1)) | n)

# Driver code

n = 21
print(setRightmostUnsetBit(n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# implementation to set
// the rightmost unset bit
using System;

class GFG{

// Function to find the position
// of rightmost set bit
static int getPosOfRightmostSetBit(int n)
{
    return (int)((Math.Log10(n & -n)) /
                 (Math.Log10(2))) + 1;
}

static int setRightmostUnsetBit(int n)
{

    // If n = 0, return 1
    if (n == 0)
        return 1;

    // If all bits of 'n' are set
    if ((n & (n + 1)) == 0)
        return n;

    // Position of rightmost unset bit in 'n'
    // passing ~n as argument
    int pos = getPosOfRightmostSetBit(~n);

    // Set the bit at position 'pos'
    return ((1 << (pos - 1)) | n);
}

// Driver code
public static void Main(String []arg)
{
    int n = 21;

    Console.Write(setRightmostUnsetBit(n));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript implementation to set
// the rightmost unset bit

    // function to find the position
    // of rightmost set bit
    function getPosOfRightmostSetBit(n)
    {
        return ((Math.log10(n & -n)) / (Math.log10(2))) + 1;
    }

    function setRightmostUnsetBit(n)
    {
        // if n = 0, return 1
    if (n == 0)
        return 1;

    // if all bits of 'n' are set
    if ((n & (n + 1)) == 0)
        return n;

    // position of rightmost unset bit in 'n'
    // passing ~n as argument
    let pos = getPosOfRightmostSetBit(~n);

    // set the bit at position 'pos'
    return ((1 << (pos - 1)) | n);
    }

    // Driver code
    let n = 21;
    document.write(setRightmostUnsetBit(n));

// This code is contributed by unknown2108

</script>
```

**输出:**

```
23
```

**替代实现**
想法是使用 [Integer.toBinaryString()](https://www.geeksforgeeks.org/java-lang-integer-tobinarystring-method/)

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.Scanner;

public class SetMostRightUnsetBit {
    public static void main(String args[])
    {
        int a = 21;
        setMostRightUnset(a);
    }

    private static void setMostRightUnset(int a)
    {
        // will get a number with all set bits except the
        // first set bit
        int x = a ^ (a - 1);
        System.out.println(Integer.toBinaryString(x));

        // We reduce it to the number with single 1's on
        // the position of first set bit in given number
        x = x & a;
        System.out.println(Integer.toBinaryString(x));

        // Move x on right by one shift to make OR
        // operation and make first rightest unset bit 1
        x = x >> 1;

        int b = a | x;

        System.out.println("before setting bit " +
                               Integer.toBinaryString(a));
        System.out.println("after setting bit " +
                               Integer.toBinaryString(b));
    }
}
```

## 蟒蛇 3

```
def setMostRightUnset(a):

    # Will get a number with all set
    # bits except the first set bit
    x = a ^ (a - 1)
    print(bin(x)[2:])

    # We reduce it to the number with
    # single 1's on the position of
    # first set bit in given number
    x = x & a
    print(bin(x)[2:])

    # Move x on right by one shift to
    # make OR operation and make first
    # rightest unset bit 1
    x = x >> 1

    b = a | x

    print("before setting bit ", bin(a)[2:])
    print("after setting bit ", bin(b)[2:])

# Driver Code
if __name__ == '__main__':

    a = 21

    setMostRightUnset(a)

# This code is contributed by mohit kumar 29
```

## C#

```
using System;

class SetMostRightUnsetBit{

// Driver Code
public static void Main(String []args)
{
    int a = 21;
    setMostRightUnset(a);
}

private static void setMostRightUnset(int a)
{

    // will get a number with all set bits
    // except the first set bit
    int x = a ^ (a - 1);
    Console.WriteLine(Convert.ToString(x));

    // We reduce it to the number with single 1's on
    // the position of first set bit in given number
    x = x & a;
    Console.WriteLine(Convert.ToString(x));

    // Move x on right by one shift to make OR
    // operation and make first rightest unset bit 1
    x = x >> 1;

    int b = a | x;

    Console.WriteLine("before setting bit " +
    Convert.ToString(a, 2));
    Console.WriteLine("after setting bit " +
    Convert.ToString(b, 2));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    function setMostRightUnset(a)
    {
        // will get a number with all set bits except the
        // first set bit
        let x = a ^ (a - 1);
        document.write((x >>> 0).toString(2)+"<br>");

        // We reduce it to the number with single 1's on
        // the position of first set bit in given number
        x = x & a;
        document.write((x >>> 0).toString(2)+"<br>");

        // Move x on right by one shift to make OR
        // operation and make first rightest unset bit 1
        x = x >> 1;

        let b = a | x;

        document.write("before setting bit " +
                               (a >>> 0).toString(2)+"<br>");
        document.write("after setting bit " +
                               (b >>> 0).toString(2)+"<br>");
    }

    let a = 21;
    setMostRightUnset(a);

// This code is contributed by patel2127
</script>
```

**输出:**

```
1
1
before setting bit 10101
after setting bit 10101
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。