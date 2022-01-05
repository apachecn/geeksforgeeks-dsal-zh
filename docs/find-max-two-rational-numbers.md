# 求两个有理数的最大值

> 原文:[https://www . geesforgeks . org/find-max-two-rational-numbers/](https://www.geeksforgeeks.org/find-max-two-rational-numbers/)

给定两个有理数，任务是找到给定两个有理数的最大值。
示例:

```
Input : first = 3/4, second= 3/2
Output : 3/2

Input : first = 100/100, second = 300/400
Output : 100/100
```

一个简单的解决方案是找到浮点值并比较浮点值。浮点计算可能会导致精度错误。我们可以用下面的方法来避免它们。
说第一个= 3/2，第二个= 3/4

*   首先取(4，2)的一个 [LCM](https://www.geeksforgeeks.org/c-program-find-lcm-two-numbers/) ，它是有理数的分母。所以这个的 LCM 是 4，然后用分母和倍数分别除以第一个和第二个分子，所以分母值是第一个分子= 6，第二个分子= 3。
*   然后找出这两者之间的最大值。所以这里第一个分子是 max，然后打印第一个有理数。

## C++

```
// CPP program to find max between
// two Rational numbers
#include <bits/stdc++.h>
using namespace std;

struct Rational
{
    int nume, deno;
};

// Get lcm of two number's
int lcm(int a, int b)
{
    return (a * b) / (__gcd(a, b));
}

// Get max rational number
Rational maxRational(Rational first, Rational sec)
{
    // Find the LCM of first->denominator
    // and sec->denominator
    int k = lcm(first.deno, sec.deno);

    // Declare nume1 and nume2 for get the value of
    // first numerator and second numerator
    int nume1 = first.nume;
    int nume2 = sec.nume;

    nume1 *= k / (first.deno);
    nume2 *= k / (sec.deno);

    return (nume2 < nume1)? first : sec;
}

// Driver Code
int main()
{
    Rational first = { 3, 2 };
    Rational sec = { 3, 4 };

    Rational res = maxRational(first, sec);
    cout << res.nume << "/" << res.deno;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find max between
// two Rational numbers

class GFG
{

static class Rational
{
    int nume, deno;

    public Rational(int nume, int deno)
    {
        this.nume = nume;
        this.deno = deno;
    }

};

// Get lcm of two number's
static int lcm(int a, int b)
{
    return (a * b) / (__gcd(a, b));
}

// Get max rational number
static Rational maxRational(Rational first, Rational sec)
{
    // Find the LCM of first.denominator
    // and sec.denominator
    int k = lcm(first.deno, sec.deno);

    // Declare nume1 and nume2 for get the value of
    // first numerator and second numerator
    int nume1 = first.nume;
    int nume2 = sec.nume;

    nume1 *= k / (first.deno);
    nume2 *= k / (sec.deno);

    return (nume2 < nume1)? first : sec;
}
static int __gcd(int a, int b)
{
    return b == 0 ? a:__gcd(b, a % b);    
}

// Driver Code
public static void main(String[] args)
{
    Rational first = new Rational(3, 2 );
    Rational sec = new Rational(3, 4 );

    Rational res = maxRational(first, sec);
    System.out.print(res.nume+ "/" + res.deno);
}
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python program to find max between
# two Rational numbers
import math

# Get lcm of two number's
def lcm(a, b):

    return (a * b) // (math.gcd(a, b))

# Get max rational number
def maxRational(first, sec):

    # Find the LCM of first->denominator
    # and sec->denominator
    k = lcm(first[1], sec[1])

    # Declare nume1 and nume2 for get the value of
    # first numerator and second numerator
    nume1 = first[0]
    nume2 = sec[0]

    nume1 *= k // (first[1])
    nume2 *= k // (sec[1])

    return first if (nume2 < nume1) else sec

# Driver Code
first = [3, 2]
sec = [3, 4]
res = maxRational(first, sec)
print(res[0], "/", res[1], sep = "")

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to find max between
// two Rational numbers
using System;

class GFG
{

class Rational
{
    public int nume, deno;

    public Rational(int nume, int deno)
    {
        this.nume = nume;
        this.deno = deno;
    }

};

// Get lcm of two number's
static int lcm(int a, int b)
{
    return (a * b) / (__gcd(a, b));
}

// Get max rational number
static Rational maxRational(Rational first, Rational sec)
{
    // Find the LCM of first.denominator
    // and sec.denominator
    int k = lcm(first.deno, sec.deno);

    // Declare nume1 and nume2 for get the value of
    // first numerator and second numerator
    int nume1 = first.nume;
    int nume2 = sec.nume;

    nume1 *= k / (first.deno);
    nume2 *= k / (sec.deno);

    return (nume2 < nume1)? first : sec;
}
static int __gcd(int a, int b)
{
    return b == 0 ? a:__gcd(b, a % b);    
}

// Driver Code
public static void Main(String[] args)
{
    Rational first = new Rational(3, 2);
    Rational sec = new Rational(3, 4);

    Rational res = maxRational(first, sec);
    Console.Write(res.nume + "/" + res.deno);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JAVASCRIPT program to find max between
// two Rational numbers

class Rational
{
    constructor(nume,deno)
    {
        this.nume = nume;
        this.deno = deno;
    }
}

// Get lcm of two number's
function lcm(a,b)
{
    return (a * b) / (__gcd(a, b));   
}

// Get max rational number
function maxRational(first,sec)
{
    // Find the LCM of first.denominator
    // and sec.denominator
    let k = lcm(first.deno, sec.deno);

    // Declare nume1 and nume2 for get the value of
    // first numerator and second numerator
    let nume1 = first.nume;
    let nume2 = sec.nume;

    nume1 *= k / (first.deno);
    nume2 *= k / (sec.deno);

    return (nume2 < nume1)? first : sec;
}

function __gcd(a,b)
{
    return b == 0 ? a:__gcd(b, a % b);    
}

// Driver Code
let first = new Rational(3, 2 );
let sec = new Rational(3, 4 );

let res = maxRational(first, sec);
document.write(res.nume+ "/" + res.deno);

// This code is contributed by rag2127
</script>
```

**输出:**

```
3/2
```