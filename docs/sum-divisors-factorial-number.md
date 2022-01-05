# 一个数的阶乘因子之和

> 原文:[https://www . geesforgeks . org/sum-除数-阶乘-数/](https://www.geeksforgeeks.org/sum-divisors-factorial-number/)

给定一个数 n，我们需要计算这个数的阶乘的除数之和。

**示例:**

```
Input : 4
Output : 60
Factorial of 4 is 24\. Divisors of 24 are
1 2 3 4 6 8 12 24, sum of these is 60.

Input : 6
Output : 2418
```

一个**简单的解法**是先计算给定数的阶乘，然后计算阶乘的除数。这种解决方案效率不高，并且可能由于阶乘计算而导致溢出。

下面是上述方法的实现:

## C++

```
// C++ program to find sum of proper divisor of
// factorial of a number
#include <bits/stdc++.h>
using namespace std;

// function to calculate factorial
int fact(int n)
{
    if (n == 0)
        return 1;
    return n * fact(n - 1);
}

// function to calculate sum of divisor
int div(int x)
{
    int ans = 0;
    for (int i = 1; i<= x; i++)
        if (x % i == 0)
            ans += i;
    return ans;
}

// Returns sum of divisors of n!
int sumFactDiv(int n)
{
    return div(fact(n));
}

// Driver Code
int main()
{
    int n = 4;
    cout << sumFactDiv(n);
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// C program to find sum of proper divisor of
// factorial of a number
#include <stdio.h>
// function to calculate factorial

int fact(int n) {
    if (n == 0)
        return 1;
    return n * fact(n - 1);
}

// function to calculate sum of divisor

int div(int x) {
    int ans = 0;
    for (int i = 1; i<= x; i++)
        if (x % i == 0)
            ans += i;
    return ans;
}

// Returns sum of divisors of n!

int sumFactDiv(int n) {
    return div(fact(n));
}

// driver program

int main() {
    int n = 4;
    printf("%d",sumFactDiv(n));
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of proper divisor of
// factorial of a number
import java.io.*;
import java.util.*;

public class Division
{
    // function to calculate factorial
    static int fact(int n)
    {
        if (n == 0)
            return 1;
        return n*fact(n-1);
    }

    // function to calculate sum of divisor
    static int div(int x)
    {
        int ans = 0;
        for (int i = 1; i<= x; i++)
            if (x%i == 0)
                ans += i;
        return ans;
    }

    // Returns sum of divisors of n!
    static int sumFactDiv(int n)
    {
        return div(fact(n));
    }

    // driver program
    public static void main(String args[])
    {
        int n = 4;
        System.out.println(sumFactDiv(n));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find sum of proper
# divisor of factorial of a number

# function to calculate factorial
def fact(n):

    if (n == 0):
        return 1
    return n * fact(n - 1)

# function to calculate sum
# of divisor
def div(x):
    ans = 0;
    for i in range(1, x + 1):
        if (x % i == 0):
            ans += i
    return ans

# Returns sum of divisors of n!
def sumFactDiv(n):
    return div(fact(n))

# Driver Code
n = 4
print(sumFactDiv(n))

# This code is contributed
# by Rajput-Ji
```

## C#

```
// C# program to find sum of proper
// divisor of factorial of a number
using System;
class Division {

    // function to calculate factorial
    static int fac(int n)
    {
        if (n == 0)
            return 1;
        return n * fac(n - 1);
    }

    // function to calculate
    // sum of divisor
    static int div(int x)
    {
        int ans = 0;
        for (int i = 1; i <= x; i++)
            if (x % i == 0)
                ans += i;
        return ans;
    }

    // Returns sum of divisors of n!
    static int sumFactDiv(int n)
    {
        return div(fac(n));
    }

    // Driver Code
    public static void Main()
    {
        int n = 4;
        Console.Write(sumFactDiv(n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of proper
// divisor of factorial of a number

// function to calculate factorial
function fact($n)
{
    if ($n == 0)
        return 1;
    return $n * fact($n - 1);
}

// function to calculate sum of divisor
function div($x)
{
    $ans = 0;
    for ($i = 1; $i<= $x; $i++)
        if ($x % $i == 0)
            $ans += $i;
    return $ans;
}

// Returns sum of divisors of n!
function sumFactDiv($n)
{
    return div(fact($n));
}

// Driver Code
$n = 4;
echo sumFactDiv($n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// JavaScript program to find
// sum of proper divisor of
// factorial of a number

// function to calculate factorial
function fact(n)
{
    if (n == 0)
        return 1;
    return n * fact(n - 1);
}

// function to calculate sum of divisor
function div(x)
{
    let ans = 0;
    for (let i = 1; i<= x; i++)
        if (x % i == 0)
            ans += i;
    return ans;
}

// Returns sum of divisors of n!
function sumFactDiv(n)
{
    return div(fact(n));
}

// Driver Code

    let n = 4;
    document.write(sumFactDiv(n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
60
```

一个**有效的解决方案**是基于[勒让德公式](https://www.geeksforgeeks.org/given-p-and-n-find-the-largest-x-such-that-px-divides-n-2/)。以下是步骤。

1.  查找所有小于或等于 n(输入数)的质数。对此我们可以使用[筛选算法](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)。设 n 为 6。所有小于 6 的素数都是{2，3，5}。
2.  对于每个质数，p 求它除 n 的最大幂！。为此，我们使用勒让德公式。
    *   2 除以 6 的最大幂！，exp1 = 4。
    *   3 除以 6 的最大幂！，exp2 = 2。
    *   5 除以 6 的最大幂！，exp3 = 1。
3.  结果基于[除数函数](http://mathworld.wolfram.com/DivisorFunction.html)。

## C++

```
// C++ program to find sum of divisors in n!
#include<bits/stdc++.h>
#include<math.h>
using namespace std;

// allPrimes[] stores all prime numbers less
// than or equal to n.
vector<int> allPrimes;

// Fills above vector allPrimes[] for a given n
void sieve(int n)
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // not a prime, else true.
    vector<bool> prime(n+1, true);

    // Loop to update prime[]
    for (int p = 2; p*p <= n; p++)
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
            allPrimes.push_back(p);
}

// Function to find all result of factorial number
int factorialDivisors(int n)
{
    sieve(n);  // create sieve

    // Initialize result
    int result = 1;

    // find exponents of all primes which divides n
    // and less than n
    for (int i = 0; i < allPrimes.size(); i++)
    {
        // Current divisor
        int p = allPrimes[i];

        // Find the highest power (stored in exp)'
        // of allPrimes[i] that divides n using
        // Legendre's formula.
        int exp = 0;
        while (p <= n)
        {
            exp = exp + (n/p);
            p = p*allPrimes[i];
        }

        // Using the divisor function to calculate
        // the sum
        result = result*(pow(allPrimes[i], exp+1)-1)/
                                    (allPrimes[i]-1);
    }

    // return total divisors
    return result;
}

// Driver program to run the cases
int main()
{
    cout << factorialDivisors(4);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of divisors in n!
import java.util.*;

class GFG{
// allPrimes[] stores all prime numbers less
// than or equal to n.
static ArrayList<Integer> allPrimes=new ArrayList<Integer>();

// Fills above vector allPrimes[] for a given n
static void sieve(int n)
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // not a prime, else true.
    boolean[] prime=new boolean[n+1];

    // Loop to update prime[]
    for (int p = 2; p*p <= n; p++)
    {
        // If prime[p] is not changed, then it
        // is a prime
        if (prime[p] == false)
        {
            // Update all multiples of p
            for (int i = p*2; i <= n; i += p)
                prime[i] = true;
        }
    }

    // Store primes in the vector allPrimes
    for (int p = 2; p <= n; p++)
        if (prime[p]==false)
            allPrimes.add(p);
}

// Function to find all result of factorial number
static int factorialDivisors(int n)
{
    sieve(n); // create sieve

    // Initialize result
    int result = 1;

    // find exponents of all primes which divides n
    // and less than n
    for (int i = 0; i < allPrimes.size(); i++)
    {
        // Current divisor
        int p = allPrimes.get(i);

        // Find the highest power (stored in exp)'
        // of allPrimes[i] that divides n using
        // Legendre's formula.
        int exp = 0;
        while (p <= n)
        {
            exp = exp + (n/p);
            p = p*allPrimes.get(i);
        }

        // Using the divisor function to calculate
        // the sum
        result = result*((int)Math.pow(allPrimes.get(i), exp+1)-1)/
                                    (allPrimes.get(i)-1);
    }

    // return total divisors
    return result;
}

// Driver program to run the cases
public static void main(String[] args)
{
    System.out.println(factorialDivisors(4));
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find sum of divisors in n!

# allPrimes[] stores all prime numbers
# less than or equal to n.
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
    while (p * p <= n):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, n + 1, p):
                prime[i] = False;
        p += 1;

    # Store primes in the vector allPrimes
    for p in range(2, n + 1):
        if (prime[p]):
            allPrimes.append(p);

# Function to find all result of factorial number
def factorialDivisors(n):

    sieve(n); # create sieve

    # Initialize result
    result = 1;

    # find exponents of all primes which
    # divides n and less than n
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

        # Using the divisor function to 
        # calculate the sum
        result = int(result * (pow(allPrimes[i], exp + 1) - 1) /
                                           (allPrimes[i] - 1));

    # return total divisors
    return result;

# Driver Code
print(factorialDivisors(4));

# This code is contributed by mits
```

## C#

```
// C# program to find sum of divisors in n!
using System;
using System.Collections;

class GFG{
// allPrimes[] stores all prime numbers less
// than or equal to n.
static ArrayList allPrimes=new ArrayList();

// Fills above vector allPrimes[] for a given n
static void sieve(int n)
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // not a prime, else true.
    bool[] prime=new bool[n+1];

    // Loop to update prime[]
    for (int p = 2; p*p <= n; p++)
    {
        // If prime[p] is not changed, then it
        // is a prime
        if (prime[p] == false)
        {
            // Update all multiples of p
            for (int i = p*2; i <= n; i += p)
                prime[i] = true;
        }
    }

    // Store primes in the vector allPrimes
    for (int p = 2; p <= n; p++)
        if (prime[p]==false)
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
            exp = exp + (n/p);
            p = p*(int)allPrimes[i];
        }

        // Using the divisor function to calculate
        // the sum
        result = result*((int)Math.Pow((int)allPrimes[i], exp+1)-1)/
                                    ((int)allPrimes[i]-1);
    }

    // return total divisors
    return result;
}

// Driver program to run the cases
static void Main()
{
    Console.WriteLine(factorialDivisors(4));
}
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of divisors in n!

// allPrimes[] stores all prime numbers less
// than or equal to n.
$allPrimes=array();

// Fills above vector allPrimes[] for a given n
function sieve($n)
{
    global $allPrimes;
    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // not a prime, else true.
    $prime=array_fill(0,$n+1,true);

    // Loop to update prime[]
    for ($p = 2; $p*$p <= $n; $p++)
    {
        // If prime[p] is not changed, then it
        // is a prime
        if ($prime[$p] == true)
        {
            // Update all multiples of p
            for ($i = $p*2; $i <= $n; $i += $p)
                $prime[$i] = false;
        }
    }

    // Store primes in the vector allPrimes
    for ($p = 2; $p <= $n; $p++)
        if ($prime[$p])
            array_push($allPrimes,$p);
}

// Function to find all result of factorial number
function factorialDivisors($n)
{
    global $allPrimes;
    sieve($n); // create sieve

    // Initialize result
    $result = 1;

    // find exponents of all primes which divides n
    // and less than n
    for ($i = 0; $i < count($allPrimes); $i++)
    {
        // Current divisor
        $p = $allPrimes[$i];

        // Find the highest power (stored in exp)'
        // of allPrimes[i] that divides n using
        // Legendre's formula.
        $exp = 0;
        while ($p <= $n)
        {
            $exp = $exp + (int)($n/$p);
            $p = $p*$allPrimes[$i];
        }

        // Using the divisor function to calculate
        // the sum
        $result = $result*(pow($allPrimes[$i], $exp+1)-1)/
                                    ($allPrimes[$i]-1);
    }

    // return total divisors
    return $result;
}

// Driver program to run the cases

    print(factorialDivisors(4));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of divisors in n!

// allPrimes[] stores all prime numbers less
// than or equal to n.
let allPrimes=[];

// Fills above vector allPrimes[] for a given n
function sieve(n)
{

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // not a prime, else true.
    let prime = new Array(n + 1);
    for(let i = 0; i < n + 1; i++)
        prime[i] = true;

    // Loop to update prime[]
    for(let p = 2; p * p <= n; p++)
    {

        // If prime[p] is not changed, then it
        // is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(let i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }

    // Store primes in the vector allPrimes
    for(let p = 2; p <= n; p++)
        if (prime[p])
            allPrimes.push(p);
}

// Function to find all result of
// factorial number
function factorialDivisors(    n)
{

    // Create sieve
    sieve(n);

    // Initialize result
    let result = 1;

    // Find exponents of all primes which
    // divides n and less than n
    for(let i = 0; i < allPrimes.length; i++)
    {

        // Current divisor
        let p = allPrimes[i];

        // Find the highest power (stored in exp)'
        // of allPrimes[i] that divides n using
        // Legendre's formula.
        let exp = 0;

        while (p <= n)
        {
            exp = exp + Math.floor(n/p);
            p = p*allPrimes[i];
        }

        // Using the divisor function to calculate
        // the sum
        result = Math.floor(result * (Math.pow(
                 allPrimes[i], exp + 1) - 1) /
                     (allPrimes[i] - 1));
    }

    // Return total divisors
    return result;
}

// Driver code
document.write(factorialDivisors(4));

// This code is contributed by rag2127

</script>
```

**输出:**

```
60
```

本文由**普拉莫德·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。