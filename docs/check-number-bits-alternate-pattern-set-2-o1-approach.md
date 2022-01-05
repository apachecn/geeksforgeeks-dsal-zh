# 检查一个数字是否有交替模式的位|设置-2 O(1)接近

> 原文:[https://www . geesforgeks . org/check-number-bits-alternate-pattern-set-2-O1-approach/](https://www.geeksforgeeks.org/check-number-bits-alternate-pattern-set-2-o1-approach/)

给定正整数 **n** 。问题是检查这个整数在其二进制表示中是否有替换模式。这里的交替模式是指 **n** 中的置位和未置位以交替顺序出现。例如- 5 具有交替模式，即 101。
如果有替代图案，则打印“是”，否则打印“否”。
**注:** 0 < n.
**例:**

```
Input : 10
Output : Yes
(10)<sub>10</sub> = (1010)2, has an alternate pattern.

Input : 12
Output : No
(12)<sub>10</sub> = (1100)2, does not have an alternate pattern.
```

**简单方法:**在[这篇](https://www.geeksforgeeks.org/check-if-a-number-has-bits-in-alternate-pattern/)帖子中已经讨论过时间复杂度为 O(n)。
**高效方法:**以下是步骤:

1.  计算 **num** = n ^ (n > > 1)。如果 **n** 具有交替模式，那么 **n ^ (n > > 1)** 操作将产生仅具有设定位的数。 **'^'** 是按位异或运算。
2.  检查**号**中的所有位是否都设置好了。参考[这篇](https://www.geeksforgeeks.org/check-bits-number-set/)帖子。

## C++

```
// C++ implementation to check if a number
// has bits in alternate pattern
#include <bits/stdc++.h>

using namespace std;

// function to check if all the bits are set or not
// in the binary representation of 'n'
bool allBitsAreSet(unsigned int n)
{
    // if true, then all bits are set
    if (((n + 1) & n) == 0)
        return true;

    // else all bits are not set
    return false;
}

// function to check if a number
// has bits in alternate pattern
bool bitsAreInAltOrder(unsigned int n)
{
    unsigned int num = n ^ (n >> 1);

    // to check if all bits are set
    // in 'num'
    return allBitsAreSet(num);       
}

// Driver program to test above
int main()
{
    unsigned int n = 10;

    if (bitsAreInAltOrder(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;       
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if a
// number has bits in alternate pattern
class AlternateSetBits
{
    // function to check if all the bits
    // are set or not in the binary
    // representation of 'n'
    static boolean allBitsAreSet(int n)
    {
        // if true, then all bits are set
        if (((n + 1) & n) == 0)
            return true;

        // else all bits are not set
        return false;
    }

    // function to check if a number
    // has bits in alternate pattern
    static boolean bitsAreInAltOrder(int n)
    {
        int num = n ^ (n >>> 1);

        // to check if all bits are set
        // in 'num'
        return allBitsAreSet(num);       
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 10;

        if (bitsAreInAltOrder(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
/* This code is contributed by Danish Kaleem */
```

## 蟒蛇 3

```
# Python implementation to check if a number
# has bits in alternate pattern

# function to check if all the bits are set or not
# in the binary representation of 'n'
def allBitsAreSet(n):

    # if true, then all bits are set
    if (((n + 1) & n) == 0):
        return True;

    # else all bits are not set
    return False;

# function to check if a number
# has bits in alternate pattern
def bitsAreInAltOrder(n):
    num = n ^ (n >> 1);

    # to check if all bits are set
    # in 'num'
    return allBitsAreSet(num);    

# Driver code
n = 10;

if (bitsAreInAltOrder(n)):
    print("Yes");
else:
    print("No");

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation to check if a
// number has bits in alternate pattern
using System;

class GFG {

    // function to check if all the bits
    // are set or not in the binary
    // representation of 'n'
    static bool allBitsAreSet(int n)
    {
        // if true, then all bits are set
        if (((n + 1) & n) == 0)
            return true;

        // else all bits are not set
        return false;
    }

    // function to check if a number
    // has bits in alternate pattern
    static bool bitsAreInAltOrder(int n)
    {
        int num = n ^ (n >> 1);

        // to check if all bits are set
        // in 'num'
        return allBitsAreSet(num);
    }

    // Driver Code
    public static void Main()
    {
        int n = 10;

        if (bitsAreInAltOrder(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }

}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// if a number has bits in
// alternate pattern

// function to check if all the
// bits are set or not in the
// binary representation of 'n'
function allBitsAreSet($n)
{
    // if true, then all
    // bits are set
    if ((($n + 1) & $n) == 0)
        return true;

    // else all bits are not set
    return false;
}

// function to check if a number
// has bits in alternate pattern
function bitsAreInAltOrder($n)
{
        $num = $n ^ ($n >> 1);

    // to check if all bits
    // are set in 'num'
    return allBitsAreSet($num);
}

// Driver Code
$n = 10;

if (bitsAreInAltOrder($n))
    echo "Yes";
else
    echo "No";

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// Javascript implementation to check if a
// number has bits in alternate pattern

    // function to check if all the bits
    // are set or not in the binary
    // representation of 'n'
     function allBitsAreSet(n)
    {
        // if true, then all bits are set
        if (((n + 1) & n) == 0)
            return true;

        // else all bits are not set
        return false;
    }

    // function to check if a number
    // has bits in alternate pattern
   function bitsAreInAltOrder(n)
    {
        let num = n ^ (n >>> 1);

        // to check if all bits are set
        // in 'num'
        return allBitsAreSet(num);       
    }

// driver function

        let n = 10;

        if (bitsAreInAltOrder(n))
            document.write("Yes");
        else
            document.write("No");

 // This code is contributed by code_hunt.
</script>   
```

**输出:**

```
Yes
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。