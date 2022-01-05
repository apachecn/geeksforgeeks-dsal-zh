# 比较两个分数的程序

> 原文:[https://www . geesforgeks . org/program-compare-two-fractions/](https://www.geeksforgeeks.org/program-compare-two-fractions/)

给定两个分数 a/b 和 c/d，比较它们并打印两者中较大的一个。

**示例:**

```
Input: 5/6, 11/45
Output: 5/6

Input: 4/5 and 2/3
Output: 4/5 
```

我们可以简单地通过分子除以分母将分数转换成浮点值。一旦我们有了对应于每个分数的两个浮点数，我们就可以比较这些数字，并确定哪个分数更大。
但是，由于除法过程中的浮点近似和截断，计算的答案可能不正确。为了得到最准确的答案，我们应该避免使用浮点除法。
要比较两个分数，我们需要使它们的分母相同。我们可以通过将记数器和分母相乘来做到这一点。让我们看看这是如何工作的

```
We have two fractions a/b and c/d.
Let Y = (a/b - c/d) 
      = (ad - bc)/(bd)
Now,
if Y > 0 then a/b > c/d 
if Y = 0 then a/b = c/d
if Y < o then a/b < c/d

Since bd is always positive, the sign of Y depends only on the
numerator (ad-bc). So we need to compute (ad-bc) only.
```

**复杂度:**
由于我们执行两次乘法和一次减法运算，所以答案是在恒定时间内计算的，即 O(1)

## C++

```
// CPP program to find max between
// two Rational numbers
#include <bits/stdc++.h>
using namespace std;

struct Fraction {
    int num, den;
};

// Get max of the two fractions
Fraction maxFraction(Fraction first, Fraction sec)
{
    // Declare nume1 and nume2 for get the value of
    // first numerator and second numerator
    int a = first.num;
    int b = first.den;
    int c = sec.num;
    int d = sec.den;

    // Compute ad-bc
    int Y = a * d - b * c;

    return (Y > 0) ? first : sec;
}

// Driver Code
int main()
{
    Fraction first = { 3, 2 };
    Fraction sec = { 3, 4 };

    Fraction res = maxFraction(first, sec);
    cout << res.num << "/" << res.den;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find max between
// two Rational numbers

import java.io.*;
import java.util.*;

class Fraction {

 int num, den;

//Constructor
Fraction(int n,int d){
    num=n;
    den=d;
}

 // Get max of the two fractions
static Fraction maxFraction(Fraction first, Fraction sec)
{
    // Declare nume1 and nume2 for get the value of
    // first numerator and second numerator
    int a = first.num;
    int b = first.den;
    int c = sec.num;
    int d = sec.den;

    // Compute ad-bc
    int Y = a * d - b * c;

    return (Y > 0) ? first : sec;
}

// Driver function
public static void main (String[] args) {

   Fraction first = new Fraction( 3, 2 );
   Fraction sec = new Fraction( 3, 4 );

    Fraction res = maxFraction(first, sec);
    System.out.println(res.num +"/"+ res.den);

}
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python3 program to find max
# between two Rational numbers

# Get max of the two fractions
def maxFraction(first, sec):

    # Declare nume1 and nume2 for get the value
    # of first numerator and second numerator
    a = first[0]; b = first[1]
    c = sec[0]; d = sec[1]

    # Compute ad-bc
    Y = a * d - b * c

    return first if Y else sec

# Driver Code
first = ( 3, 2 )
sec = ( 3, 4 )
res = maxFraction(first, sec)
print(str(res[0]) + "/" + str(res[1]))

# This code is contributed by Ansu Kumari.
```

## C#

```
// C# program to find max between
// two Rational numbers
using System;

class Fraction {

    int num, den;

    //Constructor
    Fraction(int n,int d)
    {
        num=n;
        den=d;
    }

    // Get max of the two fractions
    static Fraction maxFraction(Fraction first, Fraction sec)
    {
        // Declare nume1 and nume2 for get the value of
        // first numerator and second numerator
        int a = first.num;
        int b = first.den;
        int c = sec.num;
        int d = sec.den;

        // Compute ad-bc
        int Y = a * d - b * c;

        return (Y > 0) ? first : sec;
    }

    // Driver function
    public static void Main ()
    {

        Fraction first = new Fraction( 3, 2 );
        Fraction sec = new Fraction( 3, 4 );

        Fraction res = maxFraction(first, sec);
        Console.WriteLine(res.num +"/"+ res.den);

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find max
// between two Rational numbers

// Get max of the two fractions
function maxFraction($first, $sec)
{

    // Declare nume1 and nume2
    // for get the value of
    // first numerator and second
    // numerator
    $a = $first[0];
    $b = $first[1];
    $c = $sec[0];
    $d = $sec[1];

    // Compute ad-bc
    $Y = $a * $d - $b * $c;

    return ($Y) ? $first : $sec;
}

// Driver Code
$first = array( 3, 2 );
$sec = array ( 3, 4 );
$res = maxFraction($first, $sec);
echo $res[0] . "/" . $res[1];

// This code is contributed
// by mits.
?>
```

## java 描述语言

```
// javascript program to find max
// between two Rational numbers

// Get max of the two fractions
function maxFraction(first, sec) {

    // Declare nume1 and nume2 for get the value
    // of first numerator and second numerator
    a = first[0]; b = first[1]
    c = sec[0]; d = sec[1]

    // Compute ad-bc
    Y = a * d - b * c

    return (Y > 0) ? first : sec;

}

// Driver Code

first = [ 3, 2 ];
sec = [ 3, 4 ];
res = maxFraction(first, sec);

document.write(res[0] + "/" + res[1]);
```

**输出:**

```
3/2
```