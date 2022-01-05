# 最小的数字 k，使得 k 的位数的乘积等于 n

> 原文:[https://www . geesforgeks . org/minist-number-k-product-digits-k-equal-n/](https://www.geeksforgeeks.org/smallest-number-k-product-digits-k-equal-n/)

给定一个非负数 **n** 。问题是找到最小的数 **k** ，使得 **k** 的位数乘积等于 **n** 。如果不能形成这样的数字 **k** ，则打印“-1”。
**举例:**

```
Input : 100
Output : 455
4*5*5 = 100 and 455 is the
smallest possible number.

Input : 26
Output : -1
```

**来源:**亚马逊采访
提问

**逼近:**对于每一个 **i** = 9 到 2，反复用 **i** 除 **n** ，直到不能再除或者从 **9** 到 **2** 的数字列表完成。此外，在分割过程中，将每个数字 **i** 推到将 **n** 完全分割的堆栈上。上述过程完成后，检查 n == 1。如果不是，则打印“-1”，否则使用堆栈中的数字形成数字 **k** ，这些数字包含与堆栈中弹出的数字相同的顺序。

## C++

```
// C++ implementation to find smallest number k such that
// the product of digits of k is equal to n
#include <bits/stdc++.h>

using namespace std;

// function to find smallest number k such that
// the product of digits of k is equal to n
long long int smallestNumber(int n)
{
    // if 'n' is a single digit number, then
    // it is the required number
    if (n >= 0 && n <= 9)
        return n;

    // stack the store the digits
    stack<int> digits;

    // repeatedly divide 'n' by the numbers
    // from 9 to 2 until all the numbers are
    // used or 'n' > 1
    for (int i=9; i>=2 && n > 1; i--)
    {
        while (n % i == 0)
        {
            // save the digit 'i' that divides 'n'
            // onto the stack
            digits.push(i);
            n = n / i;
        }
    }

    // if true, then no number 'k' can be formed
    if (n != 1)
        return -1;

    // pop digits from the stack 'digits'
    // and add them to 'k'
    long long int k = 0;
    while (!digits.empty())
    {
        k = k*10 + digits.top();
        digits.pop();
    }

    // required smallest number
    return k;
}

// Driver program to test above
int main()
{
    int n = 100;
    cout << smallestNumber(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation to find smallest number k such that
// the product of digits of k is equal to n
import java.util.Stack;

public class GFG {

// function to find smallest number k such that
// the product of digits of k is equal to n
    static long smallestNumber(int n) {
        // if 'n' is a single digit number, then
        // it is the required number
        if (n >= 0 && n <= 9) {
            return n;
        }

        // stack the store the digits
        Stack<Integer> digits = new Stack<>();

        // repeatedly divide 'n' by the numbers
        // from 9 to 2 until all the numbers are
        // used or 'n' > 1
        for (int i = 9; i >= 2 && n > 1; i--) {
            while (n % i == 0) {
                // save the digit 'i' that divides 'n'
                // onto the stack
                digits.push(i);
                n = n / i;
            }
        }

        // if true, then no number 'k' can be formed
        if (n != 1) {
            return -1;
        }

        // pop digits from the stack 'digits'
        // and add them to 'k'
        long k = 0;
        while (!digits.empty()) {
            k = k * 10 + digits.peek();
            digits.pop();
        }

        // required smallest number
        return k;
    }

// Driver program to test above
    static public void main(String[] args) {
        int n = 100;
        System.out.println(smallestNumber(n));
    }
}

/*This code is contributed by PrinciRaj1992*/
```

## 蟒蛇 3

```
# Python3 implementation to find smallest
# number k such that the product of digits
# of k is equal to n
import math as mt

# function to find smallest number k such that
# the product of digits of k is equal to n
def smallestNumber(n):

    # if 'n' is a single digit number, then
    # it is the required number
    if (n >= 0 and n <= 9):
        return n

    # stack the store the digits
    digits = list()

    # repeatedly divide 'n' by the numbers
    # from 9 to 2 until all the numbers are
    # used or 'n' > 1
    for i in range(9,1, -1):

        while (n % i == 0):

            # save the digit 'i' that
            # divides 'n' onto the stack
            digits.append(i)
            n = n //i

    # if true, then no number 'k'
    # can be formed
    if (n != 1):
        return -1

    # pop digits from the stack 'digits'
    # and add them to 'k'
    k = 0
    while (len(digits) != 0):

        k = k * 10 + digits[-1]
        digits.pop()

    # required smallest number
    return k

# Driver Code
n = 100
print(smallestNumber(n))

# This code is contributed by
# Mohit kumar 29
```

## C#

```

// C# implementation to find smallest number k such that
// the product of digits of k is equal to n
using System;
using System.Collections.Generic;
public class GFG {

// function to find smallest number k such that
// the product of digits of k is equal to n
    static long smallestNumber(int n) {
        // if 'n' is a single digit number, then
        // it is the required number
        if (n >= 0 && n <= 9) {
            return n;
        }

        // stack the store the digits
        Stack<int> digits = new Stack<int>();

        // repeatedly divide 'n' by the numbers
        // from 9 to 2 until all the numbers are
        // used or 'n' > 1
        for (int i = 9; i >= 2 && n > 1; i--) {
            while (n % i == 0) {
                // save the digit 'i' that divides 'n'
                // onto the stack
                digits.Push(i);
                n = n / i;
            }
        }

        // if true, then no number 'k' can be formed
        if (n != 1) {
            return -1;
        }

        // pop digits from the stack 'digits'
        // and add them to 'k'
        long k = 0;
        while (digits.Count!=0) {
            k = k * 10 + digits.Peek();
            digits.Pop();
        }

        // required smallest number
        return k;
    }

// Driver program to test above
    static public void Main() {
        int n = 100;
        Console.Write(smallestNumber(n));
    }
}

/*This code is contributed by Rajput-Ji*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find smallest number k such that
// the product of digits of k is equal to n

// function to find smallest number k such that
// the product of digits of k is equal to n
function smallestNumber($n)
{
    // if 'n' is a single digit number, then
    // it is the required number
    if ($n >= 0 && $n <= 9)
        return $n;

    // stack the store the digits
    $digits = array();

    // repeatedly divide 'n' by the numbers
    // from 9 to 2 until all the numbers are
    // used or 'n' > 1
    for ($i = 9; $i >= 2 && $n > 1; $i--)
    {
        while ($n % $i == 0)
        {
            // save the digit 'i' that divides 'n'
            // onto the stack
            array_push($digits,$i);
            $n =(int)( $n / $i);
        }
    }

    // if true, then no number 'k' can be formed
    if ($n != 1)
        return -1;

    // pop digits from the stack 'digits'
    // and add them to 'k'
    $k = 0;
    while (!empty($digits))
        $k = $k * 10 + array_pop($digits);

    // required smallest number
    return $k;
}

    // Driver code
    $n = 100;
    echo smallestNumber($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find
// smallest number k such that
// the product of digits of k is equal to n

    // function to find smallest number k such that
// the product of digits of k is equal to n
    function smallestNumber(n)
    {
        // if 'n' is a single digit number, then
        // it is the required number
        if (n >= 0 && n <= 9) {
            return n;
        }

        // stack the store the digits
        let digits = [];

        // repeatedly divide 'n' by the numbers
        // from 9 to 2 until all the numbers are
        // used or 'n' > 1
        for (let i = 9; i >= 2 && n > 1; i--) {
            while (n % i == 0) {
                // save the digit 'i' that divides 'n'
                // onto the stack
                digits.push(i);
                n = Math.floor(n / i);
            }
        }

        // if true, then no number 'k' can be formed
        if (n != 1) {
            return -1;
        }

        // pop digits from the stack 'digits'
        // and add them to 'k'
        let k = 0;
        while (digits.length!=0) {
            k = k * 10 + digits[digits.length-1];
            digits.pop();
        }

        // required smallest number
        return k;
    }

    // Driver program to test above
    let n = 100;
    document.write(smallestNumber(n));

// This code is contributed by patel2127

</script>
```

**输出:**

```
455
```

**时间复杂度:** O(num)，其中 **num** 就是栈的大小。
**空间复杂度:** O(num)，其中 **num** 就是栈的大小。
我们可以将需要的号码 **k** 以字符串的形式存储，用于大号码。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。