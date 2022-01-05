# 仅使用+算术运算符

实现*、–和/运算

> 原文:[https://www . geesforgeks . org/implement-and-operations-only-use-算术运算符/](https://www.geeksforgeeks.org/implement-and-operations-using-only-arithmetic-operator/)

给定两个数字，仅对它们执行乘法、减法和除法运算，仅使用“+”算术运算符。

**可以进行如下操作:**

```
Subtraction :-  a - b = a + (-1)*b.
Multiplication :- a * b = a + a + a ... b times.
Division :- a / b =  continuously subtract b from a and 
                  count how many times we can do that.
```

上面的步骤看起来很简单，但是有点挑战性，因为我们甚至不能用–来减法。

## C++

```
// CPP code to illustrate *, -, / using only
// '+' arithmetic operator
#include <bits/stdc++.h>
using namespace std;

// Function to flip the sign using only "+"
// operator (It is simple with '*' allowed.
// We need to do a = (-1)*a
int flipSign(int a)
{
    int neg = 0;

    // If sign is + ve turn it -ve
    // and vice-versa
    int tmp = a < 0 ? 1 : -1;
    while (a != 0)
    {
        neg += tmp;
        a += tmp;
    }
    return neg;
}

// Check if a and b are of different signs
bool areDifferentSign(int a, int b)
{
    return ((a<0 && b> 0) || (a > 0 && b < 0));
}

// Function to subtract two numbers
// by negating b and adding them
int sub(int a, int b)
{
    // Negating b
    return a + flipSign(b);
}

// Function to multiply a by b by
// adding a to itself b times
int mul(int a, int b)
{
    // because algo is faster if b<a
    if (a < b)
        return mul(b, a);

    // Adding a to itself b times
    int sum = 0;
    for (int i = abs(b); i > 0; i--)
        sum += a;

    // Check if final sign must be -ve or + ve
    if (b < 0)
        sum = flipSign(sum);

    return sum;
}

// Function to divide a by b by counting how many
// times 'b' can be subtracted from 'a' before
// getting 0
int division(int a, int b)
{
    // Raise exception if b is 0
    if (b == 0)
        throw(b);

    int quotient = 0, dividend;

    // Negating b to subtract from a
    int divisor = flipSign(abs(b));

    // Subtracting divisor from dividend
    for (dividend = abs(a); dividend >= abs(divisor);
                                dividend += divisor)
        quotient++;

    // Check if a and b are of similar symbols or not
    if (areDifferentSign(a, b))
        quotient = flipSign(quotient);
    return quotient;
}

// Driver code
int main()
{
    cout << "Subtraction is " << sub(4, -2) << endl;
    cout << "Product is " << mul(-9, 6) << endl;

    try
    {
        cout << "Division is " << division(8, 2);
    }

    catch (int k)
    {
        cout << " Exception :- Divide by 0";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to illustrate *, -, / using only
// '+' arithmetic operator

class GFG{

// Function to flip the sign using only "+"
// operator (It is simple with '*' allowed.
// We need to do a = (-1)*a
static int flipSign(int a)
{
    int neg = 0;

    // If sign is + ve turn it -ve
    // and vice-versa
    int tmp = a < 0 ? 1 : -1;
    while (a != 0)
    {
        neg += tmp;
        a += tmp;
    }
    return neg;
}

// Check if a and b are of different signs
static boolean areDifferentSign(int a, int b)
{
    return ((a < 0 && b > 0) || (a > 0 && b < 0));
}

// Function to subtract two numbers
// by negating b and adding them
static int sub(int a, int b)
{
    // Negating b
    return a + flipSign(b);
}

// Function to multiply a by b by
// adding a to itself b times
static int mul(int a, int b)
{
    // because algo is faster if b<a
    if (a < b)
        return mul(b, a);

    // Adding a to itself b times
    int sum = 0;
    for (int i = Math.abs(b); i > 0; i--)
        sum += a;

    // Check if final sign must be -ve or + ve
    if (b < 0)
        sum = flipSign(sum);

    return sum;
}

// Function to divide a by b by counting 
// how many times 'b' can be subtracted 
// from 'a' before getting 0
static int division(int a, int b)
{
    // Raise exception if b is 0
    if (b == 0)
        throw new ArithmeticException();

    int quotient = 0, dividend;

    // Negating b to subtract from a
    int divisor = flipSign(Math.abs(b));

    // Subtracting divisor from dividend
    for (dividend = Math.abs(a); dividend >= Math.abs(divisor);
         dividend += divisor)
        quotient++;

    // Check if a and b are of similar symbols or not
    if (areDifferentSign(a, b))
        quotient = flipSign(quotient);
    return quotient;
}

// Driver code
public static void main(String[] args)
{
    System.out.println("Subtraction is " + sub(4, -2));
    System.out.println("Product is " + mul(-9, 6));

    try
    {
        System.out.println("Division is " + division(8, 2));
    }

    catch (ArithmeticException e)
    {
        System.out.println("Exception :- Divide by 0");
    }
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 code to illustrate *, -, / using
# only  '+' arithmetic operator

# Function to flip the sign using only "+"
# operator (It is simple with '*' allowed.
# We need to do a = (-1)*a
def flipSign(a):

    neg = 0;

    # If sign is + ve turn it -ve
    # and vice-versa
    tmp = 1 if a < 0 else -1;
    while (a != 0):
        neg += tmp;
        a += tmp;

    return neg;

# Check if a and b are of different signs
def areDifferentSign(a, b):
    return ((a < 0 and b > 0) or
            (a > 0 and b < 0));

# Function to subtract two numbers
# by negating b and adding them
def sub(a, b):

    # Negating b
    return a + flipSign(b);

# Function to multiply a by b by
# adding a to itself b times
def mul(a, b):

    # because algo is faster if b<a
    if (a < b):
        return mul(b, a);

    # Adding a to itself b times
    sum = 0;
    for i in range(abs(b), 0, -1):
        sum += a;

    # Check if final sign must
    # be -ve or + ve
    if (b < 0):
        sum = flipSign(sum);

    return sum;

# Function to divide a by b by counting
# how many times 'b' can be subtracted
# from 'a' before getting 0
def division(a, b):

    quotient = 0;

    # Negating b to subtract from a
    divisor = flipSign(abs(b));

    # Subtracting divisor from dividend
    for dividend in range(abs(a),
                          abs(divisor) + divisor,
                                         divisor):
        quotient += 1;

    # Check if a and b are of similar
    # symbols or not
    if (areDifferentSign(a, b)):
        quotient = flipSign(quotient);
    return quotient;

# Driver code
print("Subtraction is", sub(4, -2));
print("Product is", mul(-9, 6));
a, b = 8, 2;
if(b):
    print("Division is", division(a, b));
else:
    print("Exception :- Divide by 0");

# This code is contributed by mits
```

## C#

```
// C# code to illustrate *, -, / using only
// '+' arithmetic operator
using System;
class GFG
{
// Function to flip the sign using only "+"
// operator (It is simple with '*' allowed.
// We need to do a = (-1)*a
static int flipSign(int a)
{
    int neg = 0;

    // If sign is + ve turn it -ve
    // and vice-versa
    int tmp = a < 0 ? 1 : -1;
    while (a != 0)
    {
        neg += tmp;
        a += tmp;
    }
    return neg;
}

// Check if a and b are of different signs
static bool areDifferentSign(int a, int b)
{
    return ((a < 0 && b > 0) || (a > 0 && b < 0));
}

// Function to subtract two numbers
// by negating b and adding them
static int sub(int a, int b)
{
    // Negating b
    return a + flipSign(b);
}

// Function to multiply a by b by
// adding a to itself b times
static int mul(int a, int b)
{
    // because algo is faster if b<a
    if (a < b)
        return mul(b, a);

    // Adding a to itself b times
    int sum = 0;
    for (int i = Math.Abs(b); i > 0; i--)
        sum += a;

    // Check if final sign must be -ve or + ve
    if (b < 0)
        sum = flipSign(sum);

    return sum;
}

// Function to divide a by b by counting how many
// times 'b' can be subtracted from 'a' before
// getting 0
static int division(int a, int b)
{
    // Raise exception if b is 0
    if (b == 0)
        throw new ArithmeticException();

    int quotient = 0, dividend;

    // Negating b to subtract from a
    int divisor = flipSign(Math.Abs(b));

    // Subtracting divisor from dividend
    for (dividend = Math.Abs(a); dividend >= Math.Abs(divisor);
                                dividend += divisor)
        quotient++;

    // Check if a and b are of similar symbols or not
    if (areDifferentSign(a, b))
        quotient = flipSign(quotient);
    return quotient;
}

// Driver code
public static void Main()
{
    Console.WriteLine("Subtraction is " + sub(4, -2));
    Console.WriteLine("Product is " + mul(-9, 6));
    try
    {
        Console.WriteLine("Division is " + division(8, 2));
    }
    catch (Exception)
    {
        Console.WriteLine("Exception :- Divide by 0");
    }
}
}

//This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to illustrate *, -, / using only
// '+' arithmetic operator

// Function to flip the sign using only "+"
// operator (It is simple with '*' allowed.
// We need to do a = (-1)*a
function flipSign($a)
{
    $neg = 0;

    // If sign is + ve turn it -ve
    // and vice-versa
    $tmp = $a < 0 ? 1 : -1;
    while ($a != 0)
    {
        $neg += $tmp;
        $a += $tmp;
    }
    return $neg;
}

// Check if a and b are of different signs
function areDifferentSign($a, $b)
{
    return (($a < 0 && $b > 0) ||
            ($a > 0 && $b < 0));
}

// Function to subtract two numbers
// by negating b and adding them
function sub($a, $b)
{
    // Negating b
    return $a + flipSign($b);
}

// Function to multiply a by b by
// adding a to itself b times
function mul($a, $b)
{
    // because algo is faster if b<a
    if ($a < $b)
        return mul($b, $a);

    // Adding a to itself b times
    $sum = 0;
    for ($i = abs($b); $i > 0; $i--)
        $sum += $a;

    // Check if final sign must be
    // -ve or + ve
    if ($b < 0)
        $sum = flipSign($sum);

    return $sum;
}

// Function to divide a by b by counting
// how many times 'b' can be subtracted
// from 'a' before getting 0
function division($a, $b)
{
    $quotient = 0;

    // Negating b to subtract from a
    $divisor = flipSign(abs($b));

    // Subtracting divisor from dividend
    for ($dividend = abs($a);
         $dividend >= abs($divisor);
         $dividend += $divisor)
        $quotient++;

    // Check if a and b are of similar
    // symbols or not
    if (areDifferentSign($a, $b))
        $quotient = flipSign($quotient);
    return $quotient;
}

// Driver code
print("Subtraction is " . sub(4, -2) . "\n");
print("Product is " . mul(-9, 6) . "\n");
list($a, $b) = array(8, 2);
if($b)
    print("Division is " . division($a, $b));
else
    print("Exception :- Divide by 0");

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript code to illustrate *, -, / using only
// '+' arithmetic operator   

// Function to flip the sign using only "+"
// operator (It is simple with '*' allowed.
// We need to do a = (-1)*a
function flipSign(a)
{
    var neg = 0;

    // If sign is + ve turn it -ve
    // and vice-versa
    var tmp = a < 0 ? 1 : -1;
    while (a != 0)
    {
        neg += tmp;
        a += tmp;
    }
    return neg;
}

// Check if a and b are of different signs
function areDifferentSign(a , b)
{
    return ((a < 0 && b > 0) || (a > 0 && b < 0));
}

// Function to subtract two numbers
// by negating b and adding them
function sub(a , b)
{
    // Negating b
    return a + flipSign(b);
}

// Function to multiply a by b by
// adding a to itself b times
function mul(a , b)
{
    // because algo is faster if b<a
    if (a < b)
        return mul(b, a);

    // Adding a to itself b times
    var sum = 0;
    for (i = Math.abs(b); i > 0; i--)
        sum += a;

    // Check if final sign must be -ve or + ve
    if (b < 0)
        sum = flipSign(sum);

    return sum;
}

// Function to divide a by b by counting 
// how many times 'b' can be subtracted 
// from 'a' before getting 0
function division(a , b)
{
    // Raise exception if b is 0
    if (b == 0)
        throw new ArithmeticException();

    var quotient = 0, dividend;

    // Negating b to subtract from a
    var divisor = flipSign(Math.abs(b));

    // Subtracting divisor from dividend
    for (dividend = Math.abs(a);
    dividend >= Math.abs(divisor);
         dividend += divisor)
        quotient++;

    // Check if a and b are of similar symbols or not
    if (areDifferentSign(a, b))
        quotient = flipSign(quotient);
    return quotient;
}

// Driver code

document.write("Subtraction is " + sub(4, -2));
document.write("<br>Product is " + mul(-9, 6));

try
{
    document.write("<br>Division is " + division(8, 2));
}

catch (e)
{
    document.write("Exception :- Divide by 0");
}

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
Subtraction is 6
Product is -54
Division is 4
```

**相关文章:**

*   [不使用算术运算符添加两个数字](https://www.geeksforgeeks.org/add-two-numbers-without-using-arithmetic-operators/)
*   [不使用算术运算符减去两个数](https://www.geeksforgeeks.org/subtract-two-numbers-without-using-arithmetic-operators/)
*   [不使用乘法、除法和按位运算符乘法两个整数，不循环](https://www.geeksforgeeks.org/multiply-two-numbers-without-using-multiply-division-bitwise-operators-and-no-loops/)

本文由**萨基提瓦里**供稿。如果你喜欢极客(我们知道你喜欢！)并愿意投稿，也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者将文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。