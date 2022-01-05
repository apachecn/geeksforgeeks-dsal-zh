# 长度为 N 的数字，具有数字 A 和 B，并且其数字总和仅包含数字 A 和 B

> 原文:[https://www . geesforgeks . org/numbers-of-length-n-having-digits-a-b-and-what-sum-of-digits-a-b/](https://www.geeksforgeeks.org/numbers-of-length-n-having-digits-a-and-b-and-whose-sum-of-digits-contain-only-digits-a-and-b/)

给定三个正整数 **N** 、 **A** 和 **B** 。任务是计算长度为 N 的数字，其中只包含数字 A 和 B，并且其数字总和也只包含数字 A 和 B。打印答案模 10 <sup>9</sup> + 7。
**举例:**

> **输入:** N = 3，A = 1，B = 3
> **输出:** 1
> 长度为 3 的可能数字有 113、131、111、333、311、331 等等……
> 但只有 111 是有效数字，因为它的数字之和是 3(只包含数字 A 和 B)
> **输入:** N = 10，A = 2，B = 3
> **输出:…**

**方法:**思路是将数字的位数之和表示为两个变量中的线性方程，即
**S = X * A + Y * B** 其中 **A** 和 **B** 为给定的位数， **X** 和 **Y** 分别为这些位数的频率。
既然 **(X + Y)** 的和根据给定的条件应该等于 **N** (数字的长度)，我们就可以用**(N–X)**代替 **Y** ，方程化简为**S = X * A+(N–X)* B**。因此，X =(S–N * B)/(A–B)。
现在，我们可以迭代所有可能的 S 值，其中 S 的最小值是一个 **N 位**数字，其中所有数字都是 **1** ，S 的最大值是一个 **N 位**数字，其中所有数字都是 **9** ，并检查当前值是否只包含数字 **A** 和 **B** 。使用以上有效电流 **S** 公式求出 **X** 和 **Y** 的值。既然如此，我们也可以将数字的位数置换为 **(N！/ X！y！)**为当前值 s .将此结果添加到最终答案中。
**注:**用[费马小定理](https://www.geeksforgeeks.org/fermats-little-theorem/)计算 **n！% p** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1e5 + 5;
const int MOD = 1e9 + 7;
#define ll long long

// Function that returns true if the num contains
// a and b digits only
int check(int num, int a, int b)
{
    while (num) {
        int rem = num % 10;
        num /= 10;
        if (rem != a && rem != b)
            return 0;
    }
    return 1;
}

// Modular Exponentiation
ll power(ll x, ll y)
{
    ll ans = 1;
    while (y) {
        if (y & 1)
            ans = (ans * x) % MOD;
        y >>= 1;
        x = (x * x) % MOD;
    }
    return ans % MOD;
}

// Function to return the modular inverse
// of x modulo MOD
int modInverse(int x)
{
    return power(x, MOD - 2);
}

// Function to return the required count
// of numbers
ll countNumbers(int n, int a, int b)
{
    ll fact[MAX], inv[MAX];
    ll ans = 0;

    // Generating factorials of all numbers
    fact[0] = 1;
    for (int i = 1; i < MAX; i++) {
        fact[i] = (1LL * fact[i - 1] * i);
        fact[i] %= MOD;
    }

    // Generating inverse of factorials modulo
    // MOD of all numbers
    inv[MAX - 1] = modInverse(fact[MAX - 1]);
    for (int i = MAX - 2; i >= 0; i--) {
        inv[i] = (inv[i + 1] * (i + 1));
        inv[i] %= MOD;
    }

    // Keeping a as largest number
    if (a < b)
        swap(a, b);

    // Iterate over all possible values of s and
    // if it is a valid S then proceed further
    for (int s = n; s <= 9 * n; s++) {
        if (!check(s, a, b))
            continue;

        // Check for invalid cases in the equation
        if (s < n * b || (s - n * b) % (a - b) != 0)
            continue;
        int numDig = (s - n * b) / (a - b);
        if (numDig > n)
            continue;

        // Find answer using combinatorics
        ll curr = fact[n];
        curr = (curr * inv[numDig]) % MOD;
        curr = (curr * inv[n - numDig]) % MOD;

        // Add this result to final answer
        ans = (ans + curr) % MOD;
    }
    return ans;
}

// Driver Code
int main()
{
    int n = 3, a = 1, b = 3;
    cout << countNumbers(n, a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

static int MAX = (int)(1E5 + 5);
static long MOD = (long)(1E9 + 7);

// Function that returns true if the num contains
// a and b digits only
static boolean check(long num, long a, long b)
{
    while (num > 0)
    {
        long rem = num % 10;
        num /= 10;
        if (rem != a && rem != b)
            return false;
    }
    return true;
}

// Modular Exponentiation
static long power(long x, long y)
{
    long ans = 1;
    while (y > 0)
    {
        if ((y & 1) > 0)
            ans = (ans * x) % MOD;
        y >>= 1;
        x = (x * x) % MOD;
    }
    return ans % MOD;
}

// Function to return the modular inverse
// of x modulo MOD
static long modInverse(long x)
{
    return power(x, MOD - 2);
}

// Function to return the required count
// of numbers
static long countNumbers(long n, long a, long b)
{
    long[] fact = new long[MAX];
    long[] inv = new long[MAX];
    long ans = 0;

    // Generating factorials of all numbers
    fact[0] = 1;
    for (int i = 1; i < MAX; i++)
    {
        fact[i] = (1 * fact[i - 1] * i);
        fact[i] %= MOD;
    }

    // Generating inverse of factorials modulo
    // MOD of all numbers
    inv[MAX - 1] = modInverse(fact[MAX - 1]);
    for (int i = MAX - 2; i >= 0; i--)
    {
        inv[i] = (inv[i + 1] * (i + 1));
        inv[i] %= MOD;
    }

    // Keeping a as largest number
    if (a < b)
    {
        long x = a;
        a = b;
        b = x;
    }

    // Iterate over all possible values of s and
    // if it is a valid S then proceed further
    for (long s = n; s <= 9 * n; s++)
    {
        if (!check(s, a, b))
            continue;

        // Check for invalid cases in the equation
        if (s < n * b || (s - n * b) % (a - b) != 0)
            continue;
        int numDig = (int)((s - n * b) / (a - b));
        if (numDig > n)
            continue;

        // Find answer using combinatorics
        long curr = fact[(int)n];
        curr = (curr * inv[numDig]) % MOD;
        curr = (curr * inv[(int)n - numDig]) % MOD;

        // Add this result to final answer
        ans = (ans + curr) % MOD;
    }
    return ans;
}

// Driver Code
public static void main (String[] args)
{
    long n = 3, a = 1, b = 3;
    System.out.println(countNumbers(n, a, b));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
MAX = 100005;
MOD = 1000000007

# Function that returns true if the num
# contains a and b digits only
def check(num, a, b):
    while (num):
        rem = num % 10
        num = int(num / 10)
        if (rem != a and rem != b):
            return 0

    return 1

# Modular Exponentiation
def power(x, y):
    ans = 1
    while (y):
        if (y & 1):
            ans = (ans * x) % MOD
        y >>= 1
        x = (x * x) % MOD

    return ans % MOD

# Function to return the modular
# inverse of x modulo MOD
def modInverse(x):
    return power(x, MOD - 2)

# Function to return the required
# count of numbers
def countNumbers(n, a, b):
    fact = [0 for i in range(MAX)]
    inv = [0 for i in range(MAX)]
    ans = 0

    # Generating factorials of all numbers
    fact[0] = 1
    for i in range(1, MAX, 1):
        fact[i] = (1 * fact[i - 1] * i)
        fact[i] %= MOD

    # Generating inverse of factorials
    # modulo MOD of all numbers
    inv[MAX - 1] = modInverse(fact[MAX - 1])
    i = MAX - 2
    while(i >= 0):
        inv[i] = (inv[i + 1] * (i + 1))
        inv[i] %= MOD
        i -= 1

    # Keeping a as largest number
    if (a < b):
        temp = a
        a = b
        b = temp

    # Iterate over all possible values of s and
    # if it is a valid S then proceed further
    for s in range(n, 9 * n + 1, 1):
        if (check(s, a, b) == 0):
            continue

        # Check for invalid cases in the equation
        if (s < n * b or (s - n * b) % (a - b) != 0):
            continue
        numDig = int((s - n * b) / (a - b))
        if (numDig > n):
            continue

        # Find answer using combinatorics
        curr = fact[n]
        curr = (curr * inv[numDig]) % MOD
        curr = (curr * inv[n - numDig]) % MOD

        # Add this result to final answer
        ans = (ans + curr) % MOD

    return ans

# Driver Code
if __name__ == '__main__':
    n = 3
    a = 1
    b = 3
    print(countNumbers(n, a, b))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static long MAX = (long)(1E5 + 5);
static long MOD = (long)(1E9 + 7);

// Function that returns true if the num contains
// a and b digits only
static bool check(long num, long a, long b)
{
    while (num > 0)
    {
        long rem = num % 10;
        num /= 10;
        if (rem != a && rem != b)
            return false;
    }
    return true;
}

// Modular Exponentiation
static long power(long x, long y)
{
    long ans = 1;
    while (y > 0)
    {
        if ((y & 1) > 0)
            ans = (ans * x) % MOD;
        y >>= 1;
        x = (x * x) % MOD;
    }
    return ans % MOD;
}

// Function to return the modular inverse
// of x modulo MOD
static long modInverse(long x)
{
    return power(x, MOD - 2);
}

// Function to return the required count
// of numbers
static long countNumbers(long n, long a, long b)
{
    long[] fact = new long[MAX];
    long[] inv = new long[MAX];
    long ans = 0;

    // Generating factorials of all numbers
    fact[0] = 1;
    for (long i = 1; i < MAX; i++)
    {
        fact[i] = (1 * fact[i - 1] * i);
        fact[i] %= MOD;
    }

    // Generating inverse of factorials modulo
    // MOD of all numbers
    inv[MAX - 1] = modInverse(fact[MAX - 1]);
    for (long i = MAX - 2; i >= 0; i--)
    {
        inv[i] = (inv[i + 1] * (i + 1));
        inv[i] %= MOD;
    }

    // Keeping a as largest number
    if (a < b)
    {
        long x = a;
        a = b;
        b = x;
    }

    // Iterate over all possible values of s and
    // if it is a valid S then proceed further
    for (long s = n; s <= 9 * n; s++)
    {
        if (!check(s, a, b))
            continue;

        // Check for invalid cases in the equation
        if (s < n * b || (s - n * b) % (a - b) != 0)
            continue;
        long numDig = (s - n * b) / (a - b);
        if (numDig > n)
            continue;

        // Find answer using combinatorics
        long curr = fact[n];
        curr = (curr * inv[numDig]) % MOD;
        curr = (curr * inv[n - numDig]) % MOD;

        // Add this result to final answer
        ans = (ans + curr) % MOD;
    }
    return ans;
}

// Driver Code
static void Main()
{
    long n = 3, a = 1, b = 3;
    Console.WriteLine(countNumbers(n, a, b));
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
    const MAX = (5);
    let MOD =  (7);

    // Function that returns true if the num contains
    // a and b digits only
    function check(num , a , b) {
        while (num > 0) {
            var rem = num % 10;
            num = parseInt(num/10);
            if (rem != a && rem != b)
                return false;
        }
        return true;
    }

    // Modular Exponentiation
    function power(x , y) {
        var ans = 1;
        while (y > 0) {
            if ((y & 1) > 0)
                ans = (ans * x) % MOD;
            y >>= 1;
            x = (x * x) % MOD;
        }
        return ans % MOD;
    }

    // Function to return the modular inverse
    // of x modulo MOD
    function modInverse(x) {
        return power(x, MOD - 2);
    }

    // Function to return the required count
    // of numbers
    function countNumbers(n , a , b) {
        var fact = Array(MAX).fill(0);
        var inv = Array(MAX).fill(0);
        var ans = 0;

        // Generating factorials of all numbers
        fact[0] = 1;
        for (var i = 1; i < MAX; i++) {
            fact[i] = (1 * fact[i - 1] * i);
            fact[i] %= MOD;
        }

        // Generating inverse of factorials modulo
        // MOD of all numbers
        inv[MAX - 1] = modInverse(fact[MAX - 1]);
        for (i = MAX - 2; i >= 0; i--) {
            inv[i] = (inv[i + 1] * (i + 1));
            inv[i] %= MOD;
        }

        // Keeping a as largest number
        if (a < b) {
            var x = a;
            a = b;
            b = x;
        }

        // Iterate over all possible values of s and
        // if it is a valid S then proceed further
        for (s = n; s <= 9 * n; s++) {
            if (!check(s, a, b))
                continue;

            // Check for invalid cases in the equation
            if (s < n * b || (s - n * b) % (a - b) != 0)
                continue;
            var numDig = parseInt( ((s - n * b) / (a - b)));
            if (numDig > n)
                continue;

            // Find answer using combinatorics
            var curr = fact[parseInt(n)];
            curr = (curr * inv[numDig]) % MOD;
            curr = (curr * inv[parseInt( n - numDig)]) % MOD;

            // Add this result to final answer
            ans = (ans + curr) % MOD;
        }
        return ans;
    }

    // Driver Code

        var n = 3, a = 1, b = 3;
        document.write(countNumbers(n, a, b));

// This code contributed by umadevi9616

</script>
```

**Output**

```
1
```

**时间复杂度:** O(最大值)

**辅助空间:**0(最大)