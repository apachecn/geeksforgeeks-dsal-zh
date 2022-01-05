# 程序寻找下一个质数

> 原文:[https://www . geesforgeks . org/program-to-find-next-prime-number/](https://www.geeksforgeeks.org/program-to-find-the-next-prime-number/)

给定一个整数 **N** 。任务是找到下一个素数，即大于 **N** 的最小素数。

**示例:**

> **输入:**N = 10
> T3】输出: 11
> 11 是大于 10 的最小素数。
> 
> **输入:**N = 0
> T3】输出: 2

**进场:**

1.  首先取一个找到的布尔变量**初始化为假。**
2.  **现在，直到该变量不等于真，在每次迭代中用 **1** 递增 **N** ，并检查它是否是素数。**
3.  **如果它是质数，则打印它并将找到的变量值更改为真。否则，循环迭代，直到得到下一个质数。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if n
// is prime else returns false
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

// Driver code
int main()
{
    int N = 3;

    cout << nextPrime(N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if n
    // is prime else returns false
    static boolean isPrime(int n)
    {
        // Corner cases
        if (n <= 1) return false;
        if (n <= 3) return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0) return false;

        for (int i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
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

    // Driver code
    public static void main (String[] args)
    {
        int N = 3;

        System.out.println(nextPrime(N));
    }
}

// This code is contributed by AnkitRai01
```

## **蟒蛇 3**

```
# Python3 implementation of the approach
import math

# Function that returns True if n
# is prime else returns False
def isPrime(n):

    # Corner cases
    if(n <= 1):
        return False
    if(n <= 3):
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if(n % 2 == 0 or n % 3 == 0):
        return False

    for i in range(5,int(math.sqrt(n) + 1), 6):
        if(n % i == 0 or n % (i + 2) == 0):
            return False

    return True

# Function to return the smallest
# prime number greater than N
def nextPrime(N):

    # Base case
    if (N <= 1):
        return 2

    prime = N
    found = False

    # Loop continuously until isPrime returns
    # True for a number greater than n
    while(not found):
        prime = prime + 1

        if(isPrime(prime) == True):
            found = True

    return prime

# Driver code
N = 3
print(nextPrime(N))

# This code is contributed by Sanjit_Prasad
```

## **C#**

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if n
    // is prime else returns false
    static bool isPrime(int n)
    {
        // Corner cases
        if (n <= 1) return false;
        if (n <= 3) return true;

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

        // Loop continuously until isPrime
        // returns true for a number
        // greater than n
        while (!found)
        {
            prime++;

            if (isPrime(prime))
                found = true;
        }
        return prime;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int N = 3;

        Console.WriteLine(nextPrime(N));
    }
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>

// Javascript implementation of the approach

// Function that returns true if n
// is prime else returns false
function isPrime(n)
{
    // Corner cases
    if (n <= 1) return false;
    if (n <= 3) return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n%2 == 0 || n%3 == 0) return false;

    for (let i=5; i*i<=n; i=i+6)
        if (n%i == 0 || n%(i+2) == 0)
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

    let prime = N;
    let found = false;

    // Loop continuously until isPrime returns
    // true for a number greater than n
    while (!found) {
        prime++;

        if (isPrime(prime))
            found = true;
    }

    return prime;
}

// Driver code

    let N = 3;

    document.write(nextPrime(N));

// This code is contributed by Mayank Tyagi

</script>
```

****Output:** 

```
5
```**