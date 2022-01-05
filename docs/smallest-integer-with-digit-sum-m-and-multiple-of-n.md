# 数字和为 M 且为 N 倍数的最小整数

> 原文:[https://www . geeksforgeeks . org/最小整数加数字和 n 的倍数/](https://www.geeksforgeeks.org/smallest-integer-with-digit-sum-m-and-multiple-of-n/)

给定两个正整数 N 和 M，任务是找到能被 N 整除且数字和为 M 的最小正整数，如果 int 范围内没有这样的整数，打印 **-1** 。

**示例:**

```
Input: N = 13, M = 32
Output: 8879
8879 is divisible by 13 and its 
Sum of digits of 8879 is 8+8+7+9 = 32 
i.e. equals to M

Input: N = 8, M = 32;
Output: 8888
```

**逼近:**从 N 开始，迭代 N 的所有倍数，检查其位数和是否等于 m。这个问题可以在**日志 <sub>n</sub> (INT_MAX) *日志 <sub>10</sub> (INT_MAX)** 时间解决。这种方法的效率可以通过从一个至少有 m/9 位数的数字开始迭代来提高。

以下是该方法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return digit sum
int digitSum(int n)
{
    int ans = 0;
    while (n) {
        ans += n % 10;
        n /= 10;
    }

    return ans;
}

// Function to find out the smallest integer
int findInt(int n, int m)
{
    int minDigit = floor(m / 9);

    // Start of the iterator (Smallest multiple of n)
    int start = pow(10, minDigit) -
                (int)pow(10, minDigit) % n;

    while (start < INT_MAX) {
        if (digitSum(start) == m)
            return start;
        else
            start += n;
    }
    return -1;
}

// Driver code
int main()
{
    int n = 13, m = 32;
    cout << findInt(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG
{

    // Function to return digit sum
    static int digitSum(int n)
    {
        int ans = 0;
        while (n != 0)
        {
            ans += n % 10;
            n /= 10;
        }

        return ans;
    }

    // Function to find out the
    // smallest integer
    static int findInt(int n, int m)
    {
        int minDigit = (int)Math.floor((double)(m / 9));

        // Start of the iterator (Smallest multiple of n)
        int start = (int)Math.pow(10, minDigit) -
                    (int)Math.pow(10, minDigit) % n;

        while (start < Integer.MAX_VALUE)
        {
            if (digitSum(start) == m)
                return start;
            else
                start += n;
        }
        return -1;
    }

    // Driver code
    static public void main(String args[])
    {
        int n = 13, m = 32;
        System.out.print(findInt(n, m));
    }
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach
from math import floor, pow

import sys

# Function to return digit sum
def digitSum(n):
    ans = 0;
    while (n):
        ans += n % 10;
        n = int(n / 10);

    return ans

# Function to find out the smallest
# integer
def findInt(n, m):
    minDigit = floor(m / 9)

    # Start of the iterator (Smallest
    # multiple of n)
    start = (int(pow(10, minDigit)) -
             int(pow(10, minDigit)) % n)

    while (start < sys.maxsize):
        if (digitSum(start) == m):
            return start
        else:
            start += n
    return -1

# Driver code
if __name__ == '__main__':
    n = 13
    m = 32
    print(findInt(n, m))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return digit sum
    static int digitSum(int n)
    {
        int ans = 0;
        while (n != 0)
        {
            ans += n % 10;
            n /= 10;
        }

        return ans;
    }

    // Function to find out the
    // smallest integer
    static int findInt(int n, int m)
    {
        int minDigit = (int)Math.Floor((double)(m / 9));

        // Start of the iterator (Smallest multiple of n)
        int start = (int)Math.Pow(10, minDigit) -
                    (int)Math.Pow(10, minDigit) % n;

        while (start < int.MaxValue)
        {
            if (digitSum(start) == m)
                return start;
            else
                start += n;
        }
        return -1;
    }

    // Driver code
    static public void Main()
    {
        int n = 13, m = 32;
        Console.WriteLine(findInt(n, m));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP implementation of the above approach
// Function to return digit sum
function digitSum($n)
{
    $ans = 0;
    while ($n)
    {
        $ans += $n % 10;
        $n /= 10;
    }

    return $ans;
}

// Function to find out the smallest integer
function findInt($n, $m)
{
    $minDigit = floor($m / 9);

    // Start of the iterator (Smallest multiple of n)
    $start = pow(10, $minDigit) -
                (int)pow(10, $minDigit) % $n;

    while ($start < PHP_INT_MAX)
    {
        if (digitSum($start) == $m)
            return $start;
        else
            $start += $n;
    }
    return -1;
}

    // Driver code
    $n = 13;
    $m = 32;
    echo findInt($n, $m);

# This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return digit sum
function digitSum(n)
{
    var ans = 0;
    while (n) {
        ans += n % 10;
        n = parseInt(n/10);
    }

    return ans;
}

// Function to find out the smallest integer
function findInt(n, m)
{
    var minDigit = Math.floor(m / 9);

    // Start of the iterator (Smallest multiple of n)
    var start = Math.pow(10, minDigit) -
                Math.pow(10, minDigit) % n;

    while (start < 1000000000) {
        if (digitSum(start) == m)
            return start;
        else
            start += n;
    }
    return -1;
}

// Driver code
var n = 13, m = 32;
document.write( findInt(n, m));

</script>
```

**Output:** 

```
8879
```