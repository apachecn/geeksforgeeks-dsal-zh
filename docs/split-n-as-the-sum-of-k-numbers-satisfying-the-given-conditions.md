# 将 N 拆分为满足给定条件的 K 个数之和

> 原文:[https://www . geesforgeks . org/split-n-as-sum-k-numbers-满足给定条件/](https://www.geeksforgeeks.org/split-n-as-the-sum-of-k-numbers-satisfying-the-given-conditions/)

给定一个整数 **N** ，任务是将给定的数表示为 **K** 个数的和，其中至少**K–1**个数是不同的，并且是 2 个素数的乘积。如果没有可能的答案，打印 **-1** 。

**示例:**

> **输入:** N = 52，K = 5
> **输出:** 6 10 14 15 7
> **说明:**
> N = 52 可以表示为 6 10 14 15 2，其中 15 = 3 * 5，14 = 2*7，10 = 2*5，6 = 2*3，即至少 4 个数是 2 个不同素数的乘积。
> 
> **输入:** N = 44 K = 5
> **输出:** -1
> **说明:**无法将 N 表示为不同数字的乘积。

**方法:**按照以下步骤解决问题:

*   使用厄拉多塞[筛将所有质数存储在一个向量中。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   迭代存储的素数，并将每对素数的乘积存储在另一个向量 *prod 中。*
*   打印*戳*向量的第一个**K–1**元素
*   如果*戳*向量的前**K–1**元素之和大于 **N** ，则打印 **-1** 。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Vector to store prime numbers
vector<int> primes;

// Function to generate prime
// numbers using SieveOfEratosthenes
void SieveOfEratosthenes()
{
    // Boolean array to store primes
    bool prime[10005];

    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= 1000; p++) {

        // If p is a prime
        if (prime[p] == true) {

            // Mark all its multiples as non-prime
            for (int i = p * p; i <= 1000; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers
    for (int p = 2; p <= 1000; p++)
        if (prime[p])
            primes.push_back(p);
}

// Function to generate n as the sum
// of k numbers where atleast K - 1
// are distinct and are product of 2 primes
void generate(int n, int k)
{
    // Stores the product of every
    // pair of prime number
    vector<long long> prod;

    SieveOfEratosthenes();

    int l = primes.size();

    for (int i = 0; i < l; i++) {
        for (int j = i + 1; j < l; j++) {
            if (primes[i] * primes[j] > 0)
                prod.push_back(primes[i]
                               * primes[j]);
        }
    }

    // Sort the products
    sort(prod.begin(), prod.end());

    int sum = 0;
    for (int i = 0; i < k - 1; i++)
        sum += prod[i];

    // If sum exceeds n
    if (sum > n)
        cout << "-1";

    // Otherwise, print the k
    // required numbers
    else {
        for (int i = 0; i < k - 1; i++) {
            cout << prod[i] << ", ";
        }
        cout << n - sum << "\n";
    }
}

// Driver Code
int main()
{
    int n = 52, k = 5;
    generate(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Vector to store prime numbers
static Vector<Integer> primes = new Vector<>();

// Function to generate prime
// numbers using SieveOfEratosthenes
static void SieveOfEratosthenes()
{
    // Boolean array to store primes
    boolean []prime = new boolean[10005];
    Arrays.fill(prime, true);

    for (int p = 2; p * p <= 1000; p++)
    {

        // If p is a prime
        if (prime[p] == true)
        {

            // Mark all its multiples as non-prime
            for (int i = p * p; i <= 1000; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers
    for (int p = 2; p <= 1000; p++)
        if (prime[p])
            primes.add(p);
}

// Function to generate n as the sum
// of k numbers where atleast K - 1
// are distinct and are product of 2 primes
static void generate(int n, int k)
{
    // Stores the product of every
    // pair of prime number
    Vector<Integer> prod = new Vector<>();
    SieveOfEratosthenes();

    int l = primes.size();

    for (int i = 0; i < l; i++)
    {
        for (int j = i + 1; j < l; j++)
        {
            if (primes.get(i) * primes.get(j) > 0)
                prod.add(primes.get(i) *
                         primes.get(j));
        }
    }

    // Sort the products
    Collections.sort(prod);

    int sum = 0;
    for (int i = 0; i < k - 1; i++)
        sum += prod.get(i);

    // If sum exceeds n
    if (sum > n)
        System.out.print("-1");

    // Otherwise, print the k
    // required numbers
    else
    {
        for (int i = 0; i < k - 1; i++)
        {
            System.out.print(prod.get(i) + ", ");
        }
        System.out.print(n - sum + "\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int n = 52, k = 5;
    generate(n, k);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# list to store prime numbers
primes = []

# Function to generate prime
# numbers using SieveOfEratosthenes
def SieveOfEratosthenes():

    # Boolean array to store primes
    prime = [True] * 10005

    p = 2
    while p * p <= 1000:

        # If p is a prime
        if (prime[p] == True):

            # Mark all its multiples as non-prime
            for i in range(p * p, 1001, p):
                prime[i] = False

        p += 1

    # Print all prime numbers
    for p in range(2, 1001):
        if (prime[p]):
            primes.append(p)

# Function to generate n as the sum
# of k numbers where atleast K - 1
# are distinct and are product of 2 primes
def generate(n, k):

    # Stores the product of every
    # pair of prime number
    prod = []

    SieveOfEratosthenes()

    l = len(primes)

    for i in range(l):
        for j in range(i + 1, l):
            if (primes[i] * primes[j] > 0):
                prod.append(primes[i] *
                            primes[j])

    # Sort the products
    prod.sort()

    sum = 0
    for i in range(k - 1):
        sum += prod[i]

    # If sum exceeds n
    if (sum > n):
        print ("-1")

    # Otherwise, print the k
    # required numbers
    else:
        for i in range(k - 1):
            print(prod[i], end = ", ")

        print(n - sum)

# Driver Code
if __name__ == "__main__":

    n = 52
    k = 5

    generate(n, k)

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// List to store prime numbers
static List<int> primes = new List<int>();

// Function to generate prime
// numbers using SieveOfEratosthenes
static void SieveOfEratosthenes()
{

    // Boolean array to store primes
    bool []prime = new bool[10005];
    for(int i = 0; i < 10005; i++)
        prime[i] = true;

    for(int p = 2; p * p <= 1000; p++)
    {

        // If p is a prime
        if (prime[p] == true)
        {

            // Mark all its multiples as non-prime
            for(int i = p * p; i <= 1000; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers
    for(int p = 2; p <= 1000; p++)
        if (prime[p])
            primes.Add(p);
}

// Function to generate n as the sum
// of k numbers where atleast K - 1
// are distinct and are product of 2 primes
static void generate(int n, int k)
{

    // Stores the product of every
    // pair of prime number
    List<int> prod = new List<int>();
    SieveOfEratosthenes();

    int l = primes.Count;

    for(int i = 0; i < l; i++)
    {
        for(int j = i + 1; j < l; j++)
        {
            if (primes[i] * primes[j] > 0)
                prod.Add(primes[i] *
                         primes[j]);
        }
    }

    // Sort the products
    prod.Sort();

    int sum = 0;
    for(int i = 0; i < k - 1; i++)
        sum += prod[i];

    // If sum exceeds n
    if (sum > n)
        Console.Write("-1");

    // Otherwise, print the k
    // required numbers
    else
    {
        for (int i = 0; i < k - 1; i++)
        {
            Console.Write(prod[i] + ", ");
        }
        Console.Write(n - sum + "\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int n = 52, k = 5;

    generate(n, k);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Array to store prime numbers
let primes = new Array();

// Function to generate prime
// numbers using SieveOfEratosthenes
function SieveOfEratosthenes()
{
    // array to store primes
    let prime = new Array(10005);

    prime.fill(true);

    for (let p = 2; p * p <= 1000; p++) {

        // If p is a prime
        if (prime[p] == true) {

            // Mark all its multiples as non-prime
            for (let i = p * p; i <= 1000; i += p)
                prime[i] = false;
        }
    }

    // Print all prime numbers
    for (let p = 2; p <= 1000; p++)
        if (prime[p])
            primes.push(p);
}

// Function to generate n as the sum
// of k numbers where atleast K - 1
// are distinct and are product of 2 primes
function generate(n, k)
{
    // Stores the product of every
    // pair of prime number
    let prod = new Array();

    SieveOfEratosthenes();

    let l = primes.length;

    for (let i = 0; i < l; i++) {
        for (let j = i + 1; j < l; j++) {
            if (primes[i] * primes[j] > 0)
                prod.push(primes[i]
                            * primes[j]);
        }
    }

    // Sort the products
    prod.sort((a, b) => a - b)

    let sum = 0;
    for (let i = 0; i < k - 1; i++)
        sum += prod[i];

    // If sum exceeds n
    if (sum > n)
        document.write("-1");

    // Otherwise, print the k
    // required numbers
    else {
        for (let i = 0; i < k - 1; i++) {
            document.write(prod[i] + ", ");
        }
        document.write( n - sum + "<br>");
    }
}

// Driver Code

let n = 52, k = 5;
generate(n, k);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
6, 10, 14, 15, 7
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*