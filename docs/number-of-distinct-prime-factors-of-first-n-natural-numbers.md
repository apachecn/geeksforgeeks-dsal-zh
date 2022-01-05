# 前 n 个自然数的不同质因数的数量

> 原文:[https://www . geeksforgeeks . org/第 n 个自然数的不同质数因子数/](https://www.geeksforgeeks.org/number-of-distinct-prime-factors-of-first-n-natural-numbers/)

在这篇文章中，我们研究了一种优化的方法，在允许预先计算的情况下，利用 O **O(n*log n)** 的时间复杂度来计算 n 个自然数的不同素因子分解。
**先决条件:** [厄拉多塞筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[直到 n](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/) 的最小素数因子。

> **关键概念:**我们的想法是为每个数字存储最小质因数(SPF)。然后通过递归地将给定数除以它的最小素因子直到它变成 1 来计算给定数的不同素因子分解。

为了计算每个数字的最小质因数，我们将使用埃拉托斯特尼的[筛。在最初的 screen 中，每次我们将一个数字标记为非质数时，我们都会为该数字存储相应的最小质因数(为了更好地理解，请参考](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[这篇](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/)文章)。
上述方法的实施如下:

## C++

```
// C++ program to find prime factorization upto n natural number
// O(n*Log n) time with precomputation
#include <bits/stdc++.h>
using namespace std;
#define MAXN 100001

// Stores smallest prime factor for every number
int spf[MAXN];

// Adjacency vector to store distinct prime factors
vector<int>adj[MAXN];

// Calculating SPF (Smallest Prime Factor) for every
// number till MAXN.
// Time Complexity : O(nloglogn)
void sieve()
{
    spf[1] = 1;
        // marking smallest prime factor for every
        // number to be itself.
    for (int i=2; i<MAXN; i++)
        spf[i] = i;

    for (int i=2; i*i<MAXN; i++)
    {
        // checking if i is prime
        if (spf[i] == i)
        {
            // marking SPF for all numbers divisible by i
            for (int j=i*i; j<MAXN; j+=i)

                // marking spf[j] if it is not
                // previously marked
                if (spf[j]==j)
                    spf[j] = i;
        }
    }
}

// A O(nlog n) function returning distinct primefactorization
// upto n natural number by dividing by smallest prime factor
// at every step
void getdistinctFactorization(int n)
{
    int index,x,i;
    for(int i=1;i<=n;i++)
    {
        index=1;
        x=i;
        if(x!=1)
            adj[i].push_back(spf[x]);
        x=x/spf[x];
        // Push all distinct prime factor in adj
        while (x != 1)
        {
            if (adj[i][index-1]!=spf[x])
            {
                adj[i].push_back(spf[x]);
                index+=1;
            }
            x = x / spf[x];
        }
    }
}

// Driver code
int main()
{
    // Precalculating smallest prime factor
    sieve();

    int n = 10;

    getdistinctFactorization(n);

    // Print the prime count
    cout <<"Distinct prime factor for first " << n
         <<" natural number" <<" : ";

    for (int i=1; i<=n; i++)
        cout << adj[i].size() << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find prime factorization upto n natural number
// O(n*Log n) time with precomputation
import java.io.*;
import java.util.*;
class GFG
{
    static int MAXN = 100001;

    // Stores smallest prime factor for every number
    static int[] spf = new int[MAXN];

    // Adjacency vector to store distinct prime factors
    static ArrayList<ArrayList<Integer>> adj =
      new ArrayList<ArrayList<Integer>>();

    // Calculating SPF (Smallest Prime Factor) for every
    // number till MAXN.
    // Time Complexity : O(nloglogn)
    static void sieve()
    {
        for(int i = 0; i < MAXN; i++)
        {
            adj.add(new ArrayList<Integer>());
        }
        spf[1] = 1;

        // marking smallest prime factor for every
        // number to be itself.
        for (int i = 2; i < MAXN; i++)
        {
            spf[i] = i;
        }
        for (int i = 2; i * i < MAXN; i++)
        {
            // checking if i is prime
        if (spf[i] == i)
        {
                // marking SPF for all numbers divisible by i
                for (int j = i * i; j < MAXN; j += i)
                {

                    // marking spf[j] if it is not
                    // previously marked
                    if (spf[j] == j)
                        spf[j] = i;
                }
            }
        }
    }

    // A O(nlog n) function returning distinct primefactorization
    // upto n natural number by dividing by smallest prime factor
    // at every step   
    static void getdistinctFactorization(int n)
    {
        int index, x, i;
        for(i = 1; i <= n; i++)
        {
            index = 1;
            x = i;
            if(x != 1)
                adj.get(i).add(spf[x]);
            x = x / spf[x];

            // Push all distinct prime factor in adj
            while (x != 1)
            {
                if (adj.get(i).get(index - 1) != spf[x])
                {
                    adj.get(i).add(spf[x]);
                    index += 1;
                }
                x = x / spf[x];
            }
        }
    }

    // Driver code
    public static void main (String[] args)
    {

        // Precalculating smallest prime factor
        sieve();    
        int n = 10;    
        getdistinctFactorization(n);

        // Print the prime count
        System.out.print("Distinct prime factor for first " +
                         n + " natural number" + " : ");
        for (int i = 1; i <= n; i++)
        {
            System.out.print(adj.get(i).size()+ " ");
        }
    }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to find prime factorization upto n natural number
# O(n*Log n) time with precomputation

# Calculating SPF (Smallest Prime Factor) for every
# number till MAXN.
# Time Complexity : O(nloglogn)
def sieve():
    global spf, adj, MAXN
    spf[1] = 1

    # marking smallest prime factor for every
    # number to be itself.
    for i in range(2, MAXN):
        spf[i] = i

    for i in range(2, MAXN):
        if i * i > MAXN:
            break

        # checking if i is prime
        if (spf[i] == i):

            # marking SPF for all numbers divisible by i
            for j in range(i * i, MAXN, i):

                # marking spf[j] if it is not
                # previously marked
                if (spf[j] == j):
                    spf[j] = i

# A O(nlog n) function returning distinct primefactorization
# upto n natural number by dividing by smallest prime factor
# at every step
def getdistinctFactorization(n):
    global adj, spf, MAXN
    index = 0
    for i in range(1, n + 1):
        index = 1
        x = i
        if(x != 1):
            adj[i].append(spf[x])
        x = x // spf[x]

        # Push all distinct prime factor in adj
        while (x != 1):
            if (adj[i][index - 1] != spf[x]):
                adj[i].append(spf[x])
                index += 1
            x = x // spf[x]

# Driver code
if __name__ == '__main__':
    MAXN = 100001
    spf = [0 for i in range(MAXN)]
    adj = [[] for i in range(MAXN)]

    # Precalculating smallest prime factor
    sieve()
    n = 10
    getdistinctFactorization(n)

    # Print prime count
    print("Distinct prime factor for first ", n, " natural number : ", end = "")

    for i in range(1, n + 1):
        print(len(adj[i]), end = " ")

# This code is contributed by mohit kumar 29
```

## C#

```
using System;
using System.Collections.Generic;
public class GFG
{
  static int MAXN = 100001;

  // Stores smallest prime factor for every number
  static int[] spf = new int[MAXN];

  // Adjacency vector to store distinct prime factors
  static List<List<int>> adj = new List<List<int>>();

  // Calculating SPF (Smallest Prime Factor) for every
  // number till MAXN.
  // Time Complexity : O(nloglogn)
  static void sieve()
  {
    for(int i = 0; i < MAXN; i++)
    {
      adj.Add(new List<int>());
    }
    spf[1] = 1;

    // marking smallest prime factor for every
    // number to be itself.
    for (int i = 2; i < MAXN; i++)
    {
      spf[i] = i;
    }
    for (int i = 2; i * i < MAXN; i++)
    {

      // checking if i is prime
      if (spf[i] == i)
      {
        // marking SPF for all numbers divisible by i
        for (int j = i * i; j < MAXN; j += i)
        {

          // marking spf[j] if it is not
          // previously marked
          if (spf[j] == j)
            spf[j] = i;
        }
      }
    }
  }

  // A O(nlog n) function returning distinct primefactorization
  // upto n natural number by dividing by smallest prime factor
  // at every step   
  static void getdistinctFactorization(int n)
  {
    int index, x, i;
    for(i = 1; i <= n; i++)
    {
      index = 1;
      x = i;
      if(x != 1)
      {
        adj[i].Add(spf[x]);

      }
      x = x / spf[x];

      // Push all distinct prime factor in adj
      while (x != 1)
      {
        if (adj[i][index-1] != spf[x])
        {
          adj[i].Add(spf[x]);
          index += 1;
        }
        x = x / spf[x];
      }
    }
  }

  // Driver code
  static public void Main ()
  {

    // Precalculating smallest prime factor
    sieve();    
    int n = 10;    
    getdistinctFactorization(n);

    // Print the prime count
    Console.Write("Distinct prime factor for first " +
                  n + " natural number" + " : ");

    for (int i = 1; i <= n; i++)
    {
      Console.Write(adj[i].Count + " ");
    }
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program to find prime
// factorization upto n natural number
// O(n*Log n) time with precomputation

    let MAXN = 100001;
    // Stores smallest prime factor
    // for every number
    let spf = new Array(MAXN);

    // Adjacency vector to store distinct prime factors
    let adj=[];

    // Calculating SPF (Smallest Prime Factor) for every
    // number till MAXN.
    // Time Complexity : O(nloglogn)
    function sieve()
    {
        for(let i = 0; i < MAXN; i++)
        {
            adj.push([]);
        }
        spf[1] = 1;

        // marking smallest prime factor for every
        // number to be itself.
        for (let i = 2; i < MAXN; i++)
        {
            spf[i] = i;
        }
        for (let i = 2; i * i < MAXN; i++)
        {
            // checking if i is prime
        if (spf[i] == i)
        {
                // marking SPF for all numbers divisible by i
                for (let j = i * i; j < MAXN; j += i)
                {

                    // marking spf[j] if it is not
                    // previously marked
                    if (spf[j] == j)
                        spf[j] = i;
                }
            }
        }
    }

    // A O(nlog n) function returning
    // distinct primefactorization
    // upto n natural number by dividing by
    // smallest prime factor
    // at every step  
    function getdistinctFactorization(n)
    {
        let index, x, i;
        for(i = 1; i <= n; i++)
        {
            index = 1;
            x = i;
            if(x != 1)
                adj[i].push(spf[x]);
            x = Math.floor(x / spf[x]);

            // Push all distinct prime factor in adj
            while (x != 1)
            {
                if (adj[i][index - 1] != spf[x])
                {
                    adj[i].push(spf[x]);
                    index += 1;
                }
                x = Math.floor(x / spf[x]);
            }
        }
    }

    // Driver code

    // Precalculating smallest prime factor
        sieve();   
        let n = 10;   
        getdistinctFactorization(n);

        // Print the prime count
        document.write("Distinct prime factor for first " +
                         n + " natural number" + " : ");
        for (let i = 1; i <= n; i++)
        {
            document.write(adj[i].length+ " ");
        }

// This code is contributed by unknown2108

</script>

```

**Output**

```
Distinct prime factor for first 10 natural number : 0 1 1 1 1 2 1 1 1 2 
```