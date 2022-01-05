# 数组中每第 K 个素数的和

> 原文:[https://www . geesforgeks . org/每 kth 素数之和数组-2/](https://www.geeksforgeeks.org/sum-of-every-kth-prime-number-in-an-array-2/)

给定一个整数 *k* 和一个整数数组 *arr* (小于 10^6)，任务是找出数组中每第 k 个素数的和。
**例:**

> **输入:** arr[] = {2，3，5，7，11}，k = 2
> **输出:** 10
> 数组的所有元素都是质数。所以，每个 K(即 2)区间后的素数是 3，7，它们的和是 10。
> **输入:** arr[] = {11，13，15，17，19}，k = 2
> **输出:** 32

**简单方法:**遍历数组，找出数组中每第 K 个素数，计算运行和。这样，我们将不得不检查数组的每个元素是否是质数，随着数组大小的增加，这将花费更多的时间。
**有效方法:**创建一个筛子，用来存储一个数是否是质数。然后，它可以用来在 O(1)时间内检查一个数字是否符合质数。这样，我们只需要跟踪每一个第 K 个素数，并保持运行和。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 1000000
bool prime[MAX + 1];
void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]"
    // and initialize all the entries as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    memset(prime, true, sizeof(prime));

    // 0 and 1 are not prime numbers
    prime[1] = false;
    prime[0] = false;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// compute the answer
void SumOfKthPrimes(int arr[], int n, int k)
{
    // count of primes
    int c = 0;

    // sum of the primes
    long long int sum = 0;

    // traverse the array
    for (int i = 0; i < n; i++) {

        // if the number is a prime
        if (prime[arr[i]]) {

            // increase the count
            c++;

            // if it is the K'th prime
            if (c % k == 0) {
                sum += arr[i];
                c = 0;
            }
        }
    }
    cout << sum << endl;
}

// Driver code
int main()
{
    // create the sieve
    SieveOfEratosthenes();

    int arr[] = { 2, 3, 5, 7, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;

    SumOfKthPrimes(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

public class GFG {

    static int MAX = 1000000;
    static boolean prime[] = new boolean[MAX + 1];

    static void SieveOfEratosthenes() {
        // Create a boolean array "prime[0..n]"
        // and initialize all the entries as true.
        // A value in prime[i] will finally be false
        // if i is Not a prime, else true.
        for (int i = 0; i < prime.length; i++) {
            prime[i] = true;
        }

        // 0 and 1 are not prime numbers
        prime[1] = false;
        prime[0] = false;

        for (int p = 2; p * p <= MAX; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= MAX; i += p) {
                    prime[i] = false;
                }
            }
        }
    }

// compute the answer
    static void SumOfKthPrimes(int arr[], int n, int k) {
        // count of primes
        int c = 0;

        // sum of the primes
        long sum = 0;

        // traverse the array
        for (int i = 0; i < n; i++) {

            // if the number is a prime
            if (prime[arr[i]]) {

                // increase the count
                c++;

                // if it is the K'th prime
                if (c % k == 0) {
                    sum += arr[i];
                    c = 0;
                }
            }
        }
        System.out.println(sum);
    }

// Driver code
    public static void main(String[] args) {
        // create the sieve
        SieveOfEratosthenes();
        int arr[] = {2, 3, 5, 7, 11};
        int n = arr.length;
        int k = 2;
        SumOfKthPrimes(arr, n, k);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 100000;
prime = [True] * (MAX + 1);

def SieveOfEratosthenes():

    # Create a boolean array "prime[0..n]"
    # and initialize all the entries
    # as true. A value in prime[i] will
    # finally be false if i is Not a prime,
    # else true.

    # 0 and 1 are not prime numbers
    prime[1] = False;
    prime[0] = False;

    p = 2;
    while(p * p <= MAX):

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p]):

            # Update all multiples of p
            i = p * 2;
            while(i <= MAX):
                prime[i] = False;
                i += p;
        p += 1;

# compute the answer
def SumOfKthPrimes(arr, n, k):

    # count of primes
    c = 0;

    # sum of the primes
    sum = 0;

    # traverse the array
    for i in range(n):

        # if the number is a prime
        if (prime[arr[i]]):

            # increase the count
            c+=1;

            # if it is the K'th prime
            if (c % k == 0):
                sum += arr[i];
                c = 0;

    print(sum);

# Driver code

# create the sieve
SieveOfEratosthenes();

arr = [ 2, 3, 5, 7, 11 ];
n = len(arr);
k = 2;

SumOfKthPrimes(arr, n, k);

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
class GFG
{
static int MAX = 1000000;
static bool[] prime = new bool[MAX + 1];
static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]"
    // and initialize all the entries as true.
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.

    // 0 and 1 are not prime numbers
    prime[1] = false;
    prime[0] = false;

    for (int p = 2; p * p <= MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == false)
        {

            // Update all multiples of p
            for (int i = p * 2;
                     i <= MAX; i += p)
                prime[i] = true;
        }
    }
}

