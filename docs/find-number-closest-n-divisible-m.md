# 求最接近 n 且能被 m 整除的数

> 原文:[https://www . geesforgeks . org/find-number-close-n-除尽-m/](https://www.geeksforgeeks.org/find-number-closest-n-divisible-m/)

给定两个整数 **n** 和 **m** 。问题是找到最接近 **n** 且能被 **m** 整除的数。如果有一个以上这样的数字，那么输出具有最大绝对值的那个。如果 **n** 完全被 **m** 整除，则只输出 **n** 。要求 O(1)的时间复杂度。
**约束:** m！= 0
**示例:**

```
Input : n = 13, m = 4
Output : 12

Input : n = -15, m = 6
Output : -18
Both -12 and -18 are closest to -15, but
-18 has the maximum absolute value.
```

**来源:** [微软面试心得|第 125 集](https://www.geeksforgeeks.org/microsoft-interview-experience-set-125-campus-idc/)。

我们找到 n/m 的值，让这个值为 q，然后我们找到两种可能性中最接近的一种。一个是 q * m，另一个是(m * (q + 1))或(m *(q–1))，这取决于给定的两个数字中是否有一个是负数。
**算法:**

```
closestNumber(n, m)
    Declare q, n1, n2
    q = n / m
    n1 = m * q

    if (n * m) > 0
        n2 = m * (q + 1)
    else
        n2 = m * (q - 1)

    if abs(n-n1) < abs(n-n2)
        return n1
    return n2  
```

## C++

```
// C++ implementation to find the number closest to n
// and divisible by m
#include <bits/stdc++.h>

using namespace std;

// function to find the number closest to n
// and divisible by m
int closestNumber(int n, int m)
{
    // find the quotient
    int q = n / m;

    // 1st possible closest number
    int n1 = m * q;

    // 2nd possible closest number
    int n2 = (n * m) > 0 ? (m * (q + 1)) : (m * (q - 1));

    // if true, then n1 is the required closest number
    if (abs(n - n1) < abs(n - n2))
        return n1;

    // else n2 is the required closest number   
    return n2;   
}

// Driver program to test above
int main()
{
    int n = 13, m = 4;
    cout << closestNumber(n, m) << endl;

    n = -15; m = 6;
    cout << closestNumber(n, m) << endl;

    n = 0; m = 8;
    cout << closestNumber(n, m) << endl;

    n = 18; m = -7;
    cout << closestNumber(n, m) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the number closest to n
// and divisible by m
public class close_to_n_divisible_m {

    // function to find the number closest to n
    // and divisible by m
    static int closestNumber(int n, int m)
    {
        // find the quotient
        int q = n / m;

        // 1st possible closest number
        int n1 = m * q;

        // 2nd possible closest number
        int n2 = (n * m) > 0 ? (m * (q + 1)) : (m * (q - 1));

        // if true, then n1 is the required closest number
        if (Math.abs(n - n1) < Math.abs(n - n2))
            return n1;

        // else n2 is the required closest number   
        return n2;   
    }

    // Driver program to test above
    public static void main(String args[])
    {
        int n = 13, m = 4;
        System.out.println(closestNumber(n, m));

        n = -15; m = 6;
        System.out.println(closestNumber(n, m));

        n = 0; m = 8;
        System.out.println(closestNumber(n, m));

        n = 18; m = -7;
        System.out.println(closestNumber(n, m));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 implementation to find
# the number closest to n

# Function to find the number closest
# to n and divisible by m
def closestNumber(n, m) :
    # Find the quotient
    q = int(n / m)

    # 1st possible closest number
    n1 = m * q

    # 2nd possible closest number
    if((n * m) > 0) :
        n2 = (m * (q + 1))
    else :
        n2 = (m * (q - 1))

    # if true, then n1 is the required closest number
    if (abs(n - n1) < abs(n - n2)) :
        return n1

    # else n2 is the required closest number
    return n2

# Driver program to test above
n = 13; m = 4
print(closestNumber(n, m))

n = -15; m = 6
print(closestNumber(n, m))

n = 0; m = 8
print(closestNumber(n, m))

n = 18; m = -7
print(closestNumber(n, m))

# This code is contributed by Nikita tiwari.
```

## C#

```
// C# implementation to find the
// number closest to n and divisible by m
using System;

class GFG {

    // function to find the number closest to n
    // and divisible by m
    static int closestNumber(int n, int m)
    {
        // find the quotient
        int q = n / m;

        // 1st possible closest number
        int n1 = m * q;

        // 2nd possible closest number
        int n2 = (n * m) > 0 ? (m * (q + 1)) : (m * (q - 1));

        // if true, then n1 is the required closest number
        if (Math.Abs(n - n1) < Math.Abs(n - n2))
            return n1;

        // else n2 is the required closest number
        return n2;
    }

    // Driver program to test above
    public static void Main()
    {
        int n = 13, m = 4;
        Console.WriteLine(closestNumber(n, m));

        n = -15;
        m = 6;
        Console.WriteLine(closestNumber(n, m));

        n = 0;
        m = 8;
        Console.WriteLine(closestNumber(n, m));

        n = 18;
        m = -7;
        Console.WriteLine(closestNumber(n, m));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// the number closest to n and
// divisible by m

// function to find the number
// closest to n and divisible by m
function closestNumber($n, $m)
{
    // find the quotient
    $q = (int) ($n / $m);

    // 1st possible closest number
    $n1 = $m * $q;

    // 2nd possible closest number
    $n2 = ($n * $m) > 0 ?
        ($m * ($q + 1)) : ($m * ($q - 1));

    // if true, then n1 is the
    // required closest number
    if (abs($n - $n1) < abs($n - $n2))
        return $n1;

    // else n2 is the required
    // closest number
    return $n2;
}

// Driver Code
$n = 13;
$m = 4;
echo closestNumber($n, $m), "\n";

$n = -15;
$m = 6;
echo closestNumber($n, $m), "\n";

$n = 0;
$m = 8;
    echo closestNumber($n, $m), "\n";

$n = 18;
$m = -7;
    echo closestNumber($n, $m), "\n";

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>
// Javascript implementation to find
// the number closest to n and
// divisible by m

// function to find the number
// closest to n and divisible by m
function closestNumber(n, m)
{

    // find the quotient
    let q = parseInt(n / m);

    // 1st possible closest number
    let n1 = m * q;

    // 2nd possible closest number
    let n2 = (n * m) > 0 ?
        (m * (q + 1)) : (m * (q - 1));

    // if true, then n1 is the
    // required closest number
    if (Math.abs(n - n1) < Math.abs(n - n2))
        return n1;

    // else n2 is the required
    // closest number
    return n2;
}

// Driver Code
let n = 13;
let m = 4;
document.write(closestNumber(n, m) + "<br>");

n = -15;
m = 6;
document.write(closestNumber(n, m) + "<br>");

n = 0;
m = 8;
document.write(closestNumber(n, m) + "<br>");

n = 18;
m = -7;
document.write(closestNumber(n, m) + "<br>");

// This code is contributed by gfgking
</script>
```

**输出:**

```
12
-18
0
21
```

**时间复杂度:** O(1)
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。