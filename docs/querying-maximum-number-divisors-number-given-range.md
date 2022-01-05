# 查询给定范围内某个数的最大除数

> 原文:[https://www . geesforgeks . org/query-最大数-除数-数-给定范围/](https://www.geeksforgeeks.org/querying-maximum-number-divisors-number-given-range/)

给定 Q 个查询，类型为: **L R** ，对于每个查询，您必须打印一个数字 **x (L < = x < = R)** 所具有的除数的最大值。
**例:**

```
L = 1 R = 10:
    1 has 1 divisor.
    2 has 2 divisors.
    3 has 2 divisors.
    4 has 3 divisors.
    5 has 2 divisors.
    6 has 4 divisors.
    7 has 2 divisors.
    8 has 4 divisors.
    9 has 3 divisors.
    10 has 4 divisors.

So the answer for above query is 4, as it is the maximum number of 
divisors a number has in [1, 10].
```

**先决条件:** [厄拉多塞筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[段树](https://www.geeksforgeeks.org/segment-tree-set-1-range-minimum-query/)
以下是解决问题的步骤。

1.  首先，我们来看看一个数有多少个除数**n = p<sub>1</sub>T3】kT5<sup>1</sup>T8】* p<sub>2</sub>T11】kT13<sup>2</sup>T16】*……* p<sub>n</sub>T19】kT21<sup>n</sup>T24**(其中 p <sub>1 【T27 答案是**(k<sub>1</sub>+1)*(k<sub>2</sub>+1)*……*(k<sub>n</sub>+1)**。怎么做？对于素数因式分解中的每个素数，我们可以在除数(0，1，2，…，k <sub>i</sub> 中拥有其 **k <sub>i</sub> + 1** 可能的幂。</sub>
2.  现在我们来看看如何才能找到一个数的素因子分解，我们首先构建一个数组，**minist _ prime[]**，它存储了 **i** 的最小素因子在 **i <sup>th</sup>** 索引处，我们将一个数除以它的最小素因子得到一个新数(我们也存储了这个新数的最小素因子)，我们一直这样做，直到这个数的最小素发生变化， 当新数的最小质因数与前一个数不同时，在给定数的质因数分解中，对于 i <sup>第</sup>个质数，我们有 k <sub>i</sub> 。
3.  最后，我们获得所有数字的除数，并将其存储在段树中，该树保持段中的最大数字。我们通过查询段树来响应每个查询。

## C++

```
// A C++ implementation of the above idea to process
// queries of finding a number with maximum divisors.
#include <bits/stdc++.h>
using namespace std;

#define maxn 1000005
#define INF 99999999

int smallest_prime[maxn];
int divisors[maxn];
int segmentTree[4 * maxn];

// Finds smallest prime factor of all numbers in
// range[1, maxn) and stores them in smallest_prime[],
// smallest_prime[i] should contain the smallest prime
// that divides i
void findSmallestPrimeFactors()
{
    // Initialize the smallest_prime factors of all
    // to infinity
    for (int i = 0 ; i < maxn ; i ++ )
        smallest_prime[i] = INF;

    // to be built like eratosthenes sieve
    for (long long i = 2; i < maxn; i++)
    {
        if (smallest_prime[i] == INF)
        {
            // prime number will have its smallest_prime
            // equal to itself
            smallest_prime[i] = i;
            for (long long j = i * i; j < maxn; j += i)

                // if 'i' is the first prime number reaching 'j'
                if (smallest_prime[j] > i)
                    smallest_prime[j] = i;
        }
    }
}

// number of divisors of n = (p1 ^ k1) * (p2 ^ k2) ... (pn ^ kn)
// are equal to (k1+1) * (k2+1) ... (kn+1)
// this function finds the number of divisors of all numbers
// in range [1, maxn) and stores it in divisors[]
// divisors[i] stores the number of divisors i has
void buildDivisorsArray()
{
    for (int i = 1; i < maxn; i++)
    {
        divisors[i] = 1;
        int n = i, p = smallest_prime[i], k = 0;

        // we can obtain the prime factorization of the number n
        // n = (p1 ^ k1) * (p2 ^ k2) ... (pn ^ kn) using the
        // smallest_prime[] array, we keep dividing n by its
        // smallest_prime until it becomes 1, whilst we check
        // if we have need to set k zero
        while (n > 1)
        {
            n = n / p;
            k ++;

            if (smallest_prime[n] != p)
            {
                //use p^k, initialize k to 0
                divisors[i] = divisors[i] * (k + 1);
                k = 0;
            }

            p = smallest_prime[n];
        }
    }
}

// builds segment tree for divisors[] array
void buildSegtmentTree(int node, int a, int b)
{
    // leaf node
    if (a == b)
    {
        segmentTree[node] = divisors[a];
        return ;
    }

    //build left and right subtree
    buildSegtmentTree(2 * node, a, (a + b) / 2);
    buildSegtmentTree(2 * node + 1, ((a + b) / 2) + 1, b);

    //combine the information from left
    //and right subtree at current node
    segmentTree[node] = max(segmentTree[2 * node],
                            segmentTree[2 *node + 1]);
}

//returns the maximum number of divisors in [l, r]
int query(int node, int a, int b, int l, int r)
{
    // If current node's range is disjoint with query range
    if (l > b || a > r)
        return -1;

    // If the current node stores information for the range
    // that is completely inside the query range
    if (a >= l && b <= r)
        return segmentTree[node];

    // Returns maximum number of divisors from left
    // or right subtree
    return max(query(2 * node, a, (a + b) / 2, l, r),
               query(2 * node + 1, ((a + b) / 2) + 1, b,l,r));
}

// driver code
int main()
{
    // First find smallest prime divisors for all
    // the numbers
    findSmallestPrimeFactors();

    // Then build the divisors[] array to store
    // the number of divisors
    buildDivisorsArray();

    // Build segment tree for the divisors[] array
    buildSegtmentTree(1, 1, maxn - 1);

    cout << "Maximum divisors that a number has "
         << " in [1, 100] are "
         << query(1, 1, maxn - 1, 1, 100) << endl;

    cout << "Maximum divisors that a number has"
         << " in [10, 48] are "
         << query(1, 1, maxn - 1, 10, 48) << endl;

    cout << "Maximum divisors that a number has"
         << " in [1, 10] are "
         << query(1, 1, maxn - 1, 1, 10) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above idea to process
// queries of finding a number with maximum divisors.
import java.util.*;

class GFG
{
static int maxn = 10005;
static int INF = 999999;

static int []smallest_prime = new int[maxn];
static int []divisors = new int[maxn];
static int []segmentTree = new int[4 * maxn];

// Finds smallest prime factor of all numbers
// in range[1, maxn) and stores them in
// smallest_prime[], smallest_prime[i] should
// contain the smallest prime that divides i
static void findSmallestPrimeFactors()
{
    // Initialize the smallest_prime factors
    // of all to infinity
    for (int i = 0 ; i < maxn ; i ++ )
        smallest_prime[i] = INF;

    // to be built like eratosthenes sieve
    for (int i = 2; i < maxn; i++)
    {
        if (smallest_prime[i] == INF)
        {
            // prime number will have its
            // smallest_prime equal to itself
            smallest_prime[i] = i;
            for (int j = i * i; j < maxn; j += i)

                // if 'i' is the first
                // prime number reaching 'j'
                if (smallest_prime[j] > i)
                    smallest_prime[j] = i;
        }
    }
}

// number of divisors of n = (p1 ^ k1) * (p2 ^ k2) ... (pn ^ kn)
// are equal to (k1+1) * (k2+1) ... (kn+1)
// this function finds the number of divisors of all numbers
// in range [1, maxn) and stores it in divisors[]
// divisors[i] stores the number of divisors i has
static void buildDivisorsArray()
{
    for (int i = 1; i < maxn; i++)
    {
        divisors[i] = 1;
        int n = i, p = smallest_prime[i], k = 0;

        // we can obtain the prime factorization of
        // the number n, n = (p1 ^ k1) * (p2 ^ k2) ... (pn ^ kn)
        // using the smallest_prime[] array, we keep dividing n
        // by its smallest_prime until it becomes 1,
        // whilst we check if we have need to set k zero
        while (n > 1)
        {
            n = n / p;
            k ++;

            if (smallest_prime[n] != p)
            {
                // use p^k, initialize k to 0
                divisors[i] = divisors[i] * (k + 1);
                k = 0;
            }
            p = smallest_prime[n];
        }
    }
}

// builds segment tree for divisors[] array
static void buildSegtmentTree(int node, int a, int b)
{
    // leaf node
    if (a == b)
    {
        segmentTree[node] = divisors[a];
        return ;
    }

    //build left and right subtree
    buildSegtmentTree(2 * node, a, (a + b) / 2);
    buildSegtmentTree(2 * node + 1, ((a + b) / 2) + 1, b);

    //combine the information from left
    //and right subtree at current node
    segmentTree[node] = Math.max(segmentTree[2 * node],
                                 segmentTree[2 *node + 1]);
}

// returns the maximum number of divisors in [l, r]
static int query(int node, int a, int b, int l, int r)
{
    // If current node's range is disjoint
    // with query range
    if (l > b || a > r)
        return -1;

    // If the current node stores information
    // for the range that is completely inside
    // the query range
    if (a >= l && b <= r)
        return segmentTree[node];

    // Returns maximum number of divisors from left
    // or right subtree
    return Math.max(query(2 * node, a, (a + b) / 2, l, r),
                    query(2 * node + 1,
                         ((a + b) / 2) + 1, b, l, r));
}

// Driver Code
public static void main(String[] args)
{

    // First find smallest prime divisors
    // for all the numbers
    findSmallestPrimeFactors();

    // Then build the divisors[] array to store
    // the number of divisors
    buildDivisorsArray();

    // Build segment tree for the divisors[] array
    buildSegtmentTree(1, 1, maxn - 1);

    System.out.println("Maximum divisors that a number " +
                       "has in [1, 100] are " +
                        query(1, 1, maxn - 1, 1, 100));

    System.out.println("Maximum divisors that a number " +
                       "has in [10, 48] are " +
                        query(1, 1, maxn - 1, 10, 48));

    System.out.println("Maximum divisors that a number " +
                       "has in [1, 10] are " +
                        query(1, 1, maxn - 1, 1, 10));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 implementation of the above
# idea to process queries of finding a
# number with maximum divisors.
maxn = 1000005
INF = 99999999

smallest_prime = [0] * maxn
divisors = [0] * maxn
segmentTree = [0] * (4 * maxn)

# Finds smallest prime factor of all
# numbers in range[1, maxn) and stores
# them in smallest_prime[], smallest_prime[i]
# should contain the smallest prime that divides i
def findSmallestPrimeFactors():

    # Initialize the smallest_prime
    # factors of all to infinity
    for i in range(maxn ):
        smallest_prime[i] = INF

    # to be built like eratosthenes sieve
    for i in range(2, maxn):
        if (smallest_prime[i] == INF):

            # prime number will have its
            # smallest_prime equal to itself
            smallest_prime[i] = i
            for j in range(i * i, maxn , i):

                # if 'i' is the first prime
                # number reaching 'j'
                if (smallest_prime[j] > i):
                    smallest_prime[j] = i

# number of divisors of n = (p1 ^ k1) *
# (p2 ^ k2) ... (pn ^ kn) are equal to
# (k1+1) * (k2+1) ... (kn+1). This function
# finds the number of divisors of all numbers
# in range [1, maxn) and stores it in divisors[]
# divisors[i] stores the number of divisors i has
def buildDivisorsArray():
    for i in range(1, maxn):
        divisors[i] = 1
        n = i
        p = smallest_prime[i]
        k = 0

        # we can obtain the prime factorization
        # of the number n n = (p1 ^ k1) * (p2 ^ k2)
        # ... (pn ^ kn) using the smallest_prime[]
        # array, we keep dividing n by its
        # smallest_prime until it becomes 1, whilst
        # we check if we have need to set k zero
        while (n > 1):
            n = n // p
            k += 1

            if (smallest_prime[n] != p):

                # use p^k, initialize k to 0
                divisors[i] = divisors[i] * (k + 1)
                k = 0

            p = smallest_prime[n]

# builds segment tree for divisors[] array
def buildSegtmentTree( node, a, b):

    # leaf node
    if (a == b):
        segmentTree[node] = divisors[a]
        return

    #build left and right subtree
    buildSegtmentTree(2 * node, a, (a + b) // 2)
    buildSegtmentTree(2 * node + 1,
                     ((a + b) // 2) + 1, b)

    #combine the information from left
    #and right subtree at current node
    segmentTree[node] = max(segmentTree[2 * node],
                            segmentTree[2 * node + 1])

# returns the maximum number of
# divisors in [l, r]
def query(node, a, b, l, r):

    # If current node's range is disjoint
    # with query range
    if (l > b or a > r):
        return -1

    # If the current node stores information
    # for the range that is completely inside
    # the query range
    if (a >= l and b <= r):
        return segmentTree[node]

    # Returns maximum number of divisors
    # from left or right subtree
    return max(query(2 * node, a, (a + b) // 2, l, r),
               query(2 * node + 1,
                    ((a + b) // 2) + 1, b, l, r))

# Driver code
if __name__ == "__main__":

    # First find smallest prime divisors
    # for all the numbers
    findSmallestPrimeFactors()

    # Then build the divisors[] array to
    # store the number of divisors
    buildDivisorsArray()

    # Build segment tree for the divisors[] array
    buildSegtmentTree(1, 1, maxn - 1)
    print("Maximum divisors that a number has ",
                            " in [1, 100] are ",
                  query(1, 1, maxn - 1, 1, 100))

    print("Maximum divisors that a number has",
                           " in [10, 48] are ",
                 query(1, 1, maxn - 1, 10, 48))

    print( "Maximum divisors that a number has",
                             " in [1, 10] are ",
                   query(1, 1, maxn - 1, 1, 10))

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the above idea
// to process queries of finding a number
// with maximum divisors.
using System;

class GFG
{
static int maxn = 10005;
static int INF = 999999;

static int []smallest_prime = new int[maxn];
static int []divisors = new int[maxn];
static int []segmentTree = new int[4 * maxn];

// Finds smallest prime factor of all numbers
// in range[1, maxn) and stores them in
// smallest_prime[], smallest_prime[i] should
// contain the smallest prime that divides i
static void findSmallestPrimeFactors()
{
    // Initialize the smallest_prime
    // factors of all to infinity
    for (int i = 0 ; i < maxn ; i ++ )
        smallest_prime[i] = INF;

    // to be built like eratosthenes sieve
    for (int i = 2; i < maxn; i++)
    {
        if (smallest_prime[i] == INF)
        {
            // prime number will have its
            // smallest_prime equal to itself
            smallest_prime[i] = i;
            for (int j = i * i; j < maxn; j += i)

                // if 'i' is the first
                // prime number reaching 'j'
                if (smallest_prime[j] > i)
                    smallest_prime[j] = i;
        }
    }
}

// number of divisors of
// n = (p1 ^ k1) * (p2 ^ k2) ... (pn ^ kn)
// are equal to (k1+1) * (k2+1) ... (kn+1)
// this function finds the number of divisors
// of all numbers in range [1, maxn) and stores
// it in divisors[] divisors[i] stores the
// number of divisors i has
static void buildDivisorsArray()
{
    for (int i = 1; i < maxn; i++)
    {
        divisors[i] = 1;
        int n = i, p = smallest_prime[i], k = 0;

        // we can obtain the prime factorization of
        // the number n,
        // n = (p1 ^ k1) * (p2 ^ k2) ... (pn ^ kn)
        // using the smallest_prime[] array,
        // we keep dividing n by its smallest_prime
        // until it becomes 1, whilst we check if
        // we have need to set k zero
        while (n > 1)
        {
            n = n / p;
            k ++;

            if (smallest_prime[n] != p)
            {
                // use p^k, initialize k to 0
                divisors[i] = divisors[i] * (k + 1);
                k = 0;
            }
            p = smallest_prime[n];
        }
    }
}

// builds segment tree for divisors[] array
static void buildSegtmentTree(int node,
                              int a, int b)
{
    // leaf node
    if (a == b)
    {
        segmentTree[node] = divisors[a];
        return;
    }

    //build left and right subtree
    buildSegtmentTree(2 * node, a, (a + b) / 2);
    buildSegtmentTree(2 * node + 1,
                    ((a + b) / 2) + 1, b);

    //combine the information from left
    //and right subtree at current node
    segmentTree[node] = Math.Max(segmentTree[2 * node],
                                 segmentTree[2 *node + 1]);
}

// returns the maximum number of divisors in [l, r]
static int query(int node, int a, int b, int l, int r)
{
    // If current node's range is disjoint
    // with query range
    if (l > b || a > r)
        return -1;

    // If the current node stores information
    // for the range that is completely inside
    // the query range
    if (a >= l && b <= r)
        return segmentTree[node];

    // Returns maximum number of divisors from left
    // or right subtree
    return Math.Max(query(2 * node, a, (a + b) / 2, l, r),
                    query(2 * node + 1,
                        ((a + b) / 2) + 1, b, l, r));
}

// Driver Code
public static void Main(String[] args)
{

    // First find smallest prime divisors
    // for all the numbers
    findSmallestPrimeFactors();

    // Then build the divisors[] array
    // to store the number of divisors
    buildDivisorsArray();

    // Build segment tree for the divisors[] array
    buildSegtmentTree(1, 1, maxn - 1);

    Console.WriteLine("Maximum divisors that a number " +
                                 "has in [1, 100] are " +
                          query(1, 1, maxn - 1, 1, 100));

    Console.WriteLine("Maximum divisors that a number " +
                                 "has in [10, 48] are " +
                          query(1, 1, maxn - 1, 10, 48));

    Console.WriteLine("Maximum divisors that a number " +
                                  "has in [1, 10] are " +
                           query(1, 1, maxn - 1, 1, 10));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the above idea to process
// queries of finding a number with maximum divisors.

    let maxn = 10005;
    let INF = 999999;
    let smallest_prime = new Array(maxn);
    for(let i=0;i<maxn;i++)
    {
        smallest_prime[i]=0;
    }
    let divisors = new Array(maxn);
    for(let i=0;i<maxn;i++)
    {
        divisors[i]=0;
    }
    let segmentTree = new Array(4 * maxn);
    for(let i=0;i<4*maxn;i++)
    {
        segmentTree[i]=0;
    }

    // Finds smallest prime factor of all numbers
    // in range[1, maxn) and stores them in
    // smallest_prime[], smallest_prime[i] should
    // contain the smallest prime that divides i
    function findSmallestPrimeFactors()
    {
        // Initialize the smallest_prime factors
        // of all to infinity
        for (let i = 0 ; i < maxn ; i ++ )
            smallest_prime[i] = INF;

        // to be built like eratosthenes sieve
        for (let i = 2; i < maxn; i++)
        {
            if (smallest_prime[i] == INF)
            {
                // prime number will have its
                // smallest_prime equal to itself
                smallest_prime[i] = i;
                for (let j = i * i; j < maxn; j += i)
                {     
                    // if 'i' is the first
                    // prime number reaching 'j'
                    if (smallest_prime[j] > i)
                        smallest_prime[j] = i;
                }
            }
        }
    }

    // number of divisors of n = (p1 ^ k1) * (p2 ^ k2) ... (pn ^ kn)
    // are equal to (k1+1) * (k2+1) ... (kn+1)
    // this function finds the number of divisors of all numbers
    // in range [1, maxn) and stores it in divisors[]
    // divisors[i] stores the number of divisors i has
    function buildDivisorsArray()
    {
        for (let i = 1; i < maxn; i++)
        {
            divisors[i] = 1;
            let n = i;
            let p = smallest_prime[i]
            let k = 0;

            // we can obtain the prime factorization of
            // the number n, n = (p1 ^ k1) * (p2 ^ k2) ... (pn ^ kn)
            // using the smallest_prime[] array, we keep dividing n
            // by its smallest_prime until it becomes 1,
            // whilst we check if we have need to set k zero
            while (n > 1)
            {
                n = Math.floor(n / p);
                k++;

                if (smallest_prime[n] != p)
                {
                    // use p^k, initialize k to 0
                    divisors[i] = divisors[i] * (k + 1);
                    k = 0;
                }
                p = smallest_prime[n];
            }
        }
    }

    // builds segment tree for divisors[] array
    function buildSegtmentTree(node,a,b)
    {
        // leaf node
        if (a == b)
        {
            segmentTree[node] = divisors[a];
            return ;
        }

        //build left and right subtree
        buildSegtmentTree(2 * node, a, Math.floor((a + b) / 2));
        buildSegtmentTree((2 * node) + 1, Math.floor((a + b) / 2) + 1, b);

        //combine the information from left
        //and right subtree at current node
        segmentTree[node] = Math.max(segmentTree[2 * node],
                                     segmentTree[(2 *node) + 1]);
    }

    // returns the maximum number of divisors in [l, r]
    function query(node,a,b,l,r)
    {
        // If current node's range is disjoint
        // with query range
        if (l > b || a > r)
            return -1;

        // If the current node stores information
        // for the range that is completely inside
        // the query range
        if (a >= l && b <= r)
            return segmentTree[node];

        // Returns maximum number of divisors from left
        // or right subtree
        return Math.max(query(2 * node, a,
        Math.floor((a + b) / 2), l, r),
                        query(2 * node + 1,
                        Math.floor((a + b) / 2) + 1, b, l, r));
    }
    // Driver Code

    // First find smallest prime divisors
    // for all the numbers
    findSmallestPrimeFactors();

    // Then build the divisors[] array to store
    // the number of divisors
    buildDivisorsArray();

    // Build segment tree for the divisors[] array
    buildSegtmentTree(1, 1, maxn - 1);

    document.write("Maximum divisors that a number " +
    "has in [1, 100] are " + query(1, 1, maxn - 1, 1, 100)+"<br>");

    document.write("Maximum divisors that a number " +
                       "has in [10, 48] are " +
                        query(1, 1, maxn - 1, 10, 48)+"<br>");

    document.write("Maximum divisors that a number " +
                       "has in [1, 10] are " +
                        query(1, 1, maxn - 1, 1, 10)+"<br>");

    //  This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Maximum divisors that a number has in [1, 100] are 12
Maximum divisors that a number has in [10, 48] are 10
Maximum divisors that a number has in [1, 10] are 4
```

**时间复杂度:**

```
For sieve: O(maxn * log(log(maxn)) )
For calculating divisors of each number: O(k<sub>1 + k2 + ... + kn)</sub> < O(log(maxn))
For querying each range: O(log(maxn))
Total: O((maxn + Q) * log(maxn))
```

本文由**索米·马尔霍特拉**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。