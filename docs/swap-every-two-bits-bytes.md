# 每两个字节交换一位

> 原文:[https://www.geeksforgeeks.org/swap-every-two-bits-bytes/](https://www.geeksforgeeks.org/swap-every-two-bits-bytes/)

交换一个字节中的所有位对。交换前:11-10-11-01 交换后:11-01-11-10
示例:

```
Input  : 00000010
Output : 00000001

Input  : 00000100
Output : 00001000
```

**方法:**
x =((x&0b 10101010)>>1)|((x&0b 01010101)<>1 提取高位比特位置并将其移动到低位比特位置。
类似地，表达式(x & 0b01010101) < < 1 从每对中提取低位，并将其移动到高位位置。
然后使用按位“或”将这两部分组合起来。

```
x= 00011010
((x & 0b10101010) >> 1) = 00001010 >> 1
                        = 00000101
((x & 0b01010101) << 1) = 00010000 <> 1) | ((x & 0b01010101) << 1) = 00100101
```

下面是上面的实现:
**注:**这个解决方案只适用于 8 位。

## C++

```
// C++ program to swap every two bits in a byte.
#include<bits/stdc++.h>
using namespace std;

unsigned int swapBitsInPair(unsigned int x)
{
    // Extracting the high bit shift it to lowbit
    // Extracting the low bit shift it to highbit
    return ((x & 0b10101010) >> 1) |
            ((x & 0b01010101) << 1);   
}

/* Driver function to test above function */
int main()
{
    unsigned int x = 4;
    cout << swapBitsInPair(x);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to swap every
// two bits in a byte.
import java.util.*;

class GFG
{
    static int swapBitsInPair( int x)
    {
        // Extracting the high bit shift it to lowbit
        // Extracting the low bit shift it to highbit
        return ((x & 0b10101010) >> 1) |
                ((x & 0b01010101) << 1);
    }

    // Driver Function
    public static void main(String[] args)
    {
    int x = 4;
    System.out.print(swapBitsInPair(x));
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python program to swap every
# two bits in a byte.

import math

def swapBitsInPair( x):

    # Extracting the high bit shift it to lowbit
    # Extracting the low bit shift it to highbit
    return ((x & 0b10101010) >> 1) or ((x & 0b01010101) << 1)

# driver Function
x = 4;
print(swapBitsInPair(x))

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to swap every two bits in a byte.
using System;

public class GFG{

    static uint swapBitsInPair(uint x)
    {
        // Extracting the high bit shift it to lowbit
        // Extracting the low bit shift it to highbit
        return ((x & 010101010) >> 1) |
                ((x & 001010101) << 1);
    }

    // Driver function to test above function
    static public void Main () {

        uint x = 4;

        Console.WriteLine(swapBitsInPair(x));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to swap every
// two bits in a byte.

function swapBitsInPair($x)
{

    // Extracting the high bit
    // shift it to lowbit
    // Extracting the low bit
    // shift it to highbit
    return (($x & 0b10101010) >> 1) |
           (($x & 0b01010101) << 1);
}

    // Driver Code
    $x = 4;
    echo swapBitsInPair($x);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// java script program to swap every
// two bits in a byte.

function swapBitsInPair(x)
{

    // Extracting the high bit
    // shift it to lowbit
    // Extracting the low bit
    // shift it to highbit
    return ((x & 0b10101010) >> 1) |
           ((x & 0b01010101) << 1);
}

    // Driver Code
    let x = 4;
    document.write( swapBitsInPair(x));

// This code is contributed by sravan kumar
</script>
```

输出:

```
8
```

**参考:**
[https://stackoverflow . com/questions/4788799/交换每对字节位](https://stackoverflow.com/questions/4788799/swap-every-pair-of-bits-in-byte)