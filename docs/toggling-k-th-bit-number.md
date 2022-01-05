# 切换数字的第 k 位

> 原文:[https://www.geeksforgeeks.org/toggling-k-th-bit-number/](https://www.geeksforgeeks.org/toggling-k-th-bit-number/)

对于给定的数字 n，如果第 k 位为 0，则切换为 1，如果为 1，则切换为 0。
**例:**

```
Input : n = 5, k = 1
Output : 4
5 is represented as 101 in binary
and has its first bit 1, so toggling 
it will result in 100 i.e. 4.

Input : n = 2, k = 3
Output : 6

Input : n = 75, k = 4
Output : 67
```

以下是找到第 k 位
值的简单步骤

```
1) Left shift given number 1 by k-1 to create 
   a number that has only set bit as k-th bit.
    temp = 1 << (k-1)
2) Return bitwise XOR of temp and n.  Since temp
   has only k-th bit set, doing XOR would toggle 
   only this bit.
```

**示例:**

```
 n = 75 and k = 4
 temp = 1 << (k-1) = 1 << 3 = 8 
 Binary Representation of temp = 0..00001000 
 Binary Representation of n = 0..01001011 
 Bitwise XOR of two numbers = 0..01000011
```

## C++

```
// CPP program to toggle k-th bit of n
#include<iostream>
using namespace std;

int toggleKthBit(int n, int k)
{
    return (n ^ (1 << (k-1)));
}

// Driver code
int main()
{
    int n = 5, k = 1;
    cout << toggleKthBit(n , k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to toggle
// k-th bit of a number

class Toggle
{
    static int toggleKthBit(int n, int k)
    {
        return (n ^ (1 << (k-1)));
    }

    // main function
    public static void main (String[] args)
    {  
        int n = 5, k = 1;
        System.out.println(toggleKthBit(n , k));
    }
}
```

## 蟒蛇 3

```
# Python3 code to toggle k-th bit of n

def toggleKthBit(n, k):
    return (n ^ (1 << (k-1)))

# Driver code
n = 5
k = 1
print( toggleKthBit(n , k))

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to toggle
// k-th bit of a number
using System;

class GFG {

    static int toggleKthBit(int n, int k)
    {
        return (n ^ (1 << (k-1)));
    }

    // main function
    public static void Main()
    {  
        int n = 5, k = 1;

        Console.WriteLine(toggleKthBit(n , k));
    }
}

//This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php program to toggle k-th bit of n

function toggleKthBit($n, $k)
{
    return ($n ^ (1 << ($k - 1)));
}

// Driver code
$n = 5;
$k = 1;
echo toggleKthBit($n, $k);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to toggle
    // k-th bit of a number

    function toggleKthBit(n, k)
    {
        return (n ^ (1 << (k-1)));
    }

    let n = 5, k = 1;

      document.write(toggleKthBit(n , k));

</script>
```

**输出:**

```
4
```

本文由 **SAKSHI TIWARI** 供稿。如果你喜欢极客(我们知道你喜欢！)并愿意投稿，也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者将文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。