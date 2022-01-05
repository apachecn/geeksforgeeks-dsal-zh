# 检查给定的数字 N 是否为莫兰数字

> 原文:[https://www . geesforgeks . org/check-given-number-n-is-a-Moran-number-or-not/](https://www.geeksforgeeks.org/check-whether-given-number-n-is-a-moran-number-or-not/)

给定一个**整数 N** ，检查给定的数字是否为**莫兰数字**。莫兰数字是[哈沙德数字](https://www.geeksforgeeks.org/harshad-or-niven-number/)的一个子集。

> 一个数 **N** 是一个**莫兰数**如果 N 除以其数字的和得到一个**质数**。例如，一些莫兰数字是 18、21、27、42、45 等等。

**例:**

> **输入:** N = 34
> **输出:**否
> **说明:**
> 34 不是莫兰数，因为它不能完全被 7 整除(其位数之和)。
> **输入:** N = 21
> **输出:**是
> **说明:**
> 21 是一个莫兰数，因为 21 除以其位数之和就得到一个素数。

**方法:**要解决上面提到的问题，我们必须找到那个数字的位数之和。然后用这个数除以它的位数之和来求商，并检查这个商是否是素数，然后给定的数是一个莫兰数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation to check if
// the number is Moran number

#include <bits/stdc++.h>
using namespace std;

// Function to calculate digit sum
int digSum(int a)
{
    int sum = 0;
    while (a) {
        sum += a % 10;
        a = a / 10;
    }
    return sum;
}

// Function to check if number is prime
bool isPrime(int r)
{
    bool s = true;

    for (int i = 2; i * i <= r; i++) {
        if (r % i == 0) {
            s = false;
            break;
        }
    }
    return s;
}

// Function to check if
// number is moran number
void moranNo(int n)
{
    int dup = n;

    // Calculate digit sum
    int sum = digSum(dup);

    // Check if n is completely
    // divisible by digit sum
    if (n % sum == 0) {

        // Calculate the quotient
        int c = n / sum;

        // Check if the number is prime
        if (isPrime(c)) {
            cout << "Yes";
            return;
        }
    }

    cout << "No" << endl;
}

// Driver code
int main()
{
    int n = 21;

    moranNo(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if
// the number is Moran number
import java.util.*;
import java.lang.*;
class GFG{

// Function to calculate digit sum
static int digSum(int a)
{
    int sum = 0;
    while (a != 0)
    {
        sum += a % 10;
        a = a / 10;
    }
    return sum;
}

// Function to check if number is prime
static boolean isPrime(int r)
{
    boolean s = true;

    for (int i = 2; i * i <= r; i++)
    {
        if (r % i == 0)
        {
            s = false;
            break;
        }
    }
    return s;
}

// Function to check if
// number is moran number
static void moranNo(int n)
{
    int dup = n;

    // Calculate digit sum
    int sum = digSum(dup);

    // Check if n is completely
    // divisible by digit sum
    if (n % sum == 0)
    {

        // Calculate the quotient
        int c = n / sum;

        // Check if the number is prime
        if (isPrime(c))
        {
            System.out.println("Yes");
            return;
        }
    }
    System.out.println("No");
}

// Driver code
public static void main(String[] args)
{
    int n = 21;

    moranNo(n);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to check if
# the number is Moran number

# Function to calculate digit sum
def digSum(a):

    _sum = 0

    while (a):
        _sum += a % 10
        a = a // 10

    return _sum

# Function to check if number is prime
def isPrime(r):

    s = True
    i = 2

    while i * i <= r:
        if (r % i == 0):
            s = False
            break
        i += 1

    return s

# Function to check if
# number is moran number
def moranNo(n):

    dup = n

    # Calculate digit sum
    _sum = digSum(dup)

    # Check if n is completely
    # divisible by digit sum
    if (n % _sum == 0):

        # Calculate the quotient
        c = n // _sum

        # Check if the number is prime
        if (isPrime(c)):
            print("Yes")
            return

    print("No")

# Driver code
n = 21

moranNo(n)

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation to check if
// the number is Moran number
using System;

class GFG{

// Function to calculate digit sum
static int digSum(int a)
{
    int sum = 0;
    while (a != 0)
    {
        sum += a % 10;
        a = a / 10;
    }
    return sum;
}

// Function to check if number is prime
static bool isPrime(int r)
{
    bool s = true;

    for(int i = 2; i * i <= r; i++)
    {
       if (r % i == 0)
       {
           s = false;
           break;
       }
    }
    return s;
}

// Function to check if
// number is moran number
static void moranNo(int n)
{
    int dup = n;

    // Calculate digit sum
    int sum = digSum(dup);

    // Check if n is completely
    // divisible by digit sum
    if (n % sum == 0)
    {

        // Calculate the quotient
        int c = n / sum;

        // Check if the number is prime
        if (isPrime(c))
        {
            Console.Write("Yes");
            return;
        }
    }
    Console.Write("No");
}

// Driver code
public static void Main()
{
    int n = 21;

    moranNo(n);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementation to check if
// the number is Moran number

// Function to calculate digit sum
function digSum(a)
{
    let sum = 0;
    while (a) {
        sum += a % 10;
        a = Math.floor(a / 10);
    }
    return sum;
}

// Function to check if number is prime
function isPrime(r)
{
    let s = true;

    for (let i = 2; i * i <= r; i++) {
        if (r % i == 0) {
            s = false;
            break;
        }
    }
    return s;
}

// Function to check if
// number is moran number
function moranNo(n)
{
    let dup = n;

    // Calculate digit sum
    let sum = digSum(dup);

    // Check if n is completely
    // divisible by digit sum
    if (n % sum == 0) {

        // Calculate the quotient
        let c = n / sum;

        // Check if the number is prime
        if (isPrime(c)) {
            document.write("Yes");
            return;
        }
    }

    document.write("No" + "<br>");
}

// Driver code

    let n = 21;

    moranNo(n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
Yes
```