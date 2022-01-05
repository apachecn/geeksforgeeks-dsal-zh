# 检查两个正方形的面积差是否为质数

> 原文:[https://www . geesforgeks . org/check-如果两个正方形的面积差是质数/](https://www.geeksforgeeks.org/check-if-difference-of-areas-of-two-squares-is-prime/)

给定两个边长为![a   ](img/1d69a70cf3f4a43dd0f94fdd77b8b38d.png "Rendered by QuickLaTeX.com")和![b   ](img/1b203eb16a61b21a0955f3e1b9407a28.png "Rendered by QuickLaTeX.com")的正方形(a > b)。任务是检查它们的面积差是否是质数。这里边长可以很大(1 < b < a < 10 <sup>12</sup> )。
**例** :

```
Input : a = 6, b = 5
Output : Yes

Input : a = 61690850361, b = 24777622630    
Output : No
```

**进场:**因为双方是![a   ](img/1d69a70cf3f4a43dd0f94fdd77b8b38d.png "Rendered by QuickLaTeX.com")和![b   ](img/1b203eb16a61b21a0955f3e1b9407a28.png "Rendered by QuickLaTeX.com")。因此，它们的面积之差=(a<sup>2</sup>–b<sup>2</sup>)，可以表示为(a–b)(a+b)。当且仅当**a–b = 1 且 a + b 是质数**时，此为质数。由于 a+b 最多为 2×10 <sup>12</sup> ，我们可以用试除法来检查它的素性。
以下是上述思路的实现:

## C++

```
// C++ program to check if difference of
// areas of two squares is prime or not
// when side length is large

#include <bits/stdc++.h>
using namespace std;

// Function to check if number is prime
bool isPrime(long long int n)
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

    for (long long int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check if difference of areas of
// square is prime
bool isDiffPrime(long long int a, long long int b)
{
    // when a+b is prime and a-b is 1
    if (isPrime(a + b) && a - b == 1)
        return true;
    else
        return false;
}

// Driver code
int main()
{
    long long int a = 6, b = 5;

    if (isDiffPrime(a, b))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if difference
// of areas of two squares is prime or
// not when side length is large
class GFG
{

// Function to check if number
// is prime
static boolean isPrime(long n)
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

    for (long i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check if difference
// of areas of square is prime
static boolean isDiffPrime(long a, long b)
{
    // when a+b is prime and a-b is 1
    if (isPrime(a + b) && a - b == 1)
        return true;
    else
        return false;
}

// Driver code
public static void main(String []args)
{
    long a = 6, b = 5;

    if (isDiffPrime(a, b))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by ihritik
```

## C#

```
// C# program to check if difference
// of areas of two squares is prime
// or not when side length is large
using System;

class GFG
{
// Function to check if number
// is prime
static bool isPrime(long n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we
    // can skip middle five numbers
    // in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (long i = 5;
              i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check if difference
// of areas of square is prime
static bool isDiffPrime(long a, long b)
{
    // when a+b is prime and a-b is 1
    if (isPrime(a + b) && a - b == 1)
        return true;
    else
        return false;
}

// Driver code
public static void Main()
{
    long a = 6, b = 5;

    if (isDiffPrime(a, b))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 program to check if
# difference of areas of two
# squares is prime or not when
# side length is large

def isPrime(n) :

    # Corner cases
    if (n <= 1) :
        return False
    if (n <= 3) :
        return True

    # This is checked so that we 
    # can skip middle five numbers
    # in below loop
    if (n % 2 == 0 or n % 3 == 0) :
        return False

    i = 5
    while(i * i <= n) :
        if (n % i == 0 or n % (i + 2) == 0) :
            return False
        i = i + 6

    return True

# Function to check if difference
# of areas of square is prime
def isDiffPrime(a, b):

    # when a+b is prime and a-b is 1
    if (isPrime(a + b) and a - b == 1):
        return True
    else:
        return False

# Driver code
a = 6
b = 5

if (isDiffPrime(a, b)):
    print("Yes")
else:
    print("No")

# This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if difference
// of areas of two squares is prime
// or not when side length is large
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
    if ($n % 2 == 0 || $n % 3 == 0)
        return false;

    for($i = 5; $i * $i <= $n;
                $i = $i + 6)
        if ($n % $i == 0 ||
            $n % ($i + 2) == 0)
        return false;

    return true;
}

// Function to check if difference
// of areas of square is prime
function isDiffPrime($a, $b)
{
    # when a+b is prime and a-b is 1
    if (isPrime($a + $b) &&
                $a - $b == 1)
        return true;
    else
        return false;

}

// Driver code
$a = 6;
$b = 5;

if (isDiffPrime($a, $b))
    echo "Yes";
else
    echo "No";

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
// Javascript program to check if difference
// of areas of two squares is prime
// or not when side length is large
function isPrime(n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we
    // can skip middle five numbers
    // in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(let i = 5; i * i <= n;
                i = i + 6)
        if (n % i == 0 ||
            n % (i + 2) == 0)
        return false;

    return true;
}

// Function to check if difference
// of areas of square is prime
function isDiffPrime(a, b)
{
    // when a+b is prime and a-b is 1
    if (isPrime(a + b) &&
                a - b == 1)
        return true;
    else
        return false;

}

// Driver code
let a = 6;
let b = 5;

if (isDiffPrime(a, b))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output:** 

```
Yes
```