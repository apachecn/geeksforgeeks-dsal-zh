# 检查素数之和是否能被数组中的任意素数整除

> 原文:[https://www . geesforgeks . org/check-如果素数之和可被数组中的任意素数整除/](https://www.geeksforgeeks.org/check-if-the-sum-of-primes-is-divisible-by-any-prime-from-the-array/)

给定一个数组 **arr[]** ，任务是检查数组中的素数之和是否能被数组中的任意素数整除。如果是则打印**是**，否则打印**否**。

**示例:**

> **输入:** arr[] = {2，3}
> **输出:** NO
> 素数:2，3
> 和= 2 + 3 = 5 既不能被 2 整除也不能被 3 整除
> 
> **输入:** arr[] = {1，2，3，4，5}
> **输出:**是
> 2 + 3 + 5 = 10 既可以被 2 整除，也可以被 5 整除

**方法:**想法是使用厄拉多塞的[筛从数组中生成最大元素的所有素数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

*   遍历数组，检查当前元素是否是质数。如果是质数，则更新 **sum = sum + arr[i]** 。
*   再次遍历数组，检查**总和% arr[i] = 0** ，其中 **arr[i]是质数**。如果是，则打印**是**。否则最后打印**否**。

下面是上述方法的实现:

## C++

```
// C++ program to check if sum of primes from an array
// is divisible by any of the primes from the same array
#include <bits/stdc++.h>
using namespace std;

// Function to print "YES" if sum of primes from an array
// is divisible by any of the primes from the same array
void SumDivPrime(int A[], int n)
{
    int max_val = *(std::max_element(A, A + n)) + 1;

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

    int sum = 0;

    // Traverse through the array
    for (int i = 0; i < n; ++i) {
        if (prime[A[i]])
            sum += A[i];
    }

    for (int i = 0; i < n; ++i) {
        if (prime[A[i]] && sum % A[i] == 0) {
            cout << "YES";
            return;
        }
    }

    cout << "NO";
}

// Driver program
int main()
{
    int A[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(A) / sizeof(A[0]);

    SumDivPrime(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if sum of primes from an array
// is divisible by any of the primes from the same array
class Solution
{
    //returns the maximum value
static int max_element(int A[])
{
    int max=Integer.MIN_VALUE;

    for(int i=0;i<A.length;i++)
        if(max<A[i])
            max=A[i];

    return max;
}

// Function to print "YES" if sum of primes from an array
// is divisible by any of the primes from the same array
static void SumDivPrime(int A[], int n)
{
    int max_val = (max_element(A)) + 1;

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    boolean prime[]=new boolean[max_val+1];

    //initialize the array
    for(int i=0;i<=max_val;i++)
    prime[i]=true;

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

    int sum = 0;

    // Traverse through the array
    for (int i = 0; i < n; ++i) {
        if (prime[A[i]])
            sum += A[i];
    }

    for (int i = 0; i < n; ++i) {
        if (prime[A[i]] && sum % A[i] == 0) {
            System.out.println( "YES");
            return;
        }
    }

    System.out.println("NO");
}

// Driver program
public static void main(String args[])
{
    int A[] = { 1, 2, 3, 4, 5 };
    int n = A.length;

    SumDivPrime(A, n);
}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to check if sum of
# primes from an array is divisible
# by any of the primes from the same array
import math

# Function to print "YES" if sum of primes
# from an array is divisible by any of the
# primes from the same array
def SumDivPrime(A, n):

    max_val = max(A) + 1

    # USE SIEVE TO FIND ALL PRIME NUMBERS
    # LESS THAN OR EQUAL TO max_val
    # Create a boolean array "prime[0..n]".
    # A value in prime[i] will finally be
    # false if i is Not a prime, else true.
    prime = [True] * (max_val + 1)

    # Remaining part of SIEVE
    prime[0] = False
    prime[1] = False
    for p in range(2, int(math.sqrt(max_val)) + 1):

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p] == True :

            # Update all multiples of p
            for i in range(2 * p, max_val + 1, p):
                prime[i] = False

    sum = 0

    # Traverse through the array
    for i in range(0, n):
        if prime[A[i]]:
            sum += A[i]

    for i in range(0, n):
        if prime[A[i]] and sum % A[i] == 0:
            print("YES")
            return

    print("NO")

# Driver Code
A = [ 1, 2, 3, 4, 5 ]
n = len(A)

SumDivPrime(A, n)

# This code is contributed
# by saurabh_shukla
```

## C#

```
// C# program to check if sum of primes
// from an array is divisible by any of
// the primes from the same array
class GFG
{

//returns the maximum value
static int max_element(int[] A)
{
    int max = System.Int32.MinValue;

    for(int i = 0; i < A.Length; i++)
        if(max < A[i])
            max = A[i];

    return max;
}

// Function to print "YES" if sum of
// primes from an array  is divisible
// by any of the primes from the same array
static void SumDivPrime(int[] A, int n)
{
    int max_val = (max_element(A)) + 1;

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    bool[] prime=new bool[max_val+1];

    //initialize the array
    for(int i = 0; i <= max_val; i++)
        prime[i] = true;

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
                prime[i] = false;
        }
    }
    int sum = 0;

    // Traverse through the array
    for (int i = 0; i < n; ++i)
    {
        if (prime[A[i]])
            sum += A[i];
    }

    for (int i = 0; i < n; ++i)
    {
        if (prime[A[i]] && sum % A[i] == 0)
        {
            System.Console.WriteLine( "YES");
            return;
        }
    }
    System.Console.WriteLine("NO");
}

// Driver code
public static void Main()
{
    int []A = { 1, 2, 3, 4, 5 };
    int n = A.Length;
    SumDivPrime(A, n);
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if sum of primes
// from an array is divisible by any of
// the primes from the same array

// Function to print "YES" if sum of primes
// from an array is divisible by any of the
// primes from the same array
function SumDivPrime($A, $n)
{
    $max_val = max($A);

    // USE SIEVE TO FIND ALL PRIME NUMBERS
    // LESS THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    $prime = array_fill(1, $max_val + 1, true);

    // Remaining part of SIEVE
    $prime[0] = false;
    $prime[1] = false;
    for ($p = 2; $p * $p <= $max_val; $p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if ($prime[$p] == true)
        {

            // Update all multiples of p
            for ($i = $p * 2;
                 $i <= $max_val; $i += $p)
                $prime[$i] = false;
        }
    }

    $sum = 0;

    // Traverse through the array
    for ($i = 0; $i < $n; ++$i)
    {
        if ($prime[$A[$i]])
            $sum += $A[$i];
    }

    for ($i = 0; $i < $n; ++$i)
    {
        if ($prime[$A[$i]] &&
            $sum % $A[$i] == 0)
        {
            echo "YES";
            return;
        }
    }

    echo "NO";
}

// Driver Code
$A = array( 1, 2, 3, 4, 5 );
$n = sizeof($A) ;

SumDivPrime($A, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript program to check if sum
// of primes from an array is divisible
// by any of the primes from the same array 

// Returns the maximum value
function max_element(A)
{
    var max = Number.MIN_VALUE;

    for(var i = 0; i < A.length; i++)
        if (max < A[i])
            max = A[i];

    return max;
}

// Function to print "YES" if sum of primes
// from an array is divisible by any of the
// primes from the same array
function SumDivPrime(A, n)
{
    var max_val = (max_element(A)) + 1;

    // USE SIEVE TO FIND ALL PRIME NUMBERS LESS
    // THAN OR EQUAL TO max_val
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    var prime = new Array(max_val + 1);

    // Initialize the array
    for(var i = 0; i <= max_val; i++)
        prime[i] = true;

    // Remaining part of SIEVE
    prime[0] = false;
    prime[1] = false;

    for(var p = 2; p * p <= max_val; p++)
    {

        // If prime[p] is not changed, then
        // it is a prime
        if (prime[p] == true)
        {

            // Update all multiples of p
            for(var i = p * 2; i <= max_val; i += p)
                prime[i] = false;
        }
    }

    var sum = 0;

    // Traverse through the array
    for(var i = 0; i < n; ++i)
    {
        if (prime[A[i]])
            sum += A[i];
    }

    for(var i = 0; i < n; ++i)
    {
        if (prime[A[i]] && sum % A[i] == 0)
        {
            document.write("YES");
            return;
        }
    }
    document.write("NO");
}

// Driver code
var A = [ 1, 2, 3, 4, 5 ];
var n = A.length;
SumDivPrime(A, n);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
YES
```