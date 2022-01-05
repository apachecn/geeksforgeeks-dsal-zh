# 佩兰数之和

> 原文:[https://www.geeksforgeeks.org/sum-perrin-numbers/](https://www.geeksforgeeks.org/sum-perrin-numbers/)

给定一个正数 n，求 P0 + P1 + P2 +的值。+ Pn，其中 pi 表示 I 是 Perrin 数。前几个佩兰数字是 3，0，2，3，2，5，5，7……。
示例:

```
Input  : 4 
Output : 8
Explanation : 3 + 0 + 2 + 3

Input  : 6
Output : 15
Explanation : 3 + 0 + 2 + 3 + 2 + 5
```

在之前的帖子中，我们已经介绍了[佩兰号码](https://www.geeksforgeeks.org/program-perrin-numbers/)。在数学术语中，佩兰数的序列 p(n)由递归关系
定义

```
 P(n) = P(n-2) + P(n-3) for n > 2, 

with initial values
    P(0) = 3, P(1) = 0, P(2) = 2\. 
```

**方法 1(使用第 n 个佩兰数的递归公式)**
我们可以简单地使用上述第 n 个佩兰数的递归公式来添加数字。

## C++

```
// C++ program to calculate sum of Perrin Numbers
#include <bits/stdc++.h>
using namespace std;

// function for sum of first n Perrin number.
int calSum(int n)
{
    int a = 3, b = 0, c = 2;
    if (n == 0) // n=0
        return 3;
    if (n == 1) // n=1
        return 3;
    if (n == 2) // n=2
        return 5;

    // calculate k=5 sum of three previous step.
    int sum = 5;

    // Sum remaining numbers
    while (n > 2) {
        int d = a + b; // calculate next term
        sum += d;
        a = b;
        b = c;
        c = d;
        n--;
    }

    return sum;
}

// Driver code
int main()
{
    int n = 9;
    cout << calSum(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate
// sum of Perrin Numbers
import java.lang.*;

class GFG {

    // function for sum of first n Perrin number.
    static int calSum(int n)
    {

        int a = 3, b = 0, c = 2;
        if (n == 0) // n=0
            return 3;
        if (n == 1) // n=1
            return 3;
        if (n == 2) // n=2
            return 5;

        // calculate k=5 sum of three previous step.
        int sum = 5;

        // Sum remaining numbers
        while (n > 2) {

            // calculate next term
            int d = a + b;
            sum += d;
            a = b;
            b = c;
            c = d;
            n--;
        }

        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 9;
        System.out.print(calSum(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to calculate
# sum of Perrin Numbers

# function for sum of first
# n Perrin number.
def calSum(n):

    a = 3
    b = 0
    c = 2

    if (n == 0):  # n = 0
        return 3
    if (n == 1):  # n = 1
        return 3
    if (n == 2):  # n = 2
        return 5

    # calculate k = 5 sum of
    # three previous step.
    sum = 5

    # Sum remaining numbers
    while (n > 2):

        # calculate next term
        d = a + b
        sum = sum + d
        a = b
        b = c
        c = d
        n = n-1

    return sum

# Driver code

n = 9
print(calSum(n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to calculate
// sum of Perrin Numbers
using System;

class GFG {

    // function for sum of first n Perrin number.
    static int calSum(int n)
    {

        int a = 3, b = 0, c = 2;

        if (n == 0) // n=0
            return 3;
        if (n == 1) // n=1
            return 3;
        if (n == 2) // n=2
            return 5;

        // calculate k=5 sum of three
        // previous step.
        int sum = 5;

        // Sum remaining numbers
        while (n > 2) {

            // calculate next term
            int d = a + b;
            sum += d;
            a = b;
            b = c;
            c = d;
            n--;
        }

        return sum;
    }

    // Driver code
    public static void Main()
    {

        int n = 9;

        Console.WriteLine(calSum(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate
// sum of Perrin Numbers

// function for sum of
// first n Perrin number.
function calSum($n)
{

    $a = 3;
    $b = 0;
    $c = 2;
    if ($n == 0) // n=0
        return 3;
    if ($n == 1) // n=1
        return 3;
    if ($n == 2) // n=2
        return 5;

    // calculate k=5 sum of
    // three previous step.
    $sum = 5;

    // Sum remaining numbers
    while ($n > 2)
    {

        // calculate next term
        $d = $a + $b;

        $sum += $d;
        $a = $b;
        $b = $c;
        $c = $d;
        $n--;
    }

    return $sum;
}

    // Driver code
    $n = 9;
    echo calSum($n);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to calculate
// sum of Perrin Numbers

    // function for sum of first n Perrin number.
    function calSum(n)
    {

        let a = 3, b = 0, c = 2;
        if (n == 0) // n=0
            return 3;
        if (n == 1) // n=1
            return 3;
        if (n == 2) // n=2
            return 5;

        // calculate k=5 sum of three previous step.
        let sum = 5;

        // Sum remaining numbers
        while (n > 2) {

            // calculate next term
            let d = a + b;
            sum += d;
            a = b;
            b = c;
            c = d;
            n--;
        }

        return sum;
    }

// Driver code   

           let n = 9;
        document.write(calSum(n));

</script>
```

**输出:**

```
49
```

**方法二(使用直接公式)**
思路是找出佩兰数之和与第 n 个佩兰数的关系。

```
p(i) refers to the i’th perrin number.
S(i) refers to sum of perrin numbers till p(i),

We can rewrite the relation P(n) = P(n-2) + P(n-3) 
as below :
P(n-3)    = P(n)  -  P(n-2)

Similarly,
P(n-4)    = P(n-1)  -  P(n-3)
P(n-5)    = P(n-2)  -  P(n-4)
.          .           .
.          .             .
.          .             .
P(1)      = P(4)    -  P(2)
P(0)      = P(3)    -  P(1)
-------------------------------
Adding all the equations, on left side, we have
{(n) + P(n-1) - P(1) - P(2) which is S(n-3).
Therefore,
S(n-3) = P(n) + P(n-1) - P(1) - P(2)
S(n-3) = P(n) + P(n-1) - 2
S(n)   = P(n+3) + P(n+2) - 2
```

为了求 S(n)，我们可以简单地计算第(n+3)个和第(n+2)个 Perrin 数，然后从结果中减去 2。
本文由**丹麦语 _RAZA** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。