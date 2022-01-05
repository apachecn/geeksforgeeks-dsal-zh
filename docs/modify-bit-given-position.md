# 在给定位置修改一个位

> 原文:[https://www.geeksforgeeks.org/modify-bit-given-position/](https://www.geeksforgeeks.org/modify-bit-given-position/)

给定一个数字 **n** ，一个位置 **p** 和一个二进制值 **b** ，我们需要将 n 中位置 p 处的位改为值 b。

**示例:**

```
Input : n = 7, p = 2, b = 0
Output : 3
7 is 00000111 after clearing bit at 
2rd position, it becomes 0000011.

Input : n = 7, p = 3, b = 1
Output : 15
7 is 00000111 after setting bit at 
3rd position it becomes 00001111.
```

```
We first create a mask that has set bit only 
at given position using bit wise shift.
      mask = 1 << position

Then to change value of bit to b, we first
make it 0 using below operation
      value & ~mask

After changing it 0, we change it to b by
doing or of above expression with following
(b << p) & mask, i.e., we return
      ((n & ~mask) | (b << p))
```

以下是上述步骤的实现:

## C++

```
// CPP program to modify a bit at position
// p in n to b.
#include <bits/stdc++.h>
using namespace std;

// Returns modified n.
int modifyBit(int n, int p, int b)
{
    int mask = 1 << p;
    return ((n & ~mask) | (b << p));
}

// Driver code
int main()
{
    cout << modifyBit(6, 2, 0) << endl;
    cout << modifyBit(6, 5, 1) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to modify a bit
// at position p in n to b.
import java.io.*;

class GFG
{

// Returns modified n.
public static int modifyBit(int n,
                            int p,
                            int b)
{
    int mask = 1 << p;
    return (n & ~mask) |
           ((b << p) & mask);
}
    // Driver Code
    public static void main (String[] args)
    {
        System.out.println(modifyBit(6, 2, 0));
        System.out.println (modifyBit(6, 5, 1));
    }
}

// This code is contributed by m_kit
```

## 蟒蛇 3

```
# Python3 program to modify a bit at position
# p in n to b.

# Returns modified n.
def modifyBit( n,  p,  b):
    mask = 1 << p
    return (n & ~mask) | ((b << p) & mask)

# Driver code
def main():
    print(modifyBit(6, 2, 0))
    print(modifyBit(6, 5, 1))

if __name__ == '__main__':
    main()
# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to modify a bit
// at position p in n to b.
using System;

class GFG
{
// Returns modified n.
public static int modifyBit(int n,
                            int p,
                            int b)
{
    int mask = 1 << p;
    return (n & ~mask) |
           ((b << p) & mask);
}

    // Driver Code
    static public void Main ()
    {

        Console.WriteLine(modifyBit(6, 2, 0));
        Console.WriteLine(modifyBit(6, 5, 1));
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to modify a bit
// at position p in n to b.

// Returns modified n.
function modifyBit($n, $p, $b)
{
    $mask = 1 << $p;
    return ($n & ~$mask) |
           (($b << $p) & $mask);
}

    // Driver code
    echo modifyBit(6, 2, 0),"\n";
    echo modifyBit(6, 5, 1) ,"\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to modify a bit
// at position p in n to b.

// Returns modified n.
function modifyBit(n, p, b)
{
    let mask = 1 << p;
    return (n & ~mask) |
           ((b << p) & mask);
}

// Driver code
document.write(modifyBit(6, 2, 0) + "<br/>");
document.write(modifyBit(6, 5, 1));

// This code is contributed by susmitakundugoaldanga

</script>
```

**输出:**

```
 2
 38
```

**时间复杂度:** O(1)

本文由 [**帕万·阿西普**](https://www.facebook.com/pawan.asipu.5) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。