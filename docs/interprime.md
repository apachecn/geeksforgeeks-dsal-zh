# 演绎

> 原文:[https://www.geeksforgeeks.org/interprime/](https://www.geeksforgeeks.org/interprime/)

给定一个正数 n，任务是检查给定的数是否为互素。如果给定的数字是“是”，则打印“是”，否则打印“否”。
[**互素**](https://en.wikipedia.org/wiki/Interprime) **:** 在数学中，互素是一个正整数，代表两个连续奇素数的平均值。
前几个 Interprimes 是–
4、6、9、12、15、18、21、26、30、34、39、42、45、50、56、60、64、69、72、76、81、86、93、99
**示例:**

> 输入:12
> 输出:是
> 说明:12 是连续质数 11 和 13 的平均值。
> 输入:20
> 输出:否

这个问题的一个**简单的解决方法**是生成素数，并检查我们是否可以从连续的奇数素数中得到给定的平均值。
**进场:**

1.  从 i=3 到素数 p > n 开始生成素数“p”
2.  如果我们找到 p 和 p+1 的平均值作为给定的数字 n，那么停止并打印“是”

3.  如果我们没有找到这样的 p 和 p+1 与给定的平均打印“否”。

一个**有效的解决方法**是只检查素数 p1 和 p2 的平均值，这样 p1 和 p2 是连续的，p1 < n < p2。
**进场:**

1.  计算连续的素数 p1 和 p2。使得 p1 < n < p2. 

2.  计算 p1 和 p2 的平均值。

3.  如果我们得到给定的平均值，则打印“是”，否则打印“否”。

## C++

```
// CPP program to check if a number is
// interprime  or not

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number is prime or not
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6) {
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }

    return true;
}

// Function to check
// if the given number is interprime or not
bool isInterprime(int n)
{

    // Smallest Interprime is 4
    // So the number less than 4
    // can not be a Interprime

    if (n < 4)
        return false;

    int prev_prime = n;
    int next_prime = n;

    // Calculate first prime number < n
    while (!isPrime(prev_prime)) {
        prev_prime--;
    }

    // Calculate first prime number > n
    while (!isPrime(next_prime)) {
        next_prime++;
    }

    // Check if prev_prime and next_prime
    // have the same average
    if ((prev_prime + next_prime) == 2 * n)
        return true;
    else
        return false;
}

int main()
{
    int n = 9;
    if (isInterprime(n))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to check if a number is
// interprime  or not

class GFG {
    // Function to check if a number is prime or not
    static boolean isPrime(int n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6) {
            if (n % i == 0 || n % (i + 2) == 0) {
                return false;
            }
        }
        return true;
    }

    // Function to check
    // if the given number is interprime or not
    static boolean isInterprime(int n)
    {

        // Smallest Interprime is 4
        // So the number less than 4
        // can not be a Interprime

        if (n < 4)
            return false;

        int prev_prime = n;
        int next_prime = n;

        // Calculate first prime number < n
        while (!isPrime(prev_prime)) {
            prev_prime--;
        }

        // Calculate first prime number > n
        while (!isPrime(next_prime)) {
            next_prime++;
        }

        // check if next_prime and prev_prime
        // have the same average
        if ((prev_prime + next_prime) == 2 * n)
            return true;
        else
            return false;
    }

    public static void main(String[] args)
    {

        int n = 9;
        if (isInterprime(n))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}
```

## 蟒蛇 3

```
# Python 3 program to check if a number is  
# interprime  or not 

# Utility function to check 
# if a number is prime or not 
def isPrime(n) :  

    # Corner cases  
    if (n <= 1) :  
        return False
    if (n <= 3) :  
        return True

    # This is checked so that we can skip  
    # middle five numbers in below loop  
    if (n % 2 == 0 or n % 3 == 0) :  
        return False

    i = 5
    while (i * i <= n) :  
        if (n % i == 0 or n % (i + 2) == 0) :  
            return False
        i = i + 6

    return True

# Function to check
# if the given number is interprime or not
def isInterprime( n):

     # Smallest Interprime is 4
     # So the number less than 4
     # can not be a Interprime

     if (n < 4):
        return False

     prev_prime = n
     next_prime = n

     # Calculate first prime number < n
     while (isPrime(prev_prime)== 0):
         prev_prime = prev_prime-1

     # Calculate first prime number > n
     while (isPrime(next_prime)== 0):
         next_prime = next_prime + 1

     # check if next_prime and prev_prime
     # have the same average
     if ((prev_prime + next_prime)== 2 * n):
         return True
     else:
        return False   

n = 9
if(isInterprime(n)):
    print("YES")
else:
    print("NO")
```

## C#

```
// C# program to check if a number is
// interprime  or not

using System;
class GFG {
    // Function to check if a number is prime or not
    static bool isPrime(int n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (int i = 5; i * i <= n; i = i + 6) {
            if (n % i == 0 || n % (i + 2) == 0) {
                return false;
            }
        }
        return true;
    }

    // Function to check
    // if the given number is interprime or not
    static bool isInterprime(int n)
    {

        // Smallest Interprime is 4
        // So the number less than 4
        // can not be a Interprime

        if (n < 4)
            return false;

        int prev_prime = n;
        int next_prime = n;

        // Calculate first prime number < n
        while (!isPrime(prev_prime)) {
            prev_prime--;
        }

        // Calculate first prime number > n
        while (!isPrime(next_prime)) {
            next_prime++;
        }

        // check if next_prime and prev_prime
        // have the same average
        if ((prev_prime + next_prime) == 2 * n)
            return true;
        else
            return false;
    }

    public static void Main()
    {

        int n = 9;
        if (isInterprime(n))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a
// number is interprime or not

// Function to check if a
// number is prime or not
function isPrime($n)
{
    // Corner cases
    if ($n <= 1)
        return false;
    if ($n <= 3)
        return true;

    // This is checked so that we
    // can skip middle five numbers
    // in below loop
    if ($n % 2 == 0 or $n % 3 == 0)
        return false;

    for ($i = 5;
         $i * $i <= $n; $i = $i + 6)
    {
        if ($n % $i == 0 or
            $n % ($i + 2) == 0)
        {
            return false;
        }
    }

    return true;
}

// Function to check if the
// given number is interprime or not
function isInterprime($n)
{

    // Smallest Interprime is 4
    // So the number less than 4
    // can not be a Interprime

    if ($n < 4)
        return false;

    $prev_prime = $n;
    $next_prime = $n;

    // Calculate first prime
    // number < n
    while (!isPrime($prev_prime))
    {
        $prev_prime--;
    }

    // Calculate first prime
    // number > n
    while (!isPrime($next_prime))
    {
        $next_prime++;
    }

    // Check if prev_prime and
    // next_prime have the same average
    if (($prev_prime +
         $next_prime) == 2 * $n)
        return true;
    else
        return false;
}

// Driver Code
$n = 9;
if (isInterprime($n))
    echo "YES";
else
    echo "NO";

// This code is contributed
// by Shashank
?>
```

## java 描述语言

```
<script>

// Javascript program to check if a number is
// interprime  or not

// Function to check if a number is prime or not
function isPrime(n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (var i = 5; i * i <= n; i = i + 6) {
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }

    return true;
}

// Function to check
// if the given number is interprime or not
function isInterprime(n)
{

    // Smallest Interprime is 4
    // So the number less than 4
    // can not be a Interprime

    if (n < 4)
        return false;

    var prev_prime = n;
    var next_prime = n;

    // Calculate first prime number < n
    while (!isPrime(prev_prime)) {
        prev_prime--;
    }

    // Calculate first prime number > n
    while (!isPrime(next_prime)) {
        next_prime++;
    }

    // Check if prev_prime and next_prime
    // have the same average
    if ((prev_prime + next_prime) == 2 * n)
        return true;
    else
        return false;
}

var n = 9;
if (isInterprime(n))
    document.write( "YES");
else
    document.write( "NO");

// This code is contributed by noob2000.
</script>
```

**输出:**

```
YES
```