# 根据不同质因数的递增计数对数组进行排序

> 原文:[https://www . geeksforgeeks . org/按不同质因数的递增计数对数组进行排序/](https://www.geeksforgeeks.org/sort-an-array-according-to-the-increasing-count-of-distinct-prime-factors/)

给定一个整数数组。任务是根据不同质因数的递增计数对给定数组进行排序。
**例:**

```
Input : arr[] = {30, 2, 1024, 210, 3, 6}
Output : 2 1024 3 6 30 210 

Input : arr[] = {12, 16, 27, 6}
Output : 16 27 6 12
```

一种**简单的方法**是[找到数组中每个元素](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的所有素因子，并将素因子的计数与向量中的元素配对，并根据素因子的计数对数组进行排序。

一个有效的方法是使用一个 T2 筛来寻找不同质因数的计数并将其存储在一个向量中。现在，遍历数组，将不同质因数的计数与向量中的元素配对，并使用[比较器函数](https://www.geeksforgeeks.org/comparator-function-of-qsort-in-c/)根据质因数的计数对数组进行排序。

下面是该方法的实现:

## C++

```
// C++ program to sort array according to the
// count of distinct prime factors
#include <bits/stdc++.h>
using namespace std;

// array to store the count of distinct prime
int prime[100001];

void SieveOfEratosthenes()
{
    // Create a int array "prime[0..n]" and initialize
    // all entries it as 0\. A value in prime[i] will
    // count of distinct prime factors.

    memset(prime, 0, sizeof(prime));

    // 0 and 1 does not have any prime factors
    prime[0] = 0;
    prime[1] = 0;

    for (int p = 2; p * p <= 100001; p++) {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == 0) {
            prime[p]++;

            // Update all multiples of p greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i <= 100001; i += p)
                prime[i]++;
        }
    }
}

// comparator function to sort the vector in
// ascending order of second element of the pair
bool Compare(pair<int, int> p1, pair<int, int> p2)
{
    return (p1.second < p2.second);
}

// Function to sort the array on the
// basis increasing count of distinct
// prime factors
void sortArr(int arr[], int n)
{
    // vector to store the number and
    // count of prime factor
    vector<pair<int, int> > v;

    for (int i = 0; i < n; i++) {
        // push_back the element and
        // count of distinct
        // prime factors
        v.push_back(make_pair(arr[i], prime[arr[i]]));
    }

    // sort the array on the
    // basis increasing count of
    // distinct prime factors
    sort(v.begin(), v.end(), Compare);

    // display the sorted array
    for (int i = 0; i < n; i++)
        cout << v[i].first << " ";

    cout << endl;
}

// Driver code
int main()
{
    // create the sieve
    SieveOfEratosthenes();

    int arr[] = { 30, 2, 1024, 210, 3, 6 };

    int n = sizeof(arr) / sizeof(int);

    sortArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

class GFG
{

    static class Pair implements Comparable<Pair>
    {
        int first, second;

        Pair(int f, int s)
        {
            first = f;
            second = s;
        }

        @Override
        public int compareTo(Pair o)
        {
            if(this.second > o.second)
                return 1;
            else if(this.second == o.second)
                return 0;
            return -1;
        }
    }
    // array to store the count of distinct prime
    static int prime[] = new int[100002];

    static void SieveOfEratosthenes()
    {
        // Create a int array "prime[0..n]" and initialize
        // all entries it as 0\. A value in prime[i] will
        // count of distinct prime factors.
        Arrays.fill(prime, 0);

        // 0 and 1 does not have any prime factors
        prime[0] = 0;
        prime[1] = 0;

        for (int p = 2; p * p <= 100001; p++)
        {
            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == 0)
            {
                prime[p]++;

                // Update all multiples of p greater than or
                // equal to the square of it
                // numbers which are multiple of p and are
                // less than p^2 are already been marked.
                for (int i = p * p; i <= 100001; i += p)
                    prime[i]++;
            }
        }
    }

    // Function to sort the array on the
    // basis increasing count of distinct
    // prime factors
    static void sortArr(int arr[], int n)
    {
        // Array to store the number and
        // count of prime factor
        Pair v[] = new Pair[n];

        for (int i = 0; i < n; i++)
        {
            // update the element and
            // count of distinct
            // prime factors
            v[i] = new Pair(arr[i], prime[arr[i]]);
        }

        // sort the array on the
        // basis increasing count of
        // distinct prime factors
        Arrays.sort(v);

        // display the sorted array
        for (int i = 0; i < n; i++)
            System.out.print(v[i].first + " ");

        System.out.println();
    }

    // Driver code
    public static void main(String args[])
    {
        // create the sieve
        SieveOfEratosthenes();

        int arr[] = { 30, 2, 1024, 210, 3, 6 };

        int n = arr.length;

        sortArr(arr, n);
    }
}

// This code is contributed by ghanshyampandey
```

## 蟒蛇 3

```
# Python3 program to sort array according to the
# count of distinct prime factors
import functools as ft

# array to store the count of distinct prime
prime = [0 for i in range(100001)]

def SieveOfEratosthenes():

    # Create a array "prime[0..n]" and initialize
    # all entries it as 0\. A value in prime[i]
    # will count of distinct prime factors.

    # memset(prime, 0, sizeof(prime))

    # 0 and 1 does not have any prime factors
    prime[0] = 0
    prime[1] = 0

    for p in range(2, 100002):

        if p * p > 100001:
            break

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == 0):
            prime[p] += 1

            # Update all multiples of p greater than
            # or equal to the square of it
            # numbers which are multiple of p and are
            # less than p^2 are already been marked.
            for i in range(2 * p, 100001, p):
                prime[i] += 1

# Function to sort the array on the
# basis increasing count of distinct
# prime factors
def sortArr(arr, n):

    # vector to store the number and
    # count of prime factor
    v = []

    for i in range(n):

        # append the element and
        # count of distinct
        # prime factors
        v.append([arr[i], prime[arr[i]]])

    # sort the array on the
    # basis increasing count of
    # distinct prime factors
    v.sort(key= lambda x:x[1])

    # display the sorted array

    for i in range(n):
        print(v[i][0], end = " ")

    print()

# Driver code

# create the sieve
SieveOfEratosthenes()

arr = [30, 2, 1024, 210, 3, 6]

n = len(arr)

sortArr(arr, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to sort array according to the
// count of distinct prime factors
using System;
using System.Collections.Generic;

class GFG{

public class Pair : IComparable<Pair>
{
    public int first, second;

    public Pair(int f, int s)
    {
        first = f;
        second = s;
    }

    // @Override
    public int CompareTo(Pair o)
    {
        if (this.second > o.second)
            return 1;
        else if (this.second == o.second)
            return 0;

        return -1;
    }
}

// Array to store the count of distinct prime
static int[] prime = new int[100002];

static void SieveOfEratosthenes()
{

    // Create a int array "prime[0..n]"
    // and initialize all entries it as
    // 0\. A value in prime[i] will
    // count of distinct prime factors.
    Array.Fill(prime, 0);

    // 0 and 1 does not have any prime factors
    prime[0] = 0;
    prime[1] = 0;

    for(int p = 2; p * p <= 100001; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == 0)
        {
            prime[p]++;

            // Update all multiples of p greater
            // than or equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for(int i = p * p; i <= 100001; i += p)
                prime[i]++;
        }
    }
}

// Function to sort the array on the
// basis increasing count of distinct
// prime factors
static void sortArr(int[] arr, int n)
{

    // Array to store the number and
    // count of prime factor
    Pair[] v = new Pair[n];

    for(int i = 0; i < n; i++)
    {

        // Update the element and
        // count of distinct
        // prime factors
        v[i] = new Pair(arr[i],
                  prime[arr[i]]);
    }

    // Sort the array on the
    // basis increasing count of
    // distinct prime factors
    Array.Sort(v);

    // Display the sorted array
    for(int i = 0; i < n; i++)
        Console.Write(v[i].first + " ");

    Console.WriteLine();
}

// Driver code
public static void Main(string[] args)
{

    // Create the sieve
    SieveOfEratosthenes();

    int[] arr = { 30, 2, 1024, 210, 3, 6 };
    int n = arr.Length;

    sortArr(arr, n);
}
}

// This code is contributed by grand_master
```

## java 描述语言

```
<script>

   // JavaScript program to sort array according to the
  // count of distinct prime factors

    // array to store the count of distinct prime
    let prime = new Array(100002);

    function SieveOfEratosthenes()
    {
        // Create a int array "prime[0..n]" and initialize
        // all entries it as 0\. A value in prime[i] will
        // count of distinct prime factors.
        for(let i=0;i<prime.length;i++)
        {
            prime[i]=0;
        }

        // 0 and 1 does not have any prime factors
        prime[0] = 0;
        prime[1] = 0;

        for (let p = 2; p * p <= 100001; p++)
        {
            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == 0)
            {
                prime[p]++;

                // Update all multiples of p greater than or
                // equal to the square of it
                // numbers which are multiple of p and are
                // less than p^2 are already been marked.
                for (let i = p * p; i <= 100001; i += p)
                    prime[i]++;
            }
        }
    }

    // Function to sort the array on the
    // basis increasing count of distinct
    // prime factors
    function sortArr(arr,n)
    {
        // Array to store the number and
        // count of prime factor
        let v=[];

        for (let i = 0; i < n; i++)
        {
            // update the element and
            // count of distinct
            // prime factors
            v.push([arr[i], prime[arr[i]]]);

        }

        // sort the array on the
        // basis increasing count of
        // distinct prime factors
        v.sort(function(a,b){return a[1]-b[1];});

        // display the sorted array
        for (let i = 0; i < n; i++)
            document.write(v[i][0] + " ");

        document.write("<br>");
    }

    // Driver code

    // create the sieve
    SieveOfEratosthenes();

    let arr=[30, 2, 1024, 210, 3, 6];
    let n = arr.length;

    sortArr(arr, n);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
2 1024 3 6 30 210
```