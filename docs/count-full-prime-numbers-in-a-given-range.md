# 计算给定范围内的全素数

> 原文:[https://www . geesforgeks . org/count-full-质数-给定范围内的数字/](https://www.geeksforgeeks.org/count-full-prime-numbers-in-a-given-range/)

给定两个整数 **L** 和 **R** ，任务是计算给定范围内存在的完整[素数](https://www.geeksforgeeks.org/prime-numbers/)的数量。

> 如果一个数本身是质数，并且它的所有数字也都是质数，那么这个数被称为**全质数**。
> 
> **示例:**
> 
> *   53 是全素数，因为它是素数，它的所有数字(5 和 3)也是素数。
> *   13 不是全素数，因为它有一个非素数(1 不是素数)。

**示例:**

> **输入:** L = 1，R = 100
> **输出:** 8
> **说明:** 2 3 5 7 23 37 53 73 是 1 到 100 之间的全素数。因此，计数为 8。
> 
> **输入:** L = 200，R = 300
> **输出:** 5
> **说明:** 223 227 233 257 277 是 200 到 300 之间的全素数。因此，计数为 5。

**方法:**按照以下步骤解决问题:

*   只需遍历从 **L** 到 **R** 的范围。
*   对于范围内的每个数字 **i** ，检查它是否能被范围**【2，sqrt(I)】**中的任何数字整除。如果发现是真的，那么它就不是质数。进入下一个号码。
*   否则，检查它的所有数字是否都是质数。如果发现为真，增加**计数**。
*   最后，在完成范围遍历后，打印**计数**的值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is prime or not
bool isPrime(int num)
{
    if (num <= 1)
        return false;

    for (int i = 2; i * i <= num; i++)

        // If a divisor of n exists
        if (num % i == 0)
            return false;
    return true;
}

// Function to check if a
// number is Full Prime or not
bool isFulPrime(int n)
{
    // If n is not a prime
    if (!isPrime(n))
        return false;

    // Otherwise
    else {
        while (n > 0) {
            // Extract digit
            int rem = n % 10;
            // If any digit of n
            // is non-prime
            if (!(rem == 2 || rem == 3
                  || rem == 5 || rem == 7))
                return false;

            n = n / 10;
        }
    }
    return true;
}

// Function to print count of
// Full Primes in a range [L, R]
int countFulPrime(int L, int R)
{
    // Stores count of full primes
    int cnt = 0;

    for (int i = L; i <= R; i++) {

        // Check if i is full prime
        if ((i % 2) != 0 && isFulPrime(i)) {
            cnt++;
        }
    }
    return cnt;
}

// Driver Code
int main()
{
    int L = 1, R = 100;

    // Stores count of full primes
    int ans = 0;

    if (L < 3)
        ans++;
    cout << ans + countFulPrime(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to check if a
// number is prime or not
static boolean isPrime(int num)
{
    if (num <= 1)
        return false;

    for(int i = 2; i * i <= num; i++)

        // If a divisor of n exists
        if (num % i == 0)
            return false;

    return true;
}

// Function to check if a
// number is Full Prime or not
static boolean isFulPrime(int n)
{

    // If n is not a prime
    if (!isPrime(n))
        return false;

    // Otherwise
    else
    {
        while (n > 0)
        {

            // Extract digit
            int rem = n % 10;

            // If any digit of n
            // is non-prime
            if (!(rem == 2 || rem == 3 ||
                  rem == 5 || rem == 7))
                return false;

            n = n / 10;
        }
    }
    return true;
}

// Function to print count of
// Full Primes in a range [L, R]
static int countFulPrime(int L, int R)
{

    // Stores count of full primes
    int cnt = 0;

    for(int i = L; i <= R; i++)
    {

        // Check if i is full prime
        if ((i % 2) != 0 && isFulPrime(i))
        {
            cnt++;
        }
    }
    return cnt;
}

// Driver Code
public static void main (String[] args)
{
    int L = 1, R = 100;

    // Stores count of full primes
    int ans = 0;

    if (L < 3)
        ans++;

    System.out.println(ans + countFulPrime(L, R));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if a
# number is prime or not
def isPrime(num):

    if (num <= 1):
        return False

    for i in range(2, num + 1):
        if i * i > num:
            break

        # If a divisor of n exists
        if (num % i == 0):
            return False

    return True

# Function to check if a
# number is Full Prime or not
def isFulPrime(n):

    # If n is not a prime
    if (not isPrime(n)):
        return False

    # Otherwise
    else:
        while (n > 0):

            # Extract digit
            rem = n % 10

            # If any digit of n
            # is non-prime
            if (not (rem == 2 or rem == 3 or
                     rem == 5 or rem == 7)):
                return False

            n = n // 10

    return True

# Function to prcount of
# Full Primes in a range [L, R]
def countFulPrime(L, R):

    # Stores count of full primes
    cnt = 0

    for i in range(L, R + 1):

        # Check if i is full prime
        if ((i % 2) != 0 and isFulPrime(i)):
            cnt += 1

    return cnt

# Driver Code
if __name__ == '__main__':

    L = 1
    R = 100

    # Stores count of full primes
    ans = 0

    if (L < 3):
        ans += 1

    print(ans + countFulPrime(L, R))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if a
// number is prime or not
static bool isPrime(int num)
{
    if (num <= 1)
        return false;

    for(int i = 2; i * i <= num; i++)

        // If a divisor of n exists
        if (num % i == 0)
            return false;

    return true;
}

// Function to check if a
// number is Full Prime or not
static bool isFulPrime(int n)
{

    // If n is not a prime
    if (!isPrime(n))
        return false;

    // Otherwise
    else
    {
        while (n > 0)
        {

            // Extract digit
            int rem = n % 10;

            // If any digit of n
            // is non-prime
            if (!(rem == 2 || rem == 3 ||
                  rem == 5 || rem == 7))
                return false;

            n = n / 10;
        }
    }
    return true;
}

// Function to print count of
// Full Primes in a range [L, R]
static int countFulPrime(int L, int R)
{

    // Stores count of full primes
    int cnt = 0;

    for(int i = L; i <= R; i++)
    {

        // Check if i is full prime
        if ((i % 2) != 0 && isFulPrime(i))
        {
            cnt++;
        }
    }
    return cnt;
}

// Driver Code
public static void Main (String[] args)
{
    int L = 1, R = 100;

    // Stores count of full primes
    int ans = 0;

    if (L < 3)
        ans++;

    Console.WriteLine(ans + countFulPrime(L, R));
}
}

// This code is contributed by math_lover
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to check if a
// number is prime or not
function isPrime(num)
{
    if (num <= 1)
        return false;

    for(let i = 2; i * i <= num; i++)

        // If a divisor of n exists
        if (num % i == 0)
            return false;

    return true;
}

// Function to check if a
// number is Full Prime or not
function isFulPrime(n)
{

    // If n is not a prime
    if (!isPrime(n))
        return false;

    // Otherwise
    else
    {
        while (n > 0)
        {

            // Extract digit
            let rem = n % 10;

            // If any digit of n
            // is non-prime
            if (!(rem == 2 || rem == 3 ||
                  rem == 5 || rem == 7))
                return false;

            n = Math.floor(n / 10);
        }
    }
    return true;
}

// Function to prlet count of
// Full Primes in a range [L, R]
function countFulPrime(L, R)
{

    // Stores count of full primes
    let cnt = 0;

    for(let i = L; i <= R; i++)
    {

        // Check if i is full prime
        if ((i % 2) != 0 && isFulPrime(i))
        {
            cnt++;
        }
    }
    return cnt;
}

// Driver code
let L = 1, R = 100;

// Stores count of full primes
let ans = 0;

if (L < 3)
    ans++;

document.write(ans + countFulPrime(L, R));

// This code is contributed by splevel62

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N<sup>3/2</sup>)*
***辅助空间:** O(1)*