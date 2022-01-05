# 四元素数

> 原文:[https://www.geeksforgeeks.org/tetradic-primes/](https://www.geeksforgeeks.org/tetradic-primes/)

A **四进制素数**是[素数](https://www.geeksforgeeks.org/prime-numbers/)也是四进制数。

> 四进制数是一个回文数字，在数字中只包含 0、1 和 8。

### 求小于 N 的四进制素数

给定一个数字 **N** ，任务是打印所有小于或等于 N 的四进制素数。

**示例:**

> **输入:**N = 20
> T3】输出: 11
> 
> **输入:**N = 200
> T3】输出: 11 101 181

**方法:**思想是生成所有小于或等于给定数 N 的素数，并检查每个素数是否为四进制。

*   使用[筛埃拉托斯特尼方法来确定给定的数是否是素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   要检查给定的数字是否是四进制数，请检查该数字是否是回文，并且只包含数字 0、1 和 8。

下面是上述算法的实现:

## C++

```
// C++ implementation to print all
// Tetradic primes smaller than or
// equal to N.
#include <bits/stdc++.h>
using namespace std;

// Function to check if the number
// N having all digits lies in
// the set (0, 1, 8)
bool isContaindigit(int n)
{
    while (n > 0)
    {
        if (!(n % 10 == 0 || 
              n % 10 == 1 || 
              n % 10 == 8))
            return false;

        n = n / 10;
    }
    return true;
}

// Function to check if the number
// N is palindrome
bool ispalindrome(int n)
{
    string temp = to_string(n);
    int l = temp.length();

    for(int i = 0; i < l / 2; i++)
    {
        if (temp[i] != temp[l - i - 1])
            return false;
    }
    return true;
}

// Function to check if a number
// N is Tetradic
bool isTetradic(int n)
{
    if (ispalindrome(n) && isContaindigit(n))
        return true;

    return false;
}

// Function to generate all primes and checking
// whether number is Tetradic or not
void printTetradicPrimesLessThanN(int n)
{

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    int p = 2;

    while (p * p <= n)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) 
        {

            // Update all multiples of p
            for(int i = p * 2; i < n + 1; i += p)
                prime[i] = false;
        }
        p += 1;
    }

    // Print all Tetradic prime numbers
    for(p = 2; p < n + 1; p++)
    {

        // Checking whether the given number
        // is prime Tetradic or not
        if (prime[p] && isTetradic(p))
            cout << p << " ";
    }
}

// Driver code
int main()
{
    int n = 1000;
    printTetradicPrimesLessThanN(n);

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print all
// Tetradic primes smaller than or equal to N.
import java.util.*;

class GFG{

// Function to check if the number
// N having all digits lies in
// the set (0, 1, 8)
public static boolean isContaindigit(int n)
{
    while (n > 0)
    {
        if (!(n % 10 == 0 ||
              n % 10 == 1 ||
              n % 10 == 8))
            return false;
        n = n / 10;
    }
    return true;
}

// Function to check if the number
// N is palindrome
public static boolean ispalindrome(int n)
{
    String temp = Integer.toString(n);
    int l = temp.length();

    for(int i = 0; i < l / 2; i++)
    {
        if (temp.charAt(i) !=
            temp.charAt(l - i - 1))
            return false;
    }
    return true;
}

// Function to check if a number
// N is Tetradic
public static boolean isTetradic(int n)
{
    if (ispalindrome(n) && isContaindigit(n))
        return true;
    return false;
}

// Function to generate all primes and checking
// whether number is Tetradic or not
public static void printTetradicPrimesLessThanN(int n)
{

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    boolean prime[] = new boolean[n + 1];
    Arrays.fill(prime, true);

    int p = 2;

    while (p * p <= n)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p])
        {

            // Update all multiples of p
            for(int i = p * 2; i < n + 1; i += p)
                prime[i] = false;
        }
        p += 1;
    }

    // Print all Tetradic prime numbers
    for(p = 2; p < n + 1; p++)
    {

        // Checking whether the given number
        // is prime Tetradic or not
        if (prime[p] && isTetradic(p))
            System.out.print(p + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int n = 1000;
    printTetradicPrimesLessThanN(n);
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 implementation to print all
# Tetradic primes smaller than or equal to N. 

# Function to check if the number
# N having all digits lies in
# the set (0, 1, 8)
def isContaindigit(n):
    temp = str(n)
    for i in temp:
        if i not in ['0', '1', '8']:
            return False
    return True

# Function to check if the number
# N is palindrome
def ispalindrome(n):
    temp = str(n)
    if temp == temp[::-1]:
        return True
    return False

# Function to check if a number
# N is Tetradic  
def isTetradic(n):      
    if ispalindrome(n):
        if isContaindigit(n):
            return True
    return False

# Function to generate all primes and checking 
# whether number is Tetradic or not 
def printTetradicPrimesLessThanN(n):

    # Create a boolean array "prime[0..n]" and 
    # initialize all entries it as true. A value 
    # in prime[i] will finally be false if i is 
    # Not a prime, else true. 
    prime = [True] * (n + 1); 
    p = 2;
    while (p * p <= n):

        # If prime[p] is not changed, 
        # then it is a prime 
        if (prime[p]): 

            # Update all multiples of p 
            for i in range(p * 2, n + 1, p): 
                prime[i] = False;
        p += 1;

    # Print all Tetradic prime numbers 
    for p in range(2, n + 1): 

        # checking whether the given number 
        # is prime Tetradic or not 
        if (prime[p] and isTetradic(p)): 
            print(p, end = " "); 

# Driver Code 
n = 1000;
printTetradicPrimesLessThanN(n);
```

## C#

```
// C# implementation to print all
// Tetradic primes smaller than
// or equal to N.
using System;

class GFG{

// Function to check if the number
// N having all digits lies in
// the set (0, 1, 8)
static bool isContaindigit(int n)
{
    while (n > 0)
    {
        if (!(n % 10 == 0 || 
              n % 10 == 1 || 
              n % 10 == 8))
            return false;

        n = n / 10;
    }
    return true;
}

// Function to check if the number
// N is palindrome
static bool ispalindrome(int n)
{
    string temp = n.ToString();
    int l = temp.Length;

    for(int i = 0; i < l / 2; i++)
    {
        if (temp[i] != temp[l - i - 1])
            return false;
    }
    return true;
}

// Function to check if a number
// N is Tetradic
static bool isTetradic(int n)
{
    if (ispalindrome(n) &&
        isContaindigit(n))
        return true;

    return false;
}

// Function to generate all primes and checking
// whether number is Tetradic or not
static void printTetradicPrimesLessThanN(int n)
{

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    bool[] prime = new bool[n + 1];
    Array.Fill(prime, true);

    int p = 2;

    while (p * p <= n)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) 
        {

            // Update all multiples of p
            for(int i = p * 2; i < n + 1; i += p)
                prime[i] = false;
        }
        p += 1;
    }

    // Print all Tetradic prime numbers
    for(p = 2; p < n + 1; p++)
    {

        // Checking whether the given number
        // is prime Tetradic or not
        if (prime[p] && isTetradic(p))
            Console.Write(p + " ");
    }
}

// Driver code
static void Main()
{
    int n = 1000;

    printTetradicPrimesLessThanN(n);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // Javascript implementation to print all
    // Tetradic primes smaller than
    // or equal to N.

    // Function to check if the number
    // N having all digits lies in
    // the set (0, 1, 8)
    function isContaindigit(n)
    {
        while (n > 0)
        {
            if (!(n % 10 == 0 ||
                  n % 10 == 1 ||
                  n % 10 == 8))
                return false;

            n = parseInt(n / 10, 10);
        }
        return true;
    }

    // Function to check if the number
    // N is palindrome
    function ispalindrome(n)
    {
        let temp = n.toString();
        let l = temp.length;

        for(let i = 0; i < parseInt(l / 2, 10); i++)
        {
            if (temp[i] != temp[l - i - 1])
                return false;
        }
        return true;
    }

    // Function to check if a number
    // N is Tetradic
    function isTetradic(n)
    {
        if (ispalindrome(n) &&
            isContaindigit(n))
            return true;

        return false;
    }

    // Function to generate all primes and checking
    // whether number is Tetradic or not
    function printTetradicPrimesLessThanN(n)
    {

        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value
        // in prime[i] will finally be false if i is
        // Not a prime, else true.
        let prime = new Array(n + 1);
        prime.fill(true);

        let p = 2;

        while (p * p <= n)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p])
            {

                // Update all multiples of p
                for(let i = p * 2; i < n + 1; i += p)
                    prime[i] = false;
            }
            p += 1;
        }

        // Print all Tetradic prime numbers
        for(p = 2; p < n + 1; p++)
        {

            // Checking whether the given number
            // is prime Tetradic or not
            if (prime[p] && isTetradic(p))
                document.write(p + " ");
        }
    }

    let n = 1000;

    printTetradicPrimesLessThanN(n);

</script>
```

**Output:** 

```
11 101 181
```