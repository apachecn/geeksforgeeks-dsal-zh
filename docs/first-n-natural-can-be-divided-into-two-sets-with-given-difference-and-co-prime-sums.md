# 前 N 个自然数可以分成给定差和同素和的两组

> 原文:[https://www . geeksforgeeks . org/first-n-natural-can-division-two-set-with-given-different-and-co-prime-sums/](https://www.geeksforgeeks.org/first-n-natural-can-be-divided-into-two-sets-with-given-difference-and-co-prime-sums/)

给定 N 和 M，任务是找出数字 1 到 N 是否可以分成两个集合，使得两个集合之和的绝对差为 M，两个集合之和的 gcd 为 1(即两个集合之和为同素)。
**先决条件:**[CPP 中的 GCD](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/)| GCD
**示例:**

> 输入:N = 5 和 M = 7
> 输出:是
> **解释:**由于从 1 到 5 的数字可以分为两组{1，2，3，5}和{4}，因此两组之和的绝对差为 11–4 = 7，等于 M，也等于 GCD(11，4) = 1。
> 输入:N = 6，M = 3
> 输出:NO
> **说明:**在这种情况下，从 1 到 6 的数字可以分为两组{1，2，4，5}和{3，6}，这样它们之和的绝对差为 12–9 = 3。但是，由于 12 和 9 不像 GCD(12，9) = 3 那样是同素的，答案是“否”。

**逼近:**既然我们有 1 到 N 个数，就知道所有数的和是 N * (N + 1) / 2。设 S1 和 S2 是两个集合，这样，
1)和(S1) +和(S2) = N * (N + 1) / 2
2)和(S1)–和(S2) = M
解这两个方程就可以得到这两个集合的和。如果 sum(S1)和 sum(S2)是整数并且它们是同素的(它们的 GCD 是 1)，那么有一种方法可以将数字分成两组。否则，没有办法拆分这 N 个数字。
下面是上述解决方案的实现。

## C++

