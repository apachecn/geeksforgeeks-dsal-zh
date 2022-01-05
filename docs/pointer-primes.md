# 指针-质数

> 原文:[https://www.geeksforgeeks.org/pointer-primes/](https://www.geeksforgeeks.org/pointer-primes/)

**指针质数**是质数 **p** 这样 p 之后的下一个质数就可以通过将 p 的数字乘积加起来从 p 中得到
一些指针质数是:

> 23, 61, 1123, 1231, 1321, 2111, 2131, 11261….

### 检查 N 是否是指针素数

给定一个数字 **N** ，任务是检查 **N** 是否为**指针-质数**。如果 **N** 是指针质数，则打印**“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 23
> **输出:**是
> **说明:**
> 23+23 位数的乘积= 29，
> 是 23 之后的下一个素数。
> **输入:** N = 29
> **输出:**否

**进近:** :

1.  求 N 位数的乘积
2.  然后，找到 N 的下一个质数
3.  现在如果 N 是素数，N 位数的 N +积等于 N 的下一个素数，那么打印**“是”**否则打印**“否”**。

以下是上述方法的实现:

## C++

```
// C++ implementation for the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the product of
// digits of a number N
int digProduct(int n)
{
    int product = 1;

    while (n != 0) {
        product = product * (n % 10);
        n = n / 10;
    }

    return product;
}

// Function that returns true if n
// is prime else returns false
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

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to return the smallest
// prime number greater than N
int nextPrime(int N)
{

    // Base case
    if (N <= 1)
        return 2;

    int prime = N;
    bool found = false;

    // Loop continuously until isPrime returns
    // true for a number greater than n
    while (!found) {
        prime++;

        if (isPrime(prime))
            found = true;
    }

    return prime;
}

// Function to check Pointer-Prime numbers
bool isPointerPrime(int n)
{
    if (isPrime(n)
        && (n + digProduct(n) == nextPrime(n)))
        return true;
    else
        return false;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 23;

    // Function Call
    if (isPointerPrime(N))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

// Function to find the product of
// digits of a number N
static int digProduct(int n)
{
    int product = 1;

    while (n != 0)
    {
        product = product * (n % 10);
        n = n / 10;
    }
    return product;
}

// Function that returns true if n
// is prime else returns false
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
        if (n % i == 0 ||
            n % (i + 2) == 0)
            return false;

    return true;
}

// Function to return the smallest
// prime number greater than N
static int nextPrime(int N)
{

    // Base case
    if (N <= 1)
        return 2;

    int prime = N;
    boolean found = false;

    // Loop continuously until isPrime returns
    // true for a number greater than n
    while (!found)
    {
        prime++;

        if (isPrime(prime))
            found = true;
    }
    return prime;
}

// Function to check Pointer-Prime numbers
static boolean isPointerPrime(int n)
{
    if (isPrime(n) &&
       (n + digProduct(n) == nextPrime(n)))
        return true;
    else
        return false;
}

// Driver Code
public static void main(String[] args)
{
    // Given Number N
    int N = 23;

    // Function Call
    if (isPointerPrime(N))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Shubham Prakash
```

## 蟒蛇 3

```
# Python3 implementation for the above approach
def digProduct(n):

    product = 1

    while(n != 0):
        product = product * (n % 10)
        n = int(n / 10)

    return product

# Function that returns true if n
# is prime else returns false
def isPrime(n):

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
        if (n % i == 0 or n % (i + 2) == 0):
            return False

        i = i + 6

    return True

# Function to return the smallest prime
# number greater than N
def nextPrime(N):

    # Base case
    if(N <= 1):
        return 2;

    prime = N
    found = False

    # Loop continuously until isPrime
    # returns true for a number greater
    # than n
    while(not found):
        prime = prime + 1

        if(isPrime(prime)):
            found = True

    return prime

# Function to check Pointer-Prime numbers
def isPointerPrime(n):

    if(isPrime(n) and
      (n + digProduct(n) == nextPrime(n))):
        return True
    else:
        return False

# Driver Code
if __name__=="__main__":

    # Given number N
    N = 23

    # Function call
    if(isPointerPrime(N)):
        print("Yes")
    else:
        print("No")

# This code is contributed by adityakumar27200
```

## C#

```
// C# program for above approach
using System;
class GFG{

// Function to find the product of
// digits of a number N
static int digProduct(int n)
{
    int product = 1;

    while (n != 0)
    {
        product = product * (n % 10);
        n = n / 10;
    }
    return product;
}

// Function that returns true if n
// is prime else returns false
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

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 ||
            n % (i + 2) == 0)
            return false;

    return true;
}

// Function to return the smallest
// prime number greater than N
static int nextPrime(int N)
{

    // Base case
    if (N <= 1)
        return 2;

    int prime = N;
    bool found = false;

    // Loop continuously until isPrime returns
    // true for a number greater than n
    while (!found)
    {
        prime++;

        if (isPrime(prime))
            found = true;
    }
    return prime;
}

// Function to check Pointer-Prime numbers
static bool isPointerPrime(int n)
{
    if (isPrime(n) &&
       (n + digProduct(n) == nextPrime(n)))
        return true;
    else
        return false;
}

// Driver Code
public static void Main()
{
    // Given Number N
    int N = 23;

    // Function Call
    if (isPointerPrime(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation for the
// above approach

// Function to find the product of
// digits of a number N
function digProduct(n)
{
    var product = 1;

    while (n != 0) {
        product = product * (n % 10);
        n = parseInt(n / 10);
    }

    return product;
}

// Function that returns true if n
// is prime else returns false
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

    for (var i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to return the smallest
// prime number greater than N
function nextPrime(N)
{

    // Base case
    if (N <= 1)
        return 2;

    var prime = N;
    var found = false;

    // Loop continuously until isPrime returns
    // true for a number greater than n
    while (!found) {
        prime++;

        if (isPrime(prime))
            found = true;
    }

    return prime;
}

// Function to check Pointer-Prime numbers
function isPointerPrime(n)
{
    if (isPrime(n)
        && (n + digProduct(n) == nextPrime(n)))
        return true;
    else
        return false;
}

// Driver Code
// Given Number N
var N = 23;
// Function Call
if (isPointerPrime(N))
    document.write( "Yes");
else
    document.write( "No");

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(n)。*