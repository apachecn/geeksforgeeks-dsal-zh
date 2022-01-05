# 数组中所有自然数的除数之和

> 原文:[https://www . geesforgeks . org/sum-proper-dividers-natural-numbers-array/](https://www.geeksforgeeks.org/sum-proper-divisors-natural-numbers-array/)

给定一个自然数数组，计算数组中每个元素的除数之和。

```
Input  : int arr[] = {8, 13, 24, 36, 59, 75, 87}
Output : 7 1 36 55 1 49 21
Number 8 has 3 proper divisors 1, 2, 4
and their sum comes out to be 7.
```

这个问题的一个天真的解决方案已经在下面的帖子中讨论过了。
[自然数的所有适当因子之和](https://www.geeksforgeeks.org/sum-of-all-proper-divisors-of-a-natural-number/)
我们可以通过利用厄拉多塞的[筛更有效地做到这一点。
思想基于一个数的素分解。通过](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[使用筛子，我们可以存储一个数的所有质因数及其幂](https://www.geeksforgeeks.org/print-all-prime-factors-and-their-powers/)。

```
To find all divisors, we need to consider
all powers of a prime factor and multiply
it with all all powers of other prime factors.
(For example, if the number is 36, its prime
factors are 2 and 3 and all divisors are 1,
2, 3, 4, 6, 9, 12 and 18.

Consider a number N can be written 
as P1^Q1 * P2^Q2 * P3^Q3 (here only 3 
prime factors are considered but there can 
be more than that) then sum of its divisors 
will be written as:
 = P1^0 * P2^0 * P3^0 + P1^0 * P2^0 * P3^1 + 
   P1^0 * P2^0 * P3^2 + ................ + 
   P1^0 * P2^0 * P3^Q3 + P1^0 * P2^1 * P3^0 + 
   P1^0 * P2^1 * P3^1 + P1^0 * P2^1 * P3^2 + 
   ................ + P1^0 * P2^1 * P3^Q3 +
   .
   .
   .
   P1^Q1 * P2^Q2 * P3^0 + P1^Q1 * P2^Q2 * P3^1 + 
   P1^Q1 * P2^Q2 * P3^2 + .......... + 
   P1^Q1 * P2^Q2 * P3^Q3

Above can be written as,
(((P1^(Q1+1)) - 1) / 
  (P1 - 1)) * (((P2^(Q2+1)) - 1) / 
  (P2 - 1)) * (((P3^(Q3 + 1)) - 1) / 
  (P3 - 1))
```

以下是基于上述公式的实现。

## C++

```
// C++ program to find sum of proper divisors for
// every element in an array.
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000001
#define pii pair<int, int>
#define F first
#define S second

// To store prime factors and their
// powers
vector<pii> factors[MAX];

// Fills factors such that factors[i] is
// a vector of pairs containing prime factors
// (of i) and their powers.
// Also sets values in isPrime[]
void sieveOfEratothenese()
{
    // To check if a number is prime
    bool isPrime[MAX];
    memset(isPrime, true, sizeof(isPrime));
    isPrime[0] = isPrime[1] = false;

    for (int i = 2; i < MAX; i++)
    {
        // If i is prime, then update its
        // powers in all multiples of it.
        if (isPrime[i])
        {
            for (int j = i; j < MAX; j += i)
            {
                int k, l;
                isPrime[j] = false;
                for (k = j, l = 0; k % i == 0; l++, k /= i)
                    ;
                factors[j].push_back(make_pair(i, l));
            }
        }
    }
}

// Returns sum of proper divisors of num
// using factors[]
int sumOfProperDivisors(int num)
{
    // Applying above discussed formula for every
    // array element
    int mul = 1;
    for (int i = 0; i < factors[num].size(); i++)
        mul *= ((pow(factors[num][i].F,
                     factors[num][i].S + 1) - 1) /
                (factors[num][i].F - 1));
    return mul - num;
}

// Driver code
int main()
{
    sieveOfEratothenese();
    int arr[] = { 8, 13, 24, 36, 59, 75, 91 };
    for (int i = 0; i < sizeof(arr) / sizeof(int); i++)
        cout << sumOfProperDivisors(arr[i]) << " ";
    cout << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of proper divisors for
// every element in an array.
import java.util.*;

class GFG
{

static final int MAX = 100001;

static class pair
{
    int F, S;

    public pair(int f, int s) {
        F = f;
        S = s;
    }

}
// To store prime factors and their
// powers
static Vector<pair> []factors = new Vector[MAX];

// Fills factors such that factors[i] is
// a vector of pairs containing prime factors
// (of i) and their powers.
// Also sets values in isPrime[]
static void sieveOfEratothenese()
{
    // To check if a number is prime
    boolean []isPrime = new boolean[MAX];
    Arrays.fill(isPrime, true);
    isPrime[0] = isPrime[1] = false;

    for (int i = 2; i < MAX; i++)
    {
        // If i is prime, then update its
        // powers in all multiples of it.
        if (isPrime[i])
        {
            for (int j = i; j < MAX; j += i)
            {
                int k, l;
                isPrime[j] = false;
                for (k = j, l = 0; k % i == 0; l++, k /= i)
                    ;
                factors[j].add(new pair(i, l));
            }
        }
    }
}

// Returns sum of proper divisors of num
// using factors[]
static int sumOfProperDivisors(int num)
{
    // Applying above discussed formula for every
    // array element
    int mul = 1;
    for (int i = 0; i < factors[num].size(); i++)
        mul *= ((Math.pow(factors[num].get(i).F,
                    factors[num].get(i).S + 1) - 1) /
                (factors[num].get(i).F - 1));
    return mul - num;
}

// Driver code
public static void main(String[] args)
{
    for (int i = 0; i < MAX; i++)
        factors[i] = new Vector<pair>();
    sieveOfEratothenese();
    int arr[] = { 8, 13, 24, 36, 59, 75, 91 };
    for (int i = 0; i < arr.length; i++)
        System.out.print(sumOfProperDivisors(arr[i])+ " ");
    System.out.println();
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find sum of proper divisors for
// every element in an array.
using System;
using System.Collections.Generic;

class GFG
{

static readonly int MAX = 100001;

class pair
{
    public int F, S;

    public pair(int f, int s)
    {
        F = f;
        S = s;
    }

}

// To store prime factors and their
// powers
static List<pair> []factors = new List<pair>[MAX];

// Fills factors such that factors[i] is
// a vector of pairs containing prime factors
// (of i) and their powers.
// Also sets values in isPrime[]
static void sieveOfEratothenese()
{
    // To check if a number is prime
    bool []isPrime = new bool[MAX];
    for (int i = 0; i < MAX; i++)
        isPrime[i] = true;
    isPrime[0] = isPrime[1] = false;

    for (int i = 2; i < MAX; i++)
    {
        // If i is prime, then update its
        // powers in all multiples of it.
        if (isPrime[i])
        {
            for (int j = i; j < MAX; j += i)
            {
                int k, l;
                isPrime[j] = false;
                for (k = j, l = 0; k % i == 0; l++, k /= i)
                    ;
                factors[j].Add(new pair(i, l));
            }
        }
    }
}

// Returns sum of proper divisors of num
// using factors[]
static int sumOfProperDivisors(int num)
{
    // Applying above discussed formula for every
    // array element
    int mul = 1;
    for (int i = 0; i < factors[num].Count; i++)
        mul *= (int)((Math.Pow(factors[num][i].F,
                    factors[num][i].S + 1) - 1) /
                (factors[num][i].F - 1));
    return mul - num;
}

// Driver code
public static void Main(String[] args)
{
    for (int i = 0; i < MAX; i++)
        factors[i] = new List<pair>();
    sieveOfEratothenese();
    int []arr = { 8, 13, 24, 36, 59, 75, 91 };
    for (int i = 0; i < arr.Length; i++)
        Console.Write(sumOfProperDivisors(arr[i])+ " ");
    Console.WriteLine();
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find sum of proper divisors for
// every element in an array.

let MAX = 100001;
class pair
{
    constructor(f,s)
    {
        this.F = f;
           this.S = s;
    }
}

// To store prime factors and their
// powers
let factors = new Array(MAX);

// Fills factors such that factors[i] is
// a vector of pairs containing prime factors
// (of i) and their powers.
// Also sets values in isPrime[]
function sieveOfEratothenese()
{
    // To check if a number is prime
    let isPrime = new Array(MAX);
    for(let i=0;i<MAX;i++)
    {
        isPrime[i]=true;
    }
    isPrime[0] = isPrime[1] = false;

    for (let i = 2; i < MAX; i++)
    {
        // If i is prime, then update its
        // powers in all multiples of it.
        if (isPrime[i])
        {
            for (let j = i; j < MAX; j += i)
            {
                let k, l;
                isPrime[j] = false;
                for (k = j, l = 0; k % i == 0; l++, k = Math.floor(k/i))
                    ;
                factors[j].push(new pair(i, l));
            }
        }
    }
}

// Returns sum of proper divisors of num
// using factors[]
function sumOfProperDivisors(num)
{
    // Applying above discussed formula for every
    // array element
    let mul = 1;
    for (let i = 0; i < factors[num].length; i++)
        mul *= Math.floor((Math.pow(factors[num][i].F,
        factors[num][i].S + 1) - 1) / (factors[num][i].F - 1));
    return mul - num;
}

// Driver code
for (let i = 0; i < MAX; i++)
    factors[i] = [];
sieveOfEratothenese();
let arr = [ 8, 13, 24, 36, 59, 75, 91 ];
for (let i = 0; i < arr.length; i++)
    document.write(sumOfProperDivisors(arr[i])+ " ");
document.write("<br>");

// This code is contributed by rag2127

</script>
```

**输出:**

```
7 1 36 55 1 49 21
```

本文由 **Shubham Singh (singh_8)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。