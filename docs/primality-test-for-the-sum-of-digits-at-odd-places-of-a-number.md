# 一个数奇数位数字之和的素性检验

> 原文:[https://www . geeksforgeeks . org/primality-数字奇数位数字总和测试/](https://www.geeksforgeeks.org/primality-test-for-the-sum-of-digits-at-odd-places-of-a-number/)

给定一个整数“n”，任务是检查奇数位置(从右到左)的数字总和是否为素数。
如果是质数，则打印“是”或“否”。
**例:**

> **输入:**n = 123
> T3】输出: NO
> As，1 + 3 = 4 不是素数。
> **输入:** n = 42
> **输出:** YES
> 既然，2 是素数。

**逼近:**首先求奇数位即 1，3，5，…(从右开始)的位数之和。
如果总和是质数，则打印“是”，否则打印“否”。
以下是上述办法的实施:

## C++

```
// C++ program to do Primality test
// for the sum of digits at
// odd places of a number

#include <bits/stdc++.h>
using namespace std;

// Function that return sum
// of the digits at odd places
int sum_odd(int n)
{
    int sum = 0, pos = 1;
    while (n) {
        if (pos % 2 == 1)
            sum += n % 10;
        n = n / 10;
        pos++;
    }
    return sum;
}

// Function that returns true
// if the number is prime
// else false
bool check_prime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This condition is checked so that
    // we can skip middle five
    // numbers in the below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Driver code
int main()
{
    int n = 223;

    // Get the sum of the
    // digits at odd places
    int sum = sum_odd(n);

    if (check_prime(sum))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to do Primality test
// for the sum of digits at
// odd places of a number

import java.io.*;

class GFG {
    // Function that return sum
// of the digits at odd places
static int sum_odd(int n)
{
    int sum = 0, pos = 1;
    while (n>0) {
        if (pos % 2 == 1)
            sum += n % 10;
        n = n / 10;
        pos++;
    }
    return sum;
}

// Function that returns true
// if the number is prime
// else false
static boolean check_prime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This condition is checked so that
    // we can skip middle five
    // numbers in the below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Driver code
    public static void main (String[] args) {

    int n = 223;
    // Get the sum of the
    // digits at odd places
    int sum = sum_odd(n);
    if (check_prime(sum))
        System.out.println ("YES" );
    else
        System.out.println("NO");
    }
}
```

## 蟒蛇 3

```
# Python3 program to do Primality test 
# for the sum of digits at 
# odd places of a number

# Function that return sum
# of the digits at odd places
def sum_odd(n):
    sums = 0
    pos = 1
    while (n!=0):
        if (pos % 2 == 1):
            sums += n % 10
        n = n // 10
        pos+=1
    return sums

# Function to check if a
# number is prime

def check_prime(n):
    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

     # This is checked so that we can skip
     # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    for i in range(5,n,6):
        if (n % i == 0 or n % (i + 2) == 0):
            return False
    return True

#driver code
n = 223
# Get the sum of the
# digits at odd places
sums = sum_odd(n)
if (check_prime(sums)):
    print("YES")
else:
    print("NO")

#this code is improved by sahilshelangia
```

## C#

```
// C#  program to do Primality test
// for the sum of digits at
// odd places of a number
using System;

public class GFG{

// Function that return sum
// of the digits at odd places
static int sum_odd(int n)
{
    int sum = 0, pos = 1;
    while (n>0) {
        if (pos % 2 == 1)
            sum += n % 10;
        n = n / 10;
        pos++;
    }
    return sum;
}

// Function that returns true
// if the number is prime
// else false
static bool check_prime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This condition is checked so that
    // we can skip middle five
    // numbers in the below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Driver code

    static public void Main (){
        int n = 223;
    // Get the sum of the
    // digits at odd places
    int sum = sum_odd(n);
    if (check_prime(sum))
        Console.WriteLine("YES" );
    else
            Console.WriteLine("NO");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to do Primality test
// for the sum of digits at odd
// places of a number

// Function that return sum
// of the digits at odd places
function sum_odd($n)
{
    $sum = 0;
    $pos = 1;
    while ($n)
    {
        if ($pos % 2 == 1)
            $sum += $n % 10;
        $n = (int)($n / 10);
        $pos++;
    }
    return $sum;
}

// Function that returns true
// if the number is prime
// else false
function check_prime($n)
{
    // Corner cases
    if ($n <= 1)
        return false;
    if ($n <= 3)
        return true;

    // This condition is checked so
    // that we can skip middle five
    // numbers in the below loop
    if ($n % 2 == 0 || $n % 3 == 0)
        return false;

    for ($i = 5; $i * $i <= $n;
                 $i = ($i + 6))
        if ($n % $i == 0 ||
            $n % ($i + 2) == 0)
            return false;

    return true;
}

// Driver code
$n = 223;

// Get the sum of the
// digits at odd places
$sum = sum_odd($n);

if (check_prime($sum))
    echo "YES";
else
    echo "NO";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to do Primality test
// for the sum of digits at
// odd places of a number

// Function that return sum
// of the digits at odd places
function sum_odd(n)
{
    let sum = 0, pos = 1;
    while (n) {
        if (pos % 2 == 1)
            sum += n % 10;
        n = Math.floor(n / 10);
        pos++;
    }
    return sum;
}

// Function that returns true
// if the number is prime
// else false
function check_prime(n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This condition is checked so that
    // we can skip middle five
    // numbers in the below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (let i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Driver code

    let n = 223;

    // Get the sum of the
    // digits at odd places
    let sum = sum_odd(n);

    if (check_prime(sum))
        document.write("YES" + "<br>");
    else
        document.write("NO" + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
YES
```