# 具有最大可能 GCD 的大小为 k 的子序列

> 原文:[https://www . geesforgeks . org/subsequence-of-size-k-with-maximum-gcd/](https://www.geeksforgeeks.org/subsequence-of-size-k-with-maximum-possible-gcd/)

给我们一个正整数数组和一个整数 k，求大小为 k 的子序列的最大可能 GCD。

**示例:**

```
Input : arr[] = [2, 1, 4, 6] k = 3
Output : 2
GCD of [2, 4, 6] is 2

Input : arr[] = [1, 2, 3] k = 3
Output : 1
GCD of [1, 2, 3] is 1 
```

**方法 1** 逐个生成大小为 k 的所有子序列，然后找到所有这样生成的子序列的 GCD。打印找到的最大的 GCD。

**方法 2** 在这个方法中，我们维护一个计数数组来存储每个元素的除数。我们将遍历给定的数组，对于每个元素，我们将在计数数组的索引处计算它的除数和增量。计算除数的过程将花费 O(sqrt(arr[i]))时间，其中 arr[i]是索引 I 处给定数组中的元素。在整个遍历之后，我们可以简单地遍历计数数组，从最后一个索引到索引 1。如果我们找到一个值等于或大于 k 的索引，那么这意味着它是至少 k 个元素的除数，也是最大 GCD。

## C++

```
// CPP program to find subsequence of size
// k with maximum possible GCD.
#include <bits/stdc++.h>
using namespace std;

// function to find GCD of sub sequence of
// size k with max GCD in the array
int findMaxGCD(int arr[], int n, int k)
{
    // Computing highest element
    int high = *max_element(arr, arr+n);

    // Array to store the count of divisors
    // i.e. Potential GCDs
    int divisors[high + 1] = { 0 };

    // Iterating over every element
    for (int i = 0; i < n; i++) {

        // Calculating all the divisors
        for (int j = 1; j <= sqrt(arr[i]); j++) {

            // Divisor found
            if (arr[i] % j == 0) {

                // Incrementing count for divisor
                divisors[j]++;

                // Element/divisor is also a divisor
                // Checking if both divisors are
                // not same
                if (j != arr[i] / j)
                    divisors[arr[i] / j]++;
            }
        }
    }

    // Checking the highest potential GCD
    for (int i = high; i >= 1; i--)

        // If this divisor can divide at least k
        // numbers, it is a GCD of at least one
        // sub sequence of size k
        if (divisors[i] >= k)
            return i;
}

// Driver code
int main()
{
    // Array in which sub sequence with size
    // k with max GCD is to be found
    int arr[] = { 1, 2, 4, 8, 8, 12 };
    int k = 3;

    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findMaxGCD(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// subsequence of size
// k with maximum possible GCD
import java .io.*;
import java .util.*;

class GFG
{

// function to find GCD of
// sub sequence of size k
// with max GCD in the array
static int findMaxGCD(int []arr,
                      int n, int k)
{
    Arrays.sort(arr);

    // Computing highest element
    int high = arr[n - 1];

    // Array to store the
    // count of divisors
    // i.e. Potential GCDs
    int []divisors = new int[high + 1];

    // Iterating over
    // every element
    for (int i = 0; i < n; i++)
    {

        // Calculating all the divisors
        for (int j = 1;            
                 j <= Math.sqrt(arr[i]);
                 j++)
        {

            // Divisor found
            if (arr[i] % j == 0)
            {

                // Incrementing count
                // for divisor
                divisors[j]++;

                // Element/divisor is
                // also a divisor Checking
                // if both divisors are
                // not same
                if (j != arr[i] / j)
                    divisors[arr[i] / j]++;
            }
        }
    }

    // Checking the highest
    // potential GCD
    for (int i = high; i >= 1; i--)

        // If this divisor can divide
        // at least k numbers, it is
        // a GCD of at least one sub
        // sequence of size k
        if (divisors[i] >= k)
            return i;
            return 0 ;
}

// Driver code
static public void main (String[] args)
{
    // Array in which sub sequence
    // with size k with max GCD is
    // to be found
    int []arr = { 1, 2, 4,
                  8, 8, 12 };
    int k = 3;

    int n = arr.length;
    System.out.println(findMaxGCD(arr, n, k));
}
}

// This code is contributed
// by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to find subsequence
# of size k with maximum possible GCD.
import math

# function to find GCD of sub sequence
# of size k with max GCD in the array
def findMaxGCD(arr, n, k):

    # Computing highest element
    high = max(arr)

    # Array to store the count of
    # divisors i.e. Potential GCDs
    divisors = [0] * (high + 1)

    # Iterating over every element
    for i in range(n) :

        # Calculating all the divisors
        for j in range(1, int(math.sqrt(arr[i])) + 1):

            # Divisor found
            if (arr[i] % j == 0) :

                # Incrementing count for divisor
                divisors[j] += 1

                # Element/divisor is also a divisor
                # Checking if both divisors are
                # not same
                if (j != arr[i] // j):
                    divisors[arr[i] // j] += 1

    # Checking the highest potential GCD
    for i in range(high, 0, -1):

        # If this divisor can divide at least k
        # numbers, it is a GCD of at least one
        # sub sequence of size k
        if (divisors[i] >= k):
            return i

# Driver code
if __name__ == "__main__":

    # Array in which sub sequence with size
    # k with max GCD is to be found
    arr = [ 1, 2, 4, 8, 8, 12 ]
    k = 3

    n = len(arr)
    print(findMaxGCD(arr, n, k))

# This code is contributed by ita_c
```

## C#

```
// C# program to find subsequence of size
// k with maximum possible GCD
using System;
using System.Linq;

public class GFG {

    // function to find GCD of sub sequence of
    // size k with max GCD in the array
    static int findMaxGCD(int []arr, int n, int k)
    {
        // Computing highest element
        int high = arr.Max();

        // Array to store the count of divisors
        // i.e. Potential GCDs
        int []divisors = new int[high+1];

        // Iterating over every element
        for (int i = 0; i < n; i++) {

            // Calculating all the divisors
            for (int j = 1; j <= Math.Sqrt(arr[i]); j++)
            {

                // Divisor found
                if (arr[i] % j == 0) {

                    // Incrementing count for divisor
                    divisors[j]++;

                    // Element/divisor is also a divisor
                    // Checking if both divisors are
                    // not same
                    if (j != arr[i] / j)
                        divisors[arr[i] / j]++;
                }
            }
        }

        // Checking the highest potential GCD
        for (int i = high; i >= 1; i--)

            // If this divisor can divide at least k
            // numbers, it is a GCD of at least one
            // sub sequence of size k
            if (divisors[i] >= k)
                return i;
                return 0 ;
    }

    // Driver code
    static public void Main ()
    {
        // Array in which sub sequence with
        // size k with max GCD is to be found
        int []arr = { 1, 2, 4, 8, 8, 12 };
        int k = 3;

        int n = arr.Length;
        Console.WriteLine(findMaxGCD(arr, n, k));
    }
}

// This code is contributed by anuj_67.
```

## java 描述语言

```
<script>
// Javascript program to find
// subsequence of size
// k with maximum possible GCD

    // function to find GCD of
// sub sequence of size k
// with max GCD in the array
    function findMaxGCD(arr,n,k)
    {
        arr.sort(function(a,b){return a-b;});

    // Computing highest element
    let high = arr[n - 1];

    // Array to store the
    // count of divisors
    // i.e. Potential GCDs
    let divisors = new Array(high + 1);
    for(let i=0;i<divisors.length;i++)
    {
        divisors[i]=0;
    }

    // Iterating over
    // every element
    for (let i = 0; i < n; i++)
    {

        // Calculating all the divisors
        for (let j = 1;            
                 j <= Math.sqrt(arr[i]);
                 j++)
        {

            // Divisor found
            if (arr[i] % j == 0)
            {

                // Incrementing count
                // for divisor
                divisors[j]++;

                // Element/divisor is
                // also a divisor Checking
                // if both divisors are
                // not same
                if (j != Math.floor(arr[i] / j))
                    divisors[Math.floor(arr[i] / j)]++;
            }
        }
    }

    // Checking the highest
    // potential GCD
    for (let i = high; i >= 1; i--)

        // If this divisor can divide
        // at least k numbers, it is
        // a GCD of at least one sub
        // sequence of size k
        if (divisors[i] >= k)
            return i;
            return 0 ;
    }

    // Driver code
    let arr=[1, 2, 4,
                  8, 8, 12];
    let k = 3;
    let n = arr.length;
    document.write(findMaxGCD(arr, n, k));

    // This code is contributed by rag2127
</script>
```

**Output:** 

```
4
```