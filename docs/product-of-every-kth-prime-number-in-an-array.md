# 数组中每第 K 个素数的乘积

> 原文:[https://www . geeksforgeeks . org/每 kth 个素数的乘积在数组中/](https://www.geeksforgeeks.org/product-of-every-kth-prime-number-in-an-array/)

给定一个整数“k”和一个整数数组“arr”(小于 10^6)，任务是找出数组中每第 k 个素数的乘积。
**例:**

> **输入:** arr = {2，3，5，7，11}，k = 2
> **输出:** 21
> 数组的所有元素都是质数。所以，每个 K(即 2)区间后的素数是 3，7，它们的乘积是 21。
> **输入:** arr = {41，23，12，17，18，19}，k = 2
> **输出:** 437

**一个简单的方法:**遍历数组，找到数组中的每 K 个素数，计算运行乘积。这样，我们将不得不检查数组的每个元素是否是质数，随着数组大小的增加，这将花费更多的时间。
**有效方法:**创建一个筛子，用来存储一个数是否是质数。然后，它可以用来在 O(1)时间内检查一个数字是否符合质数。这样，我们只需要跟踪每个第 K 个素数，并维护运行的产品。
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
void productOfKthPrimes(int arr[], int n, int k)
{
    // count of primes
    int c = 0;

    // product of the primes
    long long int product = 1;

    // traverse the array
    for (int i = 0; i < n; i++) {

        // if the number is a prime
        if (prime[arr[i]]) {

            // increase the count
            c++;

            // if it is the K'th prime
            if (c % k == 0) {
                product *= arr[i];
                c = 0;
            }
        }
    }
    cout << product << endl;
}

// Driver code
int main()
{

    // create the sieve
    SieveOfEratosthenes();

    int n = 5, k = 2;

    int arr[n] = { 2, 3, 5, 7, 11 };

    productOfKthPrimes(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{
static int MAX=1000000;
static boolean[] prime=new boolean[MAX + 1];
static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]"
    // and initialize all the entries as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    //memset(prime, true, sizeof(prime));

    // 0 and 1 are not prime numbers
    prime[1] = true;
    prime[0] = true;

    for (int p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == false) {

            // Update all multiples of p
            for (int i = p * 2; i <= MAX; i += p)
                prime[i] = true;
        }
    }
}

// compute the answer
static void productOfKthPrimes(int arr[], int n, int k)
{
    // count of primes
    int c = 0;

    // product of the primes
    int product = 1;

    // traverse the array
    for (int i = 0; i < n; i++) {

        // if the number is a prime
        if (!prime[arr[i]]) {

            // increase the count
            c++;

            // if it is the K'th prime
            if (c % k == 0) {
                product *= arr[i];
                c = 0;
            }
        }
    }
    System.out.println(product);
}

// Driver code
public static void main(String[] args)
{

    // create the sieve
    SieveOfEratosthenes();

    int n = 5, k = 2;

    int[] arr=new int[]{ 2, 3, 5, 7, 11 };

    productOfKthPrimes(arr, n, k);
}
}
// This code is contributed by mits
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

MAX = 1000000
prime = [True]*(MAX + 1)
def SieveOfEratosthenes():

    # Create a boolean array "prime[0..n]"
    # and initialize all the entries as true.
    # A value in prime[i] will finally be false
    # if i is Not a prime, else true.

    # 0 and 1 are not prime numbers
    prime[1] = False;
    prime[0] = False;

    p = 2
    while p * p <= MAX:

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            for i in range(p * 2, MAX+1, p):
                prime[i] = False
        p+=1

# compute the answer
def productOfKthPrimes(arr, n, k):

    # count of primes
    c = 0

    # product of the primes
    product = 1

    # traverse the array
    for i in range( n):

        # if the number is a prime
        if (prime[arr[i]]):

            # increase the count
            c+=1

            # if it is the K'th prime
            if (c % k == 0) :
                product *= arr[i]
                c = 0

    print(product)

# Driver code
if __name__ == "__main__":

    # create the sieve
    SieveOfEratosthenes()

    n = 5
    k = 2

    arr = [ 2, 3, 5, 7, 11 ]

    productOfKthPrimes(arr, n, k)

# This code is contributed by ChitraNayal
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
    // and initialize all the entries as
    // true. A value in prime[i] will
    // finally be false if i is Not a prime,
    // else true.

    // 0 and 1 are not prime numbers
    prime[1] = true;
    prime[0] = true;

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
static void productOfKthPrimes(int[] arr,
                               int n, int k)
{
    // count of primes
    int c = 0;

    // product of the primes
    int product = 1;

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
                product *= arr[i];
                c = 0;
            }
        }
    }
    System.Console.WriteLine(product);
}

// Driver code
static void Main()
{

    // create the sieve
    SieveOfEratosthenes();

    int n = 5, k = 2;

    int[] arr=new int[]{ 2, 3, 5, 7, 11 };

    productOfKthPrimes(arr, n, k);
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

let MAX = 1000000;
let prime = new Array(MAX + 1);
function SieveOfEratosthenes() {
    // Create a boolean array "prime[0..n]"
    // and initialize all the entries as true.
    // A value in prime[i] will finally be false
    // if i is Not a prime, else true.
    prime.fill(true)

    // 0 and 1 are not prime numbers
    prime[1] = false;
    prime[0] = false;

    for (let p = 2; p * p <= MAX; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (let i = p * 2; i <= MAX; i += p)
                prime[i] = false;
        }
    }
}

// compute the answer
function productOfKthPrimes(arr, n, k) {
    // count of primes
    let c = 0;

    // product of the primes
    let product = 1;

    // traverse the array
    for (let i = 0; i < n; i++) {

        // if the number is a prime
        if (prime[arr[i]]) {

            // increase the count
            c++;

            // if it is the K'th prime
            if (c % k == 0) {
                product *= arr[i];
                c = 0;
            }
        }
    }
    document.write(product + "<br>");
}

// Driver code

// create the sieve
SieveOfEratosthenes();

let n = 5, k = 2;

let arr = [2, 3, 5, 7, 11];

productOfKthPrimes(arr, n, k);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
21
```

**时间复杂度:** O(n)