# 使用质因数分解的一个数的因子的和

> 原文:[https://www . geeksforgeeks . org/使用素数因子分解的数的因子之和/](https://www.geeksforgeeks.org/sum-of-factors-of-a-number-using-prime-factorization/)

给定一个数 n，任务是求给定数 n 的所有因子的和

**示例**:

```
Input : N = 12
Output : 28
All factors of 12 are: 1,2,3,4,6,12

Input : 60
Output : 168 
```

**逼近:**假设 N = 1100，思路是先求给定数 N 的素因式分解
因此，1100 的素因式分解= **2 <sup>2</sup> * 5 <sup>2</sup> * 11。**
所以，计算所有因素之和的公式可以给出为:

> **(2<sup>0</sup>+2<sup>1</sup>+2<sup>2</sup>)*(5<sup>0</sup>+5<sup>1</sup>+5<sup>2</sup>)*(11<sup>0</sup>+11<sup>1</sup>)**
> (截止因子分解的幂，即 **2 和 5 的幂为 2 【T20)
> =(1+2+2<sup>2</sup>)*(1+5+5<sup>2</sup>)*(1+11)
> = 7 * 31 * 12
> = 2604
> 所以，1100 的所有因子之和= 2604**

下面是上述方法的实现:

## C++

```
// C++ Program to find sum of all
// factors of a given number

#include <bits/stdc++.h>

using namespace std;

// Using SieveOfEratosthenes to find smallest prime
// factor of all the numbers.
// For example, if N is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
void sieveOfEratosthenes(int N, int s[])
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries in it as false.
    vector<bool> prime(N + 1, false);

    // Initializing smallest factor equal to 2
    // for all the even numbers
    for (int i = 2; i <= N; i += 2)
        s[i] = 2;

    // For odd numbers less then equal to n
    for (int i = 3; i <= N; i += 2) {
        if (prime[i] == false) {

            // s(i) for a prime is the number itself
            s[i] = i;

            // For all multiples of current prime number
            for (int j = i; j * i <= N; j += 2) {
                if (prime[i * j] == false) {
                    prime[i * j] = true;

                    // i is the smallest prime factor for
                    // number "i*j".
                    s[i * j] = i;
                }
            }
        }
    }
}

// Function to find sum of all prime factors
int findSum(int N)
{
    // Declaring array to store smallest prime
    // factor of i at i-th index
    int s[N + 1];

    int ans = 1;

    // Filling values in s[] using sieve
    sieveOfEratosthenes(N, s);

    int currFactor = s[N]; // Current prime factor of N
    int power = 1; // Power of current prime factor

    while (N > 1) {
        N /= s[N];

        // N is now N/s[N]. If new N als has smallest
        // prime factor as currFactor, increment power
        if (currFactor == s[N]) {
            power++;
            continue;
        }

        int sum = 0;

        for(int i=0; i<=power; i++)
            sum += pow(currFactor,i);

        ans *= sum;

        // Update current prime factor as s[N] and
        // initializing power of factor as 1.
        currFactor = s[N];
        power = 1;
    }

    return ans;
}

// Driver code
int main()
{
    int n = 12;

    cout << "Sum of the factors is : ";

    cout << findSum(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java Program to find sum of all
//factors of a given number
public class GFG {

    //Using SieveOfEratosthenes to find smallest prime
    //factor of all the numbers.
    //For example, if N is 10,
    //s[2] = s[4] = s[6] = s[10] = 2
    //s[3] = s[9] = 3
    //s[5] = 5
    //s[7] = 7
    static void sieveOfEratosthenes(int N, int s[])
    {
     // Create a boolean array "prime[0..n]" and
     // initialize all entries in it as false.
     boolean[] prime = new boolean[N + 1];

     for(int i = 0; i < N+1; i++)
         prime[i] = false;

     // Initializing smallest factor equal to 2
     // for all the even numbers
     for (int i = 2; i <= N; i += 2)
         s[i] = 2;

     // For odd numbers less then equal to n
     for (int i = 3; i <= N; i += 2) {
         if (prime[i] == false) {

             // s(i) for a prime is the number itself
             s[i] = i;

             // For all multiples of current prime number
             for (int j = i; j * i <= N; j += 2) {
                 if (prime[i * j] == false) {
                     prime[i * j] = true;

                     // i is the smallest prime factor for
                     // number "i*j".
                     s[i * j] = i;
                 }
             }
         }
     }
    }

    //Function to find sum of all prime factors
    static int findSum(int N)
    {
     // Declaring array to store smallest prime
     // factor of i at i-th index
     int[] s = new int[N + 1];

     int ans = 1;

     // Filling values in s[] using sieve
     sieveOfEratosthenes(N, s);

     int currFactor = s[N]; // Current prime factor of N
     int power = 1; // Power of current prime factor

     while (N > 1) {
         N /= s[N];

         // N is now N/s[N]. If new N als has smallest
         // prime factor as currFactor, increment power
         if (currFactor == s[N]) {
             power++;
             continue;
         }

         int sum = 0;

         for(int i=0; i<=power; i++)
             sum += Math.pow(currFactor,i);

         ans *= sum;

         // Update current prime factor as s[N] and
         // initializing power of factor as 1.
         currFactor = s[N];
         power = 1;
     }

     return ans;
    }

    //Driver code
    public static void main(String[] args) {

        int n = 12;

         System.out.print("Sum of the factors is : ");

         System.out.print(findSum(n));
    }
}
```

## 蟒蛇 3

```
# Python 3 Program to find
# sum of all factors of a
# given number

# Using SieveOfEratosthenes
# to find smallest prime
# factor of all the numbers.
# For example, if N is 10,
# s[2] = s[4] = s[6] = s[10] = 2
# s[3] = s[9] = 3
# s[5] = 5
# s[7] = 7
def sieveOfEratosthenes(N, s) :

    # Create a boolean list "prime[0..n]"
    # and initialize all entries in it
    # as false.
    prime = [False] * (N + 1)

    # Initializing smallest
    # factor equal to 2 for
    # all the even numbers
    for i in range(2, N + 1, 2) :
        s[i] = 2

    # For odd numbers less
    # then equal to n
    for i in range(3, N + 1, 2) :

        if prime[i] == False :

            # s[i] for a prime is
            # the number itself
            s[i] = i

            # For all multiples of
            # current prime number
            for j in range(i, (N + 1) // i, 2) :

                if prime[i * j] == False :
                    prime[i * j] = True

                    # i is the smallest
                    # prime factor for
                    # number "i*j".
                    s[i * j] = i

                #J += 2

# Function to find sum
# of all prime factors
def findSum(N) :

    # Declaring list to store
    # smallest prime factor of
    # i at i-th index
    s = [0] * (N + 1)
    ans = 1

    # Filling values in s[] using
    # sieve function calling
    sieveOfEratosthenes(N, s)

    # Current prime factor of N
    currFactor = s[N]

    # Power of current prime factor
    power = 1

    while N > 1 :
        N //= s[N]

        # N is now N//s[N]. If new N
        # also has smallest prime
        # factor as currFactor,
        # increment power
        if currFactor == s[N] :
            power += 1
            continue

        sum = 0

        for i in range(power + 1) :
            sum += pow(currFactor, i)

        ans *= sum

        # Update current prime factor
        # as s[N] and initializing
        # power of factor as 1.
        currFactor = s[N]
        power = 1

    return ans

# Driver Code
if __name__ == "__main__" :

    n = 12
    print("Sum of the factors is :", end = " ")
    print(findSum(n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# Program to find sum of all
// factors of a given number
using System;

class GFG
{

// Using SieveOfEratosthenes to find smallest
// prime factor of all the numbers.
// For example, if N is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
static void sieveOfEratosthenes(int N, int []s)
{

// Create a boolean array "prime[0..n]" and
// initialize all entries in it as false.
bool[] prime = new bool[N + 1];

for(int i = 0; i < N + 1; i++)
    prime[i] = false;

// Initializing smallest factor equal
// to 2 for all the even numbers
for (int i = 2; i <= N; i += 2)
    s[i] = 2;

// For odd numbers less then equal to n
for (int i = 3; i <= N; i += 2)
{
    if (prime[i] == false)
    {

        // s(i) for a prime is the
        // number itself
        s[i] = i;

        // For all multiples of current
        // prime number
        for (int j = i; j * i <= N; j += 2)
        {
            if (prime[i * j] == false)
            {
                prime[i * j] = true;

                // i is the smallest prime factor
                // for number "i*j".
                s[i * j] = i;
            }
        }
    }
}
}

// Function to find sum of all
// prime factors
static int findSum(int N)
{
// Declaring array to store smallest
// prime factor of i at i-th index
int[] s = new int[N + 1];

int ans = 1;

// Filling values in s[] using sieve
sieveOfEratosthenes(N, s);

int currFactor = s[N]; // Current prime factor of N
int power = 1; // Power of current prime factor

while (N > 1)
{
    N /= s[N];

    // N is now N/s[N]. If new N als has smallest
    // prime factor as currFactor, increment power
    if (currFactor == s[N])
    {
        power++;
        continue;
    }

    int sum = 0;

    for(int i = 0; i <= power; i++)
        sum += (int)Math.Pow(currFactor, i);

    ans *= sum;

    // Update current prime factor as s[N]
    // and initializing power of factor as 1.
    currFactor = s[N];
    power = 1;
}

return ans;
}

// Driver code
public static void Main()
{
    int n = 12;

    Console.Write("Sum of the factors is : ");

    Console.WriteLine(findSum(n));
}
}

// This code is contributed by Shashank
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find sum of all
// factors of a given number

// Using SieveOfEratosthenes to find smallest prime
// factor of all the numbers.
// For example, if N is 10,
// s[2] = s[4] = s[6] = s[10] = 2
// s[3] = s[9] = 3
// s[5] = 5
// s[7] = 7
function sieveOfEratosthenes($N, &$s)
{
    // Create a boolean array "prime[0..n]" and
    // initialize all entries in it as false.
    $prime=array_fill(0,$N + 1, false);

    // Initializing smallest factor equal to 2
    // for all the even numbers
    for ($i = 2; $i <= $N; $i += 2)
        $s[$i] = 2;

    // For odd numbers less then equal to n
    for ($i = 3; $i <= $N; $i += 2) {
        if ($prime[$i] == false) {

            // s(i) for a prime is the number itself
            $s[$i] = $i;

            // For all multiples of current prime number
            for ($j = $i; $j * $i <= $N; $j += 2) {
                if ($prime[$i * $j] == false) {
                    $prime[$i * $j] = true;

                    // i is the smallest prime factor for
                    // number "i*j".
                    $s[$i * $j] = $i;
                }
            }
        }
    }
}

// Function to find sum of all prime factors
function findSum($N)
{
    // Declaring array to store smallest prime
    // factor of i at i-th index
    $s=array_fill(0,$N + 1,0);

    $ans = 1;

    // Filling values in s[] using sieve
    sieveOfEratosthenes($N, $s);

    $currFactor = $s[$N]; // Current prime factor of N
    $power = 1; // Power of current prime factor

    while ($N > 1) {
        $N /= $s[$N];

        // N is now N/s[N]. If new N als has smallest
        // prime factor as currFactor, increment power
        if ($currFactor == $s[$N]) {
            $power++;
            continue;
        }
        $sum = 0;

        for($i=0; $i<=$power; $i++)
            $sum += (int)pow($currFactor,$i);

        $ans *= $sum;

        // Update current prime factor as s[N] and
        // initializing power of factor as 1.
        $currFactor = $s[$N];
        $power = 1;
    }

    return $ans;
}

// Driver code

    $n = 12;

    echo "Sum of the factors is : ";

    echo findSum($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
//Javascript Program to find sum of all
//factors of a given number

    //Using SieveOfEratosthenes to find smallest prime
    //factor of all the numbers.
    //For example, if N is 10,
    //s[2] = s[4] = s[6] = s[10] = 2
    //s[3] = s[9] = 3
    //s[5] = 5
    //s[7] = 7
    function sieveOfEratosthenes(N,s)
    {
        // Create a boolean array "prime[0..n]" and
         // initialize all entries in it as false.
         let prime = new Array(N + 1);

         for(let i = 0; i < N+1; i++)
            prime[i] = false;

         // Initializing smallest factor equal to 2
         // for all the even numbers
         for (let i = 2; i <= N; i += 2)
            s[i] = 2;

         // For odd numbers less then equal to n
         for (let i = 3; i <= N; i += 2) {
            if (prime[i] == false) {

                // s(i) for a prime is the number itself
                s[i] = i;

                 // For all multiples of current prime number
                 for (let j = i; j * i <= N; j += 2) {
                    if (prime[i * j] == false) {
                        prime[i * j] = true;

                         // i is the smallest prime factor for
                         // number "i*j".
                         s[i * j] = i;
                     }
                 }
             }
         }
    }

    //Function to find sum of all prime factors
    function findSum(N)
    {
        // Declaring array to store smallest prime
         // factor of i at i-th index
         let s = new Array(N + 1);

         let ans = 1;

         // Filling values in s[] using sieve
         sieveOfEratosthenes(N, s);

         let currFactor = s[N]; // Current prime factor of N
         let power = 1; // Power of current prime factor

         while (N > 1) {
            N = Math.floor(N/s[N]);

             // N is now N/s[N]. If new N als has smallest
             // prime factor as currFactor, increment power
             if (currFactor == s[N]) {
                 power++;
                 continue;
             }

             let sum = 0;

             for(let i=0; i<=power; i++)
                sum += Math.pow(currFactor,i);

             ans *= sum;

             // Update current prime factor as s[N] and
             // initializing power of factor as 1.
             currFactor = s[N];
             power = 1;
         }

         return ans;
    }

    //Driver code
    let n = 12;
    document.write("Sum of the factors is : ");
    document.write(findSum(n));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Sum of the factors is : 28
```