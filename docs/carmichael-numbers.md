# 卡迈克尔数字

> 原文:[https://www.geeksforgeeks.org/carmichael-numbers/](https://www.geeksforgeeks.org/carmichael-numbers/)

如果一个数 n 满足以下模算术条件，则称它为卡迈克尔数:

```
  power(b, n-1) MOD n = 1, 
  for all b ranging from 1 to n such that b and 
  n are relatively prime, i.e, gcd(b, n) = 1 
```

给定一个正整数 n，找出它是否是一个卡迈克尔数。这些数字在原始性检验的费马方法中具有重要意义。
**例:**

```
Input :  n = 8
Output : false
Explanation : 8 is not a Carmichael number because 3 is 
              relatively prime to 8 and (38-1) % 8
              = 2187 % 8 is not 1.

Input :  n = 561
Output : true
```

想法很简单，我们迭代从 1 到 n 的所有数字，对于每个相对质数，我们检查它在模 n 下的(n-1)次幂是否为 1。
下面是检查给定号码是否是卡迈克尔的程序。

## C++

```
// A C++ program to check if a number is
// Carmichael or not.
#include <iostream>
using namespace std;

// utility function to find gcd of two numbers
int gcd(int a, int b)
{
    if (a < b)
        return gcd(b, a);
    if (a % b == 0)
        return b;
    return gcd(b, a % b);
}

// utility function to find pow(x, y) under
// given modulo mod
int power(int x, int y, int mod)
{
    if (y == 0)
        return 1;
    int temp = power(x, y / 2, mod) % mod;
    temp = (temp * temp) % mod;
    if (y % 2 == 1)
        temp = (temp * x) % mod;
    return temp;
}

// This function receives an integer n and
// finds if it's a Carmichael number
bool isCarmichaelNumber(int n)
{
    for (int b = 2; b < n; b++) {
        // If "b" is relatively prime to n
        if (gcd(b, n) == 1)

            // And pow(b, n-1)%n is not 1,
            // return false.
            if (power(b, n - 1, n) != 1)
                return false;
    }
    return true;
}

// Driver function
int main()
{
    cout << isCarmichaelNumber(500) << endl;
    cout << isCarmichaelNumber(561) << endl;
    cout << isCarmichaelNumber(1105) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to check if a number is
// Carmichael or not.
import java.io.*;

class GFG {

    // utility function to find gcd of
    // two numbers
    static int gcd(int a, int b)
    {
        if (a < b)
            return gcd(b, a);
        if (a % b == 0)
            return b;
        return gcd(b, a % b);
    }

    // utility function to find pow(x, y)
    // under given modulo mod
    static int power(int x, int y, int mod)
    {
        if (y == 0)
            return 1;
        int temp = power(x, y / 2, mod) % mod;
        temp = (temp * temp) % mod;
        if (y % 2 == 1)
            temp = (temp * x) % mod;
        return temp;
    }

    // This function receives an integer n and
    // finds if it's a Carmichael number
    static int isCarmichaelNumber(int n)
    {
        for (int b = 2; b < n; b++) {
            // If "b" is relatively prime to n
            if (gcd(b, n) == 1)

                // And pow(b, n-1)%n is not 1,
                // return false.
                if (power(b, n - 1, n) != 1)
                    return 0;
        }
        return 1;
    }

    // Driver function
    public static void main(String args[])
    {
        System.out.println(isCarmichaelNumber(500));
        System.out.println(isCarmichaelNumber(561));
        System.out.println(isCarmichaelNumber(1105));
    }
}
// This code is contributed by Nikita Tiwari.
```

## 计算机编程语言

```
# A Python program to check if a number is
# Carmichael or not.

# utility function to find gcd of two numbers
def gcd( a, b) :
    if (a < b) :
        return gcd(b, a)
    if (a % b == 0) :
        return b
    return gcd(b, a % b)

# utility function to find pow(x, y) under
# given modulo mod
def power(x, y, mod) :
    if (y == 0) :
        return 1
    temp = power(x, y / 2, mod) % mod
    temp = (temp * temp) % mod
    if (y % 2 == 1) :
        temp = (temp * x) % mod
    return temp

# This function receives an integer n and
# finds if it's a Carmichael number
def isCarmichaelNumber( n) :
    b = 2
    while b<n :

        # If "b" is relatively prime to n
        if (gcd(b, n) == 1) :

            # And pow(b, n-1)% n is not 1,
            # return false.
            if (power(b, n - 1, n) != 1):
                return 0
        b = b + 1
    return 1

# Driver function
print isCarmichaelNumber(500)
print isCarmichaelNumber(561)
print isCarmichaelNumber(1105)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to check if a number is
// Carmichael or not.
using System;

class GFG {

    // utility function to find gcd of
    // two numbers
    static int gcd(int a, int b)
    {
        if (a < b)
            return gcd(b, a);
        if (a % b == 0)
            return b;
        return gcd(b, a % b);
    }

    // utility function to find pow(x, y)
    // under given modulo mod
    static int power(int x, int y, int mod)
    {
        if (y == 0)
            return 1;

        int temp = power(x, y / 2, mod) % mod;
        temp = (temp * temp) % mod;

        if (y % 2 == 1)
            temp = (temp * x) % mod;

        return temp;
    }

    // This function receives an integer n and
    // finds if it's a Carmichael number
    static int isCarmichaelNumber(int n)
    {
        for (int b = 2; b < n; b++) {
            // If "b" is relatively prime to n
            if (gcd(b, n) == 1)

                // And pow(b, n-1)%n is not 1,
                // return false.
                if (power(b, n - 1, n) != 1)
                    return 0;
        }
        return 1;
    }

    // Driver function
    public static void Main()
    {
        Console.WriteLine(isCarmichaelNumber(500));
        Console.WriteLine(isCarmichaelNumber(561));
        Console.WriteLine(isCarmichaelNumber(1105));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// number is Carmichael or not.

// utility function to find
// gcd of two numbers
function gcd($a, $b)
{
    if ($a < $b)
        return gcd($b, $a);
    if ($a % $b == 0)
        return $b;
    return gcd($b, $a % $b);
}

// utility function to find
// pow(x, y) under given modulo mod
function power($x, $y, $mod)
{
    if ($y == 0)
        return 1;
    $temp = power($x, $y / 2, $mod) % $mod;
    $temp = ($temp * $temp) % $mod;
    if ($y % 2 == 1)
        $temp = ($temp * $x) % $mod;
    return $temp;
}

// This function receives an integer
// n and finds if it's a Carmichael
// number
function isCarmichaelNumber($n)
{
    for ($b = 2; $b <= $n; $b++)
    {
        // If "b" is relatively
        // prime to n
        if (gcd($b, $n) == 1)

            // And pow(b, n - 1) % n
            // is not 1, return false.
            if (power($b, $n - 1, $n) != 1)
                return 0;
    }
    return 1;
}

// Driver Code
echo isCarmichaelNumber(500), " \n";
echo isCarmichaelNumber(561), "\n";
echo isCarmichaelNumber(1105), "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to check if a number is
    // Carmichael or not.

    // utility function to find gcd of
    // two numbers
    function gcd(a, b)
    {
        if (a < b)
            return gcd(b, a);
        if (a % b == 0)
            return b;
        return gcd(b, a % b);
    }

    // utility function to find pow(x, y)
    // under given modulo mod
    function power(x, y, mod)
    {
        if (y == 0)
            return 1;

        let temp = power(x, parseInt(y / 2, 10), mod) % mod;
        temp = (temp * temp) % mod;

        if (y % 2 == 1)
            temp = (temp * x) % mod;

        return temp;
    }

    // This function receives an integer n and
    // finds if it's a Carmichael number
    function isCarmichaelNumber(n)
    {
        for (let b = 2; b < n; b++) {
            // If "b" is relatively prime to n
            if (gcd(b, n) == 1)

                // And pow(b, n-1)%n is not 1,
                // return false.
                if (power(b, n - 1, n) != 1)
                    return 0;
        }
        return 1;
    }

    document.write(isCarmichaelNumber(500) + "</br>");
    document.write(isCarmichaelNumber(561) + "</br>");
    document.write(isCarmichaelNumber(1105));

</script>
```

## C

```
// C Program to find if a number is Carmichael Number
#include<stdio.h>
int gcd(int a, int b)    //Function to find GCD
{
if (a<b)
return gcd(b, a);
if (a % b == 0)
return b;
return gcd(b, a % b);
}

// Function to find pow(x,y) under given modulo mod
int power(int x, int y, int mod)   
{
if (y == 0)
return 1;
int temp = power(x, y / 2, mod) % mod;
temp = (temp * temp) % mod;
if (y % 2 == 1)
temp = (temp * x) % mod;
return temp;
}

//Function to find if received number n is a Carmichael number
int carmichaelnumber(int n)   
{
for (int b=2;b<n;b++)
{
if (gcd(b,n)==1)
if (power(b,n-1,n)!= 1)
{
printf("0");
return 0;
}
}
printf("1");
return 0;
};
int main()
{
carmichaelnumber(500);
printf("\n");
carmichaelnumber(561);
printf("\n");
carmichaelnumber(1105);
return 0;

// This code is contributed by Susobhan Akhuli

}
```

**输出:**

```
0
1
1
```

本文由 [**阿舒托什·库马尔**](https://www.linkedin.com/in/ashutosh-kumar-9527a7105?trk=nav_responsive_tab_profile) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。