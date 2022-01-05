# 不使用乘法运算符

将数字乘以 10

> 原文:[https://www . geesforgeks . org/乘法-number-10-不使用乘法运算符/](https://www.geeksforgeeks.org/multiply-number-10-without-using-multiplication-operator/)

给定一个数，任务是在不使用乘法运算符的情况下将其乘以 10？
示例:

```
Input : n = 50
Output: 500
// multiplication of 50 with 10 is = 500

Input : n = 16
Output: 160
// multiplication of 16 with 10 is = 160
```

这个问题的一个**简单解决方法**是运行一个循环，将 n 与自身相加 10 次。这里我们需要执行 10 个操作。
一**更好的解决办法**就是用钻头操纵。我们必须将 n 乘以 10，即:n*10，我们可以将其写成 **n*(2+8) = n*2 + n*8** 并且由于不允许使用乘法运算符，因此我们可以使用左移位按位运算符来实现。所以 n*10 = n < < 1 + n < < 3。

## C++

```
// C++ program to multiply a number with 10 using
// bitwise operators
#include<bits/stdc++.h>
using namespace std;

// Function to find multiplication of n with
// 10 without using multiplication operator
int multiplyTen(int n)
{
    return (n<<1) + (n<<3);
}

// Driver program to run the case
int main()
{
    int n = 50;
    cout << multiplyTen(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code to Multiply a number with 10
// without using multiplication operator
import java.util.*;

class GFG {

    // Function to find multiplication of n
    // with 10 without using multiplication
    // operator
    public static int multiplyTen(int n)
    {
        return (n << 1) + (n << 3);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int n = 50;
        System.out.println(multiplyTen(n));

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python 3 program to multiply a
# number with 10 using bitwise
# operators

# Function to find multiplication
# of n with 10 without using
# multiplication operator
def multiplyTen(n):

    return (n << 1) + (n << 3)

# Driver program to run the case
n = 50
print (multiplyTen(n))

# This code is contributed by
# Smitha
```

## C#

```
// C# Code to Multiply a number with 10
// without using multiplication operator
using System;

class GFG {

    // Function to find multiplication of n
    // with 10 without using multiplication
    // operator
    public static int multiplyTen(int n)
    {
        return (n << 1) + (n << 3);
    }

    // Driver Code
    public static void Main()
    {
        int n = 50;
        Console.Write(multiplyTen(n));

    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to multiply a
// number with 10 using
// bitwise operators

// Function to find multiplication
// of n with 10 without using
// multiplication operator
function multiplyTen($n)
{
    return ($n << 1) + ($n << 3);
}

    // Driver Code
    $n = 50;
    echo multiplyTen($n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
// JavaScript program to multiply a number with 10 using
// bitwise operators

// Function to find multiplication of n with
// 10 without using multiplication operator
function multiplyTen(n)
{
    return (n<<1) + (n<<3);
}

// Driver program to run the case

    let n = 50;
    document.write(multiplyTen(n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
500
```

时间复杂度:0(1)

辅助空间:0(1)

本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。