# 二进制表示中没有连续 1 的 1 到 n 位数字

> 原文:[https://www . geesforgeks . org/1-n 位数字-无连续-1s-二进制表示/](https://www.geeksforgeeks.org/1-n-bit-numbers-no-consecutive-1s-binary-representation/)

给定一个数字 n，我们的任务是找到所有 1 到 n 个二进制表示中没有连续 1 的比特数。
**例:**

```
Input: N = 4
Output: 1 2 4 5 8 9 10
These are numbers with 1 to 4
bits and no consecutive ones in
binary representation.

Input: n = 3
Output: 1 2 4 5
```

**进场:**

1.  将有 2 个 <sup>n 个</sup>数字，位数从 1 到 n
2.  遍历所有 2 <sup>n</sup> 个数字。对于每个数字，检查它是否包含连续的设置位。为了进行检查，我们对当前数字 I 和左移的 I 进行按位“与”，如果按位“与”包含非零位(或其值为非零)，则给定的数字包含连续的设置位。

下面是上述方法的实现:

## C++

```
// Print all numbers upto n bits
// with no consecutive set bits.
#include<iostream>
using namespace std;

void printNonConsecutive(int n)
{
    // Let us first compute
    // 2 raised to power n.
    int p = (1 << n);

    // loop 1 to n to check
    // all the numbers
    for (int i = 1; i < p; i++)

        // A number i doesn't contain
        // consecutive set bits if
        // bitwise and of i and left
        // shifted i do't contain a
        // commons set bit.
        if ((i & (i << 1)) == 0)
            cout << i << " ";
}

// Driver code
int main()
{
    int n = 3;
    printNonConsecutive(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code to Print all numbers upto
// n bits with no consecutive set bits.
import java.util.*;

class GFG
{
    static void printNonConsecutive(int n)
        {
            // Let us first compute
            // 2 raised to power n.
            int p = (1 << n);

            // loop 1 to n to check
            // all the numbers
            for (int i = 1; i < p; i++)

            // A number i doesn't contain
            // consecutive set bits if
            // bitwise and of i and left
            // shifted i do't contain a
            // commons set bit.
            if ((i & (i << 1)) == 0)
                System.out.print(i + " ");

        }

// Driver code
public static void main(String[] args)
    {
        int n = 3;
        printNonConsecutive(n);
    }
}

// This code is contributed by Mr. Somesh Awasthi
```

## 蟒蛇 3

```
# Python3 program to print all numbers upto
# n bits with no consecutive set bits.

def printNonConsecutive(n):

    # Let us first compute 
    # 2 raised to power n.
    p = (1 << n)

    # loop 1 to n to check
    # all the numbers
    for i in range(1, p):

        # A number i doesn't contain
        # consecutive set bits if
        # bitwise and of i and left
        # shifted i do't contain a
        # common set bit.
        if ((i & (i << 1)) == 0):
            print(i, end = " ")

# Driver code
n = 3
printNonConsecutive(n)

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# Code to Print all numbers upto
// n bits with no consecutive set bits.
using System;

class GFG
{
    static void printNonConsecutive(int n)
    {
        // Let us first compute
        // 2 raised to power n.
        int p = (1 << n);

        // loop 1 to n to check
        // all the numbers
        for (int i = 1; i < p; i++)

            // A number i doesn't contain
            // consecutive set bits if
            // bitwise and of i and left
            // shifted i do't contain a
            // commons set bit.
            if ((i & (i << 1)) == 0)
                Console.Write(i + " ");

    }

// Driver code
public static void Main()
    {
        int n = 3;
        printNonConsecutive(n);
    }
}
// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Print all numbers upto n bits
// with no consecutive set bits.

function printNonConsecutive($n)
{

    // Let us first compute
    // 2 raised to power n.
    $p = (1 << $n);

    // loop 1 to n to check
    // all the numbers
    for ($i = 1; $i < $p; $i++)

        // A number i doesn't contain
        // consecutive set bits if
        // bitwise and of i and left
        // shifted i do't contain a
        // commons set bit.
        if (($i & ($i << 1)) == 0)
            echo $i . " ";
}

    // Driver code
    $n = 3;
    printNonConsecutive($n);        

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript Code to Print all numbers upto
// n bits with no consecutive set bits.

function printNonConsecutive(n)
        {
            // Let us first compute
            // 2 raised to power n.
            let p = (1 << n);

            // loop 1 to n to check
            // all the numbers
            for (let i = 1; i < p; i++)

            // A number i doesn't contain
            // consecutive set bits if
            // bitwise and of i and left
            // shifted i do't contain a
            // commons set bit.
            if ((i & (i << 1)) == 0)
                document.write(i + " ");

        }

// driver program

        let n = 3;
        printNonConsecutive(n);

</script>
```

**Output**

```
1 2 4 5 
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

本文由**德万舒·阿加瓦尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。