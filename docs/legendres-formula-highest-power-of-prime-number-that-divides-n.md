# 勒让德公式(给定 p 和 n，求最大的 x，使得 p^x 除以 n！)

> 原文:[https://www . geeksforgeeks . org/legendres-formula-最高次质数除法-n/](https://www.geeksforgeeks.org/legendres-formula-highest-power-of-prime-number-that-divides-n/)

给定一个整数 n 和一个素数 p，求最大的 x，这样 p <sup>x</sup> (p 升到 x 的幂)除以 n！(析因)
**例:**

```
Input:  n = 7, p = 3
Output: x = 2
32 divides 7! and 2 is the largest such power of 3.

Input:  n = 10, p = 3
Output: x = 4
34 divides 10! and 4 is the largest such power of 3.
```

n！是{1，2，3，4，…n}的乘法。
**有多少个数字在{1，2，3，4，…..n}可以被 p 整除？**
在{1，2，3，4，…中，每第 p 个数可被 p 整除..n}。因此在 n！，有能被 p 整除的⌊n/p⌋数，所以我们知道 x 的值(p 的最大幂，除以 n！)至少是⌊n/p⌋.
**x 能比⌊n/p⌋大吗？**
是的，可能有可以被 p <sup>2</sup> 、p <sup>3</sup> 、…
**整除的数字{1、2、3、4、…..n}可被 p <sup>2</sup> ，p <sup>3</sup> 整除，…**
有⌊n/(p <sup>2</sup> )⌋数可被 p <sup>2</sup> 整除(每 p <sup>2</sup> 个数可整除)。同样，还有⌊n/(p <sup>3</sup> )⌋数可被 p <sup>3</sup> 整除等等。
**x 的最大可能值是多少？**
所以最大的可能力量是⌊n/p⌋+⌊n/(p<sup>2</sup>)⌋+⌊n/(p<sup>3</sup>)⌋+……
注意我们只加了⌊n/(p <sup>2</sup> )⌋只有一次(不是两次)因为一个 p 已经被表达式⌊n/p⌋.考虑了同样，我们考虑⌊n/(p <sup>3</sup> )⌋(不是三次)。
以下是上述思路的实现。

## C++

```
// C++ program to find largest x such that p*x divides n!
#include <iostream>
using namespace std;

// Returns largest power of p that divides n!
int largestPower(int n, int p)
{
    // Initialize result
    int x = 0;

    // Calculate x = n/p + n/(p^2) + n/(p^3) + ....
    while (n)
    {
        n /= p;
        x += n;
    }
    return x;
}

// Driver code
int main()
{
    int n = 10, p = 3;
    cout << "The largest power of "<< p <<
            " that divides " << n << "! is "<<
            largestPower(n, p) << endl;
    return 0;
}

// This code is contributed by shubhamsingh10
```

## C

```
// C program to find largest x such that p*x divides n!
#include <stdio.h>

// Returns largest power of p that divides n!
int largestPower(int n, int p)
{
    // Initialize result
    int x = 0;

    // Calculate x = n/p + n/(p^2) + n/(p^3) + ....
    while (n)
    {
        n /= p;
        x += n;
    }
    return x;
}

// Driver program
int main()
{
    int n = 10, p = 3;
    printf("The largest power of %d that divides %d! is %d\n",
           p, n, largestPower(n, p));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest x such that p*x divides n!
import java.io.*;

class GFG
{
    // Function that returns largest power of p
    // that divides n!
    static int Largestpower(int n, int p)
    {
        // Initialize result
        int ans = 0;

        // Calculate x = n/p + n/(p^2) + n/(p^3) + ....
        while (n > 0)
        {
            n /= p;
            ans += n;
        }
        return ans;
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 10;
        int p = 3;
        System.out.println(" The largest power of " + p + " that divides "
                + n + "! is " + Largestpower(n, p));

    }
}
```

## 蟒蛇 3

```
# Python3 program to find largest
# x such that p*x divides n!

# Returns largest power of p that divides n!
def largestPower(n, p):

    # Initialize result
    x = 0

    # Calculate x = n/p + n/(p^2) + n/(p^3) + ....
    while n:
        n /= p
        x += n
    return x

# Driver program
n = 10; p = 3
print ("The largest power of %d that divides %d! is %d\n"%
                                (p, n, largestPower(n, p)))

# This code is contributed by Shreyanshi Arun.
```

## C#

```
// C# program to find largest x
// such that p * x divides n!
using System;

public class GFG
{

    // Function that returns largest 
    // power of p that divides n!
    static int Largestpower(int n, int p)
    {
        // Initialize result
        int ans = 0;

        // Calculate x = n / p + n / (p ^ 2) +
        // n / (p ^ 3) + ....
        while (n > 0)
        {
            n /= p;
            ans += n;
        }
        return ans;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 10;
        int p = 3;
        Console.Write(" The largest power of " + p + " that divides "
                + n + "! is " + Largestpower(n, p));

    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find largest
// x such that p*x divides n!

// Returns largest power
// of p that divides n!
function largestPower($n, $p)
{
    // Initialize result
    $x = 0;

    // Calculate x = n/p +
    // n/(p^2) + n/(p^3) + ....
    while ($n)
    {
        $n = (int)$n / $p;
        $x += $n;
    }
    return floor($x);
}

// Driver Code
$n = 10;
$p = 3;
echo "The largest power of ", $p ;
echo " that divides ",$n , "! is ";
echo largestPower($n, $p);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Javascript program to find largest
// x such that p*x divides n!

// Returns largest power
// of p that divides n!
function largestPower(n, p)
{
    // Initialize result
    let x = 0;

    // Calculate x = n/p +
    // n/(p^2) + n/(p^3) + ....
    while (n)
    {
        n = parseInt(n / p);
        x += n;
    }
    return Math.floor(x);
}

// Driver Code
let n = 10;
let p = 3;
document.write("The largest power of " + p);
document.write(" that divides " + n + "! is ");
document.write(largestPower(n, p));

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
The largest power of 3 that divides 10! is 4
```

**时间复杂度:** O(log <sub>p</sub> n)

**辅助空间:**O(1)
T3】p 不是素数怎么办？
我们可以找到 p 的所有素因子，并计算每个素因子的结果。参见[n 中 k 的最大幂！(阶乘)其中 k 可能不是质数](https://www.geeksforgeeks.org/largest-power-k-n-factorial-k-may-not-prime/)了解详情。
**来源:**
[http://e-maxx.ru/algo/factorial_divisors](http://e-maxx.ru/algo/factorial_divisors)
本文由**安库尔**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。