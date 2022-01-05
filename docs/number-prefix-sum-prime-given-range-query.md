# 给定范围查询的前缀和素数

> 原文:[https://www . geesforgeks . org/number-prefix-sum-prime-given-range-query/](https://www.geeksforgeeks.org/number-prefix-sum-prime-given-range-query/)

给定一个非负整数数组和范围查询 l，r，找到在给定范围内素数前缀和的个数。
**先决条件:** [前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) | [素性测试](https://www.geeksforgeeks.org/primality-test-set-2-fermet-method/)

**示例:**

```
Input : {2, 3, 4, 7, 9, 10}, 
        l = 1, r = 5;
Output : 3
Explanation : prefixSum[0] = arr[l] = 3
         prefixSum[1] = prefixSum[0] + arr[2] = 7, 
         prefixSum[2] = prefixSum[1] + arr[3] = 14, 
         prefixSum[3] = prefixSum[2] + arr[4] = 23, 
         prefixSum[4] = prefixSum[3] + arr[5] = 33,
There are three primes in prefix sum array in given
range. The primes are 3, 7 and 23.

Input : {5, 7, 8, 10, 13}, 
         l = 0, r = 4;
Output : 2
         prefixSum[0] = arr[l] = 5, 
         prefixSum[1] = prefixSum[0] + arr[1] = 12, 
         prefixSum[2] = prefixSum[1] + arr[2] = 20, 
         prefixSum[3] = prefixSum[2] + arr[3] = 30, 
         prefixSum[4] = prefixSum[3] + arr[4] = 43, 
There are two primes in prefix sum array in given
range. The primes are 5 and 43
```

**方法:**通过 l 到 r 运行一个循环，其中 l 和 r 是索引的范围，通过添加**前缀和数组**的前一个元素和数组的当前元素，填充前缀和数组，前缀和数组的大小将与数组的大小相同，然后，通过检查素数的**素数测试**检查每个阶段的前缀和是否是素数。如果前缀和是质数，则增加计数，否则不增加。

## C++

```
// C++ program to count the number of
// prefix sum which are prime or not
#include<bits/stdc++.h>
using namespace std;

// Primality test to check if prefix
// sum is prime or not
bool isPrime(int num)
{
    // Corner case
    if (num <= 1) return false;
    if (num <= 3) return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (num%2 == 0 || num%3 == 0)
        return false;

    for (int j = 5; j * j <= num; j = j + 6)
        if (num%j == 0 || num%(j+2) == 0)
        return false;

    return true;
}

// to calculate the prefix sum for
// the given range of query
int primesubArraySum(int arr[], int n, int l,
                     int r, int preSum[])
{
    int count = 0;   
    preSum[0] = arr[l];   
    if (isPrime(preSum[0]))
       count++;

    for (int i = l + 1, j = 1;
        i <= r && j < n; i++,j++)
    {
        preSum[j] = preSum[j - 1] + arr[i];

        // increase the count if the
        // prefix sum is prime
        if (isPrime(preSum[j]))
            count++;
    }

    return count;
}

//driver code
int main()
{
    int arr[] = {5, 7, 8, 10, 13};
    int n = sizeof(arr)/sizeof(arr[0]);
    int preSum[n];
    int l = 0, r = 4;

    cout << primesubArraySum(arr, n, l, r, preSum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of
// prefix sum which are prime or not
import java.util.*;
class GFG
{
    // Primality test to check if
    // prefix sum is prime or not
    public static boolean isPrime(int num)
    {
        // Corner cases
        if (num <= 1)
            return false;
        if (num <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (num % 2 == 0 || num % 3 == 0)
                return false;

        for (int j = 5; j * j <= num; j = j + 6)
            if (num % j == 0 || num % (j + 2) == 0)
                return false;

        return true;
    }

    // to calculate the prefix sum for
    // the given range of query
    public static int primesubArraySum(int arr[], int n,
                                       int l, int r,
                                       int preSum[])
    {
        int count = 0;

        preSum[0] = arr[l];

        if (isPrime(preSum[0]) == true)
            count++;

        for (int i = l+1,j = 1; i <= r && j < n; i++,j++)
        {
            preSum[j] = preSum[j-1] + arr[i];

            // increase the count if the prefix sum is prime
            if (isPrime(preSum[j]) == true)
                count++;
        }

        return count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = {5, 7, 8, 10, 13};
        int n = arr.length;
        int preSum[] = new int[n];
        int l = 0, r = 4;
        System.out.println(primesubArraySum(arr, n,
                           l, r, preSum));
    }
}
```

## 蟒蛇 3

```
# Python program to count the number
# of prefix sum which are prime or not
import numpy
import math

# Primality test to check if prefix
# sum is prime or not
def isPrime(num):

    # Corner case
    if (num <= 1):
        return False;
    if (num <= 3):
        return True;

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (num % 2 == 0 or num % 3 == 0):
        return False;

    for j in range(5, (int)(math.sqrt(num)) + 1, 6):
        if (num % j == 0 or num % (j + 2) == 0):
            return False;

        return True;

# to calculate the prefix sum for
# the given range of query
def primesubArraySum(arr, n, l, r, preSum):

    count = 0;
    preSum[0] = arr[l];

    if (isPrime(preSum[0])):
        count = count + 1;

    for i in range(l + 1, r):
        for j in range(1, n):
            preSum[j] = preSum[j - 1] + arr[i];

            # increase the count if the
            # prefix sum is prime
            if (isPrime(preSum[j])):
                count = count + 1;

    return count;

# Driver code
arr = [5, 7, 8, 10, 13];
n = len(arr);

#a = numpy.arange(5)
preSum = numpy.arange(n);
l = 0;
r = 4;
print(primesubArraySum(arr, n, l, r, preSum));

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# program to count the number of
// prefix sum which are prime or not
using System;

class GFG {

    // Primality test to check if
    // prefix sum is prime or not
    public static bool isPrime(int num)
    {

        // Corner cases
        if (num <= 1)
            return false;
        if (num <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (num % 2 == 0 || num % 3 == 0)
                return false;

        for (int j = 5; j * j <= num; j = j + 6)
            if (num % j == 0 || num % (j + 2) == 0)
                return false;

        return true;
    }

    // To calculate the prefix sum
    // for the given range of query
    public static int primesubArraySum(int []arr, int n,
                                       int l, int r,
                                       int []preSum)
    {
        int count = 0;

        preSum[0] = arr[l];

        if (isPrime(preSum[0]) == true)
            count++;

        for (int i = l+1,j = 1; i <= r &&
                          j < n; i++,j++)
        {
            preSum[j] = preSum[j-1] + arr[i];

            // increase the count if the
            // prefix sum is prime
            if (isPrime(preSum[j]) == true)
                count++;
        }

        return count;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = {5, 7, 8, 10, 13};
        int n = arr.Length;
        int []preSum = new int[n];
        int l = 0, r = 4;
        Console.Write(primesubArraySum(arr, n,
                      l, r, preSum));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// the number of prefix
// sum which are prime
// or not

// Primality test to check if
// prefix sum is prime or not
function isPrime($num)
{
    // Corner case
    if ($num <= 1) return false;
    if ($num <= 3) return true;

    // This is checked so
    // that we can skip
    // middle five numbers
    // in below loop
    if ($num % 2 == 0 ||
        $num % 3 == 0)
        return false;

    for ($j = 5; $j * $j <= $num;
                 $j = $j + 6)
        if ($num % $j == 0 ||
            $num % ($j + 2) == 0)
        return false;

    return true;
}

// To calculate the prefix
// sum for the given range
// of query
function primesubArraySum($arr, $n,    
                          $l,$r, $preSum)
{
    $count = 0;
    $preSum[0] = $arr[$l];
    if (isPrime($preSum[0]))
    $count++;

    for ($i = $l + 1, $j = 1;
         $i <= $r && $j < $n;
         $i++, $j++)
    {
        $preSum[$j] = $preSum[$j - 1] +
                              $arr[$i];

        // increase the count if 
        // the prefix sum is prime
        if (isPrime($preSum[$j]))
            $count++;
    }

    return $count;
}

// Driver code
$arr = array(5, 7, 8, 10, 13);
$n = sizeof($arr);
$preSum = array();
$l = 0; $r = 4;

echo primesubArraySum($arr, $n, $l,
                      $r, $preSum);

// This code is contributed by Ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to count the number of
// prefix sum which are prime or not

// Primality test to check if
// prefix sum is prime or not
function isPrime(num)
{

    // Corner cases
    if (num <= 1)
        return false;
    if (num <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (num % 2 == 0 || num % 3 == 0)
            return false;

    for(let j = 5; j * j <= num; j = j + 6)
        if (num % j == 0 || num % (j + 2) == 0)
            return false;

    return true;
}

// To calculate the prefix sum
// for the given range of query
function primesubArraySum(arr, n, l, r, preSum)
{
    let count = 0;

    preSum[0] = arr[l];

    if (isPrime(preSum[0]) == true)
        count++;

    for(let i = l + 1, j = 1;
            i <= r && j < n;
            i++, j++)
    {
        preSum[j] = preSum[j - 1] + arr[i];

        // Increase the count if the
        // prefix sum is prime
        if (isPrime(preSum[j]) == true)
            count++;
    }
    return count;
}

// Driver code
let arr = [ 5, 7, 8, 10, 13 ];
let n = arr.length;
let preSum = new Array(n);

preSum.fill(0);
let l = 0, r = 4;

document.write(primesubArraySum(
    arr, n, l, r, preSum));

// This code is contributed by decode2207

</script>
```

**Output:** 

```
2
```