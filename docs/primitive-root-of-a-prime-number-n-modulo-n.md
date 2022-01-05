# 素数 n 模 n 的本原根

> 原文:[https://www . geesforgeks . org/prime-根号-n-模-n/](https://www.geeksforgeeks.org/primitive-root-of-a-prime-number-n-modulo-n/)

给定一个素数 n，任务是在模 n 下找到它的本原根。素数 n 的本原根是介于[1，n-1]之间的整数 r，使得 x 在[0，n-2]范围内的 r^x(mod n 的值不同。如果 n 是非质数，返回-1。

**示例:**

```
Input : 7
Output : Smallest primitive root = 3
Explanation: n = 7
3^0(mod 7) = 1
3^1(mod 7) = 3
3^2(mod 7) = 2
3^3(mod 7) = 6
3^4(mod 7) = 4
3^5(mod 7) = 5

Input : 761
Output : Smallest primitive root = 6 
```

一个**简单的解决方法**就是尝试从 2 到 n-1 的所有数字。对于每个数字 r，计算 r^x(mod 的值，其中 x 在[0，n-2]的范围内。如果所有这些值都不同，则返回 r，否则继续下一个 r 值。如果所有 r 值都尝试过，则返回-1。

一个**高效的解决方案**是基于以下事实。
如果一个数 r 模 n 的乘法阶等于[欧拉全能函数φ(n)](https://www.geeksforgeeks.org/eulers-totient-function/)(注意一个素数 n 的欧拉全能函数是 n-1)，那么它就是本原根。

```
1- Euler Totient Function phi = n-1 [Assuming n is prime]
1- Find all prime factors of phi.
2- Calculate all powers to be calculated further 
   using (phi/prime-factors) one by one.
3- Check for all numbered for all powers from i=2 
   to n-1 i.e. (i^ powers) modulo n.
4- If it is 1 then 'i' is not a primitive root of n.
5- If it is never 1 then return i;.
```

虽然一个素数可以有多个本原根，但我们只关心最小的一个。如果你想找到所有的根，那么继续这个过程直到 p-1，而不是通过找到第一个原始根来分解。

## C++

```
// C++ program to find primitive root of a
// given number n
#include<bits/stdc++.h>
using namespace std;

// Returns true if n is prime
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)  return false;
    if (n <= 3)  return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n%2 == 0 || n%3 == 0) return false;

    for (int i=5; i*i<=n; i=i+6)
        if (n%i == 0 || n%(i+2) == 0)
            return false;

    return true;
}

/* Iterative Function to calculate (x^n)%p in
   O(logy) */
int power(int x, unsigned int y, int p)
{
    int res = 1;     // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0)
    {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res*x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x*x) % p;
    }
    return res;
}

// Utility function to store prime factors of a number
void findPrimefactors(unordered_set<int> &s, int n)
{
    // Print the number of 2s that divide n
    while (n%2 == 0)
    {
        s.insert(2);
        n = n/2;
    }

    // n must be odd at this point. So we can skip
    // one element (Note i = i +2)
    for (int i = 3; i <= sqrt(n); i = i+2)
    {
        // While i divides n, print i and divide n
        while (n%i == 0)
        {
            s.insert(i);
            n = n/i;
        }
    }

    // This condition is to handle the case when
    // n is a prime number greater than 2
    if (n > 2)
        s.insert(n);
}

// Function to find smallest primitive root of n
int findPrimitive(int n)
{
    unordered_set<int> s;

    // Check if n is prime or not
    if (isPrime(n)==false)
        return -1;

    // Find value of Euler Totient function of n
    // Since n is a prime number, the value of Euler
    // Totient function is n-1 as there are n-1
    // relatively prime numbers.
    int phi = n-1;

    // Find prime factors of phi and store in a set
    findPrimefactors(s, phi);

    // Check for every number from 2 to phi
    for (int r=2; r<=phi; r++)
    {
        // Iterate through all prime factors of phi.
        // and check if we found a power with value 1
        bool flag = false;
        for (auto it = s.begin(); it != s.end(); it++)
        {

            // Check if r^((phi)/primefactors) mod n
            // is 1 or not
            if (power(r, phi/(*it), n) == 1)
            {
                flag = true;
                break;
            }
         }

         // If there was no power with value 1.
         if (flag == false)
           return r;
    }

    // If no primitive root found
    return -1;
}

// Driver code
int main()
{
    int n = 761;
    cout << " Smallest primitive root of " << n
         << " is " << findPrimitive(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find primitive root of a
// given number n
import java.util.*;

class GFG
{

    // Returns true if n is prime
    static boolean isPrime(int n)
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

        // This is checked so that we can skip
        // middle five numbers in below loop
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

    /* Iterative Function to calculate (x^n)%p in
    O(logy) */
    static int power(int x, int y, int p)
    {
        int res = 1;     // Initialize result

        x = x % p; // Update x if it is more than or
        // equal to p

        while (y > 0)
        {
            // If y is odd, multiply x with result
            if (y % 2 == 1)
            {
                res = (res * x) % p;
            }

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    // Utility function to store prime factors of a number
    static void findPrimefactors(HashSet<Integer> s, int n)
    {
        // Print the number of 2s that divide n
        while (n % 2 == 0)
        {
            s.add(2);
            n = n / 2;
        }

        // n must be odd at this point. So we can skip
        // one element (Note i = i +2)
        for (int i = 3; i <= Math.sqrt(n); i = i + 2)
        {
            // While i divides n, print i and divide n
            while (n % i == 0)
            {
                s.add(i);
                n = n / i;
            }
        }

        // This condition is to handle the case when
        // n is a prime number greater than 2
        if (n > 2)
        {
            s.add(n);
        }
    }

    // Function to find smallest primitive root of n
    static int findPrimitive(int n)
    {
        HashSet<Integer> s = new HashSet<Integer>();

        // Check if n is prime or not
        if (isPrime(n) == false)
        {
            return -1;
        }

        // Find value of Euler Totient function of n
        // Since n is a prime number, the value of Euler
        // Totient function is n-1 as there are n-1
        // relatively prime numbers.
        int phi = n - 1;

        // Find prime factors of phi and store in a set
        findPrimefactors(s, phi);

        // Check for every number from 2 to phi
        for (int r = 2; r <= phi; r++)
        {
            // Iterate through all prime factors of phi.
            // and check if we found a power with value 1
            boolean flag = false;
            for (Integer a : s)
            {

                // Check if r^((phi)/primefactors) mod n
                // is 1 or not
                if (power(r, phi / (a), n) == 1)
                {
                    flag = true;
                    break;
                }
            }

            // If there was no power with value 1.
            if (flag == false)
            {
                return r;
            }
        }

        // If no primitive root found
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 761;
        System.out.println(" Smallest primitive root of " + n
                + " is " + findPrimitive(n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to find primitive root
# of a given number n
from math import sqrt

# Returns True if n is prime
def isPrime( n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0 or n % 3 == 0):
        return False
    i = 5
    while(i * i <= n):
        if (n % i == 0 or n % (i + 2) == 0) :
            return False
        i = i + 6

    return True

""" Iterative Function to calculate (x^n)%p
    in O(logy) */"""
def power( x, y, p):

    res = 1 # Initialize result

    x = x % p # Update x if it is more
              # than or equal to p

    while (y > 0):

        # If y is odd, multiply x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1 # y = y/2
        x = (x * x) % p

    return res

# Utility function to store prime
# factors of a number
def findPrimefactors(s, n) :

    # Print the number of 2s that divide n
    while (n % 2 == 0) :
        s.add(2)
        n = n // 2

    # n must be odd at this po. So we can 
    # skip one element (Note i = i +2)
    for i in range(3, int(sqrt(n)), 2):

        # While i divides n, print i and divide n
        while (n % i == 0) :

            s.add(i)
            n = n // i

    # This condition is to handle the case
    # when n is a prime number greater than 2
    if (n > 2) :
        s.add(n)

# Function to find smallest primitive
# root of n
def findPrimitive( n) :
    s = set()

    # Check if n is prime or not
    if (isPrime(n) == False):
        return -1

    # Find value of Euler Totient function
    # of n. Since n is a prime number, the
    # value of Euler Totient function is n-1
    # as there are n-1 relatively prime numbers.
    phi = n - 1

    # Find prime factors of phi and store in a set
    findPrimefactors(s, phi)

    # Check for every number from 2 to phi
    for r in range(2, phi + 1):

        # Iterate through all prime factors of phi.
        # and check if we found a power with value 1
        flag = False
        for it in s:

            # Check if r^((phi)/primefactors)
            # mod n is 1 or not
            if (power(r, phi // it, n) == 1):

                flag = True
                break

        # If there was no power with value 1.
        if (flag == False):
            return r

    # If no primitive root found
    return -1

# Driver Code
n = 761
print("Smallest primitive root of",
         n, "is", findPrimitive(n))

# This code is contributed by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to find primitive root of a
// given number n
using System;
using System.Collections.Generic;

class GFG
{

    // Returns true if n is prime
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

        // This is checked so that we can skip
        // middle five numbers in below loop
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

    /* Iterative Function to calculate (x^n)%p in
    O(logy) */
    static int power(int x, int y, int p)
    {
        int res = 1;     // Initialize result

        x = x % p; // Update x if it is more than or
        // equal to p

        while (y > 0)
        {
            // If y is odd, multiply x with result
            if (y % 2 == 1)
            {
                res = (res * x) % p;
            }

            // y must be even now
            y = y >> 1; // y = y/2
            x = (x * x) % p;
        }
        return res;
    }

    // Utility function to store prime factors of a number
    static void findPrimefactors(HashSet<int> s, int n)
    {
        // Print the number of 2s that divide n
        while (n % 2 == 0)
        {
            s.Add(2);
            n = n / 2;
        }

        // n must be odd at this point. So we can skip
        // one element (Note i = i +2)
        for (int i = 3; i <= Math.Sqrt(n); i = i + 2)
        {
            // While i divides n, print i and divide n
            while (n % i == 0)
            {
                s.Add(i);
                n = n / i;
            }
        }

        // This condition is to handle the case when
        // n is a prime number greater than 2
        if (n > 2)
        {
            s.Add(n);
        }
    }

    // Function to find smallest primitive root of n
    static int findPrimitive(int n)
    {
        HashSet<int> s = new HashSet<int>();

        // Check if n is prime or not
        if (isPrime(n) == false)
        {
            return -1;
        }

        // Find value of Euler Totient function of n
        // Since n is a prime number, the value of Euler
        // Totient function is n-1 as there are n-1
        // relatively prime numbers.
        int phi = n - 1;

        // Find prime factors of phi and store in a set
        findPrimefactors(s, phi);

        // Check for every number from 2 to phi
        for (int r = 2; r <= phi; r++)
        {
            // Iterate through all prime factors of phi.
            // and check if we found a power with value 1
            bool flag = false;
            foreach (int a in s)
            {

                // Check if r^((phi)/primefactors) mod n
                // is 1 or not
                if (power(r, phi / (a), n) == 1)
                {
                    flag = true;
                    break;
                }
            }

            // If there was no power with value 1.
            if (flag == false)
            {
                return r;
            }
        }

        // If no primitive root found
        return -1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 761;
        Console.WriteLine(" Smallest primitive root of " + n
                + " is " + findPrimitive(n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find primitive root of a
// given number n

// Returns true if n is prime
function isPrime(n) {
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (let i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

/* Iterative Function to calculate (x^n)%p in
O(logy) */

function power(x, y, p) {
    let res = 1;     // Initialize result

    x = x % p; // Update x if it is more than or
    // equal to p

    while (y > 0) {
        // If y is odd, multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1; // y = y/2
        x = (x * x) % p;
    }
    return res;
}

// Utility function to store prime factors of a number
function findPrimefactors(s, n) {
    // Print the number of 2s that divide n
    while (n % 2 == 0) {
        s.add(2);
        n = n / 2;
    }

    // n must be odd at this point. So we can skip
    // one element (Note i = i +2)
    for (let i = 3; i <= Math.sqrt(n); i = i + 2) {
        // While i divides n, print i and divide n
        while (n % i == 0) {
            s.add(i);
            n = n / i;
        }
    }

    // This condition is to handle the case when
    // n is a prime number greater than 2
    if (n > 2)
        s.add(n);
}

// Function to find smallest primitive root of n
function findPrimitive(n) {
    let s = new Set();

    // Check if n is prime or not
    if (isPrime(n) == false)
        return -1;

    // Find value of Euler Totient function of n
    // Since n is a prime number, the value of Euler
    // Totient function is n-1 as there are n-1
    // relatively prime numbers.
    let phi = n - 1;

    // Find prime factors of phi and store in a set
    findPrimefactors(s, phi);

    // Check for every number from 2 to phi
    for (let r = 2; r <= phi; r++) {
        // Iterate through all prime factors of phi.
        // and check if we found a power with value 1
        let flag = false;
        for (let it of s) {

            // Check if r^((phi)/primefactors) mod n
            // is 1 or not
            if (power(r, phi / it, n) == 1) {
                flag = true;
                break;
            }
        }   

        // If there was no power with value 1.
        if (flag == false)
            return r;
    }

    // If no primitive root found
    return -1;
}

// Driver code

let n = 761;
document.write(" Smallest primitive root of " + n + " is " + findPrimitive(n));

// This code is contributed by gfgking
</script>
```

**输出:**

```
Smallest primitive root of 761 is 6
```

本文由**尼泰什·库马尔**[T3【萨希尔·查布拉(akku)](https://practice.geeksforgeeks.org/user-profile.php?user=sahil_coder) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。