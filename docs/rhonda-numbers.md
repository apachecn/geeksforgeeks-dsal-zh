# 朗达号码

> 原文:[https://www.geeksforgeeks.org/rhonda-numbers/](https://www.geeksforgeeks.org/rhonda-numbers/)

给定一个整数 **N** ，任务是检查 **N** 是否是以 10 为基数的朗达数。

> 基数为 10 的朗达数是指其位数的乘积等于 10 *的质因数之和(包括多重性)的数。

**示例:**

> **输入:** N = 1568
> **输出:**是
> **解释:**
> 1568 的素分解= 2 <sup>5</sup> * 7 <sup>2</sup> 。
> 素因子之和= 2*5+7*2=24。
> 1568 位数的乘积= 1*5*6*8=240 = 10*24。
> 因此 1568 是以 10 为基数的朗达数。
> 
> **输入:**N = 28
> T3】输出:否

**逼近:**思路是求 N 所有素因子的[之和，检查 N 素因子之和的十倍是否等于 N 位数的乘积。](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)

下面是上述方法的实现:

## C++

```
// C++ implementation to check if N
// is a Rhonda number

#include <bits/stdc++.h>
using namespace std;

// Function to find the 
// product of digits
int getProduct(int n)
{
    int product = 1;

    while (n != 0) {
        product = product * (n % 10);
        n = n / 10;
    }
    return product;
}

// Function to find sum of all prime
// factors of a given number N
int sumOfprimeFactors(int n)
{
    int sum = 0;
    // add the number of
    // 2s that divide n
    while (n % 2 == 0) {
        sum += 2;
        n = n / 2;
    }

    // N must be odd at this
    // point. So we can skip
    // one element
    for (int i = 3; i <= sqrt(n);
                      i = i + 2) {

        // While i divides n,
        // add i and divide n
        while (n % i == 0) {
            sum += i;
            n = n / i;
        }
    }

    // Condition to handle the case when N
    // is a prime number greater than 2
    if (n > 2)
        sum += n;
    return sum;
}

// Function to check if n
// is Rhonda number
bool isRhondaNum(int N)
{
    return 10 * sumOfprimeFactors(N) == getProduct(N);
}

// Driver code
int main()
{
    int n = 1568;
    if (isRhondaNum(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if N
// is a Rhonda number
import java.util.*;
import java.lang.*;
// import Math;

class GFG{

// Function to find the
// product of digits
static int getProduct(int n)
{
    int product = 1;

    while (n != 0)
    {
        product = product * (n % 10);
        n = n / 10;
    }
    return product;
}

// Function to find sum of all prime
// factors of a given number N
static int sumOfprimeFactors(int n)
{
    int sum = 0;

    // Add the number of
    // 2s that divide n
    while (n % 2 == 0)
    {
        sum += 2;
        n = n / 2;
    }

    // N must be odd at this
    // point. So we can skip
    // one element
    for(int i = 3; i <= Math.sqrt(n);
            i = i + 2)
    {

        // While i divides n,
        // add i and divide n
        while (n % i == 0)
        {
            sum += i;
            n = n / i;
        }
    }

    // Condition to handle the case when N
    // is a prime number greater than 2
    if (n > 2)
        sum += n;

    return sum;
}

// Function to check if n
// is Rhonda number
static boolean isRhondaNum(int N)
{
    return (10 * sumOfprimeFactors(N) ==
                        getProduct(N));
}

// Driver Code
public static void main(String[] args)
{

    // Given Number n
    int n = 1568;
    if (isRhondaNum(n))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by vikas_g
```

## 蟒蛇 3

```
# Python3 implementation to check
# if N is a Rhonda number
import math

# Function to find the
# product of digits
def getProduct(n):

    product = 1

    while (n != 0):
        product = product * (n % 10)
        n = n // 10

    return product

# Function to find sum of all prime
# factors of a given number N
def sumOfprimeFactors(n):

    Sum = 0

    # Add the number of
    # 2s that divide n
    while (n % 2 == 0):
        Sum += 2
        n = n // 2

    # N must be odd at this
    # point. So we can skip
    # one element
    for i in range(3, int(math.sqrt(n)) + 1, 2):

        # While i divides n,
        # add i and divide n
        while (n % i == 0):
            Sum += i
            n = n // i

    # Condition to handle the case when N
    # is a prime number greater than 2
    if (n > 2):
        Sum += n

    return Sum

# Function to check if n
# is Rhonda number
def isRhondaNum(N):

    return bool(10 * sumOfprimeFactors(N) ==
                            getProduct(N))

# Driver code
n = 1568

if (isRhondaNum(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation to check if N
// is a Rhonda number
using System;

class GFG{

// Function to find the
// product of digits
static int getProduct(int n)
{
    int product = 1;

    while (n != 0)
    {
        product = product * (n % 10);
        n = n / 10;
    }
    return product;
}

// Function to find sum of all prime
// factors of a given number N
static int sumOfprimeFactors(int n)
{
    int sum = 0;

    // Add the number of
    // 2s that divide n
    while (n % 2 == 0)
    {
        sum += 2;
        n = n / 2;
    }

    // N must be odd at this
    // point. So we can skip
    // one element
    for(int i = 3; i <= Math.Sqrt(n);
            i = i + 2)
    {

        // While i divides n,
        // add i and divide n
        while (n % i == 0)
        {
            sum += i;
            n = n / i;
        }
    }

    // Condition to handle the case when N
    // is a prime number greater than 2
    if (n > 2)
        sum += n;

    return sum;
}

// Function to check if n
// is Rhonda number
static bool isRhondaNum(int N)
{
    return (10 * sumOfprimeFactors(N) ==
                        getProduct(N));
}

// Driver code
public static void Main(String []args)
{
    int n = 1568;

    if (isRhondaNum(n))
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by vikas_g
```

## java 描述语言

```
<script>
// Javascript program to check if N
// is a Rhonda number

    // Function to find the
    // product of digits
    function getProduct( n)
    {
        let product = 1;

        while (n != 0)
        {
            product = product * (n % 10);
            n = parseInt(n / 10);
        }
        return product;
    }

    // Function to find sum of all prime
    // factors of a given number N
    function sumOfprimeFactors( n) {
        let sum = 0;

        // Add the number of
        // 2s that divide n
        while (n % 2 == 0) {
            sum += 2;
            n = parseInt(n / 2);
        }

        // N must be odd at this
        // point. So we can skip
        // one element
        for ( let i = 3; i <= Math.sqrt(n); i = i + 2)
        {

            // While i divides n,
            // add i and divide n
            while (n % i == 0)
            {
                sum += i;
                n = parseInt(n / i);
            }
        }

        // Condition to handle the case when N
        // is a prime number greater than 2
        if (n > 2)
            sum += n;

        return sum;
    }

    // Function to check if n
    // is Rhonda number
    function isRhondaNum( N) {
        return (10 * sumOfprimeFactors(N) == getProduct(N));
    }

    // Driver Code    
    // Given Number n
    let n = 1568;
    if (isRhondaNum(n)) {
        document.write("Yes");
    } else {
        document.write("No");
    }

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(sqrt(N))

**参考文献:**[OEIS](https://oeis.org/A099542)T4】