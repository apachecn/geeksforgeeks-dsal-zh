# 用 N 个不同的没有大小 A 或 B 的集合的东西找到一些方法来形成集合

> 原文:[https://www . geeksforgeeks . org/find-形成 n 个不同大小的集合的方法数-没有大小集合的事物-a 或-b/](https://www.geeksforgeeks.org/find-number-of-ways-to-form-sets-from-n-distinct-things-with-no-set-of-size-a-or-b/)

给定三个数字 **N，A，B** 。任务是计算选择事物的方法的数量，使得不存在一组尺寸 **A** 或 **B** 。答案可以很大。于是，输出答案模 **10 <sup>9</sup> +7** 。

**注:**空集不考虑作为方式之一。

**示例:**

> **输入:** N = 4，A = 1，B = 3
> **输出:** 7
> **说明:**
> 大小 2 的组数为 6 ( <sup>4</sup> C <sub>2</sub> )。
> 形成 4 号套的方式有 1 种( <sup>4</sup> C <sub>4</sub> )。
> 
> **输入:** N = 10，A = 4，B = 9
> T3】输出: 803

**进场:**思路是先找到包含大小套的路数包括 **A、B** 和空套。然后去掉尺寸 **A、B** 的套数，清空套数。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find number of sets without size A and B
#include <bits/stdc++.h>
using namespace std;
#define mod (int)(1e9 + 7)

// Function to find a^m1
int power(int a, int m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (1LL * a * a) % mod;
    // If m1 is odd, then return a * a^m1/2 * a^m1/2
    else if (m1 & 1)
        return (1LL * a * power(power(a, m1 / 2), 2)) % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to find factorial of a number
int factorial(int x)
{
    int ans = 1;
    for (int i = 1; i <= x; i++)
        ans = (1LL * ans * i) % mod;

    return ans;
}

// Function to find inverse of x
int inverse(int x)
{
    return power(x, mod - 2);
}

// Function to find nCr
int binomial(int n, int r)
{
    if (r > n)
        return 0;

    int ans = factorial(n);

    ans = (1LL * ans * inverse(factorial(r))) % mod;

    ans = (1LL * ans * inverse(factorial(n - r))) % mod;

    return ans;
}

// Function to find number of sets without size a and b
int number_of_sets(int n, int a, int b)
{
    // First calculate all sets
    int ans = power(2, n);

    // Remove sets of size a
    ans = ans - binomial(n, a);

    if (ans < 0)
        ans += mod;

    // Remove sets of size b
    ans = ans - binomial(n, b);

    // Remove empty set
    ans--;

    if (ans < 0)
        ans += mod;

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int N = 4, A = 1, B = 3;

    // Function call
    cout << number_of_sets(N, A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of sets without size A and B
import java.util.*;

class GFG{
static final int mod =(int)(1e9 + 7);

// Function to find a^m1
static int power(int a, int m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (int) ((1L * a * a) % mod);
    // If m1 is odd, then return a * a^m1/2 * a^m1/2
    else if (m1 % 2 == 1)
        return (int) ((1L * a * power(power(a, m1 / 2), 2)) % mod);
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to find factorial of a number
static int factorial(int x)
{
    int ans = 1;
    for (int i = 1; i <= x; i++)
        ans = (int) ((1L * ans * i) % mod);

    return ans;
}

// Function to find inverse of x
static int inverse(int x)
{
    return power(x, mod - 2);
}

// Function to find nCr
static int binomial(int n, int r)
{
    if (r > n)
        return 0;

    int ans = factorial(n);

    ans = (int) ((1L * ans * inverse(factorial(r))) % mod);

    ans = (int) ((1L * ans * inverse(factorial(n - r))) % mod);

    return ans;
}

// Function to find number of sets without size a and b
static int number_of_sets(int n, int a, int b)
{
    // First calculate all sets
    int ans = power(2, n);

    // Remove sets of size a
    ans = ans - binomial(n, a);

    if (ans < 0)
        ans += mod;

    // Remove sets of size b
    ans = ans - binomial(n, b);

    // Remove empty set
    ans--;

    if (ans < 0)
        ans += mod;

    // Return the required answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int N = 4, A = 1, B = 3;

    // Function call
    System.out.print(number_of_sets(N, A, B));

}
}

// This code contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find number of 
# sets without size A and B
mod = 10**9 + 7

# Function to find a^m1
def power(a, m1):
    if (m1 == 0):
        return 1
    elif (m1 == 1):
        return a
    elif (m1 == 2):
        return (a * a) % mod

    # If m1 is odd, then return a * a^m1/2 * a^m1/2
    elif (m1 & 1):
        return (a * power(power(a, m1 // 2), 2)) % mod
    else:
        return power(power(a, m1 // 2), 2) % mod

# Function to find factorial of a number
def factorial(x):
    ans = 1
    for i in range(1, x + 1):
        ans = (ans * i) % mod

    return ans

# Function to find inverse of x
def inverse(x):
    return power(x, mod - 2)

# Function to find nCr
def binomial(n, r):
    if (r > n):
        return 0

    ans = factorial(n)

    ans = (ans * inverse(factorial(r))) % mod

    ans = (ans * inverse(factorial(n - r))) % mod

    return ans

# Function to find number of sets without size a and b
def number_of_sets(n, a, b):

    # First calculate all sets
    ans = power(2, n)

    # Remove sets of size a
    ans = ans - binomial(n, a)

    if (ans < 0):
        ans += mod

    # Remove sets of size b
    ans = ans - binomial(n, b)

    # Remove empty set
    ans -= 1

    if (ans < 0):
        ans += mod

    # Return the required answer
    return ans

# Driver code
if __name__ == '__main__':
    N = 4
    A = 1
    B = 3

    # Function call
    print(number_of_sets(N, A, B))

# This code is contributed by mohit kumar 29    
```

## C#

```
// C# program to find number of sets without size A and B
using System;

class GFG{
static readonly int mod =(int)(1e9 + 7);

// Function to find a^m1
static int power(int a, int m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (int) ((1L * a * a) % mod);
    // If m1 is odd, then return a * a^m1/2 * a^m1/2
    else if (m1 % 2 == 1)
        return (int) ((1L * a * power(power(a, m1 / 2), 2)) % mod);
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to find factorial of a number
static int factorial(int x)
{
    int ans = 1;
    for (int i = 1; i <= x; i++)
        ans = (int) ((1L * ans * i) % mod);

    return ans;
}

// Function to find inverse of x
static int inverse(int x)
{
    return power(x, mod - 2);
}

// Function to find nCr
static int binomial(int n, int r)
{
    if (r > n)
        return 0;

    int ans = factorial(n);

    ans = (int) ((1L * ans * inverse(factorial(r))) % mod);

    ans = (int) ((1L * ans * inverse(factorial(n - r))) % mod);

    return ans;
}

// Function to find number of sets without size a and b
static int number_of_sets(int n, int a, int b)
{
    // First calculate all sets
    int ans = power(2, n);

    // Remove sets of size a
    ans = ans - binomial(n, a);

    if (ans < 0)
        ans += mod;

    // Remove sets of size b
    ans = ans - binomial(n, b);

    // Remove empty set
    ans--;

    if (ans < 0)
        ans += mod;

    // Return the required answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int N = 4, A = 1, B = 3;

    // Function call
    Console.Write(number_of_sets(N, A, B));
}
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
7

```