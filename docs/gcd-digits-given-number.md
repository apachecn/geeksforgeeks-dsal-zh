# 给定数字的位数的 GCD

> 原文:[https://www.geeksforgeeks.org/gcd-digits-given-number/](https://www.geeksforgeeks.org/gcd-digits-given-number/)

给定一个数字 n，求其位数的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 。

**示例:**

```
Input  : 345
Output : 1
GCD of 3, 4 and 5 is 1.

Input  : 2448
Output : 2
GCD of 2, 4, 4 and 8 is 2
```

我们使用下面的循环逐个遍历数字

```
digit = n mod 10;
n  = n / 10; 
```

在遍历数字时，我们跟踪当前的 GCD，并通过用当前的 GCD 查找当前数字的 GCD 来更新 GCD。

## C++

```
// CPP program to find GCD of digits of a number
#include<iostream>
#include<algorithm>
using namespace std;

int digitGCD(int n)
{
    int gcd = 0;
    while (n > 0)
    {       
        gcd = __gcd(n%10, gcd);

        // If at point GCD becomes 1,
        // return it
        if (gcd == 1)
           return 1;

        n = n/10;
    }
    return gcd;
}

// driver code
int main()
{
    long n = 2448;
    cout << digitGCD(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find GCD of digits of a number

class GFG
{
    // Recursive function to return gcd of a and b
    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);

    }
    static int digitGCD(int n)
    {
        int gcd = 0;
        while (n > 0)
        {    
            gcd = __gcd(n % 10, gcd);

            // If at point GCD becomes 1,
            // return it
            if (gcd == 1)
            return 1;

            n = n / 10;
        }
        return gcd;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 2448;
        System.out.print(digitGCD(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to find
# GCD of digits of a number

# Recursive function to return gcd of a and b
def __gcd(a,b):
    return a if(b==0) else __gcd(b, a % b)

def digitGCD(n):

    gcd = 0
    while (n > 0):

        gcd = __gcd(n % 10, gcd)

        # If at point GCD becomes 1,
        # return it
        if (gcd == 1):
           return 1

        n = n // 10

    return gcd

#Driver code
n = 2448
print(digitGCD(n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find GCD of
// digits of a number
using System;

class GFG {

    // Recursive function to return
    // gcd of a and b
    static int __gcd(int a, int b)
    {
        return b == 0 ? a : __gcd(b, a % b);

    }

    static int digitGCD(int n)
    {
        int gcd = 0;
        while (n > 0)
        {    
            gcd = __gcd(n % 10, gcd);

            // If at point GCD becomes 1,
            // return it
            if (gcd == 1)
            return 1;

            n = n / 10;
        }
        return gcd;
    }

    // Driver code
    public static void Main ()
    {
        int n = 2448;
        Console.Write(digitGCD(n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find GCD
// of digits of a number

// Recursive function to
// return gcd of a and b
function __gcd($a,$b)
{
    return $b == 0 ? $a :
      __gcd($b, $a % $b);

}

function digitGCD($n)
{
    $gcd = 0;
    while ($n > 0)
    {    
        $gcd = __gcd($n % 10, $gcd);

        // If at point GCD
        // becomes 1, return it
        if ($gcd == 1)
        return 1;

        $n = $n / 10;
    }
    return $gcd;
}

// Driver code
$n = 2448;
echo digitGCD($n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
// javascript program to find GCD of digits of a number   
// Recursive function to return gcd of a and b
    function __gcd(a, b)
    {
        return b == 0 ? a : __gcd(b, a % b);

    }

    function digitGCD(n)
    {
        var gcd = 0;
        while (n > 0)
        {
            gcd = __gcd(n % 10, gcd);

            // If at point GCD becomes 1,
            // return it
            if (gcd == 1)
                return 1;

            n = parseInt(n / 10);
        }
        return gcd;
    }

    // Driver code
    var n = 2448;
    document.write(digitGCD(n));

// This code is contributed by aashish1995
</script>
```

**输出:**

```
2
```

本文由 [**迪本杜·罗伊·乔杜里**](https://auth.geeksforgeeks.org/profile.php?user=Dibyendu Roy Chaudhuri&list=practice) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。