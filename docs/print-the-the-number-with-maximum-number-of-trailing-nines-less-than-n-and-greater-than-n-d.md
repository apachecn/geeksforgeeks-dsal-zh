# 最大数量，最大尾随 9，小于 N，大于 N-D

> 原文:[https://www . geeksforgeeks . org/print-the-the-number-with-the-number-with-max-number-of-trading-nine-小于 n-且大于 n-d/](https://www.geeksforgeeks.org/print-the-the-number-with-maximum-number-of-trailing-nines-less-than-n-and-greater-than-n-d/)

给定两个数字 **N** 和 **D** 。任务是找出小于或等于 **N** 的最大数字，该数字包含最大数量的尾随 9，N 与该数字的差值不应大于 **D** 。
**举例:**

```
Input: N = 1029, D = 102
Output: 999
1029 has 1 trailing nine while 999 has three 
trailing nine.Also 1029-999 = 30(which is less than 102).

Input: N = 10281, D = 1
Output: 10281
```

一种**天真的方法**将是从 N 迭代到 N-D，并找到尾随 9 数量最多的数字。
一个有效的方法可以通过一些关键的观察发现。这个问题的一个关键观察是，小于 **N** 的最大数字是
，其结尾至少是(**K**9)

> [n – （n MOD 10^k） – 1]

从 N 到 1 的位数总数开始遍历 k 的所有可能值，检查 d >是否为 n% ![10^k    ](img/a740938797f309896daaf1c1662bc018.png "Rendered by QuickLaTeX.com")。如果没有得到这样的值，最终的答案将是 N 本身。否则，使用上面的观察来检查答案。
以下是上述办法的实施情况。

## C++

```
// CPP to implement above function
#include <bits/stdc++.h>
using namespace std;

// It's better to use long long
// to handle big integers
#define ll long long

// function to count no of digits
ll dig(ll a)
{
    ll count = 0;
    while (a > 0) {
        a /= 10;
        count++;
    }
    return count;
}

// function to implement above approach
void required_number(ll num, ll n, ll d)
{
    ll i, j, power, a, flag = 0;
    for (i = num; i >= 1; i--) {
        power = pow(10, i);
        a = n % power;

        // if difference between power
        // and n doesn't exceed d
        if (d > a) {
            flag = 1;
            break;
        }
    }
    if (flag) {
        ll t = 0;

        // loop to build a number from the
        // appropriate no of digits containing only 9
        for (j = 0; j < i; j++) {
            t += 9 * pow(10, j);
        }

        // if the build number is
        // same as original number(n)
        if (n % power == t)
            cout << n;
        else {

            // observation
            cout << n - (n % power) - 1;
        }
    }
    else
        cout << n;
}

// Driver Code
int main()
{
    ll n = 1029, d = 102;

    // variable that stores no of digits in n
    ll num = dig(n);
    required_number(num, n, d);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above function
import java.io.*;

class GFG {

// It's better to use long
// to handle big integers
// function to count no. of digits
static long dig(long a)
{
    long count = 0;
    while (a > 0)
    {
        a /= 10;
        count++;
    }
    return count;
}

// function to implement above approach
 static void required_number(long num, long n, long d)
{
    long i, j, power=1, a, flag = 0;
    for (i = num; i >= 1; i--)
    {
        power = (long)Math.pow(10, i);
        a = n % power;

        // if difference between power
        // and n doesn't exceed d
        if (d > a)
        {
            flag = 1;
            break;
        }
    }

    if (flag>0)
    {
        long t = 0;

        // loop to build a number from the
        // appropriate no of digits containing
        // only 9
        for (j = 0; j < i; j++)
        {
            t += 9 * Math.pow(10, j);
        }

        // if the build number is
        // same as original number(n)
        if (n % power == t)
            System.out.print( n);

        else {

            // observation
            System.out.print( n - (n % power) - 1);
        }
    }
    else
        System.out.print(n);
}

    // Driver Code
    public static void main (String[] args)
    {
        long n = 1029, d = 102;

        // variable that stores no
        // of digits in n
        long num = dig(n);
        required_number(num, n, d);
    }
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 to implement above function

# function to count no of digits
def dig(a):
    count = 0;
    while (a > 0):
        a /= 10
        count+=1
    return count

# function to implement above approach
def required_number(num, n, d):
    flag = 0
    power=0
    a=0
    for i in range(num,0,-1):
        power = pow(10, i)
        a = n % power

        # if difference between power
        # and n doesn't exceed d

        if (d > a):
            flag = 1
            break
    if(flag):
        t=0
        # loop to build a number from the
        # appropriate no of digits containing only 9
        for j in range(0,i):
            t += 9 * pow(10, j)

        # if the build number is
        # same as original number(n)
        if(n % power ==t):
            print(n,end="")
        else:
            # observation
            print((n - (n % power) - 1),end="")
    else:
        print(n,end="")
# Driver Code

if __name__ == "__main__":
    n = 1029
    d = 102

# variable that stores no of digits in n
    num = dig(n)
    required_number(num, n, d)

# this code is contributed by mits
```

## C#

```
// C# code to implement
// above function
using System;

class GFG
{

// It's better to use long
// to handle big integers
// function to count no. of digits
static long dig(long a)
{
    long count = 0;
    while (a > 0)
    {
        a /= 10;
        count++;
    }
    return count;
}

// function to implement
// above approach
static void required_number(long num,
                            long n,
                            long d)
{
    long i, j, power = 1, a, flag = 0;
    for (i = num; i >= 1; i--)
    {
        power = (long)Math.Pow(10, i);
        a = n % power;

        // if difference between power
        // and n doesn't exceed d
        if (d > a)
        {
            flag = 1;
            break;
        }
    }

    if (flag > 0)
    {
        long t = 0;

        // loop to build a number
        // from the appropriate no
        // of digits containing only 9
        for (j = 0; j < i; j++)
        {
            t += (long)(9 * Math.Pow(10, j));
        }

        // if the build number is
        // same as original number(n)
        if (n % power == t)
            Console.Write( n);

        else
        {

            // observation
            Console.Write(n - (n % power) - 1);
        }
    }
    else
        Console.Write(n);
}

    // Driver Code
    public static void Main()
    {
        long n = 1029, d = 102;

        // variable that stores
        // no. of digits in n
        long num = dig(n);
        required_number(num, n, d);
    }
}

// This code is contributed
// by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP to implement above function

// function to count no of digits
function dig($a)
{
    $count = 0;
    while ($a > 0)
    {
        $a = (int)($a / 10);
        $count++;
    }
    return $count;
}

// function to implement above approach
function required_number($num, $n, $d)
{
    $flag = 0;
    for ($i = $num; $i >= 1; $i--)
    {
        $power = pow(10, $i);
        $a = $n % $power;

        // if difference between power
        // and n doesn't exceed d
        if ($d > $a)
        {
            $flag = 1;
            break;
        }
    }
    if ($flag)
    {
        $t = 0;

        // loop to build a number from the
        // appropriate no of digits containing only 9
        for ($j = 0; $j < $i; $j++)
        {
            $t += 9 * pow(10, $j);
        }

        // if the build number is
        // same as original number(n)
        if ($n % $power == $t)
            echo $n;
        else
        {

            // observation
            echo ($n - ($n % $power) - 1);
        }
    }
    else
        echo $n;
}

// Driver Code
$n = 1029;
$d = 102;

// variable that stores no of
// digits in n
$num = dig($n);
required_number($num, $n, $d);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// javascript code to implement above function

// It's better to use var
// to handle big integers
// function to count no. of digits
function dig(a)
{
    var count = 0;
    while (a > 0)
    {
        a /= 10;
        count++;
    }
    return count;
}

// function to implement above approach
 function required_number(num , n , d)
{
    var i, j, power=1, a, flag = 0;
    for (i = num; i >= 1; i--)
    {
        power = Math.pow(10, i);
        a = n % power;

        // if difference between power
        // and n doesn't exceed d
        if (d > a)
        {
            flag = 1;
            break;
        }
    }

    if (flag>0)
    {
        var t = 0;

        // loop to build a number from the
        // appropriate no of digits containing
        // only 9
        for (j = 0; j < i; j++)
        {
            t += 9 * Math.pow(10, j);
        }

        // if the build number is
        // same as original number(n)
        if (n % power == t)
            document.write( n);

        else {

            // observation
            document.write( n - (n % power) - 1);
        }
    }
    else
        document.write(n);
}

    // Driver Code
 var n = 1029, d = 102;

 // variable that stores no
 // of digits in n
 var num = dig(n);
 required_number(num, n, d);

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
999
```

**时间复杂度:** O(位数)