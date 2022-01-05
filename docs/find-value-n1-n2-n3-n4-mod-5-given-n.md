# 为给定的 n

找到(n^1 + n^2 + n^3 + n^4) mod 5 的值

> 原文:[https://www . geesforgeks . org/find-value-n1-N2-n3-n4-mod-5-given-n/](https://www.geeksforgeeks.org/find-value-n1-n2-n3-n4-mod-5-given-n/)

给你一个函数 f(n)=(n)<sup>1</sup>+n<sup>2</sup>+n<sup>3</sup>+n<sup>4</sup>，对于任意给定值正整数 n，你都要求 **f(n) mod 5** 的值，
注意:n 可能足够大，这样 f(n) > 10 <sup>18</sup> 。
**举例:**

```
Input : n = 4
Output : 0
Explanation : f(4) = 4 + 16 + 64 + 256 = 330, 
f(4) mod 5 = 330 mod 5 = 0.

Input : n = 1 
Output : 4
Explanation : f(1) = 1 + 1 + 1 + 1 = 4, 
f(1) mod 5 = 4.
```

首先为了解决这个问题，你可以借助任意幂函数和模运算符直接找到(n<sup>1</sup>+n<sup>2</sup>+n<sup>3</sup>+n<sup>4</sup>)mod 5 的值。
但是对于较大的 n 值，你的结果将是错误的，因为对于较大的 n 值，f(n)可能会超出 long long int 的范围，在这种情况下，你必须选择其他有效的方法。
为了解决这个问题，让我们对 f(n)做一些小的数学推导。

```
f(n) = (n1 + n2 + n3 + n4)
     = (n) (n+1) (n2+1)
Now, for finding f(n) mod 5 we must take care of unit digit of f(n) only,
also as f(n) mod 5 is dependent on n%5, (n+1)%5 & (n2+1)%5,
if any of these three result in zero then our whole result is 0.
So, if n = 5, 10, .. 5k then n mod 5 = 0 hence f(n) mod 5 = 0.
if n = 4, 9, .., (5k-1) then (n+1) mod 5 = 0 hence f(n) mod 5 = 0.
if n = 3, 8, 13..., (5k-2) f(n) mod 5 = (3 * 4 * 10) mod 5 = 0
if n = 2, 7, 12..., (5k-3) f(n) mod 5 = (2 * 3 * 5) mod 5 = 0.
if n = 1, 6, 11..., (5k-4) f(n) mod 5 = (1 * 2 * 2) mod 5 = 4.
```

经过上面的分析，我们可以看到，如果 n 的形式是 5k+1 或者说 5k-4，那么 f(n) mod 5 = 4，其他方面 f(n) = 0。
即如果(n%5 == 1)结果= 4，
否则结果= 0。

## C++

```
// finding the value of f(n) mod 5 for given n.
#include <bits/stdc++.h>
using namespace std;

// function for f(n) mod 5
int fnMod(int n)
{
    // if n % 5 == 1 return 4
    if (n % 5 == 1)
        return 4;

    // else return 0
    else
        return 0;
}

// driver program
int main()
{
    int n = 10;
    cout << fnMod(n) << endl;
    n = 11;
    cout << fnMod(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to finding the value
// of f(n) mod 5 for given n.
import java.io.*;

class GFG
{
    // function for f(n) mod 5
    static int fnMod(int n)
    {
        // if n % 5 == 1 return 4
        if (n % 5 == 1)
            return 4;

        // else return 0
        else
            return 0;
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 10;
        System.out.println(fnMod(n));
        n = 11;
        System.out.println(fnMod(n));

    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to find the value
# of f(n) mod 5 for given n.

# Function for f(n) mod 5
def fnMod(n):

    # if n % 5 == 1 return 4
    if (n % 5 == 1):
        return 4

    # else return 0
    else:
        return 0

# Driver Code
n = 10
print(fnMod(n))

n = 11
print(fnMod(n))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// Code for finding the value
// of f(n) mod 5 for given n.
using System;

class GFG {
    // function for f(n) mod 5
    static int fnMod(int n)
    {
        // if n % 5 == 1 return 4
        if (n % 5 == 1)
            return 4;

        // else return 0
        else
            return 0;
    }

    // Driver program
    public static void Main()
    {
        int n = 10;
        Console.WriteLine(fnMod(n));
        n = 11;
        Console.WriteLine(fnMod(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding the
// value of f(n) mod 5 for given n.

// function for f(n) mod 5
function fnMod($n)
{
    // if n % 5 == 1 return 4
    if ($n % 5 == 1)
        return 4;

    // else return 0
    else
        return 0;
}

// Driver Code
$n = 10;
echo fnMod($n),"\n";
$n = 11;
echo fnMod($n) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// JavaScript program to finding the value
// of f(n) mod 5 for given n.

// function for f(n) mod 5
    function fnMod(n)
    {

        // if n % 5 == 1 return 4
        if (n % 5 == 1)
            return 4;

        // else return 0
        else
            return 0;
    }

// Driver Code
        let n = 10;
        document.write(fnMod(n) + "<br/>");
        n = 11;
        document.write(fnMod(n) + "<br/>");

        // This code is contributed by chinmoy1997pal.      
</script>
```

**输出:**

```
0
4
```