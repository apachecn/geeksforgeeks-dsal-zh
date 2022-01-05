# 程序查找 2^n 的最后两位数字

> 原文:[https://www . geesforgeks . org/program-to-find-最后两位数-2n/](https://www.geeksforgeeks.org/program-to-find-last-two-digits-of-2n/)

给定一个数字 n，我们需要找到 2 <sup>n</sup> 的最后两位数字。

**示例**:

```
Input : n = 7
Output : 28

Input : n = 72
Output : 96
2^72 = 4722366482869645213696
```

一种天真的方法是迭代地或使用[幂](https://www.geeksforgeeks.org/write-a-c-program-to-calculate-powxn/)函数来寻找 2^n 值。计算出 2^n 值后，找出最后两位数字并打印出来。

**注意:**这种方式只会在一定范围内对 2 <sup>n</sup> 起作用，因为[溢出](https://www.geeksforgeeks.org/check-for-integer-overflow/)发生。

下面是上述方法的实现。

## C++

```
// C++ code to find last 2 digits of 2^n
#include <bits/stdc++.h>
using namespace std;

// Find the first digit
int LastTwoDigit(long long int num)
{
    // Get the last digit from the number
    int one = num % 10;

    // Remove last digit from number
    num /= 10;

    // Get the last digit from
    // the number(last second of num)
    int tens = num % 10;

    // Take last digit to ten's position
    // i.e. last second digit
    tens *= 10;

    // Add the value of ones and tens to
    // make it complete 2 digit number
    num = tens + one;

    // return the first digit
    return num;
}

// Driver program
int main()
{
    int n = 10;
    long long int num = 1;

    // pow function used
    num = pow(2, n);

    cout << "Last " << 2;

    cout << " digits of " << 2;

    cout << "^" << n << " = ";

    cout << LastTwoDigit(num) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find last 2 digits of 2^n

class Geeks {

// Find the first digit
static long LastTwoDigit(long num)
{

    // Get the last digit from the number
    long one = num % 10;

    // Remove last digit from number
    num /= 10;

    // Get the last digit from
    // the number(last second of num)
    long tens = num % 10;

    // Take last digit to ten's position
    // i.e. last second digit
    tens *= 10;

    // Add the value of ones and tens to
    // make it complete 2 digit number
    num = tens + one;

    // return the first digit
    return num;
}

    // Driver code
    public static void main(String args[])
    {
        int n = 10;
        long num = 1;

        // pow function used
        num = (long)Math.pow(2, n);

        System.out.println("Last 2 digits of 2^10 = "
                                 +LastTwoDigit(num));

    }
}

// This code is contributed by ankita_saini
```

## 蟒蛇 3

```
# Python 3 code to find
# last 2 digits of 2^n

# Find the first digit
def LastTwoDigit(num):

    # Get the last digit from the number
    one = num % 10

    # Remove last digit from number
    num //= 10

    # Get the last digit from
    # the number(last second of num)
    tens = num % 10

    # Take last digit to ten's position
    # i.e. last second digit
    tens *= 10

    # Add the value of ones and tens to
    # make it complete 2 digit number
    num = tens + one

    # return the first digit
    return num

# Driver Code
if __name__ == "__main__":
    n = 10
    num = 1

    # pow function used
    num = pow(2, n);

    print("Last " + str(2) + " digits of " +
                    str(2) + "^" + str(n) +
                           " = ", end = "")

    print(LastTwoDigit(num))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# code to find last
// 2 digits of 2^n
using System;

class GFG
{

// Find the first digit
static long LastTwoDigit(long num)
{

    // Get the last digit
    // from the number
    long one = num % 10;

    // Remove last digit
    // from number
    num /= 10;

    // Get the last digit
    // from the number(last
    // second of num)
    long tens = num % 10;

    // Take last digit to
    // ten's position i.e.
    // last second digit
    tens *= 10;

    // Add the value of ones
    // and tens to make it
    // complete 2 digit number
    num = tens + one;

    // return the first digit
    return num;
}

    // Driver code
    public static void Main(String []args)
    {
        int n = 10;
        long num = 1;

        // pow function used
        num = (long)Math.Pow(2, n);

        Console.WriteLine("Last 2 digits of 2^10 = " +
                                   LastTwoDigit(num));
    }
}

// This code is contributed
// by Ankita_Saini
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find last
// 2 digits of 2^n

// Find the first digit
function LastTwoDigit($num)
{
    // Get the last digit
    // from the number
    $one = $num % 10;

    // Remove last digit
    // from number
    $num /= 10;

    // Get the last digit
    // from the number(last
    // second of num)
    $tens = $num % 10;

    // Take last digit to
    // ten's position i.e.
    // last second digit
    $tens *= 10;

    // Add the value of ones
    // and tens to make it
    // complete 2 digit number
    $num = $tens + $one;

    // return the first digit
    return $num;
}

// Driver Code
$n = 10;
$num = 1;

// pow function used
$num = pow(2, $n);

echo ("Last " . 2);

echo (" digits of " . 2);

echo("^" . $n . " = ");

echo( LastTwoDigit($num)) ;

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript code to find last 2 digits of 2^n

// Find the first digit
function LastTwoDigit(num)
{
    // Get the last digit from the number
    let one = num % 10;

    // Remove last digit from number
    num = Math.floor(num/10);

    // Get the last digit from
    // the number(last second of num)
    let tens = num % 10;

    // Take last digit to ten's position
    // i.e. last second digit
    tens *= 10;

    // Add the value of ones and tens to
    // make it complete 2 digit number
    num = tens + one;

    // return the first digit
    return num;
}

// Driver program

    let n = 10;
    let num = 1;

    // pow function used
    num = Math.pow(2, n);

    document.write("Last " + 2);

    document.write(" digits of " + 2);

    document.write("^" + n + " = ");

    document.write(LastTwoDigit(num) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Last 2 digits of 2^10 = 24
```

**高效的方法:**高效的方法是每次乘法后只保留 2 位数字。这个想法与[模幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)中讨论的非常相似，这里讨论了一种通用的方法来寻找(a^b)%c，这里 c 是 10^2，因为只需要最后两位数字。

下面是上述方法的实现。

## C++

```
// C++ code to find last 2 digits of 2^n
#include <iostream>
using namespace std;

/* Iterative Function to calculate (x^y)%p in O(log y) */
int power(long long int x, long long int y, long long int p)
{
    long long int res = 1; // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {

        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// C++ function to calculate
// number of digits in x
int numberOfDigits(int x)
{
    int i = 0;
    while (x) {
        x /= 10;
        i++;
    }
    return i;
}

// C++ function to print last 2 digits of 2^n
void LastTwoDigit(int n)
{
    cout << "Last " << 2;
    cout << " digits of " << 2;
    cout << "^" << n << " = ";

    // Generating 10^2
    int temp = 1;
    for (int i = 1; i <= 2; i++)
        temp *= 10;

    // Calling modular exponentiation
    temp = power(2, n, temp);

    // Printing leftmost zeros. Since (2^n)%2
    // can have digits less then 2\. In that
    // case we need to print zeros
    for (int i = 0; i < 2 - numberOfDigits(temp); i++)
        cout << 0;

    // If temp is not zero then print temp
    // If temp is zero then already printed
    if (temp)
        cout << temp;
}

// Driver program to test above functions
int main()
{
    int n = 72;
    LastTwoDigit(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find last
// 2 digits of 2^n
class GFG
{

/* Iterative Function to
calculate (x^y)%p in O(log y) */
static int power(long x, long y,
                         long p)
{
int res = 1; // Initialize result

x = x % p; // Update x if it is more
           // than or equal to p

while (y > 0)
{

    // If y is odd, multiply
    // x with result
    long r = y & 1;

    if (r == 1)
        res = (res * (int)x) % (int)p;

    // y must be even now
    y = y >> 1; // y = y/2
    x = (x * x) % p;
}
return res;
}

// Java function to calculate
// number of digits in x
static int numberOfDigits(int x)
{
int i = 0;
while (x != 0)
{
    x /= 10;
    i++;
}
return i;
}

// Java function to print
// last 2 digits of 2^n
static void LastTwoDigit(int n)
{
System.out.print("Last " + 2 +
                 " digits of " + 2 + "^");
System.out.print(n +" = ");

// Generating 10^2
int temp = 1;
for (int i = 1; i <= 2; i++)
    temp *= 10;

// Calling modular exponentiation
temp = power(2, n, temp);

// Printing leftmost zeros.
// Since (2^n)%2 can have digits
// less then 2\. In that case
// we need to print zeros
for (int i = 0;
         i < ( 2 - numberOfDigits(temp)); i++)
    System.out.print(0 + " ");

// If temp is not zero then
// print temp. If temp is zero
// then already printed
if (temp != 0)
    System.out.println(temp);
}

// Driver Code
public static void main(String[] args)
{
    int n = 72;
    LastTwoDigit(n);
}
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 code to find
# last 2 digits of 2^n

# Iterative Function to
# calculate (x^y)%p in O(log y)
def power(x, y, p):

    res = 1 # Initialize result

    x = x % p # Update x if it is more
              # than or equal to p

    while (y > 0):

        # If y is odd, multiply
        # x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p

    return res

# function to calculate
# number of digits in x
def numberOfDigits(x):

    i = 0
    while (x):
        x //= 10
        i += 1

    return i

# function to print
# last 2 digits of 2^n
def LastTwoDigit(n):

    print("Last " + str(2) +
          " digits of " + str(2), end = "")
    print("^" + str(n) + " = ", end = "")

    # Generating 10^2
    temp = 1
    for i in range(1, 3):
        temp *= 10

    # Calling modular exponentiation
    temp = power(2, n, temp)

    # Printing leftmost zeros.
    # Since (2^n)%2 can have digits
    # less then 2\. In that case we
    # need to print zeros
    for i in range(2 - numberOfDigits(temp)):
        print(0, end = "")

    # If temp is not zero then print temp
    # If temp is zero then already printed
    if temp:
        print(temp)

# Driver Code
if __name__ == "__main__":
    n = 72
    LastTwoDigit(n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# code to find last
// 2 digits of 2^n
using System;

class GFG
{

/* Iterative Function to calculate
   (x^y)%p in O(log y) */
static int power(long x, long y,
                         long p)
{
int res = 1; // Initialize result

x = x % p; // Update x if it is more
           // than or equal to p

while (y > 0)
{

    // If y is odd, multiply
    // x with result
    long r = y & 1;

    if (r == 1)
        res = (res * (int)x) % (int)p;

    // y must be even now
    y = y >> 1; // y = y/2
    x = (x * x) % p;
}
return res;
}

// C# function to calculate
// number of digits in x
static int numberOfDigits(int x)
{
    int i = 0;
    while (x != 0)
    {
        x /= 10;
        i++;
    }
    return i;
}

// C# function to print
// last 2 digits of 2^n
static void LastTwoDigit(int n)
{
Console.Write("Last " + 2 +
              " digits of " + 2 + "^");
Console.Write(n + " = ");

// Generating 10^2
int temp = 1;
for (int i = 1; i <= 2; i++)
    temp *= 10;

// Calling modular exponentiation
temp = power(2, n, temp);

// Printing leftmost zeros. Since
// (2^n)%2 can have digits less
// then 2\. In that case we need
// to print zeros
for (int i = 0;
         i < ( 2 - numberOfDigits(temp)); i++)
    Console.Write(0 + " ");

// If temp is not zero then print temp
// If temp is zero then already printed
if (temp != 0)
    Console.Write(temp);
}

// Driver Code
public static void Main()
{
    int n = 72;
    LastTwoDigit(n);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find last
// 2 digits of 2^n

/* Iterative Function to
calculate (x^y)%p in O(log y) */
function power($x, $y, $p)
{
    $res = 1; // Initialize result

    $x = $x % $p; // Update x if it
                  // is more than or
                  // equal to p

    while ($y > 0)
    {

        // If y is odd, multiply
        // x with result
        if ($y & 1)
            $res = ($res * $x) % $p;

        // y must be even now
        $y = $y >> 1; // y = y/2
        $x = ($x * $x) % $p;
    }
    return $res;
}

// PHP function to calculate
// number of digits in x
function numberOfDigits($x)
{
    $i = 0;
    while ($x)
    {
        $x /= 10;
        $i++;
    }
    return $i;
}

// PHP function to print
// last 2 digits of 2^n
function LastTwoDigit($n)
{
    echo("Last " . 2);
    echo(" digits of " . 2);
    echo("^" . $n ." = ");

    // Generating 10^2
    $temp = 1;
    for ($i = 1; $i <= 2; $i++)
        $temp *= 10;

    // Calling modular
    // exponentiation
    $temp = power(2, $n, $temp);

    // Printing leftmost zeros.
    // Since (2^n)%2 can have
    // digits less then 2\. In
    // that case we need to
    // print zeros
    for ($i = 0;
         $i < 2 - numberOfDigits($temp); $i++)
        echo (0);

    // If temp is not zero then
    // print temp. If temp is zero
    // then already printed
    if ($temp)
        echo ($temp);
}

// Driver Code
$n = 72;
LastTwoDigit($n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript code to find last
// 2 digits of 2^n

/* Iterative Function to
calculate (x^y)%p in O(log y) */
function power(x, y, p)
{
let res = 1; // Initialize result

x = x % p; // Update x if it is more
           // than or equal to p

while (y > 0)
{

    // If y is odd, multiply
    // x with result
    let r = y & 1;

    if (r == 1)
        res = (res * x) % p;

    // y must be even now
    y = y >> 1; // y = y/2
    x = (x * x) % p;
}
return res;
}

// JavaScript function to calculate
// number of digits in x
function numberOfDigits(x)
{
let i = 0;
while (x != 0)
{
    x /= 10;
    i++;
}
return i;
}

// JavaScript function to print
// last 2 digits of 2^n
function LastTwoDigit(n)
{
document.write("Last " + 2 +
                 " digits of " + 2 + "^");
document.write(n +" = ");

// Generating 10^2
let temp = 1;
for (let i = 1; i <= 2; i++)
    temp *= 10;

// Calling modular exponentiation
temp = power(2, n, temp);

// Printing leftmost zeros.
// Since (2^n)%2 can have digits
// less then 2\. In that case
// we need to print zeros
for (let i = 0;
         i < ( 2 - numberOfDigits(temp)); i++)
    document.write(0 + " ");

// If temp is not zero then
// print temp. If temp is zero
// then already printed
if (temp != 0)
    document.write(temp);
}

// driver program

    let n = 72;
    LastTwoDigit(n);

</script>
```

**Output:** 

```
Last 2 digits of 2^72 = 96
```

**时间复杂度:** O(log n)