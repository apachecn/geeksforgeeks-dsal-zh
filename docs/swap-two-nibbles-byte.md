# 交换一个字节中的两个半字节

> 原文:[https://www.geeksforgeeks.org/swap-two-nibbles-byte/](https://www.geeksforgeeks.org/swap-two-nibbles-byte/)

一个[半字节](http://en.wikipedia.org/wiki/Nibble)是一个四位聚合，或者说是半个八位字节。一个字节有两个半字节。
给定一个字节，交换其中的两个半字节。例如，100 在一个字节(或 8 位)中表示为 01100100。这两个半字节是(0110)和(0100)。如果我们交换两个半字节，我们得到 01000110，十进制为 70。

为了交换半字节，我们可以使用按位&，按位”运算符。一个字节可以用 C 语言中的无符号字符来表示，因为在典型的 C 语言编译器中，字符的大小是 1 字节。
下面是上面思路的实现。

## C++

```
// C++ program to swap two
// nibbles in a byte
#include <bits/stdc++.h>
using namespace std;

int swapNibbles(int x)
{
    return ( (x & 0x0F) << 4 | (x & 0xF0) >> 4 );
}

// Driver code
int main()
{
    int x = 100;
    cout << swapNibbles(x);
    return 0;
}

//This code is contributed by Shivi_Aggarwal
```

## C

```
#include <stdio.h>

unsigned char swapNibbles(unsigned char x)
{
    return ( (x & 0x0F)<<4 | (x & 0xF0)>>4 );
}

int main()
{
    unsigned char x = 100;
    printf("%u", swapNibbles(x));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to swap two
// nibbles in a byte

class GFG {

static int swapNibbles(int x)
{
    return ((x & 0x0F) << 4 | (x & 0xF0) >> 4);
}

// Driver code
public static void main(String arg[])
{
    int x = 100;
    System.out.print(swapNibbles(x));
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# python program Swap
# two nibbles in a byte

def swapNibbles(x):
    return ( (x & 0x0F)<<4 | (x & 0xF0)>>4 )

# Driver code

x = 100
print(swapNibbles(x))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to swap two
// nibbles in a byte
using System;

class GFG {

// Function for swapping   
static int swapNibbles(int x)
{
    return ((x & 0x0F) << 4 |
            (x & 0xF0) >> 4);
}

// Driver code
public static void Main()
{
    int x = 100;
    Console.Write(swapNibbles(x));
}
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to swap two
// nibbles in a byte

// function to Swap two nibbles
// in a byte in php program
function swapNibbles($x)
{
    return ( ($x & 0x0F) << 4 |
           ($x & 0xF0) >> 4 );
}

    // Driver Code
    $x = 100;
    echo swapNibbles($x);

// This Code is Contributed by Ajit
?>
```

## java 描述语言

```
<script>
// javascript program to swap two
// nibbles in a byte  
function swapNibbles(x)
{
    return ((x & 0x0F) << 4 | (x & 0xF0) >> 4);
}

// Driver code
var x = 100;
document.write(swapNibbles(x));

// This code is contributed by Princi Singh
</script>
```

**输出:**

```
70
```

**解释:**
100 是二进制的 01100100。操作主要可以分为两部分
**1)** 表达式“ **x & 0x0F** 给出了 x 的最后 4 位，对于 x = 100，结果为 00000100。使用按位“< <”运算符，我们将最后四位向左移动 4 次，并将新的最后四位设为 0。轮班后的结果是 01000000。
**2)** 表达式“ **x & 0xF0** ”给出了 x 的前四位，对于 x = 100，结果为 01100000。使用按位“> >”运算符，我们将数字向右移动 4 次，并将前四位设为 0。轮班后的结果是 00000110。
最后我们使用上面解释的两个表达式的按位 OR“|”运算。OR 运算符将第一个半字节放在末尾，最后一个半字节放在第一个。对于 x = 100，值(01000000)或(00000110)给出的结果是 01000110，十进制等于 70。
本文由 **Anuj Garg** 供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息