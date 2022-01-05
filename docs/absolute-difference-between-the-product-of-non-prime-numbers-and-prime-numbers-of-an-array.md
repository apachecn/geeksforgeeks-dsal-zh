# 一个数组的非素数和素数之积的绝对差

> 原文:[https://www . geeksforgeeks . org/非质数乘积与数组质数的绝对差/](https://www.geeksforgeeks.org/absolute-difference-between-the-product-of-non-prime-numbers-and-prime-numbers-of-an-array/)

给定一组正数，任务是计算非素数和素数乘积之间的绝对差。
**注:** 1 既不是素数也不是非素数。
T4【示例】T5:

```
Input : arr[] = {1, 3, 5, 10, 15, 7}
Output : 45
Explanation : Product of non-primes = 150
              Product of primes = 105

Input : arr[] = {3, 4, 6, 7} 
Output : 3
```

**天真方法:**一个简单的解决方案是遍历数组，并不断检查每个元素是否是质数。如果数是质数，那么乘以 P2 积，它代表质数的乘积，否则检查它是否不是 1，然后乘以非质数的乘积，比如说 P1。遍历整个数组后，取两者的绝对差值(P1-P2)。
**时间复杂度:** O(N*sqrt(N))
**高效方法:**使用厄拉多塞筛生成数组最大元素之前的所有素数，并将其存储在哈希中。现在，遍历数组并检查该数字是否出现在哈希映射中。然后，将这些数字乘以 P2 乘积，检查它是否不是 1，然后乘以 P1 乘积。遍历整个数组后，显示两者之间的绝对差异。
以下是上述方法的实施:

## C++

```
// C++ program to find the Absolute Difference
// between the Product of Non-Prime numbers
// and Prime numbers of an Array

#include <bits/stdc++.h>
using namespace std;

// Function to find the difference between
// the product of non-primes and the
// product of primes of an array.
int calculateDifference(int arr[], int n)
{
    // Find maximum value in the array
    int max_val = *max_element(arr, arr + n);

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

    // Store the product of primes in P1 and
    // the product of non primes in P2
    int P1 = 1, P2 = 1;
    for (int i = 0; i < n; i++) {

        if (prime[arr[i]]) {

            // the number is prime
            P1 *= arr[i];
        }
        else if (arr[i] != 1) {

            // the number is non-prime
            P2 *= arr[i];
        }
    }

    // Return the absolute difference
    return abs(P2 - P1);
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 5, 10, 15, 7 };
    int n     = sizeof(arr) / sizeof(arr[0]);

    // Find the absolute difference
    cout << calculateDifference(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Absolute Difference
// between the Product of Non-Prime numbers
// and Prime numbers of an Array
import java.util.*; 
import java.util.Arrays;
import java.util.Collections;

class GFG{

    // Function to find the difference between
    // the product of non-primes and the
    // product of primes of an array.
    public static int calculateDifference(int []arr, int n)
    {
        // Find maximum value in the array

        int max_val = Arrays.stream(arr).max().getAsInt();

        // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        // THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        boolean[] prime = new boolean[max_val + 1];
        Arrays.fill(prime, true);

        // Remaining part of SIEVE
        prime[0] = false;
        prime[1] = false;
        for (int p = 2; p * p <= max_val; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2 ;i <= max_val ;i += p)
                    prime[i] = false;
            }
        }

        // Store the product of primes in P1 and
        // the product of non primes in P2
        int P1 = 1, P2 = 1;
        for (int i = 0; i < n; i++) {

            if (prime[arr[i]]) {

                // the number is prime
                P1 *= arr[i];
            }
            else if (arr[i] != 1) {

                // the number is non-prime
                P2 *= arr[i];
            }
        }

        // Return the absolute difference
        return Math.abs(P2 - P1);
    }

    // Driver Code
    public static void main(String []args)
    {
        int[] arr = new int []{ 1, 3, 5, 10, 15, 7 };
        int n     = arr.length;

        // Find the absolute difference
        System.out.println(calculateDifference(arr, n));

        System.exit(0);
    }
}
// This code is contributed
// by Harshit Saini 
```

## 蟒蛇 3

```
# Python3 program to find the Absolute Difference
# between the Product of Non-Prime numbers
# and Prime numbers of an Array

# Function to find the difference between
# the product of non-primes and the
# product of primes of an array.
def calculateDifference(arr, n):
    # Find maximum value in the array
    max_val = max(arr)

    # USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    # THAN OR EQUAL TO max_val
    # Create a boolean array "prime[0..n]". A
    # value in prime[i] will finally be false
    # if i is Not a prime, else true.

    prime    = (max_val + 1) * [True]

    # Remaining part of SIEVE
    prime[0] = False
    prime[1] = False
    p = 2

    while p * p <= max_val:

        # If prime[p] is not changed, then
        # it is a prime
        if prime[p] == True:

            # Update all multiples of p
            for i in range(p * 2, max_val+1, p):
                prime[i] = False
        p += 1

    # Store the product of primes in P1 and
    # the product of non primes in P2
    P1 = 1 ; P2 = 1
    for i in range(n):

        if prime[arr[i]]:
            # the number is prime
            P1 *= arr[i]

        elif arr[i] != 1:
            # the number is non-prime
            P2 *= arr[i]

    # Return the absolute difference
    return abs(P2 - P1)

# Driver Code
if __name__ == '__main__':
    arr   = [ 1, 3, 5, 10, 15, 7 ]
    n     = len(arr)

    # Find the absolute difference
    print(calculateDifference(arr, n))
# This code is contributed
# by Harshit Saini
```

## C#

```
// C# program to find the Absolute Difference
// between the Product of Non-Prime numbers
// and Prime numbers of an Array
using System;
using System.Linq;

class GFG{

    // Function to find the difference between
    // the product of non-primes and the
    // product of primes of an array.
    static int calculateDifference(int []arr, int n)
    {
        // Find maximum value in the array
        int max_val = arr.Max();

        // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        // THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        var prime   = Enumerable.Repeat(true,
                                    max_val+1).ToArray();

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

        // Store the product of primes in P1 and
        // the product of non primes in P2
        int P1 = 1, P2 = 1;
        for (int i = 0; i < n; i++) {

            if (prime[arr[i]]) {

                // the number is prime
                P1 *= arr[i];
            }
            else if (arr[i] != 1) {

                // the number is non-prime
                P2 *= arr[i];
            }
        }

        // Return the absolute difference
        return Math.Abs(P2 - P1);
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = new int []{ 1, 3, 5, 10, 15, 7 };
        int n     = arr.Length;

        // Find the absolute difference
        Console.WriteLine(calculateDifference(arr, n));
    }
}
// This code is contributed
// by Harshit Saini
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the Absolute Difference
// between the Product of Non-Prime numbers
// and Prime numbers of an Array

// Function to find the difference between
// the product of non-primes and the
// product of primes of an array.
function calculateDifference($arr, $n){

    // Find maximum value in the array
    $max_val = max($arr);

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    $prime   = array_fill(0 ,$max_val ,true);

    // Remaining part of SIEVE
    $prime[0] = false;
    $prime[1] = false;
    for ($p = 2; $p * $p <= $max_val; $p++) {

        // If prime[p] is not changed, then
        // it is a prime
        if ($prime[$p] == true) {

            // Update all multiples of p
            for ($i = $p * 2; $i <= $max_val; $i += $p)
                $prime[$i] = false;
        }
    }

    // Store the product of primes in P1 and
    // the product of non primes in P2
    $P1 = 1;
    $P2 = 1;
    for ($i = 0; $i < $n; $i++) {

        if ($prime[$arr[$i]]) {

            // the number is prime
            $P1 *= $arr[$i];
        }
        else if ($arr[$i] != 1) {

            // the number is non-prime
            $P2 *= $arr[$i];
        }
    }

    // Return the absolute difference
    return abs($P2 - $P1);
}

// Driver Code
$arr = array( 1, 3, 5, 10, 15, 7 );
$n   = count($arr, COUNT_NORMAL);

// Find the absolute difference
echo CalculateDifference($arr, $n);

// This code is contributed
// by Harshit Saini
?>
```

## java 描述语言

```
<script>

// Javascript program to find the Absolute Difference
// between the Product of Non-Prime numbers
// and Prime numbers of an Array

    // Function to find the difference between
    // the product of non-primes and the
    // product of primes of an array.
    function calculateDifference(arr , n)
    {
        // Find maximum value in the array

        var max_val = Math.max.apply(Math,arr);

        // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
        // THAN OR EQUAL TO max_val
        // Create a boolean array "prime[0..n]". A
        // value in prime[i] will finally be false
        // if i is Not a prime, else true.
        var prime = Array(max_val + 1).fill(true);

        // Remaining part of SIEVE
        prime[0] = false;
        prime[1] = false;
        for (p = 2; p * p <= max_val; p++) {

            // If prime[p] is not changed, then
            // it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (i = p * 2; i <= max_val; i += p)
                    prime[i] = false;
            }
        }

        // Store the product of primes in P1 and
        // the product of non primes in P2
        var P1 = 1, P2 = 1;
        for (i = 0; i < n; i++) {

            if (prime[arr[i]]) {

                // the number is prime
                P1 *= arr[i];
            } else if (arr[i] != 1) {

                // the number is non-prime
                P2 *= arr[i];
            }
        }

        // Return the absolute difference
        return Math.abs(P2 - P1);
    }

    // Driver Code

        var arr = [ 1, 3, 5, 10, 15, 7 ];
        var n = arr.length;

        // Find the absolute difference
        document.write(calculateDifference(arr, n));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
45
```

**时间复杂度:** O(N * log(log(N))
**空间复杂度:** O(MAX(N，max_val))，其中 max_val 是给定数组中元素的最大值。