# 检查一个数字是否是阿基里斯数

> 原文:[https://www . geeksforgeeks . org/check-if-a-number-is-acquires-number-or-not/](https://www.geeksforgeeks.org/check-if-a-number-is-an-achilles-number-or-not/)

给定一个正整数 N，任务是检查 N 是否是阿基里斯数。如果 N 是阿基里斯数，则打印“是”，否则打印“否”。

[**阿喀琉斯数:**](https://en.wikipedia.org/wiki/Achilles_number) 在数学中，阿喀琉斯数是一个强大的数(一个数 n 被称为强大的数，如果它的每一个质因数 p，p <sup>2</sup> 也将其除)但不是[的完美幂](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)。
阿喀琉斯号的前几名是——

> 72、108、200、288、392、432、500、648、675、800、864、968、972、1125、1152、1323

**示例:**

> 输入:72
> 输出:是
> 72 强大到 6 和 36 都除了它，它不是完美的正方形。
> 
> 输入:36
> 输出:否
> 说明:36 是幂数但是完美幂。

**先决条件:**

*   [强大的数字](https://www.geeksforgeeks.org/powerful-number/)

**接近**

1.  检查给定的数字 n 是否是一个强大的数字。要检查一个数字是否有效[参考这个。](https://www.geeksforgeeks.org/powerful-number/)
2.  检查 n 是否是完美幂。要了解检查一个数是否是完美幂的各种方法–[请参考此处。](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-xy-x-raised-to-power-y/)
3.  如果 n 很强大但不完美，那么 n 是一个阿基里斯数
    否则不是。

以下是上述想法的实现。

## C++

```
// Program to check if the given number is
// an Achilles Number
#include <bits/stdc++.h>
using namespace std;

// function to check if the number
// is powerful number
bool isPowerful(int n)
{
    // First divide the number repeatedly by 2
    while (n % 2 == 0) {
        int power = 0;
        while (n % 2 == 0) {
            n /= 2;
            power++;
        }

        // If only 2^1 divides n (not higher powers),
        // then return false
        if (power == 1)
            return false;
    }

    // if n is not a power of 2 then this loop will
    // execute repeat above process
    for (int factor = 3; factor <= sqrt(n); factor += 2) {

        // Find highest power of "factor" that
        // divides n
        int power = 0;
        while (n % factor == 0) {
            n = n / factor;
            power++;
        }

        // If only factor^1 divides n (not higher
        //  powers), then return false
        if (power == 1)
            return false;
    }

    // n must be 1 now if it is not a prime number.
    // Since prime numbers are not powerful, we
    // return false if n is not 1.
    return (n == 1);
}

// Utility function to check if
// number is a perfect power or not
bool isPower(int a)
{
    if (a == 1)
        return true;

    for (int i = 2; i * i <= a; i++) {
        double val = log(a) / log(i);
        if ((val - (int)val) < 0.00000001)
            return true;
    }

    return false;
}

// Function to check Achilles Number
bool isAchillesNumber(int n)
{
    if (isPowerful(n) && !isPower(n))
        return true;
    else
        return false;
}

// Driver Program
int main()
{
    int n = 72;
    if (isAchillesNumber(n))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;

    n = 36;
    if (isAchillesNumber(n))
        cout << "YES" << endl;
    else
        cout << "NO" << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to check if the
// Given number is
// an Achilles Number

class GFG {

    // function to check if the number
    // is powerful number
    static boolean isPowerful(int n)
    {
        // First divide the number repeatedly by 2
        while (n % 2 == 0) {
            int power = 0;
            while (n % 2 == 0) {
                n /= 2;
                power++;
            }

            // If only 2^1 divides n (not higher powers),
            // then return false
            if (power == 1)
                return false;
        }

        // if n is not a power of 2 then this loop
        // will execute repeat above process
        for (int factor = 3; factor <= Math.sqrt(n);
                                      factor += 2) {

            // Find highest power of "factor"
            // that divides n
            int power = 0;
            while (n % factor == 0) {
                n = n / factor;
                power++;
            }

            // If only factor^1 divides n (not higher
            // powers), then return false
            if (power == 1)
                return false;
        }

        // n must be 1 now if it is not a prime number.
        // Since prime numbers are not powerful, we
        // return false if n is not 1.
        return (n == 1);
    }

    // Utility function to check if
    // number is a perfect power or not
    static boolean isPower(int a)
    {
        if (a == 1)
            return true;

        for (int i = 2; i * i <= a; i++) {
            double val = Math.log(a) / Math.log(i);
            if ((val - (int)val) < 0.00000001)
                return true;
        }

        return false;
    }

    // Function to check Achilles Number
    static boolean isAchillesNumber(int n)
    {
        if (isPowerful(n) && !isPower(n))
            return true;
        else
            return false;
    }

    // Driver Program
    public static void main(String[] args)
    {
        int n = 72;
        if (isAchillesNumber(n))
            System.out.println("YES");
        else
            System.out.println("NO");

        n = 36;
        if (isAchillesNumber(n))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}
```

## 蟒蛇 3

```
# Program to check if the given number
# is an Achilles Number
from math import sqrt, log

# function to check if the number
# is powerful number
def isPowerful(n):

    # First divide the number repeatedly by 2
    while (n % 2 == 0):
        power = 0
        while (n % 2 == 0):
            n /= 2
            power += 1

        # If only 2^1 divides n (not higher
        # powers), then return false
        if (power == 1):
            return False

    # if n is not a power of 2 then this
    # loop will execute repeat above process
    p = int(sqrt(n)) + 1
    for factor in range(3, p, 2):

        # Find highest power of "factor"
        # that divides n
        power = 0
        while (n % factor == 0):
            n = n / factor
            power += 1

        # If only factor^1 divides n (not higher
        # powers), then return false
        if (power == 1):
            return False

    # n must be 1 now if it is not a prime number.
    # Since prime numbers are not powerful, we
    # return false if n is not 1.
    return (n == 1)

# Utility function to check if
# number is a perfect power or not
def isPower(a):
    if (a == 1):
        return True

    p = int(sqrt(a)) + 1

    for i in range(2, a, 1):
        val = log(a) / log(i)
        if ((val - int(val)) < 0.00000001):
            return True

    return False

# Function to check Achilles Number
def isAchillesNumber(n):
    if (isPowerful(n) == True and
        isPower(n) == False):
        return True
    else:
        return False

# Driver Code
if __name__ == '__main__':
    n = 72
    if (isAchillesNumber(n)):
        print("YES")
    else:
        print("NO")

    n = 36
    if (isAchillesNumber(n)):
        print("YES")
    else:
        print("NO")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// Program to check if the given number is
// an Achilles Number

using System;
class GFG {

    // function to check if the number
    // is powerful number
    static bool isPowerful(int n)
    {
        // First divide the number repeatedly by 2
        while (n % 2 == 0) {
            int power = 0;
            while (n % 2 == 0) {
                n /= 2;
                power++;
            }

            // If only 2^1 divides n (not higher
            // powers), then return false
            if (power == 1)
                return false;
        }

        // if n is not a power of 2 then this loop
        // will execute repeat above process
        for (int factor = 3; factor <= Math.Sqrt(n);
                                       factor += 2) {

            // Find highest power of "factor" that
            //  divides n
            int power = 0;
            while (n % factor == 0) {
                n = n / factor;
                power++;
            }

            // If only factor^1 divides n (not higher
            //  powers), then return false
            if (power == 1)
                return false;
        }

        // n must be 1 now if it is not a prime number.
        // Since prime numbers are not powerful,
        // we return false if n is not 1.
        return (n == 1);
    }

    // Utility function to check if
    // number is a perfect power or not
    static bool isPower(int a)
    {
        if (a == 1)
            return true;

        for (int i = 2; i * i <= a; i++) {
            double val = Math.Log(a) / Math.Log(i);
            if ((val - (int)val) < 0.00000001)
                return true;
        }

        return false;
    }

    // Function to check Achilles Number
    static bool isAchillesNumber(int n)
    {
        if (isPowerful(n) && !isPower(n))
            return true;
        else
            return false;
    }

    // Driver Program
    public static void Main()
    {
        int n = 72;
        if (isAchillesNumber(n))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");

        n = 36;
        if (isAchillesNumber(n))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to check if the given number
// is an Achilles Number

// Function to check if the number
// is powerful number
function isPowerful($n)
{
    // First divide the number
    // repeatedly by 2
    while ($n % 2 == 0)
    {
        $power = 0;
        while ($n % 2 == 0)
        {
            $n /= 2;
            $power++;
        }

        // If only 2^1 divides n (not higher
        // powers), then return false
        if ($power == 1)
            return false;
    }

    // if n is not a power of 2 then this
    // loop will execute repeat above process
    for ($factor = 3; $factor <= sqrt($n);
                      $factor += 2)
    {

        // Find highest power of "factor"
        // that divides n
        $power = 0;
        while ($n % $factor == 0)
        {
            $n = $n / $factor;
            $power++;
        }

        // If only factor^1 divides n (not
        // higher powers), then return false
        if ($power == 1)
            return false;
    }

    // n must be 1 now if it is not a prime
    // number. Since prime numbers are not
    // powerful, we return false if n is not 1.
    return ($n == 1);
}

// Utility function to check if
// number is a perfect power or not
function isPower($a)
{
    if ($a == 1)
        return true;

    for ($i = 2; $i * $i <= $a; $i++)
    {
        $val = log($a) / log($i);
        if (($val - (int)$val) < 0.00000001)
            return true;
    }

    return false;
}

// Function to check Achilles Number
function isAchillesNumber($n)
{
    if (isPowerful($n) && !isPower($n))
        return true;
    else
        return false;
}

// Driver Code
$n = 72;
if (isAchillesNumber($n))
    echo "YES", "\n" ;
else
    echo "NO", "\n";

$n = 36;
if (isAchillesNumber($n))
echo "YES","\n" ;
else
    echo "NO" ,"\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript Program to check if the
// given number is an Achilles Number

// Function to check if the number
// is powerful number
function isPowerful(n)
{

    // First divide the number
    // repeatedly by 2
    while (n % 2 == 0)
    {
        let power = 0;

        while (n % 2 == 0)
        {
            n = parseInt(n / 2, 10);
            power++;
        }

        // If only 2^1 divides n (not higher
        // powers), then return false
        if (power == 1)
            return false;
    }

    // If n is not a power of 2 then this loop
    // will execute repeat above process
    for(let factor = 3;
            factor <= Math.sqrt(n);
            factor += 2)
    {

        // Find highest power of "factor" that
        //  divides n
        let power = 0;

        while (n % factor == 0)
        {
            n = parseInt(n / factor, 10);
            power++;
        }

        // If only factor^1 divides n (not higher
        //  powers), then return false
        if (power == 1)
            return false;
    }

    // n must be 1 now if it is not a prime number.
    // Since prime numbers are not powerful,
    // we return false if n is not 1.
    return (n == 1);
}

// Utility function to check if
// number is a perfect power or not
function isPower(a)
{
    if (a == 1)
        return true;

    for(let i = 2; i * i <= a; i++)
    {
        let val = Math.log(a) / Math.log(i);

        if ((val - parseInt(val, 10)) < 0.00000001)
            return true;
    }
    return false;
}

// Function to check Achilles Number
function isAchillesNumber(n)
{
    if (isPowerful(n) && !isPower(n))
        return true;
    else
        return false;
}

// Driver code
let n = 72;
if (isAchillesNumber(n))
    document.write("YES" + "</br>");
else
    document.write("NO" + "</br>");

n = 36;
if (isAchillesNumber(n))
    document.write("YES" + "</br>");
else
    document.write("NO" + "</br>");

// This code is contributed by suresh07

</script>
```

**Output:** 

```
YES
NO
```