```
/* CPP code to determine whether numbers
   1 to N can be divided into two sets
   such that absolute difference between
   sum of these two sets is M and these
   two sum are co-prime*/
#include <bits/stdc++.h>
using namespace std;

// function that returns boolean value
// on the basis of whether it is possible
// to divide 1 to N numbers into two sets
// that satisfy given conditions.
bool isSplittable(int n, int m)
{
    // initializing total sum of 1
    // to n numbers
    int total_sum = (n * (n + 1)) / 2;

    // since (1) total_sum = sum_s1 + sum_s2
    // and (2) m = sum_s1 - sum_s2
    // assuming sum_s1 > sum_s2.
    // solving these 2 equations to get
    // sum_s1 and sum_s2
    int sum_s1 = (total_sum + m) / 2;

    // total_sum = sum_s1 + sum_s2
    // and therefore
    int sum_s2 = total_sum - sum_s1;

    // if total sum is less than the absolute
    // difference then there is no way we
    // can split n numbers into two sets
    // so return false
    if (total_sum < m)
        return false;

    // check if these two sums are
    // integers and they add up to
    // total sum and also if their
    // absolute difference is m.
    if (sum_s1 + sum_s2 == total_sum &&
        sum_s1 - sum_s2 == m)

        // Now if two sum are co-prime
        // then return true, else return false.
        return (__gcd(sum_s1, sum_s2) == 1);

    // if two sums don't add up to total
    // sum or if their absolute difference
    // is not m, then there is no way to
    // split n numbers, hence return false
    return false;
}

// Driver code
int main()
{
    int n = 5, m = 7;

    // function call to determine answer
    if (isSplittable(n, m))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java code to determine whether numbers
1 to N can be divided into two sets
such that absolute difference between
sum of these two sets is M and these
two sum are co-prime*/
class GFG
{
    static int GCD (int a, int b)
    {
        return b == 0 ? a : GCD(b, a % b);
    }

    // function that returns boolean value
    // on the basis of whether it is possible
    // to divide 1 to N numbers into two sets
    // that satisfy given conditions.
    static boolean isSplittable(int n, int m)
    {

        // initializing total sum of 1
        // to n numbers
        int total_sum = (n * (n + 1)) / 2;

        // since (1) total_sum = sum_s1 + sum_s2
        // and (2) m = sum_s1 - sum_s2
        // assuming sum_s1 > sum_s2.
        // solving these 2 equations to get
        // sum_s1 and sum_s2
        int sum_s1 = (total_sum + m) / 2;

        // total_sum = sum_s1 + sum_s2
        // and therefore
        int sum_s2 = total_sum - sum_s1;

        // if total sum is less than the absolute
        // difference then there is no way we
        // can split n numbers into two sets
        // so return false
        if (total_sum < m)
            return false;

        // check if these two sums are
        // integers and they add up to
        // total sum and also if their
        // absolute difference is m.
        if (sum_s1 + sum_s2 == total_sum &&
                    sum_s1 - sum_s2 == m)

            // Now if two sum are co-prime
            // then return true, else return false.
            return (GCD(sum_s1, sum_s2) == 1);

        // if two sums don't add up to total
        // sum or if their absolute difference
        // is not m, then there is no way to
        // split n numbers, hence return false
        return false;
    }

    // Driver Code
    public static void main(String args[])
    {
        int n = 5, m = 7;

        // function call to determine answer
        if (isSplittable(n, m))
            System.out.println("Yes");
        else
            System.out.println("No");

    }
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python3 code to determine whether numbers
# 1 to N can be divided into two sets
# such that absolute difference between
# sum of these two sets is M and these
# two sum are co-prime

def __gcd (a, b):

        return a if(b == 0) else __gcd(b, a % b);

# function that returns boolean value
# on the basis of whether it is possible
# to divide 1 to N numbers into two sets
# that satisfy given conditions.
def isSplittable(n, m):

    # initializing total sum of 1
    # to n numbers
    total_sum = (int)((n * (n + 1)) / 2);

    # since (1) total_sum = sum_s1 + sum_s2
    # and (2) m = sum_s1 - sum_s2
    # assuming sum_s1 > sum_s2.
    # solving these 2 equations to get
    # sum_s1 and sum_s2
    sum_s1 = int((total_sum + m) / 2);

    # total_sum = sum_s1 + sum_s2
    # and therefore
    sum_s2 = total_sum - sum_s1;

    # if total sum is less than the absolute
    # difference then there is no way we
    # can split n numbers into two sets
    # so return false
    if (total_sum < m):
        return False;

    # check if these two sums are
    # integers and they add up to
    # total sum and also if their
    # absolute difference is m.
    if (sum_s1 + sum_s2 == total_sum and
                 sum_s1 - sum_s2 == m):

        # Now if two sum are co-prime
        # then return true, else return false.
        return (__gcd(sum_s1, sum_s2) == 1);

    # if two sums don't add up to total
    # sum or if their absolute difference
    # is not m, then there is no way to
    # split n numbers, hence return false
    return False;

# Driver code
n = 5;
m = 7;

# function call to determine answer
if (isSplittable(n, m)):
    print("Yes");
else:
    print("No");

# This code is contributed by mits
```

## C#

