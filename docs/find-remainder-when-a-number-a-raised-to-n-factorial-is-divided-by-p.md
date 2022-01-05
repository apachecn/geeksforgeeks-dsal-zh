# 当一个升到 N 阶乘的数 A 除以 P 时求余数

> 原文:[https://www . geeksforgeeks . org/find-余数-当一个数-一个数-一个数-一个数-一个数-一个数-一个数-一个数-一个数-一个数-一个数-一个数-一个数-一个数-一个数-一个数-一个数-一个数-一](https://www.geeksforgeeks.org/find-remainder-when-a-number-a-raised-to-n-factorial-is-divided-by-p/)

给定三个整数 **A，N** 和 **P** ，任务是找到 **(A^(N！))% P.**

**示例:**

> **输入:** A = 2，N = 1，P = 2
> **输出:** 0
> **解释:** As (2^(1！))= 2
> 因此 2 % 2 将为 0。
> 
> **输入:** A = 3，N = 3，P = 2
> T3】输出: 1

**天真的做法:**这个问题最简单的解决方法可以是找出[T3】N 的阶乘 T5**T7】说 **f，**现在计算**](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)**[T11】A 到 f 的幂](https://www.geeksforgeeks.org/write-a-c-program-to-calculate-powxn/)**T13】说**幂**求其[T17】余数用 PT19】。](https://www.geeksforgeeks.org/modulo-1097-1000000007/)

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>

using namespace std;

// Function to calculate factorial of a Number
long long int fact(long long int n)
{
    long long int ans = 1;

    // Calculating factorial
    for (long long int i = 2; i <= n; i++)
        ans *= i;

    // Returning factorial
    return ans;
}

// Function to calculate resultant remainder
long long int remainder(
    long long int n,
    long long int a,
    long long int p)
{

    // Function call to calculate
    // factorial of n
    long long int len = fact(n);
    long long int ans = 1;

    // Calculating remainder
    for (long long int i = 1; i <= len; i++)
        ans = (ans * a) % p;

    // Returning resultant remainder
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    long long int A = 2, N = 1, P = 2;

    // Function Call
    cout << remainder(N, A, P) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to calculate factorial
static int fact(int n)
{
    int ans = 1;

    // Calculating factorial
    for (int i = 2; i <= n; i++)
        ans *= i;

    // Returning factorial
    return ans;
}

// Function to calculate resultant remainder
static int remainder(
    int n,
    int a,
    int p)
{

    // Function call to calculate
    // factorial of n
    int len = fact(n);
    int ans = 1;

    // Calculating remainder
    for (int i = 1; i <= len; i++)
        ans = (ans * a) % p;

    // Returning resultant remainder
    return ans;
}

// Driver Code
public static void main(String args[])
{

   // Given Input
    int A = 2, N = 1, P = 2;

    // Function Call
    System.out.println(remainder(N, A, P));
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python 3 program for above approach

# Function to calculate factorial of a Number
def fact(n):
    ans = 1

    # Calculating factorial
    for i in range(2,n+1,1):
        ans *= i

    # Returning factorial
    return ans

# Function to calculate resultant remainder
def remainder(n, a, p):

    # Function call to calculate
    # factorial of n
    len1 = fact(n)
    ans = 1

    # Calculating remainder
    for i in range(1,len1+1,1):
        ans = (ans * a) % p

    # Returning resultant remainder
    return ans

# Driver Code
if __name__ == '__main__':
    # Given Input
    A = 2
    N = 1
    P = 2

    # Function Call
    print(remainder(N, A, P))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach

using System;

public class GFG{

// Function to calculate factorial
static int fact(int n)
{
    int ans = 1;

    // Calculating factorial
    for (int i = 2; i <= n; i++)
        ans *= i;

    // Returning factorial
    return ans;
}

// Function to calculate resultant remainder
static int remainder(
    int n,
    int a,
    int p)
{

    // Function call to calculate
    // factorial of n
    int len = fact(n);
    int ans = 1;

    // Calculating remainder
    for (int i = 1; i <= len; i++)
        ans = (ans * a) % p;

    // Returning resultant remainder
    return ans;
}

// Driver Code
public static void Main(string []args)
{

   // Given Input
    int A = 2, N = 1, P = 2;

    // Function Call
    Console.WriteLine(remainder(N, A, P));
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript program for above approach

// Function to calculate factorial of a Number
function fact(n) {
  let ans = 1;

  // Calculating factorial
  for (let i = 2; i <= n; i++) ans *= i;

  // Returning factorial
  return ans;
}

// Function to calculate resultant remainder
function remainder(n, a, p) {
  // Function call to calculate
  // factorial of n
  let len = fact(n);
  let ans = 1;

  // Calculating remainder
  for (let i = 1; i <= len; i++) ans = (ans * a) % p;

  // Returning resultant remainder
  return ans;
}

// Driver Code

// Given Input
let A = 2,
  N = 1,
  P = 2;

// Function Call
document.write(remainder(N, A, P));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
0
```

***时间复杂度:*** O(N！)
***辅助空间:*** O(1)

**有效方法:**利用 [**模幂**](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/) 的概念和**模和幂:**的一些性质，可以优化上述方法

> 1.  X (a * b * c) can be written as:-(((x a) b) c) … the attribute of power.
>     
> 2.  ((x a) b)% p can be written as a module of:-((x a)% p) b)% p ….

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>

using namespace std;

// Function to calculate
// (A^N!)%P in O(log y)
long long int power(
    long long x,
    long long int y,
    long long int p)
{
    // Initialize result
    long long int res = 1;

    // Update x if it is more than or
    // Equal to p
    x = x % p;

    // In case x is divisible by p;
    if (x == 0)
        return 0;

    while (y > 0) {
        // If y is odd,
        // multiply x with result
        if (y & 1)
            res = (res * x) % p;

        // y must be even now
        y = y >> 1;
        x = (x * x) % p;
    }

    // Returning modular power
    return res;
}

// Function to calculate resultant remainder
long long int remainder(
    long long int n,
    long long int a,
    long long int p)
{

    // Initializing ans
    //to store final remainder
  long long int ans = a % p;

    // Calculating remainder
    for (long long int i = 1; i <= n; i++)
        ans = power(ans, i, p);

    // Returning resultant remainder
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    long long int A = 2, N = 1, P = 2;

    // Function Call
    cout << remainder(N, A, P) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG {
    static long power(long x, long y, long p)
    {

        // Initialize result
        long res = 1;

        // Update x if it is more than or
        // Equal to p
        x = x % p;

        // In case x is divisible by p;
        if (x == 0)
            return 0;

        while (y > 0)
        {

            // If y is odd,
            // multiply x with result
            if ((y & 1) == 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1;
            x = (x * x) % p;
        }

        // Returning modular power
        return res;
    }

    // Function to calculate resultant remainder
    static long remainder(long n, long a, long p)
    {

        // Initializing ans to store final remainder
        long ans = a % p;

        // Calculating remainder
        for (long i = 1; i <= n; i++)
            ans = power(ans, i, p);

        // Returning resultant remainder
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        long A = 2, N = 1, P = 2;

        // Function Call
        System.out.println(remainder(N, A, P));
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python program for above approach

# Function to calculate
# (A^N!)%P in O(log y)
def power(x, y, p):

    # Initialize result
    res = 1

    # Update x if it is more than or
    # Equal to p
    x = x % p

    # In case x is divisible by p
    if (x == 0):
        return 0

    while (y > 0):
        # If y is odd,
        # multiply x with result
        if (y & 1):
            res = (res * x) % p

        # y must be even now
        y = y >> 1
        x = (x * x) % p

    # Returning modular power
    return res

# Function to calculate resultant remainder
def remainder(n, a, p):

    # Initializing ans
    #to store final remainder
    ans = a % p

    # Calculating remainder
    for i in range(1,n+1):
        ans = power(ans, i, p)

    # Returning resultant remainder
    return ans

# Driver Code
# Given Input
A = 2
N = 1
P = 2

# Function Call
print(remainder(N, A, P))

# This code is contributed by shivanisinghss2110
```

## C#

```
/*package whatever //do not write package name here */
using System;

class GFG {
    static long power(long x, long y, long p)
    {

        // Initialize result
        long res = 1;

        // Update x if it is more than or
        // Equal to p
        x = x % p;

        // In case x is divisible by p;
        if (x == 0)
            return 0;

        while (y > 0)
        {

            // If y is odd,
            // multiply x with result
            if ((y & 1) == 1)
                res = (res * x) % p;

            // y must be even now
            y = y >> 1;
            x = (x * x) % p;
        }

        // Returning modular power
        return res;
    }

    // Function to calculate resultant remainder
    static long remainder(long n, long a, long p)
    {

        // Initializing ans to store final remainder
        long ans = a % p;

        // Calculating remainder
        for (long i = 1; i <= n; i++)
            ans = power(ans, i, p);

        // Returning resultant remainder
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Given Input
        long A = 2, N = 1, P = 2;

        // Function Call
        Console.Write(remainder(N, A, P));
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to calculate
        // (A^N!)%P in O(log y)
        function power(x, y, p)
        {

            // Initialize result
            let res = 1;

            // Update x if it is more than or
            // Equal to p
            x = x % p;

            // In case x is divisible by p;
            if (x == 0)
                return 0;

            while (y > 0)
            {
                // If y is odd,
                // multiply x with result
                if (y & 1)
                    res = (res * x) % p;

                // y must be even now
                y = y >> 1;
                x = (x * x) % p;
            }

            // Returning modular power
            return res;
        }

        // Function to calculate resultant remainder
        function remainder(n, a, p) {

            // Initializing ans
            // to store final remainder
            let ans = a % p;

            // Calculating remainder
            for (let i = 1; i <= n; i++)
                ans = power(ans, i, p);

            // Returning resultant remainder
            return ans;
        }

        // Driver Code

        // Given Input
        let A = 2, N = 1, P = 2;

        // Function Call
        document.write(remainder(N, A, P) + "<br>");

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
0
```

***时间复杂度:*****O(N * logN)
***辅助空间:*** O(1)**