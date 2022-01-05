# 二进制表示的最大数是 m 1 和 m-10

> 原文:[https://www . geesforgeks . org/maximum-number-binary-presentation-m-1s-m-1-0s/](https://www.geeksforgeeks.org/largest-number-binary-representation-m-1s-m-1-0s/)

给定 n，找出严格来说不超过 n 的最大数，其二进制表示由 m 个连续的 1 组成，然后是 m-1 个连续的 0，没有别的
**例:**

```
Input : n = 7 
Output : 6 
Explanation: 6's binary representation is 110,
and 7's is 111, so 6 consists of 2 consecutive 
1's and then 1 consecutive 0.

Input : 130
Output : 120 
Explanation: 28 and 120 are the only numbers <=120,
28 is 11100 consists of 3 consecutive 1's and then 
2 consecutive 0's. 120 is 1111000 consists of 4 
consecutive 1's and then 3 consecutive 0's. So 120
is the greatest of number<=120 which meets the
given condition. 
```

一种简单的方法是从 1 遍历到 N，检查由 m 个连续的 1 和 m-1 个连续的 0 组成的每个二进制表示，并存储满足给定条件的最大值。
一种**有效的方法**是观察数字的模式，
[ **1(1)，6(110)，28(11100)，120(1111000)，496(111110000)，…。】**
为了得到满足条件的数的公式，我们以 120 为例-
120 表示为 1111000，其中 m = 4 1，m = 3 0。将 1111000 转换为十进制，我们得到:
2^3+2^4+2^5+2^6 可以表示为(2^m-1 + 2^m+ 2^m+1 + … 2^m+2，2^2*m)
2^3*(1+2+2^2+2^3)可以表示为(2^(m-1)*(1+2+2^2+2^3+)..2^(m-1)
2^3*(2^4-1)可以表示为**【2^(m-1)*(2^m-1】。**
所以所有满足给定条件的数字都可以表示为

> [2^(m-1) * (2^m -1)]

我们可以迭代，直到个数不超过 N，打印出所有可能元素中最大的一个。仔细观察会发现，在 **m = 33 时，它将超过 10^18 标记**，因此我们计算单位时间内的数字，因为 **log(32)** 接近常数，这是计算**幂**所需要的。
所以，整体复杂度会是 O(1)。

## C++

```
// CPP program to find largest number
// smaller than equal to n with m set
// bits then m-1 0 bits.
#include <bits/stdc++.h>
using namespace std;

// Returns largest number with m set
// bits then m-1 0 bits.
long long answer(long long n)
{
    // Start with 2 bits.
    long m = 2;

    // initial answer is 1
    // which meets the given condition
    long long ans = 1;
    long long r = 1;

    // check for all numbers
    while (r < n) {

        // compute the number
        r = (int)(pow(2, m) - 1) * (pow(2, m - 1));

        // if less then N
        if (r < n)
            ans = r;

        // increment m to get the next number
        m++;
    }

    return ans;
}

// driver code to check the above condition
int main()
{
    long long n = 7;
    cout << answer(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find largest number
// smaller than equal to n with m set
// bits then m-1 0 bits.
public class GFG {

    // Returns largest number with
    // m set bits then m-1 0 bits.
    static long answer(long n)
    {

        // Start with 2 bits.
        long m = 2;

        // initial answer is 1 which
        // meets the given condition
        long ans = 1;
        long r = 1;

        // check for all numbers
        while (r < n) {

            // compute the number
            r = ((long)Math.pow(2, m) - 1) *
                ((long)Math.pow(2, m - 1));

            // if less then N
            if (r < n)
                ans = r;

            // increment m to get
            // the next number
            m++;
        }

        return ans;
    }

    // Driver code  
    public static void main(String args[]) {

         long n = 7;
         System.out.println(answer(n));
    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python3 program to find
# largest number smaller
# than equal to n with m
# set bits then m-1 0 bits.
import math

# Returns largest number
# with m set bits then
# m-1 0 bits.
def answer(n):

    # Start with 2 bits.
    m = 2;

    # initial answer is
    # 1 which meets the
    # given condition
    ans = 1;
    r = 1;

    # check for all numbers
    while r < n:

        # compute the number
        r = (int)((pow(2, m) - 1) *
                  (pow(2, m - 1)));

        # if less then N
        if r < n:
            ans = r;

        # increment m to get
        # the next number
        m = m + 1;
    return ans;

# Driver Code
print(answer(7));

# This code is contributed by mits.
```

## C#

```
// C# program to find largest number
// smaller than equal to n with m set
// bits then m-1 0 bits.
using System;

class GFG {

// Returns largest number with
// m set bits then m-1 0 bits.
static long answer(long n)
{

    // Start with 2 bits.
    long m = 2;

    // initial answer is 1 which
    // meets the given condition
    long ans = 1;
    long r = 1;

    // check for all numbers
    while (r < n) {

        // compute the number
        r = ((long)Math.Pow(2, m) - 1) *
            ((long)Math.Pow(2, m - 1));

        // if less then N
        if (r < n)
            ans = r;

        // increment m to get
        // the next number
        m++;
    }

    return ans;
}

    // Driver Code
    static public void Main ()
    {
        long n = 7;
        Console.WriteLine(answer(n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find largest number
// smaller than equal to n with m set
// bits then m-1 0 bits.

// Returns largest number with m set
// bits then m-1 0 bits.
function answer( $n)
{

    // Start with 2 bits.
    $m = 2;

    // initial answer is 1
    // which meets the
    // given condition
    $ans = 1;
    $r = 1;

    // check for all numbers
    while ($r < $n)
    {

        // compute the number
        $r = (pow(2, $m) - 1) *
             (pow(2, $m - 1));

        // if less then N
        if ($r < $n)
            $ans = $r;

        // increment m to get
        // the next number
        $m++;
    }

    return $ans;
}

    // Driver Code
    $n = 7;
    echo answer($n);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find largest number
// smaller than equal to n with m set
// bits then m-1 0 bits.

    // Returns largest number with
    // m set bits then m-1 0 bits.
    function answer(n)
    {

        // Start with 2 bits.
        let m = 2;

        // initial answer is 1 which
        // meets the given condition
        let ans = 1;
        let r = 1;

        // check for all numbers
        while (r < n) {

            // compute the number
            r = (Math.pow(2, m) - 1) *
                (Math.pow(2, m - 1));

            // if less then N
            if (r < n)
                ans = r;

            // increment m to get
            // the next number
            m++;
        }

        return ans;
    }

// Driver code

        let n = 7;
        document.write(answer(n));

</script>
```

**输出:**

```
6
```