// compute the answer
static void SumOfKthPrimes(int[] arr,
                           int n, int k)
{
    // count of primes
    int c = 0;

    // sum of the primes
    long sum = 0;

    // traverse the array
    for (int i = 0; i < n; i++)
    {

        // if the number is a prime
        if (!prime[arr[i]])
        {

            // increase the count
            c++;

            // if it is the K'th prime
            if (c % k == 0)
            {
                sum += arr[i];
                c = 0;
            }
        }
    }
    System.Console.WriteLine(sum);
}

// Driver code
static void Main()
{
    // create the sieve
    SieveOfEratosthenes();

    int[] arr = new int[] { 2, 3, 5, 7, 11 };
    int n = arr.Length;
    int k = 2;

    SumOfKthPrimes(arr, n, k);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$MAX = 100000;
$prime = array_fill(0, $MAX + 1, true);
function SieveOfEratosthenes()
{
    global $MAX, $prime;

    // Create a boolean array "prime[0..n]"
    // and initialize all the entries
    // as true. A value in prime[i] will
    // finally be false if i is Not a prime,
    // else true.

    // 0 and 1 are not prime numbers
    $prime[1] = false;
    $prime[0] = false;

    for ($p = 2; $p * $p <= $MAX; $p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2;
                 $i <= $MAX; $i += $p)
                $prime[$i] = false;
        }
    }
}

// compute the answer
function SumOfKthPrimes($arr, $n, $k)
{
    global $MAX, $prime;

    // count of primes
    $c = 0;

    // sum of the primes
    $sum = 0;

    // traverse the array
    for ($i = 0; $i < $n; $i++)
    {

        // if the number is a prime
        if ($prime[$arr[$i]])
        {

            // increase the count
            $c++;

            // if it is the K'th prime
            if ($c % $k == 0)
            {
                $sum += $arr[$i];
                $c = 0;
            }
        }
    }
    echo $sum."\n";
}

// Driver code

// create the sieve
SieveOfEratosthenes();

$arr = array( 2, 3, 5, 7, 11 );
$n = sizeof($arr);
$k = 2;

SumOfKthPrimes($arr, $n, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach
let MAX = 100000;
let prime = new Array(MAX + 1).fill(true);
function SieveOfEratosthenes() {
    // Create a boolean array "prime[0..n]"
    // and initialize all the entries
    // as true. A value in prime[i] will
    // finally be false if i is Not a prime,
    // else true.

    // 0 and 1 are not prime numbers
    prime[1] = false;
    prime[0] = false;

    for (let p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (let i = p * 2;
                i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// compute the answer
function SumOfKthPrimes(arr, n, k) {
    // count of primes
    let c = 0;

    // sum of the primes
    let sum = 0;

    // traverse the array
    for (let i = 0; i < n; i++) {

        // if the number is a prime
        if (prime[arr[i]]) {

            // increase the count
            c++;

            // if it is the K'th prime
            if (c % k == 0) {
                sum += arr[i];
                c = 0;
            }
        }
    }
    document.write(sum + "<br>");
}

// Driver code

// create the sieve
SieveOfEratosthenes();

let arr = new Array(2, 3, 5, 7, 11);
let n = arr.length;
let k = 2;

SumOfKthPrimes(arr, n, k);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
10
```