# 数组中所有复合数的乘积

> 原文:[https://www . geeksforgeeks . org/数组中所有组合数的乘积/](https://www.geeksforgeeks.org/product-of-all-the-composite-numbers-in-an-array/)

给定一个整数数组。任务是计算一个数组中所有复合数的乘积。
**注:** 1 既不是素数，也不是复合数。
**示例:**

```
Input: arr[] = {2, 3, 4, 5, 6, 7}
Output: 24
Composite numbers are 4 and 6\. 
So, product = 24

Input: arr[] = {11, 13, 17, 20, 19}
Output: 20
```

**天真方法:**一个简单的解决方案是遍历数组，对每个元素做素性测试。如果元素不是素数也不是 1，将其乘以运行乘积。
**时间复杂度–**O(Nsqrt(N))
**高效方法:**使用厄拉多塞筛生成一个布尔向量，该向量达到数组中最大元素的大小，可用于检查一个数是否为素数。另外，将 0 和 1 相加作为质数，这样它们就不会被算作复合数。现在遍历数组，使用生成的布尔向量找到那些复合元素的乘积。

## C++

```
// C++ program to find the product
// of all the composite numbers
// in an array
#include <bits/stdc++.h>
using namespace std;

// Function that returns the
// the product of all composite numbers
int compositeProduct(int arr[], int n)
{
    // Find maximum value in the array
    int max_val = *max_element(arr, arr + n);

    // Use sieve to find all prime numbers
    // less than or equal to max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    vector<bool> prime(max_val + 1, true);

    // Set 0 and 1 as primes as
    // they don't need to be
    // counted as composite numbers
    prime[0] = true;
    prime[1] = true;
    for (int p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Find the product of all
    // composite numbers in the arr[]
    int product = 1;
    for (int i = 0; i < n; i++)
        if (!prime[arr[i]]) {
            product *= arr[i];
        }

    return product;
}

// Driver code
int main()
{

    int arr[] = { 2, 3, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << compositeProduct(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the product
// of all the composite numbers
// in an array
import java.util.*;

class GFG {

    // Function that returns the
    // the product of all composite numbers
    static int compositeProduct(int arr[], int n)
    {
        // Find maximum value in the array
        int max_val = Arrays.stream(arr).max().getAsInt();

        // Use sieve to find all prime numbers
        // less than or equal to max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        boolean[] prime = new boolean[max_val + 1];
        Arrays.fill(prime, true);

        // Set 0 and 1 as primes as
        // they don't need to be
        // counted as composite numbers
        prime[0] = true;
        prime[1] = true;
        for (int p = 2; p * p <= max_val; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= max_val; i += p) {
                    prime[i] = false;
                }
            }
        }

        // Find the product of all
        // composite numbers in the arr[]
        int product = 1;
        for (int i = 0; i < n; i++) {
            if (!prime[arr[i]]) {
                product *= arr[i];
            }
        }

        return product;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 4, 5, 6, 7 };
        int n = arr.length;

        System.out.println(compositeProduct(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
'''
Python3 program to find product of
all the composite numberes in given array'''
import math as mt
'''
function to find the product of all composite
niumbers in the given array
'''
def compositeProduct(arr, n):

    # find the maximum value in the array
    max_val = max(arr)
    '''
    USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    THAN OR EQUAL TO max_val
    Create a boolean array "prime[0..n]". A
    value in prime[i] will finally be false
    if i is Not a prime, else true.
    '''
    prime =[True for i in range(max_val + 1)]

    '''
    Set 0 and 1 as primes as
    they don't need to be
    counted as composite numbers
    '''
    prime[0]= True
    prime[1]= True

    for p in range(2, mt.ceil(mt.sqrt(max_val))):
        # Remaining part of SIEVE
        '''
        if prime[p] is not changed, than it is prime
        '''
        if prime[p]:
            # update all multiples of p
            for i in range(p * 2, max_val + 1, p):
                prime[i]= False

    # find the product of all composite numbers in the arr[]
    product = 1

    for i in range(n):
        if prime[arr[i]]== False:
            product*= arr[i]

    return product

# Driver code

arr =[2, 3, 4, 5, 6, 7]

n = len(arr)

print(compositeProduct(arr, n))

# contributed by Mohit kumar 29

```

## C#

```
// C# program to find the product
// of all the composite numbers
// in an array
using System;
using System.Linq;
public class GFG {

    // Function that returns the
    // the product of all composite numbers
    static int compositeProduct(int[] arr, int n)
    {
        // Find maximum value in the array
        int max_val = arr.Max();

        // Use sieve to find all prime numbers
        // less than or equal to max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        bool[] prime = new bool[max_val + 1];
        for (int i = 0; i < max_val + 1; i++)
            prime[i] = true;

        // Set 0 and 1 as primes as
        // they don't need to be
        // counted as composite numbers
        prime[0] = true;
        prime[1] = true;
        for (int p = 2; p * p <= max_val; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= max_val; i += p) {
                    prime[i] = false;
                }
            }
        }

        // Find the product of all
        // composite numbers in the arr[]
        int product = 1;
        for (int i = 0; i < n; i++) {
            if (!prime[arr[i]]) {
                product *= arr[i];
            }
        }

        return product;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 2, 3, 4, 5, 6, 7 };
        int n = arr.Length;

        Console.WriteLine(compositeProduct(arr, n));
    }
}
/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the product
// of all the composite numbers
// in an array

// Function that returns the
// the product of all composite numbers
function compositeProduct($arr, $n)
{
    // Find maximum value in the array
    $max_val = max($arr);

    // Use sieve to find all prime numbers
    // less than or equal to max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    $prime = array_fill(0, $max_val + 1, true);

    // Set 0 and 1 as primes as
    // they don't need to be
    // counted as composite numbers
    $prime[0] = true;
    $prime[1] = true;
    for ($p = 2; $p * $p <= $max_val; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2;
                 $i <= $max_val; $i += $p)
                $prime[$i] = false;
        }
    }

    // Find the product of all
    // composite numbers in the arr[]
    $product = 1;
    for ($i = 0; $i < $n; $i++)
        if (!$prime[$arr[$i]])
        {
            $product *= $arr[$i];
        }

    return $product;
}

// Driver code
$arr = array( 2, 3, 4, 5, 6, 7 );
$n = count($arr);

echo compositeProduct($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find the product
// of all the composite numbers
// in an array

// Function that returns the
// the product of all composite numbers
function compositeProduct(arr, n)
{
    // Find maximum value in the array
    let max_val = arr.sort((A, B) => B - A)[0];

    // Use sieve to find all prime numbers
    // less than or equal to max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    let prime = new Array(max_val + 1).fill(true);

    // Set 0 and 1 as primes as
    // they don't need to be
    // counted as composite numbers
    prime[0] = true;
    prime[1] = true;
    for (let p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for (let i = p * 2;
                i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Find the product of all
    // composite numbers in the arr[]
    let product = 1;
    for (let i = 0; i < n; i++)
        if (!prime[arr[i]])
        {
            product *= arr[i];
        }

    return product;
}

// Driver code
let arr = new Array( 2, 3, 4, 5, 6, 7 );
let n = arr.length;

document.write(compositeProduct(arr, n));

// This code is contributed by gfgking
</script>
```

**Output:** 

```
24
```