```
/* C# code to determine whether numbers
1 to N can be divided into two sets
such that absolute difference between
sum of these two sets is M and these
two sum are co-prime*/
using System;

class GFG {

    static int GCD (int a, int b)
    {
        return b == 0 ? a : GCD(b, a % b);
    }

    // function that returns boolean value
    // on the basis of whether it is possible
    // to divide 1 to N numbers into two sets
    // that satisfy given conditions.
    static bool isSplittable(int n, int m)
    {

        // initializing total sum of 1
        // to n numbers
        int total_sum = (n * (n + 1)) / 2;

        // since (1) total_sum = sum_s1 + sum_s2
        // and (2) m = sum_s1 - sum_s2
        // assuming sum_s1 > sum_s2.
        // solving these 2 equations to get
        // sum_s1 and sum_s2
        int sum_s1 = (total_sum + m) / 2;

        // total_sum = sum_s1 + sum_s2
        // and therefore
        int sum_s2 = total_sum - sum_s1;

        // if total sum is less than the absolute
        // difference then there is no way we
        // can split n numbers into two sets
        // so return false
        if (total_sum < m)
            return false;

        // check if these two sums are
        // integers and they add up to
        // total sum and also if their
        // absolute difference is m.
        if (sum_s1 + sum_s2 == total_sum &&
                       sum_s1 - sum_s2 == m)

            // Now if two sum are co-prime
            // then return true, else return false.
            return (GCD(sum_s1, sum_s2) == 1);

        // if two sums don't add up to total
        // sum or if their absolute difference
        // is not m, then there is no way to
        // split n numbers, hence return false
        return false;
    }

    // Driver code
    public static void Main()
    {
        int n = 5, m = 7;

        // function call to determine answer
        if (isSplittable(n, m))
            Console.Write("Yes");
        else
            Console.Write("No");
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
/* PHP code to determine whether numbers
1 to N can be divided into two sets
such that absolute difference between
sum of these two sets is M and these
two sum are co-prime*/

function __gcd ($a, $b)
{
        return $b == 0 ? $a : __gcd($b, $a % $b);
}

// function that returns boolean value
// on the basis of whether it is possible
// to divide 1 to N numbers into two sets
// that satisfy given conditions.
function isSplittable($n, $m)
{
    // initializing total sum of 1
    // to n numbers
    $total_sum = (int)(($n * ($n + 1)) / 2);

    // since (1) total_sum = sum_s1 + sum_s2
    // and (2) m = sum_s1 - sum_s2
    // assuming sum_s1 > sum_s2.
    // solving these 2 equations to get
    // sum_s1 and sum_s2
    $sum_s1 = (int)(($total_sum + $m) / 2);

    // total_sum = sum_s1 + sum_s2
    // and therefore
    $sum_s2 = $total_sum - $sum_s1;

    // if total sum is less than the absolute
    // difference then there is no way we
    // can split n numbers into two sets
    // so return false
    if ($total_sum < $m)
        return false;

    // check if these two sums are
    // integers and they add up to
    // total sum and also if their
    // absolute difference is m.
    if ($sum_s1 + $sum_s2 == $total_sum &&
        $sum_s1 - $sum_s2 == $m)

        // Now if two sum are co-prime
        // then return true, else return false.
        return (__gcd($sum_s1, $sum_s2) == 1);

    // if two sums don't add up to total
    // sum or if their absolute difference
    // is not m, then there is no way to
    // split n numbers, hence return false
    return false;
}

// Driver code
$n = 5;
$m = 7;

// function call to determine answer
if (isSplittable($n, $m))
    echo "Yes";
else
    echo "No";

// This Code is Contributed by mits
?>
```

## java 描述语言

```
<script>

/* Javascript code to determine whether numbers
1 to N can be divided into two sets
such that absolute difference between
sum of these two sets is M and these
two sum are co-prime*/

function __gcd (a, b)
{
        return b == 0 ? a : __gcd(b, a % b);
}

// function that returns boolean value
// on the basis of whether it is possible
// to divide 1 to N numbers into two sets
// that satisfy given conditions.
function isSplittable(n, m)
{
    // initializing total sum of 1
    // to n numbers
    let total_sum = parseInt((n * (n + 1)) / 2);

    // since (1) total_sum = sum_s1 + sum_s2
    // and (2) m = sum_s1 - sum_s2
    // assuming sum_s1 > sum_s2.
    // solving these 2 equations to get
    // sum_s1 and sum_s2
    let sum_s1 = parseInt((total_sum + m) / 2);

    // total_sum = sum_s1 + sum_s2
    // and therefore
    let sum_s2 = total_sum - sum_s1;

    // if total sum is less than the absolute
    // difference then there is no way we
    // can split n numbers into two sets
    // so return false
    if (total_sum < m)
        return false;

    // check if these two sums are
    // integers and they add up to
    // total sum and also if their
    // absolute difference is m.
    if (sum_s1 + sum_s2 == total_sum &&
        sum_s1 - sum_s2 == m)

        // Now if two sum are co-prime
        // then return true, else return false.
        return (__gcd(sum_s1, sum_s2) == 1);

    // if two sums don't add up to total
    // sum or if their absolute difference
    // is not m, then there is no way to
    // split n numbers, hence return false
    return false;
}

// Driver code
let n = 5;
let m = 7;

// function call to determine answer
if (isSplittable(n, m))
    document.write("Yes");
else
    document.write("No");

// This Code is Contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(log(n))