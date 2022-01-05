# 检查形成的大数是否能被 41 整除

> 原文:[https://www . geesforgeks . org/check-如果给定了前两位数，则检查数字是否可被 41 整除/](https://www.geeksforgeeks.org/check-if-the-number-is-divisible-by-41-or-not-when-first-two-digits-are-given/)

给定一个大数字*的前两位数字 1* 和*的数字 2* 。还给出了一个数字 *c* 和实际大数字的长度。大数的下一个 n-2 位数字使用公式**数字[i] =(数字[I–1]* c+数字[I–2])% 10**计算。任务是检查形成的数是否能被 41 整除。
**举例:**

```
Input: digit1 = 1  , digit2 = 2  , c = 1  , n = 3
Output: YES
The number formed is 123
which is divisible by 41

Input: digit1 = 1  , digit2 = 4  , c = 6  , n = 3  
Output: NO
```

一种简单的方法是使用给定的公式来形成数字。检查形成的数字是否能被 41 整除，或者不使用%运算符。但是由于数量非常大，不可能存储这么大的数量。
**有效方法:**使用给定的公式计算所有数字，然后使用*乘法*和*加法*的*关联*属性来检查它是否能被 41 整除。一个数是否能被 41 整除意味着(数% 41)是否等于 0。
设 X 为由此形成的大数，可写成。

> X =(数字[0] * 10^n-1) +(数字[1] * 10^n-2) + … +(数字[n-1] * 10^0)
> X =(((数字[0] * 10 +数字[1]) * 10 +数字[2]) * 10 +数字[3]) … ) * 10 +数字[n-1]
> X % 41 =(((((((数字[0] * 10 +数字[1]) % 41) * 10 +数字[2])

因此，计算完所有数字后，遵循以下算法:

1.  将第一个数字初始化为*和*。
2.  迭代所有 n-1 个数字。
3.  使用关联属性通过 **(ans * 10 +数字[i]) % 41** 计算每 i <sup>第</sup>步的 ans。
4.  检查 ans 的最终值，如果它不能被 41 r 整除。

下面是上述方法的实现。

## C++

```
// C++ program to check a large number
// divisible by 41 or not
#include <bits/stdc++.h>
using namespace std;

// Check if a number is divisible by 41 or not
bool DivisibleBy41(int first, int second, int c, int n)
{
    // array to store all the digits
    int digit[n];

    // base values
    digit[0] = first;
    digit[1] = second;

    // calculate remaining digits
    for (int i = 2; i < n; i++)
        digit[i] = (digit[i - 1] * c + digit[i - 2]) % 10;

    // calculate answer
    int ans = digit[0];
    for (int i = 1; i < n; i++)
        ans = (ans * 10 + digit[i]) % 41;

    // check for divisibility
    if (ans % 41 == 0)
        return true;
    else
        return false;
}

// Driver Code
int main()
{

    int first = 1, second = 2, c = 1, n = 3;

    if (DivisibleBy41(first, second, c, n))
        cout << "YES";
    else
        cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// a large number divisible
// by 41 or not
import java.io.*;

class GFG
{
// Check if a number is
// divisible by 41 or not
static boolean DivisibleBy41(int first,
                             int second,
                             int c, int n)
{
    // array to store
    // all the digits
    int digit[] = new int[n];

    // base values
    digit[0] = first;
    digit[1] = second;

    // calculate remaining
    // digits
    for (int i = 2; i < n; i++)
        digit[i] = (digit[i - 1] * c +
                    digit[i - 2]) % 10;

    // calculate answer
    int ans = digit[0];
    for (int i = 1; i < n; i++)
        ans = (ans * 10 +
               digit[i]) % 41;

    // check for
    // divisibility
    if (ans % 41 == 0)
        return true;
    else
        return false;
}

// Driver Code
public static void main (String[] args)
{
    int first = 1, second = 2, c = 1, n = 3;

    if (DivisibleBy41(first, second, c, n))
        System.out.println("YES");
    else
        System.out.println("NO");
}
}

// This code is contributed
// by akt_mit
```

## 蟒蛇 3

```
# Python3 program to check
# a large number divisible
# by 41 or not

# Check if a number is
# divisible by 41 or not
def DivisibleBy41(first,
                  second, c, n):

    # array to store
    # all the digits
    digit = [0] * n

    # base values
    digit[0] = first
    digit[1] = second

    # calculate remaining
    # digits
    for i in range(2,n):
        digit[i] = (digit[i - 1] * c +
                    digit[i - 2]) % 10

    # calculate answer
    ans = digit[0]
    for i in range(1,n):
        ans = (ans * 10 + digit[i]) % 41

    # check for
    # divisibility
    if (ans % 41 == 0):
        return True
    else:
        return False

# Driver Code
first = 1
second = 2
c = 1
n = 3

if (DivisibleBy41(first,
                  second, c, n)):
    print("YES")
else:
    print("NO")

# This code is contributed
# by Smita
```

## C#

```
// C# program to check
// a large number divisible
// by 41 or not
using System;

class GFG
{

// Check if a number is
// divisible by 41 or not
static bool DivisibleBy41(int first,
                          int second,
                          int c, int n)
{
    // array to store
    // all the digits
    int []digit = new int[n];

    // base values
    digit[0] = first;
    digit[1] = second;

    // calculate
    // remaining
    // digits
    for (int i = 2; i < n; i++)
        digit[i] = (digit[i - 1] * c +
                    digit[i - 2]) % 10;

    // calculate answer
    int ans = digit[0];
    for (int i = 1; i < n; i++)
        ans = (ans * 10 +
            digit[i]) % 41;

    // check for
    // divisibility
    if (ans % 41 == 0)
        return true;
    else
        return false;
}

// Driver Code
public static void Main ()
{
    int first = 1,
        second = 2,
        c = 1, n = 3;

    if (DivisibleBy41(first, second, c, n))
        Console.Write("YES");
    else
        Console.Write("NO");
}
}

// This code is contributed
// by Smita
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check a
// large number divisible
// by 41 or not

// Check if a number is
// divisible by 41 or not
function DivisibleBy41($first, $second, $c, $n)
{
    // array to store
    // all the digits
    $digit[$n] = range(1, $n);

    // base values
    $digit[0] = $first;
    $digit[1] = $second;

    // calculate remaining digits
    for ($i = 2; $i < $n; $i++)
        $digit[$i] = ($digit[$i - 1] * $c +
                      $digit[$i - 2]) % 10;

    // calculate answer
    $ans = $digit[0];
    for ($i = 1; $i < $n; $i++)
        $ans = ($ans * 10 + $digit[$i]) % 41;

    // check for divisibility
    if ($ans % 41 == 0)
        return true;
    else
        return false;
}

// Driver Code
$first = 1;
$second = 2;
$c = 1;
$n = 3;

if (DivisibleBy41($first, $second, $c, $n))
    echo "YES";
else
    echo "NO";

// This code is contributed by Mahadev.
?>
```

## java 描述语言

```
<script>

// Javascript program to check
// a large number divisible
// by 41 or not

// Check if a number is
// divisible by 41 or not
function DivisibleBy41(first, second,  c, n)
{
    // array to store
    // all the digits
    let digit = new Array(n).fill(0);

    // base values
    digit[0] = first;
    digit[1] = second;

    // calculate remaining
    // digits
    for (let i = 2; i < n; i++)
        digit[i] = (digit[i - 1] * c +
                    digit[i - 2]) % 10;

    // calculate answer
    let ans = digit[0];
    for (let i = 1; i < n; i++)
        ans = (ans * 10 +
               digit[i]) % 41;

    // check for
    // divisibility
    if (ans % 41 == 0)
        return true;
    else
        return false;
}

// driver program

    let first = 1, second = 2, c = 1, n = 3;

    if (DivisibleBy41(first, second, c, n))
        document.write("YES");
    else
        document.write("NO");

 // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
YES
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)