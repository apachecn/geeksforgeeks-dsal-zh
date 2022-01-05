# 每 K 个集合的第一个元素，其连续元素恰好具有小于 N 的 K 个素因子

> 原文:[https://www . geeksforgeeks . org/每 k 个集合中的第一个元素具有恰好 k 个质因数小于 n 的连续元素/](https://www.geeksforgeeks.org/first-element-of-every-k-sets-having-consecutive-elements-with-exactly-k-prime-factors-less-than-n/)

给定两个整数 **N** 和 **K** ，任务是为每组 **K** 连续元素找到第一个元素，这些元素恰好具有**K**T8】素因子，并且小于 **N** 。

**例:**

> **输入:** N = 30，K = 2
> **输出:** 14 20 21
> **解释:**
> 质因数等于 2 的数小于 30 = { 14，15，18，20，21，22，24，26，28 }。
> 在上面的例子中，对于 K = 2 (14，15) (20，21) (21，22)只形成这样的集合，因此级数是 14，20，21。
> **输入:** N = 1000，K = 3
> **输出:** 644 740 804 986

**天真方法:**天真方法是从 **2 迭代到 N** 并检查每一个 **K** 连续数形成一个集合，该集合中每个元素都有 **K** 素因子。如果“是”，则打印该集合的第一个元素，并检查下一个 K 元素。
***时间复杂度:** O(N*K)*
***辅助空间:** O(1)*
**高效方法:**上述方法可以通过预计算素因子的数量直到 **N** 并检查具有 **K** 素因子的每 K 个连续元素计数来优化。以下是步骤:

1.  使用厄拉多塞的[筛创建](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[最小质因数数组 **spf[]**](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/) ，该数组存储每个数字的最小质因数直到 **N** 。
2.  使用上述步骤，计算质因数的数量，直到每个数字 **N**
3.  将数字存储在质因数计数为 **K** 的数组中(比如**结果[]** )。
4.  对于数组的每个元素**结果【】**检查是否存在 **K** 连续数字，然后打印 **K** 连续数字的第一个元素。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#define x 2000021
using namespace std;

// For storing smallest prime factor
long long int v[x];

// Function construct smallest
// prime factor array
void sieve()
{
    v[1] = 1;

    // Mark smallest prime factor for
    // every number to be itself.
    for (long long int i = 2; i < x; i++)
        v[i] = i;

    // separately mark spf for every even
    // number as 2
    for (long long int i = 4; i < x; i += 2)
        v[i] = 2;

    for (long long int i = 3; i * i < x; i++) {

        // Check if i is prime
        if (v[i] == i) {

            // Mark SPF for all numbers
            // divisible by i
            for (long long int j = i * i;
                 j < x; j += i) {

                // Mark spf[j] if it is
                // not previously marked
                if (v[j] == j) {
                    v[j] = i;
                }
            }
        }
    }
}

// Function for counts total number
// of prime factors
long long int prime_factors(long long n)
{
    set<long long int> s;

    while (n != 1) {
        s.insert(v[n]);
        n = n / v[n];
    }
    return s.size();
}

// Function to print elements of sets
// of K consecutive elements having
// K prime factors
void distinctPrimes(long long int m,
                    long long int k)
{

    // To store the result
    vector<long long int> result;
    for (long long int i = 14;
         i < m + k; i++) {

        // Count number of prime
        // factors of number
        long long count
            = prime_factors(i);

        // If number has exactly K
        // factors push in result[]
        if (count == k) {
            result.push_back(i);
        }
    }

    long long int p = result.size();

    for (long long int index = 0;
         index < p - 1; index++) {

        long long element = result[index];
        long long count = 1, z = index;

        // Iterate till we get K consecutive
        // elements in result[]
        while (z < p - 1 && count <= k
               && result[z] + 1
                      == result[z + 1]) {

            // Count sequence until K
            count++;
            z++;
        }

        // Print the element if count >= K
        if (count >= k)
            cout << element << ' ';
    }
}

// Driver Code
int main()
{
    // To construct spf[]
    sieve();

    // Given N and K
    long long int N = 1000, K = 3;

    // Function Call
    distinctPrimes(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static final int x = 2000021;

// For storing smallest prime factor
static int []v = new int[x];

// Function consmallest
// prime factor array
static void sieve()
{
    v[1] = 1;

    // Mark smallest prime factor for
    // every number to be itself.
    for(int i = 2; i < x; i++)
        v[i] = i;

    // Separately mark spf for every even
    // number as 2
    for(int i = 4; i < x; i += 2)
        v[i] = 2;

    for(int i = 3; i * i < x; i++)
    {

        // Check if i is prime
        if (v[i] == i)
        {

            // Mark SPF for all numbers
            // divisible by i
            for(int j = i * i; j < x; j += i)
            {

                // Mark spf[j] if it is
                // not previously marked
                if (v[j] == j)
                {
                    v[j] = i;
                }
            }
        }
    }
}

// Function for counts total number
// of prime factors
static int prime_factors(int n)
{
    HashSet<Integer> s = new HashSet<Integer>();

    while (n != 1)
    {
        s.add(v[n]);
        n = n / v[n];
    }

    return s.size();
}

// Function to print elements of sets
// of K consecutive elements having
// K prime factors
static void distinctPrimes(int m, int k)
{

    // To store the result
    Vector<Integer> result = new Vector<Integer>();
    for (int i = 14; i < m + k; i++)
    {

        // Count number of prime
        // factors of number
        long count = prime_factors(i);

        // If number has exactly K
        // factors push in result[]
        if (count == k)
        {
            result.add(i);
        }
    }

    int p = result.size();
    for(int index = 0;
            index < p - 1; index++)
    {

        long element = result.get(index);
        int count = 1, z = index;

        // Iterate till we get K consecutive
        // elements in result[]
        while (z < p - 1 && count <= k &&
                     result.get(z) + 1 ==
                     result.get(z + 1))
        {

            // Count sequence until K
            count++;
            z++;
        }

        // Print the element if count >= K
        if (count >= k)
            System.out.print(element + " ");
    }
}

// Driver code
public static void main(String[] args)
{

    // To construct spf[]
    sieve();

    // Given N and K
    int N = 1000, K = 3;

    // Function call
    distinctPrimes(N, K);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach
x = 2000021

# For storing smallest prime factor
v = [0] * x

# Function construct smallest
# prime factor array
def sieve():

    v[1] = 1

    # Mark smallest prime factor for
    # every number to be itself
    for i in range(2, x):
        v[i] = i

    # separately mark spf for every
    # even number as 2
    for i in range(4, x, 2):
        v[i] = 2

    i = 3
    while (i * i < x):

        # Check if i is prime
        if (v[i] == i):

            # Mark SPF for all numbers
            # divisible by i
            for j in range(i * i, x, i):

                # Mark spf[i] if it is
                # not previously marked
                if (v[j] == j):
                    v[j] = i

        i += 1

# Function for counts total number
# of prime factors
def prime_factors(n):

    s = set()

    while (n != 1):
        s.add(v[n])
        n = n // v[n]

    return len(s)

# Function to print elements of sets
# of K consecutive elements having
# K prime factors
def distinctPrimes(m, k):

    # To store the result
    result = []

    for i in range(14, m + k):

        # Count number of prime
        # factors of number
        count = prime_factors(i)

        # If number has exactly K
        # factors puch in result[]
        if (count == k):
            result.append(i)

    p = len(result)

    for index in range(p - 1):
        element = result[index]
        count = 1
        z = index

        # Iterate till we get K consecutive
        # elements in result[]
        while (z < p - 1 and count <= k and
               result[z] + 1 == result[z + 1]):

            # Count sequence until K
            count += 1
            z += 1

        # Print the element if count >= K
        if (count >= k):
            print(element, end = ' ')

# Driver Code
if __name__ == '__main__':

    # To construct spf[]
    sieve()

    # Given N and K
    N = 1000
    K = 3

    # Function call
    distinctPrimes(N, K)

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static readonly int x = 2000021;

// For storing smallest prime factor
static int []v = new int[x];

// Function consmallest
// prime factor array
static void sieve()
{
    v[1] = 1;

    // Mark smallest prime factor for
    // every number to be itself.
    for(int i = 2; i < x; i++)
        v[i] = i;

    // Separately mark spf for every even
    // number as 2
    for(int i = 4; i < x; i += 2)
        v[i] = 2;

    for(int i = 3; i * i < x; i++)
    {

        // Check if i is prime
        if (v[i] == i)
        {

            // Mark SPF for all numbers
            // divisible by i
            for(int j = i * i; j < x; j += i)
            {

                // Mark spf[j] if it is
                // not previously marked
                if (v[j] == j)
                {
                    v[j] = i;
                }
            }
        }
    }
}

// Function for counts total number
// of prime factors
static int prime_factors(int n)
{
    HashSet<int> s = new HashSet<int>();

    while (n != 1)
    {
        s.Add(v[n]);
        n = n / v[n];
    }
    return s.Count;
}

// Function to print elements of sets
// of K consecutive elements having
// K prime factors
static void distinctPrimes(int m, int k)
{

    // To store the result
    List<int> result = new List<int>();
    for (int i = 14; i < m + k; i++)
    {

        // Count number of prime
        // factors of number
        long count = prime_factors(i);

        // If number has exactly K
        // factors push in result[]
        if (count == k)
        {
            result.Add(i);
        }
    }

    int p = result.Count;
    for(int index = 0;
            index < p - 1; index++)
    {
        long element = result[index];
        int count = 1, z = index;

        // Iterate till we get K consecutive
        // elements in result[]
        while (z < p - 1 && count <= k &&
               result[z] + 1 == result[z + 1])
        {

            // Count sequence until K
            count++;
            z++;
        }

        // Print the element if count >= K
        if (count >= k)
            Console.Write(element + " ");
    }
}

// Driver code
public static void Main(String[] args)
{

    // To construct spf[]
    sieve();

    // Given N and K
    int N = 1000, K = 3;

    // Function call
    distinctPrimes(N, K);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

let x  = 2000021

// For storing smallest prime factor
let v = new Array(x);

// Function construct smallest
// prime factor array
function sieve()
{
    v[1] = 1;

    // Mark smallest prime factor for
    // every number to be itself.
    for (let i = 2; i < x; i++)
        v[i] = i;

    // separately mark spf for every even
    // number as 2
    for (let i = 4; i < x; i += 2)
        v[i] = 2;

    for (let i = 3; i * i < x; i++) {

        // Check if i is prime
        if (v[i] == i) {

            // Mark SPF for all numbers
            // divisible by i
            for (let j = i * i;
                j < x; j += i) {

                // Mark spf[j] if it is
                // not previously marked
                if (v[j] == j) {
                    v[j] = i;
                }
            }
        }
    }
}

// Function for counts total number
// of prime factors
function prime_factors(n)
{
    let s = new Set();

    while (n != 1) {
        s.add(v[n]);
        n = n / v[n];
    }
    return s.size;
}

// Function to print elements of sets
// of K consecutive elements having
// K prime factors
function distinctPrimes(m, k)
{

    // To store the result
    let result = new Array();
    for (let i = 14;
        i < m + k; i++) {

        // Count number of prime
        // factors of number
        let count
            = prime_factors(i);

        // If number has exactly K
        // factors push in result[]
        if (count == k) {
            result.push(i);
        }
    }

    let p = result.length;

    for (let index = 0;
        index < p - 1; index++) {

        let element = result[index];
        let count = 1, z = index;

        // Iterate till we get K consecutive
        // elements in result[]
        while (z < p - 1 && count <= k
            && result[z] + 1
                    == result[z + 1]) {

            // Count sequence until K
            count++;
            z++;
        }

        // Print the element if count >= K
        if (count >= k)
            document.write(element + ' ');
    }
}

// Driver Code

    // To construct spf[]
    sieve();

    // Given N and K
    let N = 1000, K = 3;

    // Function Call
    distinctPrimes(N, K);

    // This code is contributed by_saurabh_jaiswal

</script>
```

**Output:** 

```
644 740 804 986
```

**时间复杂度:***O(N * log(log N))*
T5】辅助空间: *O(N)*