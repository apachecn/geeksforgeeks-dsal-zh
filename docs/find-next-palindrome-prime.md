# 查找下一个回文素数

> 原文:[https://www.geeksforgeeks.org/find-next-palindrome-prime/](https://www.geeksforgeeks.org/find-next-palindrome-prime/)

找出最小的回文数，它也是质数并且大于给定的数 N.
**举例:**

```
Input : N = 7
Output :11
11 is the smallest palindrome prime which
is greater than N.

Input : N = 112
Output : 131
```

一种简单的方法是从 N+1 开始循环。对于每个数字，检查是否是[回文](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)和[质数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)。
一个**有效的解决方案**是基于以下观察。所有偶数的回文都是 11 的倍数。
我们可以证明如下:
11% 11 = 0
1111% 11 = 0
111111% 11 = 0
1111111% 11 = 0
所以:
1001% 11 =(1111–11 * 10)% 11 = 0
100001% 11 =(11111–11111) % 11 = 0
对于任何偶数位数的回文:
abcdcba % 11
=(a * 10000001+b * 100001 * 10+c * 1001 * 100+d * 11 * 1000)% 11
= 0
所有偶数位数的回文都是 11 的倍数。
所以其中，11 是唯一一个素数
如果(8 < = N < = 11)返回 11
对于其他，我们只考虑奇数位的回文。

## C++

```
// CPP program to find next palindromic
// prime for a given number.
#include <iostream>
#include <string>
using namespace std;

bool isPrime(int num)
{
    if (num < 2 || num % 2 == 0)
        return num == 2;
    for (int i = 3; i * i <= num; i += 2)
        if (num % i == 0)
            return false;
    return true;
}

int primePalindrome(int N)
{
    // if(8<=N<=11) return 11
    if (8 <= N && N <= 11)
        return 11;

    // generate odd length palindrome number
    // which will cover given constraint.
    for (int x = 1; x < 100000; ++x) {

        string s = to_string(x), r(s.rbegin(), s.rend());
        int y = stoi(s + r.substr(1));

        // if y>=N and it is a prime number
        // then return it.
        if (y >= N && isPrime(y))
            return y;
    }

    return -1;
}

// Driver code
int main()
{
    cout << primePalindrome(112);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find next palindromic
// prime for a given number.
import java.lang.*;
class Geeks {

static boolean isPrime(int num)
{
    if (num < 2 || num % 2 == 0)
        return num == 2;
    for (int i = 3; i * i <= num; i += 2)
        if (num % i == 0)
            return false;
    return true;
}

static int primePalindrome(int N)
{
    // if(8<=N<=11) return 11
    if (8 <= N && N <= 11)
        return 11;

    // generate odd length palindrome number
    // which will cover given constraint.
    for (int x = 1; x < 100000; ++x) {

        String s = Integer.toString(x);
        StringBuffer buffer = new StringBuffer(s);
        buffer.reverse();

        int y = Integer.parseInt(s +
        buffer.substring(1).toString());

        // if y>=N and it is a prime number
        // then return it.
        if (y >= N && isPrime(y) == true)
            return y;
    }

    return -1;
}

// Driver code
public static void main(String args[])
{
    System.out.print(primePalindrome(112));

}
}
```

## 蟒蛇 3

```
# Python3 program to find next palindromic
# prime for a given number.
import math as mt

def isPrime(num):

    if (num < 2 or num % 2 == 0):
        return num == 2
    for i in range(3, mt.ceil(mt.sqrt(num + 1))):
        if (num % i == 0):
            return False
    return True

def primePalindrome(N):

    # if(8<=N<=11) return 11
    if (8 <= N and N <= 11):
        return 11

    # generate odd length palindrome number
    # which will cover given constraint.
    for x in range(1, 100000):

        s = str(x)
        d = s[::-1]
        y = int(s + d[1:])

        # if y>=N and it is a prime number
        # then return it.
        if (y >= N and isPrime(y)):
            return y

# Driver code
print(primePalindrome(112))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# program to find next palindromic
// prime for a given number.
using System;
using System.Text;
using System.Collections;

class Geeks {

static bool isPrime(int num)
{
    if (num < 2 || num % 2 == 0)
        return num == 2;
    for (int i = 3; i * i <= num; i += 2)
        if (num % i == 0)
            return false;
    return true;
}

static int primePalindrome(int N)
{
    // if(8<=N<=11) return 11
    if (8 <= N && N <= 11)
        return 11;

    // generate odd length palindrome number
    // which will cover given constraint.
    for (int x = 1; x < 100000; ++x) {

        string s = x.ToString();
        char[] buffer = s.ToCharArray();
        Array.Reverse(buffer);

        int y = Int32.Parse(s + new string(buffer).Substring(1));

        // if y>=N and it is a prime number
        // then return it.
        if (y >= N && isPrime(y) == true)
            return y;
    }

    return -1;
}

// Driver code
public static void Main()
{
    Console.WriteLine(primePalindrome(112));
}
}

// This code is contributed by Mithun Kumar.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find next palindromic
// prime for a given number.

function isPrime($num)
{
    if ($num < 2 || $num % 2 == 0)
        return $num == 2;
    for ($i = 3; $i * $i <= $num; $i += 2)
        if ($num % $i == 0)
            return false;
    return true;
}

function primePalindrome($N)
{
    // if(8<=N<=11) return 11
    if (8 <= $N && $N <= 11)
        return 11;

    // generate odd length palindrome number
    // which will cover given constraint.
    for ($x = 1; $x < 100000; ++$x)
    {
        $s = strval($x);
        $r = strrev($s);
        $y = intval($s.substr($r, 1));

        // if y>=N and it is a prime number
        // then return it.
        if ($y >= $N && isPrime($y) == true)
            return $y;
    }

    return -1;
}

// Driver code
print(primePalindrome(112));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find next palindromic
// prime for a given number.

function isPrime(num)
{
    if (num < 2 || num % 2 == 0)
        return num == 2;
    for (i = 3; i * i <= num; i += 2)
        if (num % i == 0)
            return false;
    return true;
}

function primePalindrome(N)
{
    // if(8<=N<=11) return 11
    if (8 <= N && N <= 11)
        return 11;

    // generate odd length palindrome number
    // which will cover given constraint.
    for (let x = 1; x < 100000; ++x)
    {
        let s = String(x);
        let r = s.split("").reverse().join("");
        let y = parseInt(s + r.substr(1));

        // if y>=N and it is a prime number
        // then return it.
        if (y >= N && isPrime(y) == true)
            return y;
    }

    return -1;
}

// Driver code
document.write(primePalindrome(112));

// This code is contributed by gfgking
</script>
```

**Output:** 

```
131
```