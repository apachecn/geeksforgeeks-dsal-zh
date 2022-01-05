# 两个数字中的一个可以很大时的 GCD

> 原文:[https://www . geesforgeks . org/gcd-of-two-numbers-当其中一个可以非常大-2/](https://www.geeksforgeeks.org/gcd-of-two-numbers-when-one-of-them-can-be-very-large-2/)

给定两个数字‘a’和‘b’，使得(0 <= a <= 10^12 and b <= b < 10^250). Find the GCD of two given numbers.
**)示例:**

```
Input: a = 978 
       b = 89798763754892653453379597352537489494736
Output: 6

Input: a = 1221 
       b = 1234567891011121314151617181920212223242526272829
Output: 3
```

**<u>解法:</u>** 在给定的问题中，我们可以看到第一个数字‘a’可以用 long long int 数据类型处理，但是第二个数字‘b’不能用任何 int 数据类型处理。在这里，我们将第二个数字读作一个字符串，我们将通过取它与“a”的模来使它小于和等于“a”。
下面是上述想法的实现。

## C++

```
// C++ program to find GCD of two numbers such that
// the second number can be very large.
#include<bits/stdc++.h>
using namespace std;
typedef long long int ll;

// function to find gcd of two integer numbers
ll gcd(ll a, ll b)
{
    if (!a)
        return b;
    return gcd(b % a, a);
}

// Here 'a' is integer and 'b' is string.
// The idea is to make the second number (represented
// as b) less than and equal to first number by
// calculating its mod with first integer number
// using basic mathematics
ll reduceB(ll a, char b[])
{
    // Initialize result
    ll mod = 0;

    // calculating mod of b with a to make
    // b like 0 <= b < a
    for (int i = 0; i < strlen(b); i++)
        mod = (mod * 10 + b[i] - '0') % a;

    return mod; // return modulo
}

// This function returns GCD of 'a' and 'b'
// where b can be very large and is represented
// as a character array or string
ll gcdLarge(ll a, char b[])
{
    // Reduce 'b' (second number) after modulo with a
    ll num = reduceB(a, b);

    // gcd of two numbers
    return gcd(a, num);
}

// Driver program
int main()
{
    // first number which is integer
    ll a = 0;

    // second number is represented as string because
    // it can not be handled by integer data type
    char b[] = "1234567891011121314151617181920212223242526272829";
    if (a == 0)
        cout << b << endl;
    else
        cout << gcdLarge(a, b) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// GCD of two numbers
// such that the second
// number can be very large.

class GFG
{

    // This function computes
    // the gcd of 2 numbers
    private static int gcd(int reduceNum, int b)
    {
        return b == 0 ?
            reduceNum : gcd(b, reduceNum % b);
    }

    // Here 'a' is integer and 'b'
    // is string. The idea is to make
    // the second number (represented
    // as b) less than and equal to
    // first number by calculating its
    // modulus with first integer
    // number using basic mathematics
    private static int reduceB(int a, String b)
    {
        int result = 0;
        for (int i = 0; i < b.length(); i++)
        {
            result = (result * 10 +
                      b.charAt(i) - '0') % a;
        }
        return result;
    }

    private static int gcdLarge(int a, String b)
    {
        // Reduce 'b' i.e the second
        // number after modulo with a
        int num = reduceB(a, b);

        // Now,use the euclid's algorithm
        // to find the gcd of the 2 numbers
        return gcd(num, a);
    }

    // Driver code
    public static void main(String[] args)
    {
        // First Number which
        // is the integer
        int a = 1221;

        // Second Number is represented
        // as a string because it cannot
        // be represented as an integer
        // data type
        String b = "19837658191095787329";
        if (a == 0)
            System.out.println(b);
        else
            System.out.println(gcdLarge(a, b));
    }

// This code is contributed
// by Tanishq Saluja.
}
```

## 蟒蛇 3

