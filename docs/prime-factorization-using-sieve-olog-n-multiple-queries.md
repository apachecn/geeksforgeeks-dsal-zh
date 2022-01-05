# 对多个查询使用 0(对数 n)筛的素因子分解

> 原文:[https://www . geesforgeks . org/prime-factoring-use-screen-olog-n-multi-query/](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)

我们可以在 **O(sqrt(n))** 中计算一个数**“n”**的素因子分解，如这里[所讨论的](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。但是当我们需要回答关于素分解的多个查询时，O(sqrt n)方法超时。
在本文中，我们研究了一种利用 O(n)空间和 **O(log n)** 时间复杂度计算素因子分解的有效方法，并且允许预先计算。

**先决条件:** [筛选厄拉多塞](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[直到 n](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/) 的最小素数因子。

> **关键概念:**我们的想法是为每个数字存储最小质因数(SPF)。然后计算给定数的素因子分解，用它的最小素因子递归地除给定数，直到它变成 1。

为了计算每个数字的最小质因数，我们将使用埃拉托斯特尼的[筛。在最初的 screen 中，每次我们将一个数字标记为非质数时，我们都会为该数字存储相应的最小质因数(为了更好地理解，请参考](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[这篇](https://www.geeksforgeeks.org/least-prime-factor-of-numbers-till-n/)文章)。

现在，在我们完成对每个数的最小质因数的预先计算之后，我们将把我们的数 n(它的质因数分解将被计算)除以它对应的最小质因数，直到 n 变成 1。

```
Pseudo Code for prime factorization assuming
SPFs are computed :

PrimeFactors[] // To store result

i = 0  // Index in PrimeFactors

while n != 1 :

    // SPF : smallest prime factor
    PrimeFactors[i] = SPF[n]    
    i++ 
    n = n / SPF[n]
```

上述方法的实现如下:

## C++

```
// C++ program to find prime factorization of a
// number n in O(Log n) time with precomputation
// allowed.
#include "bits/stdc++.h"
using namespace std;

#define MAXN   100001

// stores smallest prime factor for every number
int spf[MAXN];

// Calculating SPF (Smallest Prime Factor) for every
// number till MAXN.
// Time Complexity : O(nloglogn)
void sieve()
{
    spf[1] = 1;
    for (int i=2; i<MAXN; i++)

        // marking smallest prime factor for every
        // number to be itself.
        spf[i] = i;

    // separately marking spf for every even
    // number as 2
    for (int i=4; i<MAXN; i+=2)
        spf[i] = 2;

    for (int i=3; i*i<MAXN; i++)
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

// A O(log n) function returning primefactorization
// by dividing by smallest prime factor at every step
vector<int> getFactorization(int x)
{
    vector<int> ret;
    while (x != 1)
    {
        ret.push_back(spf[x]);
        x = x / spf[x];
    }
    return ret;
}

// driver program for above function
int main(int argc, char const *argv[])
{
    // precalculating Smallest Prime Factor
    sieve();
    int x = 12246;
    cout << "prime factorization for " << x << " : ";

    // calling getFactorization function
    vector <int> p = getFactorization(x);

    for (int i=0; i<p.size(); i++)
        cout << p[i] << " ";
    cout << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find prime factorization of a
// number n in O(Log n) time with precomputation
// allowed.

import java.util.Vector;

class Test
{
    static final int MAXN = 100001;

    // stores smallest prime factor for every number
    static int spf[] = new int[MAXN];

    // Calculating SPF (Smallest Prime Factor) for every
    // number till MAXN.
    // Time Complexity : O(nloglogn)
    static void sieve()
    {
        spf[1] = 1;
        for (int i=2; i<MAXN; i++)

            // marking smallest prime factor for every
            // number to be itself.
            spf[i] = i;

        // separately marking spf for every even
        // number as 2
        for (int i=4; i<MAXN; i+=2)
            spf[i] = 2;

        for (int i=3; i*i<MAXN; i++)
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

    // A O(log n) function returning primefactorization
    // by dividing by smallest prime factor at every step
    static Vector<Integer> getFactorization(int x)
    {
        Vector<Integer> ret = new Vector<>();
        while (x != 1)
        {
            ret.add(spf[x]);
            x = x / spf[x];
        }
        return ret;
    }

    // Driver method
    public static void main(String args[])
    {
        // precalculating Smallest Prime Factor
        sieve();
        int x = 12246;
        System.out.print("prime factorization for " + x + " : ");

        // calling getFactorization function
        Vector <Integer> p = getFactorization(x);

        for (int i=0; i<p.size(); i++)
            System.out.print(p.get(i) + " ");
        System.out.println();
    }
}
```

## 蟒蛇 3

```
# Python3 program to find prime factorization
# of a number n in O(Log n) time with
# precomputation allowed.
import math as mt

MAXN = 100001

# stores smallest prime factor for
# every number
spf = [0 for i in range(MAXN)]

# Calculating SPF (Smallest Prime Factor)
# for every number till MAXN.
# Time Complexity : O(nloglogn)
def sieve():
    spf[1] = 1
    for i in range(2, MAXN):

        # marking smallest prime factor
        # for every number to be itself.
        spf[i] = i

    # separately marking spf for
    # every even number as 2
    for i in range(4, MAXN, 2):
        spf[i] = 2

    for i in range(3, mt.ceil(mt.sqrt(MAXN))):

        # checking if i is prime
        if (spf[i] == i):

            # marking SPF for all numbers
            # divisible by i
            for j in range(i * i, MAXN, i):

                # marking spf[j] if it is
                # not previously marked
                if (spf[j] == j):
                    spf[j] = i

# A O(log n) function returning prime
# factorization by dividing by smallest
# prime factor at every step
def getFactorization(x):
    ret = list()
    while (x != 1):
        ret.append(spf[x])
        x = x // spf[x]

    return ret

# Driver code

# precalculating Smallest Prime Factor
sieve()
x = 12246
print("prime factorization for", x, ": ",
                                end = "")

# calling getFactorization function
p = getFactorization(x)

for i in range(len(p)):
    print(p[i], end = " ")

# This code is contributed
# by Mohit kumar 29
```

## C#

```
// C# program to find prime factorization of a
// number n in O(Log n) time with precomputation
// allowed.
using System;
using System.Collections;

class GFG
{
    static int MAXN = 100001;

    // stores smallest prime factor for every number
    static int[] spf = new int[MAXN];

    // Calculating SPF (Smallest Prime Factor) for every
    // number till MAXN.
    // Time Complexity : O(nloglogn)
    static void sieve()
    {
        spf[1] = 1;
        for (int i = 2; i < MAXN; i++)

            // marking smallest prime factor for every
            // number to be itself.
            spf[i] = i;

        // separately marking spf for every even
        // number as 2
        for (int i = 4; i < MAXN; i += 2)
            spf[i] = 2;

        for (int i = 3; i * i < MAXN; i++)
        {
            // checking if i is prime
            if (spf[i] == i)
            {
                // marking SPF for all numbers divisible by i
                for (int j = i * i; j < MAXN; j += i)

                    // marking spf[j] if it is not
                    // previously marked
                    if (spf[j] == j)
                        spf[j] = i;
            }
        }
    }

    // A O(log n) function returning primefactorization
    // by dividing by smallest prime factor at every step
    static ArrayList getFactorization(int x)
    {
        ArrayList ret = new ArrayList();
        while (x != 1)
        {
            ret.Add(spf[x]);
            x = x / spf[x];
        }
        return ret;
    }

    // Driver code
    public static void Main()
    {
        // precalculating Smallest Prime Factor
        sieve();
        int x = 12246;
        Console.Write("prime factorization for " + x + " : ");

        // calling getFactorization function
        ArrayList p = getFactorization(x);

        for (int i = 0; i < p.Count; i++)
            Console.Write(p[i] + " ");
        Console.WriteLine("");
    }
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find prime factorization
// of a number n in O(Log n) time with
// precomputation allowed.

$MAXN = 19999;

// stores smallest prime factor for
// every number
$spf = array_fill(0, $MAXN, 0);

// Calculating SPF (Smallest Prime Factor)
// for every number till MAXN.
// Time Complexity : O(nloglogn)
function sieve()
{
    global $MAXN, $spf;
    $spf[1] = 1;
    for ($i = 2; $i < $MAXN; $i++)

        // marking smallest prime factor
        // for every number to be itself.
        $spf[$i] = $i;

    // separately marking spf for every
    // even number as 2
    for ($i = 4; $i < $MAXN; $i += 2)
        $spf[$i] = 2;

    for ($i = 3; $i * $i < $MAXN; $i++)
    {
        // checking if i is prime
        if ($spf[$i] == $i)
        {
            // marking SPF for all numbers
            // divisible by i
            for ($j = $i * $i; $j < $MAXN; $j += $i)

                // marking spf[j] if it is not
                // previously marked
                if ($spf[$j] == $j)
                    $spf[$j] = $i;
        }
    }
}

// A O(log n) function returning primefactorization
// by dividing by smallest prime factor at every step
function getFactorization($x)
{
    global $spf;
    $ret = array();
    while ($x != 1)
    {
        array_push($ret, $spf[$x]);
        if($spf[$x])
        $x = (int)($x / $spf[$x]);
    }
    return $ret;
}

// Driver Code

// precalculating Smallest
// Prime Factor
sieve();
$x = 12246;
echo "prime factorization for " .
                      $x . " : ";

// calling getFactorization function
$p = getFactorization($x);

for ($i = 0; $i < count($p); $i++)
    echo $p[$i] . " ";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find prime factorization of a
// number n in O(Log n) time with precomputation
// allowed.

    let MAXN = 100001;
     // stores smallest prime factor for every number
    let spf=new Array(MAXN);

    // Calculating SPF (Smallest Prime Factor) for every
    // number till MAXN.
    // Time Complexity : O(nloglogn)
    function sieve()
    {
        spf[1] = 1;
        for (let i=2; i<MAXN; i++)

            // marking smallest prime factor for every
            // number to be itself.
            spf[i] = i;

        // separately marking spf for every even
        // number as 2
        for (let i=4; i<MAXN; i+=2)
            spf[i] = 2;

        for (let i=3; i*i<MAXN; i++)
        {
            // checking if i is prime
            if (spf[i] == i)
            {
                // marking SPF for all numbers divisible by i
                for (let j=i*i; j<MAXN; j+=i)

                    // marking spf[j] if it is not
                    // previously marked
                    if (spf[j]==j)
                        spf[j] = i;
            }
        }
    }

    // A O(log n) function returning primefactorization
    // by dividing by smallest prime factor at every step
    function getFactorization(x)
    {
        let ret =[];
        while (x != 1)
        {
            ret.push(spf[x]);
            x = Math.floor(x / spf[x]);
        }
        return ret;
    }

    // Driver method

    // precalculating Smallest Prime Factor
    sieve();
    let x = 12246;
    document.write("prime factorization for " + x + " : ");
    // calling getFactorization function
    let  p = getFactorization(x);
    for (let i=0; i<p.length; i++)
            document.write(p[i] + " ");
        document.write("<br>");

// This code is contributed by unknown2108
</script>
```

**输出:**

```
prime factorization for 12246 : 2 3 13 157 
```

**注:**上述代码适用于 10^7.阶以上除此之外，我们将面临记忆问题。

**时间复杂度:**最小质因数的预计算是用筛子在 O(n log log n)中完成的。而在计算步骤中，我们每次都用最小质数除以这个数，直到它变成 1。所以，让我们考虑一个最坏的情况，每次 SPF 都是 2。因此会有 log n 的划分步骤。因此，我们可以说，在最坏的情况下，我们的时间复杂度将是 **O(对数 n)** 。

本文由 [**尼提什·库马尔**](https://www.linkedin.com/in/nk17kumar/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。