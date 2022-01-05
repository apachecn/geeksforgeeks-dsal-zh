# 将 n 分为最大合成数

> 原文:[https://www . geesforgeks . org/split-n-maximum-composite-numbers/](https://www.geeksforgeeks.org/split-n-maximum-composite-numbers/)

给定 n，打印总和为 n 的最大数量的[复合数](https://www.geeksforgeeks.org/composite-number/)，前几个复合数为 4、6、8、9、10、12、14、15、16、18、20、……
**示例:**

```
Input: 90   
Output: 22
Explanation: If we add 21 4's, then we 
get 84 and then add 6 to it, we get 90.

Input: 10
Output: 2
Explanation: 4 + 6 = 10
```

以下是一些重要的观察结果。

1.  如果数字小于 4，就不会有任何组合。
2.  如果数字是 5，7，11，它不会有任何分裂。
3.  因为最小的复合数是 4，所以使用最大的 4 是有意义的。
4.  对于除以 4 后没有复合余数的数字，我们做如下处理。如果余数是 1，我们从中减去 9，得到完全可被 4 整除的数。如果余数是 2，那就减去 6，使 n 成为一个能被 4 整除的数。如果余数是 3，那么从中减去 15，使 n 完全能被 4 整除，15 就能被 9 + 6 整除。

所以主要的观察是使 n 这样，它由最大数为 4 的组成，剩下的可以由 6 和 9 组成。我们不需要比这更多的复合数，因为 9 以上的复合数可以由 4、6 和 9 组成。
以下是上述方法的实施

## C++

```
// CPP program to split a number into maximum
// number of composite numbers.
#include <bits/stdc++.h>
using namespace std;

// function to calculate the maximum number of
// composite numbers adding upto n
int count(int n)
{
    // 4 is the smallest composite number
    if (n < 4)
        return -1;

    // stores the remainder when n is divided
    // by 4
    int rem = n % 4;

    // if remainder is 0, then it is perfectly
    // divisible by 4.
    if (rem == 0)
        return n / 4;

    // if the remainder is 1
    if (rem == 1) {

        // If the number is less then 9, that
        // is 5, then it cannot be expressed as
        // 4 is the only composite number less
        // than 5
        if (n < 9)
            return -1;

        // If the number is greater then 8, and
        // has a remainder of 1, then express n
        // as n-9 a and it is perfectly divisible
        // by 4 and for 9, count 1.
        return (n - 9) / 4 + 1;
    }

    // When remainder is 2, just subtract 6 from n,
    // so that n is perfectly divisible by 4 and
    // count 1 for 6 which is subtracted.
    if (rem == 2)
        return (n - 6) / 4 + 1;

    // if the number is 7, 11 which cannot be
    // expressed as sum of any composite numbers
    if (rem == 3) {
        if (n < 15)
            return -1;

        // when the remainder is 3, then subtract
        // 15 from it and n becomes perfectly
        // divisible by 4 and we add 2 for 9 and 6,
        // which is getting subtracted to make n
        // perfectly divisible by 4.
        return (n - 15) / 4 + 2;
    }
}

// driver program to test the above function
int main()
{
    int n = 90;
    cout << count(n) << endl;

    n = 143;
    cout << count(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to split a number into maximum
// number of composite numbers.
import java.io.*;

class GFG
{
    // function to calculate the maximum number of
    // composite numbers adding upto n
    static int count(int n)
    {
        // 4 is the smallest composite number
        if (n < 4)
            return -1;

        // stores the remainder when n is divided
        // by 4
        int rem = n % 4;

        // if remainder is 0, then it is perfectly
        // divisible by 4.
        if (rem == 0)
            return n / 4;

        // if the remainder is 1
        if (rem == 1) {

            // If the number is less then 9, that
            // is 5, then it cannot be expressed as
            // 4 is the only composite number less
            // than 5
            if (n < 9)
                return -1;

            // If the number is greater then 8, and
            // has a remainder of 1, then express n
            // as n-9 a and it is perfectly divisible
            // by 4 and for 9, count 1.
            return (n - 9) / 4 + 1;
        }

        // When remainder is 2, just subtract 6 from n,
        // so that n is perfectly divisible by 4 and
        // count 1 for 6 which is subtracted.
        if (rem == 2)
            return (n - 6) / 4 + 1;

        // if the number is 7, 11 which cannot be
        // expressed as sum of any composite numbers
        if (rem == 3)
        {
            if (n < 15)
                return -1;

            // when the remainder is 3, then subtract
            // 15 from it and n becomes perfectly
            // divisible by 4 and we add 2 for 9 and 6,
            // which is getting subtracted to make n
            // perfectly divisible by 4.
            return (n - 15) / 4 + 2;
        }
        return 0;
    }

    // Driver program
    public static void main (String[] args)
    {
        int n = 90;
        System.out.println(count(n));

        n = 143;
        System.out.println(count(n));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python3 program to split a number into
# maximum number of composite numbers.

# Function to calculate the maximum number
# of composite numbers adding upto n
def count(n):

    # 4 is the smallest composite number
    if (n < 4):
        return -1

    # stores the remainder when n 
    # is divided n is divided by 4
    rem = n % 4

    # if remainder is 0, then it is 
    # perfectly divisible by 4.
    if (rem == 0):
        return n // 4

    # if the remainder is 1
    if (rem == 1):

        # If the number is less then 9, that
        # is 5, then it cannot be expressed as
        # 4 is the only composite number less
        # than 5
        if (n < 9):
            return -1

        # If the number is greater then 8, and
        # has a remainder of 1, then express n
        # as n-9 a and it is perfectly divisible
        # by 4 and for 9, count 1.
        return (n - 9) // 4 + 1

    # When remainder is 2, just subtract 6 from n,
    # so that n is perfectly divisible by 4 and
    # count 1 for 6 which is subtracted.
    if (rem == 2):
        return (n - 6) // 4 + 1

    # if the number is 7, 11 which cannot be
    # expressed as sum of any composite numbers
    if (rem == 3):
        if (n < 15):
            return -1

        # when the remainder is 3, then subtract
        # 15 from it and n becomes perfectly
        # divisible by 4 and we add 2 for 9 and 6,
        # which is getting subtracted to make n
        # perfectly divisible by 4.
        return (n - 15) // 4 + 2

# Driver Code
n = 90
print(count(n))

n = 143
print(count(n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to split a number into maximum
// number of composite numbers.
using System;

class GFG {

    // function to calculate the maximum number
    // of composite numbers adding upto n
    static int count(int n)
    {

        // 4 is the smallest composite number
        if (n < 4)
            return -1;

        // stores the remainder when n is divided
        // by 4
        int rem = n % 4;

        // if remainder is 0, then it is perfectly
        // divisible by 4.
        if (rem == 0)
            return n / 4;

        // if the remainder is 1
        if (rem == 1) {

            // If the number is less then 9, that
            // is 5, then it cannot be expressed as
            // 4 is the only composite number less
            // than 5
            if (n < 9)
                return -1;

            // If the number is greater then 8, and
            // has a remainder of 1, then express n
            // as n-9 a and it is perfectly divisible
            // by 4 and for 9, count 1.
            return (n - 9) / 4 + 1;
        }

        // When remainder is 2, just subtract 6 from n,
        // so that n is perfectly divisible by 4 and
        // count 1 for 6 which is subtracted.
        if (rem == 2)
            return (n - 6) / 4 + 1;

        // if the number is 7, 11 which cannot be
        // expressed as sum of any composite numbers
        if (rem == 3)
        {
            if (n < 15)
                return -1;

            // when the remainder is 3, then subtract
            // 15 from it and n becomes perfectly
            // divisible by 4 and we add 2 for 9 and 6,
            // which is getting subtracted to make n
            // perfectly divisible by 4.
            return (n - 15) / 4 + 2;
        }

        return 0;
    }

    // Driver program
    public static void Main()
    {
        int n = 90;
        Console.WriteLine(count(n));

        n = 143;
        Console.WriteLine(count(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to split a number
// into maximum number of
// composite numbers.

// function to calculate the
// maximum number of composite
// numbers adding upto n
function c_ount($n)
{

    // 4 is the smallest
    // composite number
    if ($n < 4)
        return -1;

    // stores the remainder when
    // n is divided by 4
    $rem = $n % 4;

    // if remainder is 0, then it
    // is perfectly divisible by 4.
    if ($rem == 0)
        return $n / 4;

    // if the remainder is 1
    if ($rem == 1) {

        // If the number is less
        // then 9, that is 5, then
        // it cannot be expressed
        // as  4 is the only
        //composite number less
        // than 5
        if ($n < 9)
            return -1;

        // If the number is greater
        // then 8, and has a
        // remainder of 1, then
        // express n as n-9 a and
        // it is perfectly divisible
        // by 4 and for 9, count 1.
        return ($n - 9) / 4 + 1;
    }

    // When remainder is 2, just
    // subtract 6 from n, so that n
    // is perfectly divisible by 4
    // and count 1 for 6 which is
    // subtracted.
    if ($rem == 2)
        return ($n - 6) / 4 + 1;

    // if the number is 7, 11 which
    // cannot be expressed as sum of
    // any composite numbers
    if ($rem == 3) {
        if ($n < 15)
            return -1;

        // when the remainder is 3,
        // then subtract 15 from it
        // and n becomes perfectly
        // divisible by 4 and we add
        // 2 for 9 and 6, which is
        // getting subtracted to make
        // n perfectly divisible by 4.
        return ($n - 15) / 4 + 2;
    }
}

// driver program to test the above
// function

    $n = 90;
    echo c_ount($n),"\n";

    $n = 143;
    echo c_ount($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to split a number
// into maximum number of
// composite numbers.

// function to calculate the
// maximum number of composite
// numbers adding upto n
function c_ount(n)
{

    // 4 is the smallest
    // composite number
    if (n < 4)
        return -1;

    // stores the remainder when
    // n is divided by 4
    let rem = n % 4;

    // if remainder is 0, then it
    // is perfectly divisible by 4.
    if (rem == 0)
        return n / 4;

    // if the remainder is 1
    if (rem == 1) {

        // If the number is less
        // then 9, that is 5, then
        // it cannot be expressed
        // as  4 is the only
        //composite number less
        // than 5
        if (n < 9)
            return -1;

        // If the number is greater
        // then 8, and has a
        // remainder of 1, then
        // express n as n-9 a and
        // it is perfectly divisible
        // by 4 and for 9, count 1.
        return (n - 9) / 4 + 1;
    }

    // When remainder is 2, just
    // subtract 6 from n, so that n
    // is perfectly divisible by 4
    // and count 1 for 6 which is
    // subtracted.
    if (rem == 2)
        return (n - 6) / 4 + 1;

    // if the number is 7, 11 which
    // cannot be expressed as sum of
    // any composite numbers
    if (rem == 3) {
        if (n < 15)
            return -1;

        // when the remainder is 3,
        // then subtract 15 from it
        // and n becomes perfectly
        // divisible by 4 and we add
        // 2 for 9 and 6, which is
        // getting subtracted to make
        // n perfectly divisible by 4.
        return (n - 15) / 4 + 2;
    }
}

// driver program to test the above
// function

    let n = 90;
    document.write(c_ount(n) + "<br>");

    n = 143;
    document.write(c_ount(n));

// This code is contributed by _saurabh_jaiswal.
</script>
```

输出:

```
22 
34 
```

时间复杂度:O(1)
辅助空间:O(1)
本文由 [**拉贾·维克拉玛迪特亚**](https://www.facebook.com/raja.vikramaditya.7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。