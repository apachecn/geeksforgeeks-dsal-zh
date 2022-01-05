# 求给定数的超级幂

> 原文:[https://www . geesforgeks . org/find-给定数字的超级幂/](https://www.geeksforgeeks.org/find-the-super-power-of-a-given-number/)

给定一个整数![n   ](img/9568f18f8a74cc2f215afd053ad828dd.png "Rendered by QuickLaTeX.com")。任务是从![n   ](img/9568f18f8a74cc2f215afd053ad828dd.png "Rendered by QuickLaTeX.com")的因式分解中找到超级大国。
**超级大国**是质数分解中质数最高的国家。

```
Input :  n = 32
Output :  5

Input : n = 240
Output : 4
```

为了找到任意给定数的超级幂![n   ](img/9568f18f8a74cc2f215afd053ad828dd.png "Rendered by QuickLaTeX.com")，我们必须完成 n 的因式分解，并找出所有质因数中最高的幂。
**注**:使用[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)存储素数列表在优化方面很有用。
**算法** :

*   迭代素数并计算 n 的因式分解。
*   对于存储的素数列表中的每个素数，也是 n 的因子，
    找到它的幂，并检查它的超幂。

下面是上述方法的实现:

## C++

```
// CPP for finding super power of n
#include <bits/stdc++.h>
#define MAX 100000
using namespace std;

// global hash for prime
bool prime[100002];

// sieve method for storing a list of prime
void SieveOfEratosthenes()
{
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= MAX; p++)
        if (prime[p] == true)
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
}

// function to return super power
int superpower(int n)
{
    SieveOfEratosthenes();
    int superPower = 0, factor = 0;
    int i = 2;
    // find the super power
    while (n > 1 && i <= MAX) {
        if (prime[i]) {
            factor = 0;
            while (n % i == 0 && n > 1) {
                factor++;
                n = n / i;
            }

            if (superPower < factor)
                superPower = factor;
        }
        i++;
    }

    return superPower;
}

// Driver program
int main()
{
    int n = 256;
    cout << superpower(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java for finding super power of n

class GFG{
static int MAX=100000;
// global hash for prime
static boolean[] prime=new boolean[100002];

// sieve method for storing a list of prime
static void SieveOfEratosthenes()
{

    for (int p = 2; p * p <= MAX; p++)
        if (prime[p] == false)
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = true;
}

// function to return super power
static int superpower(int n)
{
    SieveOfEratosthenes();
    int superPower = 0, factor = 0;
    int i = 2;
    // find the super power
    while (n > 1 && i <= MAX) {
        if (!prime[i]) {
            factor = 0;
            while (n % i == 0 && n > 1) {
                factor++;
                n = n / i;
            }

            if (superPower < factor)
                superPower = factor;
        }
        i++;
    }

    return superPower;
}

// Driver program
public static void main(String[] args)
{
    int n = 256;
    System.out.println(superpower(n));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 for finding super
# power of n
MAX = 100000;

# global hash for prime
prime = [True] * 100002;

# sieve method for storing
# a list of prime
def SieveOfEratosthenes():

    p = 2;
    while(p * p <= MAX):
        if (prime[p] == True):
            i = p * 2;
            while(i <= MAX):
                prime[i] = False;
                i += p;
        p += 1;

# function to return super power
def superpower(n):

    SieveOfEratosthenes();
    superPower = 0;
    factor = 0;
    i = 2;

    # find the super power
    while (n > 1 and i <= MAX):
        if (prime[i]):
            factor = 0;
            while (n % i == 0 and n > 1):
                factor += 1;
                n = int(n / i);

            if (superPower < factor):
                superPower = factor;
        i += 1;

    return superPower;

# Driver Code
n = 256;
print(superpower(n));

# This code is contributed by mits
```

## C#

```
// C# for finding super power of n

class GFG
{
static int MAX = 100000;

// global hash for prime
static bool[] prime = new bool[100002];

// sieve method for storing
// a list of prime
static void SieveOfEratosthenes()
{

    for (int p = 2;
             p * p <= MAX; p++)
        if (prime[p] == false)
            for (int i = p * 2;
                     i <= MAX; i += p)
                prime[i] = true;
}

// function to return super power
static int superpower(int n)
{
    SieveOfEratosthenes();
    int superPower = 0, factor = 0;
    int i = 2;

    // find the super power
    while (n > 1 && i <= MAX)
    {
        if (!prime[i])
        {
            factor = 0;
            while (n % i == 0 && n > 1)
            {
                factor++;
                n = n / i;
            }

            if (superPower < factor)
                superPower = factor;
        }
        i++;
    }

    return superPower;
}

// Driver Code
static void Main()
{
    int n = 256;
    System.Console.WriteLine(superpower(n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP for finding super power of n
$MAX = 100000;

// global hash for prime
$prime = array_fill(0, 100002, true);

// sieve method for storing
// a list of prime
function SieveOfEratosthenes()
{
    global $MAX, $prime;

    for ($p = 2; $p * $p <= $MAX; $p++)
        if ($prime[$p] == true)
            for ($i = $p * 2;
                 $i <= $MAX; $i += $p)
                $prime[$i] = false;
}

// function to return super power
function superpower($n)
{
    SieveOfEratosthenes();
    global $MAX, $prime;
    $superPower = 0;
    $factor = 0;
    $i = 2;
    // find the super power
    while ($n > 1 && $i <= $MAX)
    {
        if ($prime[$i])
        {
            $factor = 0;
            while ($n % $i == 0 && $n > 1)
            {
                $factor++;
                $n = $n / $i;
            }

            if ($superPower < $factor)
                $superPower = $factor;
        }
        $i++;
    }

    return $superPower;
}

// Driver Code
$n = 256;
echo superpower($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript for finding super power of n
var MAX = 100000;

// global hash for prime
var prime = Array(100002).fill(true);

// sieve method for storing a list of prime
function SieveOfEratosthenes()
{
    for (var p = 2; p * p <= MAX; p++)
        if (prime[p] == true)
            for (var i = p * 2; i <= MAX; i += p)
                prime[i] = false;
}

// function to return super power
function superpower(n)
{
    SieveOfEratosthenes();
    var superPower = 0, factor = 0;
    var i = 2;
    // find the super power
    while (n > 1 && i <= MAX) {
        if (prime[i]) {
            factor = 0;
            while (n % i == 0 && n > 1) {
                factor++;
                n = n / i;
            }

            if (superPower < factor)
                superPower = factor;
        }
        i++;
    }

    return superPower;
}

// Driver program
var n = 256;
document.write( superpower(n));

</script>
```

**Output:** 

```
8
```