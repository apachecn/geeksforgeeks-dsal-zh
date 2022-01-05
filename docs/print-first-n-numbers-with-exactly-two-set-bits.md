# 打印前 n 个正好有两个设定位的数字

> 原文:[https://www . geeksforgeeks . org/print-first-n-numbers-with-two-set-bit/](https://www.geeksforgeeks.org/print-first-n-numbers-with-exactly-two-set-bits/)

给定一个数字 n，打印前 n 个正整数，在其二进制表示中正好有两个设置位。
**例:**

```
Input: n = 3
Output: 3 5 6
The first 3 numbers with two set bits are 3 (0011),
5 (0101) and 6 (0110)

Input: n = 5
Output: 3 5 6 9 10 12
```

一个**简单解法**就是从 1 开始逐个考虑所有正整数。对于每个数字，检查它是否正好有两组位。如果一个数字正好有两个设定位，打印出来并增加这些数字的计数。
一个**高效的解决方案**就是直接生成这样的数字。如果我们清楚地观察这些数字，我们可以把它们改写为下面给定的幂(2，1)+幂(2，0)，幂(2，2)+幂(2，0)，幂(2，2)+幂(2，1)，幂(2，3)+幂(2，0)，幂(2，3)+幂(2，1)，幂(2，3)+幂(2，2)，……
所有的数字都可以按照两组位中较高的一组按递增的顺序产生。这个想法是一个接一个地固定两个比特中较高的一个。对于当前较高的设置位，考虑所有较低的位并打印形成的数字。

## C++

```
// C++ program to print first n numbers
// with exactly two set bits
#include <iostream>
using namespace std;

// Prints first n numbers with two set bits
void printTwoSetBitNums(int n)
{
    // Initialize higher of two sets bits
    int x = 1;

    // Keep reducing n for every number
    // with two set bits.
    while (n > 0)
    {
        // Consider all lower set bits for
        // current higher set bit
        int y = 0;
        while (y < x)
        {
            // Print current number
            cout << (1 << x) + (1 << y) << " ";

            // If we have found n numbers
            n--;
            if (n == 0)
                return;

            // Consider next lower bit for current
            // higher bit.
            y++;
        }

        // Increment higher set bit
        x++;
    }
}

// Driver code
int main()
{
    printTwoSetBitNums(4);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print first n numbers
// with exactly two set bits
import java.io.*;

class GFG
{
    // Function to print first n numbers with two set bits
    static void printTwoSetBitNums(int n)
    {
        // Initialize higher of two sets bits
        int x = 1;

        // Keep reducing n for every number
        // with two set bits
        while (n > 0)
        {
            // Consider all lower set bits for
            // current higher set bit
            int y = 0;
            while (y < x)
            {
                // Print current number
                System.out.print(((1 << x) + (1 << y)) +" ");

                // If we have found n numbers
                n--;
                if (n == 0)
                    return;

                // Consider next lower bit for current
                // higher bit.
                y++;
            }

            // Increment higher set bit
            x++;
        }
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 4;
        printTwoSetBitNums(n);
    }
}

// This code is contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python3 program to print first n
# numbers with exactly two set bits

# Prints first n numbers
# with two set bits
def printTwoSetBitNums(n) :

    # Initialize higher of
    # two sets bits
    x = 1

    # Keep reducing n for every
    # number with two set bits.
    while (n > 0) :

        # Consider all lower set bits
        # for current higher set bit
        y = 0
        while (y < x) :

            # Print current number
            print((1 << x) + (1 << y),
                          end = " " )

            # If we have found n numbers
            n -= 1
            if (n == 0) :
                return

            # Consider next lower bit
            # for current higher bit.
            y += 1

        # Increment higher set bit
        x += 1

# Driver code
printTwoSetBitNums(4)

# This code is contributed
# by Smitha
```

## C#

```
// C# program to print first n numbers
// with exactly two set bits
using System;

class GFG
    {

    // Function to print first n
    // numbers with two set bits
    static void printTwoSetBitNums(int n)
    {

        // Initialize higher of
        // two sets bits
        int x = 1;

        // Keep reducing n for every
        // number with two set bits
        while (n > 0)
        {

            // Consider all lower set bits
            // for current higher set bit
            int y = 0;
            while (y < x)
            {

                // Print current number
                Console.Write(((1 << x) +
                                (1 << y)) +" ");

                // If we have found n numbers
                n--;
                if (n == 0)
                    return;

                // Consider next lower bit
                // for current higher bit.
                y++;
            }

            // Increment higher set bit
            x++;
        }
    }

    // Driver program
    public static void Main()
    {
        int n = 4;
        printTwoSetBitNums(n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print
// first n numbers with
// exactly two set bits

// Prints first n numbers
// with two set bits
function printTwoSetBitNums($n)
{
    // Initialize higher of
    // two sets bits
    $x = 1;

    // Keep reducing n for
    // every number with
    // two set bits.
    while ($n > 0)
    {
        // Consider all lower set
        // bits for current higher
        // set bit
        $y = 0;
        while ($y < $x)
        {
            // Print current number
            echo (1 << $x) + (1 << $y), " ";

            // If we have found n numbers
            $n--;
            if ($n == 0)
                return;

            // Consider next lower
            // bit for current
            // higher bit.
            $y++;
        }

        // Increment higher set bit
        $x++;
    }
}

// Driver code
printTwoSetBitNums(4);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to print first n numbers
// with exactly two set bits

// Prints first n numbers with two set bits
function printTwoSetBitNums(n)
{

    // Initialize higher of two sets bits
    let x = 1;

    // Keep reducing n for every number
    // with two set bits.
    while (n > 0)
    {

        // Consider all lower set bits for
        // current higher set bit
        let y = 0;
        while (y < x)
        {

            // Print current number
            document.write((1 << x) + (1 << y) + " ");

            // If we have found n numbers
            n--;
            if (n == 0)
                return;

            // Consider next lower bit for current
            // higher bit.
            y++;
        }

        // Increment higher set bit
        x++;
    }
}

// Driver code
printTwoSetBitNums(4);

// This code is contributed by Mayank Tyagi
</script>
```

**输出:**

```
3 5 6 9
```

**时间复杂度:** O(n)

**辅助空间:** O(1)
本文由**巴拉思·雷迪·阿帕迪**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。