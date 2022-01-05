# 用于多重评估的优化欧拉全能函数

> 原文:[https://www . geesforgeks . org/optimized-Euler-totilent-function-multi-evaluations/](https://www.geeksforgeeks.org/optimized-euler-totient-function-multiple-evaluations/)

[**E**uler**T**otient**F**function(ETF)](https://www.geeksforgeeks.org/eulers-totient-function/)φ(n)对于输入 n 是{1，2，3，…，n}中与 n 相对素数的数的计数，即 [GCD(最大公约数)](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)与 n 为 1 的数。
**举例:**

```
Φ(5) = 4
gcd(1, 5) is 1, gcd(2, 5) is 1, 
gcd(3, 5) is 1 and gcd(4, 5) is 1

Φ(6) = 2
gcd(1, 6) is 1 and gcd(5, 6) is 1,
```

我们已经讨论了[计算欧拉全能函数](https://www.geeksforgeeks.org/eulers-totient-function/)的不同方法，这些方法适用于单个输入。在像《10^5 时报》那样我们不得不多次调用欧拉全能函数的问题中，简单的解决方案将导致 TLE(超过时间限制)。想法是用厄拉多塞的[筛子。
使用埃拉托斯特尼](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)的[筛找出所有达到最大极限的质数，比如 10^5。
为了计算φ(n)，我们执行以下操作。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

1.  将结果初始化为 n。
2.  迭代所有小于或等于 n 的平方根的素数(这是它不同于简单方法的地方。我们不是迭代所有小于或等于平方根的数字，而是只迭代素数)。让当前素数为 p，我们检查 p 是否除以 n，如果是，我们通过重复用 n 除 p 来从 n 中移除 p 的所有出现，我们还将我们的结果减少 n/p(这许多数不会像用 n 除 1 那样具有 GCD)。
3.  最后我们返回结果。

## C++

```
// C++ program to efficiently compute values
// of euler totient function for multiple inputs.
#include <bits/stdc++.h>
using namespace std;

#define ll long long
const int MAX = 100001;

// Stores prime numbers upto MAX - 1 values
vector<ll> p;

// Finds prime numbers upto MAX-1 and
// stores them in vector p
void sieve()
{
    ll isPrime[MAX+1];

    for (ll i = 2; i<= MAX; i++)
    {
        // if prime[i] is not marked before
        if (isPrime[i] == 0)
        {
            // fill vector for every newly
            // encountered prime
            p.push_back(i);

            // run this loop till square root of MAX,
            // mark the index i * j as not prime
            for (ll j = 2; i * j<= MAX; j++)
                isPrime[i * j]= 1;
        }
    }
}

// function to find totient of n
ll phi(ll n)
{
    ll res = n;

    // this loop runs sqrt(n / ln(n)) times
    for (ll i=0; p[i]*p[i] <= n; i++)
    {
        if (n % p[i]== 0)
        {
            // subtract multiples of p[i] from r
            res -= (res / p[i]);

            // Remove all occurrences of p[i] in n
            while (n % p[i]== 0)
               n /= p[i];
        }
    }

    // when n has prime factor greater
    // than sqrt(n)
    if (n > 1)
       res -= (res / n);

    return res;
}

// Driver code
int main()
{
    // preprocess all prime numbers upto 10 ^ 5
    sieve();
    cout << phi(11) << "\n";
    cout << phi(21) << "\n";
    cout << phi(31) << "\n";
    cout << phi(41) << "\n";
    cout << phi(51) << "\n";
    cout << phi(61) << "\n";
    cout << phi(91) << "\n";
    cout << phi(101) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to efficiently compute values
// of euler totient function for multiple inputs.
import java.util.*;

class GFG{
static int MAX = 100001;

// Stores prime numbers upto MAX - 1 values
static ArrayList<Integer> p = new ArrayList<Integer>();

// Finds prime numbers upto MAX-1 and
// stores them in vector p
static void sieve()
{
    int[] isPrime=new int[MAX+1];

    for (int i = 2; i<= MAX; i++)
    {
        // if prime[i] is not marked before
        if (isPrime[i] == 0)
        {
            // fill vector for every newly
            // encountered prime
            p.add(i);

            // run this loop till square root of MAX,
            // mark the index i * j as not prime
            for (int j = 2; i * j<= MAX; j++)
                isPrime[i * j]= 1;
        }
    }
}

// function to find totient of n
static int phi(int n)
{
    int res = n;

    // this loop runs sqrt(n / ln(n)) times
    for (int i=0; p.get(i)*p.get(i) <= n; i++)
    {
        if (n % p.get(i)== 0)
        {
            // subtract multiples of p[i] from r
            res -= (res / p.get(i));

            // Remove all occurrences of p[i] in n
            while (n % p.get(i)== 0)
            n /= p.get(i);
        }
    }

    // when n has prime factor greater
    // than sqrt(n)
    if (n > 1)
    res -= (res / n);

    return res;
}

// Driver code
public static void main(String[] args)
{
    // preprocess all prime numbers upto 10 ^ 5
    sieve();
    System.out.println(phi(11));
    System.out.println(phi(21));
    System.out.println(phi(31));
    System.out.println(phi(41));
    System.out.println(phi(51));
    System.out.println(phi(61));
    System.out.println(phi(91));
    System.out.println(phi(101));

}
}
// this code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to efficiently compute values
# of euler totient function for multiple inputs.

MAX = 100001;

# Stores prime numbers upto MAX - 1 values
p = [];

# Finds prime numbers upto MAX-1 and
# stores them in vector p
def sieve():

    isPrime = [0] * (MAX + 1);

    for i in range(2, MAX + 1):

        # if prime[i] is not marked before
        if (isPrime[i] == 0):

            # fill vector for every newly
            # encountered prime
            p.append(i);

            # run this loop till square root of MAX,
            # mark the index i * j as not prime
            j = 2;
            while (i * j <= MAX):
                isPrime[i * j]= 1;
                j += 1;

# function to find totient of n
def phi(n):

    res = n;

    # this loop runs sqrt(n / ln(n)) times
    i = 0;
    while (p[i] * p[i] <= n):
        if (n % p[i]== 0):

            # subtract multiples of p[i] from r
            res -= int(res / p[i]);

            # Remove all occurrences of p[i] in n
            while (n % p[i]== 0):
                n = int(n / p[i]);
        i += 1;

    # when n has prime factor greater
    # than sqrt(n)
    if (n > 1):
        res -= int(res / n);

    return res;

# Driver code

# preprocess all prime numbers upto 10 ^ 5
sieve();
print(phi(11));
print(phi(21));
print(phi(31));
print(phi(41));
print(phi(51));
print(phi(61));
print(phi(91));
print(phi(101));

# This code is contributed by mits
```

## C#

```
// C# program to efficiently compute values
// of euler totient function for multiple inputs.
using System;
using System.Collections;
class GFG{
static int MAX = 100001;

// Stores prime numbers upto MAX - 1 values
static ArrayList p = new ArrayList();

// Finds prime numbers upto MAX-1 and
// stores them in vector p
static void sieve()
{
    int[] isPrime=new int[MAX+1];

    for (int i = 2; i<= MAX; i++)
    {
        // if prime[i] is not marked before
        if (isPrime[i] == 0)
        {
            // fill vector for every newly
            // encountered prime
            p.Add(i);

            // run this loop till square root of MAX,
            // mark the index i * j as not prime
            for (int j = 2; i * j<= MAX; j++)
                isPrime[i * j]= 1;
        }
    }
}

// function to find totient of n
static int phi(int n)
{
    int res = n;

    // this loop runs sqrt(n / ln(n)) times
    for (int i=0; (int)p[i]*(int)p[i] <= n; i++)
    {
        if (n % (int)p[i]== 0)
        {
            // subtract multiples of p[i] from r
            res -= (res / (int)p[i]);

            // Remove all occurrences of p[i] in n
            while (n % (int)p[i]== 0)
            n /= (int)p[i];
        }
    }

    // when n has prime factor greater
    // than sqrt(n)
    if (n > 1)
    res -= (res / n);

    return res;
}

// Driver code
static void Main()
{
    // preprocess all prime numbers upto 10 ^ 5
    sieve();
    Console.WriteLine(phi(11));
    Console.WriteLine(phi(21));
    Console.WriteLine(phi(31));
    Console.WriteLine(phi(41));
    Console.WriteLine(phi(51));
    Console.WriteLine(phi(61));
    Console.WriteLine(phi(91));
    Console.WriteLine(phi(101));

}
}
// this code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to efficiently compute values
// of euler totient function for multiple inputs.

$MAX = 100001;

// Stores prime numbers upto MAX - 1 values
$p = array();

// Finds prime numbers upto MAX-1 and
// stores them in vector p
function sieve()
{
    global $MAX,$p;
    $isPrime=array_fill(0,$MAX+1,0);

    for ($i = 2; $i<= $MAX; $i++)
    {
        // if prime[i] is not marked before
        if ($isPrime[$i] == 0)
        {
            // fill vector for every newly
            // encountered prime
            array_push($p,$i);

            // run this loop till square root of MAX,
            // mark the index i * j as not prime
            for ($j = 2; $i * $j<= $MAX; $j++)
                $isPrime[$i * $j]= 1;
        }
    }
}

// function to find totient of n
function phi($n)
{
    global $p;
    $res = $n;

    // this loop runs sqrt(n / ln(n)) times
    for ($i=0; $p[$i]*$p[$i] <= $n; $i++)
    {
        if ($n % $p[$i]== 0)
        {
            // subtract multiples of p[i] from r
            $res -= (int)($res / $p[$i]);

            // Remove all occurrences of p[i] in n
            while ($n % $p[$i]== 0)
            $n = (int)($n/$p[$i]);
        }
    }

    // when n has prime factor greater
    // than sqrt(n)
    if ($n > 1)
    $res -= (int)($res / $n);

    return $res;
}

// Driver code

    // preprocess all prime numbers upto 10 ^ 5
    sieve();
    print(phi(11)."\n");
    print(phi(21)."\n");
    print(phi(31)."\n");
    print(phi(41)."\n");
    print(phi(51)."\n");
    print(phi(61)."\n");
    print(phi(91)."\n");
    print(phi(101)."\n");

// this code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to efficiently compute values
// of euler totient function for multiple inputs.

var MAX = 100001;

// Stores prime numbers upto MAX - 1 values
var p = [];

// Finds prime numbers upto MAX-1 and
// stores them in vector p
function sieve()
{
    var isPrime = Array(MAX+1).fill(0);

    for (var i = 2; i<= MAX; i++)
    {
        // if prime[i] is not marked before
        if (isPrime[i] == 0)
        {
            // fill vector for every newly
            // encountered prime
            p.push(i);

            // run this loop till square root of MAX,
            // mark the index i * j as not prime
            for (var j = 2; i * j<= MAX; j++)
                isPrime[i * j]= 1;
        }
    }
}

// function to find totient of n
function phi(n)
{
    var res = n;

    // this loop runs sqrt(n / ln(n)) times
    for (var i=0; p[i]*p[i] <= n; i++)
    {
        if (n % p[i]== 0)
        {
            // subtract multiples of p[i] from r
            res -= parseInt(res / p[i]);

            // Remove all occurrences of p[i] in n
            while (n % p[i]== 0)
            n = parseInt(n/p[i]);
        }
    }

    // when n has prime factor greater
    // than sqrt(n)
    if (n > 1)
    res -= parseInt(res / n);

    return res;
}

// Driver code
// preprocess all prime numbers upto 10 ^ 5
sieve();
document.write(phi(11)+ "<br>");
document.write(phi(21)+ "<br>");
document.write(phi(31)+ "<br>");
document.write(phi(41)+ "<br>");
document.write(phi(51)+ "<br>");
document.write(phi(61)+ "<br>");
document.write(phi(91)+ "<br>");
document.write(phi(101)+ "<br>");

// This code is contributed by rutvik_56.
</script>
```

**输出:**

```
10
12
30
40
32
60
72
100
```

本文由 **Abhishek Rajput** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。