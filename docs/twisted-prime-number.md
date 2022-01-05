# 扭曲质数

> 原文:[https://www.geeksforgeeks.org/twisted-prime-number/](https://www.geeksforgeeks.org/twisted-prime-number/)

如果一个数是质数，它的反数也是质数，那么这个数被称为扭曲质数。
示例:

```
Input : 97
Output : Twisted Prime Number
Explanation: 97 is a prime number
and its reverse 79 is also a prime
number.

Input : 43
Output : Not a Twisted Prime Number
Explanation: 43 is a prime number
but its reverse 34 is not a prime
number.
```

这个想法是首先检查 n 是否是质数，然后反转 n，检查反转的 n 是否是质数。
我们用下面两篇文章的方法。
1) [检查一个数字是否是质数(学校方法)](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)
2) [反转一个数字的数字](https://www.geeksforgeeks.org/write-a-c-program-to-reverse-digits-of-a-number/)。

## C++

```
// C/C++ program to check if a given number
// is Twisted Prime or not
#include <bits/stdc++.h>
using namespace std;

// Returns reverse of n
int reverse(int n)
{
    int rev = 0, r;
    while (n > 0) {
        r = n % 10;
        rev = rev * 10 + r;
        n /= 10;
    }
    return rev;
}

// Returns true if n is prime
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five nbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// function to check Twisted Prime nber
bool checkTwistedPrime(int n)
{
    if (isPrime(n) == false)
        return false;

    return isPrime(reverse(n));
}

// Driver Code
int main(void)
{
    // Printing Twisted Prime nbers upto 200
    cout << "First few Twisted Prime nbers are :- n";
    for (int i = 2; i <= 200; i++)
        if (checkTwistedPrime(i))
            cout << i << " ";

    return 0;
}
// This code is contributed by Nikita Tiwari
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given number
// is Twisted Prime or not
import java.io.*;
import java.math.*;

class GFG
{
    static int reverse(int n)
    {
        int rev = 0, r;
        while (n > 0)
        {
            r = n % 10;
            rev = rev * 10 + r;
            n /= 10;
        }
        return rev;
    }
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

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // function to check Twisted Prime Number
    static boolean checkTwistedPrime(int n)
    {
        if (isPrime(n) == false)
            return false;

        return isPrime(reverse(n));
    }

    // Driver Code
    public static void main(String args[])
    throws IOException
    {
        // Printing Twisted Prime Numbers upto 200
        System.out.println("First few Twisted Prime" +
        " Numbers are :- n");
        for (int i = 2; i <= 200; i++)
            if (checkTwistedPrime(i))
                System.out.print(i + " ");
    }
}
// This code is contributed by Nikita Tiwari.
```

## 计算机编程语言

```
# Python program to check if a given number
# is Twisted Prime or not

def reverse(n) :
    rev = 0

    # reversing the nber
    while n > 0 :
        r = n % 10
        rev = rev * 10 + r
        n = n / 10
    return rev

# Returns true if n is prime, else false
def isPrime(n) :

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # This is checked so that we can skip
    # middle five nbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False

    i = 5
    while (i * i <= n):
        if (n % i == 0 or n % (i + 2) == 0):
            return False
        i = i + 6

    return True;

# function to check Twisted Prime nber
def checkTwistedPrime (n) :
    if (isPrime(n) == False):
        return False

    return isPrime(reverse(n))

# Driver Code
# Printing Twisted Prime nbers upto 200
print "First few Twisted Prime numbers are :- "
i = 2
while i<= 200 :
    if (checkTwistedPrime(i) == True) :
        print i,
    i = i + 1

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to check if a given
// number is Twisted Prime or not
using System;

class GFG
{
static int reverse(int n)
{
    int rev = 0, r;
    while (n > 0)
    {
        r = n % 10;
        rev = rev * 10 + r;
        n /= 10;
    }
    return rev;
}

static bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that
    // we can skip middle five
    // numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5;
             i * i <= n; i = i + 6)
        if (n % i == 0 ||
            n % (i + 2) == 0)
            return false;

    return true;
}

// function to check
// Twisted Prime Number
static bool checkTwistedPrime(int n)
{
    if (isPrime(n) == false)
        return false;

    return isPrime(reverse(n));
}

// Driver Code
static public void Main ()
{

// Printing Twisted Prime
// Numbers upto 200
Console.WriteLine("First few Twisted Prime" +
                         " Numbers are :- ");

for (int i = 2; i <= 200; i++)
    if (checkTwistedPrime(i))
        Console.Write(i + " ");
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a given number
// is Twisted Prime or not

function reverse($n)
{
    $rev = 0;

    // reversing the nber
    while($n > 0){
        $r = $n % 10;
        $rev = $rev * 10 + $r;
        $n = (int)($n / 10);
        }
    return $rev;
}

// Returns true if n is prime, else false
function isPrime($n)
{
    // Corner cases
    if ($n <= 1)
        return false;
    if ($n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five nbers in below loop
    if ($n % 2 == 0 or $n % 3 == 0)
        return false;

    $i = 5;
    while ($i * $i <= $n){
        if ($n % $i == 0 or $n % ($i + 2) == 0)
            return false;
        $i = $i + 6;
        }

    return true;
}

// function to check Twisted Prime nber
function checkTwistedPrime ($n)
{
    if (isPrime($n) == false)
        return false;

    return isPrime(reverse($n));
}

// Driver Code
// Printing Twisted Prime nbers upto 200
print("First few Twisted Prime numbers are :- \n");
$i = 2;
while($i<= 200)
{
    if (checkTwistedPrime($i) == true)
        print($i." ");
    $i = $i + 1;
}

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript program to check if a given
    // number is Twisted Prime or not

    function reverse(n)
    {
        let rev = 0, r;
        while (n > 0)
        {
            r = n % 10;
            rev = rev * 10 + r;
            n = parseInt(n / 10, 10);
        }
        return rev;
    }

    function isPrime(n)
    {
        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that
        // we can skip middle five
        // numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for (let i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // function to check
    // Twisted Prime Number
    function checkTwistedPrime(n)
    {
        if (isPrime(n) == false)
            return false;

        return isPrime(reverse(n));
    }

    // Printing Twisted Prime
    // Numbers upto 200
    document.write("First few Twisted Prime Numbers are :- " + "</br>");

    for (let i = 2; i <= 200; i++)
        if (checkTwistedPrime(i))
            document.write(i + " ");

</script>
```

**输出:**

```
First few Twisted Prime Numbers are :-
2 3 5 7 11 13 17 31 37 71 73 79 97 101 107 113 131 149 151 157 167 179 181 191 199
```

本文由**尼基塔·蒂瓦里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。