# 莫比乌斯函数程序|第 2 集

> 原文:[https://www . geesforgeks . org/program-for-Mobius-function-set-2/](https://www.geeksforgeeks.org/program-for-mobius-function-set-2/)

给定一个整数 **N** 。任务是找到从 1 到 **N** 的所有数字的莫比乌斯函数。
**例:**

> **输入:** N = 5
> **输出:** 1 -1 -1 0 -1
> **输入:** N = 10
> **输出:** 1 -1 -1 0 -1 1 -1 0 0 1

**方法:**想法是首先使用厄拉多塞的[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)找到从 **1** 到 **N** 的所有数字的最小质因数，然后使用这些最小质因数，可以计算所有数字的莫比乌斯函数，这取决于一个数字包含奇数个不同质数还是偶数个不同质数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 100005

int lpf[N];

// Function to calculate least
// prime factor of each number
void least_prime_factor()
{
    for (int i = 2; i < N; i++)

        // If it is a prime number
        if (!lpf[i])

            for (int j = i; j < N; j += i)

                // For all multiples which are not
                // visited yet.
                if (!lpf[j])
                    lpf[j] = i;
}

// Function to find the value of Mobius function
// for all the numbers from 1 to n
void Mobius(int n)
{
    // To store the values of Mobius function
    int mobius[N];

    for (int i = 1; i < N; i++) {

        // If number is one
        if (i == 1)
            mobius[i] = 1;
        else {

            // If number has a squared prime factor
            if (lpf[i / lpf[i]] == lpf[i])
                mobius[i] = 0;

            // Multiply -1 with the previous number
            else
                mobius[i] = -1 * mobius[i / lpf[i]];
        }
    }

    for (int i = 1; i <= n; i++)
        cout << mobius[i] << " ";
}

// Driver code
int main()
{
    int n = 5;

    // Function to find least prime factor
    least_prime_factor();

    // Function to find mobius function
    Mobius(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int N = 100005;

static int []lpf = new int[N];

// Function to calculate least
// prime factor of each number
static void least_prime_factor()
{
    for (int i = 2; i < N; i++)

        // If it is a prime number
        if (lpf[i] % 2 != 1)

            for (int j = i; j < N; j += i)

                // For all multiples which are not
                // visited yet.
                if (lpf[j] % 2 != 0)
                    lpf[j] = i;
}

// Function to find the value of Mobius function
// for all the numbers from 1 to n
static void Mobius(int n)
{
    // To store the values of Mobius function
    int []mobius = new int[N];

    for (int i = 1; i < N; i++)
    {

        // If number is one
        if (i == 1)
            mobius[i] = 1;
        else
        {

            // If number has a squared prime factor
            if (lpf[i / lpf[i]] == lpf[i])
                mobius[i] = 0;

            // Multiply -1 with the previous number
            else
                mobius[i] = -1 * mobius[i / lpf[i]];
        }
    }

    for (int i = 1; i <= n; i++)
        System.out.print(mobius[i] + " ");
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    Arrays.fill(lpf, -1);

    // Function to find least prime factor
    least_prime_factor();

    // Function to find mobius function
    Mobius(n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 100005

lpf = [0] * N;

# Function to calculate least
# prime factor of each number
def least_prime_factor() :

    for i in range(2, N) :

        # If it is a prime number
        if (not lpf[i]) :

            for j in range(i, N, i) :

                # For all multiples which are not
                # visited yet.
                if (not lpf[j]) :
                    lpf[j] = i;

# Function to find the value of Mobius function
# for all the numbers from 1 to n
def Mobius(n) :

    # To store the values of Mobius function
    mobius = [0] * N;

    for i in range(1, N) :

        # If number is one
        if (i == 1) :
            mobius[i] = 1;
        else :

            # If number has a squared prime factor
            if (lpf[i // lpf[i]] == lpf[i]) :
                mobius[i] = 0;

            # Multiply -1 with the previous number
            else :
                mobius[i] = -1 * mobius[i // lpf[i]];

    for i in range(1, n + 1) :
        print(mobius[i], end = " ");

# Driver code
if __name__ == "__main__" :

    n = 5;

    # Function to find least prime factor
    least_prime_factor();

    # Function to find mobius function
    Mobius(n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int N = 100005;

static int []lpf = new int[N];

// Function to calculate least
// prime factor of each number
static void least_prime_factor()
{
    for (int i = 2; i < N; i++)

        // If it is a prime number
        if (lpf[i] % 2 != 1)

            for (int j = i; j < N; j += i)

                // For all multiples which
                // are not visited yet.
                if (lpf[j] % 2 != 0)
                    lpf[j] = i;
}

// Function to find the value of
// Mobius function for all the numbers
// from 1 to n
static void Mobius(int n)
{
    // To store the values of
    // Mobius function
    int []mobius = new int[N];

    for (int i = 1; i < N; i++)
    {

        // If number is one
        if (i == 1)
            mobius[i] = 1;
        else
        {

            // If number has a squared prime factor
            if (lpf[i / lpf[i]] == lpf[i])
                mobius[i] = 0;

            // Multiply -1 with the
            // previous number
            else
                mobius[i] = -1 * mobius[i / lpf[i]];
        }
    }

    for (int i = 1; i <= n; i++)
        Console.Write(mobius[i] + " ");
}

// Driver code
static public void Main ()
{
    int n = 5;
    Array.Fill(lpf, -1);

    // Function to find least prime factor
    least_prime_factor();

    // Function to find mobius function
    Mobius(n);
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

const N = 100005;

let lpf = new Array(N);

// Function to calculate least
// prime factor of each number
function least_prime_factor()
{
    for (let i = 2; i < N; i++)

        // If it is a prime number
        if (!lpf[i])

            for (let j = i; j < N; j += i)

                // For all multiples which are not
                // visited yet.
                if (!lpf[j])
                    lpf[j] = i;
}

// Function to find the value of Mobius function
// for all the numbers from 1 to n
function Mobius(n)
{
    // To store the values of Mobius function
    let mobius = new Array(N);

    for (let i = 1; i < N; i++) {

        // If number is one
        if (i == 1)
            mobius[i] = 1;
        else {

            // If number has a squared prime factor
            if (lpf[parseInt(i / lpf[i])] == lpf[i])
                mobius[i] = 0;

            // Multiply -1 with the previous number
            else
                mobius[i] = -1 * mobius[parseInt(i / lpf[i])];
        }
    }

    for (let i = 1; i <= n; i++)
        document.write(mobius[i] + " ");
}

// Driver code
    let n = 5;

    // Function to find least prime factor
    least_prime_factor();

    // Function to find mobius function
    Mobius(n);

</script>
```

**Output:** 

```
1 -1 -1 0 -1
```