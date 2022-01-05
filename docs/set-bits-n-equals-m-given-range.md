# 在给定范围内，将 N 中的位设置为等于 M。

> 原文:[https://www . geesforgeks . org/set-bits-n-equals-m-给定范围/](https://www.geeksforgeeks.org/set-bits-n-equals-m-given-range/)

给你两个 32 位数字，N 和 M，两个位位置，I 和 j，写一个方法，将 N 中 I 和 j 之间的所有位设置为 M(例如，M 变成 N 的子串，位于 I，从 j 开始)。
**例:**

```
Input : N = 1, M = 2, i = 2, j = 4
Output: 9
N = 00000001(Considering 8 bits only)
M = 10 (Binary of 2) For more indexes,
leading zeroes will be considered.
Now set 3 bits from ith index to j in 
the N as in the M.
Bits:-    0 0 0 (0  1  0) 0 1 = 9
Indexes:- 7 6 5  4  3  2  1 0
From index 2 to 4, bits are set according 
to the M.
```

问于:土坯

一个简单的解决方案是遍历 N 中从 0 到 31 的所有位，并将 I 到 j 范围内的位设置为等于 M。
一个有效的解决方案是执行以下步骤。

1.  设置数字中 j 之后的所有位。
2.  在我输入一个数字之前设置好所有的位。
3.  然后对两者执行按位“或”，然后我们得到除 I 到 j 以外的所有位都已设置的数字
4.  对给定的 N 执行按位“与”，以便根据 N 设置位
5.  然后将 M 移到正确的位置，即在 I 到 j 的范围内。
6.  最后执行按位“或”运算(在第四步中修改移位的 M 和 N)。
7.  结果将是 N，M 是从第 1 位到第 16 位的子串

## C++

```
// C++ program for above implementation
#include <iostream>
using namespace std;

// Function to set the bits
int setBits(int n, int m, int i, int j)
{
    // number with all 1's
    int allOnes = ~0;

    // Set all the bits in the left of j
    int left = allOnes << (j + 1);

    // Set all the bits in the right of j
    int right = ((1 << i) - 1);

    // Do Bitwise OR to get all the bits
    // set except in the range from i to j
    int mask = left | right;

    // clear bits j through i
    int masked_n = n & mask;

    // move m into the correct position
    int m_shifted = m << i;

    // return the Bitwise OR of masked_n
    // and shifted_m
    return (masked_n | m_shifted);
}

// Drivers program
int main()
{
    int n = 2, m = 4;
    int i = 2, j = 4;
    cout << setBits(n, m, i, j);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program
public class GFG
{
    // Function to set the bits
    static int setBits(int n, int m, int  i, int j)
    {

        // number with all 1's
        int  allOnes = ~0;

        // Set all the bits in the left of j
        int left = allOnes << (j + 1);

        // Set all the bits in the right of j
        int right = ((1 << i) - 1);

        // Do Bitwise OR to get all the bits
        // set except in the range from i to j
        int mask = left | right;

        // clear bits j through i
        int masked_n = n & mask;

        // move m into the correct position
        int m_shifted = m << i;

        // return the Bitwise OR of masked_n
        // and shifted_m
        return (masked_n | m_shifted);
    }

    // Driver Program to test above function
    public static void main(String[] args)
    {
        int n = 2, m = 4;
        int i = 2, j = 4;
        System.out.println(setBits(n, m, i, j));
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program for above implementation

# Function to set the bits
def setBits(n, m, i, j):

    # number with all 1's
    allOnes = not 0

    # Set all the bits in the left of j
    left = allOnes << (j + 1)

    # Set all the bits in the right of j
    right = ((1 << i) - 1)

    # Do Bitwise OR to get all the bits
    # set except in the range from i to j
    mask = left | right

    # clear bits j through i
    masked_n = n & mask

    # move m into the correct position
    m_shifted = m << i

    # return the Bitwise OR of masked_n
    # and shifted_m
    return (masked_n | m_shifted)

# Drivers program
n, m = 2, 4
i, j = 2, 4
print setBits(n, m, i, j)

# This code is submitted by Sachin Bisht
```

## C#

```
// C# Program for above implementation
using System;

public class GFG {

    // Function to set the bits
    static int setBits(int n, int m, int  i, int j)
    {

        // number with all 1's
        int  allOnes = ~0;

        // Set all the bits in the left of j
        int left = allOnes << (j + 1);

        // Set all the bits in the right of j
        int right = ((1 << i) - 1);

        // Do Bitwise OR to get all the bits
        // set except in the range from i to j
        int mask = left | right;

        // clear bits j through i
        int masked_n = n & mask;

        // move m into the correct position
        int m_shifted = m << i;

        // return the Bitwise OR of masked_n
        // and shifted_m
        return (masked_n | m_shifted);
    }

    // Driver Program to test above function
    public static void Main()
    {
        int n = 2, m = 4;
        int i = 2, j = 4;

        Console.WriteLine(setBits(n, m, i, j));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for above implementation

// Function to set the bits
function setBits($n, $m, $i, $j)
{
    // number with all 1's
    $allOnes = ~0;

    // Set all the bits
    // in the left of j
    $left = $allOnes << ($j + 1);

    // Set all the bits
    // in the right of j
    $right = ((1 << $i) - 1);

    // Do Bitwise OR to get all
    // the bits set except in
    // the range from i to j
    $mask = $left | $right;

    // clear bits j through i
    $masked_n = $n & $mask;

    // move m into the
    // correct position
    $m_shifted = $m << $i;

    // return the Bitwise OR
    // of masked_n and shifted_m
    return ($masked_n | $m_shifted);
}

// Driver Code
$n = 2; $m = 4;
$i = 2; $j = 4;
echo setBits($n, $m, $i, $j);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript Program for above implementation

    // Function to set the bits
    function setBits(n, m, i, j)
    {

        // number with all 1's
        let  allOnes = ~0;

        // Set all the bits in the left of j
        let left = allOnes << (j + 1);

        // Set all the bits in the right of j
        let right = ((1 << i) - 1);

        // Do Bitwise OR to get all the bits
        // set except in the range from i to j
        let mask = left | right;

        // clear bits j through i
        let masked_n = n & mask;

        // move m into the correct position
        let m_shifted = m << i;

        // return the Bitwise OR of masked_n
        // and shifted_m
        return (masked_n | m_shifted);
    }

    let n = 2, m = 4;
    let i = 2, j = 4;

    document.write(setBits(n, m, i, j));

</script>
```

**输出:**

```
18
```

参考:
[【https://www.careercup.com/question?id=8863294】](https://www.careercup.com/question?id=8863294)
本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。