# 方程的最小根 x^2+s(x)* x–n = 0，其中 s(x)是根 x 的位数之和。

> 原文:[https://www . geesforgeks . org/minist-root-equation-x2-sxx-n-0-sx-sum-digits-root-x/](https://www.geeksforgeeks.org/smallest-root-equation-x2-sxx-n-0-sx-sum-digits-root-x/)

给你一个整数 n，求方程 x 的最小正整数根，如果找不到根，就打印-1。
方程:x^2+s(x)* x–n = 0
其中 x，n 为正整数，s(x)为函数，等于十进制数制中数字 x 的位数之和。
1 < = N < = 10^18

**示例:**

```
Input: N = 110 
Output: 10 
Explanation: x = 10 is the minimum root. 
             As s(10) = 1 + 0 = 1 and 
             102 + 1*10 - 110=0\.  

Input: N = 4
Output: -1 
Explanation: there are no roots of the 
equation possible
```

一种**天真的方法**将是迭代所有可能的 X 值，并找出是否存在这样的根，但这是不可能的，因为 n 的值非常大。

一个**有效的方法**将如下
首先让我们找到 s(x)的可能值的区间。因此 x^2 < = N 和 N < = 10^18，x < = 109。换句话说，对于每一个可观的解 x，x 的十进制长度不超过 10 位。所以 Smax = s(9999999999) = 10*9 = 90。
让我们暴力破解 s(x)的值(0 < = s(x) < = 90)。现在我们有一个普通的平方方程。交易是求解方程，并检查当前 s(x)的强力值是否等于解的位数总和。如果解存在并且等式成立，我们应该得到答案并存储可能的根的最小值。

下面是上述方法的实现

## C++

```
// CPP program to find smallest value of root
// of an equation under given constraints.
#include <bits/stdc++.h>
using namespace std;

// function to check if the sum of digits is
// equal to the summation assumed
bool check(long long a, long long b)
{
    long long int c = 0;

    // calculate the sum of digit
    while (a != 0) {
        c = c + a % 10;
        a = a / 10;
    }

    return (c == b);
}

// function to find the largest root possible.
long long root(long long n)
{
    bool found = 0;
    long long mx = 1e18;

    // iterate for all possible sum of digits.
    for (long long i = 0; i <= 90; i++) {

        // check if discriminant is a perfect square.
        long long s = i * i + 4 * n;
        long long sq = sqrt(s);

        // check if discriminant is a perfect square and
        // if it as perefect root of the equation
        if (sq * sq == s && check((sq - i) / 2, i)) {
            found = 1;
            mx = min(mx, (sq - i) / 2);
        }
    }

    // function returns answer
    if (found)
        return mx;
    else
        return -1;
}

// driver program to check the above function
int main()
{
    long long n = 110;
    cout << root(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest value of root
// of an equation under given constraints.

class GFG{
// function to check if the sum of digits is
// equal to the summation assumed
static boolean check(long a, long b)
{
    long c = 0;

    // calculate the sum of digit
    while (a != 0) {
        c = c + a % 10;
        a = a / 10;
    }

    return (c == b);
}

// function to find the largest root possible.
static long root(long n)
{
    boolean found = false;
    long mx = (long)1E18;

    // iterate for all possible sum of digits.
    for (long i = 0; i <= 90; i++) {

        // check if discriminant is a perfect square.
        long s = i * i + 4 * n;
        long sq = (long)Math.sqrt(s);

        // check if discriminant is a perfect square and
        // if it as perefect root of the equation
        if (sq * sq == s && check((sq - i) / 2, i)) {
            found = true;
            mx = Math.min(mx, (sq - i) / 2);
        }
    }

    // function returns answer
    if (found)
        return mx;
    else
        return -1;
}

// driver program to check the above function
public static void main(String[] args)
{
    long n = 110;
    System.out.println(root(n));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find smallest
# value of root of an equation
# under given constraints.
import math

# function to check if the sum
# of digits is equal to the
# summation assumed
def check(a, b):
    c = 0;

    # calculate the
    # sum of digit
    while (a != 0):
        c = c + a % 10;
        a = int(a / 10);

    return True if(c == b) else False;

# function to find the
# largest root possible.
def root(n):
    found = False;

    # float(1E+18)
    mx = 1000000000000000001;

    # iterate for all
    # possible sum of digits.
    for i in range(91):

        # check if discriminant
        # is a perfect square.
        s = i * i + 4 * n;
        sq = int(math.sqrt(s));

        # check if discriminant is
        # a perfect square and
        # if it as perefect root
        # of the equation
        if (sq * sq == s and
            check(int((sq - i) / 2), i)):
            found = True;
            mx = min(mx, int((sq-i) / 2));

    # function returns answer
    if (found):
        return mx;
    else:
        return -1;

# Driver Code
n = 110;
print(root(n));

# This code is contributed by mits
```

## C#

```
//C# program to find smallest value of root
// of an equation under given constraints.
using System;
public class GFG{
    // function to check if the sum of digits is
    // equal to the summation assumed
    static bool check(long a, long b)
    {
        long c = 0;

        // calculate the sum of digit
        while (a != 0) {
            c = c + a % 10;
            a = a / 10;
        }

        return (c == b);
    }

    // function to find the largest root possible.
    static long root(long n)
    {
        bool found = false;
        long mx = (long)1E18;

        // iterate for all possible sum of digits.
        for (long i = 0; i <= 90; i++) {

            // check if discriminant is a perfect square.
            long s = i * i + 4 * n;
            long sq = (long)Math.Sqrt(s);

            // check if discriminant is a perfect square and
            // if it as perefect root of the equation
            if (sq * sq == s && check((sq - i) / 2, i)) {
                found = true;
                mx = Math.Min(mx, (sq - i) / 2);
            }
        }

        // function returns answer
        if (found)
            return mx;
        else
            return -1;
    }

    // driver program to check the above function
    public static void Main()
    {
        long n = 110;
        Console.Write(root(n));
    }
}
// This code is contributed by Raput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// smallest value of root
// of an equation under
// given constraints.

// function to check if
// the sum of digits is
// equal to the summation
// assumed
function check($a, $b)
{
    $c = 0;

    // calculate the
    // sum of digit
    while ($a != 0)
    {
        $c = $c + $a % 10;
        $a = (int)($a / 10);
    }

    return ($c == $b) ? true : false;
}

// function to find the
// largest root possible.
function root($n)
{
    $found = false;

    // float(1E+18)
    $mx = 1000000000000000001;

    // iterate for all
    // possible sum of digits.
    for ($i = 0; $i <= 90; $i++)
    {

        // check if discriminant
        // is a perfect square.
        $s = $i * $i + 4 * $n;
        $sq = (int)(sqrt($s));

        // check if discriminant is
        // a perfect square and
        // if it as perefect root
        // of the equation
        if ($sq * $sq == $s &&
            check((int)(($sq - $i) / 2), $i))
        {
            $found = true;
            $mx = min($mx, (int)(($sq -
                                  $i) / 2));
        }
    }

    // function returns answer
    if ($found)
        return $mx;
    else
        return -1;
}

// Driver Code
$n = 110;
echo root($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find smallest
// value of root of an equation under
// given constraints.   

// Function to check if the sum of digits is
// equal to the summation assumed
function check(a, b)
{
    var c = 0;

    // Calculate the sum of digit
    while (a != 0)
    {
        c = c + a % 10;
        a = parseInt(a / 10);
    }

    return (c == b);
}

// Function to find the largest root possible.
function root(n)
{
    var found = false;
    var mx =  1E18;

    // Iterate for all possible
    // sum of digits.
    for(i = 0; i <= 90; i++)
    {

        // Check if discriminant is a
        // perfect square.
        var s = i * i + 4 * n;
        var sq =  Math.sqrt(s);

        // Check if discriminant is a
        // perfect square and if it as
        // perefect root of the equation
        if (sq * sq == s && check((sq - i) / 2, i))
        {
            found = true;
            mx = Math.min(mx, (sq - i) / 2);
        }
    }

    // Function returns answer
    if (found)
        return mx;
    else
        return -1;
}

// Driver code
var n = 110;

document.write(root(n));

// This code is contributed by todaysgaurav

</script>
```

**输出:**

```
10 
```