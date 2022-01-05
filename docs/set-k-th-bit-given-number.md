# 设置给定数字的第 K 位

> 原文:[https://www.geeksforgeeks.org/set-k-th-bit-given-number/](https://www.geeksforgeeks.org/set-k-th-bit-given-number/)

给定一个数字 n 和值 k。从右边开始，设置 n 的二进制表示中的第 k 位。LSB(或最后一位)的位置是 0，第二个最后一位是 1，依此类推。还有，0 <= k < x, where x is the number of bits in the binary representation of n.
**例:**

```
Input : n = 10, k = 2
Output : 14
(10)<sub>10</sub> = (1010)2
Now, set the 2nd bit from right.
(14)<sub>10</sub> = (1110)2
2nd bit has been set.

Input : n = 15, k = 3
Output : 15
3rd bit of 15 is already set.
```

要设置任何位，我们使用按位或|运算符。正如我们已经知道的，如果操作数的任何对应位被置位(1)，按位 OR |运算符会将结果的每个位计算为 1。为了设置一个数字的第 k 位，我们需要向左移位 1 k 次，然后用之前执行的左移的数字和结果执行按位“或”运算。

```
                            In general, (1 << k) | n.
```

## C++

```
// C++ implementation to set the kth bit
// of the given number
#include <bits/stdc++.h>

using namespace std;

// function to set the kth bit
int setKthBit(int n, int k)
{
    // kth bit of n is being set by this operation
    return ((1 << k) | n);
}

// Driver program to test above
int main()
{
    int n = 10, k = 2;
    cout << "Kth bit set number = "
         << setKthBit(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to set the kth bit
// of the given number

class GFG {

// function to set the kth bit
static int setKthBit(int n, int k)
{
    // kth bit of n is being set by this operation
    return ((1 << k) | n);
}

// Driver code
public static void main(String arg[])
{
    int n = 10, k = 2;
    System.out.print("Kth bit set number = " +
                             setKthBit(n, k));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python implementation
# to set the kth bit
# of the given number

# function to set
# the kth bit
def setKthBit(n,k):

    # kth bit of n is being
    # set by this operation
    return ((1 << k) | n)

# Driver code

n = 10
k = 2

print("Kth bit set number = ",
          setKthBit(n, k))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# implementation to set the
// kth bit of the given number
using System;

class GFG {

// function to set the kth bit
static int setKthBit(int n, int k)
{
    // kth bit of n is being set
    // by this operation
    return ((1 << k) | n);
}

// Driver code
public static void Main()
{
    int n = 10, k = 2;
    Console.Write("Kth bit set number = "
                    + setKthBit(n, k));

}
}

// This code is contributed by
// Smitha Dinesh Semwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// set the kth bit of
// the given number

// function to set
// the kth bit
function setKthBit($n, $k)
{
    // kth bit of n is being
    // set by this operation
    return ((1 << $k) | $n);
}

// Driver Code
$n = 10; $k = 2;
echo "Kth bit set number = ",
           setKthBit($n, $k);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>
    // Javascript implementation to set the
    // kth bit of the given number

    // function to set the kth bit
    function setKthBit(n, k)
    {
        // kth bit of n is being set
        // by this operation
        return ((1 << k) | n);
    }

    let n = 10, k = 2;
    document.write("Kth bit set number = " + setKthBit(n, k));

    // This code is contributed by rameshtravel07.
</script>
```

**输出:**

```
Kth bit set number = 14
```

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。