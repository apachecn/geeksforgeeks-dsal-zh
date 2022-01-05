# 用数组中数字的质数和打印质数

> 原文:[https://www . geesforgeks . org/print-质数-带质数和的数组/](https://www.geeksforgeeks.org/print-prime-numbers-with-prime-sum-of-digits-in-an-array/)

给定一个数组 **arr[]** ，任务是打印数组中的加法素数。
**加性素数:**这样的素数，它们的位数之和也是素数，如 **2、3、7、11、23** 是加性素数但不是 **13、19、31** 等。
**举例:**

```
Input: arr[] = {2, 4, 6, 11, 12, 18, 7}
Output: 2, 11, 7 

Input: arr[] = {2, 3, 19, 13, 25, 7}
Output: 2, 3, 7
```

一种简单的方法是遍历所有的数组元素。对于每个元素，检查它是否是加法素数。
当数组很小或数组值很大时，上述方法可以。对于数值相对较小的大型数组，我们使用**筛选**来存储最大数组元素的素数。然后检查当前元素是否是质数。如果是，那么检查它的数字之和是否也是质数。如果是，则打印该号码。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to store the primes
void sieve(int maxEle, int prime[])
{
    prime[0] = prime[1] = 1;

    for (int i = 2; i * i <= maxEle; i++) {
        if (!prime[i]) {
            for (int j = 2 * i; j <= maxEle; j += i)
                prime[j] = 1;
        }
    }
}

// Function to return the sum of digits
int digitSum(int n)
{
    int sum = 0;
    while (n) {
        sum += n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to print additive primes
void printAdditivePrime(int arr[], int n)
{

    int maxEle = *max_element(arr, arr + n);

    int prime[maxEle + 1];
    memset(prime, 0, sizeof(prime));
    sieve(maxEle, prime);

    for (int i = 0; i < n; i++) {

        // If the number is prime
        if (prime[arr[i]] == 0) {
            int sum = digitSum(arr[i]);

            // Check if it's digit sum is prime
            if (prime[sum] == 0)
                cout << arr[i] << " ";
        }
    }
}

// Driver code
int main()
{

    int a[] = { 2, 4, 6, 11, 12, 18, 7 };
    int n = sizeof(a) / sizeof(a[0]);

    printAdditivePrime(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;

class GFG
{

// Function to store the primes
static void sieve(int maxEle, int prime[])
{
    prime[0] = prime[1] = 1;

    for (int i = 2; i * i <= maxEle; i++)
    {
        if (prime[i]==0)
        {
            for (int j = 2 * i; j <= maxEle; j += i)
                prime[j] = 1;
        }
    }
}

// Function to return the sum of digits
static int digitSum(int n)
{
    int sum = 0;
    while (n > 0)
    {
        sum += n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to print additive primes
static void printAdditivePrime(int arr[], int n)
{

    int maxEle = Arrays.stream(arr).max().getAsInt();

    int prime[] = new int[maxEle + 1];
    sieve(maxEle, prime);

    for (int i = 0; i < n; i++)
    {

        // If the number is prime
        if (prime[arr[i]] == 0)
        {
            int sum = digitSum(arr[i]);

            // Check if it's digit sum is prime
            if (prime[sum] == 0)
                System.out.print(arr[i]+" ");
        }
    }
}

// Driver code
public static void main(String[] args)
{

    int a[] = { 2, 4, 6, 11, 12, 18, 7 };
    int n =a.length;
    printAdditivePrime(a, n);
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# from math lib import sqrt
from math import sqrt

# Function to store the primes
def sieve(maxEle, prime) :

    prime[0], prime[1] = 1 , 1

    for i in range(2, int(sqrt(maxEle)) + 1) :
        if (not prime[i]) :
            for j in range(2 * i , maxEle + 1, i) :
                prime[j] = 1

# Function to return the sum of digits
def digitSum(n) :
    sum = 0
    while (n) :

        sum += n % 10
        n = n // 10
    return sum

# Function to print additive primes
def printAdditivePrime(arr, n):
    maxEle = max(arr)
    prime = [0] * (maxEle + 1)
    sieve(maxEle, prime)
    for i in range(n) :

        # If the number is prime
        if (prime[arr[i]] == 0):
            sum = digitSum(arr[i])

            # Check if it's digit sum is prime
            if (prime[sum] == 0) :
                print(arr[i], end = " ")

# Driver code
if __name__ == "__main__" :
    a = [ 2, 4, 6, 11, 12, 18, 7 ]
    n = len(a)
    printAdditivePrime(a, n)

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach
using System.Linq;
using System;

class GFG
{

// Function to store the primes
static void sieve(int maxEle, int[] prime)
{
    prime[0] = prime[1] = 1;

    for (int i = 2; i * i <= maxEle; i++)
    {
        if (prime[i] == 0)
        {
            for (int j = 2 * i; j <= maxEle; j += i)
                prime[j] = 1;
        }
    }
}

// Function to return the sum of digits
static int digitSum(int n)
{
    int sum = 0;
    while (n > 0)
    {
        sum += n % 10;
        n = n / 10;
    }
    return sum;
}

// Function to print additive primes
static void printAdditivePrime(int []arr, int n)
{

    int maxEle = arr.Max();

    int[] prime = new int[maxEle + 1];
    sieve(maxEle, prime);

    for (int i = 0; i < n; i++)
    {

        // If the number is prime
        if (prime[arr[i]] == 0)
        {
            int sum = digitSum(arr[i]);

            // Check if it's digit sum is prime
            if (prime[sum] == 0)
                Console.Write(arr[i] + " ");
        }
    }
}

// Driver code
static void Main()
{
    int[] a = { 2, 4, 6, 11, 12, 18, 7 };
    int n = a.Length;
    printAdditivePrime(a, n);
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to store the primes
function sieve($maxEle, &$prime)
{
    $prime[0] = $prime[1] = 1;

    for ($i = 2; $i * $i <= $maxEle; $i++)
    {
        if (!$prime[$i])
        {
            for ($j = 2 * $i;
                 $j <= $maxEle; $j += $i)
                $prime[$j] = 1;
        }
    }
}

// Function to return the sum of digits
function digitSum($n)
{
    $sum = 0;
    while ($n)
    {
        $sum += $n % 10;
        $n = $n / 10;
    }
    return $sum;
}

// Function to print additive primes
function printAdditivePrime($arr, $n)
{

    $maxEle = max($arr);

    $prime = array_fill(0, $maxEle + 1, 0);
    sieve($maxEle, $prime);

    for ($i = 0; $i < $n; $i++)
    {

        // If the number is prime
        if ($prime[$arr[$i]] == 0)
        {
            $sum = digitSum($arr[$i]);

            // Check if it's digit sum is prime
            if ($prime[$sum] == 0)
                print($arr[$i] . " ");
        }
    }
}

// Driver code
$a = array(2, 4, 6, 11, 12, 18, 7);
$n = count($a);

printAdditivePrime($a, $n);

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to store the primes
function sieve(maxEle, prime)
{
    prime[0] = prime[1] = 1;

    for (var i = 2; i * i <= maxEle; i++) {
        if (!prime[i]) {
            for (var j = 2 * i; j <= maxEle; j += i)
                prime[j] = 1;
        }
    }
}

// Function to return the sum of digits
function digitSum(n)
{
    var sum = 0;
    while (n) {
        sum += n % 10;
        n = parseInt(n / 10);
    }
    return sum;
}

// Function to print additive primes
function printAdditivePrime(arr, n)
{

    var maxEle = arr.reduce((a,b)=> Math.max(a,b));

    var prime = Array(maxEle + 1).fill(0);
    sieve(maxEle, prime);

    for (var i = 0; i < n; i++) {

        // If the number is prime
        if (prime[arr[i]] == 0) {
            var sum = digitSum(arr[i]);

            // Check if it's digit sum is prime
            if (prime[sum] == 0)
                document.write( arr[i] + " ");
        }
    }
}

// Driver code
var a = [ 2, 4, 6, 11, 12, 18, 7 ];
var n = a.length;
printAdditivePrime(a, n);

</script>
```

**Output:** 

```
2 11 7
```