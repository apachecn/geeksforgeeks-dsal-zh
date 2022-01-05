# 将所有位设置在一个数字的给定范围内

> 原文:[https://www.geeksforgeeks.org/set-bits-given-range-number/](https://www.geeksforgeeks.org/set-bits-given-range-number/)

给定一个非负数 n 和两个值 l 和 r，问题是在 n 的二进制表示中设置 l 到 r 范围内的位，即从最右边的第 1 位到最右边的第 r 位不设置位。
约束:1<= l<= r<= n 的二进制表示中的位数
**示例:**

```
Input : n = 17, l = 2, r = 3
Output : 23
(17)10 = (10001)2
(23)10 = (10111)2
The bits in the range 2 to 3 in the binary
representation of 17 are set.

Input : n = 50, l = 2, r = 5
Output : 62
```

方法:步骤如下:

```
1\. Find a number 'range' that has all set
   bits in given range. And all other bits
   of this number are 0.
     range = (((1 << (l - 1)) - 1) ^ 
              ((1 << (r)) - 1));

2\. Now, perform "n = n | range". This will 
   set the bits in the range from l to r 
   in n.
```

## C++

```
// C++ implementation to Set bits in
// the given range
#include <iostream>
using namespace std;

// function to toggle bits in the given range
int setallbitgivenrange(int n, int l, int r)
{
    // calculating a number 'range' having set
    // bits in the range from l to r and all other
    // bits as 0 (or unset).
    int range = (((1 << (l - 1)) - 1) ^   
                ((1 << (r)) - 1));

    return (n | range);
}

// Driver code
int main()
{
    int n = 17, l = 2, r = 3;
    cout << setallbitgivenrange(n, l, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java implementation to Set bits in
// the given range
import java.util.*;

class GFG
{

    // function to toggle bits in the
    // given range
    static int setallbitgivenrange(int n,
                             int l, int r)
    {

        // calculating a number 'range'
        // having set bits in the range
        // from l to r and all other
        // bits as 0 (or unset).
        int range = (((1 << (l - 1)) - 1) ^
                    ((1 << (r)) - 1));

        return (n | range);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 17, l = 2, r = 3;

        System.out.println(setallbitgivenrange(
                                      n, l, r));
    }

}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Python3 implementation to Set
# bits in the given range

# Function to toggle bits
# in the given range
def setallbitgivenrange(n, l, r):

    # calculating a number 'range'
    # having set bits in the range
    # from l to r and all other
    # bits as 0 (or unset).
    range = (((1 << (l - 1)) - 1) ^
                ((1 << (r)) - 1))

    return (n | range)

# Driver code
n, l, r = 17, 2, 3
print(setallbitgivenrange(n, l, r))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# implementation to Set
// bits in the given range
using System;

class GFG
{
    // function to toggle bits
    // in the given range
    static int setallbitgivenrange(int n, int l, int r)
    {

        // calculating a number 'range'
        // having set bits in the range
        // from l to r and all other
        // bits as 0 (or unset).
        int range = (((1 << (l - 1)) - 1) ^
                     ((1 << (r)) - 1));

        return (n | range);
    }

    // Driver code
    static void Main()
    {
        int n = 17, l = 2, r = 3;
        Console.Write(setallbitgivenrange(n, l, r));
    }

}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to Set
// bits in the given range

// function to toggle bits
// in the given range
function setallbitgivenrange($n, $l, $r)
{
    // calculating a number 'range'
    // having set bits in the range
    // from l to r and all other
    // bits as 0 (or unset).
    $range = (((1 << ($l - 1)) - 1) ^
                  ((1 << ($r)) - 1));

    return ($n | $range);
}

// Driver code
$n = 17;
$l = 2;
$r = 3;
echo setallbitgivenrange($n, $l, $r);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript implementation to Set bits in
// the given range

// function to toggle bits in the given range
function setallbitgivenrange(n, l, r)
{
    // calculating a number 'range' having set
    // bits in the range from l to r and all other
    // bits as 0 (or unset).
    let range = (((1 << (l - 1)) - 1) ^   
                ((1 << (r)) - 1));

    return (n | range);
}

// Driver code
    let n = 17, l = 2, r = 3;
    document.write(setallbitgivenrange(n, l, r));

</script>
```

**输出:**

```
23
```

本文由**德万舒·阿加瓦尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。