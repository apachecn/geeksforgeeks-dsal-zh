# 检查一个数字是否是克里希那穆提数字

> 原文:[https://www . geesforgeks . org/check-if-a-number-is-a-krishnamurthy-number-or-not-2/](https://www.geeksforgeeks.org/check-if-a-number-is-a-krishnamurthy-number-or-not-2/)

克氏数是一个数的阶乘之和等于数本身的数。比如 145，每个数字的阶乘之和:
**1！+ 4!+ 5!= 1 + 24 + 120 = 145**

**示例:**

```
Input : 145
Output : YES
Explanation: 1! + 4! + 5! = 
1 + 24 + 120 = 145, which is equal to input,
hence YES.

Input : 235
Output : NO
Explanation: 2! + 3! + 5! = 
2 + 6 + 120 = 128, which is not equal to input, 
hence NO.
```

想法很简单，我们计算所有数字的阶乘和，然后将和与 n 进行比较。

## C++

```
// C++ program to check if a number
// is a krishnamurthy number
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the factorial of any number
int factorial(int n)
{
    int fact = 1;
    while (n != 0) {
        fact = fact * n;
        n--;
    }
    return fact;
}

// function to Check if number is krishnamurthy
bool isKrishnamurthy(int n)
{
    int sum = 0;

    int temp = n;
    while (temp != 0) {
        // calculate factorial of last digit
        // of temp and add it to sum
        sum += factorial(temp % 10);

        // replace value of temp by temp/10
        temp = temp / 10;
    }

    // Check if number is krishnamurthy
    return (sum == n);
}

// Driver code
int main()
{
    int n = 145;
    if (isKrishnamurthy(n))
        cout << "YES";
    else
        cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a number
// is a krishnamurthy number.
import java.util.*;
import java.io.*;

class Krishnamurthy {
    // function to calculate the factorial
    // of any number
    static int factorial(int n)
    {
        int fact = 1;
        while (n != 0) {
            fact = fact * n;
            n--;
        }
        return fact;
    }

    // function to Check if number is krishnamurthy
    static boolean isKrishnamurthy(int n)
    {
        int sum = 0;

        int temp = n;
        while (temp != 0) {
            // calculate factorial of last digit
            // of temp and add it to sum
            sum += factorial(temp % 10);

            // replace value of temp by temp/10
            temp = temp / 10;
        }

        // Check if number is krishnamurthy
        return (sum == n);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 145;
        if (isKrishnamurthy(n))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}
```

## 蟒蛇 3

```
# Python program to check if a number
# is a krishnamurthy number

# function to calculate the factorial
# of any number
def factorial(n) :
    fact = 1
    while (n != 0) :
        fact = fact * n
        n = n - 1
    return fact

# function to Check if number is
# krishnamurthy/special
def isKrishnamurthy(n) :
    sum = 0
    temp = n
    while (temp != 0) :

        # calculate factorial of last digit
        # of temp and add it to sum
        rem = temp%10
        sum = sum + factorial(rem)

        # replace value of temp by temp / 10
        temp = temp // 10

    # Check if number is krishnamurthy
    return (sum == n)

# Driver code
n = 145
if (isKrishnamurthy(n)) :
    print("YES")
else :
    print("NO")

# This code is contributed by Prashant Aggarwal
```

## C#

```
// C# program to check if a number
// is a krishnamurthy number.
using System;

class GFG {

    // function to calculate the
    // factorial of any number
    static int factorial(int n)
    {
        int fact = 1;

        while (n != 0) {
            fact = fact * n;
            n--;
        }

        return fact;
    }

    // function to Check if number is
    // krishnamurthy
    static bool isKrishnamurthy(int n)
    {
        int sum = 0;

        int temp = n;
        while (temp != 0) {

            // calculate factorial of
            // last digit of temp and
            // add it to sum
            sum += factorial(temp % 10);

            // replace value of temp
            // by temp/10
            temp = temp / 10;
        }

        // Check if number is
        // krishnamurthy
        return (sum == n);
    }

    // Driver code
    public static void Main()
    {
        int n = 145;
        if (isKrishnamurthy(n))
            Console.Write("YES");
        else
            Console.Write("NO");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number
// is a krishnamurthy number

// Function to find Factorial
// of any number
function factorial($n)
{
    $fact = 1;
    while($n != 0)
    {
        $fact = $fact * $n;
        $n--;
    }

    return $fact;
}

// function to Check if number
// is krishnamurthy
function isKrishnamurthyNumber($n)
{
    $sum = 0;

    // Storing the value in
    // other variable
    $temp = $n;

    while($temp != 0)
    {
        // calculate factorial of last digit
        // of temp and add it to sum
        $sum = $sum + factorial($temp % 10);

        // Integer Division
        // replace value of temp by temp/10
        $temp = intdiv($temp, 10);
    }

    // Check if number is krishnamurthy
    return $sum == $n;
}

// Driver code
$n = 145;

if (isKrishnamurthyNumber($n))
    echo "YES";
else
    echo "NO";

// This code is contributed by akash7981
?>
```

## java 描述语言

```
<script>

// Javascript program to check if a number
// is a krishnamurthy number

// Function to find Factorial
// of any number
function factorial(n)
{
    let fact = 1;

    while (n != 0)
    {
        fact = fact * n;
        n--;
    }

    return fact;
}

// Function to check if number
// is krishnamurthy
function isKrishnamurthyNumber(n)
{
    let sum = 0;

    // Storing the value in
    // other variable
    let temp = n;

    while (temp != 0)
    {

        // Calculate factorial of last digit
        // of temp and add it to sum
        sum = sum + factorial(temp % 10);

        // Integer Division
        // replace value of temp by temp/10
        temp = parseInt(temp / 10);
    }

    // Check if number is krishnamurthy
    return sum == n;
}

// Driver code
let n = 145;

if (isKrishnamurthyNumber(n))
    document.write("YES");
else
    document.write("NO");

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
YES
```

有趣的是，我们知道的克里希那穆提数字正好有四个，即 1、2、145 和 40585。

本文由 [**丹麦 KALEEM**](https://www.linkedin.com/in/mohdanishh/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。