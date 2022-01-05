# 位数和差大于 s 的数

> 原文:[https://www . geesforgeks . org/numbers-difference-digital-sum-s/](https://www.geeksforgeeks.org/numbers-difference-digit-sum-s/)

给你两个正整数值 n 和 s，你必须找出从 1 到 n 的整数的总数，这样整数与其数字和的差就大于给定的 s
**例:**

```
Input : n = 20, s = 5
Output :11
Explanation : Integer from 1 to 9 have 
diff(integer - digitSum) = 0 but for 10 to 
20 they have diff(value - digitSum) > 5

Input : n = 20, s = 20
Output : 0
Explanation : Integer from 1 to 20 have diff
(integer - digitSum) >  5
```

解决这个问题的第一个也是最基本的方法是检查从 1 到 n 的所有整数，并检查每个整数的负数字和是否大于 s。这将变得非常耗时，因为我们必须遍历 1 到 n，并且对于每个整数，我们还必须计算数字和。
在转向更好的方法之前，让我们对这个问题及其特点进行一些关键分析:

*   对于最大可能的整数(比如 long long int，即 10^18)，最大可能的数字总和是 9*18(当所有数字都是 9 时)= 162。这意味着在任何情况下，所有大于 s + 162 的整数都满足整数–digitSum > s 的条件。
*   所有小于 s 的整数肯定不能满足给定的条件。
*   十进制范围内的所有整数(0-9，10-19…100-109)都有相同的整数减数字的值。

使用以上三个关键特性，我们可以缩短我们的方法和时间复杂度，只需要迭代 s 到 s+163 个整数。除了检查范围内的所有整数之外，我们只检查每 10 个整数(例如 150、160、170..).
**算法:**

```
// if n < s then return 0
if n<s 
    return 0
else

    // iterate for s to min(n, s+163)
    for i=s to i min(n, s+163)

        // return n-i+1
        if (i-digitSum)>s
            return (n-i+1)

// if no such integer found return 0
return 0
```

## C++

```
// Program to find number of integer such that
// integer - digSum  > s
#include <bits/stdc++.h>
using namespace std;

// function for digit sum
int digitSum(long long int n) {
  int digSum = 0;
  while (n) {
    digSum += n % 10;
    n /= 10;
  }
  return digSum;
}

// function to calculate count of integer s.t.
// integer - digSum > s

long long int countInteger(long long int n,
                          long long int s) {

  // if n < s no integer possible
  if (n < s)
    return 0;

  // iterate for s range and then calculate
  // total count of such integer if starting
  // integer is found
  for (long long int i = s; i <= min(n, s + 163); i++)
    if ((i - digitSum(i)) > s)
      return (n - i + 1);

  // if no integer found return 0
  return 0;
}

// driver program
int main() {
  long long int n = 1000, s = 100;
  cout << countInteger(n, s);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find number of integer
// such that integer - digSum > s
import java.io.*;

class GFG
{
    // function for digit sum
    static int digitSum(long n)
    {
        int digSum = 0;
        while (n > 0)
        {
            digSum += n % 10;
            n /= 10;
        }
        return digSum;
    }

    // function to calculate count of integer s.t.
    // integer - digSum > s
    public static long countInteger(long n, long s)
    {
        // if n < s no integer possible
        if (n < s)
            return 0;

        // iterate for s range and then calculate
        // total count of such integer if starting
        // integer is found
        for (long i = s; i <= Math.min(n, s + 163); i++)
            if ((i - digitSum(i)) > s)
                return (n - i + 1);

        // if no integer found return 0
        return 0;
    }

    // Driver program
    public static void main(String args[])
    {
            long n = 1000, s = 100;
            System.out.println(countInteger(n, s));
    }
}

// This code is contributed by Anshika Goyal.
```

## 蟒蛇 3

```
# Program to find number
# of integer such that
# integer - digSum  > s

# function for digit sum
def digitSum(n):

    digSum = 0

    while (n>0):
        digSum += n % 10
        n //= 10

    return digSum

# function to calculate
# count of integer s.t.
# integer - digSum > s

def countInteger(n, s):

    # if n < s no integer possible
    if (n < s):
        return 0

    # iterate for s range
    # and then calculate
    # total count of such
    # integer if starting
    # integer is found
    for i in range(s,min(n, s + 163)+1):
        if ((i - digitSum(i)) > s):
            return (n - i + 1)

    # if no integer found return 0
    return 0

# driver code
n = 1000
s = 100

print(countInteger(n, s))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# Program to find number of integer
// such that integer - digSum > s
using System;

class GFG
{
    // function for digit sum
    static long digitSum(long n)
    {
        long digSum = 0;

        while (n > 0)
        {
            digSum += n % 10;
            n /= 10;
        }
        return digSum;
    }

    // function to calculate count of integer s.t.
    // integer - digSum > s
    public static long countInteger(long n, long s)
    {
        // if n < s no integer possible
        if (n < s)
            return 0;

        // iterate for s range and then calculate
        // total count of such integer if starting
        // integer is found
        for (long i = s; i <= Math.Min(n, s + 163); i++)
            if ((i - digitSum(i)) > s)
                return (n - i + 1);

        // if no integer found return 0
        return 0;
    }

    // Driver program
    public static void Main()
    {
            long n = 1000, s = 100;
            Console.WriteLine(countInteger(n, s));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find number of integer
// such that integer - digSum > s

// function for digit sum
function digitSum( $n)
{
$digSum = 0;
while ($n)
{
    $digSum += $n % 10;
    $n /= 10;
}
return $digSum;
}

// function to calculate count of
// integer s.t. integer - digSum > s

function countInteger( $n, $s)
{

// if n < s no integer possible
if ($n < $s)
    return 0;

// iterate for s range and then 
// calculate total count of such
// integer if starting integer is found
for ( $i = $s; $i <= min($n, $s + 163); $i++)
    if (($i - digitSum($i)) > $s)
    return ($n - $i + 1);

// if no integer found return 0
return 0;
}

// Driver Code
$n = 1000; $s = 100;
echo countInteger($n, $s);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// JavaScript Program to find number of integer
// such that integer - digSum > s

    // function for digit sum
    function digitSum(n)
    {
        let digSum = 0;
        while (n > 0)
        {
            digSum += n % 10;
            n /= 10;
        }
        return digSum;
    }

    // function to calculate count of integer s.t.
    // integer - digSum > s
    function countInteger(n, s)
    {
        // if n < s no integer possible
        if (n < s)
            return 0;

        // iterate for s range and then calculate
        // total count of such integer if starting
        // integer is found
        for (let i = s; i <= Math.min(n, s + 163); i++)
            if ((i - digitSum(i)) > s)
                return (n - i + 1);

        // if no integer found return 0
        return 0;
    }

// Driver Code

        let n = 1000, s = 100;
        document.write(countInteger(n, s));

// This code is contributed by splevel62.
</script>
```

**输出:**

```
891
```