# 陈素数

> 原文:[https://www.geeksforgeeks.org/chen-prime-number/](https://www.geeksforgeeks.org/chen-prime-number/)

给定一个正整数 n，任务是检查它是否是陈素数。如果给定的数字是陈质数，则打印“是”，否则打印“否”。
[**陈质数**](https://en.wikipedia.org/wiki/Chen_prime) **:** 在数学中，如果*‘p+2’*是质数或半质数，则称质数‘p’为*陈质数*。
A [半素数](https://www.geeksforgeeks.org/check-whether-number-semiprime-not/)是两个素数的乘积。
前几个陈素数是:

> 2、3、5、7、11、13、17、19、23、29、31、37、41、47、53、59、67、71、83、89、101

**例:**

```
Input : 11
Output: YES
Explanation: 11 is prime number and 11+2 
(i.e 13 is also prime number)

Input : 7
Output: YES
Explanation: 7 is prime number and 7+2 
( i.e 9 ) is a semi prime number 
```

**先决条件** :

*   [质数](https://www.geeksforgeeks.org/prime-numbers/)
*   [半素数](https://www.geeksforgeeks.org/check-whether-number-semiprime-not/)

**进场:**

1.  检查给定的数字–“n”是否是质数。
2.  如果 n 是素数:
    *   检查 n+2 是素数还是半素数
    *   如果 n+2 是质数或半质数，则打印“是”
    *   否则，打印“否”
3.  如果 n 不是质数，打印“否”。

以下是上述思路的实现

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to check
// Chen prime number

#include <bits/stdc++.h>
using namespace std;

// Utility function to check whether
// number is semiprime or not
int isSemiprime(int num)
{
    int cnt = 0;

    for (int i = 2; cnt < 2 && i * i <= num; ++i)
        while (num % i == 0)
            num /= i, ++cnt; // Increment count
    // of prime numbers

    // If number is greater than 1, add it to
    // the count variable as it indicates the
    // number remain is prime number
    if (num > 1)
        ++cnt;

    // Return '1' if count is equal to '2' else
    // return '0'
    return cnt == 2;
}

// Utility function to check whether
// the given number is prime or not
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

// Function to check Chen prime number
bool isChenPrime(int n)
{

    if (isPrime(n) && (isSemiprime(n + 2) || isPrime(n + 2)))
        return true;
    else
        return false;
}

// Driver code
int main()
{
    int n = 7;

    if (isChenPrime(n))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to check
// Chen Prime number

class GFG {
    // Utility function to check
    // if the given number is semi-prime or not
    static boolean isSemiPrime(int num)
    {
        int cnt = 0;

        for (int i = 2; cnt < 2 && i * i <= num; ++i)

            while (num % i == 0) {
                num /= i;

                // Increment count
                // of prime numbers
                ++cnt;
            }

        // If number is greater than 1,
        // add it to the count variable
        // as it indicates the number
        // remain is prime number
        if (num > 1)
            ++cnt;

        // Return '1' if count is equal
        // to '2' else return '0'
        return cnt == 2 ? true : false;
    }

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

    // Function to check chen prime number
    static boolean isChenPrime(int n)
    {

        if (isPrime(n) && (isSemiPrime(n + 2) || isPrime(n + 2)))
            return true;
        else
            return false;
    }
    // Driver code
    public static void main(String[] args)
    {

        int n = 7;

        if (isChenPrime(n))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}
```

## C#

```
// C# program to check
// Chen Prime number
using System;
class GFG {
    // Utility function to check
    // if the given number is semi-prime or not
    static bool isSemiPrime(int num)
    {
        int cnt = 0;

        for (int i = 2; cnt < 2 && i * i <= num; ++i)

            while (num % i == 0) {
                num /= i;

                // Increment count
                // of prime numbers
                ++cnt;
            }

        // If number is greater than 1,
        // add it to the count variable
        // as it indicates the number
        // remain is prime number
        if (num > 1)
            ++cnt;

        // Return '1' if count is equal
        // to '2' else return '0'
        return cnt == 2 ? true : false;
    }

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

    // Function to check chen prime number
    static bool isChenPrime(int n)
    {

        if (isPrime(n) && (isSemiPrime(n + 2) || isPrime(n + 2)))
            return true;
        else
            return false;
    }
    // Driver code
    public static void Main()
    {

        int n = 7;

        if (isChenPrime(n))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}
```

## 蟒蛇 3

```
# Python3 program to check
# Chen Prime number

import math

# Utility function to Check
# Semi-prime number

def isSemiPrime(num):
    cnt = 0

    for i in range(2, int(math.sqrt(num)) + 1):
        while num % i == 0:
            num /= i
            cnt += 1 # Increment count
                    # of prime number

        # If count is greater than 2,
        # break loop 
        if cnt >= 2: 
            break
    # If number is greater than 1, add it to
    # the count variable as it indicates the
    # number remain is prime number
    if(num > 1):
        cnt += 1

    # Return '1' if count is equal to '2' else
    # return '0'
    return cnt == 2

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

# Function to check if the
# Given number is Chen prime number or not

def isChenPrime( n):

    if(isPrime(n) and (isSemiPrime(n + 2) or isPrime(n + 2))):
        return True
    else:
        return False

# Driver code

n = 7

if(isChenPrime(n)):
    print("YES");
else:
    print("NO");

```

## java 描述语言

```
<script>

// Javascript program to check
// Chen prime number

// Utility function to check whether
// number is semiprime or not
function isSemiprime(num)
{
    var cnt = 0;

    for (var i = 2; cnt < 2 && i * i <= num; ++i)
        while (num % i == 0)
            num /= i, ++cnt; // Increment count
    // of prime numbers

    // If number is greater than 1, add it to
    // the count variable as it indicates the
    // number remain is prime number
    if (num > 1)
        ++cnt;

    // Return '1' if count is equal to '2' else
    // return '0'
    return cnt == 2;
}

// Utility function to check whether
// the given number is prime or not
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

// Function to check Chen prime number
function isChenPrime(n)
{

    if (isPrime(n) && (isSemiprime(n + 2) || isPrime(n + 2)))
        return true;
    else
        return false;
}

// Driver code
var n = 7;
if (isChenPrime(n))
    document.write( "YES");
else
    document.write( "NO");

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
YES
```