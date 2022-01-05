# 找出配对数，使它们的 gcd 等于 1

> 原文:[https://www . geeksforgeeks . org/find-配对数-这样-他们的-gcd-等于-1/](https://www.geeksforgeeks.org/find-the-number-of-pairs-such-that-their-gcd-is-equals-to-1/)

给定一个大小为 **N** 的数组**。任务是找到配对数，使得 **gcd(a[i]，a[j])** 等于 **1** ，其中 **1 ≤ i < j ≤ N** 。**

****示例:****

> ****输入:** a[] = {1，2，4，6}
> **输出:** 3
> {1，2}、{1，4}、{1，6}就是这样的一对**
> 
> ****输入:** a[] = {1，2，3，4，5，6}
> **输出:** 11**

****逼近:**
答案是 **μ(X) * C(D(X)，2)** 整体整数 **X** 之和。其中， **μ(X)** 为[莫比乌斯函数](https://www.geeksforgeeks.org/program-for-mobius-function-set-2/)， **C(N，K)** 为从 **N** 中选择 **K** 事物， **D(X)** 为给定序列中可被 **X** 整除的整数个数。
解决方案的正确性源于这样一个事实，即我们可以做一个[包含-排除原则](https://www.geeksforgeeks.org/inclusion-exclusion-various-applications/)的解决方案，并表明它实际上等于我们的答案。也就是说，如果 **D** 是由偶数个素数相乘形成的，我们将在答案中加上可被某个中间数除尽的对的数量(在 IEP 中)乘积 **D** 否则减去这个对的数量。**

**所以，我们得到:**

*   **1 表示加法，因为这是素数为偶数的无平方数的莫比乌斯函数。**
*   **-1 表示减法，也就是素数为奇数的无平方数的 Mobius 函数。**
*   **0 表示无平方数。根据定义，它们不会出现在我们的 IEP 解决方案中。**

**下面是上述方法的实现:**

## **C++**

```
// CPP program to find the number of pairs
// such that gcd equals to 1
#include <bits/stdc++.h>
using namespace std;

#define N 100050

int lpf[N], mobius[N];

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
void Mobius()
{
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
}

// Function to find the number of pairs
// such that gcd equals to 1
int gcd_pairs(int a[], int n)
{
    // To store maximum number
    int maxi = 0;

    // To store frequency of each number
    int fre[N] = { 0 };

    // Find frequency and maximum number
    for (int i = 0; i < n; i++) {
        fre[a[i]]++;
        maxi = max(a[i], maxi);
    }

    least_prime_factor();
    Mobius();

    // To store number of pairs with gcd equals to 1
    int ans = 0;

    // Traverse through the all possible elements
    for (int i = 1; i <= maxi; i++) {
        if (!mobius[i])
            continue;

        int temp = 0;
        for (int j = i; j <= maxi; j += i)
            temp += fre[j];

        ans += temp * (temp - 1) / 2 * mobius[i];
    }

    // Return the number of pairs
    return ans;
}

// Driver code
int main()
{
    int a[] = { 1, 2, 3, 4, 5, 6 };

    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    cout << gcd_pairs(a, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find the number of pairs
// such that gcd equals to 1
class GFG
{

static int N = 100050;

static int []lpf = new int[N];
static int []mobius = new int[N];

// Function to calculate least
// prime factor of each number
static void least_prime_factor()
{
    for (int i = 2; i < N; i++)

        // If it is a prime number
        if (lpf[i] == 0)

            for (int j = i; j < N; j += i)

                // For all multiples which are not
                // visited yet.
                if (lpf[j] == 0)
                    lpf[j] = i;
}

// Function to find the value of Mobius function
// for all the numbers from 1 to n
static void Mobius()
{
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
}

// Function to find the number of pairs
// such that gcd equals to 1
static int gcd_pairs(int a[], int n)
{
    // To store maximum number
    int maxi = 0;

    // To store frequency of each number
    int []fre = new int[N];

    // Find frequency and maximum number
    for (int i = 0; i < n; i++)
    {
        fre[a[i]]++;
        maxi = Math.max(a[i], maxi);
    }

    least_prime_factor();
    Mobius();

    // To store number of pairs with gcd equals to 1
    int ans = 0;

    // Traverse through the all possible elements
    for (int i = 1; i <= maxi; i++)
    {
        if (mobius[i] == 0)
            continue;

        int temp = 0;
        for (int j = i; j <= maxi; j += i)
            temp += fre[j];

        ans += temp * (temp - 1) / 2 * mobius[i];
    }

    // Return the number of pairs
    return ans;
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 1, 2, 3, 4, 5, 6 };

    int n = a.length;

    // Function call
    System.out.print(gcd_pairs(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## **蟒蛇 3**

```
# Python3 program to find the number of pairs
# such that gcd equals to 1
N = 100050

lpf = [0 for i in range(N)]
mobius = [0 for i in range(N)]

# Function to calculate least
# prime factor of each number
def least_prime_factor():

    for i in range(2, N):

        # If it is a prime number
        if (lpf[i] == 0):

            for j in range(i, N, i):

                # For all multiples which are not
                # visited yet.
                if (lpf[j] == 0):
                    lpf[j] = i

# Function to find the value of Mobius function
# for all the numbers from 1 to n
def Mobius():

    for i in range(1, N):

        # If number is one
        if (i == 1):
            mobius[i] = 1
        else:

            # If number has a squared prime factor
            if (lpf[ (i // lpf[i]) ] == lpf[i]):
                mobius[i] = 0

            # Multiply -1 with the previous number
            else:
                mobius[i] = -1 * mobius[i // lpf[i]]

# Function to find the number of pairs
# such that gcd equals to 1
def gcd_pairs(a, n):

    # To store maximum number
    maxi = 0

    # To store frequency of each number
    fre = [0 for i in range(N)]

    # Find frequency and maximum number
    for i in range(n):
        fre[a[i]] += 1
        maxi = max(a[i], maxi)

    least_prime_factor()
    Mobius()

    # To store number of pairs with gcd equals to 1
    ans = 0

    # Traverse through the all possible elements
    for i in range(1, maxi + 1):
        if (mobius[i] == 0):
            continue

        temp = 0
        for j in range(i, maxi + 1, i):
            temp += fre[j]

        ans += temp * (temp - 1) // 2 * mobius[i]

    # Return the number of pairs
    return ans

# Driver code
a = [1, 2, 3, 4, 5, 6]

n = len(a)

# Function call
print(gcd_pairs(a, n))

# This code is contributed by Mohit Kumar
```

## **C#**

```
// C# program to find the number of pairs
// such that gcd equals to 1
using System;

class GFG
{
static int N = 100050;

static int []lpf = new int[N];
static int []mobius = new int[N];

// Function to calculate least
// prime factor of each number
static void least_prime_factor()
{
    for (int i = 2; i < N; i++)

        // If it is a prime number
        if (lpf[i] == 0)

            for (int j = i; j < N; j += i)

                // For all multiples which are not
                // visited yet.
                if (lpf[j] == 0)
                    lpf[j] = i;
}

// Function to find the value of Mobius function
// for all the numbers from 1 to n
static void Mobius()
{
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
}

// Function to find the number of pairs
// such that gcd equals to 1
static int gcd_pairs(int []a, int n)
{
    // To store maximum number
    int maxi = 0;

    // To store frequency of each number
    int []fre = new int[N];

    // Find frequency and maximum number
    for (int i = 0; i < n; i++)
    {
        fre[a[i]]++;
        maxi = Math.Max(a[i], maxi);
    }

    least_prime_factor();
    Mobius();

    // To store number of pairs with gcd equals to 1
    int ans = 0;

    // Traverse through the all possible elements
    for (int i = 1; i <= maxi; i++)
    {
        if (mobius[i] == 0)
            continue;

        int temp = 0;
        for (int j = i; j <= maxi; j += i)
            temp += fre[j];

        ans += temp * (temp - 1) / 2 * mobius[i];
    }

    // Return the number of pairs
    return ans;
}

// Driver code
public static void Main (String[] args)
{
    int []a = { 1, 2, 3, 4, 5, 6 };

    int n = a.Length;

    // Function call
    Console.Write(gcd_pairs(a, n));
}
}

// This code is contributed by Rajput-Ji
```

## **java 描述语言**

```
<script>

// Javascript program to find the number of pairs
// such that gcd equals to 1   
var N = 100050;

    var lpf = Array(N).fill(0);
    var mobius = Array(N).fill(0);

    // Function to calculate least
    // prime factor of each number
    function least_prime_factor() {
        for (i = 2; i < N; i++)

            // If it is a prime number
            if (lpf[i] == 0)

                for (j = i; j < N; j += i)

                    // For all multiples which are not
                    // visited yet.
                    if (lpf[j] == 0)
                        lpf[j] = i;
    }

    // Function to find the value of Mobius function
    // for all the numbers from 1 to n
    function Mobius() {
        for (i = 1; i < N; i++) {

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
    }

    // Function to find the number of pairs
    // such that gcd equals to 1
    function gcd_pairs(a , n) {
        // To store maximum number
        var maxi = 0;

        // To store frequency of each number
        var fre = Array(n+1).fill(0);

        // Find frequency and maximum number
        for (i = 0; i < n; i++) {
            fre[a[i]]++;
            maxi = Math.max(a[i], maxi);
        }

        least_prime_factor();
        Mobius();

        // To store number of pairs with gcd equals to 1
        var ans = 0;

        // Traverse through the all possible elements
        for (i = 1; i <= maxi; i++) {
            if (mobius[i] == 0)
                continue;

            var temp = 0;
            for (j = i; j <= maxi; j += i)
                temp = parseInt(temp+fre[j]);

            ans += parseInt(temp * (temp - 1) / 2 * mobius[i]);
        }

        // Return the number of pairs
        return ans;
    }

    // Driver code

        var a = [ 1, 2, 3, 4, 5, 6 ];

        var n = a.length;

        // Function call
        document.write(gcd_pairs(a, n));

// This code contributed by Rajput-Ji

</script>
```

****Output:** 

```
11
```**