# 除 N 时比商多的除数计数

> 原文:[https://www . geesforgeks . org/count-dividers-set-bits-商-除法-n/](https://www.geeksforgeeks.org/count-divisors-set-bits-quotient-dividing-n/)

给定一个正整数 N，任务是找出除数(比如说 **d** )的个数，它给出整数除法(比如说 q = N/d)的商(比如说 **q** ),使得商比除数有更多的位或相等的设定位。换句话说，找出“d”的可能值的数量，这将在整数除“N”(q = N/d)上产生“q”，使得“q”比“d”具有更少或相等的设置位(至少 1)。

**示例:**

```
Input : N = 5
Output : 4
for d = 1 (set bit = 1), 
    q = 5/1 = 5 (set bit = 2), count = 0.
for d = 2 (set bit = 1), 
    q = 5/2 = 2 (set bit = 1), count = 1.
for d = 3 (set bit = 2), 
    q = 5/3 = 1 (set bit = 1), count = 2.
for d = 4 (set bit = 1), 
    q = 5/4 = 1 (set bit = 1), count = 3.
for d = 5 (set bit = 2), 
    q = 5/5 = 1 (set bit = 1), count = 4.

Input : N = 3
Output : 2
```

注意，对于所有的 **d > n** ，q 有 0 个设置位，所以没有必要超过 n。
同样，对于 **n/2 < d < = n** ，它将返回 q = 1，其中有 1 个设置位总是小于或等于 d。并且，d 的最小可能值是 1。所以，d 的可能值是从 1 到 n.
现在，通过 n 除以 d 来观察，其中 **1 < = d < = n** ，它将按排序顺序给出 q(递减)。
所以，随着 d 的增加，我们会得到递减的 q，所以，我们得到了两个排序的序列，一个用于增加 d
，另一个用于减少 q，现在，观察一下，最初，d 的设置位数大于 q，但是在一个点之后，d 的设置位数小于或等于 q
所以，我们的问题简化为找到那个点，即 d 值的‘x’， 从 **1 < = d < = n** ，使得 q 具有小于或等于 d 的设定位。
因此，使得 q 具有小于或等于 d 的设定位的可能 d 的计数将等于 n–x+1。

下面是该方法的实现:

## C++

```
// C++ Program to find number of Divisors
// which on integer division produce quotient
// having less set bit than divisor
#include <bits/stdc++.h>
using namespace std;

// Return the count of set bit.
int bit(int x)
{
    int ans = 0;

    while (x) {
        x /= 2;
        ans++;
    }

    return ans;
}

// check if q and d have same number of set bit.
bool check(int d, int x)
{
    if (bit(x / d) <= bit(d))
        return true;

    return false;
}

// Binary Search to find the point at which
// number of set in q is less than or equal to d.
int bs(int n)
{
    int l = 1, r = sqrt(n);

    // while left index is less than right index
    while (l < r) {
        // finding the middle.
        int m = (l + r) / 2;

        // check if q and d have same number of
       // set it or not.
        if (check(m, n))
            r = m;
        else
            l = m + 1;
    }

    if (!check(l, n))
        return l + 1;

    else
        return l;
}

int countDivisor(int n)
{
    return n - bs(n) + 1;
}
// Driven Program
int main()
{
    int n = 5;
    cout << countDivisor(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find number
// of Divisors which on integer
// division produce quotient
// having less set bit than divisor
import java .io.*;

class GFG
{

// Return the count of set bit.
static int bit(int x)
{
    int ans = 0;
    while (x > 0)
    {
        x /= 2;
        ans++;
    }

    return ans;
}

// check if q and d have
// same number of set bit.
static boolean check(int d, int x)
{
    if (bit(x / d) <= bit(d))
        return true;

    return false;
}

// Binary Search to find
// the point at which
// number of set in q is
// less than or equal to d.
static int bs(int n)
{
    int l = 1, r = (int)Math.sqrt(n);

    // while left index is
    // less than right index
    while (l < r)
    {
        // finding the middle.
        int m = (l + r) / 2;

    // check if q and d have
    // same number of
    // set it or not.
        if (check(m, n))
            r = m;
        else
            l = m + 1;
    }

    if (!check(l, n))
        return l + 1;

    else
        return l;
}

static int countDivisor(int n)
{
    return n - bs(n) + 1;
}

    // Driver Code
    static public void main (String[] args)
    {
        int n = 5;
        System.out.println(countDivisor(n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 Program to find number
# of Divisors which on integer
# division produce quotient
# having less set bit than divisor
import math
# Return the count of set bit.
def bit(x) :
    ans = 0
    while (x) :
        x /= 2
        ans = ans + 1

    return ans

# check if q and d have
# same number of set bit.
def check(d, x) :
    if (bit(x /d) <= bit(d)) :
        return True

    return False;

# Binary Search to find
# the point at which
# number of set in q is
# less than or equal to d.
def bs(n) :
    l = 1
    r = int(math.sqrt(n))

    # while left index is less
    # than right index
    while (l < r) :        
        # finding the middle.
        m = int((l + r) / 2)

        # check if q and d have
        # same number of
        # set it or not.
        if (check(m, n)) :
            r = m
        else :
            l = m + 1

    if (check(l, n) == False) :
        return math.floor(l + 1)
    else :
        return math.floor(l)

def countDivisor(n) :
    return n - bs(n) + 1

# Driver Code
n = 5
print (countDivisor(n))

# This code is contributed by
# Manish Shaw (manishshaw1)
```

## C#

```
// C# Program to find number of Divisors
// which on integer division produce quotient
// having less set bit than divisor
using System;
class GFG {

// Return the count of set bit.
static int bit(int x)
{
    int ans = 0;
    while (x > 0) {
        x /= 2;
        ans++;
    }

    return ans;
}

// check if q and d have
// same number of set bit.
static bool check(int d, int x)
{
    if (bit(x / d) <= bit(d))
        return true;

    return false;
}

// Binary Search to find
// the point at which
// number of set in q is
// less than or equal to d.
static int bs(int n)
{
    int l = 1, r = (int)Math.Sqrt(n);

    // while left index is
    // less than right index
    while (l < r) {
        // finding the middle.
        int m = (l + r) / 2;

    // check if q and d have
    // same number of
    // set it or not.
        if (check(m, n))
            r = m;
        else
            l = m + 1;
    }

    if (!check(l, n))
        return l + 1;

    else
        return l;
}

static int countDivisor(int n)
{
    return n - bs(n) + 1;
}

    // Driver Code
    static public void Main ()
    {
        int n = 5;
        Console.WriteLine(countDivisor(n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find number of Divisors
// which on integer division produce quotient
// having less set bit than divisor

// Return the count of set bit.
function bit( $x)
{
    $ans = 0;

    while ($x)
    {
        $x /= 2;
        $ans++;
    }

    return $ans;
}

// check if q and d have
// same number of set bit.
function check( $d, $x)
{
    if (bit($x /$d) <= bit($d))
        return true;

    return false;
}

// Binary Search to find
// the point at which
// number of set in q is
// less than or equal to d.
function bs(int $n)
{
    $l = 1;
    $r = sqrt($n);

    // while left index is less
    // than right index
    while ($l < $r)
    {

        // finding the middle.
        $m = ($l + $r) / 2;

        // check if q and d have
        // same number of
        // set it or not.
        if (check($m, $n))
            $r = $m;
        else
            $l = $m + 1;
    }

    if (!check($l, $n))
        return floor($l + 1);

    else
        return floor($l);
}

function countDivisor( $n)
{
    return $n - bs($n) + 1;
}

    // Driver Code
    $n = 5;
    echo countDivisor($n) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript Program to find number of Divisors
    // which on integer division produce quotient
    // having less set bit than divisor

    // Return the count of set bit.
    function bit(x)
    {
        let ans = 0;
        while (x > 0) {
            x = parseInt(x / 2, 10);
            ans++;
        }

        return ans;
    }

    // check if q and d have
    // same number of set bit.
    function check(d, x)
    {
        if (bit(parseInt(x / d, 10)) <= bit(d))
            return true;

        return false;
    }

    // Binary Search to find
    // the point at which
    // number of set in q is
    // less than or equal to d.
    function bs(n)
    {
        let l = 1, r = Math.sqrt(n);

        // while left index is
        // less than right index
        while (l < r) {
            // finding the middle.
            let m = parseInt((l + r) / 2, 10);

            // check if q and d have
                // same number of
            // set it or not.
            if (check(m, n))
                r = m;
            else
                l = m + 1;
        }

        if (!check(l, n))
            return l + 1;

        else
            return l;
    }

    function countDivisor(n)
    {
        return n - bs(n) + 1;
    }

    let n = 5;
    document.write(countDivisor(n));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(logN)

**辅助空间:** O(1)