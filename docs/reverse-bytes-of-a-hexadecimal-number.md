# 反转十六进制数的字节

> 原文:[https://www . geesforgeks . org/16 进制数的反向字节数/](https://www.geeksforgeeks.org/reverse-bytes-of-a-hexadecimal-number/)

给定一个无符号整数 **N** 。任务是在不使用临时变量的情况下反转 **N** 的所有字节，并打印反转后的数字。

**示例:**

> **输入:**N = 0x aabbccdd
> T3】输出: 0xddccbbaa
> 
> **输入:**N = 0xa 912 CBD 4
> T3】输出: 0xd4cb12a9

**天真的**方法是提取适当的字节是使用带移位运算符的掩码(&)。

> #定义 REV(x)(((x & 0x ff 000000)> > 24)|((x & 0x 00ff 0000)<<8)>> 16)|((x & 0x 0000 ff 00)> > 8)<<16) |
> ((x&0x 000000 ff)<T4】24))

**高效方法:**
思路是只使用移位运算符。

*   使用左移位运算符(<
*   使用右移运算符(>>)将第一个字节的位置移动到最后一个字节。
*   使用左移位和右移位运算符的组合来移动中间的字节。
*   对上述所有表达式的输出应用逻辑 OR (|)，以获得所需的输出。

下面是上述方法的实现:

```
// C program to reverse bytes of a hexadecimal number
#include <stdio.h>
// macro which reverse the hexadecimal integer
#define REV(n) ((n << 24) | (((n>>16)<<24)>>16) | \
                    (((n<<16)>>24)<<16) | (n>>24))

// Driver code
int main()
{
    unsigned int n = 0xa912cbd4;

    //  n = 0xaabbccdd
    // (n >> 24) - 0x000000aa
    // (n << 24) - 0xdd000000
    // (((n >> 16) << 24) >> 16) - 0xbb00
    // (((n >> 8) << 24) >> 8) - 0xcc0000
    // If output of all the above expression is 
    // OR'ed then it results in 0xddccbbaa

    printf("%x is reversed to %x", n, REV(n));

    return 0;
}
```

**Output:**

```
a912cbd4 is reversed to d4cb12a9

```