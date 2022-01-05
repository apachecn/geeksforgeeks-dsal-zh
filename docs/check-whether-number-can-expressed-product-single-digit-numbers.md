# 检查一个数字是否可以表示为一位数的乘积

> 原文:[https://www . geesforgeks . org/check-number-can-expressed-product-个位数-numbers/](https://www.geeksforgeeks.org/check-whether-number-can-expressed-product-single-digit-numbers/)

给定一个非负数 **n** 。问题是检查给定的数字 **n** 是否可以表示为一位数的乘积。
示例:

```
Input : n = 24
Output : Yes
Different combinations are:
(8*3) and (6*4)

Input : 68
Output : No
To represent 68 as product of 
number, 17 must be included which
is a two digit number.
```

**进场:**我们要检查号码 **n** 除了 **2、3、5、7** 外是否没有质因数。为此，我们反复将数字 **n** 除以(2，3，5，7)，直到不能再被这些数字除为止。经过这个过程如果 **n** == 1，那么可以表示为一位数的乘积，否则如果大于 1，那么就不能表示。

## C++

```
// C++ implementation to check whether a number can be
// expressed as a product of single digit numbers
#include <bits/stdc++.h>
using namespace std;

// Number of single digit prime numbers
#define SIZE 4

// function to check whether a number can be
// expressed as a product of single digit numbers
bool productOfSingelDgt(int n)
{
    // if 'n' is a single digit number, then
    // it can be expressed
    if (n >= 0 && n <= 9)
        return true;

    // define single digit prime numbers array
    int prime[] = { 2, 3, 5, 7 };

    // repeatedly divide 'n' by the given prime
    // numbers until all the numbers are used
    // or 'n' > 1
    for (int i = 0; i < SIZE && n > 1; i++)
        while (n % prime[i] == 0)
            n = n / prime[i];

    // if true, then 'n' can
    // be expressed
    return (n == 1);
}

// Driver program to test above
int main()
{
    int n = 24;
    productOfSingelDgt(n)? cout << "Yes" :
                           cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether
// a number can be expressed as a
// product of single digit numbers
import java.util.*;

class GFG
{

// Number of single digit prime numbers
static int SIZE = 4;

// function to check whether a number can
// be expressed as a product of single
// digit numbers
static boolean productOfSingelDgt(int n)
{
    // if 'n' is a single digit number,
    // then it can be expressed
    if (n >= 0 && n <= 9)
        return true;

    // define single digit prime numbers
    // array
    int[] prime = { 2, 3, 5, 7 };

    // repeatedly divide 'n' by the given
    // prime numbers until all the numbers
    // are used or 'n' > 1
    for (int i = 0; i < SIZE && n > 1; i++)
        while (n % prime[i] == 0)
            n = n / prime[i];

    // if true, then 'n' can
    // be expressed
    return (n == 1);
}

// Driver program to test above
public static void main (String[] args)
{
    int n = 24;
    if(productOfSingelDgt(n))
    System.out.println("Yes");
    else
    System.out.println("No");
}

}
/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python3 program to check
# whether a number can be
# expressed as a product of
# single digit numbers

# Number of single digit
# prime numbers
SIZE = 4

# function to check whether
# a number can be
# expressed as a product
# of single digit numbers
def productOfSingelDgt(n):

    # if 'n' is a single digit
        # number, then
    # it can be expressed
    if n >= 0 and n <= 9:
        return True

    # define single digit prime
        # numbers array
    prime = [ 2, 3, 5, 7 ]

    # repeatedly divide 'n' by
        # the given prime
    # numbers until all the
        # numbers are used
    # or 'n' > 1
    i = 0
    while i < SIZE and n > 1:
        while n % prime[i] == 0:
            n = n / prime[i]
        i += 1

    # if true, then 'n' can
    # be expressed
    return n == 1

n = 24
if productOfSingelDgt(n):
    print ("Yes")
else :
    print ("No")

# This code is contributed
# by Shreyanshi Arun.
```

## C#

```
// C# implementation to check whether
// a number can be expressed as a
// product of single digit numbers
using System;

class GFG {

    // Number of single digit prime numbers
    static int SIZE = 4;

    // function to check whether a number can
    // be expressed as a product of single
    // digit numbers
    static bool productOfSingelDgt(int n)
    {
        // if 'n' is a single digit number,
        // then it can be expressed
        if (n >= 0 && n <= 9)
            return true;

        // define single digit prime numbers
        // array
        int[] prime = { 2, 3, 5, 7 };

        // repeatedly divide 'n' by the given
        // prime numbers until all the numbers
        // are used or 'n' > 1
        for (int i = 0; i < SIZE && n > 1; i++)
            while (n % prime[i] == 0)
                n = n / prime[i];

        // if true, then 'n' can
        // be expressed
        return (n == 1);
    }

    // Driver program to test above
    public static void Main()
    {
        int n = 24;
        if (productOfSingelDgt(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }

}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check
// whether a number can be
// expressed as a product of
// single digit numbers

// function to check whether
// a number can be expressed
//as a product of single
// digit numbers
function productOfSingelDgt($n,$SIZE)
{

    // if 'n' is a single
    // digit number, then
    // it can be expressed
    if ($n >= 0 && $n <= 9)
        return true;

    // define single digit
    // prime numbers array
    $prime = array(2, 3, 5, 7);

    // repeatedly divide 'n'
    // by the given prime
    // numbers until all
    // the numbers are used
    // or 'n' > 1
    for ($i = 0; $i < $SIZE && $n > 1; $i++)
        while ($n % $prime[$i] == 0)
            $n = $n / $prime[$i];

    // if true, then 'n' can
    // be expressed
    return ($n == 1);
}

    // Driver Code
    $SIZE = 4;
    $n = 24;
    if(productOfSingelDgt($n, $SIZE))
        echo "Yes" ;
    else
        echo "No";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
// javascript implementation to check whether
// a number can be expressed as a
// product of single digit numbers

    // Number of single digit prime numbers
    const SIZE = 4;

    // function to check whether a number can
    // be expressed as a product of single
    // digit numbers
    function productOfSingelDgt(n)
    {

        // if 'n' is a single digit number,
        // then it can be expressed
        if (n >= 0 && n <= 9)
            return true;

        // define single digit prime numbers
        // array
        var prime = [ 2, 3, 5, 7 ];

        // repeatedly divide 'n' by the given
        // prime numbers until all the numbers
        // are used or 'n' > 1
        for (i = 0; i < SIZE && n > 1; i++)
            while (n % prime[i] == 0)
                n = n / prime[i];

        // if true, then 'n' can
        // be expressed
        return (n == 1);
    }

    // Driver program to test above
        var n = 24;
        if (productOfSingelDgt(n))
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by gauravrajput1
</script>
```

输出:

```
Yes
```

时间复杂度:O(num)，其中 **num** 是 **n** 的素因子(2，3，5，7)的个数。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。