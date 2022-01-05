# 检查一个数字是否为 1 次

> 原文:[https://www . geesforgeks . org/check-what-number-emirpimes-not/](https://www.geeksforgeeks.org/check-whether-number-emirpimes-not/)

给定一个数字“n”，检查它是否是一个整数。

一个**符号(“半素”当向后拼写时)**的定义来源于它的拼写方式。所以，一个素数本身就是一个[半素](https://www.geeksforgeeks.org/check-whether-number-semiprime-not/)(两个素数的乘积)的数，它的数字的反转给出了另一个新的数，它也是一个半素。因此，根据定义，我们可以得出结论，没有一个回文数字可以是反码，因为它们的数字反转不会产生任何新的数字，但会再次形成相同的数字。

**示例:**

> **输入:** 15
> **输出:**是
> **说明:** 15 本身是半素数，因为它是两个素数 3 和 5 的乘积。数字的反转产生了一个新的数字 51，它也是一个半素数，它是两个素数的乘积，即。、3 和 17
> 
> **输入:** 49
> **输出:**是
> **解释:** 49 本身是半素数，因为它是两个素数(不一定截然不同)7 和 7 的乘积。数字的反转产生了一个新的数字 94，它也是一个半素数，它是两个素数的乘积，即。、2 和 47
> 
> **输入:** 25
> **输出:**否
> **说明:** 25 本身是半素数，因为它是两个素数(不一定截然不同)5 和 5 的乘积。其数字的反转给出了一个新的数字 52，它不是半素数，它是三个而不是两个素数的乘积，即。、2、2 和 13

**进场:**

1.  首先检查输入的数字本身是否是半素数。
2.  如果是，通过反转数字形成一个数字。
3.  现在，将这个数字与最初输入的数字进行比较，以确定这个数字是否是回文。
4.  如果这个数不是回文，检查这个新数是否也是半素数。
5.  如果是，则最初输入的数字被报告为一个整数倍。

## C++

```
// CPP code to check whether
// a number is Emirpimes or not
#include <bits/stdc++.h>
using namespace std;

// Checking whether a number
// is semi-prime or not
int checkSemiprime(int num)
{
    int cnt = 0;
    for (int i = 2; cnt < 2 &&
                    i * i <= num; ++i)
    {
        while (num % i == 0)
        {
            num /= i;

            // Increment count of
            // prime numbers
            ++cnt;
        }
    }

    // If number is still greater than 1, after
    // exiting the for loop add it to the count
    // variable as it indicates the number is
    // a prime number
    if (num > 1)
        ++cnt;

    // Return '1' if count is
    // equal to '2' else return '0'
    return cnt == 2;
}

// Checking whether a number
// is emirpimes or not
bool isEmirpimes(int n)
{
    // Number itself is not semiprime.
    if (checkSemiprime(n) == false)
        return false;

    // Finding reverse of n.
    int r = 0;
    for (int t=n; t!=0; t=t/n)
        r = r * 10 + t % 10;

    // The definition of emirpimes excludes
    // palindromes, hence we do not check
    // further, if the number entered is a
    // palindrome
    if (r == n)
        return false;

    // Checking whether the reverse of the
    // semi prime number entered is also
    // a semi prime number or not
    return (checkSemiprime(r));
}

// Driver Code
int main()
{
    int n = 15;
    if (isEmirpimes(n))
    cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to check whether a
// number is Emirpimes or not
import java.io.*;

class GFG
{

    // Checking whether a number
    // is semi-prime or not
    static boolean checkSemiprime(int num)
    {
        int cnt = 0;
        for (int i = 2; cnt < 2 &&
                        i * i <= num; ++i)
        {
            while (num % i == 0)
            {
                num /= i;

                // Increment count of
                // prime numbers
                ++cnt;
            }
        }

        // If number is still greater than 1,
        // after exiting the for loop add it
        // to the count variable as it indicates
        // the number is a prime number
        if (num > 1)
            ++cnt;

        // Return '1' if count is equal
        // to '2' else return '0'
        return cnt == 2;
    }

    // Checking whether a number
    // is emirpimes or not
    static boolean isEmirpimes(int n)
    {
        // Number itself is not semiprime.
        if (checkSemiprime(n) == false)
            return false;

        // Finding reverse of n.
        int r = 0;
        for (int t = n; t != 0; t = t / n)
            r = r * 10 + t % 10;

        // The definition of emirpimes excludes
        // palindromes, hence we do not check
        // further, if the number entered is a
        // palindrome
        if (r == n)
            return false;

        // Checking whether the reverse of the
        // semi prime number entered is also
        // a semi prime number or not
        return (checkSemiprime(r));
    }

    // Driver Code
    public static void main (String[] args)
    {
        int n = 15;
        if (isEmirpimes(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Ajit.
```

## 蟒蛇 3

```
# Python3 code to check whether
# a number is Emirpimesor not

# Checking whether a number
# is semi-prime or not
def checkSemiprime(num):

    cnt = 0;
    i = 2;
    while (cnt < 2 and (i * i) <= num):

        while (num % i == 0):
            num /= i;

            # Increment count of
            # prime numbers
            cnt += 1;
        i += 1;

    # If number is still greater than 1,
    # after exiting the add it to the
    # count variable as it indicates
    # the number is a prime number
    if (num > 1):
        cnt += 1;

    # Return '1' if count is equal
    # to '2' else return '0'
    return cnt == 2;

# Checking whether a number
# is emirpimes or not
def isEmirpimes(n):

    # Number itself is not semiprime.
    if (checkSemiprime(n) == False):
        return False;

    # Finding reverse of n.
    r = 0;
    t = n;
    while (t != 0):
        r = r * 10 + t % 10;
        t = t / n;

    # The definition of emirpimes excludes
    # palindromes, hence we do not check
    # further, if the number entered
    # is a palindrome
    if (r == n):
        return false;

    # Checking whether the reverse of the
    # semi prime number entered is also
    # a semi prime number or not
    return (checkSemiprime(r));

# Driver Code
n = 15;
if (isEmirpimes(n)):
    print("No");
else:
    print("Yes");

# This code is contributed by mits
```

## C#

```
// C# code to check whether a
// number is Emirpimes or not
using System;

class GFG
{

    // Checking whether a number
    // is semi-prime or not
    static bool checkSemiprime(int num)
    {
        int cnt = 0;
        for (int i = 2; cnt < 2 &&
                        i * i <= num; ++i)
        {
            while (num % i == 0)
            {
                num /= i;

                // Increment count of
                // prime numbers
                ++cnt;
            }
        }

        // If number is still greater than 1,
        // after exiting the for loop add it
        // to the count variable as it
        // indicates the number is a prime number
        if (num > 1)
            ++cnt;

        // Return '1' if count is equal
        // to '2' else return '0'
        return cnt == 2;
    }

    // Checking whether a number
    // is emirpimes or not
    static bool isEmirpimes(int n)
    {
        // Number itself is not semiprime.
        if (checkSemiprime(n) == false)
            return false;

        // Finding reverse of n.
        int r = 0;
        for (int t = n; t != 0; t = t / n)
            r = r * 10 + t % 10;

        // The definition of emirpimes excludes
        // palindromes, hence we do not check
        // further, if the number entered is a
        // palindrome
        if (r == n)
            return false;

        // Checking whether the reverse of the
        // semi prime number entered is also
        // a semi prime number or not
        return (checkSemiprime(r));
    }

    // Driver Code
    public static void Main ()
    {
        int n = 15;
        if (isEmirpimes(n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to check whether
// a number is Emirpimesor not

// Checking whether a number
// is semi-prime or not
function checkSemiprime($num)
{
    $cnt = 0;
    for ($i = 2; $cnt < 2 &&
         $i * $i <= $num; ++$i)
    {
        while ($num % $i == 0)
        {
            $num /= $i;

            // Increment count of
            // prime numbers
            ++$cnt;
        }
    }

    // If number is still greater
    // than 1, after exiting the
    // for loop add it to the
    // count variable as it
    // indicates the number is a
    // prime number
    if ($num > 1)
        ++$cnt;

    // Return '1' if count
    // is equal to '2' else
    // return '0'
    return $cnt == 2;
}

// Checking whether a number
// is emirpimes or not
function isEmirpimes($n)
{

    // Number itself is
    // not semiprime.
    if (checkSemiprime($n) == false)
        return false;

    // Finding reverse
    // of n.
    $r = 0;
    for ($t = $n; $t != 0; $t = $t / $n)
         $r = $r * 10 + $t % 10;

    // The definition of emirpimes 
    // excludes palindromes,hence 
    // we do not check further,
    // if the number entered
    // is a palindrome
    if ($r == $n)
        return false;

    // Checking whether the
    // reverse of the
    // semi prime number
    // entered is also
    // a semi prime number
    // or not
    return (checkSemiprime($r));
}

    // Driver Code
    $n = 15;
    if (isEmirpimes($n))

    echo "No";
    else
    echo "Yes";

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript code to check whether a
// number is Emirpimes or not

// Checking whether a number
// is semi-prime or not
function checkSemiprime(num)
{
    let cnt = 0;
    for(let i = 2; cnt < 2 && i * i <= num; ++i)
    {
        while (num % i == 0)
        {
            num = parseInt(num / i, 10);

            // Increment count of
            // prime numbers
            ++cnt;
        }
    }

    // If number is still greater than 1,
    // after exiting the for loop add it
    // to the count variable as it
    // indicates the number is a prime number
    if (num > 1)
        ++cnt;

    // Return '1' if count is equal
    // to '2' else return '0'
    return cnt == 2;
}

// Checking whether a number
// is emirpimes or not
function isEmirpimes(n)
{

    // Number itself is not semiprime.
    if (checkSemiprime(n) == false)
        return false;

    // Finding reverse of n.
    let r = 0;
    for(let t = n;
            t != 0;
            t = parseInt(t / n, 10))
        r = r * 10 + t % 10;

    // The definition of emirpimes excludes
    // palindromes, hence we do not check
    // further, if the number entered is a
    // palindrome
    if (r == n)
        return false;

    // Checking whether the reverse of the
    // semi prime number entered is also
    // a semi prime number or not
    return (checkSemiprime(r));
}

// Driver code
let n = 15;
if (isEmirpimes(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by decode2207

</script>
```

**输出:**

```
Yes
```