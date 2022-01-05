# 设置位最大位置≤ D 的所有素数之和

> 原文:[https://www . geeksforgeeks . org/所有素数之和与集合位 d 的最大位置/](https://www.geeksforgeeks.org/sum-of-all-the-prime-numbers-with-the-maximum-position-of-set-bit-d/)

给定一个整数 **D** ，任务是找出所有素数的和，这些素数的最大设定位位置(最右边的设定位)小于或等于 **D** 。
**注:二进制中的** 2 为 10，最大设置位位置为 2。7 在二进制中是 111，最大设置位位置是 3。

**示例:**

> **输入:** D = 3
> **输出:** 17
> 2、3、5、7 是唯一满足给定条件的素数
> 。
> **输入:** D = 8
> **输出:** 6081

**趋近:**满足给定条件的最大数为**2<sup>D</sup>–1**。因此，使用厄拉多塞的[筛生成所有质数直到**2<sup>D</sup>–1**然后找到相同范围内所有质数的和。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

下面是上述方法的实现:

## C++

```
// C++
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

    // Maximum number of the required range
    int maxVal = pow(2, d) - 1;

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
    int d = 8;

    cout << sumPrime(d);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function for Sieve of Eratosthenes
static void sieve(boolean prime[], int n)
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

    // Maximum number of the required range
    int maxVal = (int) (Math.pow(2, d) - 1);

    // Sieve of Eratosthenes
    boolean []prime = new boolean[maxVal + 1];
    Arrays.fill(prime, true);
    sieve(prime, maxVal);

    // To store the required sum
    int sum = 0;

    for (int i = 2; i <= maxVal; i++)
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
public static void main(String[] args)
{
    int d = 8;

    System.out.println(sumPrime(d));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import sqrt, pow

# Function for Sieve of Eratosthenes
def sieve(prime, n):
    prime[0] = False
    prime[1] = False
    for p in range(2, int(sqrt(n)) + 1, 1):
        if (prime[p] == True):
            for i in range(p * p, n + 1, p):
                prime[i] = False

# Function to return the sum of
# the required prime numbers
def sumPrime(d):

    # Maximum number of the required range
    maxVal = int(pow(2, d)) - 1;

    # Sieve of Eratosthenes
    prime = [True for i in range(maxVal + 1)]

    sieve(prime, maxVal)

    # To store the required sum
    sum = 0

    for i in range(2, maxVal + 1, 1):

        # If current element is prime
        if (prime[i]):
            sum += i

    return sum

# Driver code
if __name__ == '__main__':
    d = 8

    print(sumPrime(d))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

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

    // Maximum number of the required range
    int maxVal = (int) (Math.Pow(2, d) - 1);

    // Sieve of Eratosthenes
    Boolean []prime = new Boolean[maxVal + 1];

    for (int i = 0; i <= maxVal; i++)
        prime.SetValue(true,i);
    sieve(prime, maxVal);

    // To store the required sum
    int sum = 0;

    for (int i = 2; i <= maxVal; i++)
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
public static void Main(String[] args)
{
    int d = 8;

    Console.WriteLine(sumPrime(d));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
//Javascript implementation of the approach

// Function for Sieve of Eratosthenes
function sieve(prime, n)
{
    prime[0] = false;
    prime[1] = false;
    for (var p = 2; p * p <= n; p++) {
        if (prime[p] == true) {
            for (var i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to return the sum of
// the required prime numbers
function sumPrime(d)
{

    // Maximum number of the required range
    var maxVal = Math.pow(2, d) - 1;

    // Sieve of Eratosthenes
    var prime = new Array(maxVal + 1);
    prime.fill(true);
    sieve(prime, maxVal);

    // To store the required sum
    var sum = 0;

    for (var i = 2; i <= maxVal; i++) {

        // If current element is prime
        if (prime[i]) {
            sum += i;
        }
    }

    return sum;
}

var d = 8;
 document.write(  sumPrime(d));

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
6081
```