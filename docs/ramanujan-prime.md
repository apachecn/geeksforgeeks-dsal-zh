# 拉马努扬质数

> 原文:[https://www.geeksforgeeks.org/ramanujan-prime/](https://www.geeksforgeeks.org/ramanujan-prime/)

第 n 个拉玛努詹素数是最小整数**R<sub>n</sub>T5** 

其中π(x)是一个[素数计数函数](https://en.wikipedia.org/wiki/Prime-counting_function)
注意，整数 **Rn** 必然是一个素数:**π(x)–π(x/2)**因此， **π(x)** 必须通过在 **x = R <sub>n</sub>** 处获得另一个素数来增加。由于**π(x)–π(x/2)**最多可以增加 1，
的范围 **R <sub>n</sub>** 为 **(2n log(2n)，4n log(4n))** 。

**拉玛努詹素数:**

> 2、11、17、29、41、47、59、67、71、97

对于给定的 **N** ，任务是首先打印 **N** 拉玛努詹素数
T5【示例:

> **输入:** N = 5
> **输出:** 2、11、17、29、41
> **输入:** N = 10
> **输出:** 2、11、17、29、41、47、59、67、71、97

**方法:**
让我们将我们的解分成几部分，
首先，我们将使用埃拉托斯特尼筛得到所有小于 10^6 的素数
现在我们将不得不找到 **π(x)** ， **π(x)** 的值是小于或等于 **x** 的素数的计数。素数以递增的顺序存储。所以我们可以进行二分搜索法运算，找出所有小于 **x** 的素数，这可以在 **O(log n)** 中完成。
现在我们有了范围**R<sub>n</sub>T19】介于:**2n log(2n)<R<sub>n</sub><4n log(4n)**所以，我们取上界，从上界到下界迭代，直到**π(I)–π(I/2)<n**，i+1 是第 n 个 Ramanujan 素数。
以下是上述方法的实施:** 

## C++

```
// CPP program to find Ramanujan numbers
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000000

// FUnction to return a vector of primes
vector<int> addPrimes()
{
    int n = MAX;

    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    bool prime[n + 1];
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= n; p++)
    {
        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    vector<int> ans;
    // Print all prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            ans.push_back(p);

    return ans;
}
// Function to find number of primes
// less than or equal to x
int pi(int x, vector<int> v)
{
    int l = 0, r = v.size() - 1, m, in = -1;

    // Binary search to find out number of
    // primes less than or equal to x
    while (l <= r) {
        m = (l + r) / 2;
        if (v[m] <= x) {
            in = m;
            l = m + 1;
        }
        else {
            r = m - 1;
        }
    }
    return in + 1;
}

// Function to find the nth ramanujan prime
int Ramanujan(int n, vector<int> v)
{
    // For n>=1, a(n)<4*n*log(4n)
    int upperbound = 4 * n * (log(4 * n) / log(2));

    // We start from upperbound and find where
    // pi(i)-pi(i/2)<n the previous number being
    // the nth ramanujan prime
    for (int i = upperbound;; i--) {
        if (pi(i, v) - pi(i / 2, v) < n)
            return 1 + i;
    }
}

// Function to find first n Ramanujan numbers
void Ramanujan_Numbers(int n)
{
    int c = 1;

    // Get the prime numbers
    vector<int> v = addPrimes();

    for (int i = 1; i <= n; i++) {
        cout << Ramanujan(i, v);
        if(i!=n)
            cout << ", ";
    }
}

// Driver code
int main()
{
    int n = 10;

    Ramanujan_Numbers(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Ramanujan numbers
import java.util.*;
class GFG
{

static int MAX = 1000000;

// FUnction to return a vector of primes
static Vector<Integer> addPrimes()
{
    int n = MAX;

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    boolean []prime= new boolean[n + 1];
    Arrays.fill(prime, true);

    for (int p = 2; p * p <= n; p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    Vector<Integer> ans = new Vector<Integer>();

    // Print all prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            ans.add(p);

    return ans;
}

// Function to find number of primes
// less than or equal to x
static int pi(int x, Vector<Integer> v)
{
    int l = 0, r = v.size() - 1, m, in = -1;

    // Binary search to find out number of
    // primes less than or equal to x
    while (l <= r)
    {
        m = (l + r) / 2;
        if (v.get(m) <= x)
        {
            in = m;
            l = m + 1;
        }
        else
        {
            r = m - 1;
        }
    }
    return in + 1;
}

// Function to find the nth ramanujan prime
static int Ramanujan(int n, Vector<Integer> v)
{
    // For n>=1, a(n)<4*n*log(4n)
    int upperbound = (int) (4 * n * (Math.log(4 * n) /
                                     Math.log(2)));

    // We start from upperbound and find where
    // pi(i)-pi(i/2)<n the previous number being
    // the nth ramanujan prime
    for (int i = upperbound;; i--)
    {
        if (pi(i, v) - pi(i / 2, v) < n)
            return 1 + i;
    }
}

// Function to find first n Ramanujan numbers
static void Ramanujan_Numbers(int n)
{
    int c = 1;

    // Get the prime numbers
    Vector<Integer> v = addPrimes();

    for (int i = 1; i <= n; i++)
    {
        System.out.print(Ramanujan(i, v));
        if(i != n)
            System.out.print(", ");
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 10;

    Ramanujan_Numbers(n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find Ramanujan numbers
from math import log, ceil
MAX = 1000000

# FUnction to return a vector of primes
def addPrimes():

    n = MAX

    # Create a boolean array "prime[0..n]"
    # and initialize all entries it as true.
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.
    prime = [True for i in range(n + 1)]

    for p in range(2, n + 1):
        if p * p > n:
            break

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            # greater than or equal to the
            # square of it. numbers which are
            # multiple of p and are less than p^2
            # are already been marked.
            for i in range(2 * p, n + 1, p):
                prime[i] = False

    ans = []

    # Print all prime numbers
    for p in range(2, n + 1):
        if (prime[p]):
            ans.append(p)

    return ans

# Function to find number of primes
# less than or equal to x
def pi(x, v):

    l, r = 0, len(v) - 1

    # Binary search to find out number of
    # primes less than or equal to x
    m, i = 0, -1
    while (l <= r):
        m = (l + r) // 2
        if (v[m] <= x):
            i = m
            l = m + 1
        else:
            r = m - 1

    return i + 1

# Function to find the nth ramanujan prime
def Ramanujan(n, v):

    # For n>=1, a(n)<4*n*log(4n)
    upperbound = ceil(4 * n * (log(4 * n) / log(2)))

    # We start from upperbound and find where
    # pi(i)-pi(i/2)<n the previous number being
    # the nth ramanujan prime
    for i in range(upperbound, -1, -1):
        if (pi(i, v) - pi(i / 2, v) < n):
            return 1 + i

# Function to find first n Ramanujan numbers
def Ramanujan_Numbers(n):
    c = 1

    # Get the prime numbers
    v = addPrimes()

    for i in range(1, n + 1):
        print(Ramanujan(i, v), end = "")
        if(i != n):
            print(end = ", ")

# Driver code
n = 10

Ramanujan_Numbers(n)

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to find Ramanujan numbers
using System;
using System.Collections.Generic;

class GFG
{
static int MAX = 1000000;

// FUnction to return a vector of primes
static List<int> addPrimes()
{
    int n = MAX;

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    Boolean []prime = new Boolean[n + 1];
    for(int i = 0; i < n + 1; i++)
        prime[i] = true;

    for (int p = 2; p * p <= n; p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p greater than
            // or equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    List<int> ans = new List<int>();

    // Print all prime numbers
    for (int p = 2; p <= n; p++)
        if (prime[p])
            ans.Add(p);

    return ans;
}

// Function to find number of primes
// less than or equal to x
static int pi(int x, List<int> v)
{
    int l = 0, r = v.Count - 1, m, i = -1;

    // Binary search to find out number of
    // primes less than or equal to x
    while (l <= r)
    {
        m = (l + r) / 2;
        if (v[m] <= x)
        {
            i = m;
            l = m + 1;
        }
        else
        {
            r = m - 1;
        }
    }
    return i + 1;
}

// Function to find the nth ramanujan prime
static int Ramanujan(int n, List<int> v)
{
    // For n>=1, a(n)<4*n*log(4n)
    int upperbound = (int) (4 * n * (Math.Log(4 * n) /
                                     Math.Log(2)));

    // We start from upperbound and find where
    // pi(i)-pi(i/2)<n the previous number being
    // the nth ramanujan prime
    for (int i = upperbound;; i--)
    {
        if (pi(i, v) - pi(i / 2, v) < n)
            return 1 + i;
    }
}

// Function to find first n Ramanujan numbers
static void Ramanujan_Numbers(int n)
{
    int c = 1;

    // Get the prime numbers
    List<int> v = addPrimes();

    for (int i = 1; i <= n; i++)
    {
        Console.Write(Ramanujan(i, v));
        if(i != n)
            Console.Write(", ");
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 10;

    Ramanujan_Numbers(n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find Ramanujan numbers

const MAX = 1000000;

// FUnction to return a vector of primes
function addPrimes()
{
    let n = MAX;

    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    let prime = new Array(n + 1).fill(true);

    for (let p = 2; p * p <= n; p++)
    {
        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (let i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    let ans = [];
    // Print all prime numbers
    for (let p = 2; p <= n; p++)
        if (prime[p])
            ans.push(p);

    return ans;
}
// Function to find number of primes
// less than or equal to x
function pi(x, v)
{
    let l = 0, r = v.length - 1, m, inn = -1;

    // Binary search to find out number of
    // primes less than or equal to x
    while (l <= r) {
        m = parseInt((l + r) / 2);
        if (v[m] <= x) {
            inn = m;
            l = m + 1;
        }
        else {
            r = m - 1;
        }
    }
    return inn + 1;
}

// Function to find the nth ramanujan prime
function Ramanujan(n, v)
{
    // For n>=1, a(n)<4*n*log(4n)
    let upperbound = 4 * n * parseInt((Math.log(4 * n) / Math.log(2)));

    // We start from upperbound and find where
    // pi(i)-pi(i/2)<n the previous number being
    // the nth ramanujan prime
    for (let i = upperbound;; i--) {
        if (pi(i, v) - pi(parseInt(i / 2), v) < n)
            return 1 + i;
    }
}

// Function to find first n Ramanujan numbers
function Ramanujan_Numbers(n)
{
    let c = 1;

    // Get the prime numbers
    let v = addPrimes();

    for (let i = 1; i <= n; i++) {
        document.write(Ramanujan(i, v));
        if(i!=n)
            document.write(", ");
    }
}

// Driver code
    let n = 10;

    Ramanujan_Numbers(n);

</script>
```

**输出:**

```
2, 11, 17, 29, 41, 47, 59, 67, 71, 97
```