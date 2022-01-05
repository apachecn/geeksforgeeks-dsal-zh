# 罗瑟定理

> 原文:[https://www.geeksforgeeks.org/rossers-theorem/](https://www.geeksforgeeks.org/rossers-theorem/)

在数学中，[罗瑟定理](https://en.wikipedia.org/wiki/Rosser%27s_theorem)规定，对于所有大于 1 的 n，第 n 个素数大于 n 和 n 的自然对数的乘积。
***数学上，***
为 n > = 1，若 p <sub>n</sub> 为第 n 个素数，则
p<sub>n</sub>>n *(ln n)

```
Illustrative Examples:

       For n = 1, nth prime number = 2
    2 > 1 * ln(1)
Explanations, the above relation inherently holds true and it verifies the 
statement of Rosser's Theorem clearly.
Some more examples are, 
       For n = 2, nth prime number = 3
    3 > 2 * ln(2)
       For n = 3, nth prime number = 5
    5 > 3 * ln(3)
       For n = 4, nth prime number = 7
    7 > 4 * ln(4)
       For n = 5, nth prime number = 11
    11 > 5 * ln(5)
       For n = 6, nth prime number = 13
    13 > 6 * ln(6)
```

**代码的方法:**
*使用* [*素数筛*](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) *高效生成素数，并分别检查每个素数的罗瑟定理条件。*

## C++

```
// CPP code to verify Rosser's Theorem
#include <bits/stdc++.h>
using namespace std;

#define show(x) cout << #x << " = " << x << "\n";

vector<int> prime;

// Sieve of Eratosthenes
void sieve()
{
    // prime sieve to generate prime numbers efficiently
    int n = 1e5;
    vector<bool> isprime(n + 2, true);
    isprime[0] = isprime[1] = false;
    for (long long i = 2; i <= n; i++) {
        if (isprime[i]) {
            for (long long j = i * i; j <= n; j += i)
                isprime[j] = false;
        }
    }
    // store primes in prime[] vector
    for (int i = 0; i <= n; i++)
        if (isprime[i])
            prime.push_back(i);
}

// Verifies ROSSER'S THEOREM for all numbers
// smaller than n.
void verifyRosser(int n)
{
    cout << "ROSSER'S THEOREM: nth prime "
            "number > n * (ln n)\n";
    for (int i = 0; i < n; i++)
        if (prime[i] > (i + 1) * log(i + 1)) {
            cout << "For n = " << i + 1
                 << ", nth prime number = "
                 << prime[i] << "\n\t"
                 << prime[i] << " > " << i + 1
                 << " * ln(" << i + 1 << ")\n";
        }
}

int main()
{
    sieve();
    verifyRosser(20);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to verify Rosser's Theorem

import java.util.*;
class GFG
{
    static Vector<Integer> prime=new Vector<Integer>();
    // Sieve of Eratosthenes
    static void sieve()
    {
        // prime sieve to generate prime numbers efficiently
        int n = 10000;
        boolean []isprime=new boolean[n+2];
        for(int i=0;i<n;i++)
        isprime[i]=true;

        isprime[0]=false;
        isprime[1] =false;
        for (int i = 2; i <= n; i++) {
            if (isprime[i]) {
                for (int j = i * i; j <= n; j += i)
                    isprime[j] =false;
            }
        }
        // store primes in prime[] vector
        for (int i = 0; i <= n; i++)
            if (isprime[i])
                prime.add(i);
    }

    // Verifies ROSSER'S THEOREM for all numbers
    // smaller than n.
    static void verifyRosser(int n)
    {
        System.out.println("ROSSER'S THEOREM: nth prime number > n * (ln n)");

        for (int i = 0; i < n; i++)
            if (prime.get(i) > (i + 1) * Math.log(i + 1)) {
                System.out.println( "For n = " + (i+1)
                    + ", nth prime number = "
                    + prime.get(i) + "\n\t"
                    + prime.get(i) + " > " + (i + 1)
                    + " * ln(" + (i + 1) + ")");
            }
    }

    // Driver code
    public static void main(String [] args)
    {
        sieve();
        verifyRosser(20);

    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 code to verify Rosser's Theorem
import math
prime = [];

# Sieve of Eratosthenes
def sieve():

    # prime sieve to generate
    # prime numbers efficiently
    n = 100001;
    isprime = [True] * (n + 2);
    isprime[0] = False;
    isprime[1] = False;
    for i in range(2, n + 1):
        if(isprime[i]):
            j = i * i;
            while (j <= n):
                isprime[j] = False;
                j += i;

    # store primes in
    # prime[] vector
    for i in range(n + 1):
        if (isprime[i]):
            prime.append(i);

# Verifies ROSSER'S THEOREM
# for all numbers smaller than n.
def verifyRosser(n):

    print("ROSSER'S THEOREM: nth",
          "prime number > n * (ln n)");
    for i in range(n):
        if (prime[i] > int((i + 1) * math.log(i + 1))):
            print("For n =", (i + 1), ", nth prime number =",
                   prime[i], "\n\t", prime[i], " >", (i + 1),
                                      "* ln(", (i + 1), ")");

# Driver Code
sieve();
verifyRosser(20);

# This code is contributed
# by mits
```

## C#

```
// C# code to verify Rosser's Theorem
using System;
using System.Collections.Generic;

class GFG
{
    static List<int> prime = new List<int>();

    // Sieve of Eratosthenes
    static void sieve()
    {
        // prime sieve to generate
        // prime numbers efficiently
        int n = 10000;
        bool []isprime = new bool[n + 2];
        for(int i = 0; i < n; i++)
        isprime[i] = true;

        isprime[0] = false;
        isprime[1] = false;
        for (int i = 2; i <= n; i++)
        {
            if (isprime[i])
            {
                for (int j = i * i;
                         j <= n; j += i)
                    isprime[j] = false;
            }
        }

        // store primes in prime[] vector
        for (int i = 0; i <= n; i++)
            if (isprime[i])
                prime.Add(i);
    }

    // Verifies ROSSER'S THEOREM for
    // all numbers smaller than n.
    static void verifyRosser(int n)
    {
        Console.WriteLine("ROSSER'S THEOREM: " +   
                          "nth prime number > n * (ln n)");

        for (int i = 0; i < n; i++)
            if (prime[i] > (i + 1) * Math.Log(i + 1))
            {
                Console.WriteLine( "For n = " + (i + 1) +
                                ", nth prime number = " +
                           prime[i] + "\n\t" + prime[i] +
                             " > " + (i + 1) + " * ln(" +
                                          (i + 1) + ")");
            }
    }

    // Driver code
    public static void Main(String [] args)
    {
        sieve();
        verifyRosser(20);
    }
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to verify
// Rosser's Theorem
$prime;
$y = 0;

// function show($x)
// {echo $x" = ".$x."\n";}

// Sieve of Eratosthenes
function sieve()
{
    global $prime,$y;

    // prime sieve to generate
    // prime numbers efficiently
    $n = 100001;
    $isprime = array_fill(0, ($n + 2), true);
    $isprime[0] = false;
    $isprime[1] = false;
    for ($i = 2; $i <= $n; $i++)
    {
        if ($isprime[$i])
        {
            for ($j = $i * $i;
                 $j <= $n; $j += $i)
                $isprime[$j] = false;
        }
    }

    // store primes in
    // prime[] vector
    for ($i = 0; $i <= $n; $i++)
        if ($isprime[$i])
            $prime[$y++]=$i;
}

// Verifies ROSSER'S THEOREM
// for all numbers smaller than n.
function verifyRosser($n)
{
    global $prime;

    echo "ROSSER'S THEOREM: nth " .
         "prime number > n * (ln n)\n";
    for ($i = 0; $i < $n; $i++)
        if ($prime[$i] > (int)(($i + 1) * log($i + 1)))
        {
            echo "For n = " . ($i + 1).
                 ", nth prime number = " .
                  $prime[$i] . "\n\t" .
                  $prime[$i] . " > " .
                  ($i + 1) . " * ln(" .
                  ($i + 1) . ")\n";
        }
}

// Driver Code
sieve();
verifyRosser(20);

// This code is contributed
// by mits
?>
```

## java 描述语言

```
<script>

// JavaScript code to verify
// Rosser's Theorem
let prime = new Array();
let y = 0;

// function show(x)
// {echo x" = ".x."\n";}

// Sieve of Eratosthenes
function sieve()
{
    // prime sieve to generate
    // prime numbers efficiently
    let n = 100001;
    let isprime = new Array(n + 2).fill(true);
    isprime[0] = false;
    isprime[1] = false;
    for (let i = 2; i <= n; i++)
    {
        if (isprime[i])
        {
            for (let j = i * i;
                j <= n; j += i)
                isprime[j] = false;
        }
    }

    // store primes in
    // prime[] vector
    for (let i = 0; i <= n; i++)
        if (isprime[i])
            prime[y++] = i;
}

// Verifies ROSSER'S THEOREM
// for all numbers smaller than n.
function verifyRosser(n)
{   
    document.write(
    "ROSSER'S THEOREM: nth prime number > n * (ln n) <br>"
    );
    for (let i = 0; i < n; i++)
        if (prime[i] > Math.floor((i + 1) * Math.log(i + 1)))
        {
            document.write("For n = " + (i + 1) +
                ", nth prime number = " +
                prime[i] + "<br>" +
                prime[i] + " > " +
                (i + 1) + " * ln(" +
                (i + 1) + ")<br>");
        }
}

// Driver Code
sieve();
verifyRosser(20);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
ROSSER'S THEOREM: nth prime number > n * (ln n)
For n = 1, nth prime number = 2
    2 > 1 * ln(1)
For n = 2, nth prime number = 3
    3 > 2 * ln(2)
For n = 3, nth prime number = 5
    5 > 3 * ln(3)
For n = 4, nth prime number = 7
    7 > 4 * ln(4)
For n = 5, nth prime number = 11
    11 > 5 * ln(5)
For n = 6, nth prime number = 13
    13 > 6 * ln(6)
For n = 7, nth prime number = 17
    17 > 7 * ln(7)
For n = 8, nth prime number = 19
    19 > 8 * ln(8)
For n = 9, nth prime number = 23
    23 > 9 * ln(9)
For n = 10, nth prime number = 29
    29 > 10 * ln(10)
For n = 11, nth prime number = 31
    31 > 11 * ln(11)
For n = 12, nth prime number = 37
    37 > 12 * ln(12)
For n = 13, nth prime number = 41
    41 > 13 * ln(13)
For n = 14, nth prime number = 43
    43 > 14 * ln(14)
For n = 15, nth prime number = 47
    47 > 15 * ln(15)
For n = 16, nth prime number = 53
    53 > 16 * ln(16)
For n = 17, nth prime number = 59
    59 > 17 * ln(17)
For n = 18, nth prime number = 61
    61 > 18 * ln(18)
For n = 19, nth prime number = 67
    67 > 19 * ln(19)
For n = 20, nth prime number = 71
    71 > 20 * ln(20)
```