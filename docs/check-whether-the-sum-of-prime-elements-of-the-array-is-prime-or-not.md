# 检查数组的素数元素之和是否为素数

> 原文:[https://www . geesforgeks . org/check-数组的素元素之和是否为素/](https://www.geeksforgeeks.org/check-whether-the-sum-of-prime-elements-of-the-array-is-prime-or-not/)

给定一个有 N 个元素的数组。任务是检查数组中素数元素的和是否是素数。
**例:**

```
Input: arr[] = {1, 2, 3}
Output: Yes
As there are two primes in the array i.e. 2 and 3\. 
So, the sum of prime is 2 + 3 = 5 and 5 is also prime. 

Input: arr[] = {2, 3, 2, 2}
Output: No
```

**方法:**首先使用[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)找到 10^5 的素数。然后迭代数组的所有元素。如果这个数是质数，那就把它加到和上。最后，检查总和是否为质数。如果灌注，则打印**是**否则**否**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#define ll long long int
#define MAX 100000
using namespace std;
bool prime[MAX];

// Sieve to find prime
void sieve()
{
    memset(prime, true, sizeof(prime));
    prime[0] = prime[1] = false;
    for (int i = 2; i < MAX; i++)
        if (prime[i])
            for (int j = 2 * i; j < MAX; j += i)
                prime[j] = false;

}

// Function to check if the sum of
// prime is prime or not
bool checkArray(int arr[], int n)
{
    // find sum of all prime number
    ll sum = 0;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
            sum += arr[i];

    // if sum is prime
    // then return yes
    if (prime[sum])
        return true;

    return false;
}

// Driver code
int main()
{
    // array of elements
    int arr[] = { 1, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    sieve();

    if (checkArray(arr, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG {

static int MAX =100000;

static boolean prime[] = new boolean[MAX];

// Sieve to find prime
static void sieve()
{
    for(int i=0;i<MAX;i++)
    {
        prime[i] =true;
    }
    prime[0] = prime[1] = false;
    for (int i = 2; i < MAX; i++)
        if (prime[i])
            for (int j = 2 * i; j < MAX; j += i)
                prime[j] = false;

}

// Function to check if the sum of
// prime is prime or not
static boolean checkArray(int arr[], int n)
{
    // find sum of all prime number
    int sum = 0;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
            sum += arr[i];

    // if sum is prime
    // then return yes
    if (prime[sum])
        return true;

    return false;
}

// Driver code

    public static void main (String[] args) {
    // array of elements
    int arr[] = { 1, 2, 3 };
    int n = arr.length;

    sieve();

    if (checkArray(arr, n))
        System.out.println("Yes");
    else
         System.out.println("No");

    }
}
// This code is contributed by shs..
```

## 蟒蛇 3

```
# Python3 implementation of above approach
from math import gcd, sqrt

MAX = 100000

prime = [True] * MAX

# Sieve to find prime
def sieve() :

    # 0 and 1 are not prime numbers
    prime[0] = False
    prime[1] = False

    for i in range(2, MAX) :

        if prime[i] :
            for j in range(2**i, MAX, i) :
                prime[j] = False

# Function to check if the sum of
# prime is prime or not
def checkArray(arr, n) :

    # find sum of all prime number
    sum = 0
    for i in range(n) :

        if prime[arr[i]] :
            sum += arr[i]

    # if sum is prime
    # then return yes
    if prime[sum] :
        return True

    return False

# Driver code
if __name__ == "__main__" :

    # list of elements
    arr = [1, 2, 3]
    n = len(arr)

    sieve()

    if checkArray(arr, n) :
        print("Yes")
    else :
        print("No")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
static int MAX = 100000;

static bool[] prime = new bool[MAX];

// Sieve to find prime
static void sieve()
{
    for(int i = 0; i < MAX; i++)
    {
        prime[i] = true;
    }
    prime[0] = prime[1] = false;
    for (int i = 2; i < MAX; i++)
        if (prime[i])
            for (int j = 2 * i;
                     j < MAX; j += i)
                prime[j] = false;
}

// Function to check if the sum of
// prime is prime or not
static bool checkArray(int[] arr, int n)
{
    // find sum of all prime number
    int sum = 0;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
            sum += arr[i];

    // if sum is prime
    // then return yes
    if (prime[sum])
        return true;

    return false;
}

// Driver code
public static void Main ()
{
    // array of elements
    int[] arr = new int[] { 1, 2, 3 };
    int n = arr.Length;

    sieve();

    if (checkArray(arr, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// above approach

// Sieve to find prime
function sieve()
{
    $MAX = 100000;
    $prime = array($MAX);
    for($i = 0; $i < $MAX; $i++)
    {
        $prime[$i] = true;
    }
    $prime[0] = $prime[1] = false;
    for ($i = 2; $i < $MAX; $i++)
        if ($prime[$i])
            for ($j = 2 * $i;
                 $j < $MAX; $j += $i)
                $prime[$j] = false;
}

// Function to check if the sum of
// prime is prime or not
function checkArray($arr, $n)
{
    $prime = array(100000);

    // find sum of all prime number
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        if ($prime[$arr[$i]])
            $sum += $arr[$i];

    // if sum is prime
    // then return yes
    if ($prime[$sum])
        return true;

    return false;
}

// Driver code
$arr= array(1, 2, 3);
$n = sizeof($arr);

sieve();

if (checkArray($arr, $n))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

// function check whether a number
// is prime or not
function isPrime(n)
{
    // Corner case
    if (n <= 1)
        return 0;

    // Check from 2 to n-1
    for (let i = 2; i < n; i++)
        if (n % i == 0)
            return 0;

    return 1;
}

var prime = new Array(5);

// Sieve to find prime
function sieve()
{
    for(i = 0; i <=5; i++)
    {
        prime[i] = isPrime(i);
    }
}

// Function to check if the sum of
// prime is prime or not
function checkArray(arr, n)
{

    // find sum of all prime number
    sum = 0;
    for (i = 0; i <= n; i++)
        if (prime[arr[i]])
            sum += arr[i];

    // if sum is prime
    // then return yes
    if (sum)
        return 1;

    return 0;
}

var arr= [1, 2, 3];
n = 3;

sieve();

if (checkArray(arr, n))
    document.write("Yes");
else
    document.write("No");

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(n * log(log n))*

***辅助空间:** O(MAX)*