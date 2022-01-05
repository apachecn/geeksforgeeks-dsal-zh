# 从给定的数组中找出所有选择的集合的和

> 原文:[https://www . geeksforgeeks . org/find-sum-of-fs-for-all-selected-set-from-the-给定数组/](https://www.geeksforgeeks.org/find-sum-of-fs-for-all-the-chosen-sets-from-the-given-array/)

给定一个大小为 **N** 的数组 **arr[]** 和一个整数 **K** 。任务是找到所有可能集合的 **f(S)** 的和。对于有限集合 **X** ， **f(X)** 是**最大(X)–最小(X)** 。设置 **X** 包含给定数组中的任意 **K** 个数字。输出可以很大，所以，输出答案模 **10 <sup>9</sup> +7** 。

**示例:**

> **输入:** arr[] = {1，1，3，4}，K = 2
> **输出:** 11
> 集合为{1，1}、{1，3}、{1，4}、{1，3}、{1，4}、{3，4}和 f(X)为 0，2，3，2，3，1。
> 
> **输入:** arr[] = {10，-10，10，-10，10，-10}，K = 3
> **输出:** 360
> 18 套 f(x)等于 20，2 套 f(X)等于 0

**方法:**在假设 **arr** 预先排序的情况下，思路是通过预先计算阶乘直到 **N** 及其逆来执行预计算以快速计算二项式系数。最小值和最大值分别计算。换句话说，**(∑max(S))–(∑min(S))**而不是 **∑ f(S)** 。
为简单起见，假设 **arr <sub>i</sub>** 互不相同。**最大值**的可能值是 **arr** 的任意元素。因此，通过计算 **S** 的数量，使得 **max(S) = arr <sub>i</sub>** 对于每个 **i** ，可以找到 **∑ max(S)** 。 **max(S) = arr <sub>i</sub>** 的充要条件是 **S** 含有**arr<sub>I</sub>T38】，还含有小于**arr<sub>I</sub>T44】的 **K-1** 元素，所以这样的数可以直接用二项式系数计算。同样可以计算 **∑ minS** 。
如果 **A <sub>i</sub>** 包含重复项，则可以证明如果假设 **arr** 之间的任意顺序具有相同的值，则上述解释也成立(例如，考虑( **arr <sub>i</sub>** ， **i** 的字典顺序，并计算满足 **max(S) = (A <sub>i</sub> ，I)【的元素数量)因此，在这种情况下，您也可以用相同的方式进行处理。******

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 100005
#define mod (int)(1e9 + 7)

// To store the factorial and the
// factorial mod inverse of a number
int factorial[N], modinverse[N];

// Function to find (a ^ m1) % mod
int power(int a, int m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (1LL * a * a) % mod;
    else if (m1 & 1)
        return (1LL * a
                * power(power(a, m1 / 2), 2))
               % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to find factorial
// of all the numbers
void factorialfun()
{
    factorial[0] = 1;
    for (int i = 1; i < N; i++)
        factorial[i] = (1LL
                        * factorial[i - 1] * i)
                       % mod;
}

// Function to find the factorial
// mod inverse of all the numbers
void modinversefun()
{
    modinverse[N - 1]
        = power(factorial[N - 1], mod - 2) % mod;

    for (int i = N - 2; i >= 0; i--)
        modinverse[i] = (1LL * modinverse[i + 1]
                         * (i + 1))
                        % mod;
}

// Function to return nCr
int binomial(int n, int r)
{
    if (r > n)
        return 0;

    int a = (1LL * factorial[n]
             * modinverse[n - r])
            % mod;

    a = (1LL * a * modinverse[r]) % mod;
    return a;
}

// Function to find sum of f(s) for all
// the chosen sets from the given array
int max_min(int a[], int n, int k)
{
    // Sort the given array
    sort(a, a + n);

    // Calculate the factorial and
    // modinverse of all elements
    factorialfun();
    modinversefun();

    long long ans = 0;
    k--;

    // For all the possible sets
    // Calculate max(S) and min(S)
    for (int i = 0; i < n; i++) {
        int x = n - i - 1;
        if (x >= k)
            ans -= binomial(x, k) * a[i] % mod;

        int y = i;
        if (y >= k)
            ans += binomial(y, k) * a[i] % mod;

        ans = (ans + mod) % mod;
    }

    return (int)(ans);
}

// Driver code
int main()
{
    int a[] = { 1, 1, 3, 4 }, k = 2;
    int n = sizeof(a) / sizeof(int);

    cout << max_min(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

static int N = 100005;
static int mod = 1000000007;
static int temp = 391657242;

// To store the factorial and the
// factorial mod inverse of a number
static int []factorial = new int[N];
static int []modinverse = new int[N];

// Function to find (a ^ m1) % mod
static int power(int a, int m1)
{
    if (m1 == 0)
        return 1;
    else if (m1 == 1)
        return a;
    else if (m1 == 2)
        return (a * a) % mod;
    else if ((m1 & 1)!=0)
        return (a * power(power(a, m1 / 2), 2)) % mod;
    else
        return power(power(a, m1 / 2), 2) % mod;
}

// Function to find factorial
// of all the numbers
static void factorialfun()
{
    factorial[0] = 1;
    for (int i = 1; i < N; i++)
        factorial[i] = (factorial[i - 1] * i)% mod;
}

// Function to find the factorial
// mod inverse of all the numbers
static void modinversefun()
{
    modinverse[N - 1] = power(factorial[N - 1], mod - 2) % mod;

    for (int i = N - 2; i >= 0; i--)
        modinverse[i] = (modinverse[i + 1]*(i + 1))%mod;
}

// Function to return nCr
static int binomial(int n, int r)
{
    if (r > n)
        return 0;

    int a = (factorial[n] * modinverse[n - r]) % mod;

    a = (a * modinverse[r]) % mod;
    return a;
}

// Function to find sum of f(s) for all
// the chosen sets from the given array
static int max_min(int a[], int n, int k)
{
    // Sort the given array
    Arrays.sort(a);

    // Calculate the factorial and
    // modinverse of all elements
    factorialfun();
    modinversefun();

    int ans = 0;
    k--;

    // For all the possible sets
    // Calculate max(S) and min(S)
    for (int i = 0; i < n; i++) {
        int x = n - i - 1;
        if (x >= k)
            ans -= binomial(x, k) * a[i] % mod;

        int y = i;
        if (y >= k)
            ans += binomial(y, k) * a[i] % mod;

        ans = (ans + mod) % mod;
    }

    return ans%temp;
}

// Driver code
public static void main(String args[])
{
    int []a = { 1, 1, 3, 4 };
    int k = 2;
    int n = a.length;

    System.out.println(max_min(a, n, k));
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 100005
mod = (10 ** 9 + 7)

# To store the factorial and the
# factorial mod inverse of a number
factorial = [0]*N
modinverse = [0]*N

# Function to find factorial
# of all the numbers
def factorialfun():
    factorial[0] = 1
    for i in range(1, N):
        factorial[i] = (factorial[i - 1] * i)%mod

# Function to find the factorial
# mod inverse of all the numbers
def modinversefun():
    modinverse[N - 1] = pow(factorial[N - 1], 
                            mod - 2, mod) % mod

    for i in range(N - 2, -1, -1):
        modinverse[i] = (modinverse[i + 1]* (i + 1))% mod

# Function to return nCr
def binomial(n, r):
    if (r > n):
        return 0

    a = (factorial[n]* modinverse[n - r])% mod

    a = (a * modinverse[r]) % mod
    return a

# Function to find sum of f(s) for all
# the chosen sets from the given array
def max_min(a, n, k):

    # Sort the given array
    a = sorted(a)

    # Calculate the factorial and
    # modinverse of all elements
    factorialfun()
    modinversefun()

    ans = 0
    k -= 1

    # For all the possible sets
    # Calculate max(S) and min(S)
    for i in range(n):
        x = n - i - 1
        if (x >= k):
            ans -= (binomial(x, k) * a[i]) % mod

        y = i
        if (y >= k):
            ans += (binomial(y, k) * a[i]) % mod

        ans = (ans + mod) % mod

    return ans

# Driver code

a = [1, 1, 3, 4]
k = 2
n = len(a)

print(max_min(a, n, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach 
using System;

class GFG{ 

    static int N = 100005; 
    static int mod = 1000000007; 
    static int temp = 391657242; 

    // To store the factorial and the 
    // factorial mod inverse of a number 
    static int []factorial = new int[N]; 
    static int []modinverse = new int[N]; 

    // Function to find (a ^ m1) % mod 
    static int power(int a, int m1) 
    { 
        if (m1 == 0) 
            return 1; 
        else if (m1 == 1) 
            return a; 
        else if (m1 == 2) 
            return (a * a) % mod; 
        else if ((m1 & 1)!=0) 
            return (a * power(power(a, m1 / 2), 2)) % mod; 
        else
            return power(power(a, m1 / 2), 2) % mod; 
    } 

    // Function to find factorial 
    // of all the numbers 
    static void factorialfun() 
    { 
        factorial[0] = 1; 
        for (int i = 1; i < N; i++) 
            factorial[i] = (factorial[i - 1] * i)% mod; 
    } 

    // Function to find the factorial 
    // mod inverse of all the numbers 
    static void modinversefun() 
    { 
        modinverse[N - 1] = power(factorial[N - 1], mod - 2) % mod; 

        for (int i = N - 2; i >= 0; i--) 
            modinverse[i] = (modinverse[i + 1]*(i + 1)) % mod; 
    } 

    // Function to return nCr 
    static int binomial(int n, int r) 
    { 
        if (r > n) 
            return 0; 

        int a = (factorial[n] * modinverse[n - r]) % mod; 

        a = (a * modinverse[r]) % mod; 
        return a; 
    } 

    // Function to find sum of f(s) for all 
    // the chosen sets from the given array 
    static int max_min(int []a, int n, int k) 
    { 
        // Sort the given array 
        Array.Sort(a); 

        // Calculate the factorial and 
        // modinverse of all elements 
        factorialfun(); 
        modinversefun(); 

        int ans = 0; 
        k--; 

        // For all the possible sets 
        // Calculate max(S) and min(S) 
        for (int i = 0; i < n; i++) { 
            int x = n - i - 1; 
            if (x >= k) 
                ans -= binomial(x, k) * a[i] % mod; 

            int y = i; 
            if (y >= k) 
                ans += binomial(y, k) * a[i] % mod; 

            ans = (ans + mod) % mod; 
        } 

        return ans % temp; 
    } 

    // Driver code 
    public static void Main(string []args) 
    { 
        int []a = { 1, 1, 3, 4 }; 
        int k = 2; 
        int n = a.Length; 

        Console.WriteLine(max_min(a, n, k)); 
    } 
} 

// This code is contributed by AnkitRai01
```

**Output:**

```
11

```