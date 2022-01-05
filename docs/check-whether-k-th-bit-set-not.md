# 检查第 K 位是否置位

> 原文:[https://www . geesforgeks . org/check-what-k-th-bit-set-not/](https://www.geeksforgeeks.org/check-whether-k-th-bit-set-not/)

给定一个数字 n，检查 n 的 Kth 位是否置位。

**示例:**

```
Input : n = 5, k = 1
Output : SET
5 is represented as 101 in binary and has its first bit set.

Input : n = 2, k = 3
Output : NOT SET
2 is represented as 10 in binary, all higher i.e. beyond MSB, bits are NOT SET.
```

**方法 1(使用左移运算符)**
下面是查找第 k 位值的简单步骤:

```
1) Left shift given number 1 by k-1 to create a number that has only set bit as k-th bit.
   temp = 1 << (k-1)
2) If bitwise AND of n and temp is non-zero, then result is SET else result is NOT SET.
```

**示例:**

```
 n = 75 and k = 4
 temp = 1 << (k-1) = 1 << 3 = 8 
 Binary Representation of temp = 0..00001000 
 Binary Representation of n = 0..01001011 
 Since bitwise AND of n and temp is non-zero, result is SET.
```

## C++

```
// CPP program to check if k-th bit
// of a given number is set or not
#include <iostream>
using namespace std;

void isKthBitSet(int n, int k)
{
    if (n & (1 << (k - 1)))
        cout << "SET";
    else
        cout << "NOT SET";
}

// Driver code
int main()
{
    int n = 5, k = 1;
    isKthBitSet(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if k-th bit
// of a given number is set or not

class Number {
    public static void isKthBitSet(int n,
                                   int k)
    {
        if ((n & (1 << (k - 1))) > 0)
            System.out.print("SET");
        else
            System.out.print("NOT SET");
    }

    // driver code
    public static void main(String[] args)
    {
        int n = 5, k = 1;
        isKthBitSet(n, k);
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 code to check if k-th bit
# of a given number is set or not

def isKthBitSet(n, k):
    if n & (1 << (k - 1)):
        print( "SET")
    else:
        print("NOT SET")

# Driver code
n = 5
k = 1
isKthBitSet(n, k)

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to check if k-th bit
// of a given number is set or not.
using System;

class GFG {

    public static void isKthBitSet(int n,
                                   int k)
    {
        if ((n & (1 << (k - 1))) > 0)
            Console.Write("SET");
        else
            Console.Write("NOT SET");
    }

    // Driver code
    public static void Main()
    {
        int n = 5, k = 1;

        isKthBitSet(n, k);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// k-th bit of a given
// number is set or not
function isKthBitSet($n, $k)
{
    if ($n & (1 << ($k - 1)))
        echo "SET";
    else
        echo "NOT SET";
}

// Driver code
$n = 5; $k = 1;
isKthBitSet($n, $k);

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if k-th bit
    // of a given number is set or not.

    function isKthBitSet(n, k)
    {
        if ((n & (1 << (k - 1))) > 0)
            document.write("SET");
        else
            document.write("NOT SET");
    }

    let n = 5, k = 1;

      isKthBitSet(n, k);

</script>
```

**输出:**

```
SET
```

**方法 2(使用右移运算符)**
如果我们将 n 右移 k-1，如果第 Kth 位设置为 else 0，则最后一位为 1。

## C++

```
// CPP program to check if k-th bit
// of a given number is set or not using
// right shift operator.
#include <iostream>
using namespace std;

void isKthBitSet(int n, int k)
{
    if ((n >> (k - 1)) & 1)
        cout << "SET";
    else
        cout << "NOT SET";
}

// Driver code
int main()
{
    int n = 5, k = 1;
    isKthBitSet(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if
// k-th bit of a given number
// is set or not using right
// shift operator.
import java.io.*;

class GFG
{
static void isKthBitSet(int n,
                        int k)
{
    if (((n >> (k - 1)) &
               1) > 0)
        System.out.println("SET");
    else
        System.out.println("NOT SET");
}

// Driver code
public static void main (String[] args)
{
    int n = 5, k = 1;
    isKthBitSet(n, k);
}
}

// This code is contributed
// by ajit
```

## 蟒蛇 3

```
# PHP program to check if k-th bit of
# a given number is set or not using
# right shift operator.

def isKthBitSet(n, k):
    if ((n >> (k - 1)) and 1):
        print("SET")
    else:
        print("NOT SET")

# Driver code
n, k = 5, 1
isKthBitSet(n, k)

# This code contributed by
# PrinciRaj1992
```

## C#

```
// C# program to check if
// k-th bit of a given number
// is set or not using right
// shift operator
using System;

class GFG
{
static void isKthBitSet(int n,
                        int k)
{
    if (((n >> (k - 1)) &
              1) > 0)
        Console.WriteLine("SET");
    else
        Console.WriteLine("NOT SET");
}

// Driver code
static public void Main ()
{
    int n = 5, k = 1;
    isKthBitSet(n, k);
}
}

// This code is contributed
// by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check
// if k-th bit of a given
// number is set or not
// using right shift operator.

function isKthBitSet($n, $k)
{
    if (($n >> ($k - 1)) & 1)
        echo "SET";
    else
        echo "NOT SET";
}

// Driver code
$n = 5; $k = 1;
isKthBitSet($n, $k);

// This code is contributed
// by akt_mit
?>
```

## java 描述语言

```
<script>

// Javascript program to check if
// k-th bit of a given number
// is set or not using right
// shift operator.

function isKthBitSet(n, k)
{
    if (((n >> (k - 1)) &
               1) > 0)
        document.write("SET");
    else
        document.write("NOT SET");
}

// Driver Code

    let n = 5, k = 1;
    isKthBitSet(n, k);

// This code is contributed by sanjoy_62.
</script>
```

**输出:**

```
SET
```

本文由 **SAKSHI TIWARI** 供稿。如果你喜欢极客(我们知道你喜欢！)并愿意投稿，也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者将文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。