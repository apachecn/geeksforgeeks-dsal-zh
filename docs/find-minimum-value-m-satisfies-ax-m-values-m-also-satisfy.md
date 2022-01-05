# 求满足 ax + by = m 的 m 的最小值，m 之后的所有值也满足

> 原文:[https://www . geesforgeks . org/find-最小值-m-满足-ax-m-values-m-还-满足/](https://www.geeksforgeeks.org/find-minimum-value-m-satisfies-ax-m-values-m-also-satisfy/)

给定两个正整数‘a’和‘b’，它们代表方程 ax + by = m 中的系数。找到满足方程中 x 和 y 的任何正整数值的 m 的最小值。在这个最小值之后，方程由 m 的所有(更大的)值满足。如果不存在这样的最小值，返回“-1”。
**例:**

```
Input: a = 4, b = 7
Output: 18
Explanation: 18 is the smallest value that can
             can be satisfied by equation 4x + 7y.         
             4*1 + 7*2 = 18

             And after 18 all values are satisifed 
             4*3 + 7*1 = 19
             4*5 + 7*0 = 20
             ... and so on.
```

这是 [Frobenius 硬币问题](https://www.geeksforgeeks.org/frobenius-coin-problem/)的一个变种。在 Frobenius 硬币问题中，我们需要找到不能用两个硬币表示的最大数字。面值为“a”和“b”的硬币的最大金额是 a * b–(a+b)。所以最小的数字，可以用两个硬币来表示，之后的所有数字都可以表示，a * b –( a+b)+1。
一个重要的情况是‘a’和‘b’的 GCD 不为 1。例如，如果‘a’= 4 和‘b’= 6，那么所有可以用两个硬币表示的值都是偶数(或者所有可以对等式进行分层的 m 的值都是偶数)。所以所有不是 2 的倍数的值都不能满足方程。在这种情况下，没有最小值，此后所有值都满足等式。
以下是上述思路的实现:

## C++

```
// C++ program to find the minimum value of m that satisfies
// ax + by = m and all values after m also satisfy
#include<bits/stdc++.h>
using namespace std;

int findMin(int a, int b)
{
    // If GCD is not 1, then there is no such value,
    // else value is obtained using "a*b-a-b+1'
    return (__gcd(a, b) == 1)? a*b-a-b+1 : -1;
}

// Driver code
int main()
{
    int a = 4, b = 7;
    cout << findMin(a, b) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// minimum value of m that
// satisfies ax + by = m
// and all values after m
// also satisfy
import java.io.*;

class GFG
{
// Recursive function to
// return gcd of a and b   
static int __gcd(int a, int b)
{

    // Everything divides 0
    if (a == 0 && b == 0)
    return 0;

    // base case
    if (a == b)
        return a;

    // a is greater$
    if (a > b)
        return __gcd(a - b, b);
    return __gcd(a, b - a);
}

static int findMin( int a, int b)
{

    // If GCD is not 1, then
    // there is no such value,
    // else value is obtained
    // using "a*b-a-b+1'
    return (__gcd(a, b) == 1)?
        a * b - a - b + 1 : -1;
}

// Driver code
public static void main (String[] args)
{
    int a = 4;
    int b = 7;
    System.out.println(findMin(a, b));
}
}

// This code is contributed
// by akt_mit
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# value of m that satisfies ax + by = m
# and all values after m also satisfy

# Recursive function to return
# gcd of a and b
def __gcd(a, b):

    # Everything divides 0
    if (a == 0 or b == 0):
        return 0;

    # base case
    if (a == b):
        return a;

    # a is greater
    if (a > b):
        return __gcd(a - b, b);
    return __gcd(a, b - a);

def findMin( a, b):

    # If GCD is not 1, then
    # there is no such value,
    # else value is obtained
    # using "a*b-a-b+1'
    if(__gcd(a, b) == 1):
        return (a * b - a - b + 1)
    else:
        return -1

# Driver code
a = 4;
b = 7;
print(findMin(a, b));

# This code is contributed by mits
```

## C#

```
// C# program to find the minimum
// value of m that satisfies 
// ax + by = m and all values
// after m also satisfy
class GFG
{
// Recursive function to
// return gcd of a and b
static int __gcd(int a, int b)
{

    // Everything divides 0
    if (a == 0 && b == 0)
    return 0;

    // base case
    if (a == b)
        return a;

    // a is greater$
    if (a > b)
        return __gcd(a - b, b);
    return __gcd(a, b - a);
}

static int findMin( int a, int b)
{

    // If GCD is not 1, then
    // there is no such value,
    // else value is obtained
    // using "a*b-a-b+1'
    return (__gcd(a, b) == 1)?
           a * b - a - b + 1 : -1;
}

// Driver code
public static void Main()
{
    int a = 4;
    int b = 7;
    System.Console.WriteLine(findMin(a, b));
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// minimum value of m that
// satisfies ax + by = m
// and all values after m
// also satisfy

// Recursive function to
// return gcd of a and b
function __gcd($a, $b)
{

    // Everything divides 0
    if ($a == 0 or $b == 0)
    return 0;

    // base case
    if ($a == $b)
        return $a;

    // a is greater$
    if ($a > $b)
        return __gcd($a - $b, $b);
    return __gcd($a, $b - $a);
}

function findMin( $a, $b)
{

    // If GCD is not 1, then
    // there is no such value,
    // else value is obtained
    // using "a*b-a-b+1'
    return (__gcd($a, $b) == 1)?
           $a * $b - $a - $b + 1 : -1;
}

    // Driver code
    $a = 4; $b = 7;
    echo findMin($a, $b) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

    // Javascript program
    // to find the minimum
    // value of m that satisfies 
    // ax + by = m and all values
    // after m also satisfy

    // Recursive function to
    // return gcd of a and b
    function __gcd(a, b)
    {

        // Everything divides 0
        if (a == 0 && b == 0)
            return 0;

        // base case
        if (a == b)
            return a;

        // a is greater$
        if (a > b)
            return __gcd(a - b, b);
        return __gcd(a, b - a);
    }

    function findMin(a, b)
    {

        // If GCD is not 1, then
        // there is no such value,
        // else value is obtained
        // using "a*b-a-b+1'
        return (__gcd(a, b) == 1)?
                a * b - a - b + 1 : -1;
    }

    let a = 4;
    let b = 7;
    document.write(findMin(a, b));

</script>
```

**输出:**

```
18
```

本文由**里沙布·贾恩**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。