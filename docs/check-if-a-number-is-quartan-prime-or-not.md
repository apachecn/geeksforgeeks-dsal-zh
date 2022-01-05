# 检查一个数是否是四次素数

> 原文:[https://www . geeksforgeeks . org/check-a-number-is-quartan-prime-or-not/](https://www.geeksforgeeks.org/check-if-a-number-is-quartan-prime-or-not/)

给定一个正整数 N，检查它是否是 Quartan 素数。如果是四次质数，则打印“是”，否则打印“否”。
[**Quartan Prime**](https://en.wikipedia.org/wiki/Quartan_prime)T5:x<sup>4</sup>+y<sup>4</sup>形式的素数，其中 x > 0，y > 0，x 和 y 是整数是 Quartan Prime。
1-100 范围内的四次质数为:

> 2、17、97

**示例** :

```
Input : 17
Output : Yes
Explanation : 17 is a prime number and can be
expressed in the form of:
x4 + y4  as ( 14 + 24 )

Input : 31
Output : No
Explanation: 31 is prime number but can not be
expressed in the form of x4 + y4.
```

一个**简单的解决方法**是检查给定的数是否是素数，然后检查它是否可以用 x <sup>4</sup> + y <sup>4</sup> 的形式表示。
一个**高效解**是基于每个 Quartan Prime 也可以用 **16*n + 1** 的形式表示。所以，我们可以检查一个数是否是质数，是否可以用 16*n + 1 的形式表示。如果是，那么这个数是四次素数，否则不是。
以下是上述方法的实施

## C++

```
// CPP program to check if a number is
// Quartan Prime or not

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is prime or not
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

// Driver Program
int main()
{
    int n = 17;

    // Check if number is prime
    // and of the form 16*n + 1
    if (isPrime(n) && (n % 16 == 1)) {
        cout << "YES";
    }
    else {
        cout << "NO";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to check if a number is
// Quartan Prime or not

class GFG {

    // Function to check if a number
    // is prime or not
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

    // Driver Program
    public static void main(String[] args)
    {
        int n = 17;

        // Check if number is prime
        // and of the form 16*n + 1
        if (isPrime(n) && (n % 16 == 1)) {
            System.out.println("YES");
        }
        else {
            System.out.println("NO");
        }
    }
}
```

## 蟒蛇 3

```
# Python 3 program to check if a number is
# Quartan Prime or not

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
    while(i * i <= n) :
        if (n % i == 0 or n % (i + 2) == 0) :
            return False
        i = i + 6

    return True

# Driver Code
n = 17

# Check if number is prime
# and of the form 16 * n + 1

if(isPrime(n) and (n % 16 == 1) ):

    print("YES")

else:

    print("NO")

```

## C#

```
// C# program to check if a number
// is Quartan Prime or not
using System;

class GFG
{

// Function to check if a number
// is prime or not
static bool isPrime(int n)
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

    for (int i = 5; i * i <= n; i = i + 6)
    {
        if (n % i == 0 || n % (i + 2) == 0)
        {
            return false;
        }
    }
    return true;
}

// Driver Code
public static void Main()
{
    int n = 17;

    // Check if number is prime
    // and of the form 16*n + 1
    if (isPrime(n) && (n % 16 == 1))
    {
        Console.WriteLine("YES");
    }
    else
    {
        Console.WriteLine("NO");
    }
}
}

// This code is contributed
// by inder_verma
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if a number
// is Quartan Prime or not

// Function to check if a
// number is prime or not
function isPrime($n)
{
    // Corner cases
    if ($n <= 1)
        return false;
    if ($n <= 3)
        return true;

    // This is checked so that
    // we can skip middle five
    // numbers in below loop
    if ($n % 2 == 0 || $n % 3 == 0)
        return false;

    for ($i = 5; $i * $i <= $n;
                 $i = $i + 6)
    {
        if ($n % $i == 0 ||
            $n % ($i + 2) == 0)
        {
            return false;
        }
    }
    return true;
}

// Driver Code
$n = 17;

// Check if number is prime
// and of the form 16*n + 1
if (isPrime($n) && ($n % 16 == 1))
{
    echo "YES";
}
else
{
    echo "NO";
}

// This code is contributed
// anuj_67
?>
```

## java 描述语言

```
<script>
// Javascript program to check if a number is
// Quartan Prime or not

// Function to check if a number
// is prime or not
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

// Driver Program
var n = 17;

// Check if number is prime
// and of the form 16*n + 1
if (isPrime(n) && (n % 16 == 1)) {
    document.write( "YES");
}
else {
    document.write( "NO");
}

// This code is contributed by itsok.
</script>
```

**Output:** 

```
YES
```