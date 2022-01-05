# 检查一个数是否是毕达哥拉斯素数

> 原文:[https://www . geeksforgeeks . org/check-如果一个数是一个毕达哥拉斯素数或不是/](https://www.geeksforgeeks.org/check-if-a-number-is-a-pythagorean-prime-or-not/)

给定一个正整数 N，检查它是否是毕达哥拉斯素数。如果是毕达哥拉斯素数，则打印“是”，否则打印“否”。
[**毕达哥拉斯素数**](https://en.wikipedia.org/wiki/Pythagorean_prime)T5:4 * n+1 形式的素数是毕达哥拉斯素数。也可以表示为两个平方之和。
1-100 范围内的毕达哥拉斯素数是:

> 5、13、17、29、37、41、53、61、73、89、97

**示例** :

```
Input : N = 5
Output : Yes
Explanation : 5 is a prime number and can be expressed 
in the form ( 4*n + 1 ) as ( 4*1 + 1 ).

Input : N = 13
Output : Yes
Explanation: 13 is a prime number and can be expressed 
in the form ( 4*n + 1 ) as ( 4*3 + 1 ).
```

一个简单的解决方法是首先检查给定的数是否是质数，是否可以写成 4*n + 1 的形式。如果是，那么这个数就是毕达哥拉斯素数，否则不是。
以下是上述方法的实施

## C++

```
// CPP program to check  if a number is
// Pythagorean prime or not

#include <bits/stdc++.h>
using namespace std;

// Function to check if a number is
// prime or not
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
    int n = 13;

    // Check if number is prime
    // and of the form 4*n+1
    if (isPrime(n) && (n % 4 == 1)) {
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
// JAVA program to check  if a number is
// Pythagorean prime or not

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
        int n = 13;

        // Check if number is prime
        // and of the form 4n+1
        if (isPrime(n) && (n % 4 == 1)) {
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
# Pythagorean prime or not

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
n = 13

# Check if number is prime
# and of the form 4n + 1

if(isPrime(n) and (n % 4 == 1)):

    print("YES")

else:

    print("NO")

```

## C#

```
// C# program to check if a number
// is Pythagorean prime or not
using System;

class GFG
{

// Function to check if a number
// is prime or not
static bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
    {
        return false;
    }
    if (n <= 3)
    {
        return true;
    }

    // This is checked so that we
    // can skip middle five numbers
    // in below loop
    if (n % 2 == 0 || n % 3 == 0)
    {
        return false;
    }

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
public static void Main(string[] args)
{
    int n = 13;

    // Check if number is prime
    // and of the form 4n+1
    if (isPrime(n) && (n % 4 == 1))
    {
        Console.WriteLine("YES");
    }
    else
    {
        Console.WriteLine("NO");
    }
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if
// a number is Pythagorean
// prime or not

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
    if ($n % 2 == 0 or $n % 3 == 0)
        return false;

    for ($i = 5; $i * $i <= $n;
                 $i = $i + 6)
    {
        if ($n % $i == 0 or
            $n % ($i + 2) == 0)
        {
            return false;
        }
    }

    return true;
}

// Driver Code
$n = 13;

// Check if number is prime
// and of the form 4*n+1
if (isPrime($n) && ($n % 4 == 1))
{
    echo "YES";
}
else
{
    echo "NO";
}

// This code is contributed
// by inder_verma
?>
```

## java 描述语言

```
<script>

// Javascript program to check  if a number is
// Pythagorean prime or not

// Function to check if a number is
// prime or not
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
var n = 13;

// Check if number is prime
// and of the form 4*n+1
if (isPrime(n) && (n % 4 == 1)) {
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