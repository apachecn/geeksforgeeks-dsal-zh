# 平衡质数

> 原文:[https://www.geeksforgeeks.org/balanced-prime/](https://www.geeksforgeeks.org/balanced-prime/)

在数论中，一个 [**平衡素数**](https://en.wikipedia.org/wiki/Balanced_prime) 是上下素数间隙大小相等的素数，因此等于上下最近素数的算术平均值。或者用代数的方法来说，给定一个素数 p <sub>n</sub> ，其中 N 是它在有序素数集中的索引，
![\Huge p_n= \frac{p_{n-1}+p_{n+1}}{2} ](img/010674ec47544c190281cb0359ae6e6a.png "Rendered by QuickLaTeX.com")
前几个平衡素数是 5，53，157，173……
给定一个正整数 **N** 。任务是打印第 n 个平衡素数。
示例:

```
Input : n = 2
Output : 53

Input : n = 3
Output : 157
```

这个想法是使用厄拉多塞的[筛生成素数，并将其存储在数组中。现在迭代数组，检查它是否是平衡素数，并继续计算平衡素数。一旦你到达第 n 个质数，把它还回来。
以下是本办法的实施情况:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// CPP Program to find Nth Balanced Prime
#include<bits/stdc++.h>
#define MAX 501
using namespace std;

// Return the Nth balanced prime.
int balancedprime(int n)
{
    // Sieve of Eratosthenes
    bool prime[MAX+1];
    memset(prime, true, sizeof(prime));

    for (int p = 2; p*p <= MAX; p++)
    {
        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (int i = p*2; i <= MAX; i += p)
                prime[i] = false;
        }
    }

    // storing all primes
    vector<int> v;
    for (int p = 3; p <= MAX; p += 2)
       if (prime[p])
          v.push_back(p);

    int count = 0;

    // Finding the Nth balanced Prime
    for (int i = 1; i < v.size(); i++)
    {
        if (v[i] == (v[i+1] + v[i - 1])/2)
          count++;

        if (count == n)
          return v[i];
    }
}

// Driven Program
int main()
{
  int n = 4; 
  cout << balancedprime(n) << endl;
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find Nth Balanced Prime
import java.util.*;

public class GFG
{
    static int MAX = 501;

    // Return the Nth balanced prime.
    public static int balancedprime(int n)
    {

        // Sieve of Eratosthenes
        boolean[] prime = new boolean[MAX+1];

        for(int k = 0 ; k < MAX+1; k++)
            prime[k] = true;

        for (int p = 2; p*p <= MAX; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true)
            {

                // Update all multiples of p
                for (int i = p*2; i <= MAX;
                                     i += p)
                    prime[i] = false;
            }
        }

        // storing all primes
        Vector<Integer> v =
                     new Vector<Integer>();
        for (int p = 3; p <= MAX; p += 2)
            if (prime[p])
                v.add(p);

        int count = 0;

        // Finding the Nth balanced Prime
        for (int i = 1; i < v.size(); i++)
        {
            if ((int)v.get(i) == ((int)v.get(i+1)
                           + (int)v.get(i-1))/2)
                count++;

            if (count == n)
                return (int) v.get(i);
        }

        return 1;
    }

    // Driven Program
    public static void main(String[] args)
    {
        int n = 4;
        System.out.print(balancedprime(n));
    }
}

// This code is contributed by Prasad Kshirsagar
```

## 蟒蛇 3

```
# Python3 code to find Nth Balanced Prime

MAX = 501

# Return the Nth balanced prime.
def balancedprime( n ):

    # Sieve of Eratosthenes
    prime = [True]*(MAX+1)
    p=2
    while p * p <= MAX:

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p] == True:

            # Update all multiples of p
            i = p * 2
            while i <= MAX:
                prime[i] = False
                i = i + p
        p = p +1

    # storing all primes
    v = list()
    p = 3
    while p <= MAX:
        if prime[p]:
            v.append(p)
        p = p + 2

    count = 0

    # Finding the Nth balanced Prime
    i=1
    for i in range(len(v)):
        if v[i] == (v[i+1] + v[i - 1])/2:
            count += 1

        if count == n:
            return v[i]

# Driven Program
n = 4
print(balancedprime(n))

# This code is contributed by "Sharad_Bhardwaj".
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find Nth Balanced Prime

$MAX=501;

// Return the Nth balanced prime.
function balancedprime($n)
{
    global $MAX;
    // Sieve of Eratosthenes
    $prime=array_fill(0,$MAX+1,true);

    for ($p = 2; $p*$p <= $MAX; $p++)
    {
        // If prime[p] is not changed, then it is a prime
        if ($prime[$p] == true)
        {
            // Update all multiples of p
            for ($i = $p*2; $i <= $MAX; $i += $p)
                $prime[$i] = false;
        }
    }

    // storing all primes
    $v=array();
    for ($p = 3; $p <= $MAX; $p += 2)
    if ($prime[$p])
        array_push($v,$p);

    $count = 0;

    // Finding the Nth balanced Prime
    for ($i = 1; $i < count($v); $i++)
    {
        if ($v[$i] == ($v[$i+1] + $v[$i - 1])/2)
        $count++;

        if ($count == $n)
        return $v[$i];
    }
}

// Driven Program

$n = 4;
echo balancedprime($n);

// this code is contributed by mits.
?>
```

## C#

```
// C# Program to find Nth Balanced Prime
using System;
using System.Collections.Generic;
public class GFG
{
    static int MAX = 501;

    // Return the Nth balanced prime.
    public static int balancedprime(int n)
    {

        // Sieve of Eratosthenes
        bool[] prime = new bool[MAX+1];

        for(int k = 0 ; k < MAX+1; k++)
            prime[k] = true;

        for (int p = 2; p*p <= MAX; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true)
            {

                // Update all multiples of p
                for (int i = p*2; i <= MAX;
                                    i += p)
                    prime[i] = false;
            }
        }

        // storing all primes
        List<int> v = new List<int>();
        for (int p = 3; p <= MAX; p += 2)
            if (prime[p])
                v.Add(p);

        int c = 0;
        // Finding the Nth balanced Prime
        for (int i = 1; i < v.Count-1; i++)
        {
            if ((int)v[i]==(int)(v[i+1]+v[i-1])/2)
            c++;
            if (c == n)
                return (int) v[i];
        }

        return 1;
    }

    // Driven Program
    public static void Main()
    {
        int n = 4;
        Console.WriteLine(balancedprime(n));
    }
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// Javascript Program to find Nth Balanced Prime

var MAX = 501;

// Return the Nth balanced prime.
function balancedprime(n)
{
    // Sieve of Eratosthenes
    var prime = Array(MAX+1).fill(true);

    for (var p = 2; p*p <= MAX; p++)
    {
        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (var i = p*2; i <= MAX; i += p)
                prime[i] = false;
        }
    }

    // storing all primes
    var v = [];
    for (var p = 3; p <= MAX; p += 2)
       if (prime[p])
          v.push(p);

    var count = 0;

    // Finding the Nth balanced Prime
    for (var i = 1; i < v.length; i++)
    {
        if (v[i] == (v[i+1] + v[i - 1])/2)
          count++;

        if (count == n)
          return v[i];
    }
}

// Driven Program
var n = 4; 
document.write( balancedprime(n) );

</script>
```

**输出:**

```
173
```