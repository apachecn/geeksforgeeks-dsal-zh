# 从给定数组中移除所有质数

> 原文:[https://www . geesforgeks . org/从给定数组中移除所有质数/](https://www.geeksforgeeks.org/remove-all-the-prime-numbers-from-the-given-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是移除所有质数。

**示例:**

> **输入:** arr[] = {4，6，5，3，8，7，10，11，14，15 }
> T3】输出: 4 6 8 10 14 15
> 
> **输入:** arr[] = {2，4，7，8，9，11}
> 输出: 4 8 9

**方法:**遍历数组，检查当前数是否是质数，如果是，则左移其后的所有元素，去掉这个质数，减少数组长度的值。对数组的所有元素重复此操作。要检查数字是否为质数，使用厄拉多塞[筛](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)生成所有质数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int sz = 1e5;
bool isPrime[sz + 1];

// Function for Sieve of Eratosthenes
void sieve()
{
    memset(isPrime, true, sizeof(isPrime));

    isPrime[0] = isPrime[1] = false;

    for (int i = 2; i * i <= sz; i++) {
        if (isPrime[i]) {
            for (int j = i * i; j < sz; j += i) {
                isPrime[j] = false;
            }
        }
    }
}

// Function to print the elements of the array
void printArray(int arr[], int len)
{
    for (int i = 0; i < len; i++) {
        cout << arr[i] << ' ';
    }
}

// Function to remove all the prime numbers
void removePrimes(int arr[], int len)
{
    // Generate primes
    sieve();

    // Traverse the array
    for (int i = 0; i < len; i++) {

        // If the current element is prime
        if (isPrime[arr[i]]) {

            // Shift all the elements on the
            // right of it to the left
            for (int j = i; j < len; j++) {
                arr[j] = arr[j + 1];
            }

            // Decrease the loop counter by 1
            // to check the shifted element
            i--;

            // Decrease the length
            len--;
        }
    }

    // Print the updated array
    printArray(arr, len);
}

// Driver code
int main()
{
    int arr[] = { 4, 6, 5, 3, 8, 7,
                  10, 11, 14, 15 };
    int len = sizeof(arr) / sizeof(int);

    removePrimes(arr, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int sz = (int) 1e5;
static boolean []isPrime = new boolean[sz + 1];

// Function for Sieve of Eratosthenes
static void sieve()
{
    for (int i = 0; i < sz + 1; i++)
        isPrime[i] = true;

    isPrime[0] = isPrime[1] = false;

    for (int i = 2; i * i <= sz; i++)
    {
        if (isPrime[i])
        {
            for (int j = i * i; j < sz; j += i)
            {
                isPrime[j] = false;
            }
        }
    }
}

// Function to print the elements of the array
static void printArray(int arr[], int len)
{
    for (int i = 0; i < len; i++)
    {
        System.out.print(arr[i] + " ");
    }
}

// Function to remove all the prime numbers
static void removePrimes(int arr[], int len)
{
    // Generate primes
    sieve();

    // Traverse the array
    for (int i = 0; i < len; i++)
    {

        // If the current element is prime
        if (isPrime[arr[i]])
        {

            // Shift all the elements on the
            // right of it to the left
            for (int j = i; j < len-1; j++)
            {
                arr[j] = arr[j + 1];
            }

            // Decrease the loop counter by 1
            // to check the shifted element
            i--;

            // Decrease the length
            len--;
        }
    }

    // Print the updated array
    printArray(arr, len);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 6, 5, 3, 8, 7,
                  10, 11, 14, 15 };
    int len = arr.length;

    removePrimes(arr, len);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
sz = 10**5
isPrime = [True for i in range(sz + 1)]

# Function for Sieve of Eratosthenes
def sieve():

    isPrime[0] = isPrime[1] = False

    i = 2
    while i * i < sz:
        if (isPrime[i]):
            for j in range(i * i, sz, i):
                isPrime[j] = False
        i += 1

# Function to pr the elements of the array
def prArray(arr, lenn):
    for i in range(lenn):
        print(arr[i], end = " ")

# Function to remove all the prime numbers
def removePrimes(arr, lenn):

    # Generate primes
    sieve()

    # Traverse the array
    i = 0
    while i < lenn:

        # If the current element is prime
        if (isPrime[arr[i]]):

            # Shift all the elements on the
            # right of it to the left
            for j in range(i, lenn - 1):
                arr[j] = arr[j + 1]

            # Decrease the loop counter by 1
            # to check the shifted element
            i -= 1

            # Decrease the length
            lenn -= 1

        i += 1

    # Pr the updated array
    prArray(arr, lenn)

# Driver code
if __name__ == '__main__':
    arr = [4, 6, 5, 3, 8, 7, 10, 11, 14, 15]
    lenn = len(arr)

    removePrimes(arr, lenn)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int sz = (int) 1e5;
static bool []isPrime = new bool[sz + 1];

// Function for Sieve of Eratosthenes
static void sieve()
{
    for (int i = 0; i < sz + 1; i++)
        isPrime[i] = true;

    isPrime[0] = isPrime[1] = false;

    for (int i = 2; i * i <= sz; i++)
    {
        if (isPrime[i])
        {
            for (int j = i * i;
                     j < sz; j += i)
            {
                isPrime[j] = false;
            }
        }
    }
}

// Function to print the elements
// of the array
static void printArray(int []arr,
                       int len)
{
    for (int i = 0; i < len; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Function to remove
// all the prime numbers
static void removePrimes(int []arr,
                         int len)
{
    // Generate primes
    sieve();

    // Traverse the array
    for (int i = 0; i < len; i++)
    {

        // If the current element is prime
        if (isPrime[arr[i]])
        {

            // Shift all the elements on the
            // right of it to the left
            for (int j = i; j < len - 1; j++)
            {
                arr[j] = arr[j + 1];
            }

            // Decrease the loop counter by 1
            // to check the shifted element
            i--;

            // Decrease the length
            len--;
        }
    }

    // Print the updated array
    printArray(arr, len);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 6, 5, 3, 8, 7,
                 10, 11, 14, 15 };
    int len = arr.Length;

    removePrimes(arr, len);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
const sz = 1e5;
let isPrime = new Array(sz + 1);

// Function for Sieve of Eratosthenes
function sieve()
{
    isPrime.fill(true)
    isPrime[0] = isPrime[1] = false;

    for(let i = 2; i * i <= sz; i++)
    {
        if (isPrime[i])
        {
            for(let j = i * i; j < sz; j += i)
            {
                isPrime[j] = false;
            }
        }
    }
}

// Function to print the elements of the array
function printArray(arr, len)
{
    for(let i = 0; i < len; i++)
    {
        document.write(arr[i] + ' ');
    }
}

// Function to remove all the prime numbers
function removePrimes(arr, len)
{

    // Generate primes
    sieve();

    // Traverse the array
    for(let i = 0; i < len; i++)
    {

        // If the current element is prime
        if (isPrime[arr[i]])
        {

            // Shift all the elements on the
            // right of it to the left
            for(let j = i; j < len; j++)
            {
                arr[j] = arr[j + 1];
            }

            // Decrease the loop counter by 1
            // to check the shifted element
            i--;

            // Decrease the length
            len--;
        }
    }

    // Print the updated array
    printArray(arr, len);
}

// Driver code
let arr = [ 4, 6, 5, 3, 8, 7,
            10, 11, 14, 15 ];
let len = arr.length;

removePrimes(arr, len);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
4 6 8 10 14 15
```