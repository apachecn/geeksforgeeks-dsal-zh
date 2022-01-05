# 六角形号

> 原文:[https://www.geeksforgeeks.org/hexagonal-number/](https://www.geeksforgeeks.org/hexagonal-number/)

给定一个整数 n，任务是找到第 n 个[六边形数](https://en.wikipedia.org/wiki/Hexagonal_number)。第 n 个六边形数 Hn 是由规则六边形的轮廓组成的点图案中的不同点的数量，当六边形重叠以共享一个顶点时，边多达 n 个点。{来源:[维基](https://en.wikipedia.org/wiki/Hexagonal_number) }

```
Input: n = 2
Output: 6

Input: n = 5
Output: 45

Input: n = 7
Output: 91
```

一般来说，[多边形数](https://en.wikipedia.org/wiki/Polygonal_number)(三角形数、正方形数等)是以正多边形形状排列的点或卵石表示的数。前几个五边形数字是 1、5、12 等。
如果 s 是多边形的边数，则第 n 个边数 P (s，n)的公式为

```
nth s-gonal number P(s, n) = (s - 2)n(n-1)/2 + n

If we put s = 6, we get

n'th Hexagonal number Hn = 2(n*n)-n 
                             = n(2n - 1) 
```

## C

```
// C program for above approach
#include <stdio.h>
#include <stdlib.h>

// Finding the nth Hexagonal Number
int hexagonalNum(int n)
{
    return n*(2*n - 1);
}

// Driver program to test above function
int main()
{
    int n = 10;
    printf("10th Hexagonal Number is = %d",
                             hexagonalNum(n));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class Hexagonal
{
    int hexagonalNum(int n)
    {
        return n*(2*n - 1);
    }
}

public class GeeksCode
{
    public static void main(String[] args)
    {
        Hexagonal obj = new Hexagonal();
        int n = 10;
        System.out.printf("10th Hexagonal number is = "
                          + obj.hexagonalNum(n));
    }
}
```

## 计算机编程语言

```
# Python program for finding Hexagonal numbers
def hexagonalNum( n ):
    return n*(2*n - 1)

# Driver code
n = 10
print "10th Hexagonal Number is = ", hexagonalNum(n)
```

## C#

```
// C# program for above approach
using System;

class GFG {

    static int hexagonalNum(int n)
    {
        return n * (2 * n - 1);
    }

    public static void Main()
    {

        int n = 10;

        Console.WriteLine("10th Hexagonal"
        + " number is = " + hexagonalNum(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for above approach

// Finding the nth Hexagonal Number
function hexagonalNum($n)
{
    return $n * (2 * $n - 1);
}

// Driver program to test above function
$n = 10;
echo("10th Hexagonal Number is " .
                        hexagonalNum($n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program for above approach

// centered pentadecagonal function
function hexagonalNum(n)
{
    return n * (2 * n - 1);
}

// Driver Code
var n = 10;
document.write("10th Hexagonal number is = " +
               hexagonalNum(n));

// This code is contributed by Kirti

</script>
```

**输出:**

```
10th Hexagonal Number is =  190
```

参考:[https://en.wikipedia.org/wiki/Hexagonal_number](https://en.wikipedia.org/wiki/Hexagonal_number)
本文由**尼尚特 _ 辛格(平图)**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客网的主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。