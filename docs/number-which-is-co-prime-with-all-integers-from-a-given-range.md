# 与给定范围内所有整数同素的数

> 原文:[https://www . geesforgeks . org/number-is-co-prime-with-all-integer-from-a-给定范围/](https://www.geeksforgeeks.org/number-which-is-co-prime-with-all-integers-from-a-given-range/)

给定两个正整数 **L** 和 **R** ，任务是找到一个大于 **1** 的整数 **X** ，使得 **X** 与[范围内的所有整数**【L，R】**同素。](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)

**示例:**

> **输入:** L = 16，R = 17
> **输出:** 19
> **说明:**只有与[16，17]范围内所有整数同素的数才是 9。
> 
> **输入:** L = 973360，R = 973432
> T3】输出: 973439

**方法:**解决给定问题最简单的方法就是找一个大于 **R** 的[素数](https://www.geeksforgeeks.org/prime-numbers/)，因为这个整数不除**【L，R】**范围内的任何整数。所以思路是从 **(R + 1)** 这个值开始迭代，如果有一个整数是素数，那么打印这个整数，[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check whether the
// given number N is prime or not
bool isPrime(int N)
{
    // Base Case
    if (N == 1)
        return false;

    for (int i = 2; i * i <= N; i++) {

        // If N has more than one
        // factor, then return false
        if (N % i == 0)
            return false;
    }

    // Otherwise, return true
    return true;
}

// Function to find X which is co-prime
// with the integers from the range [L, R]
int findCoPrime(int L, int R)
{
    // Store the resultant number
    int coPrime;

    // Check for prime integers
    // greater than R
    for (int i = R + 1;; i++) {

        // If the current number is
        // prime, then update coPrime
        // and break out of loop
        if (isPrime(i)) {
            coPrime = i;
            break;
        }
    }

    // Print the resultant number
    return coPrime;
}

// Driver Code
int main()
{
    int L = 16, R = 17;
    cout << findCoPrime(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to check whether the
// given number N is prime or not
static boolean isPrime(int N)
{

    // Base Case
    if (N == 1)
        return false;

    for(int i = 2; i * i <= N; i++)
    {

        // If N has more than one
        // factor, then return false
        if (N % i == 0)
            return false;
    }

    // Otherwise, return true
    return true;
}

// Function to find X which is co-prime
// with the integers from the range [L, R]
static int findCoPrime(int L, int R)
{

    // Store the resultant number
    int coPrime;

    // Check for prime integers
    // greater than R
    for(int i = R + 1;; i++)
    {

        // If the current number is
        // prime, then update coPrime
        // and break out of loop
        if (isPrime(i))
        {
            coPrime = i;
            break;
        }
    }

    // Print the resultant number
    return coPrime;
}

// Driver Code
public static void main(String[] args)
{
    int L = 16, R = 17;

    System.out.println(findCoPrime(L, R));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check whether the
# given number N is prime or not
def isPrime(N):
    # Base Case
    if (N == 1):
        return False

    for i in range(2, N + 1):
        if i*i > N:
            break

        # If N has more than one
        # factor, then return false
        if (N % i == 0):
            return False

    # Otherwise, return true
    return True

# Function to find X which is co-prime
# with the integers from the range [L, R]
def findCoPrime(L, R):

    # Store the resultant number
    coPrime, i = 0, R + 1

    # Check for prime integers
    # greater than R
    while True:

        # If the current number is
        # prime, then update coPrime
        # and break out of loop
        if (isPrime(i)):
            coPrime = i
            break
        i += 1

    # Print the resultant number
    return coPrime

# Driver Code
if __name__ == '__main__':
    L,R = 16, 17
    print (findCoPrime(L, R))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check whether the
// given number N is prime or not
static bool isPrime(int N)
{

    // Base Case
    if (N == 1)
        return false;

    for(int i = 2; i * i <= N; i++)
    {

        // If N has more than one
        // factor, then return false
        if (N % i == 0)
            return false;
    }

    // Otherwise, return true
    return true;
}

// Function to find X which is co-prime
// with the integers from the range [L, R]
static int findCoPrime(int L, int R)
{

    // Store the resultant number
    int coPrime;

    // Check for prime integers
    // greater than R
    for(int i = R + 1;; i++)
    {

        // If the current number is
        // prime, then update coPrime
        // and break out of loop
        if (isPrime(i))
        {
            coPrime = i;
            break;
        }
    }

    // Print the resultant number
    return coPrime;
}

// Driver Code
public static void Main(string[] args)
{
    int L = 16, R = 17;

    Console.WriteLine(findCoPrime(L, R));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// javascript program for the above approach
// Function to check whether the
// given number N is prime or not
function isPrime(N)
{

    // Base Case
    if (N == 1)
        return false;

    for(var i = 2; i * i <= N; i++)
    {

        // If N has more than one
        // factor, then return false
        if (N % i == 0)
            return false;
    }

    // Otherwise, return true
    return true;
}

// Function to find X which is co-prime
// with the integers from the range [L, R]
function findCoPrime(L , R)
{

    // Store the resultant number
    var coPrime;

    // Check for prime integers
    // greater than R
    for(var i = R + 1;; i++)
    {

        // If the current number is
        // prime, then update coPrime
        // and break out of loop
        if (isPrime(i))
        {
            coPrime = i;
            break;
        }
    }

    // Prvar the resultant number
    return coPrime;
}

// Driver Code
var L = 16, R = 17;

document.write(findCoPrime(L, R));

// This code contributed by Princi Singh
</script>
```

**Output:** 

```
19
```

***时间复杂度:**O(L * R<sup>1/2</sup>)*
***辅助空间:** O(1)*