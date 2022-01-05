# 加法素数

> 原文:[https://www.geeksforgeeks.org/additive-prime-number/](https://www.geeksforgeeks.org/additive-prime-number/)

给定一个数字 **N** ，任务是检查 **N** 是否为**加质数**。如果 **N** 是**加质数**，则打印**“是”**否则打印**“否”**。

> 加性素数是素数 P，这样 P 的位数之和也是[素数](https://www.geeksforgeeks.org/prime-numbers/)。
> 例如，23 是加法素数，因为 2 + 3 = 5 是素数。

**示例:**

> **输入:** N = 23
> **输出:**是
> **说明:**
> 23 位数之和= 2 + 3 = 5。
> 
> **输入:**N = 10
> T3】输出:否

**逼近:**思路是求数字 **N** 的位数之和，检查是否为素数。如果 sum 是质数，则打印**“是”**否则打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Check if N is prime or not
bool isPrime(int n)
{
    // Corner Cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    // This is checked to skip
    // middle five numbers
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to get sum of digits
int getSum(int n)
{
    int sum = 0;
    while (n != 0) {
        sum = sum + n % 10;
        n = n / 10;
    }

    // Return the sum of digits
    return sum;
}

// Function to check whether
// the given number is
// Additive Prime number or not
bool isAdditivePrime(int n)
{
    // If number is not prime
    if (!isPrime(n))
        return false;

    // Check if sum of digits
    // is prime or not
    return isPrime(getSum(n));
}

// Driver Code
int main()
{
    // Given Number N
    int N = 23;

    // Function Call
    if (isAdditivePrime(N))
        cout << "Yes";
    else
        cout << "No";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Check if N is prime or not
static boolean isPrime(int n)
{

    // Corner Cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    // This is checked to skip
    // middle five numbers
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
       if (n % i == 0 || n % (i + 2) == 0)
           return false;

    return true;
}

// Function to get sum of digits
static int getSum(int n)
{
    int sum = 0;
    while (n != 0)
    {
        sum = sum + n % 10;
        n = n / 10;
    }

    // Return the sum of digits
    return sum;
}

// Function to check whether
// the given number is
// Additive Prime number or not
static boolean isAdditivePrime(int n)
{

    // If number is not prime
    if (!isPrime(n))
        return false;

    // Check if sum of digits
    // is prime or not
    return isPrime(getSum(n));
}

// Driver code
public static void main(String[] args)
{

    // Given Number N
    int n = 23;

    // Function Call
    if (isAdditivePrime(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Check if N is prime or not
def isPrime(n):

    # Corner Cases
    if (n <= 1):
        return False

    if (n <= 3):
        return True

    # This is checked to skip
    # middle five numbers
    if (n % 2 == 0 or n % 3 == 0):
        return False

    i = 5
    while(i * i <= n):
        if (n % i == 0 or n % (i + 2) == 0):
            return False
        i = i + 6

    return True

# Function to get sum of digits
def getSum(n):

    sum = 0
    while (n != 0):
        sum = sum + n % 10
        n = n / 10

    # Return the sum of digits
    return sum

# Function to check whether
# the given number is
# Additive Prime number or not
def isAdditivePrime(n):

    # If number is not prime
    if (not isPrime(n)):
        return False

    # Check if sum of digits
    # is prime or not
    return isPrime(getSum(n))

# Driver Code

# Given Number N
N = 23

# Function Call
if (isAdditivePrime(N)):
    print ("Yes")
else:
    print ("No")

# This code is contributed by Pratik Basu
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Check if N is prime or not
static bool isPrime(int n)
{

    // Corner Cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    // This is checked to skip
    // middle five numbers
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
       if (n % i == 0 || n % (i + 2) == 0)
           return false;

    return true;
}

// Function to get sum of digits
static int getSum(int n)
{
    int sum = 0;
    while (n != 0)
    {
        sum = sum + n % 10;
        n = n / 10;
    }

    // Return the sum of digits
    return sum;
}

// Function to check whether
// the given number is
// Additive Prime number or not
static bool isAdditivePrime(int n)
{

    // If number is not prime
    if (!isPrime(n))
        return false;

    // Check if sum of digits
    // is prime or not
    return isPrime(getSum(n));
}

// Driver code
public static void Main()
{

    // Given Number N
    int n = 23;

    // Function Call
    if (isAdditivePrime(n))
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

// JavaScript program for the above approach

// Check if N is prime or not
function isPrime(n)
{

    // Corner Cases
    if (n <= 1)
        return false;

    if (n <= 3)
        return true;

    // This is checked to skip
    // middle five numbers
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(let i = 5; i * i <= n; i = i + 6)
       if (n % i == 0 || n % (i + 2) == 0)
           return false;

    return true;
}

// Function to get sum of digits
function getSum(n)
{
    let sum = 0;

    while (n != 0)
    {
        sum = sum + n % 10;
        n = n / 10;
    }

    // Return the sum of digits
    return sum;
}

// Function to check whether
// the given number is
// Additive Prime number or not
function isAdditivePrime(n)
{

    // If number is not prime
    if (!isPrime(n))
        return false;

    // Check if sum of digits
    // is prime or not
    return isPrime(getSum(n));
}

// Driver Code

// Given Number N
let n = 23;

// Function Call
if (isAdditivePrime(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by susmitakundugoaldanga

</script>
```

**Output:** 

```
Yes
```