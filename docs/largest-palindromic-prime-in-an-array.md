# 数组中最大的回文素数

> 原文:[https://www . geesforgeks . org/maximum-回文-数组中的质数/](https://www.geeksforgeeks.org/largest-palindromic-prime-in-an-array/)

给定一个整数数组 **arr[]** ，任务是打印数组中最大的[回文素数](https://www.geeksforgeeks.org/palindromic-primes/)。如果数组中没有元素是回文质数，则打印 **-1** 。
**举例:**

> **输入:** arr[] = {11，5，121，7，89}
> **输出:** 11
> 11，5 和 7 是数组中唯一的回文素数。
> 其中 11 个最大。
> **输入:** arr[] = {2，4，6，8，10}
> **输出:** 2

一个**简单的方法**是遍历每一个数组元素，[检查是否是素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)，[检查是否是回文](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)。如果是，如果结果也大于当前结果，则更新结果。
**大量元素的高效方法:**

*   使用厄拉多塞的[筛计算一个数是否是素数，直到数组中的最大元素。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   现在，初始化一个变量 **currentMax = -1** 并开始遍历数组 **arr[]** 。
*   对于每一个 **i** ，如果**arr【I】**是 **prime** 以及**回文**和**arr【I】>current max**那么更新**current max = arr【I】**。
*   最后打印 **currentMax** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if n is a palindrome
bool isPal(int n)
{
    // Find the appropriate divisor
    // to extract the leading digit
    int divisor = 1;
    while (n / divisor >= 10)
        divisor *= 10;

    while (n != 0) {
        int leading = n / divisor;
        int trailing = n % 10;

        // If first and last digit
        // not same return false
        if (leading != trailing)
            return false;

        // Removing the leading and trailing
        // digit from number
        n = (n % divisor) / 10;

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        divisor = divisor / 100;
    }
    return true;
}

// Function to return the largest
// palindromic prime present in the array
int maxPalindromicPrime(int arr[], int n)
{
    int maxElement = *max_element(arr, arr + n);

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    bool prime[maxElement + 1];
    memset(prime, true, sizeof(prime));

    // 0 and 1 are not primes
    prime[0] = prime[1] = false;
    for (int p = 2; p * p <= maxElement; p++) {

        // If prime[p] is not changed, then it is
        // a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= maxElement; i += p)
                prime[i] = false;
        }
    }

    int currentMax = -1;
    for (int i = 0; i < n; i++)

        // If arr[i] is prime as well as palindrome
        if (prime[arr[i]] && isPal(arr[i]))
            currentMax = max(currentMax, arr[i]);

    return currentMax;
}

// Driver Program
int main()
{
    int arr[] = { 11, 5, 121, 7, 89 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxPalindromicPrime(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.Arrays;
public class GFG{

    // Function that returns true if n is a palindrome
    static boolean isPal(int n)
    {
        // Find the appropriate divisor
        // to extract the leading digit
        int divisor = 1;
        while (n / divisor >= 10)
            divisor *= 10;

        while (n != 0) {
            int leading = n / divisor;
            int trailing = n % 10;

            // If first and last digit
            // not same return false
            if (leading != trailing)
                return false;

            // Removing the leading and trailing
            // digit from number
            n = (n % divisor) / 10;

            // Reducing divisor by a factor
            // of 2 as 2 digits are dropped
            divisor = divisor / 100;
        }
        return true;
    }

    // Function to return the largest
    // palindromic prime present in the array
    static int maxPalindromicPrime(int []arr, int n)
    {
        int maxElement = Arrays.stream(arr).max().getAsInt();

        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value
        // in prime[i] will finally be false if i is
        // Not a prime, else true.
        boolean []prime = new boolean[maxElement + 1];
        for (int i = 0; i < maxElement + 1 ; i++)
            prime[i] = true ;

        // 0 and 1 are not primes
        prime[0] = prime[1] = false;
        for (int p = 2; p * p <= maxElement; p++) {

            // If prime[p] is not changed, then it is
            // a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= maxElement; i += p)
                    prime[i] = false;
            }
        }

        int currentMax = -1;
        for (int i = 0; i < n; i++)

            // If arr[i] is prime as well as palindrome
            if (prime[arr[i]] == true && isPal(arr[i]) == true)
                currentMax = Math.max(currentMax, arr[i]);

        return currentMax;
    }

    // Driver Program
     public static void main(String []args)
    {
        int []arr = { 11, 5, 121, 7, 89 };
        int n = arr.length ;
        System.out.println(maxPalindromicPrime(arr, n)) ;
    }

}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
from math import sqrt

# Function that returns true
# if n is a palindrome
def isPal(n):

    # Find the appropriate divisor
    # to extract the leading digit
    divisor = 1
    while (n / divisor >= 10):
        divisor *= 10

    while (n != 0):
        leading = int(n / divisor)
        trailing = n % 10

        # If first and last digit
        # not same return false
        if (leading != trailing):
            return False

        # Removing the leading and trailing
        # digit from number
        n = int((n % divisor) / 10)

        # Reducing divisor by a factor
        # of 2 as 2 digits are dropped
        divisor = int(divisor / 100)

    return True

# Function to return the largest
# palindromic prime present in the array
def maxPalindromicPrime(arr, n):
    maxElement = arr[0]
    for i in range(len(arr)):
        if (arr[i]>maxElement):
            maxElement = arr[i]

    # Create a boolean array "prime[0..n]" and
    # initialize all entries it as true. A value
    # in prime[i] will finally be false if i is
    # Not a prime, else true.
    prime = [True for i in range(maxElement + 1)]

    # 0 and 1 are not primes
    prime[0] = False
    prime[1] = False
    for p in range(2, int(sqrt(maxElement)) + 1, 1):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2,maxElement + 1, p):
                prime[i] = False

    currentMax = -1
    for i in range(n):

        # If arr[i] is prime as well as palindrome
        if (prime[arr[i]] and isPal(arr[i])):
            currentMax = max(currentMax, arr[i])

    return currentMax

# Driver Code
if __name__ == '__main__':
    arr = [11, 5, 121, 7, 89]
    n = len(arr)
    print(maxPalindromicPrime(arr, n))

# This code is contributed by
# Shashank_Shamra
```

## C#

```
// C# implementation of the above approach

using System ;
using System.Linq ;

public class GFG{

    // Function that returns true if n is a palindrome
    static bool isPal(int n)
    {
        // Find the appropriate divisor
        // to extract the leading digit
        int divisor = 1;
        while (n / divisor >= 10)
            divisor *= 10;

        while (n != 0) {
            int leading = n / divisor;
            int trailing = n % 10;

            // If first and last digit
            // not same return false
            if (leading != trailing)
                return false;

            // Removing the leading and trailing
            // digit from number
            n = (n % divisor) / 10;

            // Reducing divisor by a factor
            // of 2 as 2 digits are dropped
            divisor = divisor / 100;
        }
        return true;
    }

    // Function to return the largest
    // palindromic prime present in the array
    static int maxPalindromicPrime(int []arr, int n)
    {
        int maxElement = arr.Max() ;

        // Create a boolean array "prime[0..n]" and
        // initialize all entries it as true. A value
        // in prime[i] will finally be false if i is
        // Not a prime, else true.
        bool []prime = new bool [maxElement + 1];
        for (int i = 0; i < maxElement + 1 ; i++)
            prime[i] = true ;

        // 0 and 1 are not primes
        prime[0] = prime[1] = false;
        for (int p = 2; p * p <= maxElement; p++) {

            // If prime[p] is not changed, then it is
            // a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= maxElement; i += p)
                    prime[i] = false;
            }
        }

        int currentMax = -1;
        for (int i = 0; i < n; i++)

            // If arr[i] is prime as well as palindrome
            if (prime[arr[i]] == true && isPal(arr[i]) == true)
                currentMax = Math.Max(currentMax, arr[i]);

        return currentMax;
    }

    // Driver Program
     public static void Main()
    {
        int []arr = { 11, 5, 121, 7, 89 };
        int n = arr.Length ;
        Console.WriteLine(maxPalindromicPrime(arr, n)) ;
    }

    // This code is contributed by Ryuga
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true
// if n is a palindrome
function isPal($n)
{
    // Find the appropriate divisor
    // to extract the leading digit
    $divisor = 1;
    while ((int)($n / $divisor) >= 10)
        $divisor *= 10;

    while ($n != 0)
    {
        $leading = (int)($n / $divisor);
        $trailing = $n % 10;

        // If first and last digit
        // not same return false
        if ($leading != $trailing)
            return false;

        // Removing the leading and trailing
        // digit from number
        $n = (int)(($n % $divisor) / 10);

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        $divisor = (int)($divisor / 100);
    }
    return true;
}

// Function to return the largest
// palindromic prime present in the array
function maxPalindromicPrime($arr, $n)
{
    $maxElement = max($arr);

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    $prime = array_fill(0, ($maxElement + 1), true);

    // 0 and 1 are not primes
    $prime[0] = $prime[1] = false;
    for ($p = 2; $p * $p <= $maxElement; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2;
                 $i <= $maxElement; $i += $p)
                $prime[$i] = false;
        }
    }

    $currentMax = -1;
    for ($i = 0; $i < $n; $i++)

        // If arr[i] is prime as well as palindrome
        if ($prime[$arr[$i]] && isPal($arr[$i]))
            $currentMax = max($currentMax, $arr[$i]);

    return $currentMax;
}

// Driver Code
$arr = array( 11, 5, 121, 7, 89 );
$n = count($arr);
echo maxPalindromicPrime($arr, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that returns true
// if n is a palindrome
function isPal(n) {
    // Find the appropriate divisor
    // to extract the leading digit
    let divisor = 1;
    while (Math.floor(n / divisor) >= 10)
        divisor *= 10;

    while (n != 0) {
        let leading = Math.floor(n / divisor);
        let trailing = n % 10;

        // If first and last digit
        // not same return false
        if (leading != trailing)
            return false;

        // Removing the leading and trailing
        // digit from number
        n = Math.floor((n % divisor) / 10);

        // Reducing divisor by a factor
        // of 2 as 2 digits are dropped
        divisor = Math.floor(divisor / 100);
    }
    return true;
}

// Function to return the largest
// palindromic prime present in the array
function maxPalindromicPrime(arr, n) {
    let maxElement = arr.sort((a, b) => a - b).reverse()[0];

    // Create a boolean array "prime[0..n]" and
    // initialize all entries it as true. A value
    // in prime[i] will finally be false if i is
    // Not a prime, else true.
    let prime = new Array(maxElement + 1).fill(true);

    // 0 and 1 are not primes
    prime[0] = prime[1] = false;
    for (let p = 2; p * p <= maxElement; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (let i = p * 2;
                i <= maxElement; i += p)
                prime[i] = false;
        }
    }

    let currentMax = -1;
    for (let i = 0; i < n; i++)

        // If arr[i] is prime as well as palindrome
        if (prime[arr[i]] && isPal(arr[i]))
            currentMax = Math.max(currentMax, arr[i]);

    return currentMax;
}

// Driver Code
let arr = [11, 5, 121, 7, 89];
let n = arr.length;
document.write(maxPalindromicPrime(arr, n));

// This code is contributed by gfgking
</script>
```

**Output:** 

```
11
```