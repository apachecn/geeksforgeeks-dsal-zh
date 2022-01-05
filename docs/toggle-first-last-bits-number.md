# 切换数字的第一位和最后一位

> 原文:[https://www . geesforgeks . org/toggle-first-last-bits-number/](https://www.geeksforgeeks.org/toggle-first-last-bits-number/)

给定一个数字 n，任务是只切换一个数字的第一位和最后一位
**示例:**

```
Input : 10
Output : 3
Binary representation of 10 is
1010\. After toggling first and
last bits, we get 0011.

Input : 15
Output : 6
```

先决条件:[找到给定数量的 MSB](https://www.geeksforgeeks.org/find-significant-set-bit-number/)。
1)生成一个包含设定的第一位和最后一位的数字。我们需要将所有中间位更改为 0，并将边角位保留为 1。
2)答案是生成数与原数的异或。

## C++

```
// CPP program to toggle first and last
// bits of a number
#include <iostream>
using namespace std;

// Returns a number which has same bit
// count as n and has only first and last
// bits as set.
int takeLandFsetbits(int n)
{
    // set all the bit of the number
    n |= n >> 1;
    n |= n >> 2;
    n |= n >> 4;
    n |= n >> 8;
    n |= n >> 16;

    // Adding one to n now unsets
    // all bits and moves MSB to
    // one place. Now we shift
    // the number by 1 and add 1.
    return ((n + 1) >> 1) + 1;
}

int toggleFandLbits(int n)
{
    // if number is 1
    if (n == 1)
        return 0;

    // take XOR with first and
    // last set bit number
    return n ^ takeLandFsetbits(n);
}

// Driver code
int main()
{
    int n = 10;
    cout << toggleFandLbits(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to toggle first and last
// bits of a number
import java.io.*;

class GFG {

    // Returns a number which has same bit
    // count as n and has only first and last
    // bits as set.
    static int takeLandFsetbits(int n)
    {
        // set all the bit of the number
        n |= n >> 1;
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        // Adding one to n now unsets
        // all bits and moves MSB to
        // one place. Now we shift
        // the number by 1 and add 1.
        return ((n + 1) >> 1) + 1;
    }

    static int toggleFandLbits(int n)
    {
        // if number is 1
        if (n == 1)
            return 0;

        // take XOR with first and
        // last set bit number
        return n ^ takeLandFsetbits(n);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 10;
        System.out.println(toggleFandLbits(n));
    }
}

/*This code is contributed by Nikita Tiwari.*/
```

## 蟒蛇 3

```
# Python 3 program to toggle first
# and last bits of a number.

# Returns a number which has same bit
# count as n and has only first and last
# bits as set.
def takeLandFsetbits(n) :

# set all the bit of the number
    n = n | n >> 1
    n = n | n >> 2
    n = n | n >> 4
    n = n | n >> 8
    n = n | n >> 16

    # Adding one to n now unsets
    # all bits and moves MSB to
    # one place. Now we shift
    # the number by 1 and add 1.
    return ((n + 1) >> 1) + 1

def toggleFandLbits(n) :
    # if number is 1
    if (n == 1) :
        return 0

    # take XOR with first and
    # last set bit number
    return n ^ takeLandFsetbits(n)

# Driver code
n = 10
print(toggleFandLbits(n))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to toggle first and last
// bits of a number
using System;

class GFG {

    // Returns a number which has same bit
    // count as n and has only first and last
    // bits as set.
    static int takeLandFsetbits(int n)
    {
        // set all the bit of the number
        n |= n >> 1;
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        // Adding one to n now unsets
        // all bits and moves MSB to
        // one place. Now we shift
        // the number by 1 and add 1.
        return ((n + 1) >> 1) + 1;
    }

    static int toggleFandLbits(int n)
    {

        // if number is 1
        if (n == 1)
            return 0;

        // take XOR with first and
        // last set bit number
        return n ^ takeLandFsetbits(n);
    }

    // Driver code
    public static void Main()
    {

        int n = 10;

        Console.WriteLine(toggleFandLbits(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to toggle first and last
// bits of a number

// Returns a number which has same bit
// count as n and has only first and last
// bits as set.
function takeLandFsetbits($n)
{
    // set all the bit of the number
    $n |= $n >> 1;
    $n |= $n >> 2;
    $n |= $n >> 4;
    $n |= $n >> 8;
    $n |= $n >> 16;

    // Adding one to n now unsets
    // all bits and moves MSB to
    // one place. Now we shift
    // the number by 1 and add 1.
    return (($n + 1) >> 1) + 1;
}

function toggleFandLbits(int $n)
{
    // if number is 1
    if ($n == 1)
        return 0;

    // take XOR with first and
    // last set bit number
    return $n ^ takeLandFsetbits($n);
}

// Driver code
$n = 10;
echo toggleFandLbits($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to toggle first and last
// bits of a number

    // Returns a number which has same bit
    // count as n and has only first and last
    // bits as set.
    function takeLandFsetbits(n)
    {
        // set all the bit of the number
        n |= n >> 1;
        n |= n >> 2;
        n |= n >> 4;
        n |= n >> 8;
        n |= n >> 16;

        // Adding one to n now unsets
        // all bits and moves MSB to
        // one place. Now we shift
        // the number by 1 and add 1.
        return ((n + 1) >> 1) + 1;
    }

    function toggleFandLbits(n)
    {
        // if number is 1
        if (n == 1)
            return 0;

        // take XOR with first and
        // last set bit number
        return n ^ takeLandFsetbits(n);
    }

// Driver code

        let n = 10;
        document.write(toggleFandLbits(n));

</script>
```

**输出:**

```
3
```

时间复杂度为 0(1)。