# 计算一个数组中的素数

> 原文:[https://www . geesforgeks . org/count-数组中的素数数/](https://www.geeksforgeeks.org/count-number-of-primes-in-an-array/)

给定一个由 N 个正整数组成的数组 arr[]。任务是编写一个程序来计算给定数组中质数元素的数量。
**例** :

```
Input: arr[] = {1, 3, 4, 5, 7}
Output: 3
There are three primes, 3, 5 and 7

Input: arr[] = {1, 2, 3, 4, 5, 6, 7}
Output: 4
```

**天真方法**:一个简单的解决方法是遍历数组并保持[检查每个元素是否是素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)并同时保持素数元素的计数。
**高效方法**:使用厄拉多塞的[筛生成数组最大元素之前的所有素数，并将它们存储在散列中。现在遍历数组，使用哈希表找到那些质数元素的数量。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// CPP program to find count of
// primes in given array.
#include <bits/stdc++.h>
using namespace std;

// Function to find count of prime
int primeCount(int arr[], int n)
{
    // Find maximum value in the array
    int max_val = *max_element(arr, arr+n);

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    vector<bool> prime(max_val + 1, true);

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
    for (int p = 2; p * p <= max_val; p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    // Find all primes in arr[]
    int count = 0;
    for (int i = 0; i < n; i++)
        if (prime[arr[i]])
            count++;   

    return count;
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << primeCount(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;
import java.util.Vector;

// Java program to find count of
// primes in given array.
class GFG
{

    // Function to find count of prime
    static int primeCount(int arr[], int n)
    {
        // Find maximum value in the array
        //.*max_element(arr, arr+n);
        int max_val = Arrays.stream(arr).max().getAsInt();

        // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        // THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        Boolean[] prime = new Boolean[max_val + 1];
        for (int i = 0; i < max_val + 1; i++)
        {
            prime[i] = true;
        }

        // Remaining part of SIEVE
        prime[0] = false;
        prime[1] = false;
        for (int p = 2; p * p <= max_val; p++)
        {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == true)
            {

                // Update all multiples of p
                for (int i = p * 2; i <= max_val; i += p)
                {
                    prime[i] = false;
                }
            }
        }

        // Find all primes in arr[]
        int count = 0;
        for (int i = 0; i < n; i++)
        {
            if (prime[arr[i]])
            {
                count++;
            }
        }

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 3, 4, 5, 6, 7};
        int n = arr.length;
        System.out.println(primeCount(arr, n));
    }
}

// This code is contributed by
// PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 program to find count of
# primes in given array.
from math import sqrt

# Function to find count of prime
def primeCount(arr, n):

    # Find maximum value in the array
    max_val = arr[0];
    for i in range(len(arr)):
        if(arr[i] > max_val):
            max_val = arr[i]

    # USE SIEVE TO FIND ALL PRIME NUMBERS
    # LESS THAN OR EQUAL TO max_val
    # Create a boolean array "prime[0..n]".
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.
    prime =[ True for i in range(max_val + 1)]

    # Remaining part of SIEVE
    prime[0] = False
    prime[1] = False
    k = int(sqrt(max_val)) + 1
    for p in range(2, k, 1):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, max_val + 1, p):
                prime[i] = False

    # Find all primes in arr[]
    count = 0
    for i in range(0, n, 1):
        if (prime[arr[i]]):
            count += 1

    return count

# Driver code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5, 6, 7]
    n = len(arr)

    print(primeCount(arr, n))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to find count of
// primes in given array.
using System;
using System.Linq;

class GFG
{

    // Function to find count of prime
    static int primeCount(int []arr, int n)
    {

        // Find maximum value in the array
        //.*max_element(arr, arr+n);
        int max_val = arr.Max();

        // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        // THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        Boolean[] prime = new Boolean[max_val + 1];
        for (int i = 0; i < max_val + 1; i++)
        {
            prime[i] = true;
        }

        // Remaining part of SIEVE
        prime[0] = false;
        prime[1] = false;
        for (int p = 2; p * p <= max_val; p++)
        {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == true)
            {

                // Update all multiples of p
                for (int i = p * 2; i <= max_val; i += p)
                {
                    prime[i] = false;
                }
            }
        }

        // Find all primes in arr[]
        int count = 0;
        for (int i = 0; i < n; i++)
        {
            if (prime[arr[i]])
            {
                count++;
            }
        }
        return count;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {1, 2, 3, 4, 5, 6, 7};
        int n = arr.Length;
        Console.WriteLine(primeCount(arr, n));
    }
}

//This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find count
// of primes in given array.

// Function to find count of prime
function primeCount($arr, $n)
{
    // Find maximum value in the array
    $max_val = max($arr);

    // Use Sieve to find all Prime Numbers
    // less than or equal to max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    $prime = array_fill(0, $max_val + 1, true);

    // Remaining part of SIEVE
    $prime[0] = false;
    $prime[1] = false;
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

    // Find all primes in arr[]
    $count = 0;
    for ($i = 0; $i < $n; $i++)
        if ($prime[$arr[$i]])
            $count++;

    return $count;
}

// Driver code
$arr = array(1, 2, 3, 4, 5, 6, 7 );
$n = sizeof($arr);

echo primeCount($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript program to find count
// of primes in given array.

// Function to find count of prime
function primeCount(arr, n)
{
    // Find maximum value in the array
    let max_val = arr.sort((a, b) => b - a)[0];

    // Use Sieve to find all Prime Numbers
    // less than or equal to max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    let prime = new Array(max_val + 1).fill(true);

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;
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

    // Find all primes in arr[]
    let count = 0;
    for (let i = 0; i < n; i++)
        if (prime[arr[i]])
            count++;

    return count;
}

// Driver code
let arr = new Array(1, 2, 3, 4, 5, 6, 7 );
let n = arr.length;

document.write(primeCount(arr, n));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
4
```