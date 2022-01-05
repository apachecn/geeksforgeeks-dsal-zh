# 找出 A+nB 或 B+nA 形式的素数

> 原文:[https://www . geesforgeks . org/find-out-the-prime-numbers-in-an B- or-bna/](https://www.geeksforgeeks.org/find-out-the-prime-numbers-in-the-form-of-anb-or-bna/)

给定两个整数 **A** 和 **B** 和一个整数 **N** 。任务是找出 **A + nB** 或 **B + nA** 形式的 **N** 素数( **n** =1，2，3…)。如果不可能，请打印-1。

**示例:**

> **输入:** A = 3，B = 5，N = 4
> **输出:** 13，11，17，23
> **解释:**
> 13(3+2 * 5)
> 11(5+2 * 3)
> 17(5+4 * 3)
> 23(3+4 * 5)
> 
> **输入:** A = 4，B = 6，N = 4
> T3】输出: -1

**进场:**
既然 **A + nB** 是一个素数，有一点可以肯定的是 **A** 和 **B** 之间不应该存在任何公因数，也就是说 **A** 和 **B** 应该是同素数。
最好最有效的方法是使用**狄利克雷定理**。
**狄利克雷定理**说如果 **a** 和 **b** 是相对素数的正整数，那么算术序列 **a** 、 **a** + **b** 、 **a** + **2b** 、**a**+**3b**……包含无限多的素数。
所以，首先检查 **A** 和 **B** 是否共充。
如果 **A** 和 **B** 是同素的，那么检查 **A** + **nB** 和 **B** + **nA** 的素性，其中 **n** =1，2，3…打印其中第一个 **N** 素数。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to check
// whether two numbers is
// co-prime or not
int coprime(int a, int b)
{
    if (__gcd(a, b) == 1)
        return true;
    else
        return false;
}

// Utility function to check
// whether a number is prime
// or not
bool isPrime(int n)
{
    // Corner case
    if (n <= 1)
        return false;

    if (n == 2 or n == 3)
        return true;

    // Check from 2 to sqrt(n)
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// finding the Prime numbers
void findNumbers(int a, int b, int n)
{

    bool possible = true;

    // Checking whether given
    // numbers are co-prime
    // or not
    if (!coprime(a, b))
        possible = false;

    int c1 = 1;
    int c2 = 1;

    int num1, num2;

    // To store the N primes
    set<int> st;
    // If 'possible' is true
    if (possible) {

        // Printing n numbers
        // of prime
        while ((int)st.size() != n) {

            // checking the form of a+nb
            num1 = a + (c1 * b);
            if (isPrime(num1)) {
                st.insert(num1);
            }
            c1++;

            // Checking the form of b+na
            num2 = b + (c2 * a);
            if (isPrime(num2)) {
                st.insert(num2);
            }
            c2++;
        }

        for (int i : st)
            cout << i << " ";
    }

    // If 'possible' is false
    // return -1
    else
        cout << "-1";
}

// Driver Code
int main()
{

    int a = 3;
    int b = 5;
    int n = 4;

    findNumbers(a, b, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{
static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Utility function to check
// whether two numbers is
// co-prime or not
static boolean coprime(int a, int b)
{
    if (__gcd(a, b) == 1)
        return true;
    else
        return false;
}

// Utility function to check
// whether a number is prime
// or not
static boolean isPrime(int n)
{
    // Corner case
    if (n <= 1)
        return false;

    if (n == 2 || n == 3)
        return true;

    // Check from 2 to sqrt(n)
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// finding the Prime numbers
static void findNumbers(int a, int b, int n)
{
    boolean possible = true;

    // Checking whether given
    // numbers are co-prime
    // or not
    if (!coprime(a, b))
        possible = false;

    int c1 = 1;
    int c2 = 1;

    int num1, num2;

    // To store the N primes
    HashSet<Integer> st = new HashSet<Integer>();
    // If 'possible' is true
    if (possible)
    {

        // Printing n numbers
        // of prime
        while ((int)st.size() != n)
        {

            // checking the form of a+nb
            num1 = a + (c1 * b);
            if (isPrime(num1))
            {
                st.add(num1);
            }
            c1++;

            // Checking the form of b+na
            num2 = b + (c2 * a);
            if (isPrime(num2))
            {
                st.add(num2);
            }
            c2++;
        }

        for (int i : st)
            System.out.print(i + " ");
    }

    // If 'possible' is false
    // return -1
    else
        System.out.print("-1");
}

// Driver Code
public static void main(String[] args)
{
    int a = 3;
    int b = 5;
    int n = 4;

    findNumbers(a, b, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
from math import gcd, sqrt

# Utility function to check
# whether two numbers is
# co-prime or not
def coprime(a, b) :

    if (gcd(a, b) == 1) :
        return True;

    else :
        return False;

# Utility function to check
# whether a number is prime
# or not
def isPrime(n) :

    # Corner case
    if (n <= 1) :
        return False;

    if (n == 2 or n == 3) :
        return True;

    # Check from 2 to sqrt(n)
    for i in range(2, int(sqrt(n)) + 1) :
        if (n % i == 0) :
            return False;

    return True;

# finding the Prime numbers
def findNumbers(a, b, n) :

    possible = True;

    # Checking whether given
    # numbers are co-prime
    # or not
    if (not coprime(a, b)) :
        possible = False;

    c1 = 1;
    c2 = 1;

    num1 = 0;
    num2 = 0;

    # To store the N primes
    st = set();

    # If 'possible' is true
    if (possible) :

        # Printing n numbers
        # of prime
        while (len(st) != n) :

            # checking the form of a+nb
            num1 = a + (c1 * b);

            if (isPrime(num1)):

                st.add(num1);

            c1 += 1;

            # Checking the form of b+na
            num2 = b + (c2 * a);

            if (isPrime(num2)):
                st.add(num2);

            c2 += 1;

        for i in st :
            print(i, end = " ");

    # If 'possible' is false
    # return -1
    else :
        print("-1");

# Driver Code
if __name__ == "__main__" :

    a = 3;
    b = 5;
    n = 4;

    findNumbers(a, b, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Utility function to check
// whether two numbers is
// co-prime or not
static bool coprime(int a, int b)
{
    if (__gcd(a, b) == 1)
        return true;
    else
        return false;
}

// Utility function to check
// whether a number is prime
// or not
static bool isPrime(int n)
{
    // Corner case
    if (n <= 1)
        return false;

    if (n == 2 || n == 3)
        return true;

    // Check from 2 to sqrt(n)
    for (int i = 2; i * i <= n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// finding the Prime numbers
static void findNumbers(int a, int b, int n)
{
    bool possible = true;

    // Checking whether given
    // numbers are co-prime
    // or not
    if (!coprime(a, b))
        possible = false;

    int c1 = 1;
    int c2 = 1;

    int num1, num2;

    // To store the N primes
    HashSet<int> st = new HashSet<int>();

    // If 'possible' is true
    if (possible)
    {

        // Printing n numbers
        // of prime
        while (st.Count != n)
        {

            // checking the form of a+nb
            num1 = a + (c1 * b);
            if (isPrime(num1))
            {
                st.Add(num1);
            }
            c1++;

            // Checking the form of b+na
            num2 = b + (c2 * a);
            if (isPrime(num2))
            {
                st.Add(num2);
            }
            c2++;
        }

        foreach (int i in st)
            Console.Write(i + " ");
    }

    // If 'possible' is false
    // return -1
    else
        Console.Write("-1");
}

// Driver Code
public static void Main(String[] args)
{
    int a = 3;
    int b = 5;
    int n = 4;

    findNumbers(a, b, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript  implementation of
// the above approach

function __gcd(a, b) {
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Utility function to check
// whether two numbers is
// co-prime or not
function coprime(a, b) {
    if (__gcd(a, b) == 1)
        return true;
    else
        return false;
}

// Utility function to check
// whether a number is prime
// or not
function isPrime(n) {
    // Corner case
    if (n <= 1)
        return false;

    if (n == 2 || n == 3)
        return true;

    // Check from 2 to sqrt(n)
    for (let i = 2; i * i <= n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// finding the Prime numbers
function findNumbers(a, b, n) {

    let possible = true;

    // Checking whether given
    // numbers are co-prime
    // or not
    if (!coprime(a, b))
        possible = false;

    let c1 = 1;
    let c2 = 1;

    let num1, num2;

    // To store the N primes
    let st = new Set();
    // If 'possible' is true
    if (possible) {

        // Printing n numbers
        // of prime
        while (st.size != n) {

            // checking the form of a+nb
            num1 = a + (c1 * b);
            if (isPrime(num1)) {
                st.add(num1);
            }
            c1++;

            // Checking the form of b+na
            num2 = b + (c2 * a);
            if (isPrime(num2)) {
                st.add(num2);
            }
            c2++;
        }

        // Sort the Set by using spread operator and Array.sort() method
        st = [...st].sort((a, b) => a - b)

        for (let i of st)
            document.write(i + " ");
    }

    // If 'possible' is false
    // return -1
    else
        document.write("-1");
}

// Driver Code
let a = 3;
let b = 5;
let n = 4;

findNumbers(a, b, n);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
11 13 17 23
```