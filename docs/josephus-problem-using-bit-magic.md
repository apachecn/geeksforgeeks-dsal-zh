# 使用比特魔法的约瑟夫斯问题

> 原文:[https://www . geeksforgeeks . org/josephus-问题-使用-bit-magic/](https://www.geeksforgeeks.org/josephus-problem-using-bit-magic/)

**问题**

这个问题是以反对罗马人的犹太历史学家弗拉维奥·约瑟夫斯的名字命名的。根据约瑟夫斯的说法，他和他的犹太士兵被逼得走投无路&被罗马人包围在一个山洞里，他们选择在投降和被俘期间进行谋杀和自杀。他们决定所有的士兵坐成一圈，从坐在第一个位置的士兵开始，每个士兵将依次杀死他们的士兵。所以如果有 5 个士兵坐在一个圆圈里，位置编号为 1，2，3，4，5。士兵 1 杀了 2，然后 3 杀了 4，然后 5 杀了 1，然后 3 杀了 5，由于只剩下 3 个，然后 3 自杀。现在约瑟夫斯不想被谋杀或自杀。他宁愿被罗马人俘虏，并面临一个问题。他必须弄清楚他应该坐在一个圆圈的哪个位置(假设总共有 n 个人，坐在位置 1 的人有第一次杀人的机会)，这样他就是最后一个站着的人，他不会自杀，而是向罗马人投降。

**模式**

如果你计算出 n 的不同值，你会发现一个模式。如果 n 是 2 的真幂，那么答案总是 1。每 n 大于 2 的幂，答案就增加 2。

<figure class="table">

| 士兵 | 2 <sup>a</sup> + l | 幸存者 W(n) = 2l + 1 |
| --- | --- | --- |
| one | 1 + 0 | 2 * 0 + 1 = 1 |
| Two | 2 + 0 | 2 * 0 + 1 = 1 |
| three | 2 + 1 | 2 * 1 + 1 = 3 |
| four | 4 + 0 | 2 * 0 + 1 = 1 |
| five | 4 + 1 | 2 * 1 + 1 = 3 |
| six | 4 + 2 | 2 * 2 + 1 = 5 |
| seven | 4 + 3 | 2 * 3 + 1 = 7 |
| eight | 8 + 0 | 2 * 0 + 1 = 1 |
| nine | 8 + 1 | 2 * 1 + 1 = 3 |
| Ten | 8 + 2 | 2 * 2 + 1 = 5 |
| Eleven | 8 + 3 | 2 * 3 + 1 = 7 |
| Twelve | 8 + 4 | 2 * 4 + 1 = 9 |

</figure>

现在，对于每个 n，约瑟夫斯的正确位置可以通过从数字中扣除最大可能的 2 的幂来找到，我们得到答案(假设 n 的值不是 2 的纯幂，否则答案是 1)

**N = 2 <sup>a</sup> +某物**

其中 a =最大可能功率

**诀窍**
每当有人谈论 2 的幂时，脑海中出现的第一个词是“二进制”。这个问题的解决方案用二进制比用十进制容易得多，也短得多。这是有诀窍的。因为我们需要在二进制中扣除最大可能的幂，所以这个数是最高有效位。在最初的约瑟夫斯问题中，除了约瑟夫斯还有 40 名士兵，这使得 **n = 41** 。二进制中的 41 是 101001。如果我们将 MSB，即最左边的 1 移动到最右边的位置，我们得到的答案是 010011，即 19(十进制)。所有情况都是如此。这可以使用位操作轻松完成。

## C++

```
// C++ program for josephus problem
#include <bits/stdc++.h>
using namespace std;

// function to find the position of the Most
// Significant Bit
int msbPos(int n)
{
    int pos = 0;
    while (n != 0) {
        pos++;

        // keeps shifting bits to the right
        // until we are left with 0
        n = n >> 1;
    }
    return pos;
}

// function to return at which place Josephus
// should sit to avoid being killed
int josephify(int n)
{
    /* Getting the position of the Most Significant
        Bit(MSB). The leftmost '1'. If the number is
    '41' then its binary is '101001'.
        So msbPos(41) = 6 */
    int position = msbPos(n);

    /* 'j' stores the number with which to XOR the
        number 'n'. Since we need '100000'
    We will do 1<<6-1 to get '100000' */
    int j = 1 << (position - 1);

    /* Toggling the Most Significant Bit. Changing
    the leftmost '1' to '0'.
    101001 ^ 100000 = 001001 (9) */
    n = n ^ j;

    /* Left-shifting once to add an extra '0' to
        the right end of the binary number
        001001 = 010010 (18) */
    n = n << 1;

    /* Toggling the '0' at the end to '1' which
    is essentially the same as putting the
    MSB at the rightmost place. 010010 | 1
    = 010011 (19) */
    n = n | 1;

    return n;
}

// hard coded driver main function to run the program
int main()
{
    int n = 41;
    cout <<josephify(n);
    return 0;
}// This code is contributed by Mukul singh.
```

## C

```
// C program for josephus problem

#include <stdio.h>

// function to find the position of the Most
// Significant Bit
int msbPos(int n)
{
    int pos = 0;
    while (n != 0) {
        pos++;

        // keeps shifting bits to the right
        // until we are left with 0
        n = n >> 1;
    }
    return pos;
}

// function to return at which place Josephus
// should sit to avoid being killed
int josephify(int n)
{
    /*  Getting the position of the Most Significant
        Bit(MSB). The leftmost '1'. If the number is
       '41' then its binary is '101001'.
        So msbPos(41) = 6   */
    int position = msbPos(n);

    /* 'j' stores the number with which to XOR the
        number 'n'. Since we need '100000'
       We will do 1<<6-1 to get '100000' */
    int j = 1 << (position - 1);

    /* Toggling the Most Significant Bit. Changing
       the leftmost '1' to '0'.
       101001 ^ 100000 = 001001 (9) */
    n = n ^ j;

    /*  Left-shifting once to add an extra '0' to
        the right end of the binary number
        001001 = 010010 (18) */
    n = n << 1;

    /* Toggling the '0' at the end to '1' which
       is essentially the same as putting the
       MSB at the rightmost place. 010010 | 1
       = 010011 (19) */
    n = n | 1;

    return n;
}

// hard coded driver main function to run the program
int main()
{
    int n = 41;
    printf("%d\n", josephify(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for josephus problem

public class GFG
{
    // method to find the position of the Most
    // Significant Bit
    static int msbPos(int n)
    {
        int pos = 0;
        while (n != 0) {
            pos++;

            // keeps shifting bits to the right
            // until we are left with 0
            n = n >> 1;
        }
        return pos;
    }

    // method to return at which place Josephus
    // should sit to avoid being killed
    static int josephify(int n)
    {
        /*  Getting the position of the Most Significant
            Bit(MSB). The leftmost '1'. If the number is
           '41' then its binary is '101001'.
            So msbPos(41) = 6   */
        int position = msbPos(n);

        /* 'j' stores the number with which to XOR the
            number 'n'. Since we need '100000'
           We will do 1<<6-1 to get '100000' */
        int j = 1 << (position - 1);

        /* Toggling the Most Significant Bit. Changing
           the leftmost '1' to '0'.
           101001 ^ 100000 = 001001 (9) */
        n = n ^ j;

        /*  Left-shifting once to add an extra '0' to
            the right end of the binary number
            001001 = 010010 (18) */
        n = n << 1;

        /* Toggling the '0' at the end to '1' which
           is essentially the same as putting the
           MSB at the rightmost place. 010010 | 1
           = 010011 (19) */
        n = n | 1;

        return n;
    }

    // Driver Method
    public static void main(String[] args)
    {
        int n = 41;
        System.out.println(josephify(n));
    }
}
```

## 蟒蛇 3

```
# Python3 program for josephus problem

# Function to find the position
# of the Most Significant Bit
def msbPos(n):
    pos = 0
    while n != 0:
        pos += 1
        n = n >> 1
    return pos

# Function to return at which
# place Josephus should sit to
# avoid being killed
def josephify(n):

    # Getting the position of the Most
    # Significant Bit(MSB). The leftmost '1'.
    # If the number is '41' then its binary
    # is '101001'. So msbPos(41) = 6
    position = msbPos(n)

    # 'j' stores the number with which to XOR 
    # the number 'n'. Since we need '100000'
    # We will do 1<<6-1 to get '100000'
    j = 1 << (position - 1)

    # Toggling the Most Significant Bit.
    # Changing the leftmost '1' to '0'.
    # 101001 ^ 100000 = 001001 (9)
    n = n ^ j

    # Left-shifting once to add an extra '0' 
    # to the right end of the binary number
    # 001001 = 010010 (18)
    n = n << 1

    # Toggling the '0' at the end to '1' 
    # which is essentially the same as
    # putting the MSB at the rightmost
    # place. 010010 | 1 = 010011 (19)
    n = n | 1

    return n

# Driver Code
n = 41
print (josephify(n))

# This code is contributed by Shreyanshi Arun.
```

## C#

```
// C# program for Josephus Problem
using System;

public class GFG
{

    // Method to find the position
    // of the Most Significant Bit
    static int msbPos(int n)
    {
        int pos = 0;
        while (n != 0) {
            pos++;

            // keeps shifting bits to the right
            // until we are left with 0
            n = n >> 1;
        }
        return pos;
    }

    // method to return at which place Josephus
    // should sit to avoid being killed
    static int josephify(int n)
    {

        // Getting the position of the Most Significant
        // Bit(MSB). The leftmost '1'. If the number is
        // '41' then its binary is '101001'.
        // So msbPos(41) = 6
        int position = msbPos(n);

        // 'j' stores the number with which to XOR 
        // the number 'n'. Since we need '100000'
        // We will do 1<<6-1 to get '100000'
        int j = 1 << (position - 1);

        // Toggling the Most Significant Bit.
        // Changing the leftmost '1' to '0'.
        // 101001 ^ 100000 = 001001 (9)
        n = n ^ j;

        // Left-shifting once to add an extra '0'
        // to the right end of the binary number
        // 001001 = 010010 (18)
        n = n << 1;

        // Toggling the '0' at the end to '1' which
        // is essentially the same as putting the
        // MSB at the rightmost place. 010010 | 1
        // = 010011 (19)
        n = n | 1;

        return n;
    }

    // Driver code
    public static void Main()
    {
        int n = 41;
        Console.WriteLine(josephify(n));
    }
}

// This code is contributed by vt_m .
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for josephus problem

// function to find the position of
// the Most Significant Bit
function msbPos($n)
{
    $pos = 0;
    while ($n != 0)
    {
        $pos++;

        // keeps shifting bits to the right
        // until we are left with 0
        $n = $n >> 1;
    }
    return $pos;
}

// function to return at which place Josephus
// should sit to avoid being killed
function josephify($n)
{
    /* Getting the position of the Most
       Significant Bit(MSB). The leftmost '1'.
       If the number is '41' then its binary
       is '101001'. So msbPos(41) = 6 */
    $position = msbPos($n);

    /* 'j' stores the number with which to
        XOR the number 'n'. Since we need
    '100000'. We will do 1<<6-1 to get '100000' */
    $j = 1 << ($position - 1);

    /* Toggling the Most Significant Bit.
    Changing the leftmost '1' to '0'.
    101001 ^ 100000 = 001001 (9) */
    $n = $n ^ $j;

    /* Left-shifting once to add an extra '0'
       to the right end of the binary number
       001001 = 010010 (18) */
    $n = $n << 1;

    /* Toggling the '0' at the end to '1' which
    is essentially the same as putting the
    MSB at the rightmost place. 010010 | 1
    = 010011 (19) */
    $n = $n | 1;

    return $n;
}

// Driver Code
$n = 41;
print(josephify($n));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript program for josephus problem

// method to find the position of the Most
// Significant Bit
function msbPos(n)
{
    var pos = 0;
    while (n != 0) {
        pos++;

        // keeps shifting bits to the right
        // until we are left with 0
        n = n >> 1;
    }
    return pos;
}

// method to return at which place Josephus
// should sit to avoid being killed
function josephify(n)
{
    /*  Getting the position of the Most Significant
        Bit(MSB). The leftmost '1'. If the number is
       '41' then its binary is '101001'.
        So msbPos(41) = 6   */
    var position = msbPos(n);

    /* 'j' stores the number with which to XOR the
        number 'n'. Since we need '100000'
       We will do 1<<6-1 to get '100000' */
    var j = 1 << (position - 1);

    /* Toggling the Most Significant Bit. Changing
       the leftmost '1' to '0'.
       101001 ^ 100000 = 001001 (9) */
    n = n ^ j;

    /*  Left-shifting once to add an extra '0' to
        the right end of the binary number
        001001 = 010010 (18) */
    n = n << 1;

    /* Toggling the '0' at the end to '1' which
       is essentially the same as putting the
       MSB at the rightmost place. 010010 | 1
       = 010011 (19) */
    n = n | 1;

    return n;
}

// Driver Method
var n = 41;
document.write(josephify(n));

// This code is contributed by Amit Katiyar
</script>
```

**输出:**

```
19
```

**同一主题的往期文章:**

1.  [约瑟夫斯问题|集合 1 (A O(n)解)](https://www.geeksforgeeks.org/josephus-problem-set-1-a-on-solution/)
2.  [约瑟夫斯问题|集合 2(k = 2 时的简单解)](https://www.geeksforgeeks.org/josephus-problem-set-2-simple-solution-k-2/)

本文由 [Palash Nigam](https://www.linkedin.com/in/palash25) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。