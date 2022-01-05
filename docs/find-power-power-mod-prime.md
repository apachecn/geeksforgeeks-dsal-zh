# 求素数模下的幂的幂

> 原文:[https://www.geeksforgeeks.org/find-power-power-mod-prime/](https://www.geeksforgeeks.org/find-power-power-mod-prime/)

给定四个数字 A，B，C 和 M，其中 M 是质数。我们的任务是找到 A <sup>BC</sup> (mod M)。
**例:**

```
Input  : A = 2, B = 4, C = 3, M = 23
Output : 6
43 = 64 so,
2^64(mod 23) = 6 
```

A **天真法**是先计算 res = B <sup>C</sup> ，然后用模指数计算 A <sup>res</sup> % M。这种方法的问题是，我们不能直接在 B <sup>C</sup> 上应用 mod M，所以我们必须在没有 mod M 的情况下计算这个值。但是如果我们直接求解它，那么我们会得出 A 的指数的大值，这肯定会在最终答案中溢出。
一种**有效的方法**是利用[费马小定理](https://en.wikipedia.org/wiki/Fermat's_little_theorem)将 B <sup>C</sup> 缩小到一个较小的值，然后应用模指数。

```
According the Fermat's little
a(M - 1) = 1 (mod M) if M is a prime.

So if we rewrite BC as x*(M-1) + y, then the
task of computing ABC becomes Ax*(M-1) + y
which can be written as Ax*(M-1)*Ay.
From Fermat's little theorem, we know Ax*(M-1) = 1.
So task of computing ABC reduces to computing Ay

What is the value of y?
From BC = x * (M - 1) + y,
y can be written as BC % (M-1)

We can easily use the above theorem such that we can get
A ^ (B ^ C) % M = (A ^ y ) %  M

Now we only need to find two things as:-
1\. y = (B ^ C) % (M - 1)
2\. Ans = (A ^ y) % M
```

## C++

```
// C++ program to find (a^b) mod m for a large 'a'
#include<bits/stdc++.h>
using namespace std;

// Iterative Function to calculate (x^y)%p in O(log y)
unsigned int power(unsigned int x, unsigned int y,
                                   unsigned int p)
{
    unsigned int res = 1;      // Initialize result

    x = x % p;  // Update x if it is more than or
                // equal to p

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res*x) % p;

        // y must be even now
        y = y>>1; // y = y/2
        x = (x*x) % p;
    }
    return res;
}

unsigned int Calculate(unsigned int A, unsigned int B,
                       unsigned int C, unsigned int M)
{
    unsigned int res, ans;

    // Calculate B ^ C (mod M - 1)
    res = power(B, C, M-1);

    // Calculate A ^ res ( mod M )
    ans = power(A, res, M);

    return ans;
}

// Driver program to run the case
int main()
{   // M must be be a Prime Number
    unsigned int A = 3, B = 9, C = 4, M = 19;

    cout << Calculate(A, B, C, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find (a^b)
// mod m for a large 'a'
import java.util.*;

class GFG {

// Iterative Function to
// calculate (x^y)%p in O(log y)
static int power(int x, int y, int p) {

    // Initialize result
    int res = 1;

    // Update x if it is more
    // than or equal to p
    x = x % p;

    while (y > 0) {

    // If y is odd, multiply x with result
    if (y % 2 != 0)
        res = (res * x) % p;

    // y must be even now
    y = y >> 1; // y = y/2
    x = (x * x) % p;
    }
    return res;
}

static int Calculate(int A, int B, int C, int M) {
    int res, ans;

    // Calculate B ^ C (mod M - 1)
    res = power(B, C, M - 1);

    // Calculate A ^ res ( mod M )
    ans = power(A, res, M);

    return ans;
}

// Driver code
public static void main(String[] args) {

    // M must be be a Prime Number
    int A = 3, B = 9, C = 4, M = 19;

    System.out.print(Calculate(A, B, C, M));
}
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to calculate the ans
def calculate(A, B, C, M):

    # Calculate B ^ C (mod M - 1)
    res = pow(B, C, M-1)

    # Calculate A ^ res ( mod M )
    ans = pow(A, res, M)

    return ans

# Driver program to run the case
A = 3
B = 9
C = 4

# M must be Prime Number
M = 19
print( calculate(A, B, C, M) )
```

## C#

```
// C# program to find (a^b) mod m for
// a large 'a'
using System;

class GFG {

    // Iterative Function to calculate
    // (x^y)%p in O(log y)
    static int power(int x, int y, int p)
    {

        // Initialize result
        int res = 1;

        // Update x if it is more
        // than or equal to p
        x = x % p;

        while (y > 0) {

            // If y is odd, multiply x
            // with result
            if (y % 2 != 0)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    static int Calculate(int A, int B,
                          int C, int M)
    {
        int res, ans;

        // Calculate B ^ C (mod M - 1)
        res = power(B, C, M - 1);

        // Calculate A ^ res ( mod M )
        ans = power(A, res, M);

        return ans;
    }

    // Driver code
    public static void Main()
    {

        // M must be be a Prime Number
        int A = 3, B = 9, C = 4, M = 19;

        Console.Write(Calculate(A, B, C, M));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// (a^b) mod m for a
// large 'a'

// Iterative Function
// to calculate (x^y)%p
// in O(log y)
function power($x, $y, $p)
{
    $res = 1; // Initialize result

    $x = $x % $p; // Update x if it
                  // is more than or
                  // equal to p

    while ($y > 0)
    {
        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }
    return $res;
}

function Calculate($A, $B, $C, $M)
{
    $res; $ans;

    // Calculate B ^ C
    // (mod M - 1)
    $res = power($B, $C, $M - 1);

    // Calculate A ^
    // res ( mod M )
    $ans = power($A, $res, $M);

    return $ans;
}

// Driver Code

// M must be be
// a Prime Number
$A = 3; $B = 9;
$C = 4; $M = 19;

echo Calculate($A, $B, 
               $C, $M);

// This code is contributed
// by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find (a^b)
// mod m for a large 'a'

// Iterative Function to 
// calculate (x^y)%p in O(log y)
function power(x, y, p) {

    // Initialize result
    let res = 1; 

    // Update x if it is more
    // than or equal to p
    x = x % p; 

    while (y > 0) {

    // If y is odd, multiply x with result
    if (y % 2 != 0)
        res = (res * x) % p;

    // y must be even now
    y = y >> 1; // y = y/2
    x = (x * x) % p;
    }
    return res;
}

function Calculate(A, B, C, M) {
    let res, ans;

    // Calculate B ^ C (mod M - 1)
    res = power(B, C, M - 1);

    // Calculate A ^ res ( mod M )
    ans = power(A, res, M);

    return ans;
}

// Driver Code

    // M must be be a Prime Number
    let A = 3, B = 9, C = 4, M = 19;

    document.write(Calculate(A, B, C, M));

</script>
```

**输出:**

```
18
```

**时间复杂度:** O(log(B) + log(C))
**辅助空间:** O(1)
本文由 [Shubham Bansal](https://www.facebook.com/banalshubham) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。