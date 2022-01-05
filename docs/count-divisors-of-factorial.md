# 计算阶乘的除数

> 原文:[https://www.geeksforgeeks.org/count-divisors-of-factorial/](https://www.geeksforgeeks.org/count-divisors-of-factorial/)

给定一个数字 **n** ，计算 **n 的除数总数！**。

**示例:**

> **输入:** n = 4
> **输出:** 8
> **解释:**
> 4！是 24 岁。24 的除数是 1、2、3、4、6、
> 8、12 和 24。
> 
> **输入:** n = 5
> **输出:** 16
> **说明:**
> 5！是 120。120 的除数是 1、2、3、4、5、6、8、10、12、15、20、24、30、40、60 和 12

一个简单的解决方案是首先计算给定数的阶乘，然后计算阶乘的除数。这种解决方案效率不高，并且可能由于阶乘计算而导致溢出。
更好的解决方案是基于[勒让德公式](https://www.geeksforgeeks.org/given-p-and-n-find-the-largest-x-such-that-px-divides-n-2/)。以下是步骤:

1.  查找所有小于或等于 n(输入数)的质数。对此我们可以使用[筛选算法](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)。设 n 为 6。所有小于 6 的素数都是{2，3，5}。
2.  对于每个质数，p 求它除 n 的最大幂！。为此我们使用[勒让德公式](https://www.geeksforgeeks.org/given-p-and-n-find-the-largest-x-such-that-px-divides-n-2/)。
    除以 n 的最大幂的值！是⌊n/p⌋+⌊n/(p<sup>2</sup>)⌋+⌊n/(p<sup>3</sup>)⌋+……
    让这些值为 exp1，exp2，exp3，…使用上面的公式，我们得到 n = 6 的以下值。
    *   2 除以 6 的最大幂！，exp1 = 4。
    *   3 除以 6 的最大幂！，exp2 = 2。
    *   5 除以 6 的最大幂！，exp3 = 1。
3.  结果是(exp1 + 1) * (exp2 + 1) * (exp3 + 1) …对于所有素数，对于 n = 6，exp1、exp2 和 exp3 的值分别是 4 ^ 2 和 1(在上面的步骤 2 中计算)。所以我们的结果是(4 + 1)*(2 + 1) * (1 + 1) = 30

以下是上述想法的实现。

## C++

```
// C++ program to find count of divisors in n!
#include<bits/stdc++.h>
using namespace std;
typedef unsigned long long int ull;

// allPrimes[] stores all prime numbers less
// than or equal to n.
vector<ull> allPrimes;

// Fills above vector allPrimes[] for a given n
void sieve(int n)
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // not a prime, else true.
    vector<bool> prime(n+1, true);

    // Loop to update prime[]
    for (int p=2; p*p<=n; p++)
    {
        // If prime[p] is not changed, then it
        // is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            for (int i=p*2; i<=n; i += p)
                prime[i] = false;
        }
    }

    // Store primes in the vector allPrimes
    for (int p=2; p<=n; p++)
        if (prime[p])
            allPrimes.push_back(p);
}

// Function to find all result of factorial number
ull factorialDivisors(ull n)
{
    sieve(n);  // create sieve

    // Initialize result
    ull result = 1;

    // find exponents of all primes which divides n
    // and less than n
    for (int i=0; i < allPrimes.size(); i++)
    {
        // Current divisor
        ull p = allPrimes[i];

        // Find the highest power (stored in exp)'
        // of allPrimes[i] that divides n using
        // Legendre's formula.
        ull exp = 0;
        while (p <= n)
        {
            exp = exp + (n/p);
            p = p*allPrimes[i];
        }

        // Multiply exponents of all primes less
        // than n
        result = result*(exp+1);
    }

    // return total divisors
    return result;
}

// Driver code
int main()
{
    cout << factorialDivisors(6);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find count of divisors in n!

import java.util.*;
class GFG
{
    // allPrimes[] stores all prime numbers less
    // than or equal to n.
    static Vector<Integer> allPrimes=new Vector<Integer>();

    // Fills above vector allPrimes[] for a given n
    static void sieve(int n){
        // Create a boolean array "prime[0..n]" and
       // initialize all entries it as true. A value
        // in prime[i] will finally be false if i is
        // not a prime, else true.
        boolean []prime=new boolean[n+1];

        for(int i=0;i<=n;i++)
        prime[i]=true;

        // Loop to update prime[]
        for (int p=2; p*p<=n; p++)
        {
        // If prime[p] is not changed, then it
        // is a prime
        if (prime[p] == true)
        {
        // Update all multiples of p
            for (int i=p*2; i<=n; i += p)
                prime[i] = false;
        }
        }
        // Store primes in the vector allPrimes
            for (int p=2; p<=n; p++)
                if (prime[p])
                    allPrimes.add(p);
        }

        // Function to find all result of factorial number
        static long factorialDivisors(int n)
        {
            sieve(n); // create sieve

            // Initialize result
            long result = 1;

            // find exponents of all primes which divides n
            // and less than n
            for (int i=0; i < allPrimes.size(); i++)
            {
                // Current divisor
                long p = allPrimes.get(i);

                // Find the highest power (stored in exp)'
                // of allPrimes[i] that divides n using
                // Legendre's formula.
                long exp = 0;
                while (p <= n)
                {
                    exp = exp + (n/p);
                    p = p*allPrimes.get(i);
                }

                // Multiply exponents of all primes less
                // than n
                result = result*(exp+1);
            }

            // return total divisors
            return result;
        }

        // Driver code
        public static void main(String []args)
        {
            System.out.println(factorialDivisors(6));

        }

}

//This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 program to find count
# of divisors in n!

# allPrimes[] stores all prime
# numbers less than or equal to n.
allPrimes = [];

# Fills above vector allPrimes[]
# for a given n
def sieve(n):

    # Create a boolean array "prime[0..n]"
    # and initialize all entries it as true.
    # A value in prime[i] will finally be
    # false if i is not a prime, else true.
    prime = [True] * (n + 1);

    # Loop to update prime[]
    p = 2;
    while(p * p <= n):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            i = p * 2;
            while(i <= n):
                prime[i] = False;
                i += p;
        p += 1;

    # Store primes in the vector allPrimes
    for p in range(2, n + 1):
        if (prime[p]):
            allPrimes.append(p);

# Function to find all result of
# factorial number
def factorialDivisors(n):

    sieve(n); # create sieve

    # Initialize result
    result = 1;

    # find exponents of all primes
    # which divides n and less than n
    for i in range(len(allPrimes)):

        # Current divisor
        p = allPrimes[i];

        # Find the highest power (stored in exp)'
        # of allPrimes[i] that divides n using
        # Legendre's formula.
        exp = 0;
        while (p <= n):
            exp = exp + int(n / p);
            p = p * allPrimes[i];

        # Multiply exponents of all
        # primes less than n
        result = result * (exp + 1);

    # return total divisors
    return result;

# Driver Code
print(factorialDivisors(6));

# This code is contributed by mits
```

## C#

```
// C# program to find count of divisors in n!
using System;
using System.Collections;

class GFG
{
    // allPrimes[] stores all prime numbers less
    // than or equal to n.
    static ArrayList allPrimes = new ArrayList();

    // Fills above vector allPrimes[] for a given n
    static void sieve(int n)
    {

        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value
        // in prime[i] will finally be false if i is
        // not a prime, else true.
        bool[] prime = new bool[n+1];

        for(int i = 0; i <= n; i++)
        prime[i] = true;

        // Loop to update prime[]
        for (int p = 2; p * p <= n; p++)
        {
        // If prime[p] is not changed, then it
        // is a prime
        if (prime[p] == true)
        {
        // Update all multiples of p
            for (int i = p*2; i <= n; i += p)
                prime[i] = false;
        }
        }
        // Store primes in the vector allPrimes
            for (int p = 2; p <= n; p++)
                if (prime[p])
                    allPrimes.Add(p);
        }

        // Function to find all result of factorial number
        static int factorialDivisors(int n)
        {
            sieve(n); // create sieve

            // Initialize result
            int result = 1;

            // find exponents of all primes which divides n
            // and less than n
            for (int i = 0; i < allPrimes.Count; i++)
            {
                // Current divisor
                int p = (int)allPrimes[i];

                // Find the highest power (stored in exp)'
                // of allPrimes[i] that divides n using
                // Legendre's formula.
                int exp = 0;
                while (p <= n)
                {
                    exp = exp + (n / p);
                    p = p * (int)allPrimes[i];
                }

                // Multiply exponents of all primes less
                // than n
                result = result * (exp + 1);
            }

            // return total divisors
            return result;
        }

        // Driver code
        public static void Main()
        {
            Console.WriteLine(factorialDivisors(6));
        }
}

//This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find count of
// divisors in n!

// allPrimes[] stores all prime numbers
// less than or equal to n.
$allPrimes = array();

// Fills above vector allPrimes[]
// for a given n
function sieve($n)
{
    global $allPrimes;

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // not a prime, else true.
    $prime = array_fill(0, $n + 1, true);

    // Loop to update prime[]
    for ($p = 2; $p * $p <= $n; $p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {
            // Update all multiples of p
            for ($i = $p * 2; $i <= $n; $i += $p)
                $prime[$i] = false;
        }
    }

    // Store primes in the vector allPrimes
    for ($p = 2; $p <= $n; $p++)
        if ($prime[$p])
            array_push($allPrimes, $p);
}

// Function to find all result
// of factorial number
function factorialDivisors($n)
{
    global $allPrimes;
    sieve($n); // create sieve

    // Initialize result
    $result = 1;

    // find exponents of all primes
    // which divides n and less than n
    for ($i = 0; $i < count($allPrimes); $i++)
    {
        // Current divisor
        $p = $allPrimes[$i];

        // Find the highest power (stored in exp)
        // of allPrimes[i] that divides n using
        // Legendre's formula.
        $exp = 0;
        while ($p <= $n)
        {
            $exp = $exp + (int)($n / $p);
            $p = $p * $allPrimes[$i];
        }

        // Multiply exponents of all primes
        // less than n
        $result = $result * ($exp + 1);
    }

    // return total divisors
    return $result;
}

// Driver Code
echo factorialDivisors(6);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find count of divisors in n!

    // allPrimes[] stores all prime numbers less
    // than or equal to n.
    let allPrimes = [];

    // Fills above vector allPrimes[] for a given n
    function sieve(n)
    {

        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value
        // in prime[i] will finally be false if i is
        // not a prime, else true.
        let prime = new Array(n+1);

        for(let i = 0; i <= n; i++)
            prime[i] = true;

        // Loop to update prime[]
        for (let p = 2; p * p <= n; p++)
        {
          // If prime[p] is not changed, then it
          // is a prime
          if (prime[p] == true)
          {
          // Update all multiples of p
              for (let i = p*2; i <= n; i += p)
                  prime[i] = false;
          }
        }
        // Store primes in the vector allPrimes
        for (let p = 2; p <= n; p++)
          if (prime[p])
            allPrimes.push(p);
      }

    // Function to find all result of factorial number
    function factorialDivisors(n)
    {
      sieve(n); // create sieve

      // Initialize result
      let result = 1;

      // find exponents of all primes which divides n
      // and less than n
      for (let i = 0; i < allPrimes.length; i++)
      {
        // Current divisor
        let p = allPrimes[i];

        // Find the highest power (stored in exp)'
        // of allPrimes[i] that divides n using
        // Legendre's formula.
        let exp = 0;
        while (p <= n)
        {
          exp = exp + parseInt(n / p, 10);
          p = p * allPrimes[i];
        }

        // Multiply exponents of all primes less
        // than n
        result = result * (exp + 1);
      }

      // return total divisors
      return result;
    }

    document.write(factorialDivisors(6));

</script>
```

**Output**

```
30
```

本文由 [**沙莎克·米什拉(古卢)**](https://practice.geeksforgeeks.org/user-profile.php?user=Shashank%20Mishra) 供稿。本文由 GeeksforGeeks 团队审阅。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。