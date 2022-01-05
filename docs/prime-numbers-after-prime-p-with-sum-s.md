# 和为 S 的素数 P 后的素数

> 原文:[https://www . geesforgeks . org/prime-numbers-after-prime-p-with-sum-s/](https://www.geeksforgeeks.org/prime-numbers-after-prime-p-with-sum-s/)

给定三个数的和 S，素数 P 和 N，求素数 P 之后的所有 N 个素数，使它们的和等于 S.
**例:**

```
Input :  N = 2, P = 7, S = 28 
Output : 11 17
Explanation : 11 and 17 are primes after
prime 7 and (11 + 17 = 28) 

Input :  N = 3, P = 2, S = 23 
Output : 3 7 13
         5 7 11
Explanation : 3, 5, 7, 11 and 13 are primes 
after prime 2\. And (3 + 7 + 13 = 5 + 7 + 11 
= 23) 

Input :  N = 4, P = 3, S = 54
Output : 5 7 11 31 
         5 7 13 29 
         5 7 19 23 
         5 13 17 19 
         7 11 13 23 
         7 11 17 19 
Explanation : All are prime numbers and 
their sum is 54
```

**方法:**使用的方法是产生所有小于 S 且大于 P 的素数，然后回溯寻找是否存在这样的 N 个素数，它们的和等于 S。
例如，S = 10，N = 2，P = 2

![](img/066127d1e4d23ded827463482b533d2c.png)

## C++

```
// CPP Program to print all N primes after
// prime P whose sum equals S
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;

// vector to store prime and N primes
// whose sum equals given S
vector<int> set;
vector<int> prime;

// function to check prime number
bool isPrime(int x)
{
    // square root of x
    int sqroot = sqrt(x);
    bool flag = true;

    // since 1 is not prime number
    if (x == 1)
        return false;

    // if any factor is found return false
    for (int i = 2; i <= sqroot; i++)
        if (x % i == 0)
            return false;

    // no factor found
    return true;
}

// function to display N primes whose sum equals S
void display()
{
    int length = set.size();
    for (int i = 0; i < length; i++)
        cout << set[i] << " ";
    cout << "\n";
}

// function to evaluate all possible N primes
// whose sum equals S
void primeSum(int total, int N, int S, int index)
{
    // if total equals S And
    // total is reached using N primes
    if (total == S && set.size() == N)
    {
        // display the N primes
        display();
        return;
    }

    // if total is greater than S
    // or if index has reached last element
    if (total > S || index == prime.size())
        return;

    // add prime[index] to set vector
    set.push_back(prime[index]);

    // include the (index)th prime to total
    primeSum(total+prime[index], N, S, index+1);

    // remove element from set vector
    set.pop_back();

    // exclude (index)th prime
    primeSum(total, N, S, index+1);
}

// function to generate all primes
void allPrime(int N, int S, int P)
{
    // all primes less than S itself
    for (int i = P+1; i <=S ; i++)
    {
        // if i is prime add it to prime vector
        if (isPrime(i))
            prime.push_back(i);
    }

    // if primes are less than N
    if (prime.size() < N)
        return;
    primeSum(0, N, S, 0);
}

// Driver Code
int main()
{
    int S = 54, N = 2, P = 3;
    allPrime(N, S, P);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to print
// all N primes after prime
// P whose sum equals S
import java.io.*;
import java.util.*;

class GFG
{
    // vector to store prime
    // and N primes whose sum
    // equals given S
    static ArrayList<Integer> set =
                     new ArrayList<Integer>();
    static ArrayList<Integer> prime =
                     new ArrayList<Integer>();

    // function to check
    // prime number
    static boolean isPrime(int x)
    {
        // square root of x
        int sqroot = (int)Math.sqrt(x);

        // since 1 is not
        // prime number
        if (x == 1)
            return false;

        // if any factor is
        // found return false
        for (int i = 2;
                 i <= sqroot; i++)
            if (x % i == 0)
                return false;

        // no factor found
        return true;
    }

    // function to display N
    // primes whose sum equals S
    static void display()
    {
        int length = set.size();
        for (int i = 0;
                 i < length; i++)
            System.out.print(
                   set.get(i) + " ");
        System.out.println();
    }

    // function to evaluate
    // all possible N primes
    // whose sum equals S
    static void primeSum(int total, int N,
                         int S, int index)
    {
        // if total equals S
        // And total is reached
        // using N primes
        if (total == S &&
            set.size() == N)
        {
            // display the N primes
            display();
            return;
        }

        // if total is greater
        // than S or if index
        // has reached last
        // element
        // or if set size reached to maximum or greater than maximum
        if (total > S ||
            index == prime.size() || set.size() >= N)
            return;

        // add prime.get(index)
        // to set vector
        set.add(prime.get(index));

        // include the (index)th
        // prime to total
        primeSum(total + prime.get(index),
                         N, S, index + 1);

        // remove element
        // from set vector
        set.remove(set.size() - 1);

        // exclude (index)th prime
        primeSum(total, N,
                 S, index + 1);
    }

    // function to generate
    // all primes
    static void allPrime(int N,
                         int S, int P)
    {
        // all primes less
        // than S itself
        for (int i = P + 1;
                 i <= S ; i++)
        {
            // if i is prime add
            // it to prime vector
            if (isPrime(i))
                prime.add(i);
        }

        // if primes are
        // less than N
        if (prime.size() < N)
            return;
        primeSum(0, N, S, 0);
    }

    // Driver Code
    public static void main(String args[])
    {
        int S = 54, N = 2, P = 3;
        allPrime(N, S, P);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python Program to print
# all N primes after prime
# P whose sum equals S
import math

# vector to store prime
# and N primes whose
# sum equals given S
set = []
prime = []

# function to
# check prime number
def isPrime(x) :

    # square root of x
    sqroot = int(math.sqrt(x))
    flag = True

    # since 1 is not
    # prime number
    if (x == 1) :
        return False

    # if any factor is
    # found return false
    for i in range(2, sqroot + 1) :
        if (x % i == 0) :
            return False

    # no factor found
    return True

# function to display N
# primes whose sum equals S
def display() :

    global set, prime
    length = len(set)
    for i in range(0, length) :
        print (set[i], end = " ")
    print ()

# function to evaluate
# all possible N primes
# whose sum equals S
def primeSum(total, N,
             S, index) :

    global set, prime

    # if total equals S
    # And total is reached
    # using N primes
    if (total == S and
         len(set) == N) :

        # display the N primes
        display()
        return

    # if total is greater
    # than S or if index
    # has reached last element
    if (total > S or
        index == len(prime)) :
        return

    # add prime[index]
    # to set vector
    set.append(prime[index])

    # include the (index)th
    # prime to total
    primeSum(total + prime[index],
                  N, S, index + 1)

    # remove element
    # from set vector
    set.pop()

    # exclude (index)th prime
    primeSum(total, N,
             S, index + 1)

# function to generate
# all primes
def allPrime(N, S, P) :

    global set, prime

    # all primes less
    # than S itself
    for i in range(P + 1,
                   S + 1) :

        # if i is prime add
        # it to prime vector
        if (isPrime(i)) :
            prime.append(i)

    # if primes are
    # less than N
    if (len(prime) < N) :
        return
    primeSum(0, N, S, 0)

# Driver Code
S = 54
N = 2
P = 3
allPrime(N, S, P)

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# Program to print all
// N primes after prime P
// whose sum equals S
using System;
using System.Collections.Generic;

class GFG
{
    // vector to store prime
    // and N primes whose sum
    // equals given S
    static List<int> set = new List<int>();
    static List<int> prime = new List<int>();

    // function to check prime number
    static bool isPrime(int x)
    {
        // square root of x
        int sqroot = (int)Math.Sqrt(x);

        // since 1 is not prime number
        if (x == 1)
            return false;

        // if any factor is
        // found return false
        for (int i = 2; i <= sqroot; i++)
            if (x % i == 0)
                return false;

        // no factor found
        return true;
    }

    // function to display N
    // primes whose sum equals S
    static void display()
    {
        int length = set.Count;
        for (int i = 0; i < length; i++)
            Console.Write(set[i] + " ");
        Console.WriteLine();
    }

    // function to evaluate
    // all possible N primes
    // whose sum equals S
    static void primeSum(int total, int N,
                         int S, int index)
    {
        // if total equals S And
        // total is reached using N primes
        if (total == S && set.Count == N)
        {
            // display the N primes
            display();
            return;
        }

        // if total is greater than
        // S or if index has reached
        // last element
        if (total > S || index == prime.Count)
            return;

        // add prime[index]
        // to set vector
        set.Add(prime[index]);

        // include the (index)th
        // prime to total
        primeSum(total + prime[index],
                         N, S, index + 1);

        // remove element
        // from set vector
        set.RemoveAt(set.Count - 1);

        // exclude (index)th prime
        primeSum(total, N, S, index + 1);
    }

    // function to generate
    // all primes
    static void allPrime(int N,
                         int S, int P)
    {
        // all primes less than S itself
        for (int i = P + 1; i <=S ; i++)
        {
            // if i is prime add
            // it to prime vector
            if (isPrime(i))
                prime.Add(i);
        }

        // if primes are
        // less than N
        if (prime.Count < N)
            return;
        primeSum(0, N, S, 0);
    }

    // Driver Code
    static void Main()
    {
        int S = 54, N = 2, P = 3;
        allPrime(N, S, P);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to print all
// N primes after prime P
// whose sum equals S

// vector to store prime
// and N primes whose
// sum equals given S
$set = array();
$prime = array();

// function to
// check prime number
function isPrime($x)
{
    // square root of x
    $sqroot = sqrt($x);
    $flag = true;

    // since 1 is not
    // prime number
    if ($x == 1)
        return false;

    // if any factor is
    // found return false
    for ($i = 2; $i <= $sqroot; $i++)
        if ($x % $i == 0)
            return false;

    // no factor found
    return true;
}

// function to display N
// primes whose sum equals S
function display()
{
    global $set, $prime;
    $length = count($set);
    for ($i = 0; $i < $length; $i++)
        echo ($set[$i] . " ");
    echo ("\n");
}

// function to evaluate
// all possible N primes
// whose sum equals S
function primeSum($total, $N,
                  $S, $index)
{
    global $set, $prime;

    // if total equals S
    // And total is reached
    // using N primes
    if ($total == $S &&
        count($set) == $N)
    {
        // display the N primes
        display();
        return;
    }

    // if total is greater
    // than S or if index
    // has reached last element
    if ($total > $S ||
        $index == count($prime))
        return;

    // add prime[index]
    // to set vector
    array_push($set,
               $prime[$index]);

    // include the (index)th
    // prime to total
    primeSum($total + $prime[$index],
             $N, $S, $index + 1);

    // remove element
    // from set vector
    array_pop($set);

    // exclude (index)th prime
    primeSum($total, $N, $S,
             $index + 1);
}

// function to generate
// all primes
function allPrime($N, $S, $P)
{
    global $set, $prime;

    // all primes less
    // than S itself
    for ($i = $P + 1;
         $i <= $S ; $i++)
    {
        // if i is prime add
        // it to prime vector
        if (isPrime($i))
            array_push($prime, $i);
    }

    // if primes are
    // less than N
    if (count($prime) < $N)
        return;
    primeSum(0, $N, $S, 0);
}

// Driver Code
$S = 54; $N = 2; $P = 3;
allPrime($N, $S, $P);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript Program to print all N primes after
// prime P whose sum equals S

// vector to store prime and N primes
// whose sum equals given S
var set = [];
var prime = [];

// function to check prime number
function isPrime(x)
{
    // square root of x
    var sqroot = Math.sqrt(x);
    var flag = true;

    // since 1 is not prime number
    if (x == 1)
        return false;

    // if any factor is found return false
    for (var i = 2; i <= sqroot; i++)
        if (x % i == 0)
            return false;

    // no factor found
    return true;
}

// function to display N primes whose sum equals S
function display()
{
    var length = set.length;
    for (var i = 0; i < length; i++)
        document.write( set[i] + " ");
    document.write( "<br>");
}

// function to evaluate all possible N primes
// whose sum equals S
function primeSum(total, N, S, index)
{
    // if total equals S And
    // total is reached using N primes
    if (total == S && set.length == N)
    {
        // display the N primes
        display();
        return;
    }

    // if total is greater than S
    // or if index has reached last element
    if (total > S || index == prime.length)
        return;

    // add prime[index] to set vector
    set.push(prime[index]);

    // include the (index)th prime to total
    primeSum(total+prime[index], N, S, index+1);

    // remove element from set vector
    set.pop();

    // exclude (index)th prime
    primeSum(total, N, S, index+1);
}

// function to generate all primes
function allPrime(N, S, P)
{
    // all primes less than S itself
    for (var i = P+1; i <=S ; i++)
    {
        // if i is prime add it to prime vector
        if (isPrime(i))
            prime.push(i);
    }

    // if primes are less than N
    if (prime.length < N)
        return;
    primeSum(0, N, S, 0);
}

// Driver Code
var S = 54, N = 2, P = 3;
allPrime(N, S, P);

</script>
```

**Output:** 

```
7 47 
11 43 
13 41 
17 37 
23 31
```

**优化:**
上述解决方案可以通过使用厄拉多塞
的[筛预先计算所有需要的素数来优化](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)