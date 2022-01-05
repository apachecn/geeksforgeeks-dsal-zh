# 仅按递增顺序对数组中的非质数进行排序

> 原文:[https://www . geesforgeks . org/sort-only-non-prime-numbers-of-a-array-in-递增顺序/](https://www.geeksforgeeks.org/sort-only-non-prime-numbers-of-an-array-in-increasing-order/)

给定一组 **N 个**整数。任务是打印排序后的数组，使得所有的**质数**都停留在同一个地方，只排序**非质数**的数字。
**示例** :

```
Input : arr[] = {10, 7, 6}
Output : 6 7 10

Input : arr[] = {100, 11, 500, 2, 17, 1}
Output : 1 11 100 2 17 500
```

**进场:**

*   遍历数组，取出所有非质数并存储在向量中。
*   现在，对向量进行排序。
*   然后，再次遍历数组，检查一个数字是否是质数，如果是，则按原样打印。否则，从向量中打印一个数字。

为了检查一个数是否是质数，我们可以使用[筛除](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)。
以下是上述办法的实施:

## C++

```
// C++ program to sort only non primes
#include <bits/stdc++.h>
using namespace std;

// Create a boolean array "prime[0..n]" and initialize
// all entries it as true. A value in prime[i] will
// finally be false if i is Not a prime, else true.
bool prime[100005];

void SieveOfEratosthenes(int n)
{

    memset(prime, true, sizeof(prime));

    prime[1] = false;

    for (int p = 2; p * p <= n; p++) {
        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {
            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to print the array such that
// only non primes are sorted
void sortedArray(int arr[], int n)
{
    SieveOfEratosthenes(100005);

    // vector v will store all non
    // prime numbers
    std::vector<int> v;

    // If not prime, insert into vector
    for (int i = 0; i < n; ++i) {
        if (prime[arr[i]] == 0)
            v.push_back(arr[i]);
    }

    // sorting vector of non primes
    sort(v.begin(), v.end());

    int j = 0;
    // print the required array
    for (int i = 0; i < n; ++i) {
        if (prime[arr[i]] == true)
            cout << arr[i] << " ";
        else {
            cout << v[j] << " ";
            j++;
        }
    }
}

// Driver Code
int main()
{

    int n = 6;
    int arr[] = { 100, 11, 500, 2, 17, 1 };

    sortedArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```

// Java program to sort only non primes
import java.util.*;
class solution
{
// Create a boolean array "prime[0..n]" and initialize
// all entries it as true. A value in prime[i] will
// finally be false if i is Not a prime, else true.
static boolean prime[] = new boolean[100006];

static void SieveOfEratosthenes(int n)
{

    for(int i=1;i<=n;i++)
    prime[i]=true;
    prime[1] = false;

    for (int p = 2; p * p <= n; p++) {
        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {
            // Update all multiples of p
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to print the array such that
// only non primes are sorted
static void sortedArray(int arr[], int n)
{
    SieveOfEratosthenes(100005);

    // vector v will store all non
    // prime numbers
    Vector<Integer> v = new Vector<Integer>();

    // If not prime, insert into vector
    for (int i = 0; i < n; ++i) {
        if (prime[arr[i]]==false)
            v.add(arr[i]);
    }

    // sorting vector of non primes
    Collections.sort(v);

    int j = 0;
    // print the required array
    for (int i = 0; i < n; ++i) {
        if (prime[arr[i]] == true)
            System.out.print( arr[i] + " ");
        else {
            System.out.print( v.get(j) + " ");
            j++;
        }
    }
}

// Driver Code
public static void main(String args[])
{

    int n = 6;
    int arr[] = { 100, 11, 500, 2, 17, 1 };

    sortedArray(arr, n);

}
}
//contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to sort only
# non primes

# from math import sqrt method
from math import sqrt

# Create a boolean array "prime[0..n]"
# and initialize all entries it as true.
# A value in prime[i] will  finally be false
# if i is Not a prime, else true.
prime = [0] * 100005

def SieveOfEratosthenes(n) :

    for i in range(len(prime)) :
        prime[i] = True

    prime[1] = False

    for p in range(2, int(sqrt(n)) + 1) :

        # If prime[p] is not changed,
        # then it is a prime    
        if prime[p] == True :

            # Update all multiples of p
            for i in range(p * 2, n, p) :
                prime[i] = False

# Function to print the array such that
# only non primes are sorted
def sortedArray(arr, n) :

    SieveOfEratosthenes(100005)

    # list v will store all non
    # prime numbers
    v = []

    # If not prime, insert into list
    for i in range(n) :
        if prime[arr[i]] == 0 :
            v.append(arr[i])

    # sorting list of non primes
    v.sort()

    j = 0

    # print the required array
    for i in range(n) :

        if prime[arr[i]] == True :
            print(arr[i],end = " ")
        else :
            print(v[j],end = " ")
            j += 1

# Driver code
if __name__ == "__main__" :

    n = 6
    arr = [100, 11, 500, 2, 17, 1]

    sortedArray(arr, n)

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# program to sort only non primes
using System;
using System.Collections.Generic;

class GFG
{
    // Create a boolean array "prime[0..n]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally be
    // false if i is Not a prime, else true.
    static bool []prime = new bool[100006];

    static void SieveOfEratosthenes(int n)
    {

        for(int i = 1; i <= n; i++)
        prime[i] = true;
        prime[1] = false;

        for (int p = 2; p * p <= n; p++)
        {
            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true)
            {
                // Update all multiples of p
                for (int i = p * 2; i <= n; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to print the array such that
    // only non primes are sorted
    static void sortedArray(int []arr, int n)
    {
        SieveOfEratosthenes(100005);

        // vector v will store all non
        // prime numbers
        List<int> v = new List<int>();

        // If not prime, insert into vector
        for (int i = 0; i < n; ++i)
        {
            if (prime[arr[i]] == false)
                v.Add(arr[i]);
        }

        // sorting vector of non primes
        v.Sort();

        int j = 0;
        // print the required array
        for (int i = 0; i < n; ++i)
        {
            if (prime[arr[i]] == true)
                Console.Write( arr[i] + " ");
            else
            {
                Console.Write( v[j] + " ");
                j++;
            }
        }
    }

    // Driver Code
    public static void Main()
    {

        int n = 6;
        int []arr = { 100, 11, 500, 2, 17, 1 };

        sortedArray(arr, n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to sort only non primes

// Create a boolean array "prime[0..n]" and initialize
// all entries it as true. A value in prime[i] will
// finally be false if i is Not a prime, else true.
prime = new Array(100005);

function SieveOfEratosthenes( n)
{

    prime.fill(true);

    prime[1] = false;

    for (var p = 2; p * p <= n; p++) {
        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {
            // Update all multiples of p
            for (var i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function to print the array such that
// only non primes are sorted
function sortedArray(arr, n)
{
    SieveOfEratosthenes(100005);

    // vector v will store all non
    // prime numbers
    var v = [];

    // If not prime, insert into vector
    for (var i = 0; i < n; ++i) {
        if (prime[arr[i]] == 0)
            v.push(arr[i]);
    }

    // sorting vector of non primes
    v.sort();

    var j = 0;
    // print the required array
    for (var i = 0; i < n; ++i) {
        if (prime[arr[i]] == true)
            document.write( arr[i] + " ");
        else {
            document.write( v[j] + " ");
            j++;
        }
    }
}
var n = 6;
var arr = [ 100, 11, 500, 2, 17, 1 ];
sortedArray(arr, n);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
1 11 100 2 17 500
```

**时间复杂度:** ![O(Nlog(N))  ](img/11800cd73564bc1f3de848efdee4308e.png "Rendered by QuickLaTeX.com")