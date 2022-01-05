# 无奇素数的素数之和

> 原文:[https://www . geesforgeks . org/不带奇数素数的素数之和/](https://www.geeksforgeeks.org/sum-of-prime-numbers-without-odd-prime-digits/)

给定一个整数 **N** 。任务是找到第一个不包含任何奇数素数的素数的和 **N** 。
这样的素数有 2、11、19、29、41 ……
**例:**

> **输入:** N = 2
> **输出:** 13
> 2 + 11 = 13
> **输入:** N = 7
> **输出:** 252

**进场:**

*   我们首先使用厄拉多塞的[筛来存储所有质数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   接下来检查每个质数是否有奇数个质数。
*   如果没有这样的数字，那么我们将把这个质数包括到我们需要的答案中
*   继续上面的步骤，直到我们得到 N 个这样的素数

以下是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

#define MAX 100005

// Find all prime numbers
vector<int> addPrimes()
{
    int n = MAX;

    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= n; p++) {

        if (prime[p] == true) {
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
    vector<int> ans;
    // Store all prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            ans.push_back(p);

    return ans;
}

// Function to check if a digit is odd prime or not
bool is_prime(int n)
{
    return (n == 3 || n == 5 || n == 7);
}

// Function to find sum
int find_Sum(int n)
{
    // To store required answer
    int sum = 0;

    // Get all prime numbers
    vector<int> v = addPrimes();

    // Traverse through all the prime numbers
    for (int i = 0; i < v.size() and n; i++)
    {
        // Flag stores 1 if a number does
        // not contain any odd primes
        int flag = 1;
        int a = v[i];

        // Find all digits of a number
        while (a != 0)
        {
            int d = a % 10;
            a = a / 10;
            if (is_prime(d)) {
                flag = 0;
                break;
            }
        }

        // If number does not contain any odd primes
        if (flag==1)
        {
            n--;
            sum = sum + v[i];
        }
    }

    // Return the required answer
    return sum;
}

// Driver code
int main()
{
    int n = 7;

    // Function call
    cout << find_Sum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG
{
static int MAX = 100005;

// Find all prime numbers
static Vector<Integer> addPrimes()
{
    int n = MAX;

    boolean []prime = new boolean[n + 1];
    Arrays.fill(prime, true);

    for (int p = 2; p * p <= n; p++)
    {
        if (prime[p] == true)
        {
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
    Vector<Integer> ans = new Vector<Integer>();

    // Store all prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            ans.add(p);

    return ans;
}

// Function to check if a digit
// is odd prime or not
static boolean is_prime(int n)
{
    return (n == 3 || n == 5 || n == 7);
}

// Function to find sum
static int find_Sum(int n)
{
    // To store required answer
    int sum = 0;

    // Get all prime numbers
    Vector<Integer> v = addPrimes();

    // Traverse through all the prime numbers
    for (int i = 0; i < v.size() && n > 0; i++)
    {
        // Flag stores 1 if a number does
        // not contain any odd primes
        int flag = 1;
        int a = v.get(i);

        // Find all digits of a number
        while (a != 0)
        {
            int d = a % 10;
            a = a / 10;
            if (is_prime(d))
            {
                flag = 0;
                break;
            }
        }

        // If number does not contain
        // any odd primes
        if (flag == 1)
        {
            n--;
            sum = sum + v.get(i);
        }
    }

    // Return the required answer
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int n = 7;

    // Function call
    System.out.println(find_Sum(n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for above approach
MAX = 100005

def addPrimes():
    n = MAX

    prime = [True for i in range(n + 1)]

    for p in range(2, n + 1):

        if p * p > n:
            break

        if (prime[p] == True):
            for i in range(2 * p, n + 1, p):
                prime[i] = False

    ans = []

    # Store all prime numbers
    for p in range(2, n + 1):
        if (prime[p]):
            ans.append(p)

    return ans

# Function to check if
# a digit is odd prime or not
def is_prime(n):
    if n in [3, 5, 7]:
        return True
    return False

# Function to find sum
def find_Sum(n):

    # To store required answer
    Sum = 0

    # Get all prime numbers
    v = addPrimes()

    # Traverse through all the prime numbers
    for i in range(len(v)):

        # Flag stores 1 if a number does
        # not contain any odd primes
        flag = 1
        a = v[i]

        # Find all digits of a number
        while (a != 0):

            d = a % 10;
            a = a // 10;
            if (is_prime(d)):
                flag = 0
                break

        # If number does not contain any odd primes
        if (flag == 1):
            n -= 1
            Sum = Sum + v[i]
        if n == 0:
            break

    # Return the required answer
    return Sum

# Driver code
n = 7

# Function call
print(find_Sum(n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

class GFG
{
static int MAX = 100005;

// Find all prime numbers
static List<int> addPrimes()
{
    int n = MAX;

    Boolean []prime = new Boolean[n + 1];
    for(int i = 0; i < n + 1; i++)
        prime[i]=true;

    for (int p = 2; p * p <= n; p++)
    {
        if (prime[p] == true)
        {
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
    List<int> ans = new List<int>();

    // Store all prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            ans.Add(p);

    return ans;
}

// Function to check if a digit
// is odd prime or not
static Boolean is_prime(int n)
{
    return (n == 3 ||
            n == 5 || n == 7);
}

// Function to find sum
static int find_Sum(int n)
{
    // To store required answer
    int sum = 0;

    // Get all prime numbers
    List<int> v = addPrimes();

    // Traverse through all the prime numbers
    for (int i = 0;
             i < v.Count && n > 0; i++)
    {
        // Flag stores 1 if a number does
        // not contain any odd primes
        int flag = 1;
        int a = v[i];

        // Find all digits of a number
        while (a != 0)
        {
            int d = a % 10;
            a = a / 10;
            if (is_prime(d))
            {
                flag = 0;
                break;
            }
        }

        // If number does not contain
        // any odd primes
        if (flag == 1)
        {
            n--;
            sum = sum + v[i];
        }
    }

    // Return the required answer
    return sum;
}

// Driver code
public static void Main(String[] args)
{
    int n = 7;

    // Function call
    Console.WriteLine(find_Sum(n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

const MAX = 100005;

// Find all prime numbers
function addPrimes()
{
    let n = MAX;

    let prime = new Array(n + 1).fill(true);

    for (let p = 2; p * p <= n; p++) {

        if (prime[p] == true) {
            for (let i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
    let ans = [];
    // Store all prime numbers
    for (let p = 2; p <= n; p++)
        if (prime[p])
            ans.push(p);

    return ans;
}

// Function to check if a digit is odd prime or not
function is_prime(n)
{
    return (n == 3 || n == 5 || n == 7);
}

// Function to find sum
function find_Sum(n)
{
    // To store required answer
    let sum = 0;

    // Get all prime numbers
    let v = addPrimes();

    // Traverse through all the prime numbers
    for (let i = 0; i < v.length && n > 0; i++)
    {
        // Flag stores 1 if a number does
        // not contain any odd primes
        let flag = 1;
        let a = v[i];

        // Find all digits of a number
        while (a != 0)
        {
            let d = a % 10;
            a = parseInt(a / 10);
            if (is_prime(d)) {
                flag = 0;
                break;
            }
        }

        // If number does not contain any odd primes
        if (flag==1)
        {
            n--;
            sum = sum + v[i];
        }
    }

    // Return the required answer
    return sum;
}

// Driver code
    let n = 7;

    // Function call
    document.write(find_Sum(n));

</script>
```

**输出:**

```
252
```