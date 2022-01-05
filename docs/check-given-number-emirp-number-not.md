# 检查给定的号码是否为 Emirp 号码

> 原文:[https://www . geesforgeks . org/check-given-number-emirp-number-not/](https://www.geeksforgeeks.org/check-given-number-emirp-number-not/)

一个 **Emirp 数**(质数向后拼)是一个质数，当它的十进制数字颠倒时会产生一个不同的质数。这个定义排除了相关的回文素数。
**例:**

```
Input : n = 13
Output : 13 is Emirp!
Explanation :
13 and 31 are both prime numbers. 
Thus, 13 is an Emirp number.

Input : n = 27
Output : 27 is not Emirp.
```

**目的:**输入一个数字，找出这个数字是否是 emirp 数。

**方法:**输入一个数，首先检查它是否是素数。如果数是质数，那么我们找到原数的反数，检查反数是否为质数。如果反数也是质数，那么原数就是 Emirp 数，否则不是。
以下是上述办法的实施情况:。

## C++

```
// C++ program to check if given
// number is Emirp or not.
#include <iostream>
using namespace std;

// Returns true if n is prime.
// Else false.
bool isPrime(int n)
{
    // Corner case
    if (n <= 1)
        return false;

    // Check from 2 to n-1
    for (int i = 2; i < n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function will check whether number
// is Emirp or not
bool isEmirp(int n)
{
    // Check if n is prime
    if (isPrime(n) == false)
        return false;

    // Find reverse of n
    int rev = 0;
    while (n != 0) {
        int d = n % 10;
        rev = rev * 10 + d;
        n /= 10;
    }

    // If both Original and Reverse are Prime,
    // then it is an Emirp number
    return isPrime(rev);
}

// Driver code
int main()
{
    int n = 13; // Input number
    if (isEmirp(n) == true)
        cout << "Yes";
    else
        cout << "No";
}

// This code is contributed by Anant Agarwal.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if given number is
// Emirp or not.
import java.io.*;
class Emirp {
    // Returns true if n is prime. Else
    // false.
    public static boolean isPrime(int n)
    {
        // Corner case
        if (n <= 1)
            return false;

        // Check from 2 to n-1
        for (int i = 2; i < n; i++)
            if (n % i == 0)
                return false;

        return true;
    }

    // Function will check whether number
    // is Emirp or not
    public static boolean isEmirp(int n)
    {
        // Check if n is prime
        if (isPrime(n) == false)
            return false;

        // Find reverse of n
        int rev = 0;
        while (n != 0) {
            int d = n % 10;
            rev = rev * 10 + d;
            n /= 10;
        }

        // If both Original and Reverse are Prime,
        // then it is an Emirp number
        return isPrime(rev);
    }

    // Driver Function
    public static void main(String args[]) throws IOException
    {
        int n = 13; // Input number
        if (isEmirp(n) == true)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}
```

## 蟒蛇 3

```
# Python3 code to check if
# given number is Emirp or not.

# Returns true if n is prime.
# Else false.
def isPrime( n ):

    # Corner case
    if n <= 1:
        return False

    # Check from 2 to n-1
    for i in range(2, n):
        if n % i == 0:
            return False

    return True

# Function will check whether
# number is Emirp or not
def isEmirp( n):

    # Check if n is prime
    n = int(n)
    if isPrime(n) == False:
        return False

        # Find reverse of n
    rev = 0
    while n != 0:
        d = n % 10
        rev = rev * 10 + d
        n = int(n / 10)

    # If both Original and Reverse
    # are Prime, then it is an
    # Emirp number
    return isPrime(rev)

# Driver Function
n = 13 # Input number
if isEmirp(n):
    print("Yes")
else:
    print("No")

# This code is contributed by "Sharad_Bhardwaj".
```

## C#

```
// C# program to check if given
// number is Emirp or not.
using System;

class Emirp {
    // Returns true if n is prime
    // Else false.
    public static bool isPrime(int n)
    {
        // Corner case
        if (n <= 1)
            return false;

        // Check from 2 to n-1
        for (int i = 2; i < n; i++)
            if (n % i == 0)
                return false;

        return true;
    }

    // Function will check whether number
    // is Emirp or not
    public static bool isEmirp(int n)
    {
        // Check if n is prime
        if (isPrime(n) == false)
            return false;

        // Find reverse of n
        int rev = 0;
        while (n != 0) {
            int d = n % 10;
            rev = rev * 10 + d;
            n /= 10;
        }

        // If both Original and Reverse are Prime,
        // then it is an Emirp number
        return isPrime(rev);
    }

    // Driver Function
    public static void Main()
    {
        int n = 13; // Input number
        if (isEmirp(n) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if given
// number is Emirp or not.

// Returns true if n
// is prime else false

function isPrime($n)
{
    // Corner case
    if ($n <= 1)
        return -1;

    // Check from 2 to n-1
    for ($i = 2; $i < $n; $i++)
        if ($n % $i == 0)
            return -1;

    return 1;
}

// Function will check
// whether number is
// Emirp or not
function isEmirp($n)
{
    // Check if n is prime
    if (isPrime($n) == -1)
        return -1;

    // Find reverse of n
    $rev = 0;
    while ($n != 0)
    {
        $d = $n % 10;
        $rev = $rev * 10 + $d;
        $n /= 10;
    }

    // If both Original and
    // Reverse are Prime,
    // then it is an Emirp number
    return isPrime($rev);
}

// Driver code
$n = 13;

if (isEmirp($n) ==-1)
    echo "Yes";
    else
    echo "No";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// javascript program to check if given number is
// Emirp or not.

    // Returns true if n is prime. Else
    // false.
    function isPrime(n)
    {
        // Corner case
        if (n <= 1)
            return false;

        // Check from 2 to n-1
        for (i = 2; i < n; i++)
            if (n % i == 0)
                return false;

        return true;
    }

    // Function will check whether number
    // is Emirp or not
    function isEmirp(n)
    {
        // Check if n is prime
        if (isPrime(n) == false)
            return false;

        // Find reverse of n
        var rev = 0;
        while (n != 0) {
            var d = n % 10;
            rev = rev * 10 + d;
            n = parseInt(n/10);
        }

        // If both Original and Reverse are Prime,
        // then it is an Emirp number
        return isPrime(rev);
    }

    // Driver Function

        var n = 13; // Input number
        if (isEmirp(n) == true)
            document.write("Yes");
        else
            document.write("No");

// This code contributed by Princi Singh
</script>
```

**输出:**

```
Yes
```