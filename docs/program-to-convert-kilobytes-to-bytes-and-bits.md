# 将千字节转换为字节和位的程序

> 原文:[https://www . geesforgeks . org/program-to-convert-kb-bytes-and-bits/](https://www.geeksforgeeks.org/program-to-convert-kilobytes-to-bytes-and-bits/)

给定千字节数。任务是将它们转换成字节和位。
**Bit:**Bit 是计算机信息中的基本单位，只有**两个不同的值**，通常定义为一个 **0 或一个**。这些值可以解释为开或关、是或否、真或假等。这取决于二进制代码。
加 1 位，图案数量翻倍。

> **1 位**–2 个模式即 0 和 1
> **2 位**–4 个模式即 00、01、10、11
> **3 位**–8 个模式即 000、001、010、011、100、101、110、111

**数学上** : n 位产生 2 <sup>n</sup> 模式。
**字节:**一个字节只有 8 位，是许多计算机系统中可以寻址的最小内存单元。

关于字节的要点:

*   一个字节可以存储一个字符，例如“A”或“x”或“内容”。等等。
*   1 个字节，即 8 位，可以构成 256 种不同的模式。
*   一个字节可以容纳 0 到 255 之间的数字。
*   不同的形式:-
    1.  千字节，KB，约 1000 字节。
    2.  兆字节，MB，约 100 万字节。
    3.  千兆字节，GB，约 10 亿字节。
    4.  万亿字节，约 1 万亿字节

**示例:**

```
Input: kilobytes = 1
Output: 1 Kilobytes = 1024 Bytes and 8192 Bits.

Input: kilobytes = 8
Output: 8 Kilobytes = 8192 Bytes and 65536 Bits.
```

以下是将千字节转换为字节和位的程序:

## C++

```
// C++ implementation of above program
#include <bits/stdc++.h>
using namespace std;

// Function to calculates the bits
long Bits(int kilobytes)
{
    long Bits = 0;

    // calculates Bits
    // 1 kilobytes(s) = 8192 bits
    Bits = kilobytes * 8192;

    return Bits;
}

// Function to calculates the bytes
long Bytes(int kilobytes)
{
    long Bytes = 0;

    // calculates Bytes
    // 1 KB = 1024 bytes
    Bytes = kilobytes * 1024;

    return Bytes;
}

// Driver code
int main()
{
    int kilobytes = 1;

    cout << kilobytes << " Kilobytes = "
         << Bytes(kilobytes) << " Bytes and "
         << Bits(kilobytes) << " Bits.";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above program

import java.util.*;
import java.lang.*;
import java.io.*;
import java.math.BigInteger;

class GFG
{

// Function to calculates the bits
static BigInteger Bits(int kilobytes)
{
    BigInteger  Bits = new BigInteger("0");

    // calculates Bits
    // 1 kilobytes(s) = 8192 bits

    BigInteger kilo = BigInteger.valueOf(kilobytes);
    Bits = kilo.multiply(BigInteger.valueOf(8192));

    return Bits;
}

// Function to calculates the bytes
static BigInteger Bytes(int kilobytes)
{
    BigInteger Bytes = new BigInteger("0");

    // calculates Bytes
    // 1 KB = 1024 bytes

   BigInteger kilo = BigInteger.valueOf(kilobytes);
   Bytes = kilo.multiply(BigInteger.valueOf(1024));

    return Bytes;
}

// Driver code
public static void main(String args[])
{
    int kilobytes = 1;

    System.out.print(kilobytes + " Kilobytes = "
         + Bytes(kilobytes) + " Bytes and "
         + Bits(kilobytes) + " Bits.");
}
}
```

## 蟒蛇 3

```
# Python implementation of above program

# Function to calculates the bits
def Bits(kilobytes) :

    # calculates Bits
    # 1 kilobytes(s) = 8192 bits
    Bits = kilobytes * 8192

    return Bits

# Function to calculates the bytes
def Bytes(kilobytes) :

    # calculates Bytes
    # 1 KB = 1024 bytes
    Bytes = kilobytes * 1024

    return Bytes

# Driver code
if __name__ == "__main__" :

    kilobytes = 1

    print(kilobytes, "Kilobytes =",
    Bytes(kilobytes) , "Bytes and",
    Bits(kilobytes), "Bits")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation of above program
using System;

class GFG
{

// Function to calculates the bits
static long Bits(int kilobytes)
{
    long Bits = 0;

    // calculates Bits
    // 1 kilobytes(s) = 8192 bits
    Bits = kilobytes * 8192;

    return Bits;
}

// Function to calculates the bytes
static long Bytes(int kilobytes)
{
    long Bytes = 0;

    // calculates Bytes
    // 1 KB = 1024 bytes
    Bytes = kilobytes * 1024;

    return Bytes;
}

// Driver code
static public void Main ()
{
    int kilobytes = 1;

    Console.WriteLine (kilobytes +" Kilobytes = "+
                 Bytes(kilobytes) + " Bytes and "+
                  Bits(kilobytes) + " Bits.");
}
}

// This code is contributed by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above program

// Function to calculates the bits
function Bits($kilobytes)
{
    $Bits = 0;

    // calculates Bits
    // 1 kilobytes(s) = 8192 bits
    $Bits = $kilobytes * 8192;

    return $Bits;
}

// Function to calculates the bytes
function Bytes($kilobytes)
{
    $Bytes = 0;

    // calculates Bytes
    // 1 KB = 1024 bytes
    $Bytes = $kilobytes * 1024;

    return $Bytes;
}

// Driver code
$kilobytes = 1;

echo $kilobytes;
echo (" Kilobytes = ");
echo Bytes($kilobytes);
echo (" Bytes and ");
echo Bits($kilobytes);
echo (" Bits.");

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above program

function Bits(kilobytes)
{
    var Bits = 0;

    // Calculates Bits
    // 1 kilobytes(s) = 8192 bits
    Bits = kilobytes * 8192;

    return Bits;
}

// Function to calculates the bytes
function Bytes(kilobytes)
{
    var Bytes = 0;

    // Calculates Bytes
    // 1 KB = 1024 bytes
    Bytes = kilobytes * 1024;

    return Bytes;
}

// Driver code
var kilobytes = 1;

document.write(kilobytes + " Kilobytes = " +
               Bytes(kilobytes) + " Bytes and " +
               Bits(kilobytes) + " Bits.");

// This code is contributed by akshitsaxenaa09

</script>
```

**Output:**

```
1 Kilobytes = 1024 Bytes and 8192 Bits.
```