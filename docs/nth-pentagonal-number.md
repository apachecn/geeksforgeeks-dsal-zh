# 第 n 个五边形数字

> 原文:[https://www.geeksforgeeks.org/nth-pentagonal-number/](https://www.geeksforgeeks.org/nth-pentagonal-number/)

给定一个整数 n，求第 n 个五边形数。前三个五边形数字是 1、5 和 12(请看下图)。
第 n 个五边形数字 P <sub>n</sub> 是由规则五边形的轮廓组成的点图案中的不同点的数量，当五边形重叠时，边长可达 n 个点【来源[Wiki](https://en.wikipedia.org/wiki/Pentagonal_number)
T6】示例:T8】

```
Input: n = 1
Output: 1

Input: n = 2
Output: 5

Input: n = 3
Output: 12
```

一般来说，[多边形数](https://en.wikipedia.org/wiki/Polygonal_number)(三角形数、正方形数等)是以正多边形形状排列的点或卵石表示的数。前几个五边形数字是:1、5、12 等。
如果 s 是多边形的边数，则第 n 个边数 P (s，n)的公式为

```
nth s-gonal number P(s, n) = (s - 2)n(n-1)/2 + n

If we put s = 5, we get

n'th Pentagonal number Pn = 3*n*(n-1)/2 + n
```

示例:

**五边形数字**

![Pentagonal Number](img/62484653e1ee38520f460db8fe1a29de.png)

下面是上述思想在不同编程语言中的实现。

## C++

```
// C++ program for above approach
#include<bits/stdc++.h>
using namespace std;

// Finding the nth pentagonal number
int pentagonalNum(int n)
{
    return (3 * n * n - n) / 2;
}

// Driver code
int main()
{
    int n = 10;

    cout << "10th Pentagonal Number is = "
         << pentagonalNum(n);

    return 0;
}

// This code is contributed by Code_Mech
```

## C

```
// C program for above approach
#include <stdio.h>
#include <stdlib.h>

// Finding the nth Pentagonal Number
int pentagonalNum(int n)
{
    return (3*n*n - n)/2;
}

// Driver program to test above function
int main()
{
    int n = 10;
    printf("10th Pentagonal Number is = %d \n \n",
                             pentagonalNum(n));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class Pentagonal
{
    int pentagonalNum(int n)
    {
        return (3*n*n - n)/2;
    }
}

public class GeeksCode
{
    public static void main(String[] args)
    {
        Pentagonal obj = new Pentagonal();
        int n = 10;   
        System.out.printf("10th petagonal number is = "
                          + obj.pentagonalNum(n));
    }
}
```

## 计算机编程语言

```
# Python program for finding pentagonal numbers
def pentagonalNum( n ):
    return (3*n*n - n)/2
#Script Begins

n = 10
print "10th Pentagonal Number is = ", pentagonalNum(n)

#Scripts Ends
```

## C#

```
// C# program for above approach
using System;

class GFG {

    static int pentagonalNum(int n)
    {
        return (3 * n * n - n) / 2;
    }

    public static void Main()
    {
        int n = 10;

        Console.WriteLine("10th petagonal"
        + " number is = " + pentagonalNum(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for above approach

// Finding the nth Pentagonal Number
function pentagonalNum($n)
{
    return (3 * $n * $n - $n) / 2;
}

// Driver Code
$n = 10;
echo "10th Pentagonal Number is = ",
                  pentagonalNum($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program for above approach

    function pentagonalNum(n)
    {
        return (3 * n * n - n) / 2;
    }

// Driver code to test above methods

        let n = 10;

        document.write("10th petagonal"
        + " number is = " + pentagonalNum(n));

         // This code is contributed by avijitmondal1998.
</script>
```

**输出:**

```
10th Pentagonal Number is = 145
```

**时间复杂度:** O(1)
**辅助空间:** O(1)
参考:
[https://en.wikipedia.org/wiki/Polygonal_number](https://en.wikipedia.org/wiki/Polygonal_number)
本文由**马扎伊玛目汗**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。