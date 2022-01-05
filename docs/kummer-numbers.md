# 库姆默数字

> 原文:[https://www.geeksforgeeks.org/kummer-numbers/](https://www.geeksforgeeks.org/kummer-numbers/)

给定一个整数 **N** ，任务是打印[库姆编号](https://oeis.org/A001951)的第一个 **N** 术语。
**举例:**

> **输入:**N = 3
> T3】输出: 1，5，29
> 1 =-1+2
> 5 =-1+2 * 3
> 29 =-1+2 * 3 * 5
> T9】输入:N = 5
> T12】输出: 1，5，29，209，2309

一种**天真的方法**是逐一检查从 1 到 n 的所有数字是否是素数，如果是，则存储结果中的乘法，类似地存储素数的乘法结果，直到 n 和 add -1。
**高效的方法**是使用 Sundaram 的 screen 找到所有的素数直到 n，然后通过将它们全部相乘并加-1 来计算第 n 个 kummer 数。
以下是上述方法的实施:

## C++

```
// C++ program to find Kummer
// number upto n terms

#include <bits/stdc++.h>
using namespace std;
const int MAX = 1000000;

// vector to store all prime
// less than and equal to 10^6
vector<int> primes;

// Function for the Sieve of Sundaram.
// This function stores all
// prime numbers less than MAX in primes
void sieveSundaram()
{
    // In general Sieve of Sundaram,
    // produces primes smaller
    // than (2*x + 2) for a
    // number given number x. Since
    // we want primes smaller than MAX,
    // we reduce MAX to half
    // This array is used to separate
    // numbers of the form
    // i+j+2ij from others
    // where 1 <= i <= j
    bool marked[MAX / 2 + 1] = { 0 };

    // Main logic of Sundaram.
    // Mark all numbers which
    // do not generate prime number
    // by doing 2*i+1
    for (int i = 1; i <= (sqrt(MAX) - 1) / 2; i++)

        for (int j = (i * (i + 1)) << 1;
             j <= MAX / 2;
             j += 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push_back(2);

    // Print other primes.
    // Remaining primes are of the
    // form 2*i + 1 such that
    // marked[i] is false.
    for (int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.push_back(2 * i + 1);
}

// Function to calculate nth Kummer number
int calculateKummer(int n)
{
    // Multiply first n primes
    int result = 1;
    for (int i = 0; i < n; i++)
        result = result * primes[i];

    // return nth Kummer number
    return -1 + result;
}

// Driver code
int main()
{
    int n = 5;
    sieveSundaram();
    for (int i = 1; i <= n; i++)
        cout << calculateKummer(i) << ", ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Kummer
// number upto n terms
import java.util.*;
class GFG{
static int MAX = 1000000;

// vector to store all prime
// less than and equal to 10^6
static Vector<Integer> primes = new Vector<Integer>();

// Function for the Sieve of Sundaram.
// This function stores all
// prime numbers less than MAX in primes
static void sieveSundaram()
{
    // In general Sieve of Sundaram,
    // produces primes smaller
    // than (2*x + 2) for a
    // number given number x. Since
    // we want primes smaller than MAX,
    // we reduce MAX to half
    // This array is used to separate
    // numbers of the form
    // i+j+2ij from others
    // where 1 <= i <= j
    boolean marked[] = new boolean[MAX / 2 + 1];

    // Main logic of Sundaram.
    // Mark all numbers which
    // do not generate prime number
    // by doing 2*i+1
    for (int i = 1;
              i <= (Math.sqrt(MAX) - 1) / 2;
             i++)

        for (int j = (i * (i + 1)) << 1;
                 j <= MAX / 2;
                 j += 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.add(2);

    // Print other primes.
    // Remaining primes are of the
    // form 2*i + 1 such that
    // marked[i] is false.
    for (int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.add(2 * i + 1);
}

// Function to calculate nth Kummer number
static int calculateKummer(int n)
{
    // Multiply first n primes
    int result = 1;
    for (int i = 0; i < n; i++)
        result = result * primes.get(i);

    // return nth Kummer number
    return -1 + result;
}

// Driver code
public static void main(String[] args)
{
    int n = 5;
    sieveSundaram();
    for (int i = 1; i <= n; i++)
        System.out.print(calculateKummer(i) + ", ");
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to find Kummer
# number upto n terms
import math

MAX = 1000000

# list to store all prime
# less than and equal to 10^6
primes=[]

# Function for the Sieve of Sundaram.
# This function stores all
# prime numbers less than MAX in primes
def sieveSundaram():

    # In general Sieve of Sundaram,
    # produces primes smaller
    # than (2*x + 2) for a
    # number given number x. Since
    # we want primes smaller than MAX,
    # we reduce MAX to half
    # This list is used to separate
    # numbers of the form
    # i+j+2ij from others
    # where 1 <= i <= j
    marked = [ 0 ] * int(MAX / 2 + 1)

    # Main logic of Sundaram.
    # Mark all numbers which
    # do not generate prime number
    # by doing 2*i+1
    for i in range(1, int((math.sqrt(MAX) - 1) // 2) + 1):
        for j in range((i * (i + 1)) << 1,
                        MAX // 2 + 1, 2 * i + 1):
            marked[j] = True

    # Since 2 is a prime number
    primes.append(2)

    # Print other primes.
    # Remaining primes are of the
    # form 2*i + 1 such that
    # marked[i] is false.
    for i in range(1, MAX // 2 + 1 ):
        if (marked[i] == False):
            primes.append(2 * i + 1)

# Function to calculate nth Kummer number
def calculateKummer(n):

    # Multiply first n primes
    result = 1
    for i in range(n):
        result = result * primes[i]

    # return nth Kummer number
    return (-1 + result)

# Driver code

# Given N
N = 5
sieveSundaram()
for i in range(1, N + 1):
    print(calculateKummer(i), end = ", ")

# This code is contributed by Vishal Maurya
```

## C#

```
// C# program to find Kummer
// number upto n terms
using System;
using System.Collections.Generic;

class GFG{
static int MAX = 1000000;

// vector to store all prime
// less than and equal to 10^6
static List<int> primes = new List<int>();

// Function for the Sieve of Sundaram.
// This function stores all
// prime numbers less than MAX in primes
static void sieveSundaram()
{
    // In general Sieve of Sundaram,
    // produces primes smaller
    // than (2*x + 2) for a
    // number given number x. Since
    // we want primes smaller than MAX,
    // we reduce MAX to half
    // This array is used to separate
    // numbers of the form
    // i+j+2ij from others
    // where 1 <= i <= j
    bool []marked = new bool[MAX / 2 + 1];

    // Main logic of Sundaram.
    // Mark all numbers which
    // do not generate prime number
    // by doing 2*i+1
    for (int i = 1;
             i <= (Math.Sqrt(MAX) - 1) / 2;
             i++)

        for (int j = (i * (i + 1)) << 1;
                 j <= MAX / 2;
                 j += 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.Add(2);

    // Print other primes.
    // Remaining primes are of the
    // form 2*i + 1 such that
    // marked[i] is false.
    for (int i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.Add(2 * i + 1);
}

// Function to calculate nth Kummer number
static int calculateKummer(int n)
{
    // Multiply first n primes
    int result = 1;
    for (int i = 0; i < n; i++)
        result = result * primes[i];

    // return nth Kummer number
    return -1 + result;
}

// Driver code
public static void Main(String[] args)
{
    int n = 5;
    sieveSundaram();
    for (int i = 1; i <= n; i++)
        Console.Write(calculateKummer(i) + ", ");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find Kummer
// number upto n terms

// Function to count the number of
// ways to decode the given digit
// sequence
let MAX = 1000000;

// vector to store all prime
// less than and equal to 10^6
let primes = [];

// Function for the Sieve of Sundaram.
// This function stores all
// prime numbers less than MAX in primes
function sieveSundaram()
{
    // In general Sieve of Sundaram,
    // produces primes smaller
    // than (2*x + 2) for a
    // number given number x. Since
    // we want primes smaller than MAX,
    // we reduce MAX to half
    // This array is used to separate
    // numbers of the form
    // i+j+2ij from others
    // where 1 <= i <= j
    let marked = Array.from(
    {length: MAX / 2 + 1}, (_, i) => 0);

    // Main logic of Sundaram.
    // Mark all numbers which
    // do not generate prime number
    // by doing 2*i+1
    for (let i = 1;
              i <= (Math.sqrt(MAX) - 1) / 2;
             i++)

        for (let j = (i * (i + 1)) << 1;
                 j <= MAX / 2;
                 j += 2 * i + 1)
            marked[j] = true;

    // Since 2 is a prime number
    primes.push(2);

    // Prlet other primes.
    // Remaining primes are of the
    // form 2*i + 1 such that
    // marked[i] is false.
    for (let i = 1; i <= MAX / 2; i++)
        if (marked[i] == false)
            primes.push(2 * i + 1);
}

// Function to calculate nth Kummer number
function calculateKummer(n)
{
    // Multiply first n primes
    let result = 1;
    for (let i = 0; i < n; i++)
        result = result * primes[i];

    // return nth Kummer number
    return -1 + result;
}
// Driver Code

        let n = 5;
    sieveSundaram();
    for (let i = 1; i <= n; i++)
        document.write(calculateKummer(i) + ", ");

</script>
```

**Output:** 1, 5, 29, 209, 2309, 

**参考文献:**T2https://oeis.org/A057588