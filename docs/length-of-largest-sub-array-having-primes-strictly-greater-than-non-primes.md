# 素数严格大于非素数的最大子阵列的长度

> 原文:[https://www . geeksforgeeks . org/最大子数组长度-有素数-严格来说-大于非素数/](https://www.geeksforgeeks.org/length-of-largest-sub-array-having-primes-strictly-greater-than-non-primes/)

给定长度为“n”的数组“arr”。任务是找到素数计数严格大于非素数计数的最大连续子阵列。
**例** :

```
Input: arr[] = {4, 7, 4, 7, 11, 5, 4, 4, 4, 5}
Output: 9

Input:  arr[] = { 1, 9, 3, 4, 5, 6, 7, 8 }
Output: 5
```

**逼近:**求素数个数严格大于非素数个数的最大子阵:
首先用筛子求素数。
将数组中所有素数替换为 1，所有非素数替换为-1。现在这个问题类似于[最长子阵列，1 的计数比 0 的计数多 1](https://www.geeksforgeeks.org/longest-subarray-count-1s-one-count-0s/)
下面是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

bool prime[1000000 + 5];

void findPrime()
{
    memset(prime, true, sizeof(prime));
    prime[1] = false;

    for (int p = 2; p * p <= 1000000; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (int i = p * 2; i <= 1000000; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the length of longest
// subarray having count of primes more
// than count of non-primes
int lenOfLongSubarr(int arr[], int n)
{
    // unordered_map 'um' implemented as
    // hash table
    unordered_map<int, int> um;
    int sum = 0, maxLen = 0;

    // traverse the given array
    for (int i = 0; i < n; i++) {

        // consider -1 as non primes and 1 as primes
        sum += prime[arr[i]] == 0 ? -1 : 1;

        // when subarray starts form index '0'
        if (sum == 1)
            maxLen = i + 1;

        // make an entry for 'sum' if it is
        // not present in 'um'
        else if (um.find(sum) == um.end())
            um[sum] = i;

        // check if 'sum-1' is present in 'um'
        // or not
        if (um.find(sum - 1) != um.end()) {

            // update maxLength
            if (maxLen < (i - um[sum - 1]))
                maxLen = i - um[sum - 1];
        }
    }

    // required maximum length
    return maxLen;
}

// Driver code
int main()
{
    findPrime();

    int arr[] = { 1, 9, 3, 4, 5, 6, 7, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << lenOfLongSubarr(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

import java.util.*;
class GfG {
    static boolean prime[] = new boolean[1000000 + 5];

    static void findPrime()
    {
        Arrays.fill(prime, true);
        prime[1] = false;

        for (int p = 2; p * p <= 1000000; p++) {

            // If prime[p] is not changed, then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= 1000000; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to find the length of longest
    // subarray having count of primes more
    // than count of non-primes
    static int lenOfLongSubarr(int arr[], int n)
    {
        // unordered_map 'um' implemented as
        // hash table
        Map<Integer, Integer> um = new HashMap<Integer, Integer>();
        int sum = 0, maxLen = 0;

        // traverse the given array
        for (int i = 0; i < n; i++) {

            // consider -1 as non primes and 1 as primes
            sum += prime[arr[i]] == false ? -1 : 1;

            // when subarray starts form index '0'
            if (sum == 1)
                maxLen = i + 1;

            // make an entry for 'sum' if it is
            // not present in 'um'
            else if (!um.containsKey(sum))
                um.put(sum, i);

            // check if 'sum-1' is present in 'um'
            // or not
            if (um.containsKey(sum - 1)) {

                // update maxLength
                if (maxLen < (i - um.get(sum - 1)))
                    maxLen = i - um.get(sum - 1);
            }
        }

        // required maximum length
        return maxLen;
    }

    // Driver code
    public static void main(String[] args)
    {
        findPrime();

        int arr[] = { 1, 9, 3, 4, 5, 6, 7, 8 };
        int n = arr.length;

        System.out.println(lenOfLongSubarr(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach

prime = [True] * (1000000 + 5)

def findPrime():

    prime[0], prime[1] = False, False

    for p in range(2, 1001):

        # If prime[p] is not changed,
        # then it is a prime
        if prime[p] == True:

            # Update all multiples of p
            for i in range(p * 2, 1000001, p):
                prime[i] = False

# Function to find the length of longest
# subarray having count of primes more
# than count of non-primes
def lenOfLongSubarr(arr, n):

    # unordered_map 'um' implemented as
    # hash table
    um = {}
    Sum, maxLen = 0, 0

    # traverse the given array
    for i in range(0, n):

        # consider -1 as non primes and 1 as primes
        Sum = Sum-1 if prime[arr[i]] == False else Sum + 1

        # when subarray starts form index '0'
        if Sum == 1:
            maxLen = i + 1

        # make an entry for 'sum' if
        # it is not present in 'um'
        elif Sum not in um:
            um[Sum] = i

        # check if 'sum-1' is present
        # in 'um' or not
        if (Sum - 1) in um:

            # update maxLength
            if maxLen < (i - um[Sum - 1]):
                maxLen = i - um[Sum - 1]

    # required maximum length
    return maxLen

# Driver Code
if __name__ == "__main__":

    findPrime()

    arr = [1, 9, 3, 4, 5, 6, 7, 8]
    n = len(arr)

    print(lenOfLongSubarr(arr, n))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;

class GfG {

    static bool[] prime = new bool[1000000 + 5];

    static void findPrime()
    {
        Array.Fill(prime, true);
        prime[1] = false;

        for (int p = 2; p * p <= 1000000; p++) {

            // If prime[p] is not changed,
            // then it is a prime
            if (prime[p] == true) {

                // Update all multiples of p
                for (int i = p * 2; i <= 1000000; i += p)
                    prime[i] = false;
            }
        }
    }

    // Function to find the length of longest
    // subarray having count of primes more
    // than count of non-primes
    static int lenOfLongSubarr(int[] arr, int n)
    {
        // unordered_map 'um' implemented as
        // hash table
        Dictionary<int, int> um = new Dictionary<int, int>();
        int sum = 0, maxLen = 0;

        // traverse the given array
        for (int i = 0; i < n; i++) {

            // consider -1 as non primes and 1 as primes
            sum += prime[arr[i]] == false ? -1 : 1;

            // when subarray starts form index '0'
            if (sum == 1)
                maxLen = i + 1;

            // make an entry for 'sum' if it is
            // not present in 'um'
            else if (!um.ContainsKey(sum))
                um[sum] = i;

            // check if 'sum-1' is present in 'um'
            // or not
            if (um.ContainsKey(sum - 1)) {

                // update maxLength
                if (maxLen < (i - um[sum - 1]))
                    maxLen = i - um[sum - 1];
            }
        }

        // required maximum length
        return maxLen;
    }

    // Driver code
    public static void Main()
    {
        findPrime();

        int[] arr = { 1, 9, 3, 4, 5, 6, 7, 8 };
        int n = arr.Length;

        Console.WriteLine(lenOfLongSubarr(arr, n));
    }
}

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

let prime = new Array(1000000 + 5);

function findPrime() {
    prime.fill(true)
    prime[1] = false;

    for (let p = 2; p * p <= 1000000; p++) {

        // If prime[p] is not changed, then it is a prime
        if (prime[p] == true) {

            // Update all multiples of p
            for (let i = p * 2; i <= 1000000; i += p)
                prime[i] = false;
        }
    }
}

// Function to find the length of longest
// subarray having count of primes more
// than count of non-primes
function lenOfLongSubarr(arr, n) {
    // unordered_map 'um' implemented as
    // hash table
    let um = new Map();
    let sum = 0, maxLen = 0;

    // traverse the given array
    for (let i = 0; i < n; i++) {

        // consider -1 as non primes and 1 as primes
        sum += prime[arr[i]] == 0 ? -1 : 1;

        // when subarray starts form index '0'
        if (sum == 1)
            maxLen = i + 1;

        // make an entry for 'sum' if it is
        // not present in 'um'
        else if (!um.has(sum))
            um.set(sum, i);

        // check if 'sum-1' is present in 'um'
        // or not
        if (um.has(sum - 1)) {

            // update maxLength
            if (maxLen < (i - um.get(sum - 1)))
                maxLen = i - um.get(sum - 1);
        }
    }

    // required maximum length
    return maxLen;
}

// Driver code

findPrime();
let arr = [1, 9, 3, 4, 5, 6, 7, 8];
let n = arr.length;
document.write(lenOfLongSubarr(arr, n) + "<br>")

// This code is contributed by Saurabh Jaiswal
</script>
```

**Output:** 

```
5
```