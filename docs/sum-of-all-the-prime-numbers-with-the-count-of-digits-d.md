# 所有素数之和，位数≤ D

> 原文:[https://www . geeksforgeeks . org/所有素数之和加上数字个数 d/](https://www.geeksforgeeks.org/sum-of-all-the-prime-numbers-with-the-count-of-digits-d/)

给定一个整数 **D** ，任务是求所有素数的和，其位数小于或等于 **D** 。

**示例:**

> **输入:** D = 2
> **输出:** 1060
> 2、3、5、7、11、13、17、19、23、29、31、37、41、43、
> 47、53、59、61、67、71、73、79、83、89 和 97 是
> 小于或等于
> 2 的素数以及这些素数的和
> 
> **输入:**D = 3
> T3】输出: 76127

**方法:**使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)生成所有质数，直到最大 D 位数，然后找出相同范围内所有质数的和。

下面是上述方法的实现:

## C++14

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function for Sieve of Eratosthenes
void sieve(bool prime[], int n)
{
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= n; p++) {
        if (prime[p] == true) {
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the sum of
// the required prime numbers
int sumPrime(int d)
{

    // Maximum number of d-digits
    int maxVal = pow(10, d) - 1;

    // Sieve of Eratosthenes
    bool prime[maxVal + 1];
    memset(prime, true, sizeof(prime));
    sieve(prime, maxVal);

    // To store the required sum
    int sum = 0;

    for (int i = 2; i <= maxVal; i++) {

        // If current element is prime
        if (prime[i]) {
            sum += i;
        }
    }

    return sum;
}

// Driver code
int main()
{
    int d = 3;

    cout << sumPrime(d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function for Sieve of Eratosthenes
    static void sieve(boolean []prime, int n)
    {
        prime[0] = false;
        prime[1] = false;
        for (int p = 2; p * p <= n; p++)
        {
            if (prime[p] == true)
            {
                for (int i = p * p; i <= n; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to return the sum of
    // the required prime numbers
    static int sumPrime(int d)
    {
        int i;
        // Maximum number of d-digits
        int maxVal = (int)Math.pow(10, d) - 1;

        // Sieve of Eratosthenes
        boolean prime[] = new boolean[maxVal + 1];

        for(i = 0; i < maxVal + 1; i++)
            prime[i] = true;

        sieve(prime, maxVal);

        // To store the required sum
        int sum = 0;

        for (i = 2; i <= maxVal; i++)
        {

            // If current element is prime
            if (prime[i])
            {
                sum += i;
            }
        }
        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int d = 3;

        System.out.println(sumPrime(d));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# Function for Sieve of Eratosthenes
def sieve(prime, n) :

    prime[0] = False;
    prime[1] = False;
    for p in range(2, int(sqrt(n)) + 1) :
        if (prime[p] == True) :
            for i in range( p * p, n + 1, p) :
                prime[i] = False;

# Function to return the sum of
# the required prime numbers
def sumPrime(d) :

    # Maximum number of d-digits
    maxVal = (10 ** d) - 1;

    # Sieve of Eratosthenes
    prime = [True] * (maxVal + 1);
    sieve(prime, maxVal);

    # To store the required sum
    sum = 0;

    for i in range(2, maxVal + 1) :

        # If current element is prime
        if (prime[i]) :
            sum += i;

    return sum;

# Driver code
if __name__ == "__main__" :

    d = 3;

    print(sumPrime(d));

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function for Sieve of Eratosthenes
    static void sieve(Boolean []prime, int n)
    {
        prime[0] = false;
        prime[1] = false;
        for (int p = 2; p * p <= n; p++)
        {
            if (prime[p] == true)
            {
                for (int i = p * p;
                         i <= n; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to return the sum of
    // the required prime numbers
    static int sumPrime(int d)
    {
        int i;
        // Maximum number of d-digits
        int maxVal = (int)Math.Pow(10, d) - 1;

        // Sieve of Eratosthenes
        Boolean []prime = new Boolean[maxVal + 1];

        for(i = 0; i < maxVal + 1; i++)
            prime[i] = true;

        sieve(prime, maxVal);

        // To store the required sum
        int sum = 0;

        for (i = 2; i <= maxVal; i++)
        {

            // If current element is prime
            if (prime[i])
            {
                sum += i;
            }
        }
        return sum;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int d = 3;

        Console.WriteLine(sumPrime(d));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function for Sieve of Eratosthenes
function sieve(prime, n)
{
    prime[0] = false;
    prime[1] = false;

    for(let p = 2; p * p <= n; p++)
    {
        if (prime[p] == true)
        {
            for(let i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the sum of
// the required prime numbers
function sumPrime(d)
{

    // Maximum number of d-digits
    let maxVal = Math.pow(10, d) - 1;

    // Sieve of Eratosthenes
    let prime = new Array(maxVal + 1);
    prime.fill(true)
    sieve(prime, maxVal);

    // To store the required sum
    let sum = 0;

    for(let i = 2; i <= maxVal; i++)
    {

        // If current element is prime
        if (prime[i])
        {
            sum += i;
        }
    }
    return sum;
}

// Driver code
let d = 3;

document.write(sumPrime(d));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
76127
```