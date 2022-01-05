# 打印数字时，不要让两个连续的数字是同素的，并且每三个连续的数字是同素的

> 原文:[https://www . geeksforgeeks . org/print-numbers-so-no-两个连续的数字是-co-prime-并且每三个连续的数字是-co-prime/](https://www.geeksforgeeks.org/print-numbers-such-that-no-two-consecutive-numbers-are-co-prime-and-every-three-consecutive-numbers-are-co-prime/)

给定一个整数 **N** ，任务是打印 **N** 整数 **≤ 10 <sup>9</sup>** ，使得这些整数中没有两个连续的是同素的，并且每 3 个连续的是同素的。

**示例:**

> **输入:**N = 3
> T3】输出: 6 15 10
> 
> **输入:**N = 4
> T3】输出: 6 15 35 14

**进场:**

*   我们可以将连续的素数相乘，最后一个数只需乘以 **gcd(last，last-1) * 2** 。我们这样做是为了使**(n–1)<sub>第</sub>T5】号、**第 n**号和**第 1**号也能遵循问题陈述中提到的属性。**
*   问题的另一个重要部分是数字应该是 **≤ 10 <sup>9</sup>** 。如果你只是把连续的质数相乘，在 3700 个左右的数字之后，数值会越过 10 <sup>9</sup> 。所以我们只需要用那些质数，它们的乘积不会越过 10 <sup>9</sup> 。
*   为了有效地做到这一点，考虑少量的质数，比如前 550 个质数，并以这样一种方式选择它们，使得在制作产品时，没有数字被重复。我们首先连续选择每个素数，然后选择间隔为 2 和 3 的素数，以此类推。通过这样做，我们已经确保没有数字被重复。

> 所以我们会选择
> 5，11，17，…
> 下次我们可以从 7 开始选择，
> 7，13，19，…

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define limit 1000000000
#define MAX_PRIME 2000000
#define MAX 1000000
#define I_MAX 50000

map<int, int> mp;

int b[MAX];
int p[MAX];
int j = 0;
bool prime[MAX_PRIME + 1];

// Function to generate Sieve of
// Eratosthenes
void SieveOfEratosthenes(int n)
{
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Add the prime numbers to the array b
    for (int p = 2; p <= n; p++) {
        if (prime[p]) {
            b[j++] = p;
        }
    }
}

// Function to return the gcd of a and b
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to print the required
// sequence of integers
void printSeries(int n)
{
    SieveOfEratosthenes(MAX_PRIME);

    int i, g, k, l, m, d;
    int ar[I_MAX + 2];

    for (i = 0; i < j; i++) {
        if ((b[i] * b[i + 1]) > limit)
            break;

        // Including the primes in a series
        // of primes which will be later
        // multiplied
        p[i] = b[i];

        // This is done to mark a product
        // as existing
        mp[b[i] * b[i + 1]] = 1;
    }

    // Maximum number of primes that we consider
    d = 550;
    bool flag = false;

    // For different interval
    for (k = 2; (k < d - 1) && !flag; k++) {

        // For different starting index of jump
        for (m = 2; (m < d) && !flag; m++) {

            // For storing the numbers
            for (l = m + k; l < d; l += k) {

                // Checking for occurrence of a
                // product. Also checking for the
                // same prime occurring consecutively
                if (((b[l] * b[l + k]) < limit)
                    && (l + k) < d && p[i - 1] != b[l + k]
                    && p[i - 1] != b[l] && mp[b[l] * b[l + k]] != 1) {
                    if (mp[p[i - 1] * b[l]] != 1) {

                        // Including the primes in a
                        // series of primes which will
                        // be later multiplied
                        p[i] = b[l];
                        mp[p[i - 1] * b[l]] = 1;
                        i++;
                    }
                }

                if (i >= I_MAX) {
                    flag = true;
                    break;
                }
            }
        }
    }

    for (i = 0; i < n; i++)
        ar[i] = p[i] * p[i + 1];

    for (i = 0; i < n - 1; i++)
        cout << ar[i] << " ";

    g = gcd(ar[n - 1], ar[n - 2]);
    cout << g * 2 << endl;
}

// Driver Code
int main()
{
    int n = 4;

    printSeries(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int limit = 1000000000;
static int MAX_PRIME = 2000000;
static int MAX = 1000000;
static int I_MAX = 50000;

static HashMap<Integer,
               Integer> mp = new HashMap<Integer,
                                         Integer>();

static int []b = new int[MAX];
static int []p = new int[MAX];
static int j = 0;
static boolean []prime = new boolean[MAX_PRIME + 1];

// Function to generate Sieve of
// Eratosthenes
static void SieveOfEratosthenes(int n)
{
    for(int i = 0; i < MAX_PRIME + 1; i++)
        prime[i] = true;

    for (int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Add the prime numbers to the array b
    for (int p = 2; p <= n; p++)
    {
        if (prime[p])
        {
            b[j++] = p;
        }
    }
}

// Function to return the gcd of a and b
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to print the required
// sequence of integers
static void printSeries(int n)
{
    SieveOfEratosthenes(MAX_PRIME);

    int i, g, k, l, m, d;
    int []ar = new int[I_MAX + 2];

    for (i = 0; i < j; i++)
    {
        if ((b[i] * b[i + 1]) > limit)
            break;

        // Including the primes in a series
        // of primes which will be later
        // multiplied
        p[i] = b[i];

        // This is done to mark a product
        // as existing
        mp.put(b[i] * b[i + 1], 1);
    }

    // Maximum number of primes that we consider
    d = 550;
    boolean flag = false;

    // For different interval
    for (k = 2; (k < d - 1) && !flag; k++)
    {

        // For different starting index of jump
        for (m = 2; (m < d) && !flag; m++)
        {

            // For storing the numbers
            for (l = m + k; l < d; l += k)
            {

                // Checking for occurrence of a
                // product. Also checking for the
                // same prime occurring consecutively
                if (((b[l] * b[l + k]) < limit) &&
                      mp.containsKey(b[l] * b[l + k]) &&
                      mp.containsKey(p[i - 1] * b[l]) &&
                      (l + k) < d && p[i - 1] != b[l + k] &&
                                         p[i - 1] != b[l] &&
                             mp.get(b[l] * b[l + k]) != 1)
                    {
                    if (mp.get(p[i - 1] * b[l]) != 1)
                    {

                        // Including the primes in a
                        // series of primes which will
                        // be later multiplied
                        p[i] = b[l];
                        mp.put(p[i - 1] * b[l], 1);
                        i++;
                    }
                }

                if (i >= I_MAX)
                {
                    flag = true;
                    break;
                }
            }
        }
    }

    for (i = 0; i < n; i++)
        ar[i] = p[i] * p[i + 1];

    for (i = 0; i < n - 1; i++)
        System.out.print(ar[i]+" ");

    g = gcd(ar[n - 1], ar[n - 2]);
    System.out.print(g * 2);
}

// Driver Code
public static void main(String[] args)
{
    int n = 4;
    printSeries(n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
limit = 1000000000
MAX_PRIME = 2000000
MAX = 1000000
I_MAX = 50000

mp = {}

b = [0] * MAX
p = [0] * MAX
j = 0
prime = [True] * (MAX_PRIME + 1)

# Function to generate Sieve of
# Eratosthenes
def SieveOfEratosthenes(n):
    global j
    p = 2
    while p * p <= n:

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):
            for i in range(p * p, n + 1, p):
                prime[i] = False
        p += 1

    # Add the prime numbers to the array b
    for p in range(2, n + 1):
        if (prime[p]):
            b[j] = p
            j += 1

# Function to return
# the gcd of a and b
def gcd(a, b):

    if (b == 0):
        return a
    return gcd(b, a % b)

# Function to print the required
# sequence of integers
def printSeries(n):

    SieveOfEratosthenes(MAX_PRIME)

    ar = [0] * (I_MAX + 2)

    for i in range(j):
        if ((b[i] * b[i + 1]) > limit):
            break

        # Including the primes in a series
        # of primes which will be later
        # multiplied
        p[i] = b[i]

        # This is done to mark a product
        # as existing
        mp[b[i] * b[i + 1]] = 1

    # Maximum number of
    # primes that we consider
    d = 550
    flag = False

    # For different interval
    k = 2
    while (k < d - 1) and not flag:

        # For different starting
        # index of jump
        m = 2
        while (m < d) and not flag:

            # For storing the numbers
            for l in range(m + k, d, k):

                # Checking for occurrence of a
                # product. Also checking for the
                # same prime occurring consecutively
                if (((b[l] * b[l + k]) < limit) and
                    (l + k) < d and p[i - 1] != b[l + k] and
                     p[i - 1] != b[l] and
                     ((b[l] * b[l + k] in mp) and
                     mp[b[l] * b[l + k]] != 1)):

                    if (mp[p[i - 1] * b[l]] != 1):

                        # Including the primes in a
                        # series of primes which will
                        # be later multiplied
                        p[i] = b[l]
                        mp[p[i - 1] * b[l]] = 1
                        i += 1

                if (i >= I_MAX):
                    flag = True
                    break
            m += 1
        k += 1

    for i in range(n):
        ar[i] = p[i] * p[i + 1]

    for i in range(n - 1):
        print(ar[i], end = " ")

    g = gcd(ar[n - 1], ar[n - 2])
    print(g * 2)

# Driver Code
if __name__ == "__main__":
    n = 4
    printSeries(n)

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;            

class GFG
{

static int limit = 1000000000;
static int MAX_PRIME = 2000000;
static int MAX = 1000000;
static int I_MAX = 50000;

static Dictionary<int,
                  int> mp = new Dictionary<int,
                                           int>();

static int []b = new int[MAX];
static int []p = new int[MAX];
static int j = 0;
static bool []prime = new bool[MAX_PRIME + 1];

// Function to generate Sieve of
// Eratosthenes
static void SieveOfEratosthenes(int n)
{
    for(int i = 0; i < MAX_PRIME + 1; i++)
        prime[i] = true;

    for (int p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {
            for (int i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Add the prime numbers to the array b
    for (int p = 2; p <= n; p++)
    {
        if (prime[p])
        {
            b[j++] = p;
        }
    }
}

// Function to return the gcd of a and b
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to print the required
// sequence of integers
static void printSeries(int n)
{
    SieveOfEratosthenes(MAX_PRIME);

    int i, g, k, l, m, d;
    int []ar = new int[I_MAX + 2];

    for (i = 0; i < j; i++)
    {
        if ((b[i] * b[i + 1]) > limit)
            break;

        // Including the primes in a series
        // of primes which will be later
        // multiplied
        p[i] = b[i];

        // This is done to mark a product
        // as existing
        mp.Add(b[i] * b[i + 1], 1);
    }

    // Maximum number of primes that we consider
    d = 550;
    bool flag = false;

    // For different interval
    for (k = 2; (k < d - 1) && !flag; k++)
    {

        // For different starting index of jump
        for (m = 2; (m < d) && !flag; m++)
        {

            // For storing the numbers
            for (l = m + k; l < d; l += k)
            {

                // Checking for occurrence of a
                // product. Also checking for the
                // same prime occurring consecutively
                if (((b[l] * b[l + k]) < limit) &&
                    mp.ContainsKey(b[l] * b[l + k]) &&
                    mp.ContainsKey(p[i - 1] * b[l]) &&
                    (l + k) < d && p[i - 1] != b[l + k] &&
                                       p[i - 1] != b[l] &&
                            mp[b[l] * b[l + k]] != 1)
                    {
                    if (mp[p[i - 1] * b[l]] != 1)
                    {

                        // Including the primes in a
                        // series of primes which will
                        // be later multiplied
                        p[i] = b[l];
                        mp.Add(p[i - 1] * b[l], 1);
                        i++;
                    }
                }

                if (i >= I_MAX)
                {
                    flag = true;
                    break;
                }
            }
        }
    }

    for (i = 0; i < n; i++)
        ar[i] = p[i] * p[i + 1];

    for (i = 0; i < n - 1; i++)
        Console.Write(ar[i] + " ");

    g = gcd(ar[n - 1], ar[n - 2]);
    Console.Write(g * 2);
}

// Driver Code
public static void Main(String[] args)
{
    int n = 4;
    printSeries(n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let limit = 1000000000
let MAX_PRIME = 2000000
let MAX = 1000000
let I_MAX = 50000

let mp = new Map();

let b = new Array(MAX);
let p = new Array(MAX);
let j = 0;
let prime = new Array(MAX_PRIME + 1);

// Function to generate Sieve of
// Eratosthenes
function SieveOfEratosthenes(n)
{
    prime.fill(true);

    for (let p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {
            for (let i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Add the prime numbers to the array b
    for (let p = 2; p <= n; p++) {
        if (prime[p]) {
            b[j++] = p;
        }
    }
}

// Function to return the gcd of a and b
function gcd(a, b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to print the required
// sequence of integers
function printSeries(n)
{
    SieveOfEratosthenes(MAX_PRIME);

    let i, g, k, l, m, d;
    let ar = new Array(I_MAX + 2);

    for (i = 0; i < j; i++) {
        if ((b[i] * b[i + 1]) > limit)
            break;

        // Including the primes in a series
        // of primes which will be later
        // multiplied
        p[i] = b[i];

        // This is done to mark a product
        // as existing
        mp[b[i] * b[i + 1]] = 1;
    }

    // Maximum number of primes that we consider
    d = 550;
    let flag = false;

    // For different interval
    for (k = 2; (k < d - 1) && !flag; k++) {

        // For different starting index of jump
        for (m = 2; (m < d) && !flag; m++) {

            // For storing the numbers
            for (l = m + k; l < d; l += k) {

                // Checking for occurrence of a
                // product. Also checking for the
                // same prime occurring consecutively
                if (((b[l] * b[l + k]) < limit)
                    && (l + k) < d && p[i - 1] != b[l + k]
                    && p[i - 1] != b[l] && mp[b[l] * b[l + k]] != 1) {
                    if (mp[p[i - 1] * b[l]] != 1) {

                        // Including the primes in a
                        // series of primes which will
                        // be later multiplied
                        p[i] = b[l];
                        mp[p[i - 1] * b[l]] = 1;
                        i++;
                    }
                }

                if (i >= I_MAX) {
                    flag = true;
                    break;
                }
            }
        }
    }

    for (i = 0; i < n; i++)
        ar[i] = p[i] * p[i + 1];

    for (i = 0; i < n - 1; i++)
        document.write(ar[i] + " ");

    g = gcd(ar[n - 1], ar[n - 2]);
    document.write( g * 2 + "<br>");
}

// Driver Code

let n = 4;

printSeries(n);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
6 15 35 14
```

**另一种方法:**使用厄拉多塞的[筛列出所有 600 万以内的质数。我们知道基本条件，即 N = 3 形式{6，10，15}。
因此，我们使用这三个值来生成序列的进一步项。
像{2，3，5}一样，这些素数不能用来生成序列，因为它们已经在{6，10，15}中使用了。我们也不能使用{7，11}，我们稍后会看到。
现在我们有了一个质数列表{13，17，19，23，29，…}。我们取第一个素数乘以
6，第二个乘以 15，第三个乘以 10，第四个乘以 6，以此类推…](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

```
13 * 6, 17 * 15, 19 * 10, 23 * 6, 29 * 15, ........upto N - 2 terms.
(N - 1)th term = (N - 1)th prime * 7.
Nth term = 7 * 11.
again, first term = first term * 11 to make 1st and last noncoprime.
For example, N = 5
6 * 11 * 13, 15 * 17, 10 * 19, 11 * 19, 7 * 11
```

现在我们看到，我们不能使用列表中的 7 和 11，因为它们用于生成最后一项和第二项。
下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
const int MAX = 620000;
int prime[MAX];

// Function for Sieve of Eratosthenes
void Sieve()
{
    for (int i = 2; i < MAX; i++) {
        if (prime[i] == 0) {
            for (int j = 2 * i; j < MAX; j += i) {
                prime[j] = 1;
            }
        }
    }
}

// Function to print the required sequence
void printSequence(int n)
{
    Sieve();
    vector<int> v, u;

    // Store only the required primes
    for (int i = 13; i < MAX; i++) {
        if (prime[i] == 0) {
            v.push_back(i);
        }
    }
    // Base condition
    if (n == 3) {
        cout << 6 << " " << 10 << " " << 15;
        return;
    }

    int k;
    for (k = 0; k < n - 2; k++) {

        // First integer in the list
        if (k % 3 == 0) {
            u.push_back(v[k] * 6);
        }

        // Second integer in the list
        else if (k % 3 == 1) {

            u.push_back(v[k] * 15);
        }

        // Third integer in the list
        else {
            u.push_back(v[k] * 10);
        }
    }
    k--;

    // Generate (N - 1)th term
    u.push_back(v[k] * 7);

    // Generate Nth term
    u.push_back(7 * 11);

    // Modify first term
    u[0] = u[0] * 11;

    // Print the sequence
    for (int i = 0; i < u.size(); i++) {
        cout << u[i] << " ";
    }
}

// Driver code
int main()
{
    int n = 4;
    printSequence(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    static int MAX = 620000;
    static int[] prime = new int[MAX];

    // Function for Sieve of Eratosthenes
    static void Sieve()
    {
        for (int i = 2; i < MAX; i++)
        {
            if (prime[i] == 0)
            {
                for (int j = 2 * i;
                         j < MAX; j += i)
                {
                    prime[j] = 1;
                }
            }
        }
    }

    // Function to print the required sequence
    static void printSequence(int n)
    {
        Sieve();
        Vector<Integer> v = new Vector<Integer>();
        Vector<Integer> u = new Vector<Integer>();

        // Store only the required primes
        for (int i = 13; i < MAX; i++)
        {
            if (prime[i] == 0)
            {
                v.add(i);
            }
        }

        // Base condition
        if (n == 3)
        {
            System.out.print(6 + " " + 10 + " " + 15);
            return;
        }

        int k;
        for (k = 0; k < n - 2; k++)
        {

            // First integer in the list
            if (k % 3 == 0)
            {
                u.add(v.get(k) * 6);
            }

            // Second integer in the list
            else if (k % 3 == 1)
            {

                u.add(v.get(k) * 15);
            }

            // Third integer in the list
            else
            {
                u.add(v.get(k) * 10);
            }
        }
        k--;

        // Generate (N - 1)th term
        u.add(v.get(k) * 7);

        // Generate Nth term
        u.add(7 * 11);

        // Modify first term
        u.set(0, u.get(0) * 11);

        // Print the sequence
        for (int i = 0; i < u.size(); i++)
        {
            System.out.print(u.get(i) + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4;
        printSequence(n);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach
MAX = 620000
prime = [0] * MAX

# Function for Sieve of Eratosthenes
def Sieve():

    for i in range(2, MAX):
        if (prime[i] == 0):
            for j in range(2 * i, MAX, i):
                prime[j] = 1

# Function to print the required sequence
def printSequence (n):

    Sieve()
    v = []
    u = []

    # Store only the required primes
    for i in range(13, MAX):
        if (prime[i] == 0):
            v.append(i)

    # Base condition
    if (n == 3):
        print(6, 10, 15)
        return

    k = 0
    for k in range(n - 2):

        # First integer in the list
        if (k % 3 == 0):
            u.append(v[k] * 6)

        # Second integer in the list
        elif (k % 3 == 1):
            u.append(v[k] * 15)

        # Third integer in the list
        else:
            u.append(v[k] * 10)

    # Generate (N - 1)th term
    u.append(v[k] * 7)

    # Generate Nth term
    u.append(7 * 11)

    # Modify first term
    u[0] = u[0] * 11

    # Print the sequence
    print(*u)

# Driver code
if __name__ == '__main__':

    n = 4
    printSequence(n)

# This code is contributed by himanshu77
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    static int MAX = 620000;
    static int[] prime = new int[MAX];

    // Function for Sieve of Eratosthenes
    static void Sieve()
    {
        for (int i = 2; i < MAX; i++)
        {
            if (prime[i] == 0)
            {
                for (int j = 2 * i;
                        j < MAX; j += i)
                {
                    prime[j] = 1;
                }
            }
        }
    }

    // Function to print the required sequence
    static void printSequence(int n)
    {
        Sieve();
        List<int> v = new List<int>();
        List<int> u = new List<int>();

        // Store only the required primes
        for (int i = 13; i < MAX; i++)
        {
            if (prime[i] == 0)
            {
                v.Add(i);
            }
        }

        // Base condition
        if (n == 3)
        {
            Console.Write(6 + " " + 10 + " " + 15);
            return;
        }

        int k;
        for (k = 0; k < n - 2; k++)
        {

            // First integer in the list
            if (k % 3 == 0)
            {
                u.Add(v[k] * 6);
            }

            // Second integer in the list
            else if (k % 3 == 1)
            {

                u.Add(v[k] * 15);
            }

            // Third integer in the list
            else
            {
                u.Add(v[k] * 10);
            }
        }
        k--;

        // Generate (N - 1)th term
        u.Add(v[k] * 7);

        // Generate Nth term
        u.Add(7 * 11);

        // Modify first term
        u[0] = u[0] * 11;

        // Print the sequence
        for (int i = 0; i < u.Count; i++)
        {
            Console.Write(u[i] + " ");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 4;
        printSequence(n);
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

    let MAX = 620000;
    let prime = new Array(MAX);
    for(let i=0;i<MAX;i++)
    {
        prime[i]=0;
    }

    // Function for Sieve of Eratosthenes
    function Sieve()
    {
        for (let i = 2; i < MAX; i++)
        {
            if (prime[i] == 0)
            {
                for (let j = 2 * i;
                         j < MAX; j += i)
                {
                    prime[j] = 1;
                }
            }
        }
    }

    // Function to print the required sequence
    function printSequence(n)
    {
        Sieve();
        let v = [];
        let u = [];

        // Store only the required primes
        for (let i = 13; i < MAX; i++)
        {
            if (prime[i] == 0)
            {
                v.push(i);
            }
        }

        // Base condition
        if (n == 3)
        {
            document.write(6 + " " + 10 + " " + 15);
            return;
        }

        let k;
        for (k = 0; k < n - 2; k++)
        {

            // First integer in the list
            if (k % 3 == 0)
            {
                u.push(v[k] * 6);
            }

            // Second integer in the list
            else if (k % 3 == 1)
            {

                u.push(v[k] * 15);
            }

            // Third integer in the list
            else
            {
                u.push(v[k] * 10);
            }
        }
        k--;

        // Generate (N - 1)th term
        u.push(v[k] * 7);

        // Generate Nth term
        u.push(7 * 11);

        // Modify first term
        u[0] = u[0] * 11;

        // Print the sequence
        for (let i = 0; i < u.length; i++)
        {
            document.write(u[i] + " ");
        }
    }

    // Driver code
    let n = 4;
    printSequence(n);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
858 255 119 77
```