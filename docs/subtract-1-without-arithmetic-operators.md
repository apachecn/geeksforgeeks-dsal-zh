# 不带算术运算符减 1

> 原文:[https://www . geesforgeks . org/减法-1-不带算术运算符/](https://www.geeksforgeeks.org/subtract-1-without-arithmetic-operators/)

写一个程序从给定的数中减去一。不允许使用“+”、“-”、“*”、“/”、“++”、“–”…等运算符。

**示例:**

```
Input:  12
Output: 11

Input:  6
Output: 5
```

**方法 1**
要从数字 x 中减去 1(比如 0011001000)，翻转最右边 1 位之后的所有位(我们得到 001100 **1** 111)。最后，翻转最右边的 1 位(我们得到 0011000111)得到答案。

## C++

```
// C++ code to subtract
// one from a given number
#include <iostream>
using namespace std;

int subtractOne(int x)
{
    int m = 1;

    // Flip all the set bits
    // until we find a 1
    while (!(x & m))
    {
        x = x ^ m;
        m <<= 1;
    }

    // Flip the rightmost 1 bit
    x = x ^ m;
    return x;
}

// Driver code
int main()
{
    cout << subtractOne(13) << endl;
    return 0;
}

// This code is contributed by noob2000
```

## C

```
// C code to subtract
// one from a given number
#include <stdio.h>

int subtractOne(int x)
{
    int m = 1;

    // Flip all the set bits
    // until we find a 1
    while (!(x & m)) {
        x = x ^ m;
        m <<= 1;
    }

    // flip the rightmost 1 bit
    x = x ^ m;
    return x;
}

/* Driver program to test above functions*/
int main()
{
    printf("%d", subtractOne(13));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to subtract
// one from a given number
import java.io.*;

class GFG
{
static int subtractOne(int x)
{
    int m = 1;

    // Flip all the set bits
    // until we find a 1
    while (!((x & m) > 0))
    {
        x = x ^ m;
        m <<= 1;
    }

    // flip the rightmost
    // 1 bit
    x = x ^ m;
    return x;
}

// Driver Code
public static void main (String[] args)
{
    System.out.println(subtractOne(13));
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python 3 code to subtract one from
# a given number
def subtractOne(x):
    m = 1

    # Flip all the set bits
    # until we find a 1
    while ((x & m) == False):
        x = x ^ m
        m = m << 1

    # flip the rightmost 1 bit
    x = x ^ m
    return x

# Driver Code
if __name__ == '__main__':
    print(subtractOne(13))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# code to subtract
// one from a given number
using System;

class GFG
{
static int subtractOne(int x)
{
    int m = 1;

    // Flip all the set bits
    // until we find a 1
    while (!((x & m) > 0))
    {
        x = x ^ m;
        m <<= 1;
    }

    // flip the rightmost
    // 1 bit
    x = x ^ m;
    return x;
}

// Driver Code
public static void Main ()
{
    Console.WriteLine(subtractOne(13));
}
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to subtract
// one from a given number

function subtractOne($x)
{
    $m = 1;

    // Flip all the set bits
    // until we find a 1
    while (!($x & $m))
    {
        $x = $x ^ $m;
        $m <<= 1;
    }

    // flip the
    // rightmost 1 bit
    $x = $x ^ $m;
    return $x;
}

// Driver Code
    echo subtractOne(13);

// This code is contributed
// by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript code to subtract
// one from a given number

function subtractOne(x)
{
    let m = 1;

    // Flip all the set bits
    // until we find a 1
    while (!(x & m)) {
        x = x ^ m;
        m <<= 1;
    }

    // flip the rightmost 1 bit
    x = x ^ m;
    return x;
}

/* Driver program to test above functions*/

    document.write(subtractOne(13));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
12
```

**方法 2(如果允许+的话)**
我们知道负数在大多数架构上是以 2 的补码形式表示的。对于有符号数的 2 补码表示，我们有以下引理。
说，x 是一个数的数值，那么
~ x =-(x+1)【~是用于按位补码】
两边加 2x，
2x+~ x = x–1
得到 2x，左移 x 一次。

## C++

```
#include <stdio.h>

int subtractOne(int x)
{
    return ((x << 1) + (~x));
}

/* Driver program to test above functions*/
int main()
{
    printf("%d", subtractOne(13));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG
{

    static int subtractOne(int x)
    {
        return ((x << 1) + (~x));
    }

    /* Driver code*/
    public static void main(String[] args)
    {
        System.out.printf("%d", subtractOne(13));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
def subtractOne(x):

    return ((x << 1) + (~x));

# Driver code
print(subtractOne(13));

# This code is contributed by mits
```

## C#

```
using System;

class GFG
{

    static int subtractOne(int x)
    {
        return ((x << 1) + (~x));
    }

    /* Driver code*/
    public static void Main(String[] args)
    {
        Console.Write("{0}", subtractOne(13));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
function subtractOne($x)
{
    return (($x << 1) + (~$x));
}

/* Driver code*/

print(subtractOne(13));

// This code has been contributed by mits
?>
```

## java 描述语言

```
<script>

function subtractOne(x)
{
    return ((x << 1) + (~x));
}

/* Driver program to test above functions*/

    document.write((subtractOne(13)));

// This is code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
12
```