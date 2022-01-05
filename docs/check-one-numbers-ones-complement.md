# 检查其中一个数字是否是另一个数字的补码

> 原文:[https://www . geesforgeks . org/check-one-numbers-one-complex/](https://www.geeksforgeeks.org/check-one-numbers-ones-complement/)

给定两个非负整数 **a** 和 **b** 。问题是检查这两个数字中是否有一个是另一个的 1 的补码。
二进制数的**1 补码**被定义为通过反转该数的二进制表示中的所有位而获得的值(将 0 交换为 1，反之亦然)。

**示例:**

```
Input : a = 10, b = 5
Output : Yes
(10)10 = (1010)2
1's complement of 10 is
= (0101)2 = (101)2 = (5)10

Input : a = 1, b = 14
Output : Yes
(14)10 = (1110)2
1's complement of 14 is
= (0001)2 = (1)2 = (1)10
```

**进场:**以下是步骤:

1.  计算 **n** = a ^ b。
2.  检查是否所有位都设置在 **n** 的二进制表示中。参考[这篇](https://www.geeksforgeeks.org/check-bits-number-set/)帖子。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to check if one of the two
// numbers is one's complement of the other
#include <bits/stdc++.h>
using namespace std;

// function to check if all the bits are set
// or not in the binary representation of 'n'
bool areAllBitsSet(unsigned int n)
{
    // all bits are not set
    if (n == 0)
        return false;

    // if true, then all bits are set
    if (((n + 1) & n) == 0)
        return true;

    // else all bits are not set
    return false;
}

// function to check if one of the two numbers
// is one's complement of the other
bool isOnesComplementOfOther(unsigned int a,
                             unsigned int b)
{
    return areAllBitsSet(a ^ b);
}

// Driver program to test above
int main()
{
    unsigned int a = 10, b = 5;

    if (isOnesComplementOfOther(a,b))
        cout << "Yes";
    else
        cout << "No";

    return 0;       
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// check if one of the two
// numbers is one's complement
// of the other

import java.util.*;
import java.lang.*;

public class GfG{

    // function to check
    // if all the bits are set
    // or not in the binary
    // representation of 'n'
    public static boolean areAllBitsSet(long n)
    {
        // all bits are not set
        if (n == 0)
            return false;

        // if true, then all bits are set
        if (((n + 1) & n) == 0)
            return true;

        // else all bits are not set
        return false;
    }

    // function to check if
    // one of the two numbers
    // is one's complement
    // of the other
    public static boolean isOnesComplementOfOther(long a,
                             long b)
    {
        return areAllBitsSet(a ^ b);
    }

    // Driver function
    public static void main(String argc[]){
        long a = 10, b = 5;

        if (isOnesComplementOfOther(a,b))
            System.out.println("Yes");
        else
            System.out.println("No");
    }

}

// This code is contributed by Sagar Shukla
```

## 蟒蛇 3

```
# Python3 implementation to
# check if one of the two
# numbers is one's complement
# of the other

# function to check if
# all the bits are set
# or not in the binary
# representation of 'n'
def areAllBitsSet(n):

    # all bits are not set
    if (n == 0):
        return False;

    # if True, then all bits are set
    if (((n + 1) & n) == 0):
        return True;

    # else all bits are not set
    return False;

# function to check if one
# of the two numbers is
# one's complement of the other
def isOnesComplementOfOther(a, b):

    return areAllBitsSet(a ^ b)

# Driver program
a = 1
b = 14
if (isOnesComplementOfOther(a, b)):
    print ("Yes")
else:
    print ("No")

# This code is contributed by
# Saloni Gupta 4
```

## C#

```
// C# implementation to check
// if one of the two numbers is
// one's complement of the other
using System;

class GFG {

    // function to check
    // if all the bits are set
    // or not in the binary
    // representation of 'n'
    public static bool areAllBitsSet(long n)
    {
        // all bits are not set
        if (n == 0)
            return false;

        // if true, then all bits are set
        if (((n + 1) & n) == 0)
            return true;

        // else all bits are not set
        return false;
    }

    // function to check if
    // one of the two numbers
    // is one's complement
    // of the other
    public static bool isOnesComplementOfOther(long a,
                                               long b)
    {
        return areAllBitsSet(a ^ b);
    }

    // Driver function
    public static void Main()
    {
        long a = 10, b = 5;

        if (isOnesComplementOfOther(a, b))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to
// check if one of the two
// numbers is one's complement
// of the other

// function to check if
// all the bits are set
// or not in the binary
// representation of 'n'
function areAllBitsSet($n)
{

    // all bits are not set
    if ($n == 0)
        return false;

    // if true, then all
    // bits are set
    if ((($n + 1) & $n) == 0)
        return true;

    // else all bits
    // are not set
    return false;
}

// function to check if
// one of the two numbers
// is one's complement of
// the other
function isOnesComplementOfOther($a,
                                 $b)
{
    return areAllBitsSet($a ^ $b);
}

    // Driver Code
    $a = 10; $b = 5;

    if (isOnesComplementOfOther($a, $b))
        echo "Yes";
    else
        echo "No";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation to
// check if one of the two
// numbers is one's complement
// of the other

    // function to check
    // if all the bits are set
    // or not in the binary
    // representation of 'n'
    function areAllBitsSet(n)
    {
        // all bits are not set
        if (n == 0)
            return false;

        // if true, then all bits are set
        if (((n + 1) & n) == 0)
            return true;

        // else all bits are not set
        return false;
    }

    // function to check if
    // one of the two numbers
    // is one's complement
    // of the other
    function isOnesComplementOfOther(a, b)
    {
        return areAllBitsSet(a ^ b);
    }

    // Driver code

        let a = 10, b = 5;

        if (isOnesComplementOfOther(a,b))
            document.write("Yes");
        else
            document.write("No");

</script>
```

输出:

```
Yes
```

本文由 [**阿育什·乔哈里**](https://auth.geeksforgeeks.org/profile.php?user=ayushjauhari14) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。