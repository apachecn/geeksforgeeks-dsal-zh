# GCD 最大且和等于 n 的系列

> 原文:[https://www . geesforgeks . org/series-maximum-gcd-sum-equals-n/](https://www.geeksforgeeks.org/series-largest-gcd-sum-equals-n/)

给定一个整数 n，打印 m 个递增的数字，使得 m 个数字的总和等于 n，并且 m 个数字的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 在所有可能的系列中是最大的。如果没有系列，则打印“-1”。
**例:**

```
Input  : n = 24,
         m = 3  
Output : 4 8 12  
Explanation : (3, 6, 15) is also a series 
of m numbers which sums to N, but gcd = 3
(4, 8, 12) has gcd = 4 which is the maximum
possible.

Input  : n = 6 
         m = 4 
Output : -1 
Explanation: It is not possible as the 
least GCD sequence will be 1+2+3+4 which
is greater then n, hence print -1.
```

**逼近:**
最常见的观察是数列的 gcd 永远是 n 的除数，最大可能的 gcd(**说 b** )将是 n/sum，其中 sum 是 1+2+的和..m.
如果 b 结果是 0，那么 1+2+3 的和..+k 超过 n，这是无效的，因此输出“-1”。
遍历找出所有可能的除数，循环到 sqrt(n)。如果当前除数是 I，取级数最好的方法就是考虑 I，2*i，3*i，…(m-1)*i，它们的和是等于 *i * (m*(m-1))/2* 的 s。最后一个数将是 n-s。
除了 I 是除数，n/i 将是另一个除数，所以也要检查一下。
取可能除数的最大值(**表示 r** )，该值应小于或等于 **b** ，并将序列打印为 *r，2*r，… (m-1)*r，n-s。*
如果没有找到这样的除数，只需输出“-1”。

## C++

```
// CPP program to find the series with largest
// GCD and sum equals to n
#include <bits/stdc++.h>
using namespace std;

// function to generate and print the sequence
void print_sequence(int n, int k)
{
    // stores the maximum gcd that can be
    // possible of sequence.
    int b = n / (k * (k + 1) / 2);

    // if maximum gcd comes out to be
    // zero then not possible
    if (b == 0) {
        cout << -1 << endl;

    } else {

        // the smallest gcd possible is 1
        int r = 1;

        // traverse the array to find out
        // the max gcd possible
        for (int x = 1; x * x <= n; x++) {

            // checks if the number is
            // divisible or not
            if (n % x != 0)
                continue;

            // checks if x is smaller then
            // the max gcd possible and x
            // is greater then the resultant
            // gcd till now, then r=x
            if (x <= b && x > r)
                r = x;

            // checks if n/x is smaller than
            // the max gcd possible and n/x
            // is greater then the resultant
            // gcd till now, then r=x
            if (n / x <= b && n / x > r)
                r = n / x;
        }

        // traverses and prints d, 2d, 3d,
        // ..., (k-1)·d,
        for (int i = 1; i < k; i++)
            cout << r * i << " ";

        // computes the last element of
        // the sequence n-s.
        int res = n - (r * (k * (k - 1) / 2));

        // prints the last element
        cout << res << endl;
    }
}

// driver program to test the above function
int main()
{
    int n = 24;
    int k = 4;
    print_sequence(n, k);

    n = 24, k = 5;
    print_sequence(n, k);

    n = 6, k = 4;
    print_sequence(n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the series with
// largest GCD and sum equals to n
import java.io.*;

class GFG {

// function to generate and print the sequence
static void print_sequence(int n, int k)
{
    // stores the maximum gcd that can be
    // possible of sequence.
    int b = n / (k * (k + 1) / 2);

    // if maximum gcd comes out to be
    // zero then not possible
    if (b == 0) {
        System.out.println("-1");

    } else {

        // the smallest gcd possible is 1
        int r = 1;

        // traverse the array to find out
        // the max gcd possible
        for (int x = 1; x * x <= n; x++) {

            // checks if the number is
            // divisible or not
            if (n % x != 0)
                continue;

            // checks if x is smaller then
            // the max gcd possible and x
            // is greater then the resultant
            // gcd till now, then r=x
            if (x <= b && x > r)
                r = x;

            // checks if n/x is smaller than
            // the max gcd possible and n/x
            // is greater then the resultant
            // gcd till now, then r=x
            if (n / x <= b && n / x > r)
                r = n / x;
        }

        // traverses and prints d, 2d, 3d,..., (k-1)
        for (int i = 1; i < k; i++)
            System.out.print(r * i + " ");

        // computes the last element of
        // the sequence n-s.
        int res = n - (r * (k * (k - 1) / 2));

        // prints the last element
        System.out.println(res);
    }
}

// driver program to test the above function
public static void main(String[] args)
{
    int n = 24;
    int k = 4;
    print_sequence(n, k);

    n = 24; k = 5;
    print_sequence(n, k);

    n = 6; k = 4;
    print_sequence(n, k);
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 code to find the series
# with largest GCD and sum equals to n

def print_sequence(n, k):

    # stores the maximum gcd that
    # can be possible of sequence.

    b = int(n / (k * (k + 1) / 2));

    # if maximum gcd comes out to be
    # zero then not possible

    if b == 0:
        print ("-1")

    else:
        # the smallest gcd possible is 1
        r = 1;

        # traverse the array to find out
        # the max gcd possible
        x = 1

        while x ** 2 <= n:

            # checks if the number is
            # divisible or not
            if n % x != 0:

                # x = x + 1
                continue;

            # checks if x is smaller then
            # the max gcd possible and x
            # is greater then the resultant
            # gcd till now, then r=x
            elif x <= b and x > r:
                r = x
                # x = x + 1

            # checks if n/x is smaller than
            # the max gcd possible and n/x
            # is greater then the resultant
            # gcd till now, then r=x
            elif n / x <= b and n / x > r :
                r = n / x
                # x = x + 1

            x = x + 1

    # traverses and prints d, 2d, 3d,
    # ..., (k-1)·d,
        i = 1
        while i < k :
            print (r * i, end = " ")
            i = i + 1

        last_term = n - (r * (k * (k - 1) / 2))
        print (last_term)

# main driver
print_sequence(24,4)
print_sequence(24,5)
print_sequence(6,4)

# This code is contributed by Saloni Gupta
```

## C#

```
// C# program to find the series with
// largest GCD and sum equals to n
using System;

class GFG {

// function to generate and
// print the sequence
static void print_sequence(int n, int k)
{

    // stores the maximum gcd that can be
    // possible of sequence.
    int b = n / (k * (k + 1) / 2);

    // if maximum gcd comes out to be
    // zero then not possible
    if (b == 0)
    {
        Console.Write("-1");

    }
    else
    {

        // the smallest gcd possible is 1
        int r = 1;

        // traverse the array to find out
        // the max gcd possible
        for (int x = 1; x * x <= n; x++)
        {

            // checks if the number is
            // divisible or not
            if (n % x != 0)
                continue;

            // checks if x is smaller then
            // the max gcd possible and x
            // is greater then the resultant
            // gcd till now, then r=x
            if (x <= b && x > r)
                r = x;

            // checks if n/x is smaller than
            // the max gcd possible and n/x
            // is greater then the resultant
            // gcd till now, then r=x
            if (n / x <= b && n / x > r)
                r = n / x;
        }

        // traverses and prints d, 2d,
        // 3d,..., (k-1)
        for (int i = 1; i < k; i++)
        Console.Write(r * i + " ");

        // computes the last element of
        // the sequence n-s.
        int res = n - (r * (k *
                  (k - 1) / 2));

        // prints the last element
        Console.WriteLine(res);
    }
}

// Driver Code
public static void Main()
{
    int n = 24;
    int k = 4;
    print_sequence(n, k);

    n = 24; k = 5;
    print_sequence(n, k);

    n = 6; k = 4;
    print_sequence(n, k);
}
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the
// series with largest GCD
// and sum equals to n

// function to generate and
// print the sequence
function print_sequence($n, $k)
{
    // stores the maximum gcd that
    // can be possible of sequence.
    $b = (int)($n / ($k * ($k + 1) / 2));

    // if maximum gcd comes out to be
    // zero then not possible
    if ($b == 0)
    {
        echo(-1);
    }
    else
    {

        // the smallest gcd possible is 1
        $r = 1;

        // traverse the array to find out
        // the max gcd possible
        for ($x = 1; $x * $x <= $n; $x++)
        {

            // checks if the number is
            // divisible or not
            if ($n % $x != 0)
                continue;

            // checks if x is smaller then
            // the max gcd possible and x
            // is greater then the resultant
            // gcd till now, then r=x
            if ($x <= $b && $x > $r)
                $r = $x;

            // checks if n/x is smaller than
            // the max gcd possible and n/x
            // is greater then the resultant
            // gcd till now, then r=x
            if ($n / $x <= $b && $n / $x > $r)
                $r = $n / $x;
        }

        // traverses and prints d, 2d, 3d,
        // ..., (k-1)·d,
        for ($i = 1; $i < $k; $i++)
            echo($r * $i . " ");

        // computes the last element of
        // the sequence n-s.
        $res = $n - ($r * ($k * ($k - 1) / 2));

        // prints the last element
        echo($res . "\n");
    }
}

// Driver Code
$n = 24;
$k = 4;
print_sequence($n, $k);

$n = 24; $k = 5;
print_sequence($n, $k);

$n = 6; $k = 4;
print_sequence($n, $k);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// series with largest GCD
// and sum equals to n

// function to generate and
// print the sequence
function print_sequence(n, k)
{
    // stores the maximum gcd that
    // can be possible of sequence.
    let b = parseInt(n / (k * (k + 1) / 2));

    // if maximum gcd comes out to be
    // zero then not possible
    if (b == 0)
    {
        document.write(-1);
    }
    else
    {

        // the smallest gcd possible is 1
        let r = 1;

        // traverse the array to find out
        // the max gcd possible
        for (let x = 1; x * x <= n; x++)
        {

            // checks if the number is
            // divisible or not
            if (n % x != 0)
                continue;

            // checks if x is smaller then
            // the max gcd possible and x
            // is greater then the resultant
            // gcd till now, then r=x
            if (x <= b && x > r)
                r = x;

            // checks if n/x is smaller than
            // the max gcd possible and n/x
            // is greater then the resultant
            // gcd till now, then r=x
            if (n / x <= b && n / x > r)
                r = n / x;
        }

        // traverses and prints d, 2d, 3d,
        // ..., (k-1)·d,
        for (let i = 1; i < k; i++)
            document.write(r * i + " ");

        // computes the last element of
        // the sequence n-s.
        let res = n - (r * (k * (k - 1) / 2));

        // prints the last element
        document.write(res + "<br>");
    }
}

// Driver Code
let n = 24;
let k = 4;
print_sequence(n, k);

n = 24;
k = 5;
print_sequence(n, k);

n = 6;
k = 4;
print_sequence(n, k);

// This code is contributed by _saurabh_jaiswal.

</script>
```

**输出:**

```
2 4 6 12
1 2 3 4 14
-1
```

**时间复杂度:** O( sqrt (n) )
**辅助空间:** O(1)
本文由[***Raja Vikramaditya***](https://www.facebook.com/raja.vikramaditya.7)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。