```
# Python3 program to find GCD of
# two numbers such that the second
# number can be very large.

# Function to find gcd
# of two integer numbers
def gcd(a, b) :

    if (a == 0) :
        return b

    return gcd(b % a, a)

# Here 'a' is integer and 'b' is string.
# The idea is to make the second number
# (represented as b) less than and equal
# to first number by calculating its mod
# with first integer number using basic
# mathematics
def reduceB(a, b) :

    # Initialize result
    mod = 0

    # Calculating mod of b with a
    # to make b like 0 <= b < a
    for i in range(0, len(b)) :

        mod = (mod * 10 + ord(b[i])) % a

    return mod      # return modulo

# This function returns GCD of
# 'a' and 'b' where b can be
# very large and is represented
# as a character array or string
def gcdLarge(a, b) :

    # Reduce 'b' (second number)
    # after modulo with a
    num = reduceB(a, b)

    # gcd of two numbers
    return gcd(a, num)

# Driver program

# First number which is integer
a = 1221

# Second number is represented
# as string because it can not
# be handled by integer data type
b = "1234567891011121314151617181920212223242526272829"
if a == 0:
    print(b)
else:
    print(gcdLarge(a, b))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find GCD of
// two numbers such that the
// second number can be very large.
using System;

class GFG
{
// function to find gcd
// of two integer numbers
public long gcd(long a, long b)
{
    if (a == 0)
    return b;
    return gcd(b % a, a);
}

// Here 'a' is integer and
// 'b' is string. The idea
// is to make the second
// number (represented as b)
// less than and equal to
// first number by calculating
// its mod with first integer
// number using basic mathematics
public long reduceB(long a, string b)
{
    // Initialize result
    long mod = 0;

    // calculating mod of
    // b with a to make
    // b like 0 <= b < a
    for (int i = 0; i < b.Length; i++)
        mod = (mod * 10 +
              (b[i] - '0')) % a;

    return mod;
}

// This function returns GCD
// of 'a' and 'b' where b can
// be very large and is
// represented as a character
// array or string
public long gcdLarge(long a, string b)
{
    // Reduce 'b' (second number)
    // after modulo with a
    long num = reduceB(a, b);

    // gcd of two numbers
    return gcd(a, num);
}

// Driver Code
static void Main()
{
    // first number
    // which is integer
    long a = 1221;

    // second number is represented
    // as string because it can not
    // be handled by integer data type
    string b = "1234567891011121314151617181920212223242526272829";
    GFG p = new GFG();
    if (a == 0)
        Console.WriteLine(b);
    else
        Console.WriteLine(p.gcdLarge(a, b));

}
}

// This code is contributed by mits.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find GCD of
// two numbers such that the
// second number can be very large.

// function to find gcd of
// two integer numbers
function gcd($a, $b)
{
    if (!$a)
    return $b;
    return gcd($b % $a, $a);
}

// Here 'a' is integer and 'b'
// is string. The idea is to
// make the second number
// (represented as b) less than
// and equal to first number by
// calculating its mod with first
// integer number using basic mathematics
function reduceB($a, $b)
{
    // Initialize result
    $mod = 0;

    // calculating mod of b with
    // a to make b like 0 <= b < a
    for ($i = 0; $i < strlen($b); $i++)
        $mod = ($mod * 10 +
                $b[$i] - '0') % $a;

    // return modulo
    return $mod;
}

// This function returns GCD of
// 'a' and 'b' where b can be
// very large and is represented
// as a character array or string
function gcdLarge($a, $b)
{
    // Reduce 'b' (second number)
    // after modulo with a
    $num = reduceB($a, $b);

    // gcd of two numbers
    return gcd($a, $num);
}

// Driver Code

// first number which is integer
$a = 1221;

// second number is represented
// as string because it can not
// be handled by integer data type
$b = "1234567891011121314151617181920212223242526272829";

if ($a == 0) {
    echo($b);
}
else {
    echo gcdLarge($a, $b);
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find GCD of two numbers such that
// the second number can be very large.

// function to find gcd of two integer numbers
function gcd( a, b)
{
    if (!a)
       return b;
    return gcd(b%a,a);
}

// Here 'a' is integer and 'b' is string.
// The idea is to make the second number (represented
// as b) less than and equal to first number by
// calculating its mod with first integer number
// using basic mathematics
function reduceB( a,  b)
{
    // Initialize result
    let mod = 0;

    // calculating mod of b with a to make
    // b like 0 <= b < a
    for (let i=0; i<b.length-1; i++)
        mod = (mod*10 + b[i] - '0')%a;

    return mod; // return modulo
}

// This function returns GCD of 'a' and 'b'
// where b can be very large and is represented
// as a character array or string
function gcdLarge( a, b)
{
    // Reduce 'b' (second number) after modulo with a
    let num = reduceB(a, b);

    // gcd of two numbers
    return gcd(a, num);
}

// Driver program
  // first number which is integer
    let a = 1221;

    // second number is represented as string because
    // it can not be handled by integer data type
    let b = "1234567891011121314151617181920212223242526272829";
    if (a == 0)
        document.write( b);
    else
        document.write(gcdLarge(a, b));

// This code contributed by aashish1995

</script>
```

**输出:**

```
3
```

本文由**沙莎克·米什拉(古卢)**供稿。本文由 GeeksforGeeks 团队审阅。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。