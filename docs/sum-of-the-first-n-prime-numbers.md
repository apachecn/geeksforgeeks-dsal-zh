# 前 N 个素数之和

> 原文:[https://www . geeksforgeeks . org/第一个 n 素数之和/](https://www.geeksforgeeks.org/sum-of-the-first-n-prime-numbers/)

给定一个整数‘n’，任务是找出前‘n’个素数的和。

> 前几个质数是:2，3，5，7，11，13，17，19，23，…

**例:**

```
Input: N = 4
Output: 17
2, 3, 5, 7 are first 4 prime numbers so their sum is equal to 17

Input: N = 40
Output: 3087
```

**进场:**

*   创建一个筛子，它将帮助我们识别这个数字在 O(1)时间内是否是质数。
*   运行一个从 1 开始的循环，直到并且除非我们找到 n 个质数。
*   把所有质数加起来，忽略那些不是质数的。
*   然后，显示前 N 个素数之和。

以下是上述解决方案
的实现

## C++

```
// C++ implementation of above solution
#include <bits/stdc++.h>
using namespace std;
#define MAX 10000

// Create a boolean array "prime[0..n]" and initialize
// all entries it as true. A value in prime[i] will
// finally be false if i is Not a prime, else true.
bool prime[MAX + 1];
void SieveOfEratosthenes()
{
    memset(prime, true, sizeof(prime));

    prime[1] = false;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Set all multiples of p to non-prime
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// find the sum of 1st N prime numbers
int solve(int n)
{
    // count of prime numbers
    int count = 0, num = 1;

    // sum of prime numbers
    long long int sum = 0;

    while (count < n) {

        // if the number is prime add it
        if (prime[num]) {
            sum += num;

            // increase the count
            count++;
        }

        // get to next number
        num++;
    }
    return sum;
}

// Driver code
int main()
{
    // create the sieve
    SieveOfEratosthenes();

    int n = 4;

    // find the value of 1st n prime numbers
    cout << "Sum of 1st N prime numbers are :" << solve(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above solution
public class Improve {

    final static double MAX = 10000 ;
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    static boolean prime[] = new boolean [(int) (MAX + 1.0)] ;
    static void SieveOfEratosthenes()
    {

        for(int i = 0; i <= MAX; i++)
            prime[i] = true ;

        prime[1] = false;

        for (int p = 2; p * p <= MAX; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true) {

                // Set all multiples of p to non-prime
                for (int i = p * 2; i <= MAX; i += p)
                    prime[i] = false;
            }
        }
    }

    // find the sum of 1st N prime numbers
    static int solve(int n)
    {
        // count of prime numbers
        int count = 0, num = 1;

        // sum of prime numbers
        long sum = 0;

        while (count < n) {

            // if the number is prime add it
            if (prime[num]) {
                sum += num;

                // increase the count
                count++;
            }

            // get to next number
            num++;
        }
        return (int) sum;
    }
    // Driver code 
    public static void main(String args[])
    {
        // create the sieve
        SieveOfEratosthenes();

        int n = 4;

        // find the value of 1st n prime numbers
        System.out.println("Sum of 1st N prime numbers are :" + solve(n));

    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python3 implementation of
# above solution
MAX = 10000

# Create a boolean array "prime[0..n]"
# and initialize all entries it as true.
# A value in prime[i] will finally be
# false if i is Not a prime, else true.
prime = [True for i in range(MAX + 1)]
def SieveOfEratosthenes():

    prime[1] = False

    for p in range(2, MAX + 1):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Set all multiples of
            # p to non-prime
            i = p * 2
            while(i <= MAX):
                prime[i] = False
                i = i + p

# find the sum of 1st
# N prime numbers
def solve( n):

    # count of prime numbers
    count = 0
    num = 1

    # sum of prime numbers
    total = 0

    while (count < n):

        # if the number is prime add it
        if ( prime[num] ):
            total = total + num

            # increase the count
            count = count + 1

        # get to next number
        num = num + 1

    return total

# Driver code
# create the sieve
SieveOfEratosthenes()

n = 4

# find the value of 1st
# n prime numbers
print("Sum of 1st N prime " +
      "numbers are :", solve(n))

# This code is contributed by ash264
```

## C#

```
//C# implementation of above solution

using System;

public class GFG{

     static double MAX = 10000 ;
    // Create a boolean array "prime[0..n]" and initialize
    // all entries it as true. A value in prime[i] will
    // finally be false if i is Not a prime, else true.
    static bool []prime = new bool [(int)(MAX + 1.0)] ;
    static void SieveOfEratosthenes()
    {

        for(int i = 0; i <= MAX; i++)
            prime[i] = true ;

        prime[1] = false;

        for (int p = 2; p * p <= MAX; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true) {

                // Set all multiples of p to non-prime
                for (int i = p * 2; i <= MAX; i += p)
                    prime[i] = false;
            }
        }
    }

    // find the sum of 1st N prime numbers
    static int solve(int n)
    {
        // count of prime numbers
        int count = 0, num = 1;

        // sum of prime numbers
        long sum = 0;

        while (count < n) {

            // if the number is prime add it
            if (prime[num]) {
                sum += num;

                // increase the count
                count++;
            }

            // get to next number
            num++;
        }
        return (int) sum;
    }
    // Driver code
    static public void Main (){
        // create the sieve
        SieveOfEratosthenes();
        int n = 4;
        // find the value of 1st n prime numbers
        Console.WriteLine("Sum of 1st N prime numbers are :" + solve(n));

    }
// This Code is contributed by ajit.
}
```

## java 描述语言

```
<script>

// javascript implementation of above solution

var MAX = 10000 ;
// Create a boolean array "prime[0..n]" and initialize
// all entries it as true. A value in prime[i] will
// finally be false if i is Not a prime, else true.
var prime = Array.from({length: parseInt( (MAX + 1.0))}, (_, i) => false);
function SieveOfEratosthenes()
{

    for(i = 0; i <= MAX; i++)
        prime[i] = true ;

    prime[1] = false;

    for (p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Set all multiples of p to non-prime
            for (i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// find the sum of 1st N prime numbers
function solve(n)
{
    // count of prime numbers
    var count = 0, num = 1;

    // sum of prime numbers
    var sum = 0;

    while (count < n) {

        // if the number is prime add it
        if (prime[num]) {
            sum += num;

            // increase the count
            count++;
        }

        // get to next number
        num++;
    }
    return parseInt( sum);
}
// Driver code 
//create the sieve
SieveOfEratosthenes();

var n = 4;

// find the value of 1st n prime numbers
document.write("Sum of 1st N prime numbers are :" + solve(n));

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
Sum of 1st N prime numbers are :17
```

**注意(对于竞争性编程):**在包含大量查询的问题中，可以使用一个向量来存储 10^8 范围内的所有素数，这将占用额外的 O(N)空间。我们还可以使用前缀数组来存储 10^8.范围内前 n 个素数的和