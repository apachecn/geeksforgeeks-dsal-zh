# 按降序排列数组的素数

> 原文:[https://www . geeksforgeeks . org/sort-质数数组降序排列/](https://www.geeksforgeeks.org/sort-prime-numbers-of-an-array-in-descending-order/)

给定一个整数数组“arr”，任务是按相对位置降序排列数组中的所有素数，即其他元素的其他位置不得受到影响。
**例:**

```
Input: arr[] = {2, 5, 8, 4, 3}
Output: 5 3 8 4 2

Input: arr[] = {10, 12, 2, 6, 5}
Output: 10 12 5 6 2
```

**进场:**

*   创建一个筛子来检查一个元素在 O(1)中是否是质数。
*   遍历数组，检查数字是否是质数。如果它是质数，把它储存在向量中。
*   然后，按降序对向量进行排序。
*   再次遍历数组，用向量元素逐个替换质数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

bool prime[100005];

void SieveOfEratosthenes(int n)
{

    memset(prime, true, sizeof(prime));

    // false here indicates
    // that it is not prime
    prime[1] = false;

    for (int p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (int i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function that sorts
// all the prime numbers
// from the array in descending
void sortPrimes(int arr[], int n)
{
    SieveOfEratosthenes(100005);

    // this vector will contain
    // prime numbers to sort
    vector<int> v;

    for (int i = 0; i < n; i++) {

        // if the element is prime
        if (prime[arr[i]])
            v.push_back(arr[i]);
    }

    sort(v.begin(), v.end(), greater<int>());

    int j = 0;

    // update the array elements
    for (int i = 0; i < n; i++) {
        if (prime[arr[i]])
            arr[i] = v[j++];
    }
}

// Driver code
int main()
{

    int arr[] = { 4, 3, 2, 6, 100, 17 };
    int n = sizeof(arr) / sizeof(arr[0]);

    sortPrimes(arr, n);

    // print the results.
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    static boolean prime[] = new boolean[100005];

    static void SieveOfEratosthenes(int n)
    {

        Arrays.fill(prime, true);

        // false here indicates
        // that it is not prime
        prime[1] = false;

        for (int p = 2; p * p <= n; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p]) {

                // Update all multiples of p,
                // set them to non-prime
                for (int i = p * 2; i < n; i += p)
                {
                    prime[i] = false;
                }
            }
        }
    }

    // Function that sorts
    // all the prime numbers
    // from the array in descending
    static void sortPrimes(int arr[], int n)
    {
        SieveOfEratosthenes(100005);

        // this vector will contain
        // prime numbers to sort
        Vector<Integer> v = new Vector<Integer>();

        for (int i = 0; i < n; i++)
        {

            // if the element is prime
            if (prime[arr[i]])
            {
                v.add(arr[i]);
            }
        }
        Comparator comparator = Collections.reverseOrder();
        Collections.sort(v, comparator);

        int j = 0;

        // update the array elements
        for (int i = 0; i < n; i++)
        {
            if (prime[arr[i]])
            {
                arr[i] = v.get(j++);
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {4, 3, 2, 6, 100, 17};
        int n = arr.length;

        sortPrimes(arr, n);

        // print the results.
        for (int i = 0; i < n; i++)
        {
            System.out.print(arr[i] + " ");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

def SieveOfEratosthenes(n):

    # false here indicates
    # that it is not prime
    prime[1] = False
    p = 2
    while p * p <= n:

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p]:

            # Update all multiples of p,
            # set them to non-prime
            for i in range(p * 2, n + 1, p):
                prime[i] = False

        p += 1

# Function that sorts all the prime
# numbers from the array in descending
def sortPrimes(arr, n):

    SieveOfEratosthenes(100005)

    # This vector will contain
    # prime numbers to sort
    v = []
    for i in range(0, n):

        # If the element is prime
        if prime[arr[i]]:
            v.append(arr[i])

    v.sort(reverse = True)
    j = 0

    # update the array elements
    for i in range(0, n):
        if prime[arr[i]]:
            arr[i] = v[j]
            j += 1

    return arr

# Driver code
if __name__ == "__main__":

    arr = [4, 3, 2, 6, 100, 17]
    n = len(arr)

    prime = [True] * 100006
    arr = sortPrimes(arr, n)

    # print the results.
    for i in range(0, n):
        print(arr[i], end = " ")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    static bool []prime = new bool[100005];

    static void SieveOfEratosthenes(int n)
    {

        for(int i = 0; i < 100005; i++)
            prime[i] = true;

        // false here indicates
        // that it is not prime
        prime[1] = false;

        for (int p = 2; p * p <= n; p++)
        {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p])
            {

                // Update all multiples of p,
                // set them to non-prime
                for (int i = p * 2; i < n; i += p)
                {
                    prime[i] = false;
                }
            }
        }
    }

    // Function that sorts
    // all the prime numbers
    // from the array in descending
    static void sortPrimes(int []arr, int n)
    {
        SieveOfEratosthenes(100005);

        // this vector will contain
        // prime numbers to sort
        List<int> v = new List<int>();

        for (int i = 0; i < n; i++)
        {

            // if the element is prime
            if (prime[arr[i]])
            {
                v.Add(arr[i]);
            }
        }
        v.Sort();
        v.Reverse();

        int j = 0;

        // update the array elements
        for (int i = 0; i < n; i++)
        {
            if (prime[arr[i]])
            {
                arr[i] = v[j++];
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {4, 3, 2, 6, 100, 17};
        int n = arr.Length;

        sortPrimes(arr, n);

        // print the results.
        for (int i = 0; i < n; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var prime = Array(100005).fill(true);

function SieveOfEratosthenes( n)
{

    // false here indicates
    // that it is not prime
    prime[1] = false;

    for (var p = 2; p * p <= n; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p]) {

            // Update all multiples of p,
            // set them to non-prime
            for (var i = p * 2; i <= n; i += p)
                prime[i] = false;
        }
    }
}

// Function that sorts
// all the prime numbers
// from the array in descending
function sortPrimes(arr, n)
{
    SieveOfEratosthenes(100005);

    // this vector will contain
    // prime numbers to sort
    var v = [];

    for (var i = 0; i < n; i++) {

        // if the element is prime
        if (prime[arr[i]])
            v.push(arr[i]);
    }

    v.sort((a,b)=>b-a)

    var j = 0;

    // update the array elements
    for (var i = 0; i < n; i++) {
        if (prime[arr[i]])
            arr[i] = v[j++];
    }
}

// Driver code
var arr = [4, 3, 2, 6, 100, 17 ];
var n = arr.length;
sortPrimes(arr, n);
// print the results.
for (var i = 0; i < n; i++) {
    document.write( arr[i] + " ");
}

</script>
```

**Output:** 

```
4 17 3 6 100 2
```