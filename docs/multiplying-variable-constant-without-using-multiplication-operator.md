# 不使用乘法运算符将变量乘以常数

> 原文:[https://www . geeksforgeeks . org/乘法-变量-常数-不使用乘法-运算符/](https://www.geeksforgeeks.org/multiplying-variable-constant-without-using-multiplication-operator/)

我们知道，每个数都可以用 2 的幂的和(或差)来表示，所以我们能做的就是用 2 的幂的和来表示常数。
为此，我们可以使用按位左移运算符。当一个数按位左移时，每移一位就乘以 2。
例如，假设我们想把一个变量“a”乘以 10，那么我们能做的就是

```
a = a << 3 + a << 1;
```

表达式 a << 3 multiplies a by 8 ans expression a<<1 multiplies it by 2.
所以基本上我们这里有 a = a*8 + a*2 = a*10
同样，对于乘以 7，我们能做的是

```
a = a<<3 - a;
or
a = a<<2 + a<<1 + a;
```

这两种说法都是 a 乘以 7。

## C++

```
#include<iostream>
using namespace std;

// Returns n * 7
int multiplyBySeven(int n)
{
    // OR (n << 2) + (n << 1) + n
    return (n << 3) - n;
}

// Returns n * 12
int multiplyByTwelve(int n)
{
    return (n << 3) + (n << 2);
}

int main()
{
    cout << multiplyBySeven(5) << endl;
    cout << multiplyByTwelve(5) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {

    // Returns n * 7
    static int multiplyBySeven(int n)
    {

        // OR (n << 2) + (n << 1) + n
        return (n << 3) - n;
    }

    // Returns n * 12
    static int multiplyByTwelve(int n)
    {
        return (n << 3) + (n << 2);
    }

    // Driver code
    public static void main(String[] args)
    {
        System.out.println(multiplyBySeven(5));
        System.out.println(multiplyByTwelve(5));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to Multiplying a
# variable with a constant

# Returns n * 7
def multiplyBySeven(n):

    # OR (n << 2) + (n << 1) + n
    return (n << 3) - n

# Returns n * 12
def multiplyByTwelve(n):
    return (n << 3) + (n << 2)

# Driver code
print(multiplyBySeven(5))
print(multiplyByTwelve(5))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to Multiplying a
// variable with a constant
using System;

class GFG
{
    // Returns n * 7
    static int multiplyBySeven(int n)
    {
        // OR (n << 2) + (n << 1) + n
        return (n << 3) - n;
    }

    // Returns n * 12
    static int multiplyByTwelve(int n)
    {
        return (n << 3) + (n << 2);
    }

    // Driver code
    public static void Main()
    {
        Console.WriteLine(multiplyBySeven(5));
        Console.WriteLine(multiplyByTwelve(5));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program of multiply operator
// Returns n * 7

function multiplyBySeven($n)
{
    return ($n << 3) - $n;
}

// Returns n * 12
function multiplyByTwelve($n)
{
    return ($n << 3) + ($n << 2);
}

// Driver Code
echo multiplyBySeven(5), "\n";
echo multiplyByTwelve(5), "\n";

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>
// Python3 program to Multiplying a
// variable with a constant

// Returns n * 7
function multiplyBySeven(n)
{
    // OR (n << 2) + (n << 1) + n
    return (n << 3) - n;
}

// Returns n * 12
function multiplyByTwelve(n)
{
    return (n << 3) + (n << 2);
}

// Driver code
document.write(multiplyBySeven(5) + "<br>");
document.write(multiplyByTwelve(5) + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
35
60
```

时间复杂度:0(1)

辅助空间:0(1)

我们只需要找到 2 的幂的组合。此外，当我们有一个非常大的数据集，并且每个数据集都需要与相同的常数相乘时，这非常方便，因为按位运算符比数学运算符更快。
本文由 **kp93** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。